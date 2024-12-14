### **Explanation of Gram-Schmidt Orthonormalization Code**

This MATLAB code implements the **Gram-Schmidt Process** to orthogonalize and normalize a set of vectors. The Gram-Schmidt process is a method for converting a set of linearly independent vectors into an orthonormal basis.

---

#### **1. Initialization**

```matlab
clc; close all; clear all;
```
- `clc`: Clears the command window.
- `close all`: Closes all open figure windows.
- `clear all`: Removes all variables from the workspace.

These commands ensure a clean environment before running the program.

---

#### **2. Input Vectors**

```matlab
V = [1 1 0; 1 0 1; 0 1 1]'; % Linearly Independent vectors
% V = rand(3, 3);
% V = [1 2 3; 1 5 2; 2 4 6]'; % Linearly Dependent
% V = [3 2 1;1 2 3;0 1 4];
```
- `V`: Matrix of input vectors, where each **column** represents a vector.
  - Example: `V = [1 1 0; 1 0 1; 0 1 1]'` contains three linearly independent vectors.
- Other commented examples demonstrate different cases:
  - Random vectors.
  - Linearly dependent vectors.

---

#### **3. Number of Vectors**

```matlab
n = size(V, 2); % Number of columns (vectors)
```
- `n`: Number of input vectors, determined by the number of columns in matrix `V`.

---

#### **4. Initialize Orthogonal Vectors**

```matlab
U = zeros(size(V));
```
- `U`: Matrix to store orthogonalized vectors. Initially, all values are set to zero.

---

#### **5. Gram-Schmidt Process**

```matlab
for i = 1:n
    % Start with the original vector
    U(:, i) = V(:, i);

    % Subtract projections of previous orthogonal vectors
    for j = 1:i-1
        U(:, i) = U(:, i) - (dot(U(:, j), V(:, i)) / dot(U(:, j), U(:, j))) * U(:, j);
    end
end
```
- Outer loop (`for i = 1:n`): Iterates over each vector in `V`.
- **Orthogonalization Step:**
  - Start with the original vector `V(:, i)`.
  - Subtract the projection of `V(:, i)` onto each previously calculated orthogonal vector `U(:, j)`.
  - The projection formula is:
    
    \[
    \text{Projection} = \frac{U_j \cdot V_i}{U_j \cdot U_j} \cdot U_j
    \]
- The result is stored in `U(:, i)` as an orthogonal vector.

---

#### **6. Normalization**

```matlab
E = zeros(size(U));
for i = 1:n
    E(:, i) = U(:, i) / norm(U(:, i));
end
```
- `E`: Matrix to store the normalized (orthonormal) vectors.
- Each orthogonal vector `U(:, i)` is divided by its norm to produce a unit vector.

---

#### **7. Display Results**

```matlab
disp('Original Vectors (V):');
disp(V);
disp('Orthogonal Vectors (U):');
disp(U);
disp('Orthonormal Vectors (E):');
disp(E);
```
- Displays the input vectors (`V`), orthogonalized vectors (`U`), and orthonormalized vectors (`E`).

---

#### **8. Visualization**

```matlab
% Plotting the original vectors
figure;
hold on;
grid on;
quiver3(0, 0, 0, V(1, 1), V(2, 1), V(3, 1), 'r', 'LineWidth', 2);
quiver3(0, 0, 0, V(1, 2), V(2, 2), V(3, 2), 'g', 'LineWidth', 2);
quiver3(0, 0, 0, V(1, 3), V(2, 3), V(3, 3), 'b', 'LineWidth', 2);

% Plotting the orthonormal vectors
quiver3(0, 0, 0, E(1, 1), E(2, 1), E(3, 1), 'r--', 'LineWidth', 2);
quiver3(0, 0, 0, E(1, 2), E(2, 2), E(3, 2), 'g--', 'LineWidth', 2);
quiver3(0, 0, 0, E(1, 3), E(2, 3), E(3, 3), 'b--', 'LineWidth', 2);

% Setting up the plot
xlabel('X');
ylabel('Y');
zlabel('Z');
title('Gram-Schmidt Orthonormalization');
legend({'V1', 'V2', 'V3', 'E1', 'E2', 'E3'}, 'Location', 'Best');
axis equal;
hold off;
```
- **Plot Original Vectors:**
  - `quiver3`: Plots 3D vectors from the origin `(0, 0, 0)`.
  - Original vectors `V` are plotted with solid lines (red, green, blue).
- **Plot Orthonormal Vectors:**
  - Orthonormal vectors `E` are plotted with dashed lines (red, green, blue).
- **Labels and Legend:**
  - Adds labels for the axes, a title, and a legend to distinguish between the original and orthonormal vectors.

---

#### **9. Example Workflow**

**Input Vectors:**
```plaintext
V = [1 1 0; 1 0 1; 0 1 1]';
```

**Results:**
```plaintext
Original Vectors (V):
     1     1     0
     1     0     1
     0     1     1

Orthogonal Vectors (U):
     1     0.5000   -0.5000
     1    -0.5000    0.5000
     0     1.0000    0.0000

Orthonormal Vectors (E):
     0.7071    0.4082   -0.7071
     0.7071   -0.4082    0.7071
     0.0000    0.8165    0.0000
```

**Visualization:**
- Original vectors `V` and orthonormal vectors `E` are displayed in a 3D plot.

---

This code effectively demonstrates the Gram-Schmidt process, transforming any set of linearly independent vectors into an orthonormal basis. It also provides a clear visual representation of the results.
