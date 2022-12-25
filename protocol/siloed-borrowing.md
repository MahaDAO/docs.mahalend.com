# Siloed Borrowing

This feature allows assets with potentially manipulatable oracles (for example, illiquid Uni V3 pairs) to be listed on MahaLend as a single borrow asset i.e., if the user borrows siloed asset, they cannot borrow any other asset.&#x20;

This helps mitigate the risk associated with such assets from impacting the overall solvency of the protocol.

{% hint style="info" %}
Risk or Pool admin, selected by [Governance](../overview/governance.md), can call `setSiloedBorrowing` to set an asset in _Siloed Borrowing_ mode.
{% endhint %}

## Supply Siloed Assets

A user can supply a _Siloed Asset_ just like any other asset using `supply()` method in `pool.sol`, though the asset will not be enabled to use as collateral i.e., the supplied amount will not add to the total collateral balance of the user.

### Borrow Siloed Assets

{% hint style="danger" %}
User borrowing a _siloed asset_ will \_ **not**\_ be allowed to \_\_ borrow \_\_ any other asset\_.\_
{% endhint %}

Users can borrow _Siloed Assets_ using `borrow()` method in `pool.sol` , only if:

* It is first borrowed on behalf of the address

OR

* Existing user debt is of the same _siloed asset._

To check if a user is in Siloed Borrowing state, you can see if the underlying asset borrowed by the user is siloed\_ using `getSiloedBorrowing()` method on AaveProtocolDataProvider.sol.

### Check if Reserved for Siloed Borrowing

```solidity
import {AaveProtocolDataProvider} from '@aave/core-v3/contracts/misc/AaveProtocolDataProvider.sol';
AaveProtocolDataProvider poolDataProvider = AaveProtocolDataProvider(provider.getPoolDataProvider());
// address of the underlying asset
address asset = "0x...";

protocolDataProvider.getSiloedBorrowing(asset);
```
