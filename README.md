# A/B Test Design & Simulation: Customer–Agent Matching

Does routing each customer to a **best-matched contact-center agent** increase sales conversion compared with the current routing?

This project designs the experiment end to end and validates the design with simulation before any real traffic is used. All numbers are **simulated assumptions**; no company data is included.

## Experiment design

| Item | Choice |
|---|---|
| Unit of randomization | Customer (not call), so a customer always stays in the same group |
| Control (A) | Current dialer routing |
| Treatment (B) | Customer routed to the best-matched agent (segment × agent score) |
| Primary metric | Policy conversion within 14 days of first call |
| Guardrail metrics | Reach rate, average talk time, calls per agent |
| Statistical test | Two-proportion z-test, α = 0.05, power = 0.80 |

## What the notebook covers

1. **Power analysis**: required sample size and test duration for a given minimum detectable effect (MDE)
2. **MDE trade-off**: how the sample size grows as the effect we want to detect gets smaller
3. **Analysis function**: conversion rates, relative uplift, 95% confidence interval and p-value
4. **A/A test**: checks that the false-positive rate stays close to 5% when there is no real effect
5. **Empirical power**: checks that a true effect is detected about 80% of the time
6. **Peeking problem**: shows how checking results daily and stopping early inflates false positives
7. **Decision rules**: ship criteria, guardrails, interference risk and a champion–challenger follow-up

## Key results (simulated)

| Check | Result |
|---|---|
| Sample size for +10% relative uplift (4% baseline) | ~39,500 customers per group, ~2 weeks |
| Sample size for +5% relative uplift | ~154,000 per group, ~52 days |
| A/A false-positive rate | ~5–6% (expected 5%) |
| Empirical power | ~80% (expected 80%) |
| False-positive rate with daily peeking | ~23% (vs 5% without peeking) |

## Tech stack

Python · NumPy · SciPy · statsmodels

## How to run

```bash
pip install numpy scipy statsmodels jupyter
jupyter notebook ab_test_agent_matching.ipynb
```

Or open it directly in Google Colab.
