# Liquidations

The health of the MahaLend Protocol is dependent on the 'health' of the collateralised positions within the protocol, also known as the 'health factor.' When the 'health factor' of an account's total loans is below 1, anyone can make a `liquidationCall()` to the `Pool` or L2Pool (in case of Arbitrum/Optimism) contract, pay back part of the debt owed and receive discounted collateral in return (also known as the liquidation bonus). This incentivises third parties to participate in the health of the overall protocol by acting in their own interest (to receive the discounted collateral) and, as a result, ensure borrows are sufficiently collateralized. There are multiple ways to participate in liquidations:

1. By calling the liquidationCall() directly in the Pool or L2Pool contract.
2. By creating your own automated bot or system to liquidate loans.

For liquidation calls to be profitable, you must take into account the gas cost involved in liquidating the loan. If a high gas price is used, liquidation may be unprofitable for you. See the Calculating profitability section for more details.V3 allows 100% of the debt (i.e. `MAX_LIQUIDATION_CLOSE_FACTOR`) to be liquidated in single `liquidationCall()` if: `HF < CLOSE_FACTOR_HF_THRESHOLD`

### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

When making a `liquidationCall()`, you must:

* Know the account (i.e., the Ethereum address: `user`) whose health factor is below 1.
* Know the valid debt amount and asset (i.e. `debtToCover` & `debtAsset`)
  * If the HF is above `CLOSE_FACTOR_HF_THRESHOLD`, then only a maximum of 50% (i.e. `DEFAULT_LIQUIDATION_CLOSE_FACTOR`) of the debt can be liquidated per valid `liquidationCall()`
  * If the HF is below `CLOSE_FACTOR_HF_THRESHOLD`, then 100% (i.e. `MAX_LIQUIDATION_CLOSE_FACTOR`) of the debt can be liquidated in a single valid `liquidationCall()`
  * You can set the `debtToCover` to `uint(-1)` and the protocol will proceed with the highest possible liquidation allowed by the close factor.
  * You must already have a sufficient balance of the debt asset, which will be used by the `liquidationCall` to pay back the debt. You can use `flashLoan` for liquidations 😉
* Know the collateral asset `collateralAsset` you closing, i.e., the asset that the user has `backing` their outstanding loan that you will receive as a `bonus`.
* Whether you want to receive _aTokens_ or the underlying asset after a successful `liquidationCall()` .

### Getting accounts to liquidate <a href="#getting-accounts-to-liquidate" id="getting-accounts-to-liquidate"></a>

"User Account" in the Aave Protocol refers to a single Ethereum address interacting with the protocol. This can be an externally owned account or contract. Only user accounts that have HF < 1 can be liquidated. There are multiple ways you can get the health factor:

#### On Chain <a href="#on-chain" id="on-chain"></a>

1.  To gather user account data from on-chain data, one way would be to monitor emitted events from the protocol and keep an up-to-date index of user data locally.

    a. Events are emitted each time a user interacts with the protocol (supply, borrow, repay, withdraw, etc.)
2. When you have the user's address, you can simply call `getUserAccountData()`, to read the user's current healthFactor. If the HF < 1, then the account can be liquidated.

#### GraphQL <a href="#graphql" id="graphql"></a>

1. Similarly to the sections above, you will need to gather user account data and keep an index of the user data locally.
2. Since GraphQL does not provide real-time calculated user data such as `healthFactor,` you will need to compute this locally. The easiest way is to use the MahaLend-utilities SDK, which has methods to compute user summary data.

### Executing the liquidation call <a href="#executing-the-liquidation-call" id="executing-the-liquidation-call"></a>

Once you have the account(s) to liquidate, you will need to calculate the amount of collateral that can be liquidated:

1. Use `getUserReserveData()`​
2. Max debt that is cleared by a single liquidation call is given by the `DEFAULT_LIQUIDATION_CLOSE_FACTOR`(when `CLOSE_FACTOR_HF_THRESHOLD < HF < 1`) or `MAX_LIQUIDATION_CLOSE_FACTOR` (when `HF < CLOSE_FACTOR_HF_THRESHOLD`)
   1. `debtToCover = (userStableDebt + userVariableDebt) * LiquidationCloseFactor`
   2. You can pass `uint(-1)`, i.e. `MAX_UINT`, as the `debtToCover` to liquidate the maximum amount allowed.
3. Max amount of collateral that can be liquidated to cover debt is given by the current _liquidationBonus_ for the reserves that have `usageAsCollateralEnabled` as true.
   1. `maxAmountOfCollateralToLiquidate = (debtAssetPrice * debtToCover * liquidationBonus)/ collateralPrice`

### Calculating profitability vs. gas cost <a href="#calculating-profitability-vs-gas-cost" id="calculating-profitability-vs-gas-cost"></a>

One way to calculate the profitability is the following:

1. Store and retrieve each collateral's relevant details, such as an address, decimals used, and liquidation bonus.
2. Get the user's collateral balance (aTokenBalance).
3. Get the asset's price according to MahaLend's oracle contract using `getAssetPrice()`.
4. The maximum collateral bonus received on liquidation is given by the `maxAmountOfCollateralToLiquidate * (1 - liquidationBonus) * collateralAssetPriceEth`
5. The maximum cost of your transaction will be your gas price multiplied by the amount of gas used. You should be able to get a good estimation of the gas amount used by calling `estimateGas` via your web3 provider.
6. Your approximate profit will be the value of the collateral bonus (4) minus the cost of your transaction (5).

### Appendix <a href="#appendix" id="appendix"></a>

#### How is the liquidation bonus determined? <a href="#how-is-liquidation-bonus-determined" id="how-is-liquidation-bonus-determined"></a>

Liquidation bonuses for all the assets are evaluated and determined based on each asset's liquidity risk and updated via the MahaLend Governance process.
