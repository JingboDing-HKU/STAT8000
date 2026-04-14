# Black–Scholes Option Pricing in C++

This project implements the Black–Scholes option pricing model in C++ to calculate theoretical European call and put option prices and estimate implied volatility using the Newton–Raphson method.

## Overview

The Black–Scholes model is one of the foundational models in quantitative finance. This project translates the model into a clean and modular C++ implementation, showing how mathematical pricing formulas can be converted into reusable computational functions.

The project focuses on two main tasks:

1. Pricing European call and put options
2. Recovering implied volatility from an observed market option price

## Objectives

- Implement the Black–Scholes pricing model in C++
- Build modular functions for key mathematical components
- Estimate implied volatility with Newton–Raphson iteration
- Demonstrate the connection between financial theory, numerical methods, and programming

## Model Framework

For a non-dividend-paying asset, the Black–Scholes model computes:

- European call option price
- European put option price
- Vega, the sensitivity of option price to volatility

Since implied volatility cannot be solved analytically from the option pricing formula, this project uses Newton–Raphson iteration to solve the inverse pricing problem numerically.

## Inputs

The model uses the following variables:

- `S0` — current underlying asset price
- `K` — strike price
- `r` — continuously compounded risk-free interest rate
- `T` — time to maturity
- `sigma` — volatility
- `C_market` — observed market call price

## Methodology

The implementation is organized into several components:

- Standard normal PDF and CDF
- Helper functions for `d1` and `d2`
- Black–Scholes call pricing function
- Black–Scholes put pricing function
- Vega calculation
- Newton–Raphson implied volatility solver

The numerical solver iteratively updates volatility until the pricing error is sufficiently small or a maximum iteration limit is reached.

## Sample Test Case

The project uses the following test parameters:

- `S0 = 100`
- `K = 100`
- `r = 0.05`
- `T = 1`
- `sigma = 0.20`

### Output

- Call price ≈ `10.4506`
- Put price ≈ `5.5735`
- Implied volatility ≈ `0.20`

These results confirm that the implementation is consistent with the theoretical Black–Scholes framework.

## Key Features

- Clear and modular C++ implementation
- Closed-form pricing for European options
- Numerical implied volatility estimation
- Easy to extend for future quantitative finance projects
## References

1. Black, F., & Scholes, M. (1973). *The Pricing of Options and Corporate Liabilities*. Journal of Political Economy, 81(3), 637–654.
2. Hull, J. C. (2022). *Options, Futures, and Other Derivatives* (11th ed.). Pearson.
3. Schurman, G. (2010). *Newton-Raphson Method for Solving Nonlinear Equations: Solution to Black-Scholes Implied Volatility*.
