# Encoder Circuit for a (15,7) Cyclic Code

## Question:
The generator polynomial of a (15,7) cyclic code is \( g(x) = 1 + x + x^4 \). Draw the encoder circuit. Illustrate the encoding procedure by listing the state of the register with the message vector \( 10010110111 \).

## 1. Encoder Circuit Design

The generator polynomial \( g(x) = 1 + x + x^4 \) implies that the circuit requires a shift register of degree 4, corresponding to the largest power of \(x\) in \(g(x)\). Here's how the encoder circuit is structured:

- **Shift Register:** A 4-stage shift register.
- **Feedback Taps:** Taps at positions \(x^1\) and \(x^4\), derived from the generator polynomial \( g(x) = 1 + x + x^4 \).
- **Output:** The encoder outputs the message bits followed by the remainder from the shift register.

## 2. Encoding Procedure

The encoding involves two parts:
1. **Appending Zeros:** Append 4 zeros (equal to the degree of \( g(x) \)) to the message vector, making it \( 100101101110000 \).
2. **Shift and Feedback:** Process each bit of the extended message vector through the shift register while applying the feedback based on \( g(x) \).

### Initial Setup:
- Message vector: \( 10010110111 \).
- Initial state of shift registers: \([0, 0, 0, 0]\).

### Steps for Encoding:
Process each input bit sequentially while updating the shift registers and applying feedback:

1. Insert the input bit into the first register.
2. Update subsequent registers, shifting the previous values.
3. Apply feedback to the input bit based on the taps in \( g(x) \).

### Detailed Table of Register States:

The table below shows how the register state evolves:

| Step | Input Bit | Register State \([r_3, r_2, r_1, r_0]\) | Feedback Calculation |
|------|-----------|-----------------------------------------|-----------------------|
| 0    | 1         | [0, 0, 0, 1]                           | Feedback = 0 ⊕ 1 = 1 |
| 1    | 0         | [1, 0, 0, 0]                           | Feedback = 1 ⊕ 0 = 1 |
| 2    | 0         | [1, 1, 0, 0]                           | Feedback = 1 ⊕ 0 = 1 |
| 3    | 1         | [1, 1, 1, 1]                           | Feedback = 1 ⊕ 1 = 0 |
| 4    | 0         | [0, 1, 1, 1]                           | Feedback = 0 ⊕ 0 = 0 |
| 5    | 1         | [0, 0, 1, 1]                           | Feedback = 0 ⊕ 1 = 1 |
| 6    | 1         | [1, 0, 0, 1]                           | Feedback = 1 ⊕ 1 = 0 |
| 7    | 0         | [0, 1, 0, 0]                           | Feedback = 0 ⊕ 0 = 0 |
| 8    | 1         | [0, 0, 1, 0]                           | Feedback = 0 ⊕ 1 = 1 |
| 9    | 1         | [1, 0, 0, 1]                           | Feedback = 1 ⊕ 1 = 0 |
| 10   | 0         | [0, 1, 0, 0]                           | Feedback = 0 ⊕ 0 = 0 |
| 11   | 0         | [0, 0, 1, 0]                           | Feedback = 0 ⊕ 0 = 0 |
| 12   | 0         | [0, 0, 0, 1]                           | Feedback = 0 ⊕ 0 = 0 |
| 13   | 0         | [1, 0, 0, 0]                           | Feedback = 1 ⊕ 0 = 1 |
| 14   | 0         | [1, 1, 0, 0]                           | Feedback = 1 ⊕ 0 = 1 |

### Final Output Codeword:
- The codeword consists of the original message vector (\(10010110111\)) followed by the remainder in the shift register (\(1100\)).
- Final codeword: **100101101111100**.

## 3. Encoder Circuit Diagram

1. A 4-stage shift register.
2. XOR gates for feedback paths corresponding to \(x^1\) and \(x^4\).
