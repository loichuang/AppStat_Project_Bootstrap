# Economic Convergence Analysis using Bootstrap Methods

Do poor countries grow faster than rich ones? This project tests the
**beta-convergence hypothesis** (Barro & Sala-i-Martin, 1992) on real GDP data,
using a non-parametric bootstrap to quantify the uncertainty of the estimate.

Individual project, Applied Statistics course at EURECOM (Prof. Motonobu Kanagawa).

## Result

| Quantity | Value |
|---|---|
| Observed difference in median log-growth | **0.185** |
| Bootstrap standard error | 0.053 |
| 95% confidence interval | **[0.081, 0.290]** |
| Bootstrap replications | B = 2000 |

The confidence interval excludes zero, so the data supports the convergence
hypothesis: countries below the global median income in 2000 grew
significantly faster over 2000-2020.

## Method

**Data.** GDP per capita from the Gapminder Data Portal, PPP-adjusted, in
constant 2021 international dollars. 193 countries with complete data for both
2000 and 2020.

**Grouping.** Split at the global median GDP per capita in 2000 ($9,351):
96 low-income countries, 97 high-income.

**Growth measure.** Log-growth over 20 years, `g_i = ln(GDP_2020 / GDP_2000)`.
The log-ratio is used instead of a percentage change because it is symmetric:
doubling and halving give values of equal magnitude and opposite sign.

**Statistic.** `θ = median(g | poor) − median(g | rich)`. The median is
preferred to the mean because a few countries have extreme growth values that
would distort the mean.

**Why bootstrap.** The median has no simple closed-form standard error, so the
distribution of θ is approximated by non-parametric resampling (B = 2000),
which is enough for stable confidence interval bounds.

## Repository

```
data/gdp_pcap.csv          Gapminder GDP per capita (PPP, constant 2021 int$)
notebook/analysis.ipynb    full analysis: EDA, grouping, bootstrap, figures
deliverable/               LaTeX source and compiled report, generated figures
requirements.txt           Python dependencies
```

## Reproduce

```bash
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
jupyter notebook notebook/analysis.ipynb
```

## Report

Full write-up: [`deliverable/rapport_appstat.pdf`](deliverable/rapport_appstat.pdf)
