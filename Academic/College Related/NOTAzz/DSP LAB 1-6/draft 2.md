
### Signal Processing Programs: Common and Unique Features ###

---
## Common Components Across Programs

### Initialization
All programs begin with:
```matlab
clc;
clear all;
close all;
```
- **Purpose**: Clear workspace, command window, and close all plots.

### Plotting with `stem`
All experiments visualize discrete signals using:
```matlab
stem(x, y);
xlabel('Time index');
ylabel('Amplitude');
title('Signal Title');
```

### Signal Generation and Manipulation Functions
1. **Basic Sequences**:
   - Unit Sample: `u = [zeros(1, N) 1 zeros(1, N)]`
   - Unit Step: `x = ones(1, N)`
   - Exponential: `x = a.^n`

2. **Signal Operations**:
   - Addition: `y = x1 + x2;`
   - Multiplication: `y = x1 .* x2;`
   - Scaling: `y = a * x;`

3. **Shifting**:
   - Right: `y = [zeros(1, k), x]`
   - Left: `y = x(k:end)`

4. **Fourier Transformation**:
   - DFT Matrix: `W(k+1, n+1) = exp(-j * 2 * pi * k * n / N);`

---
## Unique Features of Each Experiment

### Experiment 1: Sequence Generation
**Purpose**: Create and visualize sequences.

**Unique Code**:
```matlab
% Unit Sample Sequence
n = -10:10;
u = [zeros(1, 10) 1 zeros(1, 10)];
stem(n, u);
title('Unit Sample Sequence');
```

### Experiment 2: Transformations
1. **Shifting**:
```matlab
% Right Shift
n_shifted = n + k;
stem(n_shifted, x);
title('Right Shifted Signal');
```

2. **Scaling**:
```matlab
% Scale Up
y = a * x;
stem(n, y);
title('Scaled Up Signal');
```

3. **Folding**:
```matlab
% Folded Signal
y = fliplr(x);
stem(n, y);
title('Folded Signal');
```

### Experiment 3: DFT
**Unique Code**:
```matlab
% DFT Computation
for k = 0:N-1
    for n = 0:N-1
        W(k+1, n+1) = exp(-j * 2 * pi * k * n / N);
    end
end
Xk = W * x';
```

### Experiment 4: Convolution
1. **Without `conv`**:
```matlab
% Manual Convolution
for i = 1:N
    Y(i) = 0;
    for j = 1:m
        if i - j + 1 > 0
            Y(i) = Y(i) + X(j) * H(i-j+1);
        end
    end
end
```

2. **Linear Convolution**:
```matlab
% Using FFT for Convolution
Yk = fft(x, N) .* fft(h, N);
y = ifft(Yk);
```

### Experiment 5: Two-Pole Analysis
**Unique Code**:
```matlab
% Transfer Function and Pole-Zero Plot
H = tf(num, den, -1);
[zeros, poles] = tf2zp(num, den);
pzmap(H);
```

---
### Learning Strategy
1. Understand **common components** first—these repeat in every program.
2. Focus on **unique elements** program-by-program.
3. Test each block separately to understand functionality.

