## General Control and Initialization
- **clc**
  - **Syntax**: `clc`
  - **Description**: Clears the command window.

- **clear all**
  - **Syntax**: `clear all`
  - **Description**: Removes all variables, globals, functions, and MEX links.

- **close all**
  - **Syntax**: `close all`
  - **Description**: Closes all open figure windows.

## Mathematical Operations
- **abs**
  - **Syntax**: `y = abs(x)`
  - **Description**: Computes the absolute value of a number or magnitude of a complex number.

- **angle**
  - **Syntax**: `theta = angle(x)`
  - **Description**: Computes the phase angle of a complex number (in radians).

- **exp**
  - **Syntax**: `y = exp(x)`
  - **Description**: Calculates the exponential \(e^x\).

- **fft**
  - **Syntax**: `Y = fft(x)`
  - **Description**: Computes the Fast Fourier Transform.

- **ifft**
  - **Syntax**: `y = ifft(X)`
  - **Description**: Computes the Inverse Fast Fourier Transform.

- **circshift**
  - **Syntax**: `B = circshift(A, k)`
  - **Description**: Circularly shifts array elements.

- **floor**
  - **Syntax**: `y = floor(x)`
  - **Description**: Rounds elements to the nearest integer less than or equal to the input.

- **fliplr**
  - **Syntax**: `B = fliplr(A)`
  - **Description**: Flips a matrix horizontally.

- **real**
  - **Syntax**: `y = real(x)`
  - **Description**: Extracts the real part of a complex number.

- **phase**
  - **Syntax**: `theta = phase(x)`
  - **Description**: Computes the phase angle of a complex number (alternative to `angle`).

- **bit_reverse**
  - **Syntax**: `reversed = bit_reverse(data)`
  - **Description**: Rearranges indices based on bit-reversal (used in FFT).

- **collect**
  - **Syntax**: `expr = collect(expr)`
  - **Description**: Collects coefficients of terms in symbolic expressions.

- **simplify**
  - **Syntax**: `simpExpr = simplify(expr)`
  - **Description**: Simplifies symbolic expressions.

## Plotting and Display
- **disp**
  - **Syntax**: `disp('Hello World')`
  - **Description**: Displays a message or value in the command window.

- **subplot**
  - **Syntax**: `subplot(m, n, p)`
  - **Description**: Creates subplots in a single figure.

- **stem**
  - **Syntax**: `stem(x, y)`
  - **Description**: Creates a stem plot (discrete data).

- **plot**
  - **Syntax**: `plot(x, y)`
  - **Description**: Creates a 2D line plot.

- **title**
  - **Syntax**: `title('My Plot')`
  - **Description**: Adds a title to a plot.

- **xlabel**
  - **Syntax**: `xlabel('Time (s)')`
  - **Description**: Labels the x-axis.

- **ylabel**
  - **Syntax**: `ylabel('Amplitude')`
  - **Description**: Labels the y-axis.

- **grid**
  - **Syntax**: `grid on`
  - **Description**: Toggles grid on a plot.

- **axis off**
  - **Syntax**: `axis off`
  - **Description**: Hides the axes on a plot.

## Signal Processing
- **butter**
  - **Syntax**: `[b, a] = butter(n, Wn)`
  - **Description**: Designs a Butterworth filter.

- **buttord**
  - **Syntax**: `[n, Wn] = buttord(Wp, Ws, Rp, Rs)`
  - **Description**: Determines the minimum order for a Butterworth filter.

- **freqz**
  - **Syntax**: `freqz(b, a)`
  - **Description**: Computes and plots the frequency response of a filter.

- **fir1**
  - **Syntax**: `b = fir1(N, Wn)`
  - **Description**: Designs a FIR filter using the window method.

- **boxcar**
  - **Syntax**: `w = boxcar(N)`
  - **Description**: Generates a rectangular (boxcar) window.

- **bartlett**
  - **Syntax**: `w = bartlett(N)`
  - **Description**: Generates a Bartlett (triangular) window.

- **hanning**
  - **Syntax**: `w = hanning(N)`
  - **Description**: Generates a Hann window.

- **hamming**
  - **Syntax**: `w = hamming(N)`
  - **Description**: Generates a Hamming window.

- **pzplot**
  - **Syntax**: `pzplot(sys)`
  - **Description**: Plots poles and zeros of a transfer function.

- **tf**
  - **Syntax**: `sys = tf(num, den)`
  - **Description**: Creates a transfer function model.

- **tf2zp**
  - **Syntax**: `[z, p, k] = tf2zp(num, den)`
  - **Description**: Converts a transfer function to zero-pole-gain form.

## Miscellaneous
- **length**
  - **Syntax**: `n = length(x)`
  - **Description**: Returns the length of the largest dimension of an array.

- **zeros**
  - **Syntax**: `A = zeros(m, n)`
  - **Description**: Creates an array of zeros.

- **ones**
  - **Syntax**: `A = ones(m, n)`
  - **Description**: Creates an array of ones.

- **ceil**
  - **Syntax**: `y = ceil(x)`
  - **Description**: Rounds elements to the nearest integer greater than or equal to the input.

- **linspace**
  - **Syntax**: `v = linspace(a, b, n)`
  - **Description**: Generates linearly spaced vectors.

## Custom Function
- **dit_radix2_fft**
  - **Syntax**: `X = dit_radix2_fft(x)`
  - **Description**: Computes the Radix-2 Decimation-in-Time FFT.
