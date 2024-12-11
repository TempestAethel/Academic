# Bit Error Rate (BER) Simulation for Rectangular Pulse Shaping in AWGN Channel

## Overview
This simulation models the transmission of binary data over an AWGN (Additive White Gaussian Noise) channel using rectangular pulse shaping. The bit error rate (BER) is calculated for different values of Signal-to-Noise Ratio (SNR) in dB. The results are then plotted to evaluate the performance of the system.

### Step-by-Step Explanation of the Code

### Step 1: Initialize Parameters

```
N=1e6;                         % Number of bits to transmit
SNR_dB=0:2:20;                 % Range of SNR values in dB (from 0 to 20 in steps of 2)
rect_pulse_duration=1;         % Duration of the rectangular pulse (1 sample)
pulse_amplitude=1;             % Amplitude of the rectangular pulse
bits=randi([0,1],1,N);         % Generate random binary data for transmission
tx_signal=zeros(1,N*rect_pulse_duration);  % Initialize the transmitted signal
```
- **N=1e6**: The number of bits to transmit (1 million bits).
- **SNR_dB=0:2:20**: A vector representing the range of SNR values in dB, from 0 to 20 in steps of 2 dB.
- **rect_pulse_duration=1**: Defines the duration of the rectangular pulse in samples.
- **pulse_amplitude=1**: The amplitude of the rectangular pulse (1 unit).
- **bits=randi([0,1],1,N)**: Generates a random binary data stream of `N` bits.

### Step 2: Construct the Transmitted Signal

```
for k=1:N
    if bits(k)==1
        tx_signal((k-1)*rect_pulse_duration+1:k*rect_pulse_duration)=pulse_amplitude;
    end
end
```
- This loop creates the transmitted signal `tx_signal`. If the bit is 1, a rectangular pulse of amplitude `pulse_amplitude` is assigned for the duration of `rect_pulse_duration`.
- The signal is constructed by placing each pulse at the appropriate index for each bit.

### Step 3: Initialize BER Calculation

```
ber=zeros(1,length(SNR_dB));    % Initialize BER array to store results
```
- **ber=zeros(1,length(SNR_dB))**: Initializes an array `ber` to store the bit error rates (BER) for each SNR value.

### Step 4: Simulate Reception and Calculate BER for Different SNR

```
for idx=1:length(SNR_dB)
    snr_linear=10^(SNR_dB(idx)/10);   % Convert SNR from dB to linear scale
    noise_power=pulse_amplitude^2/(2*snr_linear);   % Calculate noise power based on SNR
    noise=sqrt(noise_power)*randn(1,length(tx_signal));   % Generate AWGN noise
    rx_signal=tx_signal+noise;   % Add noise to the transmitted signal
    received_bits=zeros(1,N);    % Initialize received bits array
    
    % Detect received bits
    for k=1:N
        pulse_start=(k-1)*rect_pulse_duration+1;
        pulse_end=k*rect_pulse_duration;
        if sum(rx_signal(pulse_start:pulse_end))>0   % If sum of signal is positive, detect 1
            received_bits(k)=1;
        else
            received_bits(k)=0;   % Otherwise, detect 0
        end
    end
    
    errors=sum(bits~=received_bits);   % Count the number of bit errors
    ber(idx)=errors/N;    % Calculate the bit error rate for this SNR value
end
```
- **snr_linear=10^(SNR_dB(idx)/10)**: Converts the SNR from dB to the linear scale.
- **noise_power**: The noise power is calculated based on the pulse amplitude and the linear SNR.
- **noise=sqrt(noise_power)*randn(1,length(tx_signal))**: Generates Gaussian noise with the calculated noise power.
- **rx_signal=tx_signal+noise**: Adds the generated noise to the transmitted signal to simulate the received signal.
- **received_bits**: This array stores the detected bits. For each pulse, the signal is checked; if the sum is positive, a bit 1 is detected, otherwise, a bit 0 is detected.
- **ber(idx)=errors/N**: The BER for the current SNR value is calculated by dividing the number of errors by the total number of bits `N`.

### Step 5: Plot the BER vs SNR Curve

```
figure;
semilogy(SNR_dB,ber,'o-','LineWidth',2);    % Plot BER on a semilogarithmic scale
xlabel('SNR (dB)');    % Label for the x-axis
ylabel('Bit Error Rate (BER)');    % Label for the y-axis
title('Bit Error Rate vs SNR for Rectangular Pulse Shaping in AWGN Channel');    % Title of the plot
grid on;   % Enable grid on the plot
```
- **semilogy(SNR_dB,ber,'o-','LineWidth',2)**: This plots the BER as a function of SNR using a semi-logarithmic scale (log scale for the y-axis).
- **xlabel('SNR (dB)')** and **ylabel('Bit Error Rate (BER)')**: These labels describe the axes of the plot.
- **grid on**: Enables the grid on the plot for better visibility.

## Conclusion
This script simulates the transmission of binary data with rectangular pulse shaping over an AWGN channel. It calculates the bit error rate (BER) for a range of SNR values and plots the results. The plot illustrates how the BER decreases as the SNR increases, showing the effect of noise on the transmitted signal.
