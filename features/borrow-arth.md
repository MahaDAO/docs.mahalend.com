---
description: This section explains how you can borrow ARTH using the supplied collateral
---

# Borrow ARTH

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>A screenshot of the Borrow popup</p></figcaption></figure>

Borrowing is the primary utility of the MahaLend protocol. With MahaLend you can borrow ARTH against different kinds of collateral allowing you to leverage yourself on these collateral pools.

All loans and lending protocols require the borrower to put up some collateral to ensure the loan. This is how the protocol can remain solvent and ensure the liquidity providers will never lose their investments.&#x20;

Typically, the borrower will need to over-collateralize, meaning they deposit more value than they borrow. The minimum collateral-to-debt threshold is generally around X and will change based on the market you are borrowing and the current liquidity available to borrow. &#x20;

Your collateral will automatically get liquidated to cover the loan if this **threshold is ever breached**. Depending on the type of collateral a user deposits, this may happen in high-volatility environments, where the value of the collateral depreciates against the value of the borrowed asset. This is an inherent risk to borrowing against volatile assets and is why over-collaterization is the safest way to avoid being liquidated.&#x20;

Additionally, borrowers must pay an interest on their loans at the closure time. This is how the protocol can provide a yield to liquidity providers. There are two kinds of interest rates when a borrower borrows ARTH described below.

## Stable & Variable Interest Rates

<figure><img src="../.gitbook/assets/image (1) (4).png" alt=""><figcaption><p>When borrowing ARTH, the user has an option to choose which interest rate he'd like to use when paying interest.</p></figcaption></figure>

Within the MahaLend ecosystem, there are two interest rate variations. Stable or Variable.&#x20;

Similar to a mortgage, you can choose which variation you’d like to pay, and they are both subject to change. However, it differs from mortgages in that interest must only be repaid at the end of the life of your loan. For more information on borrower interest rates and how they are calculated, please see the [Interest Rate Model](../risks/liquidity-risk/interest-rate-model.md) section.

The stable rates act as fixed rates in the short term but can be re-balanced in the long term in response to changes in market conditions.&#x20;

Whereas the variable rate is dynamic and is based on the offer and demand in ARTH.&#x20;

As its name indicates, the stable rate will remain pretty stable, and it is the best option to plan how much interest you will have to pay. The variable rate will change over time and could be the optimal rate depending on market conditions.&#x20;

You can switch between the stable and variable rates at any time through the dashboard.

## Health Factor

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>The health factor scale which is shown in the UI, showcasing the user's threashold for liquidation.</p></figcaption></figure>

The health factor is the numeric representation of the safety of your deposited assets against the borrowed assets and their underlying value. The higher the value is, the safer the state of your funds is against a liquidation scenario. If the health factor reaches 1, the liquidation of your deposits will be triggered.&#x20;

A Health Factor (`HF`) below 1 (`HF < 1`) can get liquidated.&#x20;

For an `HF=2`, the collateral value vs. borrow can reduce by 1 out of 2: 50%. The health factor depends on the liquidation threshold of your collateral against the value of your borrowed funds. You can find all of the collateral parameters in the [risk parameter](../risk/risk-framework.md#health-factor) section.&#x20;

If you would like to know more technical details about the health factor calculation, you can find those [here](../risk/risk-framework.md#health-factor).

### What happens when my health factor is reduced?

Depending on the value fluctuation of your supplies, the health factor will increase or decrease. If your health factor increases, it will improve your borrow position by making the liquidation threshold unlikely to be reached.&#x20;

{% hint style="danger" %}
In the case that the value of your collateralized assets against the borrowed ARTH decreases instead, the health factor is also reduced, causing the risk of liquidation to increase.
{% endhint %}

## FAQs

### Why would I borrow instead of selling my assets?

Selling your assets means closing your position on that particular asset. Hence, if you are long on the asset, you would not be entitled to the potential upside value gain.&#x20;

By borrowing, you can obtain liquidity (working capital) without selling your assets. Users mainly borrow for unexpected expenses, leveraging their holdings, or new investment opportunities.

### How much I can borrow?

The maximum amount you can borrow depends on your supplied value and available liquidity. For example, you can’t borrow an asset if there is insufficient liquidity or your health factor doesn’t allow you to.&#x20;

You can find every collateral available and its specific parameters for borrowing in the [risk framework](../risk/risk-framework.md) section.

### What asset do I need to repay?

You repay your loan with the same asset you borrowed. For example, if you borrow 1 ARTH, you will pay back 1 ARTH + interest accrued. You can also use your collateral to repay.&#x20;

If you want to pay back the loan based on the USD price, you can borrow any available stablecoins such as USDC, DAI, etc.

### When could my stable rate be rebalanced?

Stable rate rebalance is expected to be unlikely but will happen if the average borrow rate is lower than 25% APY and the utilization rate is over 95%.

### How do I switch my interest rate type?

To switch your interest rate between stable and variable rate, browse your dashboard and click on the “APR Type” switch button for the asset you wish to apply the rate change.

### Can I borrow using the stable and variable rates simultaneously for one asset?

No, you can only borrow using a stable or variable rate. If you switch to your desired rate, it will switch the rate for your whole debt on that asset. Despite this, you can have different borrowing rates for different assets.

### When do I need to pay back a loan?

There is no fixed time period to pay back the loan. You can borrow for an undefined period if your position is safe. However, as time passes, the accrued interest will grow to make your health factor decrease, which might result in your deposited assets becoming more likely to be liquidated.

### How do I pay back my loan?

In order to pay back the loan, you go to the Borrowings section of your dashboard and click on the repay button for the asset you borrowed and want to repay. Select the amount to pay back and confirm the transaction.

In order to avoid the reduction of your health factor leading to liquidation, you can repay the loan or deposit more assets in order to increase your health factor. Out of these two available options, repaying the loan would increase your health factor more.
