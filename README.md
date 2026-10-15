# Credible interval coverage under misspecification

Code and generated results for [When 95% credible intervals cover 81%](https://aryasomu.com/writing/when-95-percent-credible-intervals-cover-81-percent.html).

The data are generated from independent normal observations with true mean zero and standard deviation `true_sd`. The fitted normal likelihood fixes the standard deviation at one and uses a `N(0, 10²)` prior on the mean. The experiment checks the repeated-sampling coverage of its central 95% posterior interval. It also reports an interval centered on the sample mean with a sample-variance standard error.

## Browse the results

- [Results table](outputs/results.csv): simulated posterior coverage, exact prediction, comparison-interval coverage, and estimated Monte Carlo standard errors for each true standard deviation. Values are proportions, so `0.8087` means `80.87%`.
- [Coverage figure](outputs/coverage.svg): exact posterior-coverage curve and simulated points. The article displays this figure inline.
- [Simulation code](simulate.py): Python standard library only, with a fixed seed.

## Reproduce

With Python 3.10 or newer, run from the repository root:

```sh
python3 simulate.py
```

The script overwrites `outputs/results.csv` and `outputs/coverage.svg`. The checked-in outputs were generated with Python 3.14.7 and seed `20261011`; exact random draws may vary across Python implementations or versions. It uses 50,000 datasets of size 100 for each of four true standard deviations and may take several seconds. No downloaded dataset or external package is needed.

The `posterior_mc_se` and `sandwich_mc_se` columns estimate simulation noise as `sqrt(coverage * (1 - coverage) / 50,000)`. They quantify uncertainty from the finite number of independently simulated datasets, not uncertainty about the exact theoretical posterior coverage. For example, at `true_sd = 1.5`, posterior coverage `0.80676` has a Monte Carlo standard error of about `0.00177`; its difference from the exact `0.80869` is about 1.1 such standard errors.

The comparison interval uses a normal 1.96 critical value and the sample standard error. Its coverage is about 94.7% at this sample size; a Student-t critical value would be more appropriate for that interval under the normal data-generating model. This toy example does not address dependent observations or misspecification that biases the pseudo-true mean.
