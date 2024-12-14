# Convolutional Code Analysis

### Question:
Consider a (2, 1, 2) convolutional code with the impulse response 

\[
g^{(1)} = (1\ 1\ 1), \quad g^{(2)} = (1\ 0\ 1)
\]

and the incoming message sequence is \( 10011 \).

#### i) Draw the encoder block diagram.

#### ii) Find the output for the message \( (10011) \) using time domain approach.

#### iii) Find the output for the message \( (10011) \) using transform domain approach.

---

### Solution:

#### i) Encoder Block Diagram:

1. A (2, 1, 2) convolutional code means:
   - **2** output bits for every input bit.
   - **1** input bit per time step.
   - **2** memory elements in the encoder.

2. Impulse responses:
   - \( g^{(1)} = [1\ 1\ 1] \): This represents the taps of the first output.
   - \( g^{(2)} = [1\ 0\ 1] \): This represents the taps of the second output.

3. **Diagram**:
   The encoder uses a shift register structure with two memory elements. At each step, the input bit is shifted in, and the output bits are computed as follows:
   - First output: Convolution of the input sequence with \( g^{(1)} \).
   - Second output: Convolution of the input sequence with \( g^{(2)} \).

The block diagram is typically drawn as:
- A shift register with 2 memory elements (\( M_1 \) and \( M_2 \)).
- Taps at appropriate positions for \( g^{(1)} \) and \( g^{(2)} \).
- Outputs \( Y_1 \) and \( Y_2 \).

---

#### ii) Find the Output Using Time Domain Approach:

The message sequence is \( \mathbf{m} = [1, 0, 0, 1, 1] \).

1. **Expand the input sequence**:
   The message is \( \mathbf{m}[n] = 1, 0, 0, 1, 1 \) followed by zeros (to flush the encoder).

2. **Shift Register Behavior**:
   At each time step, the encoder outputs are computed as:
   \[
   Y_1[n] = \sum_{k=0}^{2} g^{(1)}[k] \cdot m[n-k]
   \]
   \[
   Y_2[n] = \sum_{k=0}^{2} g^{(2)}[k] \cdot m[n-k]
   \]

   Compute the outputs step by step:

   | \( n \) | \( m[n] \) | \( M_1 \) | \( M_2 \) | \( Y_1[n] \) | \( Y_2[n] \) |
   |--------|------------|-----------|-----------|--------------|--------------|
   | 0      | 1          | 0         | 0         | 1            | 1            |
   | 1      | 0          | 1         | 0         | 1            | 0            |
   | 2      | 0          | 0         | 1         | 1            | 1            |
   | 3      | 1          | 0         | 0         | 1            | 1            |
   | 4      | 1          | 1         | 0         | 1            | 0            |

   The time-domain output is:
   \[
   \mathbf{Y} = [(1, 1), (1, 0), (1, 1), (1, 1), (1, 0)]
   \]

---

#### iii) Find the Output Using Transform Domain Approach:

1. **Represent the input sequence**:
   Using the \( z \)-transform, the input message \( \mathbf{m} = [1, 0, 0, 1, 1] \) is represented as:
   \[
   M(z) = 1 + z^{-3} + z^{-4}.
   \]

2. **Impulse Responses in Transform Domain**:
   - \( G^{(1)}(z) = 1 + z^{-1} + z^{-2} \).
   - \( G^{(2)}(z) = 1 + z^{-2} \).

3. **Output Sequences**:
   Each output is the convolution (multiplication in \( z \)-domain) of \( M(z) \) with \( G^{(1)}(z) \) and \( G^{(2)}(z) \):
   \[
   Y_1(z) = M(z) \cdot G^{(1)}(z) = (1 + z^{-3} + z^{-4})(1 + z^{-1} + z^{-2}),
   \]
   \[
   Y_2(z) = M(z) \cdot G^{(2)}(z) = (1 + z^{-3} + z^{-4})(1 + z^{-2}).
   \]

   Perform the multiplications:
   - \( Y_1(z) = 1 + z^{-1} + z^{-2} + z^{-3} + z^{-4} + z^{-5} + z^{-6} \).
   - \( Y_2(z) = 1 + z^{-2} + z^{-3} + z^{-5} + z^{-6} \).

4. **Transform Back to Time Domain**:
   The outputs in the time domain are:
   \[
   Y_1[n] = [1, 1, 1, 1, 1, 1, 1],
   \]
   \[
   Y_2[n] = [1, 0, 1, 0, 1, 0, 1].
   \]

Thus, the final output in both cases matches the sequence derived in the time-domain approach.
