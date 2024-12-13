# Comparison of Filter Programs

This document compares the four filter programs:
1. **FIR Filters (Low Pass and High Pass)**
2. **Digital IIR Butterworth Filters (Low Pass and High Pass)**

---

## Common Steps Across All Programs

The following initialization and input steps are shared by all filter programs:

```matlab
clc;
clear all;
close all;
rp = input('enter the passband ripple=');
rs = input('enter the stopband ripple=');
fp = input('enter the passband freq='); %wp
fs = input('enter the stopband freq='); %ws
f = input('enter the sampling freq='); %fs
```

### Example Values
- **FIR Filters**:
  - `rp = 0.02`
  - `rs = 0.01`
  - `fp = 1200`
  - `fs = 1700`
  - `f = 9000`
  
- **IIR Filters**:
  - `rp = 3`
  - `rs = 60`
  - `wp = 150`
  - `ws = 300`
  - `fs = 1500`

---

# FIR and IIR Filter Design Steps  

---

## **FIR Filter Design (Low Pass and High Pass)**  

### **Step 1: Calculate Normalized Frequencies**  
Normalized passband (`wp`) and stopband (`ws`) frequencies are calculated as:  
```matlab
wp = 2 * fp / f;  % Normalized passband frequency
ws = 2 * fs / f;  % Normalized stopband frequency
```  

### **Step 2: Determine Filter Order**  
Filter order `n` is determined using ripple values and frequency specifications:  
```matlab
num = -20 * log10(sqrt(rp * rs)) - 13;  % Numerator for order calculation
den = 14.6 * (fs - fp) / f;            % Denominator for order calculation
n = ceil(num / den);                   % Filter order (rounded up)
n1 = n + 1;                            % Adjusted for even order
if (rem(n, 2) ~= 0)                    % Ensure even order
    n1 = n;
    n = n - 1;
end
```  

### **Step 3: Select Window Function**  
Window function (e.g., `boxcar`, `hanning`, `hamming`) is selected:  
```matlab
y = boxcar(n1);  % You can replace 'boxcar' with other window types namely bartlet , hanning and hamming
```  

### **Step 4: Design FIR Filter**  
FIR filter coefficients are computed using the `fir1()` function:  
```matlab
b = fir1(n, wp, 'low', y);  % Use 'high' for High Pass Filter
```  

### **Step 5: Frequency Response Analysis**  
Frequency response is computed and visualized:  
```matlab
[h, q] = freqz(b, 1, 256);           % Compute frequency response
m = 20 * log10(abs(h));              % Convert to decibels
subplot(2, 2, 1);                    % Plot magnitude response
plot(q / pi, m);
xlabel('normalised freq');
ylabel('gain in dB');
title('FIR Filter using specified window');
```  

---

## **IIR Butterworth Filter Design (Low Pass and High Pass)**  

### **Step 1: Calculate Normalized Frequencies**  
Normalized passband (`w1`) and stopband (`w2`) frequencies are calculated:  
```matlab
w1 = 2 * wp / fs;  % Normalized passband frequency
w2 = 2 * ws / fs;  % Normalized stopband frequency
```  

### **Step 2: Determine Filter Order**  
Filter order `n` and cutoff frequency `wn` are computed using `buttord()`:  
```matlab
[n, wn] = buttord(w1, w2, rp, rs);  % Compute order and cutoff frequency
disp('The order of the filter:');
disp(n);
disp('The cutoff frequency of the filter:');
disp(wn);
```  

### **Step 3: Design IIR Filter**  
Filter coefficients are computed using the `butter()` function:  
```matlab
[b, a] = butter(n, wn, 'low');  % Use 'high' for High Pass Filter
```  

### **Step 4: Frequency Response Analysis**  
Frequency response is computed and visualized:  
```matlab
w = 0:0.01:pi;                  % Frequency vector
[h] = freqz(b, a, w);           % Compute frequency response
mag = 20 * log10(abs(h));       % Magnitude response (in dB)
ang = angle(h);                 % Phase response (in radians)
subplot(2, 1, 1);               % Plot magnitude response
plot(w / pi, mag);
xlabel('normalised freq');
ylabel('magnitude');
title('Magnitude Response');
subplot(2, 1, 2);               % Plot phase response
plot(w / pi, ang);
xlabel('normalised freq');
ylabel('angle');
title('Phase Response');
```  
