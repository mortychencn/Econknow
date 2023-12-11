# Newton's Method for Solving Systems of Two Equations

Newton's Method is a numerical technique used for finding roots of equations and can be extended to systems of equations. This note explains how to apply Newton's Method to a system of two equations.

## System of Equations

Consider two functions \( f(x, y) \) and \( g(x, y) \) representing our system:

1. \( f(x, y) = 0 \)
2. \( g(x, y) = 0 \)

The goal is to find \( (x, y) \) that satisfy both equations.

## Newton's Method

This method uses iteration. Starting from an initial guess \( (x_0, y_0) \), it finds a sequence of points \( (x_n, y_n) \) converging to the solution.

### Iterative Formula

For a current approximation \( (x_n, y_n) \), the next approximation \( (x_{n+1}, y_{n+1}) \) is:

\[ \begin{bmatrix} x_{n+1} \\ y_{n+1} \end{bmatrix} = \begin{bmatrix} x_n \\ y_n \end{bmatrix} - J^{-1}(x_n, y_n) \cdot \begin{bmatrix} f(x_n, y_n) \\ g(x_n, y_n) \end{bmatrix} \]

Here, \( J^{-1}(x_n, y_n) \) is the inverse of the Jacobian matrix at \( (x_n, y_n) \).

### Jacobian Matrix

The Jacobian matrix \( J \) is:

\[ J = \begin{bmatrix} \frac{\partial f}{\partial x} & \frac{\partial f}{\partial y} \\ \frac{\partial g}{\partial x} & \frac{\partial g}{\partial y} \end{bmatrix} \]

### Example

Consider:

1. \( f(x, y) = x^2 + y^2 - 4 \)
2. \( g(x, y) = xy - 1 \)

Jacobian matrix:

$$
J = \left[ \begin{array}{cc}
2x & 2y \\
y & x 
\end{array} \right]
$$


\[ J = \begin{bmatrix} 2x & 2y \\ y & x \end{bmatrix} \]

### Iteration Steps

1. Start with \( (x_0, y_0) \).
2. Calculate \( J \) and \( J^{-1} \) at \( (x_n, y_n) \).
3. Compute \( (x_{n+1}, y_{n+1}) \).
4. Repeat until convergence.

## MATLAB Implementation

```matlab
function [x, y] = newtonsMethod2Eq(f, g, dfdx, dfdy, dgdx, dgdy, x0, y0, tol, maxIter)
    x = x0;
    y = y0;
    for i = 1:maxIter
        J = [dfdx(x, y) dfdy(x, y); dgdx(x, y) dgdy(x, y)];
        F = [f(x, y); g(x, y)];
        step = J \ (-F);
        x = x + step(1);
        y = y + step(2);
        
        if norm(step) < tol
            break;
        end
    end
end
