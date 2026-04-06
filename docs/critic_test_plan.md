
# Critique of AI-Generated Test Cases
This document outlines the human-led refinements made to the initial AI-generated test suite for the Verified Copy Trading Bridge. While the AI provided a solid technical foundation, it lacked the domain-specific nuances of the trading industry.

### TC02: Sepeartion of Fees and Commissions
* AI Suggestion: Verify that the system accurately calculates and deducts the 30% performance fee and standard broker commissions from the Child account's gross profit.
* Critique: In reality, fees and commissions are charged differently. The broker commisions are transactionally charged, while performance fees are typically caluclated monthly based on the follower's gross profit.
* update: I will splitting this into two distinct tests
- TC02a : Verify the immediate deduction of per-trade costs.
- TC02b: Verify the accuracy of the percentage gross profit calcuation at the end of a simulated 30-day period.

### TC3: Slippage as a User Risk Barrier
* AI suggestion: Verify that the bridge successfully executes the trade even if the Child account experiences up to 2 pips of slippage compared to the Master's original entry price.
* ciritque: Slippage is an inevitable market reality that the follower must bear or accept. The test shouldn't just look for "perfection" but for "successful execution" within a realistic timeframe.
* Changed the execution SLA to 2 seconds. The test now focuses on ensuring the bridge successfully completes the order despite the price gap, rather than treating slippage as a failure condition

### TC06: Historical vs. Immediate Profitability
* AI Suggestion: Verify a "Low Expectancy" warning on a single trade.
* Critique: Trading software cannot predict the future; it can only provide clarity on historical data. A single trade's profit is less important than the unrealized drawdown history.
* Update: The system will now trigger a "Low Expectancy" warning when the ratio of historical unrealized drawdown to net profit hits a critical threshold (e.g., $0.01$ profit vs. high historical drawdown).

### TC07: User Autonomy and Configurable Risk
AI Suggestion: A hard-coded $5\%$ drawdown circuit breaker
* Critique: We cannot stop users from doing what they want; we can only provide the tools for them to protect themselves. Risk appetite is subjective.
* Update: Changed this to a User-Defined Parameter. The test now verifies that the system correctly enforces a limit set by the user, providing them the option to define their own safety margin.

### Adding Security Test.
* Spoofing: Verify the bridge rejects signals that do not come from a verified Master account's IP address.
* Information Disclosure: Verify that API keys and account balances are encrypted and never printed in the clear in Docker logs.
