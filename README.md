# Comparison of Thomas Algorithm and Gauss-Jordan Method for Solving Tridiagonal Systems

### Detailed Explanation of the Code

This program compares the **Thomas Algorithm** and the **Gauss-Jordan Method** for solving tridiagonal systems of linear equations. It evaluates their performance by measuring CPU time and residual errors across a range of problem sizes, visualizing the results with plots.

---

#### **1. Libraries Used**
- **`numpy`**:  
  Provides efficient numerical operations such as random number generation and matrix manipulations.  
- **`scipy.sparse`**:  
  Optimizes memory usage and computation for sparse matrices, which are predominantly zero-valued.  
- **`time`**:  
  Measures execution time for evaluating algorithm performance.  
- **`matplotlib.pyplot`**:  
  Generates visualizations to compare the performance metrics of the algorithms.  

---

#### **2. Function: `generate_uniform_tridiagonal_system(n, seed=0)`**
This function creates a random tridiagonal matrix \( A \) and a right-hand side vector \( d \).

- **Inputs**:  
  - `n`: Size of the matrix (number of equations).  
  - `seed`: Seed for reproducible random number generation.  

- **Outputs**:  
  - `a`: Sub-diagonal of the tridiagonal matrix (\(n-1\) elements).  
  - `b`: Main diagonal (\(n\) elements, made diagonally dominant).  
  - `c`: Super-diagonal (\(n-1\) elements).  
  - `d`: Right-hand side vector (\(n\) elements).  

- **Explanation**:  
  The diagonals are randomly generated using `np.random.uniform()`. The main diagonal is adjusted to ensure diagonal dominance, enhancing numerical stability.  

---

#### **3. Function: `thomas_algorithm(a, b, c, d, precision_threshold=1e-12)`**
Implements the **Thomas Algorithm**, specifically designed for tridiagonal systems.  

- **Inputs**:  
  - `a`, `b`, `c`: Sub-diagonal, main diagonal, and super-diagonal of the matrix.  
  - `d`: Right-hand side vector.  
  - `precision_threshold`: Detects near-singular matrices.  

- **Steps**:
  1. **Forward Elimination**:  
     - Reduces the system to an upper triangular matrix.  
  2. **Backward Substitution**:  
     - Solves the upper triangular system for \( x \).  

- **Output**:  
  - The solution vector \( x \).  

- **Error Handling**:  
  If a division by zero or near-zero occurs during elimination, the function raises an exception.  

---

#### **4. Function: `gauss_jordan(A, b, precision_threshold=1e-12)`**
This function performs **Gauss-Jordan Elimination** on a general dense matrix.  

- **Inputs**:  
  - `A`: Coefficient matrix (dense).  
  - `b`: Right-hand side vector.  

- **Steps**:  
  1. Augments \( A \) with \( b \).  
  2. Performs row operations to transform the matrix into reduced row echelon form.  

- **Output**:  
  - The solution vector \( x \).  

- **Error Handling**:  
  Similar to the Thomas Algorithm, it checks for singular matrices.  

---

#### **5. Function: `main()`**
This is the entry point for benchmarking and visualizing results.  

- **Steps**:  
  1. Define problem dimensions:  
     - `dimensions_thomas`: \(10^2\) to \(10^6\).  
     - `dimensions_gauss_jordan`: Limited to \(10^2\) and \(10^3\) (due to its cubic complexity).  

  2. Initialize lists to store CPU times and residual errors.  

  3. Loop through dimensions for each algorithm:  
     - **Thomas Algorithm**:  
       - Generates a tridiagonal system.  
       - Measures execution time and calculates residual error (\( ||Ax - d|| \)).  
     - **Gauss-Jordan Method**:  
       - Uses a dense matrix representation.  
       - Performs similar measurements.  

  4. Plot results using `matplotlib`:  
     - **X-axis**: Problem size (\( n \)).  
     - **Y-axis**:  
       - CPU time in seconds (logarithmic scale).  
       - Residual error (logarithmic scale).  

---

#### **6. Visualization**
The program generates two subplots:  

1. **CPU Time Comparison**:  
   - Orange markers: Thomas Algorithm (efficient for all problem sizes).  
   - Red markers: Gauss-Jordan Method (computationally infeasible for large \( n \)).  

2. **Residual Error Comparison**:  
   - Both algorithms achieve low residual errors, demonstrating numerical accuracy.  

---

#### **7. Results and Insights**
1. **Execution Time**:  
   - Thomas Algorithm scales linearly with \( n \), making it suitable for very large systems.  
   - Gauss-Jordan’s cubic complexity leads to significant slowdowns for \( n \geq 10^4 \).  

2. **Residual Errors**:  
   - Both methods achieve comparable residual errors, confirming correctness.  

3. **Scalability**:  
   - Thomas Algorithm demonstrates superior scalability due to its design for tridiagonal matrices.  

---

### Sample Output Graph

The plot visualizes:
- **Efficiency**: Thomas Algorithm outperforms Gauss-Jordan in CPU time as \( n \) increases.  
- **Accuracy**: Both methods provide accurate solutions with minimal residual errors.  

![download](https://github.com/user-attachments/assets/1e947a43-69cb-455c-83d7-67b770222829)

---

#### **Why These Dimensions Were Chosen**
The dimensions span moderate (\(10^2\)) to very large systems (\(10^6\)), showcasing both methods' performance trends. Gauss-Jordan is limited to smaller dimensions due to its computational cost.

---

### ***To run .tex files:***
use command: ***xelatex -shell-escape filename.tex***
