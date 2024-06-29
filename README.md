# Demystifying B-spline

While studying [Kolmogorov-Arnold Networks](https://github.com/KindXiaoming/pykan), I realized that I didn't fully understand B-splines. To aid my comprehension, I used the [manim](https://github.com/3b1b/manim) library to create visual resources.

## What is B-spline?

B-splines are mathematical functions used to construct smooth curves. [Spline functions are created as linear combinations of B-splines with a set of control points.](https://en.wikipedia.org/wiki/B-spline)

$$
\begin{align}
\displaystyle
S(t) &= \sum_{i = 0}^{m - n - 2} P_i b_{i, n} (t),\qquad t \in [t_n, t_{m-n-1}]
\\
\nonumber \\
b_{j, 0}(t) &:=
\begin{cases}
1 & \text{if } t_j \leq t \lt t_{j+1} \\
0 & \text{otherwise}
\end{cases}
,\qquad j = 0, \dots, m-2
\\
b_{j, n}(t) &:= \cfrac{t - t_j}{t_{j + n}-t_j} b_{j, n-1} (t) + \cfrac{t_{j+n+1} - t}{t_{j + n + 1} - t_{j + 1}} b_{j + 1, n- 1} (t),\qquad j = 0, \dots, m - n - 2.

\end{align}
$$
- [B-spline formula](https://ko.wikipedia.org/wiki/B-%EC%8A%A4%ED%94%8C%EB%9D%BC%EC%9D%B8_%EA%B3%A1%EC%84%A0)
- NOTE: $t_i\ (\text{knots}) \neq t$

> [!TIP] A B-spline is a curve defined by a `basis function` and `control points`.

## What is a Basis function ($b_{i, n}$)?

Basis function $b_{i, n}$ is composed of a `knots vector` $t_{..}$ and `degree` $n$.
- input $t$ is the $x$ value of curve function (2-d)
- $i$ is the index corresponding to the control point
    - We said that a B-spline is a linear combination of control points and basis functions.
    - In this context, we can say that $i$ represents the index of the control point to be multiplied by corresponding basis function.

Let's examine how the components (`knots vector`, `degree`) affect the basis function.

### How `changing the degree` affects the `shape of the basis function`

<video src="./1_basis_function_degree.mp4" controls></video>

### How `changing the control point index` $i$ affects the `position of a single basis function`

This example demonstrates the role of the control point index.
As the value increases, the knots referenced to create the basis function change slightly.

<video src="./2_basis_function.mp4" controls></video>

### How `changing the knots position` affects the `shape of the basis function`

Compare this to the previous video to see how changes in knots impact the basis function.

<video src="./3_basis_function_change_knots.mp4" controls></video>

## How do `Control points` affect the `shape of the curve`?

Now that we've seen how components of a basis function affect its construction, let's examine how control points influence the final B-spline curve.

<video src="./4_b_spline.mp4" controls></video>
