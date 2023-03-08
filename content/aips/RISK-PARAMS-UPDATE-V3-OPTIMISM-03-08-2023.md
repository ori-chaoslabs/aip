---
title: Risk Parameter Updates Aave V3 Optimism
shortDescription: Update risk parameters on AAVE V3 Optimism
author: Chaos Labs (@ori-chaoslabs, @yhayun)
discussions: https://governance.aave.com/t/arc-chaos-labs-risk-parameter-updates-aave-v3-optimism-2023-02-28/12099
created: 2023-03-08
---

# Simple Summary

A proposal to adjust nine (9) total risk parameters, including Loan-to-Value, Liquidation Threshold, and Liquidation Bonus, across four (4) Aave V3 Optimism assets.

# Motivation
Chaos Labs’ Parameter Recommendation Platform runs hundreds of thousands of agent-based off-chain and on-chain simulations to examine how different Aave V3 risk parameters configurations would behave under adverse market conditions - and find the optimal values to maximize protocol borrow usage while minimizing losses from liquidations and bad debt. 

*Note: As a general guideline, we limit the proposed changes by +-3% for all parameters as a high/low bound for a given proposal. This ensures more controlled changes and allows us to analyze their effect on user behavior before recommending further amendments to the parameters if the optimal configuration is outside this range.*

Please find more information on the parameter recommendation methodology [here](https://community.chaoslabs.xyz/aave/recommendations/methodology).

You can also view the simulation results and breakdown for the different assets by clicking on them on this [page](https://community.chaoslabs.xyz/aave/recommendations).

The output of our simulations reveals an opportunity to increase LTVs and LTs for WBTC, WETH, USDC, and DAI on V3 Optimism, resulting in improved capital efficiency of the system, with no effect on the projected VaR (95th percentile of the protocol losses that will be accrued due to bad debt from under-collateralized accounts over 24 hours) and EVaR (Extreme VaR, the 99th percentile of the protocol losses that will be accrued due to bad debt from under-collateralized accounts over 24 hours)

Simulating all changes jointly yields a projected borrow increase of ~$470,000, with no increase in VaR and Extreme VaR compared to simulations with the current parameters.

**Liquidity and Position Analysis:**

The TVL in Aave on Optimism (115.5M$) is concentrated primarily on two blue-chip, high-liquidity assets, which together account for ~75% of the supplied assets in $ values: USDC (44%) and Ethereum (30%), with the remaining supply, mostly being WBTC (13%). As we see adequate on-chain liquidity to support significant liquidations with minimal slippage on these assets, we recommend increasing the LT and LTV for them and one additional high-liquidity asset (DAI). Similarly, we recommend reducing the Liquidation Penalty for WBTC, which is set conservatively at 10% to a lower level (7%) closer to that of USDC and Ethereum (5%).


**WETH**

We have not identified any outsized positions that are actively affecting our recommendations. There are a few positions that supply 1-4M$ WETH each and borrow USDC against it; with the chain's current liquidity, it is possible to liquidate these positions with slippage far below the liquidation penalty. 

**WBTC and DAI**

We have not identified any outsized positions that are actively affecting our recommendations, however, we should call out that around 50% of the on-chain supply of WBTC on Optimism is currently held on Aave, which calls for some caution. We have proposed an [amendment to the supply cap](https://governance.aave.com/t/arc-chaos-labs-supply-and-borrow-cap-updates-aave-v3-2023-02-24/12048/4) to limit the concentration of liquidity on Aave.

Given the blue-chip nature of BTC/WBTC, we expect significant arbitrage buying pressure to offset any slippage that may be created by future liquidations of WBTC and, therefore, recommend reducing the Liquidation Penalty even with the current significant liquidity concentration on Aave. We expect a lower LP to drive liquidators to liquidate positions in smaller portions, pacing the process and allowing the market more time to react. 

**USDC**

We have identified a large position that supplies approximately 75% of USDC on Optimism and does not borrow against its ~$40M USDC position, and therefore does not currently pose a liquidation/bad debt risk to the protocol.  

# Specification

The following risk parameter proposal is presented below:

| Asset | Parameter | Current | Recommended | Change |
| --- | --- | --- | --- | --- |
| WETH | Liquidation Threshold | 82.5% | 85% | +2.5% |
| WETH | Loan-to-Value | 80% | 82.5% | +2.5% |
| WBTC | Liquidation Threshold | 75% | 78% | +3% |
| WBTC | Loan-to-Value | 70% | 73% | +3% |
| WBTC | Liquidation Penalty | 10% | 7% | -3% |
| DAI | Liquidation Threshold | 80% | 82% | +2% |
| DAI | Loan-to-Value | 75% | 77% | +2% |
| USDC | Liquidation Threshold | 85% | 86% | +1% |
| USDC | Loan-to-Value | 80% | 81% | +1% |



# References
[Forum Post](https://governance.aave.com/t/arc-chaos-labs-risk-parameter-updates-aave-v3-optimism-2023-02-28/12099)

[Tests](to add)

[Proposal payload implementation](to add)

[Deployed proposal payload](to add) 


# Copyright

Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
