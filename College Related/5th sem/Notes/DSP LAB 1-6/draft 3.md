
### Signal Processing Experiments: Structured Study Guide ###

---
## Reference Overview
![Experiment Overview](Experiment_Image_Reference.png)

---
## Common Components Across All Experiments

1. **Initialization**: Every program starts by clearing the workspace, closing figures, and resetting the command window.
   ```matlab
   clc;
   clear all;
   close all;
   ```

2. **Signal Visualization**:
   Discrete signals are commonly visualized using the `stem` function:
   ```matlab
   stem(x, y);
   xlabel('Time index');
   ylabel('Amplitude');
   title('Signal Title');
   ```

3. **Basic Operations**:
   - **Addition**: `y = x1 + x2;`
   - **Multiplication**: `y = x1 .* x2;`
   - **Scaling**: `y = a * x;`
   - **Shifting**: Right and left shifts using indexing.

4. **Transformations**:
   Fourier Transform, Convolution, and Pole-Zero analysis are central to understanding signal behaviors.

---
## Experiment 1: Sequence Generation
### Objective:
Generate and analyze common discrete-time sequences:
1. Unit Sample Sequence
2. Unit Step Sequence
3. Exponential Sequence
4. Sinusoidal Sequence
5. Random Sequence

### Code:
```matlab
clc;
clear all;
close all;

% Unit Sample Sequence
n1 = -10:10;
u = [zeros(1, 10) 1 zeros(1, 10)];
subplot(3, 2, 1);
stem(n1, u);
title('Unit Sample Sequence');

% Add other sequences similarly...
```

---
## Experiment 2: Signal Operations
### Objective:
Perform operations on signals including shifting, scaling, and multiplication.

### Key Code:
#### Shifting:
```matlab
% Right Shift
N1 = n + k;
stem(N1, x);
```

#### Scaling:
```matlab
% Scaled Up
y = a * x;
```

#### Multiplication:
```matlab
% Signal Multiplication
result = x1 .* x2;
```

---
## Experiment 3: Convolution
### Objective:
Implement convolution manually (without using built-in functions).

### Code:
```matlab
for i = 1:N
    Y(i) = 0;
    for j = 1:m
        if i - j + 1 > 0
            Y(i) = Y(i) + X(j) * H(i-j+1);
        end
    end
end
```

---
## Experiment 4: Two-Pole Analysis
### Objective:
Analyze the frequency response of a system characterized by its transfer function.

### Key Code:
```matlab
H = tf(num, den, -1);
pzmap(H);
```

---
## Experiment 5: DFT Computation
### Objective:
Compute the N-point DFT of a signal and plot its magnitude and phase spectra.

### Key Code:
```matlab
W = exp(-j * 2 * pi * (0:N-1)' * (0:N-1) / N);
Xk = W * x';
```

---
## Experiment 6: Circular and Linear Convolution
### Objective:
Compare circular and linear convolutions using the DFT and IDFT.

### Key Code:
```matlab
Yk = fft(x, N) .* fft(h, N);
y = ifft(Yk);
```

---
### Study Tips
1. Start by understanding **common components**—these repeat across experiments.
2. Focus on the unique code in each experiment and understand its functionality.
3. Test small portions of code to visualize their effects.
4. Refer to the uploaded diagram for clarity.

