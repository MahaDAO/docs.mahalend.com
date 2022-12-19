---
description: To borrow you need to supply an asset to be used as collateral.
---

# Borrow ARTH

MahaLend currently supports two types of borrowing. The first is over-collateralized, which makes up the majority of loans the general user will utilize. The second is undercollateralized, or single transaction loans, which are a bit more complex.&#x20;

### Overcollateralized borrowing

All loans and lending protocols require the borrower to put up some collateral to ensure the loan. This is how the protocol can remain solvent and ensure the liquidity providers will never lose their investments. Typically, the borrower will need to overcollateralize, meaning they deposit more value than they borrow. The minimum collateral-to-debt threshold is generally around X and will change based on the market you are borrowing and the current liquidity available to borrow. To know more about how the CD ratio is calculated, please visit the Risk Parameters section below.&#x20;

Your collateral will automatically get liquidated to cover the loan if this **threshold is ever breached**. Depending on the type of collateral a user deposits, this may happen in high-volatility environments, where the value of the collateral depreciates against the value of the borrowed asset. This is an inherent risk to borrowing volatile assets and is why overcollaterization is the safest way to avoid being liquidated.&#x20;

Additionally, borrowers must pay interest on their loans at the closure time. This is how the protocol can provide a yield to liquidity providers. Within the Mahalend ecosystem, there are two interest rate variations. Stable and variable. Similar to a mortgage, you can choose which variation you’d like to pay, and they are both subject to change. However, it differs from mortgages in that interest must only be repaid at the end of the life of your loan. For more information on borrower interest rates and how they are calculated, please see the [Interest Rate Model](../risk/interest-rate-model.md) section.

### Undercollateralized loans

Undercollateralized loans, or Flash loans, are a feature designed for developers due to the technical knowledge required to execute one. Flash Loans allow you to borrow any available amount of assets without putting up any collateral as long as the liquidity is returned to the protocol within one block transaction.&#x20;

To do a Flash Loan, you will need to build a smart contract that requests a Flash Loan. The contract will then need to execute the instructed steps and pay back the loan + interest and fees, all within the same transaction. A user cannot take out a flash loan without first ensuring the smart contract is correctly written and that the transaction will return the loan. That is how the protocol ensures no risk is taken on by investors.&#x20;

Flash loans are mainly utilized by developers and dApps and have many uses, such as arbitrage and closing/opening/swapping collateralized positions. The average user will likely never utilize flash loans.
