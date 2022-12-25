# Liquidations

## FAQS

### How much is the liquidation penalty?

The liquidation penalty (or bonus for liquidators) depends on the asset used as collateral. You can find every assets' liquidation fee in the [risk parameters section](broken-reference).

### Can you give me an example?

A couple of them here:

**Example 1**&#x20;\
****Bob deposits 10 ETH and borrows 5 ETH worth of DAI.&#x20;\
If Bob’s Health Factor drops below 1, his loan will be eligible for liquidation.&#x20;\
A liquidator can repay up to 50% of a single borrowed amount = 2.5 ETH worth of DAI.&#x20;\
In return, the liquidator can claim a single collateral, ETH (5% bonus). &#x20;\
The liquidator claims 2.5 + 0.125 ETH for repaying 2.5 ETH worth of DAI.

**Example 2**&#x20;\
****Bob deposits 5 ETH and 4 ETH worth of YFI and borrows 5 ETH worth of DAI&#x20;\
If Bob’s Health Factor drops below 1, his loan will be eligible for liquidation.&#x20;\
A liquidator can repay up to 50% of a single borrowed amount = 2.5 ETH worth of DAI.&#x20;\
In return, the liquidator can claim a single collateral, as the liquidation bonus is higher for YFI (15%) than ETH (5%) if the liquidator chooses to claim YFI. &#x20;\
The liquidator claims 2.5 + 0.375 ETH worth of YFI for repaying 2.5 ETH worth of DAI.

### How can I avoid getting liquidated?

To avoid liquidation, you can raise your health factor by depositing more collateral assets or repaying part of your loan. By default, repayments increase your health factor more than deposits. Also, it's important to monitor your health factor and keep it high to avoid liquidation. For example, keeping your health factor over 2 gives you more of a margin to avoid liquidation.  \
\
You should be mindful of the stablecoin price fluctuations due to market conditions and how they might affect your health factor. For example, the market price of USDC 1.00 might not equal exactly USD 1.00, but for example, USD 0.95. The price fluctuations of stablecoins, like any assets, affect your health factor.
