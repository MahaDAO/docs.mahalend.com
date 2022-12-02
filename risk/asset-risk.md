# Asset Risk

The composability of DeFi enables the Mahalend Protocol to connect with the rest of the ecosystem; however, it also exposes the protocol to various ecosystem risks. Tokens used in the protocol affect the protocol at its core (specifically tokens accepted as collateral which safeguard the solvency of the protocol). At least three different aspects of risk are important to assessing whether an asset exposes the Mahalend Protocol to undue risk: smart contract risk, counterparty risk, and market risk.

### Smart Contract Risk

Smart contract risk focuses on measuring the technical security of the underlying code for any asset. Only code for assets that have undergone rigorous audits by well-respected auditors are appropriate for the Aave protocol. Beyond audits, smart contract risk remains (i.e., it can never be eliminated fully) and users must be vigilant in assessing such risk. Bug bounties can be used to help reduce smart contract risk. The maturity of any code can be assessed based on the number of days and the number of transactions with a particular smart contract — use, community, development and, in some instances, reliability are proxies for how battle-tested the code is.\


Smart contract hacks have already resulted in billions of funds lost. Accordingly, tokens with the highest smart-contract risk (i.e., D+ and below), are extremely risky collaterals. They should only be onboarded with strict risk mitigation such as supply caps or isolation mode.

### Counter Party risk

Counter-party risk assesses qualitatively how and by who the asset is governed. There are different degrees of governance decentralisation that may give direct control over funds (e.g., as backing) or attack vectors to the governance architecture, which could expose control and funds. Counterparty risk is determined by the level of centralisation, which is measured by the number of parties that control a token’s protocol, as well as the number of holders and the level of trust in the entity, project, community or processes.

### Market Risk

Market risks are linked to the size of a particular asset pool in the protocol, as well as fluctuations in both supply and demand. The markets need to hold sufficient volume to account for any liquidations in the particular pool (i.e., sell offs which tend to lower the price of the underlying asset through slippage affecting the value recovered).

Market risk assessments should use average daily volume representing the availability of the asset to assess liquidity risk: E\[volume]\


The volatility risk is based on the normalised fluctuations in the token price and is calculated as the standard deviation of the logarithmic returns: (check equation) This metric is in line with industry standards used by Bitmex or Gauntlet.

These values should be assessed at the following intervals: 1 week, 1 month, 3 months, 6 months, and 1 year.

Tokens can be subject to sudden volatility spikes, and it is not uncommon to witness a 50% price change within a week or a month. When a price increase occurs, a parameter readjustment may be implemented to limit the risks of new operations.

Finally, we also consider the market capitalisation representing the size of the market and potential exposure.

Market risks are used to calibrate the model’s risk parameters. Volatility helps to define the required level of collateralisation, (i.e., the Loan to Value). The liquidity risks are contained by liquidation incentives (i.e., the liquidation threshold and bonus).
