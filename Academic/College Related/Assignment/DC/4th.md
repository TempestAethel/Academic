# Convolutional Code (3,1,2) Solution

## Question
Consider a (3,1,2) convolutional code with the following generator polynomials:
- \( g^{(1)} = 110 \)
- \( g^{(2)} = 101 \)
- \( g^{(3)} = 111 \)

i) Draw the encoder block diagram.  
ii) Draw the state table.  
iii) Draw the state diagram.  
iv) Draw the code tree and find encoder output for the message sequence \( 11100 \).

---

## Solution

### (i) Encoder Block Diagram

A (3,1,2) convolutional code means:
- 1 input bit per time step.
- 3 output bits per time step.
- Constraint length \( K = 2 \) (involving 2 memory elements).

The generator polynomials are:
- \( g^{(1)} = 110 \)
- \( g^{(2)} = 101 \)
- \( g^{(3)} = 111 \)

The encoder consists of:
- 1 input bit \( u \).
- Two memory elements \( M_1 \) and \( M_2 \).
- Three output bits: \( v_1, v_2, v_3 \), defined by the following equations:
  - \( v_1 = u \oplus M_1 \)
  - \( v_2 = u \oplus M_2 \)
  - \( v_3 = u \oplus M_1 \oplus M_2 \)

This can be represented with shift registers connected to the outputs as per the generator polynomials.

---

### (ii) State Table

States are defined by the contents of the memory elements \( M_1 \) and \( M_2 \), and each state corresponds to a 2-bit value. The state table lists:
1. Current state (\( S_{curr} \)).
2. Input (\( u \)).
3. Next state (\( S_{next} \)).
4. Output (\( v_1, v_2, v_3 \)).

| Current State (\( M_1, M_2 \)) | Input (\( u \)) | Next State (\( M_1', M_2' \)) | Output (\( v_1, v_2, v_3 \)) |
|-------------------------------|----------------|--------------------------------|-----------------------------|
| 00                            | 0              | 00                             | 000                         |
| 00                            | 1              | 10                             | 111                         |
| 01                            | 0              | 00                             | 011                         |
| 01                            | 1              | 10                             | 100                         |
| 10                            | 0              | 01                             | 101                         |
| 10                            | 1              | 11                             | 010                         |
| 11                            | 0              | 01                             | 110                         |
| 11                            | 1              | 11                             | 001                         |

---

### (iii) State Diagram

The state diagram visually represents transitions between states based on the input bit (\( u \)) and includes the corresponding output.  

For each state (\( S_{curr} \)):
- Two branches emerge for \( u = 0 \) and \( u = 1 \), leading to \( S_{next} \) and producing an output.

---

### (iv) Code Tree and Output

To construct the code tree:
1. Start at the initial state (\( 00 \)).
2. Expand branches for \( u = 0 \) and \( u = 1 \) recursively, following the state transitions and outputs.
3. Mark the corresponding outputs on each branch.

For the input sequence \( 11100 \):
1. \( u = 1 \): From \( 00 \), move to \( 10 \), output \( 111 \).
2. \( u = 1 \): From \( 10 \), move to \( 11 \), output \( 010 \).
3. \( u = 1 \): From \( 11 \), stay in \( 11 \), output \( 001 \).
4. \( u = 0 \): From \( 11 \), move to \( 01 \), output \( 110 \).
5. \( u = 0 \): From \( 01 \), move to \( 00 \), output \( 011 \).

The final encoded sequence: **111 010 001 110 011**.
