# 16-QAM Modulation and Demodulation

## Overview
This script simulates the 16-QAM (Quadrature Amplitude Modulation) process, demonstrating both binary-encoded and Gray-encoded QAM. It covers the following:
- Generation of random binary data.
- Modulation using both binary and Gray encoding.
- Transmission of the modulated signals through an AWGN (Additive White Gaussian Noise) channel.
- Demodulation of the received signal and the calculation of Bit Error Rate (BER).
- Visualization of the constellation diagram and BER performance.

## Step-by-Step Code Explanation

### Step 1: Initialize Parameters and Generate Random Data

"""
clc;
clear all;
close all;

M = 16;               % Modulation order (16-QAM)
k = log2(M);          % Number of bits per symbol (log2(M))
n = 30000;            % Number of symbols per frame (total number of bits / bits per symbol)
sps = 1;              % Samples per symbol (oversampling factor)
"""

- **M = 16**: Defines the modulation order for 16-QAM. This means there are 16 distinct symbol states.
- **k = log2(M)**: Calculates the number of bits per symbol. Since 16-QAM has 16 possible symbols, `k = 4` because log₂(16) = 4.
- **n = 30000**: Specifies the total number of symbols to be transmitted in the simulation.
- **sps = 1**: This sets the oversampling factor to 1 (no oversampling in this case).

We then use the default random number generator to generate binary data:

"""
% Use default random number generator
rng default

% Generate vector of binary data
dataIn = randi([0 1],n*k,1);
"""
- **dataIn**: A column vector of random binary data, with `n*k` bits, representing the input data for the modulation.

### Step 2: Plot Random Binary Data

"""
% Plot random bits
figure;
stem(dataIn(1:40), 'filled');
title('Random Bits');
xlabel('Bit Index');
ylabel('Binary Value');
"""
- This plots the first 40 bits from the `dataIn` array using a stem plot to visually inspect the random binary data.

### Step 3: Convert Binary Data to Integer Symbols

"""
% Convert binary data to integer symbols
dataSymbolsIn = bi2de(reshape(dataIn, k, []).', 'left-msb');
"""
- **bi2de()**: Converts the binary data (`dataIn`) into decimal symbols.
  - The data is reshaped into `k` bits per symbol.
  - Each group of `k` bits is interpreted as a decimal number.
- **dataSymbolsIn**: An array containing the integer symbols that will be modulated.

### Step 4: Plot Random Symbols

"""
% Plot random symbols
figure;
stem(dataSymbolsIn(1:10));
title('Random Symbols');
xlabel('Symbol Index');
ylabel('Integer Value');
"""
- This plots the first 10 symbols in `dataSymbolsIn`, which are the integer values derived from the original binary data.

### Step 5: Modulate the Data using Binary and Gray Encoding

"""
% Binary-encoded QAM modulation
dataMod = qammod(dataSymbolsIn, M, 'bin');

% Gray-encoded QAM modulation
dataModG = qammod(dataSymbolsIn, M);
"""
- **qammod()**: Modulates the integer symbols using 16-QAM.
  - The `'bin'` option specifies binary encoding for the modulation.
  - The second call to `qammod()` uses the default Gray encoding (no `'bin'` argument), which is the most common method used in QAM.
- **dataMod**: The modulated signal using binary encoding.
- **dataModG**: The modulated signal using Gray encoding.

### Step 6: Add AWGN Noise to the Modulated Signals

"""
% Set Eb/No (in dB)
EbNo = 10;

% Convert Eb/No to SNR (dB)
snr = EbNo + 10*log10(k);  % Simple SNR conversion formula

% Add AWGN noise to the modulated signals
receivedSignal = awgn(dataMod, snr, 'measured');
receivedSignalG = awgn(dataModG, snr, 'measured');
"""
- **EbNo**: Sets the desired Energy per Bit to Noise Power Spectral Density ratio in dB.
- **snr**: Converts `EbNo` to Signal-to-Noise Ratio (SNR) in dB, considering the number of bits per symbol (`k`).
- **awgn()**: Adds Additive White Gaussian Noise to both the binary-encoded and Gray-encoded modulated signals.
  - `'measured'`: Ensures that the noise added corresponds to the specified SNR.

### Step 7: Plot the Constellation Diagram for Binary and Gray-Coded QAM

"""
% Plot the constellation diagrams for Binary and Gray-coded QAM
sPlotFig = scatterplot(receivedSignal, 1, 0, 'g.');
hold on
scatterplot(dataMod, 1, 0, 'k*', sPlotFig);
title('Constellation Diagram for Binary-Coded QAM');
"""
- **scatterplot()**: Plots the constellation diagram of the received signal (`receivedSignal`), with green dots representing the received signal, and black stars representing the transmitted signal (`dataMod`).
- This allows you to visually inspect the effect of noise on the constellation.

### Step 8: Demodulate the Received Signal

"""
% Binary-encoded QAM demodulation
dataSymbolsOut = qamdemod(receivedSignal, M, 'bin');

% Gray-coded QAM demodulation
dataSymbolsOutG = qamdemod(receivedSignalG, M);
"""
- **qamdemod()**: Demodulates the received signal using the same modulation order (`M`) and encoding method used for modulation.
  - The first call uses binary encoding (`'bin'`).
  - The second call uses Gray encoding.
- **dataSymbolsOut**: The demodulated integer symbols using binary encoding.
- **dataSymbolsOutG**: The demodulated integer symbols using Gray encoding.

### Step 9: Convert Integer Symbols Back to Binary Data

"""
% Convert integer symbols back to binary data
dataOut = de2bi(dataSymbolsOut, k, 'left-msb').';
dataOut = dataOut(:);  % Reshape into a column vector

dataOutG = de2bi(dataSymbolsOutG, k, 'left-msb').';
dataOutG = dataOutG(:);  % Reshape into a column vector
"""
- **de2bi()**: Converts the demodulated integer symbols back to binary data.
  - The `'left-msb'` option ensures that the most significant bit is on the left side.
- **dataOut**: The binary data obtained from the demodulated symbols using binary encoding.
- **dataOutG**: The binary data obtained from the demodulated symbols using Gray encoding.

### Step 10: Calculate the Bit Error Rate (BER)

"""
% Calculate bit error rate for binary-coded QAM
[numErrors, ber] = biterr(dataIn, dataOut);
fprintf('
The binary coding bit error rate is %5.2e, based on %d errors.
', ber, numErrors);

% Calculate bit error rate for Gray-coded QAM
[numErrorsG, berG] = biterr(dataIn, dataOutG);
fprintf('
The Gray coding bit error rate is %5.2e, based on %d errors.
', berG, numErrorsG);
"""
- **biterr()**: Compares the transmitted data (`dataIn`) with the demodulated data (`dataOut` for binary and `dataOutG` for Gray encoding) to calculate the number of bit errors and the bit error rate (BER).
- **ber**: The BER for binary encoding.
- **berG**: The BER for Gray encoding.

### Step 11: Modulate 16-QAM Symbols for Display

"""
% Modulation order
M = 16;

% Integer input (symbols from 0 to M-1)
x = 0:(M-1);

% 16-QAM output (binary-coded)
symbin = qammod(x, M, 'bin');

% 16-QAM output (Gray-coded)
symgray = qammod(x, M, 'gray');
"""
- **symbin**: The 16-QAM constellation points for binary-encoded symbols.
- **symgray**: The 16-QAM constellation points for Gray-encoded symbols.

### Step 12: Plot the Constellation Diagram for 16-QAM

"""
% Plot constellation diagram for Gray-coded QAM
scatterplot(symgray, 1, 0, 'b*');

% Add labels to the constellation points
for k = 1:M
    text(real(symgray(k)) - 0.0, imag(symgray(k)) + 0.3, dec2base(x(k), 2, 4), 'Color', [0 1 0]);
    text(real(symgray(k)) - 0.5, imag(symgray(k)) + 0.3, num2str(x(k)), 'Color', [0 1 0]);
    text(real(symbin(k)) - 0.0, imag(symbin(k)) - 0.3, dec2base(x(k), 2, 4), 'Color', [1 0 0]);
    text(real(symbin(k)) - 0.5, imag(symbin(k)) - 0.3, num2str(x(k)), 'Color', [1 0 0]);
   end

% Set plot title and axis limits
title('16-QAM Symbol Mapping');
axis([-4 4 -4 4]);
"""
- **scatterplot()**: Plots the constellation diagram for both binary and Gray-encoded symbols.
  - **text()**: Adds labels to each constellation point, showing the binary and decimal values for each symbol.
- **axis([-4 4 -4 4])**: Sets the axis limits to zoom in on the central part of the constellation.

## Conclusion
This script demonstrates the process of modulating and demodulating a 16-QAM signal, adding noise, calculating bit error rates, and visualizing the results with constellation diagrams. It highlights the difference between binary and Gray encoding in terms of performance (BER) and the effect of noise on signal transmission.
