# CRC Error Detection in Data Transmission

## Overview
This program simulates the process of transmitting data with a Cyclic Redundancy Check (CRC). It allows for:
1. Data input and appending of zeros based on the generator polynomial.
2. Calculation of the checksum (CRC code).
3. Optionally introducing an error in the transmitted data.
4. Checking if the received data has errors based on the checksum.

### Step-by-Step Breakdown

### Step 1: Define the Required Variables

```
char t[28], cs[28], g[] = "1101";  // Data array t, checksum array cs, and generator polynomial g[]
int a, e, c;  // Variables for lengths and iteration
#define N strlen(g)  // The length of the generator polynomial
```
- **`t[28]`**: This array holds the data to be transmitted, including the appended zeros.
- **`cs[28]`**: This array holds the calculated checksum.
- **`g[] = "1101"`**: The generator polynomial, which is used to compute the CRC. The generator polynomial can vary depending on the CRC standard.
- **`N`**: Defines the length of the generator polynomial, which is used in various loops.

### Step 2: Input Data and Prepare the Modified Data

```
printf("Enter the Data: ");
scanf("%s", t);  // Input the data string

printf("\nThe Generator Polynomial is: %s\n", g);  // Display the generator polynomial

a = strlen(t);  // Length of the data entered

// Append N-1 zeros to the data string
for (e = a; e < a + N - 1; e++)
    t[e] = '0';  // Pad the data with zeros to the required length
```
- **`scanf("%s", t)`**: Reads the data entered by the user.
- **`a = strlen(t)`**: Calculates the length of the input data string.
- **Appending zeros**: The data is padded with `N-1` zeros to make space for the checksum.

### Step 3: Compute the CRC (Checksum)

```
crc();  // Call the function to compute the CRC (checksum)
printf("\nChecksum is: %s\n", cs);  // Display the checksum
```
- **`crc()`**: This function calculates the checksum based on the generator polynomial and the padded data.

### Step 4: Construct the Final Codeword

```
for (e = a; e < a + N - 1; e++)
    t[e] = cs[e - a];  // Replace the padded zeros with the checksum

printf("\nThe Final Codeword is: %s\n", t);  // Display the final codeword (data + checksum)
```
- The checksum is inserted into the data at the positions that were previously padded with zeros.
- The final codeword is the data concatenated with the checksum.

### Step 5: Introduce Errors for Testing

```
printf("\nTest Error Detection 0(YES) 1(NO)? :");
scanf("%d", &e);  // Ask if the user wants to introduce an error

if (e == 0) {
    do {
        printf("\nEnter the position where Error is to be inserted: ");
        scanf("%d", &e);  // Ask the user for the position to insert the error
    } while (e == 0 || e > a + N - 1);  // Ensure the position is valid

    t[e - 1] = (t[e - 1] == '0') ? '1' : '0';  // Flip the bit at the specified position to introduce an error
    printf("\nErroneous Data: %s\n", t);  // Display the erroneous data
}
```
- **Introduce Error**: If the user chooses to introduce an error, they specify the position, and the bit at that position is flipped (from `0` to `1` or vice versa).

### Step 6: Perform CRC Again and Detect Errors

```
crc();  // Call the function to recompute the CRC

for (e = 0; (e < N - 1) && (cs[e] != '1'); e++);  // Check if the CRC has any '1' indicating an error

if (e < N - 1)
    printf("\nError Detected\n");  // If any '1' is found in the checksum, an error is detected
else
    printf("\nNo Error Detected\n");  // If no '1' is found, the data is error-free
```
- **`crc()`**: Recomputes the CRC with the possibly erroneous data.
- **Error Detection**: The program checks if any non-zero remainder (indicated by a '1') exists in the checksum after recomputing it. If found, it indicates an error.

### Functions Used in the Program

1. **`crc()`**: This function is responsible for calculating the CRC checksum.
   - The function uses XOR operations to process the data and generator polynomial bit-by-bit.
   - **`xor()`**: This helper function performs an XOR operation on the bits of the current remainder (`cs[]`) with the generator polynomial (`g[]`).

2. **`xor()`**: This function handles the XOR operation used during the CRC calculation.
   ```
   for (c = 1; c < N; c++)
       cs[c] = ((cs[c] == g[c]) ? '0' : '1');  // Perform XOR operation
   ```
   - This function is used to modify the current checksum based on the generator polynomial.

### Conclusion
This program demonstrates how CRC error detection works by appending a checksum to transmitted data. It also shows how errors in the data can be detected by recomputing the checksum at the receiver's end. The ability to simulate errors and check for them is a key feature of the CRC algorithm used in data communication systems.
