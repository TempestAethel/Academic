# Comparison of Filter Programs

This document compares the four filter programs:  
1. **FIR Low Pass Filter**
2. **FIR High Pass Filter**
3. **Digital IIR Butterworth Low Pass Filter**
4. **Digital IIR Butterworth High Pass Filter**

## Common Steps in All Filter Programs

### 1. **Input Parameters**
   - **Passband Ripple (`rp`)**
   - **Stopband Ripple (`rs`)**
   - **Passband Frequency (`fp`)**
   - **Stopband Frequency (`fs`)**
   - **Sampling Frequency (`f`)**

All programs ask the user for these parameters, which define the characteristics of the filter.

### 2. **Normalized Frequencies**
   - Passband (`wp`) and Stopband (`ws`) are normalized using the formula:
     ```
     wp = 2 * fp / f;
     ws = 2 * fs / f;
     ```
   These formulas convert the passband and stopband frequencies from Hz to the normalized range [0, 1], where 1 corresponds to half the sampling frequency (`f/2`).

### 3. **Filter Order Calculation**
   All programs calculate the filter order (`n`) based on a specific formula, which takes into account the passband and stopband ripples and frequencies. 
   - For FIR filters:
     ```
     num = -20 * log10(sqrt(rp * rs)) - 13;
     den = 14.6 * (fs - fp) / f;
     n = ceil(num / den);
     ```
   - For IIR filters:
     ```
     w1 = 2 * wp / fs;
     w2 = 2 * ws / fs;
     [n, wn] = buttord(w1, w2, rp, rs);
     ```

### 4. **Window Selection (FIR Filters)**
   - For FIR filters, a window function is used to shape the filter. This can be changed based on the user’s requirement:
     - `y = boxcar(n1);`
     - `y = bartlett(n1);`
     - `y = hanning(n1);`
     - `y = hamming(n1);`

### 5. **Frequency Response Calculation**
   - For both FIR and IIR filters, the frequency response (`h`) is calculated using `freqz`:
     ```
     [h, q] = freqz(b, 1, 256);
     ```

### 6. **Magnitude and Phase Response**
   The magnitude and phase responses of the filter are plotted. In the case of FIR filters, the magnitude is calculated as:
   ```
   m = 20 * log10(abs(h));
   ```
   In the case of IIR filters, the magnitude is similarly calculated, but the phase angle is also plotted:
   ```
   mag = 20 * log10(abs(h));
   ang = angle(h);
   ```

---

## FIR Filters (Low Pass and High Pass)

### 1. **Low Pass Filter Using FIR**
   - The FIR low pass filter is designed using the following steps:
     1. **Windowing**: `y = boxcar(n1);`
     2. **Filter Design**: `b = fir1(n, wp, 'low', y);`
     3. **Frequency Response**: 
        ```
        [h, q] = freqz(b, 1, 256);
        m = 20 * log10(abs(h));
        ```
     4. **Plotting**: The magnitude response is plotted.
        ```
        subplot(2, 2, 1);
        plot(q/pi, m);
        xlabel('normalized freq');
        ylabel('gain in dB');
        title('Low pass filter using rectangular window');
        ```

   ### 2. **High Pass Filter Using FIR**
   - The FIR high pass filter is designed similarly but with a high-pass filter design:
     1. **Windowing**: `y = boxcar(n1);`
     2. **Filter Design**: `b = fir1(n, wp, 'high', y);`
     3. **Frequency Response**: 
        ```
        [h, q] = freqz(b, 1, 256);
        m = 20 * log10(abs(h));
        ```
     4. **Plotting**: The magnitude response is plotted.
        ```
        subplot(2, 2, 2);
        plot(q/pi, m);
        xlabel('normalized freq');
        ylabel('gain in dB');
        title('High pass filter using rectangular window');
        ```

---

## IIR Filters (Low Pass and High Pass)

### 1. **Low Pass Filter Using IIR Butterworth**
   - The Butterworth low pass filter design involves the following steps:
     1. **Normalize Frequencies**: 
        ```
        w1 = 2 * wp / fs;
        w2 = 2 * ws / fs;
        ```
     2. **Order and Cutoff Calculation**: 
        ```
        [n, wn] = buttord(w1, w2, rp, rs);
        [b, a] = butter(n, wn, 'low');
        ```
     3. **Frequency Response**:
        ```
        w = 0:0.01:pi;
        [h] = freqz(b, a, w);
        ```
     4. **Plotting**:
        - Magnitude:
          ```
          mag = 20 * log10(abs(h));
          subplot(2, 1, 1);
          plot(w/pi, mag);
          xlabel('normalized freq');
          ylabel('magnitude');
          ```
        - Phase:
          ```
          ang = angle(h);
          subplot(2, 1, 2);
          plot(w/pi, ang);
          xlabel('normalized freq');
          ylabel('angle');
          ```

### 2. **High Pass Filter Using IIR Butterworth**
   - The Butterworth high pass filter design is similar to the low-pass filter but with a high-pass filter design:
     1. **Normalize Frequencies**: 
        ```
        w1 = 2 * wp / fs;
        w2 = 2 * ws / fs;
        ```
     2. **Order and Cutoff Calculation**:
        ```
        [n, wn] = buttord(w1, w2, rp, rs);
        [b, a] = butter(n, wn, 'high');
        ```
     3. **Frequency Response**:
        ```
        w = 0:0.01:pi;
        [h] = freqz(b, a, w);
        ```
     4. **Plotting**:
        - Magnitude:
          ```
          mag = 20 * log10(abs(h));
          subplot(2, 1, 1);
          plot(w/pi, mag);
          xlabel('normalized freq');
          ylabel('magnitude');
          ```
        - Phase:
          ```
          ang = angle(h);
          subplot(2, 1, 2);
          plot(w/pi, ang);
          xlabel('normalized freq');
          ylabel('angle');
          ```

---

## Output for FIR Filters

In both FIR and IIR designs, the order of the filter and cutoff frequency are displayed as outputs:

- **FIR Filters**: The order is indirectly determined through the window and formula for calculating `n`.
- **IIR Filters**: Directly displays the order of the Butterworth filter and the cutoff frequency.

For example:
```

```

---
## Output for FIR Filters

In both FIR and IIR designs, the order of the filter and cutoff frequency are displayed as outputs:

- **FIR Filters**: The order is indirectly determined through the window and formula for calculating `n`.
- **IIR Filters**: Directly displays the order of the Butterworth filter and the cutoff frequency.

For example:
```
the order of lpf
     9

the cut off freq of lpf
    0.2071
```

---

## Conclusion

Both FIR and IIR filters are commonly used for signal processing, but their designs and implementations differ. The key steps—such as defining the passband and stopband frequencies, calculating the filter order, and plotting the frequency response—are quite similar, but the approaches to filter design differ:
- FIR filters use windowing functions, while
- IIR filters use analytical methods like the Butterworth approximation.

The main difference in their implementation is the use of `fir1` for FIR filters and `butter` for IIR filters.
