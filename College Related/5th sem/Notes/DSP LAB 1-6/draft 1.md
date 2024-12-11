
### Signal Processing Programs: Segmented and Explained ###

---
## Experiment 1: Basic Sequence Generation
**Purpose**: Generate and visualize common discrete sequences.

**Sequences Included**:
1. Unit Sample Sequence
2. Unit Step Sequence
3. Exponential Sequence
4. Sinusoidal Sequence
5. Random Sequence

**Code**:
```matlab
clc;
clear all;
close all;

% Unit Sample Sequence
n1 = -10:10;
u = [zeros(1, 10) 1 zeros(1, 10)];
subplot(3, 2, 1);
stem(n1, u);
xlabel('Time index');
ylabel('Amplitude');
title('Unit sample sequence');

% Unit Step Sequence
n2 = 0:20;
x = ones(1, 21);
subplot(3, 2, 2);
stem(n2, x);
xlabel('Time index');
ylabel('Amplitude');
title('Unit step sequence');

% Exponential Sequence
n3 = -10:10;
x2 = 0.8 .^ n3;
subplot(3, 2, 3);
stem(n3, x2);
xlabel('Time index');
ylabel('Amplitude');
title('Exponential sequence');

% Sinusoidal Sequence
n4 = -10:10;
x1 = sin(0.2 * pi * n4);
subplot(3, 2, 4);
stem(n4, x1);
xlabel('Time index');
ylabel('Amplitude');
title('Sinusoidal sequence');

% Random Sequence
X = -10:20;
y = rand(1, 31);
subplot(3, 2, 5);
stem(X, y);
xlabel('Time index');
ylabel('Amplitude');
title('Random sequence');
```

---
## Experiment 2: Signal Transformations
### Shifting
**Purpose**: Visualize right and left shifts of a discrete signal.

**Code**:
```matlab
clc;
clear all;
close all;

% Signal Input
x1 = [1 2 3 4];
n1 = 0:3;
subplot(3, 1, 1);
stem(n1, x1);
xlabel('Time');
ylabel('Amplitude');
title('Original Signal');

% Right Shift
N1 = n1 + 3;
subplot(3, 1, 2);
stem(N1, x1);
xlabel('Time');
ylabel('Amplitude');
title('Right Shifted Signal');

% Left Shift
N2 = n1 - 3;
subplot(3, 1, 3);
stem(N2, x1);
xlabel('Time');
ylabel('Amplitude');
title('Left Shifted Signal');
```

---
### Scaling
**Purpose**: Scale a signal up or down.

**Code**:
```matlab
clc;
clear all;
close all;

% Signal Input
x1 = [1 2 3 4];
n1 = 0:3;

% Original Signal
subplot(3, 1, 1);
stem(n1, x1);
xlabel('Time');
ylabel('Amplitude');
title('Original Signal');

% Scaled Up
a = 2; % Scaling Factor
y1 = a * x1;
subplot(3, 1, 2);
stem(n1, y1);
xlabel('Time');
ylabel('Amplitude');
title('Scaled Up Signal');

% Scaled Down
y2 = (1 / a) * x1;
subplot(3, 1, 3);
stem(n1, y2);
xlabel('Time');
ylabel('Amplitude');
title('Scaled Down Signal');
```

---
### Multiplication
**Purpose**: Element-wise multiplication of two signals.

**Code**:
```matlab
clc;
clear all;
close all;

% Input Signals
x1 = [1 2 3 4];
x2 = [1 -1 1 -1];

% Original Signals
subplot(3, 1, 1);
stem(0:3, x1);
title('Signal 1');

subplot(3, 1, 2);
stem(0:3, x2);
title('Signal 2');

% Multiplication
result = x1 .* x2;
subplot(3, 1, 3);
stem(0:3, result);
title('Multiplied Signal');
```

---
## Experiment 3: Discrete Fourier Transform (DFT)
**Purpose**: Compute and analyze the DFT of a signal.

**Code**:
```matlab
clc;
clear all;
close all;

x = [1 2 3 4];
N = 4; % Number of points

% Compute DFT Matrix
for k = 0:N-1
    for n = 0:N-1
        W(k+1, n+1) = exp(-j * 2 * pi * k * n / N);
    end
end

% DFT Computation
Xk = W * x';

% Display Results
disp('DFT:');
disp(Xk);

% Magnitude and Phase
Xmag = abs(Xk);
Xpha = angle(Xk);
disp('Magnitude:');
disp(Xmag);
disp('Phase:');
disp(Xpha);
```

---
## Experiment 4: Convolution
### Without `conv` Function
**Purpose**: Perform convolution manually.

**Code**:
```matlab
clc;
clear all;
close all;

x = [1 2 3 4];
h = [1 2];
m = length(x);
n = length(h);
X = [x, zeros(1, n)];
H = [h, zeros(1, m)];
N = m + n - 1;

for i = 1:N
    Y(i) = 0;
    for j = 1:m
        if i-j+1 > 0
            Y(i) = Y(i) + X(j) * H(i-j+1);
        end
    end
end

disp('Convoluted Sequence:');
disp(Y);
```

---
## Experiment 5: Two-Pole Analysis
**Purpose**: Analyze the frequency response of a two-pole system.

**Code**:
```matlab
clc;
clear all;
close all;

num = [1];
den = [1 -0.9];
H = tf(num, den, -1);

disp('Poles and Zeros:');
[zz, pp] = tf2zp(num, den);

omega = linspace(-pi, pi, 1024);
H_freq = freqz(num, den, omega);
magnitude = abs(H_freq);
phase = angle(H_freq);

figure;
subplot(2, 1, 1);
plot(omega, magnitude);
title('Magnitude Response');

subplot(2, 1, 2);
plot(omega, phase);
title('Phase Response');
```
---
### Learning Tips:
1. Group similar operations (e.g., scaling, shifting).
2. Practice segment-by-segment for clarity.
3. Experiment with modifying inputs and observing outputs.
