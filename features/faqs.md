---
description: >-
  Here are some answers to the most asked questions regarding liquidity
  providers.
---

# FAQs

## _Borrowing_

## Why would I borrow instead of selling my assets?

Selling your assets means closing your position on that particular asset. Hence, if you are long on the asset, you would not be entitled to the potential upside value gain. By borrowing, you can obtain liquidity (working capital) without selling your assets. Users mainly borrow for unexpected expenses, leveraging their holdings, or new investment opportunities.

## How much I can borrow?

The maximum amount you can borrow depends on your supplied value and available liquidity. For example, you can’t borrow an asset if there is insufficient liquidity or your health factor doesn’t allow you to. You can find every collateral available and its specific parameters for borrowing in the [risk](broken-reference)[ framework](../risk/risk-framework.md) section.

## What asset do I need to repay?

You repay your loan with the same asset you borrowed. For example, if you borrow 1 ARTH, you will pay back 1 ARTH + interest accrued. You can also use your collateral to repay. If you want to pay back the loan based on the USD price, you can borrow any available stablecoins such as USDC, DAI, etc.

## What is the difference between stable and variable rates?

Stable rates act as fixed rates in the short term but can be re-balanced in the long term in response to changes in market conditions. The variable rate is based on the offer and demand in ARTH.&#x20;

As its name indicates, the stable rate will remain pretty stable, and it is the best option to plan how much interest you will have to pay. The variable rate will change over time and could be the optimal rate depending on market conditions. You can switch between the stable and variable rates at any time through your dashboard.

## When could my stable rate be rebalanced?

Stable rate rebalance is expected to be unlikely but will happen if the average borrow rate is lower than 25% APY and the utilization rate is over 95%.

## How do I switch my interest rate type?

To switch your interest rate between stable and variable rate, browse your dashboard and click on the “APR Type” switch button for the asset you wish to apply the rate change.

## Can I borrow using the stable and variable rates simultaneously for one asset?

No, you can only borrow using a stable or variable rate. If you switch to your desired rate, it will switch the rate for your whole debt on that asset. Despite this, you can have different borrowing rates for different assets.

## What is the health factor?

The health factor is the numeric representation of the safety of your deposited assets against the borrowed assets and their underlying value. The higher the value is, the safer the state of your funds is against a liquidation scenario. If the health factor reaches 1, the liquidation of your deposits will be triggered. A Health Factor below 1 can get liquidated. For an HF=2, the collateral value vs. borrow can reduce by 1 out of 2: 50%. The health factor depends on the liquidation threshold of your collateral against the value of your borrowed funds. You can find all of the collateral parameters in the [risk parameter](../risk/risk-framework.md#health-factor) section.&#x20;

\
If you would like to know more technical details about the health factor calculation, you can find those [here](../risk/risk-framework.md#health-factor).

## What happens when my health factor is reduced?

Depending on the value fluctuation of your supplies, the health factor will increase or decrease. If your health factor increases, it will improve your borrow position by making the liquidation threshold unlikely to be reached. In the case that the value of your collateralised assets against the borrowed assets decreases instead, the health factor is also reduced, causing the risk of liquidation to increase.

## When do I need to pay back the loan?

There is no fixed time period to pay back the loan. You can borrow for an undefined period if your position is safe. However, as time passes, the accrued interest will grow to make your health factor decrease, which might result in your deposited assets becoming more likely to be liquidated.

## How do I pay back the loan?

In order to pay back the loan, you go to the Borrowings section of your dashboard and click on the repay button for the asset you borrowed and want to repay. Select the amount to pay back and confirm the transaction.

In order to avoid the reduction of your health factor leading to liquidation, you can repay the loan or deposit more assets in order to increase your health factor. Out of these two available options, repaying the loan would increase your health factor more.

## _Supplying_

## Can I opt out of my asset from being used as collateral?

Yes. After supplying your assets, you can unselect the asset so that it will not be used as collateral. The opt-out is available in the "Supply" section within your dashboard. Switch the "**use as collateral**" button on the asset you prefer to opt out from being used as collateral. \
\
You can withdraw your assets without opting out of using them as collateral, as long as those funds are not actively being used to borrow, and the withdrawal would cause a liquidation on your loans.&#x20;

## Is there a minimum or maximum amount to supply?

You can supply any amount you want; there is no minimum or maximum limit. Still, it's important to take into account that for really low amounts, it is possible that the transaction cost of the process is higher than the expected earnings. It is recommended that you consider this when supplying very low amounts.&#x20;

## How do I withdraw?

To withdraw, you need to go to the "Dashboard" section and click “**Withdraw**.” Select the amount to withdraw and submit the transaction. Also, you can use your “**aTokens**" as liquidity without withdrawing.

You would need to ensure enough liquidity (not borrowed) to withdraw. If this is not the case you would need to wait for more liquidity from suppliers or borrowers repaying.&#x20;

## _Governance_

## How do I vote?

1. Go to the "Governance" section in the app and select the relevant proposal.
2. Read through the proposal and ensure you fully understand what is being proposed. (_**Note:**_ If you would like to discuss it, select the discussion link on the right-hand side to be directed to the post on the governance forum.)
3. On the right-hand side, select the vote you would like to cast.
4. Confirm your vote.
5. Congratulations, you have now voted!

{% hint style="warning" %}
For your vote to be valid, your balance of voting tokens **must** be the same or greater throughout the entire proposal voting and validating period.
{% endhint %}

## How do I change my vote?

You can easily change your vote by following the steps above and casting your desired vote. Your previous vote will automatically be canceled.

## Can I move my MAHA while the vote is in progress?

You can move your tokens as long as the amount you have in the wallet used to vote remains equal to or higher than the tokens used to vote. Reducing your token amount to lower than the amount used for voting would cancel your vote.

## Can I add more tokens to my vote?

Yes, voting again will reflect your new amount of tokens.

If you have any other questions, please visit the official Maha Governance document: [https://docs.mahadao.com/governance/governance-overview](https://docs.mahadao.com/governance/governance-overview)&#x20;



## _Liquidations_

## How much is the liquidation penalty?

The liquidation penalty (or bonus for liquidators) depends on the asset used as collateral. You can find every assets' liquidation fee in the [risk parameters section](broken-reference).

## Can you give me an example?

Sure! A couple of them here:

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

## How can I avoid getting liquidated?

To avoid liquidation, you can raise your health factor by depositing more collateral assets or repaying part of your loan. By default, repayments increase your health factor more than deposits. Also, it's important to monitor your health factor and keep it high to avoid liquidation. For example, keeping your health factor over 2 gives you more of a margin to avoid liquidation.  \
\
You should be mindful of the stablecoin price fluctuations due to market conditions and how they might affect your health factor. For example, the market price of USDC 1.00 might not equal exactly USD 1.00, but for example, USD 0.95. The price fluctuations of stablecoins, like any assets, affect your health factor.
