# Comparison of Thomas Algorithm and Gauss-Jordan Method for Solving Tridiagonal Systems in High Dimensions

### Detailed Explanation of the Code

This code compares two algorithms—**Thomas Algorithm** and **Gauss-Jordan Method**—for solving tridiagonal systems of linear equations. It evaluates the performance (in terms of CPU time) for problem sizes ranging from \(10^3\) to \(10^6\) and visualizes the results in a plot.

---

#### **1. Libraries Used**
- `numpy`:
  Provides tools for numerical computations, such as generating random numbers and performing matrix operations.
- `scipy.sparse`:
  Allows efficient handling of sparse matrices, which are matrices with mostly zero elements.
- `scipy.sparse.linalg.splu`:
  Provides an LU decomposition solver optimized for sparse matrices.
- `time`:
  Measures the time taken by various operations (CPU time).
- `matplotlib.pyplot`:
  Used to create the visualization comparing CPU times for the two algorithms.

---

#### **2. Function: `generate_uniform_tridiagonal_system(n, seed=0)`**
This function generates a random tridiagonal system of equations with \(n \times n\) matrices.

- **Inputs**:
  - `n`: Size of the tridiagonal matrix.
  - `seed`: Ensures reproducibility of the random numbers.

- **Outputs**:
  - `a`: Sub-diagonal elements (\(n-1\) elements).
  - `b`: Main diagonal elements (\(n\) elements).
  - `c`: Super-diagonal elements (\(n-1\) elements).
  - `d`: Right-hand side vector (\(n\) elements).
  - `A`: Sparse tridiagonal matrix \(A\) in CSC (Compressed Sparse Column) format.

- **Explanation**:
  - `np.random.uniform(1, 10, size=n-1)`: Generates random numbers between 1 and 10 for the sub-diagonal.
  - `diags([...])`: Constructs the sparse matrix using the diagonals.

---

#### **3. Function: `thomas_algorithm(a, b, c, d, precision_threshold=1e-12)`**
This function implements the **Thomas Algorithm**, an efficient solver for tridiagonal systems.

- **Inputs**:
  - `a`, `b`, `c`: Sub-diagonal, main diagonal, and super-diagonal of the tridiagonal matrix.
  - `d`: Right-hand side vector.
  - `precision_threshold`: Threshold to detect near-singular matrices.

- **Steps**:
  1. Compute forward elimination:
     - Reduces the tridiagonal matrix to an upper triangular form.
     - Arrays `c_prime` and `d_prime` store intermediate results.
  2. Compute back substitution:
     - Solves the upper triangular system for the solution vector \(x\).

- **Error Handling**:
  If the matrix is singular or nearly singular, an exception is raised.

- **Output**:
  - Solution vector \(x\).

---

#### **4. Function: `gauss_jordan_sparse(A, b)`**
This function uses the **Gauss-Jordan Method** with sparse matrix optimizations to solve the system.

- **Inputs**:
  - `A`: Sparse matrix in CSC format.
  - `b`: Right-hand side vector.

- **Steps**:
  1. LU decomposition via `splu(A)`:
     - Efficiently factorizes \(A\) into lower and upper triangular matrices.
  2. Solve the system using the LU factors.

- **Output**:
  - Solution vector \(x\).

---

#### **5. Function: `main()`**
This is the primary function that orchestrates the experiments, collects CPU time data, and plots the results.

- **Steps**:
  1. **Define Problem Dimensions**:
     - `dimensions = [10**3, 10**4, 10**5, 10**6]`:
       These dimensions are chosen to cover a wide range of problem sizes, showcasing the scalability of each algorithm.

  2. **Initialize Data Storage**:
     - `cpu_times_thomas` and `cpu_times_gauss_jordan`:
       Lists to store the CPU times for each algorithm.

  3. **Loop Through Dimensions**:
     - For each problem size:
       - Generate a random tridiagonal system.
       - Measure the CPU time for solving the system using:
         - Thomas Algorithm.
         - Gauss-Jordan Method.

  4. **Plot Results**:
     - Use `matplotlib` to create a comparison graph:
       - **X-axis (logarithmic)**: Problem dimension \(n\), showing growth patterns across several orders of magnitude.
       - **Y-axis (linear)**: CPU time in seconds.

  5. **Presentation Choices**:
     - Gridlines are included (`plt.grid()`) to improve readability.
     - The logarithmic scale for the x-axis emphasizes scalability differences.

---

#### **6. Visualization Details**
The graph provides a clear comparison:
- **Orange Line**: Thomas Algorithm (faster for large systems).
- **Red Line**: Gauss-Jordan Method (slower, especially for large dimensions due to cubic complexity).

---

#### **7. Key Features Highlighted**
- **Scalability Analysis**:
  Demonstrates how the performance of each algorithm changes with increasing problem size.

- **Readability**:
  The use of gridlines, markers, and labeled axes ensures that results are easy to interpret.

- **Logarithmic X-axis**:
  Emphasizes performance trends over several orders of magnitude.

---

### Why Were These Dimensions Chosen?
The selected dimensions align with standard benchmarks in computational experiments. They span from moderate (\(10^3\)) to very large systems (\(10^6\)), effectively illustrating:
- The scalability of each algorithm.
- How their computational costs grow with increasing problem size.

---

### Sample Example

![download](https://github.com/user-attachments/assets/672b95cd-39e7-4116-895f-78ceaa6ae2de)

