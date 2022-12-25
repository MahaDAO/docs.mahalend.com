---
description: This section explains what it means to supply liquidity to MahaLend
---

# Supply Collateral

<figure><img src="../.gitbook/assets/image (4) (1).png" alt=""><figcaption><p>A screenshot of the supply page</p></figcaption></figure>

When you supply funds to the protocol, whether to use them as collateral or as a liquidity provider, you will automatically begin earning interest or yield on your funds.

When you deposit collateral into the protocol, you will get mTokens in return that represent your principal in interest that is earned. These mTokens can be redeemed at any time for the underlying asset and can be transferred to any other wallet like a ERC20 token.

The rate of exchange between the native tokens and the tokens deposited is embedded inside the APY (annual percentage yield), i.e., an interest rate determined by the ratio between the supplied and borrowed tokens in a particular market.

{% hint style="info" %}
Currently ARTH is the only asset that can interest from borrowing. All other assets currently don't earn interest from borrowing.
{% endhint %}

### Example

The following transaction below showcases a user depositing `253 ARTH` into the protocol and in return receiving roughly `253 mARTH` in return.

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p><a href="https://etherscan.io/tx/0xe5e89793cad4cec68d0db02f7706ebcdf93bdd6d9bb6c2a5ecbaeec19843e71b">https://etherscan.io/tx/0xe5e89793cad4cec68d0db02f7706ebcdf93bdd6d9bb6c2a5ecbaeec19843e71b</a></p></figcaption></figure>

In this case, the user becomes a liquidity provider as he is providing `ARTH` into the protocol to be used by borrowers who will pay an interest fee if they borrow this `ARTH`.

## FAQs

### How much interest will I earn for supplying collateral?

mTokens holders receive continuous earnings that evolve with market conditions based on:

* **The interest rate payment on loans** - suppliers share the interests paid by borrowers corresponding to the average borrow rate times the utilisation rate. The higher the utilisation of a reserve the higher the yield for suppliers.&#x20;
* **Flash Loan fees** - suppliers receive a share of the Flash Loan fees corresponding to .09% of the Flash Loan volume.

Each asset has its own market of supply and demand with its own APY (Annual Percentage Yield) which evolves with time. You can find the average annual rate over the past 30 days to evaluate the rate evolution, and you can also find more data on the reserve overview of each asset in the home section on the app.

### Is there a minimum or maximum amount to supply?

You can supply any amount you want, there is no minimum or maximum limit. Still, it's important to take into account that for really low amounts it is possible that the transaction cost of the process is higher than the expected earnings. It is recommended that you consider this when supplying very low amounts.&#x20;

### Can I borrow using stable and variable rate at the same time for one asset

No, you can only borrow using stable or variable rate, if you switch to your desired rate it will switch the rate for your whole debt on that asset. Despite this, you can have different borrow rates for different assets.

### How do I withdraw?

To withdraw you need to go to the "Dashboard" section and click on “Withdraw”. Select the amount to withdraw and submit the transaction. Also, you can use your “aTokens" as liquidity without withdrawing.

You would need to make sure there is enough liquidity (not borrowed) in order to withdraw, if this is not the case you would need to wait for more liquidity from suppliers or borrowers repaying.&#x20;

### Can I opt-out my asset from being used as a collateral?

Yes. After supplying your assets, you are able to unselect the asset so that it will not be used as collateral. The opt-out is available in the "Supply" section within your dashboard. Simply switch the "use as collateral" button on the asset you would prefer to opt-out from being used as a collateral.&#x20;

{% hint style="info" %}
You can withdraw your assets without opting out of using them as collateral, as long as those funds are not actively being used to borrow and the withdrawal would cause a liquidation on your loans.
{% endhint %}
