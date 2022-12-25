---
description: This section explains how you can borrow ARTH using the supplied collateral
---

# Borrow ARTH

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>A screenshot of the Borrow popup</p></figcaption></figure>

Borrowing is the primary utility of the MahaLend protocol. With MahaLend you can borrow ARTH against different kinds of collateral allowing you to leverage yourself on these collateral pools.

## Types of Borrowing

There are two types of borrowing. The first is over-collateralized, which makes up the majority of loans the general user will utilize.&#x20;

The second is under-collateralized, or single transaction loans, which are a bit more complex.&#x20;

### Over-collateralized borrowing

All loans and lending protocols require the borrower to put up some collateral to ensure the loan. This is how the protocol can remain solvent and ensure the liquidity providers will never lose their investments. Typically, the borrower will need to overcollateralize, meaning they deposit more value than they borrow. The minimum collateral-to-debt threshold is generally around X and will change based on the market you are borrowing and the current liquidity available to borrow. To know more about how the CD ratio is calculated, please visit the Risk Parameters section below.&#x20;

Your collateral will automatically get liquidated to cover the loan if this **threshold is ever breached**. Depending on the type of collateral a user deposits, this may happen in high-volatility environments, where the value of the collateral depreciates against the value of the borrowed asset. This is an inherent risk to borrowing volatile assets and is why overcollaterization is the safest way to avoid being liquidated.&#x20;

Additionally, borrowers must pay interest on their loans at the closure time. This is how the protocol can provide a yield to liquidity providers. Within the Mahalend ecosystem, there are two interest rate variations. Stable and variable. Similar to a mortgage, you can choose which variation you’d like to pay, and they are both subject to change. However, it differs from mortgages in that interest must only be repaid at the end of the life of your loan. For more information on borrower interest rates and how they are calculated, please see the [Interest Rate Model](../risks/interest-rate-model.md) section.

### Under-collateralized loans or Flash Loans

Under-collateralized loans, or Flash loans, are a feature designed for developers due to the technical knowledge required to execute one. Flash Loans allow you to borrow any available amount of assets without putting up any collateral as long as the liquidity is returned to the protocol within one block transaction.&#x20;

To do a Flash Loan, you will need to build a smart contract that requests a Flash Loan. The contract will then need to execute the instructed steps and pay back the loan + interest and fees, all within the same transaction. A user cannot take out a flash loan without first ensuring the smart contract is correctly written and that the transaction will return the loan. That is how the protocol ensures no risk is taken on by investors.&#x20;

Flash loans are mainly utilized by developers and dApps and have many uses, such as arbitrage and closing/opening/swapping collateralized positions. The average user will likely never utilize flash loans.

## FAQs

### Why would I borrow instead of selling my assets?

Selling your assets means closing your position on that particular asset. Hence, if you are long on the asset, you would not be entitled to the potential upside value gain.&#x20;

By borrowing, you can obtain liquidity (working capital) without selling your assets. Users mainly borrow for unexpected expenses, leveraging their holdings, or new investment opportunities.

### How much I can borrow?

The maximum amount you can borrow depends on your supplied value and available liquidity. For example, you can’t borrow an asset if there is insufficient liquidity or your health factor doesn’t allow you to.&#x20;

You can find every collateral available and its specific parameters for borrowing in the [risk framework](../risks/risk-framework.md) section.

### What asset do I need to repay?

You repay your loan with the same asset you borrowed. For example, if you borrow 1 ARTH, you will pay back 1 ARTH + interest accrued. You can also use your collateral to repay.&#x20;

If you want to pay back the loan based on the USD price, you can borrow any available stablecoins such as USDC, DAI, etc.

### What is the difference between stable and variable rates?

Stable rates act as fixed rates in the short term but can be re-balanced in the long term in response to changes in market conditions. The variable rate is based on the offer and demand in ARTH.&#x20;

As its name indicates, the stable rate will remain pretty stable, and it is the best option to plan how much interest you will have to pay. The variable rate will change over time and could be the optimal rate depending on market conditions. You can switch between the stable and variable rates at any time through your dashboard.

### When could my stable rate be rebalanced?

Stable rate rebalance is expected to be unlikely but will happen if the average borrow rate is lower than 25% APY and the utilization rate is over 95%.

### How do I switch my interest rate type?

To switch your interest rate between stable and variable rate, browse your dashboard and click on the “APR Type” switch button for the asset you wish to apply the rate change.

### Can I borrow using the stable and variable rates simultaneously for one asset?

No, you can only borrow using a stable or variable rate. If you switch to your desired rate, it will switch the rate for your whole debt on that asset. Despite this, you can have different borrowing rates for different assets.

### What is the health factor?

The health factor is the numeric representation of the safety of your deposited assets against the borrowed assets and their underlying value. The higher the value is, the safer the state of your funds is against a liquidation scenario. If the health factor reaches 1, the liquidation of your deposits will be triggered.&#x20;

A Health Factor below 1 can get liquidated. For an HF=2, the collateral value vs. borrow can reduce by 1 out of 2: 50%. The health factor depends on the liquidation threshold of your collateral against the value of your borrowed funds. You can find all of the collateral parameters in the [risk parameter](../risks/risk-framework.md#health-factor) section.&#x20;

If you would like to know more technical details about the health factor calculation, you can find those [here](../risks/risk-framework.md#health-factor).

### What happens when my health factor is reduced?

Depending on the value fluctuation of your supplies, the health factor will increase or decrease. If your health factor increases, it will improve your borrow position by making the liquidation threshold unlikely to be reached. In the case that the value of your collateralised assets against the borrowed assets decreases instead, the health factor is also reduced, causing the risk of liquidation to increase.

### When do I need to pay back the loan?

There is no fixed time period to pay back the loan. You can borrow for an undefined period if your position is safe. However, as time passes, the accrued interest will grow to make your health factor decrease, which might result in your deposited assets becoming more likely to be liquidated.

### How do I pay back the loan?

In order to pay back the loan, you go to the Borrowings section of your dashboard and click on the repay button for the asset you borrowed and want to repay. Select the amount to pay back and confirm the transaction.

In order to avoid the reduction of your health factor leading to liquidation, you can repay the loan or deposit more assets in order to increase your health factor. Out of these two available options, repaying the loan would increase your health factor more.
