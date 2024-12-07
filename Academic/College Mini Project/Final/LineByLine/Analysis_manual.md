# Analysis.m - Line-by-Line Analysis and Manual Calculations

This document provides a detailed line-by-line explanation of the code in `Analysis.m`. For each line, the code is shown, followed by its purpose, manual calculation (if applicable), and any additional information.

---

## **Line-by-Line Explanation**

### **1. Load Parameters and Simulation Results**
**Code**:  
run('Parameters.m');  
load('Implementation_Results.mat');

- **Purpose**:  
  - **`run('Parameters.m')`**: Executes the **Parameters.m** script to load all system parameters and transfer functions into the workspace.  
  - **`load('Implementation_Results.mat')`**: Loads the simulation results saved in the file `Implementation_Results.mat`, which includes time-domain and frequency-domain data.

---

### **2. Noise Source Definitions**
**Code**:  
Ref_PN_Freq = [10e3 30e3 100e3 1e6 3e6 10e6]; % Hz  
Ref_PN_Level = [-140 -140 -140 -140 -140 -140] - 20; % dBc/Hz  
CP_PN_Freq = [10e3 30e3 100e3 1e6 3e6 10e6]; % Hz  
CP_PN_Level = [-224 -229 -234 -239 -240 -241]; % dBc/Hz  
VCO_PN_Freq = VCO_PN_F; % From Parameters.m  
VCO_PN_Level = VCO_PN_L; % From Parameters.m

- **Purpose**:  
  Defines the frequency offsets and phase noise levels for reference, charge pump, and VCO. These values are used to compute the overall phase noise.
- **Explanation**:  
  - **`Ref_PN_Freq`** and **`Ref_PN_Level`**: Frequency offsets and phase noise levels for the reference source.  
  - **`CP_PN_Freq`** and **`CP_PN_Level`**: Frequency offsets and phase noise levels for the charge pump.  
  - **`VCO_PN_Freq`** and **`VCO_PN_Level`**: Frequency offsets and phase noise levels for the VCO, imported from **Parameters.m**.

---

### **3. Frequency Range for Analysis**
**Code**:  
freqv = logspace(log10(min(VCO_PN_Freq)), log10(max(VCO_PN_Freq)), 500);

- **Purpose**:  
  Generates a logarithmic frequency vector (`freqv`) for the analysis, ranging from the minimum to the maximum frequency values of the VCO phase noise.

---

### **4. Interpolate Noise Profiles**
**Code**:  
Ref_Phase_Noise_dB = interp1(log10(Ref_PN_Freq), Ref_PN_Level, log10(freqv), 'linear')';  
CP_Phase_Noise_dB = interp1(log10(CP_PN_Freq), CP_PN_Level, log10(freqv), 'linear')';  
VCO_Phase_Noise_dB = interp1(log10(VCO_PN_Freq), VCO_PN_Level, log10(freqv), 'linear')';

- **Purpose**:  
  Interpolates the phase noise data for each source (reference, charge pump, VCO) over the frequency range defined by `freqv`. This creates smoother phase noise profiles for analysis.

---

### **5. Compute Overall Phase Noise**
**Code**:  
H_REF2VCO = abs(squeeze(freqresp(CL_TF, 2*pi*freqv)));  
H_REF2VCO_dB = 20*log10(H_REF2VCO);  

PN_FROM_REF = 10.^(Ref_Phase_Noise_dB / 10) .* (H_REF2VCO.^2);  
PN_TOTAL = PN_FROM_REF; % Add other noise sources if needed.

- **Purpose**:  
  Computes the overall phase noise contribution from the reference signal.
- **Explanation**:  
  - **`H_REF2VCO`**: Computes the frequency response of the closed-loop transfer function (`CL_TF`) at the frequencies defined by `freqv`.  
  - **`H_REF2VCO_dB`**: Converts the frequency response to decibels.  
  - **`PN_FROM_REF`**: Computes the phase noise contribution from the reference signal using the interpolated phase noise values and the transfer function response.  
  - **`PN_TOTAL`**: Currently only includes the reference noise, but can be extended to include noise from other sources like the charge pump and VCO.

---

### **6. Plot Results - Phase Noise Spectrum**
**Code**:  
figure('Name', 'Phase Noise Spectrum', 'NumberTitle', 'off');  
semilogx(freqv, 10*log10(PN_TOTAL), 'k', 'LineWidth', 2);  
xlabel('Frequency (Hz)');  
ylabel('Phase Noise (dBc/Hz)');  
title('Overall Phase Noise Spectrum');  
grid on;

- **Purpose**:  
  Generates a plot of the overall phase noise spectrum in dBc/Hz, visualizing the noise contribution over the frequency range.

---

### **7. Plot Results - Step Response**
**Code**:  
figure('Name', 'Step Response', 'NumberTitle', 'off');  
plot(t, y);  
xlabel('Time (s)');  
ylabel('Amplitude');  
title('Step Response: Closed-Loop Transfer Function');  
grid on;

- **Purpose**:  
  Plots the step response of the closed-loop transfer function, showing the time-domain behavior of the system.

---

### **8. Plot Results - Open-Loop Magnitude Response**
**Code**:  
figure('Name', 'Open-Loop Magnitude Response', 'NumberTitle', 'off');  
semilogx(w/(2*pi), mag_dB);  
xlabel('Frequency (Hz)');  
ylabel('Magnitude (dB)');  
title('Open-Loop Frequency Response');  
grid on;

- **Purpose**:  
  Plots the open-loop magnitude response in dB, showing how the system's gain varies with frequency.

---

### **9. Compute RMS Jitter**
**Code**:  
disp('Computing RMS jitter...');  
RMS_Jitter = (1 / (2*pi*N*Fref)) * sqrt(2 * trapz(freqv, 10.^(10*log10(PN_TOTAL) / 10)));  
disp(['RMS Jitter = ', num2str(RMS_Jitter * 1e12), ' ps']);

- **Purpose**:  
  Computes the root mean square (RMS) jitter from the total phase noise. Jitter represents the time-domain variation in the signal, often important in communication systems.
- **Explanation**:  
  - **`trapz`**: Performs numerical integration of the phase noise over the frequency range using the trapezoidal rule.  
  - **`RMS_Jitter`**: The RMS jitter is calculated by integrating the total phase noise and applying the formula for jitter in terms of phase noise. The result is converted to picoseconds.

---

This concludes the line-by-line explanation for **Analysis.m**. Let me know if you need further modifications or assistance!
