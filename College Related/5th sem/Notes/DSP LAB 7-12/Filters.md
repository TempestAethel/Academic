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
fp = input('enter the passband freq=');
fs = input('enter the stopband freq=');
f = input('enter the sampling freq=');
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
  - `fp = 150`
  - `fs = 300`
  - `f = 1500`

---

## FIR Filters (Low Pass and High Pass)

### Code
```matlab
wp = 2 * fp / f;
ws = 2 * fs / f;
num = -20 * log10(sqrt(rp * rs)) - 13;
den = 14.6 * (fs - fp) / f;
n = ceil(num / den);
n1 = n + 1;
if (rem(n, 2) ~= 0)
    n1 = n;
    n = n - 1;
end
y = boxcar(n1); %/ y = bartlett(n1); / y = hanning(n1); / y = hamming(n1);
b = fir1(n, wp, 'low', y);  % Use 'high' for High Pass Filter
[h, q] = freqz(b, 1, 256);
m = 20 * log10(abs(h));
subplot(2, 2, 1);
plot(q / pi, m);
xlabel('normalised freq');
ylabel('gain in dB');
title('FIR Filter using specified window');
```

---

## Digital IIR Butterworth Filters (Low Pass and High Pass)

### Code
```matlab
w1 = 2 * wp / fs;
w2 = 2 * ws / fs;
[n, wn] = buttord(w1, w2, rp, rs);
[b, a] = butter(n, wn, 'low');  % Use 'high' for High Pass Filter
disp('The order of the filter:');
disp(n);
disp('The cutoff frequency of the filter:');
disp(wn);
w = 0:0.01:pi;
[h] = freqz(b, a, w);
mag = 20 * log10(abs(h));
ang = angle(h);
subplot(2, 1, 1);
plot(w / pi, mag);
xlabel('normalised freq');
ylabel('magnitude');
title('Magnitude Response');
subplot(2, 1, 2);
plot(w / pi, ang);
xlabel('normalised freq');
ylabel('angle');
title('Phase Response');
```
