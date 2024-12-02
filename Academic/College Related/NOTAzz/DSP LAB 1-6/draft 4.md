
# Signal Processing Experiments: Comprehensive Study Guide  

---

## Common Components Across All Experiments  

1. **Initialization**: Every MATLAB script starts with clearing the environment:  
   ```matlab
   clc;         % Clear command window
   clear all;   % Clear workspace
   close all;   % Close all figures
   ```  

2. **Signal Visualization**:  
   Discrete signals are visualized using the `stem` function for clarity:  
   ```matlab
   stem(x, y);                % Discrete-time signal plot
   xlabel('Time index');      % Label for time
   ylabel('Amplitude');       % Label for amplitude
   title('Signal Title');     % Plot title
   ```  

3. **Basic Operations on Signals**:  
   - **Addition**: `y = x1 + x2;`  
   - **Multiplication**: `y = x1 .* x2;`  
   - **Scaling**: `y = a * x;`  
   - **Shifting**: Right and left shifts using indexing: `y_shifted = [zeros(1, k), x(1:end-k)];`  
   - **Folding**: Reverse a signal: `y_folded = fliplr(x);`  

---

## Experiment 1: Sequence Generation  

### Objective:  
Generate and visualize the following discrete-time sequences:  
1. Unit Sample Sequence  
2. Unit Step Sequence  
3. Exponential Sequence  
4. Sinusoidal Sequence  
5. Random Sequence  

### MATLAB Code:  
```matlab
clc;
clear all;
close all;

% Unit Sample Sequence
n1 = -10:10; % Range of n
u = [zeros(1, 10) 1 zeros(1, 10)]; % Impulse at n = 0
subplot(3, 2, 1);
stem(n1, u);
xlabel('Time index');
ylabel('Amplitude');
title('Unit Sample Sequence');

% Unit Step Sequence
n2 = 0:20;
x_step = ones(1, length(n2)); % Step signal
subplot(3, 2, 2);
stem(n2, x_step);
xlabel('Time index');
ylabel('Amplitude');
title('Unit Step Sequence');

% Exponential Sequence
n3 = 0:10;
x_exp = 0.8 .^ n3; % Exponential decay
subplot(3, 2, 3);
stem(n3, x_exp);
xlabel('Time index');
ylabel('Amplitude');
title('Exponential Sequence');

% Sinusoidal Sequence
n4 = 0:50;
x_sin = sin(0.1 * pi * n4); % Sinusoidal signal
subplot(3, 2, 4);
stem(n4, x_sin);
xlabel('Time index');
ylabel('Amplitude');
title('Sinusoidal Sequence');

% Random Sequence
n5 = 0:20;
x_rand = rand(1, length(n5)); % Random signal
subplot(3, 2, 5);
stem(n5, x_rand);
xlabel('Time index');
ylabel('Amplitude');
title('Random Sequence');
```  

---

## Experiment 2: Signal Operations  

### Objective:  
Perform the following operations on signals:  
a. Addition  
b. Multiplication  
c. Scaling  
d. Shifting  
e. Folding  

### MATLAB Code:  

#### (a) Signal Addition:  
```matlab
clc;
clear all;
close all;

x1 = [1 2 3 4];
n1 = 0:3;
x2 = [4 3 2 1];
n2 = 0:3;

y_add = x1 + x2; % Element-wise addition
stem(n1, y_add);
xlabel('Time index');
ylabel('Amplitude');
title('Signal Addition');
```  

#### (b) Signal Multiplication:  
```matlab
clc;
clear all;
close all;

x1 = [1 2 3 4];
x2 = [0.5 0.5 0.5 0.5];

y_mult = x1 .* x2; % Element-wise multiplication
stem(0:3, y_mult);
xlabel('Time index');
ylabel('Amplitude');
title('Signal Multiplication');
```  

#### (c) Scaling:  
```matlab
clc;
clear all;
close all;

x = [1 2 3 4];
a = 2; % Scaling factor

y_scaled = a * x;
stem(0:3, y_scaled);
xlabel('Time index');
ylabel('Amplitude');
title('Signal Scaling');
```  

#### (d) Shifting:  
```matlab
clc;
clear all;
close all;

x = [1 2 3 4];
n = 0:3;

% Right shift by 2
shift = 2;
x_shifted = [zeros(1, shift), x]; % Add zeros at the start
stem(0:length(x_shifted)-1, x_shifted);
xlabel('Time index');
ylabel('Amplitude');
title('Signal Right Shifting');
```  

#### (e) Folding:  
```matlab
clc;
clear all;
close all;

x = [1 2 3 4];
x_folded = fliplr(x); % Reverse the signal
stem(-3:0, x_folded);
xlabel('Time index');
ylabel('Amplitude');
title('Signal Folding');
```  

---

## Experiment 3: Convolution  

### Objective:  
Perform convolution of two signals manually (without using MATLAB’s `conv` function).  

### MATLAB Code:  
```matlab
clc;
clear all;
close all;

x = [1 2 3];
h = [4 5 6];

% Convolution
N = length(x) + length(h) - 1;
y = zeros(1, N);
for n = 1:N
    for k = 1:length(x)
        if n-k+1 > 0 && n-k+1 <= length(h)
            y(n) = y(n) + x(k) * h(n-k+1);
        end
    end
end

stem(0:N-1, y);
xlabel('Time index');
ylabel('Amplitude');
title('Convolution Without Built-in Function');
```  

---

## Experiment 4: Two-Pole Analysis  

### Objective:  
Analyze the frequency response and impulse response of a system defined by:  
\[ y(n) = 0.9y(n-1) + x(n) \]  

### MATLAB Code:  
```matlab
clc;
clear all;
close all;

% Define the system
num = [1]; % Numerator coefficients
den = [1 -0.9]; % Denominator coefficients

% Pole-Zero Plot
figure;
zplane(num, den);
title('Pole-Zero Plot');

% Impulse Response
n = 0:50;
h = filter(num, den, [1 zeros(1, 50)]); % Impulse response
figure;
stem(n, h);
xlabel('Time index');
ylabel('Amplitude');
title('Impulse Response');
```  

---

## Experiment 5: DFT Computation  

### Objective:  
Compute the N-point Discrete Fourier Transform (DFT) of a sequence and plot the magnitude and phase spectra.  

### MATLAB Code:  
```matlab
clc;
clear all;
close all;

x = [1 2 3 4];
N = length(x);

% Compute DFT manually
Xk = zeros(1, N);
for k = 0:N-1
    for n = 0:N-1
        Xk(k+1) = Xk(k+1) + x(n+1) * exp(-1j * 2 * pi * k * n / N);
    end
end

% Plot magnitude and phase
subplot(2, 1, 1);
stem(0:N-1, abs(Xk));
xlabel('Frequency index');
ylabel('Magnitude');
title('DFT Magnitude');

subplot(2, 1, 2);
stem(0:N-1, angle(Xk));
xlabel('Frequency index');
ylabel('Phase');
title('DFT Phase');
```  

---

## Experiment 6: Circular and Linear Convolution  

### Objective:  
Compare circular and linear convolutions using the DFT and IDFT.  

### MATLAB Code:  
```matlab
clc;
clear all;
close all;

x = [1 2 3];
h = [4 5 6];

% Circular Convolution
N = max(length(x), length(h));
Xk = fft(x, N);
Hk = fft(h, N);
Yk = Xk .* Hk;
y_circular = ifft(Yk);
subplot(2, 1, 1);
stem(0:N-1, y_circular);
xlabel('Time index');
ylabel('Amplitude');
title('Circular Convolution');

% Linear Convolution
y_linear = conv(x, h);
subplot(2, 1, 2);
stem(0:length(y_linear)-1, y_linear);
xlabel('Time index');
ylabel('Amplitude');
title('Linear Convolution');
```  
