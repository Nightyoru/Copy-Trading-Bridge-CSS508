### Observation & Motivation 

My selection of this project stems from my daily experience in personal asset management and as an active user of third-party copy-trading social applications compatible with major brokers like Pepperstone.

**The Platform Context:**
Copy-trading platforms allow "Master" traders to broadcast their trades to "Followers" for a performance fee (typically 20%-30%). These apps provide ranking boards, historical charts, and automated execution bridges to synchronize trades across accounts.

**The "Integrity Issue":**
Through consistent use, I have observed a significant gap in the software's validation logic regarding how "Top Traders" are ranked:

* **Social Proof Bias:** The software often ranks Master accounts based on raw percentage gain, leading users to flock to accounts at the top of the leaderboard.
* **Hidden Risk Profiles:** The current validation logic fails to adequately penalize "Martingale" strategies (doubling down on losses) or massive open drawdowns that are held indefinitely to keep "Realized Profit" looking high.
* **The Follower's Reality:** The software does not always verify if a follower remains profitable after the 30% fee and commissions are deducted, which can lead to a "Success" in the Master's account being a "Loss" in the Follower's account.

---

### My Role as a "Trust Broker"

As an engineer in an AI Native world, my goal is to verify and validate that the software is reliable for the end customer. My project—the **Verified Copy Trading Bridge**—acts as a middleware to supplement these third-party platforms. It adds a critical validation layer that checks for risk and net-profitability before a trade is copied.
