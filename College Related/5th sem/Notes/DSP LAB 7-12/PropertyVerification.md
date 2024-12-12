# DSP Code Examples  

This document contains examples of various DSP properties and their MATLAB implementations with outputs.  

---

## **Linearity Property**  

### **Step 1: Initialization**  
```matlab
clc;
close all;
clear;
```  

### **Step 2: User Inputs**  
```matlab
x1 = input('enter the first input sequence =');
x2 = input('enter the second input sequence =');
a1 = input('enter the constant a1 =');
a2 = input('enter the constant a2 =');
```  

### **Step 3: Preprocessing Input Sequences**  
```matlab
l1 = length(x1);
l2 = length(x2);
N = max(l1, l2);
x1N = [x1, zeros(1, N - l1)];
x2N = [x2, zeros(1, N - l2)];
```  

### **Step 4: Compute Output Sequence**  
```matlab
y = (a1 * x1N) + (a2 * x2N);
Yk = fft(y, N);
disp('output sequence y(k) is');
disp(Yk);
```  

### **Step 5: Verify Linearity Property**  
```matlab
x1k = fft(x1, N);
x2k = fft(x2, N);
Yv = a1 * x1k + a2 * x2k;
if (Yk == Yv)
    disp('linearty property is satisfied');
else
    disp('linearity property is not satisfied');
end
```  

### **Example Output**  
```matlab
enter the first input sequence = [1 2 3 4]
enter the second input sequence = [4 5]
enter the constant a1 = 2
enter the constant a2 = 3
output sequence y(k) is
  47.0000 + 0.0000i   8.0000 -11.0000i
  -7.0000 + 0.0000i   8.0000 +11.0000i
linearity property is satisfied
```  

---

## **Circular Time Shift Property**  

### **Step 1: Initialization**  
```matlab
clc;
clear all;
close all;
```  

### **Step 2: User Inputs**  
```matlab
x = input('enter the first input sequence =');
m = input('enter the number of shifts =');
```  

### **Step 3: Compute Circularly Shifted Sequence**  
```matlab
N = length(x);
Xs = circshift(x, [0, m]);
y = fft(Xs, N);
Xk = fft(x, N);
```  

### **Step 4: Compute Expected Output with Phase Shift**  
```matlab
for K = 0:N-1
    w(K+1) = exp((-j * 2 * pi * K * m) / N);
end
Yv = w .* Xk;
disp(y);
disp(Yv);
```  

### **Step 5: Verify Circular Time Shift Property**  
```matlab
if (floor(abs(y)) == floor(abs(Yv)))
    disp('circular time shift property is satisfied');
else
    disp('circular time shift property is not satisfied');
end
```  

### **Example Output**  
```matlab
enter the first input sequence = [1 2 3 4]
enter the number of shifts = 2
y:
  10.0000 + 0.0000i   2.0000 - 2.0000i
  -2.0000 + 0.0000i   2.0000 + 2.0000i
Yv:
  10.0000 + 0.0000i   2.0000 - 2.0000i
  -2.0000 + 0.0000i   2.0000 + 2.0000i
circular time shift property is satisfied
```  

---

## **Circular Frequency Shift Property**  

### **Step 1: Initialization**  
```matlab
clc;
close all;
clear;
```  

### **Step 2: User Inputs**  
```matlab
x = input('enter the first input sequence =');
l = input('enter the number of shifts =');
```  

### **Step 3: Compute FFT and Frequency Shift**  
```matlab
N = length(x);
Xk = fft(x, N);
Yv = circshift(Xk, [0, l]);
```  

### **Step 4: Compute Expected Time Modulation**  
```matlab
for n = 0:N-1
    w(n+1) = exp((j * 2 * pi * n * l) / N);
end
y = w .* x;
Yk = fft(y);
disp(Yk);
disp(Yv);
```  

### **Step 5: Verify Circular Frequency Shift Property**  
```matlab
if (floor(abs(Yk)) == floor(abs(Yv)))
    disp('circular Frequency shift property is satisfied');
else
    disp('circular Frequency shift property is not satisfied');
end
```  

### **Example Output**  
```matlab
enter the first input sequence = [1 2 3 4]
enter the number of shifts = 2
Yk:
  -2.0000 + 0.0000i  -2.0000 - 2.0000i
   10.0000 - 0.0000i  -2.0000 + 2.0000i
Yv:
  -2.0000 + 0.0000i  -2.0000 - 2.0000i
   10.0000 + 0.0000i  -2.0000 + 2.0000i
circular Frequency shift property is satisfied
```  
