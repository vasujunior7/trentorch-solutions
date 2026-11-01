# Monte Carlo Estimation

Intermediate | data-science | simulation | probability

### The problem, from first principles

Many quantities worth knowing have no tidy formula: the expected profit of a pricing rule, the chance a project finishes late, the area of an awkward shape. Monte Carlo estimation replaces the formula with an experiment. Draw many random samples, compute what you care about on each one, and average. The law of large numbers says the average closes in on the true value, and a second fact, how fast the error shrinks, tells you how many samples you need. This question builds the estimator, two classic uses of it and the sample-size rule.

### From theory to code

Implement `monte_carlo_mean(f, sampler, n, rng)`, which estimates an expectation and its error, then `estimate_pi(n, rng)`, which estimates pi by throwing random points at a square, then `monte_carlo_integral(f, a, b, n, rng)`, which estimates a definite integral, then `samples_for_precision(std, target_se)`, which says how many samples reach a target error. The signatures and docstrings are already in the editor.

### Constraints

- `sampler(rng, n)` returns a 1D float array of `n` independent draws from the distribution of interest. `f` takes that array and returns an array of the same length, one value per draw.
- `monte_carlo_mean` calls `sampler(rng, n)` exactly once and returns `(estimate, standard_error)` as floats, where `estimate` is the mean of `f(samples)` and `standard_error` is its sample standard deviation (with `ddof=1`) divided by `sqrt(n)`. It requires `n >= 2`.
- `estimate_pi` draws `x = rng.random(n)` first and then `y = rng.random(n)`, counts the points with `x**2 + y**2 <= 1` and returns `4 * count / n` as a float.
- `monte_carlo_integral` draws `u = rng.uniform(a, b, size=n)` once and returns `(b - a) * mean(f(u))` as a float, where `f` is vectorized.
- `samples_for_precision` returns the smallest integer `n` with `std / sqrt(n) <= target_se`, that is `ceil((std / target_se) ** 2)`, as an int. It raises `ValueError` if `target_se <= 0`.

### Hints

<details>
<summary>Hint 1</summary>

An expectation is an average over the distribution, so an average over many draws from it estimates it. The standard error is the standard deviation of that average, which shrinks as the number of draws grows.

</details>

<details>
<summary>Hint 2</summary>

For pi, the quarter circle of radius 1 inside the unit square has area pi/4, so the fraction of random points that land inside it estimates pi/4.

</details>

<details>
<summary>Hint 3</summary>

To integrate, remember that the integral of f over an interval is the interval's length times the average value of f on it.

</details>
