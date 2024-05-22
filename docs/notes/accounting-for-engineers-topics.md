---
author: Miguel Pinilla
Copyright: (c) Miguel Pinilla, All rights reserved
License: "This work is licensed under the Creative Commons License CC BY-NC-SA 4.0: https://creativecommons.org/licenses/by-nc-sa/4.0/"
email: miguel.pinilla@saldubatech.com
share: "true"
title: Topic Ideas: Accounting for Engineers Topics
---

{{ draftMark }}

!!! note
    Personal Notes, not for distribution

## (I) Financial Statements

* Accounting is Measurement
  * Measures:
  * What I have at hand (Balance)
  * How it flows (P&L)
  * Conservation of Money (as Energy, Momentum, Mass, …)
  * Inputs + Outputs = Change in Content (with appropriate signs)
  * Discrete Events: Transactions
  * Timestamp, Type, Amount ($)
* Key (non-financial) transactions in business
  * Buy & Sell → Ignore for now, not needed (!!)
  * Deliver & Receive Goods/Services (accruing/incurring)
  * Pay & Collect Cash
* Measurements
  * Balance = set of Net Assets, Deliveries, Receipts at a point in time
  * P&L = set  Deliveries, Receipts during a period
  * Measurement taken at the end of the P&L period
* Application of Business Transactions:
  * Deliver:  Add transaction to Deliveries
  * Collect: Remove Transaction from Deliveries and Add to Net Assets
  * Receive: Add transaction to Receipts
  * Pay: Remove Transaction from Receipts and Add to Net Assets
* Calculations for Business Transactions:
  * Always Summation on the set (Balance of P&L)
    * Transaction Signs:
    * Deliver, Collect:  Positive
    * Receive, Pay: Negative

* What does “closing the books” mean:
  * Pick a time.
  * Do all the calculations for Balance and P&L
  * Write down the timestamped results
  * Add the result of the P&L (earnings) to the NetAssets as its own transaction
  * Reset the P&L set to empty.
* What about Buy & Sell: Not official accounting, but good to manage the business.
  * Not for “Legal” accounting
  * Needed for managing the business
  * Usually called “bookings” of “forecast”
  * Can be considered as a “wrapper” around legal accounting.
* What is “The Goal”
  * P&L as high as possible
  * Subject to NetAssets > 0
  * Over the long run (multiple periods)
* Any other tricks?
  * Borrowing and Lending
  * Taxes
  * Capital
  * “Balancing” the books: Balance at closing books always == 0
* Is that it?
  * Pretty Much
  * Intra-Company Transactions, Chart of Accounts
  * Double Entry: Rules to not mess up the Balance and P&L sets

## (II) Cost Accounting

* Engineers Know:
  * Multivariate Calculus
  * Set theory
  * Linear approximations (Taylor series expansion)
* Cost Accounting is Measurement
  * How much does it cost me to <...>
  * How can I expect it to vary
* The Underlying object to measure: Producing and delivering a given amount of goods/services
* As simple as a derivative
  * If we know the total cost as a function of the production volume
  * The cost per unit is simply the derivative of the total cost.
* But derivatives and higher order functions are not quite taught in Biz School, so…
  * We take a linear approximation: Y = a + bX
  * Cost = Fixed + UnitCost * Volume
* Cost Variances demystified through Partial Derivatives
  * Unit Cost Variance: dC = V*dUC
  * dUC = dLabor + dMaterial
  * Volume Variance: dC = UC*dV
  * Fixed Cost Variance: dC = dF
