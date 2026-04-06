### Verified Copy Trading Bridge - AI Generated Test Cases

**Functional Testing**
* **TC01 - Basic Replication:** Verify that a standard "Market Buy" signal is successfully replicated from the Master account to the Child account within the 500ms SLA.
* **TC02 - Fee Deduction Accuracy:** Verify that the system accurately calculates and deducts the 30% performance fee and standard broker commissions from the Child account's gross profit.
* **TC03 - Slippage Tolerance:** Verify that the bridge successfully executes the trade even if the Child account experiences up to 2 pips of slippage compared to the Master's original entry price.
* **TC04 - Stop Loss Scaling:** Verify that if the Master account sets a 50-pip Stop Loss, the bridge correctly scales and applies the exact same 50-pip risk parameter to the Child's position.

**Boundary Testing**
* **TC05 - Minimum Lot Sizing:** Verify replication behavior when the Master's trade size scales down to the absolute minimum lot size allowed by the broker execution engine (e.g., 0.01 lots).
* **TC06 - Net Profitability Threshold (Break-even):** Verify the system triggers a "Low Expectancy" warning when the Master's gross profit minus commissions and the 30% fee equals exactly $0.01 of net profit for the follower.
* **TC07 - Drawdown Circuit Breaker:** Verify that if the Master's open floating drawdown reaches exactly 4.99%, the trade is allowed, but if it hits 5.01% (crossing a 5% hard limit), the bridge blocks all new incoming copy signals.

**Negative & Invalid Input Testing**
* **TC08 - Martingale Detection Block:** Verify that if the Master account loses a trade and immediately opens a new position in the same direction with >2x the original lot size, the system blocks the copy and flags "High-Risk Martingale Behavior."
* **TC09 - Insufficient Margin:** Verify that if the Master opens a valid trade, but the Child account lacks the required free margin to open the scaled position, the bridge gracefully rejects the trade and logs an "Insufficient Funds" error.
* **TC10 - Malformed Data Packet:** Attempt to process a Master signal containing an invalid ticker symbol (e.g., "INVALID_USD") or a negative execution price. Verify the system drops the packet and logs a "Data Integrity Error."

**Equivalence Partitioning & Load Testing**
* **TC11 - Order Type Equivalence (Instant):** Test replication of a Market Buy order to represent the successful handling of all instant execution types (including Market Sell).
* **TC12 - Order Type Equivalence (Pending):** Test replication of a Buy Limit order to represent the successful handling of all pending execution types (including Sell Limit, Buy Stop, and Sell Stop).
* **TC13 - Concurrency Load Test:** Simulate 100 Child accounts connected to a single Master account. Verify that a single trade signal is successfully broadcast to all 100 accounts without exceeding the 500ms latency limit.
