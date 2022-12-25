# Interest Rate Model

Liquidity risk materialises when utilisation is high, and this becomes more problematic as $$U$$ gets closer to 100%. To tailor the model to this constraint, the interest rate curve is split in two parts around an optimal utilisation rate $$U_{optimal}$$. Before $$U_{optimal}$$the slope is small, after it begins rising sharply.

The interest rate$$R_t$$follows the model:

$$if \hspace{1mm} U \leq U_{optimal}: \hspace{1cm} R_t = R_0 + \frac{U_t}{U_{optimal}} R_{slope1}$$

$$if \hspace{1mm} U > U_{optimal}: \hspace{1cm} R_t = R_0 + R_{slope1} + \frac{U_t-U_{optimal}}{1-U_{optimal}}R_{slope2}$$

In the borrow rate technical implementation, the calculateCompoundedInterest method relies on an approximation that mostly affects high interest rates. The resulting actual borrow rate is as follows:

$$Actual APY = (1+Theoretical APY/secsperyear)^{secsperyear}-1$$

* When $$U \leq U_{optimal}$$ the borrow interest rates increase slowly with utilisation
* When $$U > U_{optimal}$$ the borrow interest rates increase sharply with utilisation to above 50% APY if the liquidity is fully utilised.

Both the variable and stable interest models, are derived from the formula above from the Whitepaper with different parameters for each asset.

Variable debt sees their rate constantly evolving with utilisation.

Alternatively, stable debts maintain their interest rate at issuance until the specific rebalancing conditions are met. Interest models are optimised by new rate strategy parameter **Optimal Stable/Total Debt Ratio** to algorithmically manage stable rate.

$$if \hspace{1mm} ratio < ratio_{o}: \hspace{1cm} R_{t} = r_{0} + \frac{ratio - ratio_{o}}{1 - ratio_{o}}R_{base}$$

## Model Parameters

First, it’s crucial to distinguish assets used predominantly as collateral (i.e., volatile assets), which need liquidity at all times to enable liquidations. Second, the asset’s liquidity on Mahalend is an important factor, as the more liquidity, the more stable the utilisation. The interest rates of assets with lower liquidity levels should be more conservative.

It is also key to consider market conditions (i.e., how can the asset be used in the current market?). Mahalend's borrowing costs must be aligned with market yield opportunities, or there would be a rate arbitrage with users incentivized to borrow all the liquidity on Mahalend to take advantage of higher yield opportunities.

With the rise of liquidity mining, Maha adapted its cost of borrowing by lowering the _Uoptimal_ of the assets affected. This increased the borrowing costs that are now partially offset by the liquidity reward.

### Variable Interest Rate Model Parameters

Variable rate parameters:

* $$U_{optimal}$$
* Base Variable Borrow Rate
* Variable Rate Slope 1
* Variable Rate Slope 2

### Stable Interest Rate Model Parameters

Stable rate parameters:

* $$U_{optimal}$$
* Base Variable Borrow Rate
* Variable Rate Slope 1
* Variable Rate Slope 2
* Stable to Total Debt Ratio

The stable rate provides predictability for the borrower; however, it comes at a cost, as the interest rates are higher than the variable rate. The rate of a stable loan is fixed until the rebalancing conditions are met:

1. Utilisation Rate: $$U_t > 95\%$$
2. Overall Borrow Rate, the weighted average of all the borrow rates: $$R_O < 25\%$$

{% hint style="info" %}
The assets that are most exposed to liquidity risk do not offer stable-rate borrowing.
{% endhint %}

{% hint style="info" %}
The base rate of the stable rate model corresponds to the average market rate of the asset.
{% endhint %}



## Rate Strategy Volatile One

Volatile assets need liquidity at all times and are thus calibrated at a low Optimal Utilisation Ratio.

{% hint style="info" %}
AAVE, BAL, CRV, DPI, GHST, LINK, SUSHI, WAVAX, WBTC, WETH, WFTM, WMATIC, WONE
{% endhint %}

| Parameters                         | Value |
| ---------------------------------- | ----- |
| Optimal Usage                      | 45%   |
| Base Variable Borrow Rate          | 0     |
| Variable Rate Slope 1              | 4%    |
| Variable Rate Slope 2              | 300%  |
| Base Stable Borrow Rate            | 2%    |
| Stable Rate Slope 1                | 7%    |
| Stable Rate Slope 2                | 300%  |
| Optimal Stable to Total Debt Ratio | 20%   |

## Rate Strategy Stable One

Low liquidity stablecoins have a lower Optimal Utilisation Ratio than those with higher liquidity.

{% hint style="info" %}
DAI
{% endhint %}

| Parameters                         | Value |
| ---------------------------------- | ----- |
| Optimal Usage                      | 90%   |
| Base Variable Borrow Rate          | 0     |
| Variable Rate Slope 1              | 4%    |
| Variable Rate Slope 2              | 60%   |
| Base Stable Borrow Rate            | 2%    |
| Stable Rate Slope 1                | 0.5%  |
| Stable Rate Slope 2                | 60%   |
| Optimal Stable to Total Debt Ratio | 20%   |

## Rate Strategy Stable Two

High liquidity stablecoins are calibrated to lower rates to encourage borrowing.

{% hint style="info" %}
SUSD, USDC, USDT, EURS, JEUR, AGEUR
{% endhint %}

| Parameters                         | Value |
| ---------------------------------- | ----- |
| Optimal Usage                      | 80%   |
| Base Variable Borrow Rate          | 0     |
| Variable Rate Slope 1              | 4%    |
| Variable Rate Slope 2              | 75%   |
| Base Stable Borrow Rate            | 1%    |
| Stable Rate Slope 1                | 0.5%  |
| Stable Rate Slope 2                | 75%   |
| Optimal Stable to Total Debt Ratio | 20%   |

{% hint style="info" %}
When market conditions change, the interest rate parameters must be changed to adapt to utilisation on Mahalend's market as well as to incentives across DeFi.
{% endhint %}

## Supply rate

The borrow interest rates paid are distributed as yield for aToken holders who have supplied to the protocol, excluding a share of yields sent to the ecosystem reserve defined by the reserve factor. This interest rate is generated on the asset that is borrowed out then shared among all the liquidity providers. The supply APY, $$D_t$$, is:

$$S_t = U_t ( SB_t S_t + VB_t V_t)(1-R_t)$$

* $$U_t$$, the utilisation ratio
* $$SB_t$$, the share of stable borrows
* $$S_t$$, the average stable rate
* $$VB_t$$, the share of variable borrows
* $$V_t$$, the variable rate
* $$R_t$$, the reserve factor

The average Supply APY over a period also includes Flash Loan fees.
