#include <cmath>
#include <iostream>
#include <algorithm>

constexpr double PI = 3.14159265358979323846;

// -------------------- Normal distribution --------------------
double norm_pdf(double x) {
    return std::exp(-0.5 * x * x) / std::sqrt(2.0 * PI);
}

// Abramowitz–Stegun approximation
double norm_cdf(double x) {
    return 0.5 * std::erfc(-x / std::sqrt(2.0));
}

// -------------------- Black–Scholes helpers --------------------
double d1(double S, double K, double r, double T, double sigma) {
    return (std::log(S / K) + (r + 0.5 * sigma * sigma) * T)
           / (sigma * std::sqrt(T));
}

double d2(double S, double K, double r, double T, double sigma) {
    return d1(S, K, r, T, sigma) - sigma * std::sqrt(T);
}

// -------------------- Option pricing --------------------
double bs_call_price(double S, double K, double r, double T, double sigma) {
    double D1 = d1(S, K, r, T, sigma);
    double D2 = d2(S, K, r, T, sigma);
    return S * norm_cdf(D1) - K * std::exp(-r * T) * norm_cdf(D2);
}

double bs_put_price(double S, double K, double r, double T, double sigma) {
    double D1 = d1(S, K, r, T, sigma);
    double D2 = d2(S, K, r, T, sigma);
    return K * std::exp(-r * T) * norm_cdf(-D2) - S * norm_cdf(-D1);
}

// -------------------- Greeks --------------------
double vega(double S, double K, double r, double T, double sigma) {
    double D1 = d1(S, K, r, T, sigma);
    return S * norm_pdf(D1) * std::sqrt(T);
}

// -------------------- Implied volatility --------------------
double implied_vol_call(
    double market_price,
    double S,
    double K,
    double r,
    double T,
    double init_vol = 0.2,
    double tol = 1e-8,
    int max_iter = 100
) {
    double sigma = init_vol;

    for (int i = 0; i < max_iter; ++i) {
        double price = bs_call_price(S, K, r, T, sigma);
        double diff = price - market_price;

        if (std::fabs(diff) < tol)
            return sigma;

        double v = vega(S, K, r, T, sigma);
        if (v < 1e-8)
            break;

        sigma -= diff / v;
        sigma = std::max(1e-6, sigma);
    }
    return sigma;
}

// -------------------- Main test --------------------
int main() {
    // Input parameters
    double S = 100.0;    // Spot
    double K = 100.0;    // Strike
    double r = 0.05;     // Risk-free rate
    double T = 1.0;      // Time to maturity (years)
    double sigma = 0.2;  // True volatility

    // Pricing
    double call_price = bs_call_price(S, K, r, T, sigma);
    double put_price  = bs_put_price(S, K, r, T, sigma);

    // Implied volatility
    double iv = implied_vol_call(call_price, S, K, r, T);

    std::cout << "Black-Scholes Call Price : " << call_price << "\n";
    std::cout << "Black-Scholes Put  Price : " << put_price << "\n";
    std::cout << "Implied Volatility      : " << iv << "\n";

    return 0;
}
