# Liquidity Risk

The Mahalend Protocol is a decentralized, non-custodial liquidity protocol that enables the supplying and borrowing of different cryptoassets from liquidity pools, and earning interest on cryptoassets supplied.

The liquidity of the protocol is measured by the availability of assets for basic protocol operations such as borrowing assets backed by collateral and claiming supplied assets along with accrued yield. It is a key metric, as a lack of liquidity will block operations.

At any point in time, the liquidity of the protocol can be assessed through the utilization ratio. The utilization ratio essentially measures the amount of liquidity provided to the protocol vs the amount borrowed of each asset. This gives the user a picture of how much liquidity there is available for each asset.  A way Mahalend mitigates liquidity risk is through the borrowing interest rate model.

Mahalends’s interest rate algorithm is created to ensure liquidity while also maximizing utilization of funds. The borrow interest rates are derived from the Utilisation Rate

U is an indicator of the availability of capital within the pool. The interest rate model manages liquidity risk in the protocol through user incentives to support liquidity:

* When capital is available - the protocol deploys low interest rates in order to encourage borrowing
* When capital is scarce - the protocol deploys high interest rates in order to encourage repayments of debt and incentivize additional supplying.&#x20;
