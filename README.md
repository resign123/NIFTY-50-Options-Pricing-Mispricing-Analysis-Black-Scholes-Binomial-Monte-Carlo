# 📈 NIFTY-50-Options-Pricing-Mispricing-Analysis-Black-Scholes-Binomial-Monte-Carlo

## **Project Overview**  
This repository focuses on analyzing **mispricing in NIFTY 50 ATM options** by comparing real market prices with theoretical prices derived from various **option pricing models**.  

📌 **Key Features:**  
✅ Fetch real-time NIFTY 50 **Call (CE) & Put (PE) option** prices at **9:20 AM** using the **Fyers API**.  
✅ Calculate theoretical option prices using:  
  - **Binomial Option Pricing Model**  
  - **Black-Scholes Model**  
  - **Monte Carlo Simulations**  
✅ Identify **overvalued** and **undervalued** options based on the mispricing.  
✅ Generate in-depth **visualizations & reports** for analysis.  
✅ Provide actionable insights for traders to exploit mispricing opportunities.  

---

## **How It Works**  
1. **Fetch Live Market Data**  
   - At **9:20 AM**, fetch ATM Call & Put prices from **Fyers API** (1-min data from 13 Nov 2024 to 13 Feb 2025).  
   
2. **Calculate Theoretical Prices**  
   - Compute fair values using **Binomial Option Pricing**, **Black-Scholes Model**, & **Monte Carlo Simulations**.  

3. **Compare & Identify Mispricing**  
   - **Overvalued?** → Consider **selling** that option.  
   - **Undervalued?** → No trade (or alternative strategy).  

4. **Analysis & Visualization**  
   - Compare real vs theoretical prices.  
   - Identify trends & systematic mispricing.  
   - Evaluate strategy effectiveness.  

---

## **Example Output**  
📊 **Sample Comparison (Real vs Theoretical Pricing)**  
| Date | Option Type | Real Price | Binomial Price | Black-Scholes Price | Monte Carlo Price | Mispricing % |
|------|------------|------------|----------------|----------------------|------------------|--------------|
| 10-Feb-2025 | CE | ₹150 | ₹145 | ₹148 | ₹147 | -3.33% |
| 10-Feb-2025 | PE | ₹120 | ₹125 | ₹123 | ₹122 | +4.16% |


## **Strategy Insights**  
📌 **If an option is significantly overvalued:**  
✅ **Short it (Sell the option)** if it aligns with other indicators.  
✅ Use **hedging strategies** to manage risk.  

📌 **If an option is undervalued:**  
❌ **Avoid blindly buying** – it could be mispriced due to external factors.  
✅ Look for **confirmations in volatility, open interest, and IV changes**.  

---

## **Options Pricing Models Explained**  

### **1. Monte Carlo Simulations**

Monte Carlo simulation is used to estimate the price of options by simulating the future stock price paths and calculating the corresponding option payoffs. The method relies on **Geometric Brownian Motion (GBM)**, which models stock price evolution as:

```math
S_{t+1} = S_t \cdot \exp \left( (r - 0.5 \cdot \sigma^2) \cdot \Delta t + \sigma \cdot \sqrt{\Delta t} \cdot Z \right),
```

where:
- $S_t$ is the stock price at time $t$.
- $r$ is the risk-free interest rate.
- $\sigma$ is the volatility of the stock.
- $\Delta t$ is the time increment (daily or another small step).
- $Z$ is a random variable from a standard normal distribution (representing the random walk).

For each simulation:
1. Stock price over time is simulated using the GBM formula.
2. Option **payoff** at maturity is calculated:
   - **Call Option**: $\max(0, S_T - K)$
   - **Put Option**: $\max(0, K - S_T)$,

where $S_T$ is the simulated stock price at maturity and $K$ is the strike price.

3. The payoff is discounted back to present value using the risk-free rate:
```math
\text{Option Price} = \exp(-r \cdot T) \cdot \text{Average Payoff},
```

where $T$ is the time to expiration in years.

This approach is flexible and can handle a wide variety of option types though it requires many simulations for accuracy.

### **2. Black-Scholes Model**
The **Black-Scholes model** gives a closed-form solution for pricing call and put options, based on the assumption that stock prices follow a geometric Brownian motion.

#### **Formula**
For call options:
```math
C = S \cdot N(d_1) - K \cdot e^{-rT} \cdot N(d_2).
```

For put options:
```math
P = K \cdot e^{-rT} \cdot N(-d_2) - S \cdot N(-d_1),
```
where:

```math
d_1 = \frac{\ln(S/K) + (r + \sigma^2/2)T}{\sigma \sqrt{T}}, 
```

```math
 d_2 = d_1 - \sigma \sqrt{T}.
```

### **3. Binomial Tree Method**
The Binomial Tree method approximates option prices by constructing a tree of possible future stock prices, calculating option prices by working backwards from the terminal nodes.

#### **Steps**
1. Time is divided to expiration into `n` intervals.
2. Each interval allows the stock price to increase by a factor `u` or decrease by a factor `d`.
3. Option prices are computed by working backwards using risk-neutral probabilities.

### **Greeks Explanation**
- **$\Delta$**: Sensitivity of the option price to changes in the underlying stock price.
- **$\Gamma$**: Rate of change of delta with respect to the underlying stock price.
- **$\nu$**: Sensitivity of the option price to changes in volatility.
- **$\Theta$**: Sensitivity of the option price to time decay.
- **$\rho$**: Sensitivity of the option price to changes in the risk-free interest rate.


## **Future Improvements**  
📍 Incorporate advanced **IV-based adjustments**.  
📍 Automate strategy execution via APIs.  

---

## **Contributing**  
Feel free to open issues & PRs! 🙌  

🚀 **Star the repo if you find it useful!** ⭐  
