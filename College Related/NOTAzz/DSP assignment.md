# Signal Processing Project: Noise Removal Using Low-Pass Filter in MATLAB

## Title:
**Noise Removal in Signals Using Low-Pass Filtering in MATLAB**

---

## Theory:

Signal processing is a field that focuses on analyzing, modifying, and synthesizing signals. One common problem in signal processing is the presence of noise, which can degrade the quality and accuracy of a signal. In this project, we simulate a noisy signal by adding Additive White Gaussian Noise (AWGN) to an original signal and then attempt to remove the noise using a low-pass filter.

### Key Concepts:
- **Additive White Gaussian Noise (AWGN):** This is a type of noise commonly added to signals in simulations. It has a flat spectral density and is Gaussian distributed in the time domain.
  
- **Low-Pass Filter:** A low-pass filter allows frequencies below a certain cutoff frequency to pass through while attenuating higher frequencies. This is useful for removing high-frequency noise from a signal.

- **Fast Fourier Transform (FFT):** The FFT is used to convert a time-domain signal into its frequency-domain representation. This helps in visualizing the frequency content of the signal and the effect of filtering.

### Objective:
The goal of this project is to:
1. Generate an original signal (sine wave).
2. Add AWGN to the signal to simulate noise.
3. Apply a low-pass filter to remove the noise.
4. Analyze and compare the signal in both time and frequency domains.

---

## Block Diagram:

```
+------------+ +-----------+ +----------+ +--------------+ | Original |---->| Add Noise |---->| Filtered |---->| Frequency | | Signal | | (AWGN) | | Signal | | Analysis | +------------+ +-----------+ +----------+ +--------------+ |
+------v------+ | FFT (Freq | | Domain) | +-------------+

```
