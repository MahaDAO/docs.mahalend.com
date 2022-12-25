---
description: >-
  This section explains what are supply/borrow caps and how it is used to
  protect the protocol.
---

# Supply/Borrow Caps

In the event one of the underlying collateral collapses faster than the risk team can possibly delist or stop the borrowing of that asset, borrow/supply caps start to play a role in limiting the possible bad debt that could occur from within collateral collapse.

## **Borrow Caps**

Allow modulation of how much of each asset can be borrowed, which reduces insolvency risk.

By default borrow cap of an asset is 0, which signifies no cap. Anyone who has been granted `RISK_ADMIN` or `POOL_ADMIN` role via the ACLManager can call [`setBorrowCap` method in PoolConfigurator](broken-reference) to update the max total borrow (stable + variable) for the given reserve.

{% hint style="info" %}
In case the `Borrow Cap` of the reserve is set lower than the current `totalDebt` the existing borrowers are not effected but no more borrows (stable or variable) can be initiated for that reserve.
{% endhint %}

## **Supply Caps**

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption><p>Supply cap shown in the UI for a particular asset.</p></figcaption></figure>

Allow limiting how much of a certain asset is supplied to the MahaLend protocol. This helps reduce exposure to a certain asset and mitigate attacks like infinite minting or price oracle manipulation.

By default supply cap of an asset is 0, which signifies no cap. Anyone who has been granted `RISK_ADMIN` or `POOL_ADMIN` role via the ACLManager can call `setSupplyCap` method in PoolConfigurator to update the liquidity supply for the given reserve.

{% hint style="info" %}
In case the Supply Cap of the reserve is set lower than the current liquidity of the reserve, the existing suppliers are not affected, but no more liquidity can be supplied to that reserve.
{% endhint %}

## FAQs

### How are supply/borrow caps assigned?

[Governance](governance.md) can at any point in time appoint `RISK_ADMIN` and `POOL_ADMIN` who have the ability to configure the Borrow and Supply Caps of the individual reserves.
