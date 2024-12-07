# 2021-SE-12-Assignment-02-CV



# Harris Corner Detection Algorithm

Harris Corner Detection is a widely used algorithm in computer vision to detect corners (points of interest) in an image. Corners are regions with high variation in intensity in all directions, making them robust features for matching and recognition tasks.

---

## **Mathematical Formulation**

### **1. Corner Definition**
A corner is defined as a point in an image where shifts in any direction lead to significant changes in intensity. Mathematically, this is captured by the **autocorrelation function**:

\[
E(u, v) = \sum_{x,y} w(x, y) \left[ I(x+u, y+v) - I(x, y) \right]^2
\]

Where:
- \(E(u, v)\): Change in intensity due to a shift by \((u, v)\).
- \(I(x, y)\): Intensity of the pixel at \((x, y)\).
- \(w(x, y)\): A window function (e.g., Gaussian) to weight contributions of neighboring pixels.

### **2. Taylor Series Approximation**
The intensity change can be approximated using the first-order Taylor expansion:

\[
I(x+u, y+v) \approx I(x, y) + u \frac{\partial I}{\partial x} + v \frac{\partial I}{\partial y}
\]

Substituting this back into \(E(u, v)\), we get:

\[
E(u, v) = \sum_{x,y} w(x, y) \left[ u I_x + v I_y \right]^2
\]

Where:
- \(I_x = \frac{\partial I}{\partial x}\): Gradient in the x-direction.
- \(I_y = \frac{\partial I}{\partial y}\): Gradient in the y-direction.

### **3. Matrix Form**
Rewriting in matrix form:

\[
E(u, v) = \begin{bmatrix} u & v \end{bmatrix}
\begin{bmatrix} A & B \\ B & C \end{bmatrix}
\begin{bmatrix} u \\ v \end{bmatrix}
\]

Where:
- \(A = \sum w(x, y) I_x^2\): Sum of squared gradients in x.
- \(B = \sum w(x, y) I_x I_y\): Sum of product of gradients in x and y.
- \(C = \sum w(x, y) I_y^2\): Sum of squared gradients in y.

The matrix:
\[
M = \begin{bmatrix} A & B \\ B & C \end{bmatrix}
\]
is called the **structure tensor**.

### **4. Corner Response Function**
To classify points as corners, edges, or flat regions, the eigenvalues (\(\lambda_1, \lambda_2\)) of \(M\) are analyzed:

- Flat Region: \(\lambda_1 \approx \lambda_2 \approx 0\)
- Edge: One eigenvalue is large, the other is small (\(\lambda_1 >> \lambda_2\) or vice versa).
- Corner: Both eigenvalues are large (\(\lambda_1\) and \(\lambda_2\) are high).

The Harris Corner Detector simplifies this analysis using the **Corner Response Function (R)**:

\[
R = \text{det}(M) - k \cdot (\text{trace}(M))^2
\]

Where:
- \(\text{det}(M) = AC - B^2\): Determinant of \(M\).
- \(\text{trace}(M) = A + C\): Trace of \(M\).
- \(k\): Sensitivity parameter (typically \(k = 0.04\)).

### **5. Corner Detection Criteria**
- A corner is detected if \(R > \text{threshold}\).



## **Steps in the Algorithm**

1. **Compute Gradients**:
   - Calculate \(I_x\) and \(I_y\) using filters like Sobel or Scharr.
   
2. **Construct Structure Tensor**:
   - Compute \(A\), \(B\), and \(C\) using a weighted window function.
   
3. **Compute Corner Response**:
   - Use the formula \(R = \text{det}(M) - k \cdot (\text{trace}(M))^2\).
   
4. **Thresholding**:
   - Mark points with \(R > \text{threshold}\) as corners.
   
5. **Non-Maximum Suppression**:
   - Retain only local maxima to get precise corner locations.



## **Advantages**
- Efficient and robust.
- Detects corners invariant to rotation.

## **Disadvantages**
- Not scale-invariant.
- Sensitive to noise; preprocessing may be required.



## **Visualization**

A corner in an image appears at the intersection of two edges, and the algorithm identifies such points by analyzing changes in intensity.

**Example Output**
Original Image: Displays the user-uploaded image.
Harris Corner Detection: Corners are highlighted in red for color images or white for grayscale images.
i use the image department of softwae engineering.
<img width="704" alt="corner detection" src="https://github.com/user-attachments/assets/2a756d98-2b34-4a16-864e-6ba193be0ffc">



