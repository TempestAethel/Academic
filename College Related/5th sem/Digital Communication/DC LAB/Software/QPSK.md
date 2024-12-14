# QPSK Modulation and Demodulation in MATLAB

## Overview
This script simulates the QPSK (Quadrature Phase Shift Keying) modulation and demodulation process, where binary data is modulated into a signal using both in-phase and quadrature components. The signal is transmitted and then demodulated to recover the original data.

## Step-by-Step Code Explanation

### Step 1: Initialization and Data Setup

```
clc;
clear all;
close all;
data = [0 1 0 1 1 1 0 0 1 1]; 
```
- Clears the workspace and closes all figures.
- Defines the binary data to be transmitted.

### Step 2: Plot the Original Data

```
figure(1)
stem(data, 'linewidth', 3), grid on;
title(' Information before Transmitting ');
axis([0 11 0 1.5]);
```
- Plots the original data (before transmission) using a stem plot for visual representation.

### Step 3: Data Conversion to Non-Zero-Mean Representation (NZR)

```
data_NZR = 2 * data - 1; 
```
- Converts the binary data into a non-zero-mean representation where `0` becomes `-1` and `1` remains `1`.

### Step 4: Reshape the Data for QPSK Modulation

```
s_p_data = reshape(data_NZR, 2, length(data)/2); 
```
- Reshapes the data into pairs of symbols for QPSK modulation. Each pair consists of an in-phase and quadrature component.

### Step 5: Define Modulation Parameters

```
br = 10^6; 
f = br; 
T = 1 / br; 
t = T / 99 : T / 99 : T; 
y = [];
y_in = [];
y_qd = [];
```
- Defines the bit rate (`br`), the frequency (`f`), and the symbol period (`T`).
- Creates a time vector (`t`) to represent the signal over one period.

### Step 6: Modulate the Data

```
for (i = 1 : length(data) / 2)
    y1 = s_p_data(1, i) * cos(2 * pi * f * t); 
    y2 = s_p_data(2, i) * sin(2 * pi * f * t); 
    y_in = [y_in y1];
    y_qd = [y_qd y2]; 
    y = [y y1 + y2]; 
end
Tx_sig = y; 
tt = T / 99 : T / 99 : (T * length(data)) / 2;
```
- Performs QPSK modulation by generating in-phase (`y1`) and quadrature (`y2`) components for each data pair.
- Combines the components to form the modulated signal (`Tx_sig`).

### Step 7: Plot the Modulated Signals

```
figure(2)
subplot(3, 1, 1);
plot(tt, y_in, 'linewidth', 3), grid on;
title('wave form for inphase component in QPSK modulation ');
xlabel('time(sec)'); ylabel(' amplitude(volt) ');
subplot(3, 1, 2);
plot(tt, y_qd, 'linewidth', 3);
grid on;
title('wave form for Quadrature component in QPSK modulation ');
xlabel('time(sec)');
ylabel(' amplitude(volt) ');
subplot(3, 1, 3);
plot(tt, Tx_sig, 'r', 'linewidth', 3), grid on;
title('QPSK modulated signal (sum of inphase and Quadrature phase signal)');
xlabel('time(sec)');
ylabel(' amplitude(volt) ');
```
- Plots the in-phase, quadrature, and combined QPSK modulated signals.

### Step 8: Demodulate the Signal

```
Rx_data = [];
Rx_sig = Tx_sig; 
for (i = 1 : length(data) / 2)
    Z_in = Rx_sig((i - 1) * length(t) + 1 : i * length(t)) .* cos(2 * pi * f * t);
    Z_in_intg = (trapz(t, Z_in)) * (2 / T); 
    if (Z_in_intg > 0) 
        Rx_in_data = 1;
    else
        Rx_in_data = 0;
    end

    Z_qd = Rx_sig((i - 1) * length(t) + 1 : i * length(t)) .* sin(2 * pi * f * t);
    Z_qd_intg = (trapz(t, Z_qd)) * (2 / T); 
    if (Z_qd_intg > 0) 
        Rx_qd_data = 1;
    else
        Rx_qd_data = 0;
    end
    
    Rx_data = [Rx_data Rx_in_data Rx_qd_data];
end
```
Demodulates the received signal (Rx_sig) by integrating the in-phase and quadrature components over time to recover the data.
Step 9: Plot the Received Data
```matlab
figure(3) stem(Rx_data, 'linewidth', 3)
title('Information after Receiving'); 
axis([ 0 11 0 1.5]), grid on;
```

Plots the received data after demodulation to compare it with the original data.

# Conclusion

This MATLAB script demonstrates the basic process of QPSK modulation and demodulation, showing how data is transmitted and recovered through in-phase and quadrature components.
