# 


<!-- PROJECT LOGO -->
<br />
<div align="center">
  <h3 align="center">FE_CVAR_PORTFOLIO_OPT: Optimizing portfolio weights via CVaR.</h3>

  <p align="center">
    Using CVaR (tail VaR) to optimize portfolio returns. 
    <br />
  </p>
</div>



<!-- ABOUT THE PROJECT -->
## CVaR: A high level primer

The objective of portfolio optimization is to determine the ideal mix of investments that balances risk and return to meet desired goals. The traditional method for portfolio optimization is known as [mean-variance optimization](https://www.investopedia.com/terms/m/meanvariance-analysis.asp), which relies on the assumption that returns follow a normal distribution.

VaR (value at risk) is a measure of financial risk used to estimate the maximum loss that a portfolio of investments might incur over a specified time horizon, under normal market conditions, with a given level of confidence. In a nutshell, it is an estimate of **the worst-case scenario** for an investment portfolio, and is usually expressed as an absolute dollar figure or percentage of a portfolio's total value.

For example, if a portfolio has a VaR of $1 million at a 95% confidence level, it means that there is a 5% chance that the portfolio will lose more than $1 million over a specified period of time. VaR is commonly used by financial institutions to assess and manage investment risk.

CVaR (conditional value at risk, or expected shortfall) extends this concept, and represents the expected loss of a portfolio given that a specific threshold has been breached. It provides a more complete picture of the portfolio's risk by taking into account not only the worst-case scenario, but also the average losses in such scenarios.

In short: VaR is a single-point estimate of the maximum potential loss over a specified time horizon and confidence level, while CVaR is a risk measure that takes into account the average loss of a portfolio given that a VaR threshold has been breached. CVaR provides a more comprehensive picture of the portfolio's risk and is typically used as a complementary measure to VaR.

### Toy Example

`cvar_optimization.m` outlines a simple example in which we develop an efficient frontier of portfolios by calculating the CVaR for a range of expected returns. A high level walkthrough of the steps taken to generate a set of CVaR vs. expected return values:

1. Calculate daily stock returns. 
2. Calculate mean and covariance of returns (`mu` and `Q`, respectively).
3. Set a risk tolerance level (`0.95` is arbitrarily selected here). This means that we want to find a portfolio that has a 95% chance of not losing more than a certain amount.
4. Calcuate and store the CVaR of each portfolio. Portfolio returns are calculated by multiplying individual returns by portfolio weights. Worst scenarios are identified by finding the returns that are less than the 5th percentile (1-0.95) of returns. The CVaR is calculated as the average of worst scenario returns.
5. Set lower bounds for optimization variables (wieghts and variables required for CVaR calculations). 
6. Add constraints (expected return, sum of weights, ...) and set the objective: **minimizing CVaR**.
7. Use `linprog` to solve the LP problem. An efficient frontier of portfolios is developed by calcuating CVaR values for a range of expected returns.
8. Plot.

---

<sup><sub>Porting over from local files, circa 2016-17.</sub></sup>
