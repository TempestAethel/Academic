# QUESTION BANK

### 1. Consider a (6,3) linear block code whose generator matrix is given by:
   - (i) Find the parity check matrix.
   - (ii) Find the minimum distance of the code.
   - (iii) Draw the encoder and syndrome computation circuit.

### 2. Design a linear block code with a minimum distance of 3 and a message block size of 8 bits.

### 3. If ‘C’ is a valid code vector such as **C = DG**, then prove that **C * H^T = 0**, where H is the parity check matrix.

### 4. In a linear block code, the syndrome is given by:
   - **S1 = r1 + r2 + r3 + r5**
   - **S2 = r1 + r2 + r4 + r6**
   - **S3 = r1 + r3 + r4 + r7**
   - Find:
     - Generator matrix [G]
     - Parity check matrix [H]
     - Write encoder and decoder circuit.
     - Find the code word for all the messages.
     - How many errors it can detect and correct.
     - Write the standard array.
     - Find the syndrome for the received data **1011 011**.

### 5. Consider a (3,1,2) Convolution Encoder with **g(1) = 110**, **g(2) = 101**, and **g(3) = 111**:
   - (i) Draw the encoder diagram.
   - (ii) Find the code word for the message sequence **(11101)** using the Generator Matrix and Transform domain approach.

### 6. For a (2,1,3) Convolution Encoder with **g(1) = 1101** and **g(2) = 1011**:
   - (i) Write the transition table.
   - (ii) State diagram.
   - (iii) Draw the code tree.
   - (iv) Draw the trellis diagram.
   - (v) Find the encoded output for the message **(11101)** by traversing the code tree.

### 7. For a (7,4) binary cyclic code, the generator polynomial is given by **g(x) = 1 + x + x³**:
   - Find the generator and parity check matrices.

### 8. A (15,5) linear cyclic code has a generator polynomial **g(x) = 1 + x + x² + x⁴ + x⁵ + x⁸ + x¹⁰**:
   - Draw the block diagram of an encoder and syndrome calculator circuit for this code.
   - Find the code polynomial for the message polynomial **D(x) = 1 + x² + x⁴** (in systematic form).
   - Is **V(x) = 1 + x⁴ + x⁶ + x⁸ + x¹⁴** a code polynomial? If not, find the syndrome of **V(x)**.

### 9. In a (7,4) binary cyclic code, the generator polynomial is given by **g(x) = 1 + x + x³**:
   - Find the codeword for messages **(1001)** and **(1011)**.
   - Show the contents of registers at each step.

### 10. Derive the expression for the probability of error considering coherent Binary Phase Shift Keying (BPSK) signal.

### 11. An FSK system transmits binary data at the rate of **2 x 10⁶ bps**. During transmission, AWGN with zero mean and two-sided PSD **10⁻²⁰ W/Hz** is added to the signal. The amplitude of the received sinusoidal wave for digit 1 or 0 is **1 μV**. Determine the average probability of symbol error assuming non-coherent detection.

### 12. A binary data is transmitted over AWGN channel using BPSK at the rate of **2 Mbps**. It is desired to have average probability of error **Pe ≤ 10⁻⁵**, with noise spectral density **No/2 = 10⁻¹² W/Hz**. Determine the average carrier power required at the receiver input if the detector is of coherent type. Take **erfc(3.5) = 0.00025**.

### 13. Explain Non-coherent BFSK detection with relevant equations and explanation.

### 14. Define the Hilbert Transform. State the properties of it.

### 15. Define the complex envelope of bandpass signals. Obtain the canonical representation of bandpass signals.

### 16. Explain the Gram-Schmidt Orthogonalization procedure.

### 17. Derive the expressions for mean and variance of the correlator outputs. Also, show that the correlator outputs are statistically independent (or) the conversion of the Continuous AWGN Channel into a Vector Channel.

### 18. Derive the expression for the probability of error in a coherent **binary phase shift keying (BPSK)** system.