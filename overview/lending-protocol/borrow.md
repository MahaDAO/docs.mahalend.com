---
description: To borrow you need to supply an asset to be used as collateral.
---

# Borrow

Mahalend currently supports two types of borrowing. The first is Overcollateralized, which makes up the majority of loans the general user will utilize, and the second is undercollateralized, or single transaction loans which are a bit more complex.&#x20;

### Overcollateralized borrowing

All loans, and lending protocols require the borrower to put up some sort of collateral to ensure the loan. This is how the protocol can remain solvent and ensure the liquidity providers will never lose their investments. Typically, the borrower will need to overcollateralize, meaning they deposit more value, than they borrow. The minimum collateral to debt threshold is generally around X, and will change based on the market you are borrowing, and the current liquidity available to borrow. To know more about how the CD ratio is calculated, please visit the [Risk Parameters](broken-reference) section below.&#x20;

If this threshold is ever breached, your collateral will automatically get liquidated in order to cover the loan. Depending on the type of collateral a user deposits, this may happen in high volatility environments, where the value of the collateral depreciates against the value of the borrowed asset. This is an inherent risk to borrowing volatile assets, and is why overcollaterization is the safest way to avoid being liquidated.&#x20;

Additionally, borrowers must pay interest on their loans at the time of closure. This is how the protocol is able to provide yield to liquidity providers. Within the Mahalend ecosystem there are two interest rate variations. Stable and variable. Similar to a mortgage, you can chose which variation you’d like to pay, and they are both subject to change. However, it differs from mortgages in that interest must only be repaid at the end of the life of your loan. For more information on borrower interest rates, and how they are calculated please see the [Interest Rate Model section](broken-reference).

**Step by step instructions below👇:**

**NOTE:** For a user to be able to borrow they have to make a deposit first.

**Step 1**: Connect your wallet to the Mahalend Application. Ensure you are connected via the XXX blockchain

**Step 2:** Deposit collateral.

**Note:** Once you make a deposit you will be able to borrow from any of the assets available on the 'borrow' page based on your collateral. &#x20;

<figure><img src="../../.gitbook/assets/borrow 1.jpg" alt=""><figcaption><p>All assets which can be deposited into based on your collateral will be listed on the borrow page. </p></figcaption></figure>



**Step 3:** Chose a market you’d like to borrow from and select the amount of funds you want to borrow. The max borrowable amount will be based on your collateral.

Note: Make sure to keep an eye on your health factor. There is a slider that will show you the riskiness of the amount you have chosen to borrow.&#x20;

<figure><img src="../../.gitbook/assets/borrow 2 .jpg" alt=""><figcaption><p>Once you input an amount you will be able to decide whether it's suitable for the borrow process based on the meter that informs you regarding the same.</p></figcaption></figure>



**Step 4:** After this you will be asked to select an interest rate model.&#x20;

<figure><img src="../../.gitbook/assets/borrow 3.jpg" alt=""><figcaption><p>You need to select an interest rate and click on continue. </p></figcaption></figure>



**Step 6:** After you select an interest rate; you will be directed to a 'borrow overview' page.  Here you need to check the details and click on 'approve' if everything is right.&#x20;

<figure><img src="../../.gitbook/assets/borrow 4.jpg" alt=""><figcaption><p>You need to check the details that are displayed and if they are correct you can click on 'approve'. </p></figcaption></figure>



**Step 7:** Once the approval stage is over; you can go to the next step of completing the borrow process. Here you just need to click on 'borrow'.

<figure><img src="../../.gitbook/assets/borrow 5.jpg" alt=""><figcaption><p> The user needs to click on 'borrow to complete the process. </p></figcaption></figure>



**Step 8:** Once you have clicked on 'borrow' you will get a transaction update from your wallet. Once you confirm that the borrow process is complete.&#x20;

<figure><img src="../../.gitbook/assets/borrow 6.jpg" alt=""><figcaption><p>You will get an update on your dashboard regarding the borrow and deposit process. </p></figcaption></figure>

### Undercollateralized loans

Undercollateralized loans, or better known as Flash loans are a feature designed for developers, due to the technical knowledge required to execute one. Flash Loans allow you to borrow any available amount of assets without putting up any collateral, as long as the liquidity is returned to the protocol within one block transaction.&#x20;

To do a Flash Loan, you will need to build a smart contract that requests a Flash Loan. The contract will then need to execute the instructed steps and pay back the loan + interest and fees all within the same transaction. A user cannot take out a flash loan without first ensuring the smart contract is correctly written, and that the transaction will return the loan. That is how the protocol ensures no risk is taken on by investors.&#x20;

Flash loans are mainly utilized by developers, d’apps and has many uses such as arbitrage and closing/opening/swapping collateralized positions. The average user will likely never utilize flash loans.
