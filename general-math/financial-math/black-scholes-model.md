# Black-Scholes Model

### Equations

$$
\begin{align}
C &= S_t \Phi(d_1) - K e^{-rt} \Phi(d_2) \\[8pt]

\Phi(x) &= \int_{-\infty}^{x} \frac{1}{\sqrt{2\pi}} e^{-s^2/2} \, ds \\[10pt]

d_1 &= \frac{\ln\left(\frac{S_t}{K}\right) + \left(r + \frac{\sigma^2}{2}\right)t}{\sigma \sqrt{t}} \\[10pt]

d_2 &= d_1 - \sigma \sqrt{t}
\end{align}
$$

The core idea is pricing an option by asking:&#x20;

> "What is the expected value of the payoff at a risk-free rate?"

Formally:  $$C = e^{-rT},\mathbb{E}\big[(S_T-K)^+\big]$$

We model the stock as following geometric Brownian motion: \
$$dS_t​=rS_t​dt+σS_t​dW_t​$$

**Variables:**&#x20;

* $$W_t$$ := Brownian motion
  * Essentially a continuous random walk
  * $$W_0$$ = 0
  * $$W_t - W_s \sim \mathcal{N}(0, t - s)$$
* $$T$$ := Time to maturity
  * The time at which the option expires
* $$K$$ := Strike price
  * The price we can buy the stock at

### Concepts

**European call option:**&#x20;

A European call option is the right (not obligation) to buy a stock at price $$K$$ at time $$T$$



