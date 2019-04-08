# Approximation

Let `obj` be a subclass of `MwlsObject`.
The function call `obj(pt::Point)` returns the approximated function value at `pt`.
This calls the [`approximate`](@ref) function.

## Example

Let's initialize a dataset with input data `xs` and output data `fs`.

```@example approx
using MovingWeightedLeastSquares # hide
xs = collect(-2:0.1:2);
fs = [sin(x) for x in xs];
```

Now let's construct an approximation object `obj`.
Let's choose a weighting function ``\theta(d) = \exp(d^2)``.

```@example approx
obj = mwls_kd(xs, fs, 0.5, (d, e) -> (exp(-d^2)));
```

The approximation at 1 can be obtained by using

```@example approx
obj(1)
```

If a different range of neighbor data is needed, then use

```@example approx
obj(1, 1)
```

## Relevant documentation

```@docs
approximate
mwls_coefficients
```

# Approximation of derivative

## Example

Approximation of first derivative on the dataset from the previous example can be done by using

```@example approx
mwls_diff(obj, 1, 1)
```

Formally a tuple is required for specifying the orders of derivates for each variable.
Let ``f`` be the approximated function. For an example a tuple `(1, 2)` calculates
```math
\frac{\partial^3}{\partial x_1 \partial x_2^2}f.
```

## Relevant documentation

```@docs
mwls_diff
mwls_diff_polys
```

