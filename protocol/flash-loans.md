# Flash Loans

Flash Loans are special transactions that allow the borrowing of an asset as long as the borrowed amount (and a fee) is returned before the end of the transaction (also called One Block Borrows). These transactions do not require a user to supply collateral before engaging in the transaction. There is no real-world analogy to Flash Loans, so it requires some basic understanding of how the state is managed within blocks in blockchains. Flash Loans are an advanced concept aimed at developers. You **must** have a good understanding of EVM, programming, and smart contracts to use this feature.

### Overview <a href="#overview" id="overview"></a>

Flash-loan allows users to access the liquidity of the pool (only for reserves for which borrow is enabled) for one transaction as long as the amount taken plus fee is returned or (if allowed) debt position is opened by the end of the transaction. MahaLend offers two options for flash loans:

* \`\``flashLoan:` Allows the borrower to access liquidity of _**multiple reserves**_ in a single _flashLoan_ transaction. The borrower also has the option to open a stable or variable rate debt position backed by supplied collateral or credit delegation in this case. NOTE: _flash loan fee_ is waived for approved `flashBorrowers` (managed by ACLManager)
* \`\``flashLoanSimple`: Allows borrower to access liquidity of a _single reserve_ for the transaction. In this case, the flash loan fee is not waived, nor can the borrower open any debt position at the end of the transaction. This method is gas efficient for those trying to take advantage of the simple flash loan with a single reserve asset.

#### Execution Flow <a href="#execution-flow" id="execution-flow"></a>

For developers, a helpful mental model to consider when developing your solution:

1. Your contract calls the `Pool` contract, requesting a Flash Loan of a certain `amount(s)` of `reserve(s)` using flashLoanSimple() or `flashLoan()`.
2. After some sanity checks, the `Pool` transfers the requested `amounts` of the `reserves` to your contract, then calls `executeOperation()` on `receiver` contract.
3. Your contract, now holding the flash loaned `amount(s)`, executes any arbitrary operation in its code.
   * If you are performing a **flashLoanSimple**, you approve Pool for flash loaned amount + fee when your code has finished.
   * If you are performing **flashLoan,** then for all the reserves either depending on `interestRateMode` passed for the asset, either the Pool must be approved for flash loaned amount + fee or must or sufficient collateral or credit delegation should be available to open debt position.
   * The transaction is reverted if the amount owing is not available (due to a lack of balance or approval or insufficient collateral for debt).
4. All of the above happens in 1 transaction (hence in a single Ethereum block).

#### Applications of Flash Loans <a href="#applications-of-flash-loans" id="applications-of-flash-loans"></a>

Some of the MahaDAO applications include:

* Arbitrage between assets, without having the principal amount to execute the arbitrage.
* Liquidating borrow positions without having to repay the debt of the positions and using discounted collateral claimed to payoff flashLoan amount + fee.

#### Flash loan fee <a href="#flash-loan-fee" id="flash-loan-fee"></a>

The flash loan fee is initialized at deployment to 0.09% and can be updated via Governance Vote. Use `FLASHLOAN_PREMIUM_TOTAL` to get the current value. Flashloan fees can be shared by the LPs (liquidity providers) and the protocol treasury. The `FLASHLOAN_PREMIUM_TOTAL` represents the total fee paid by the borrowers of which:

* Fee to LP: `FLASHLOAN_PREMIUM_TOTAL - FLASHLOAN_PREMIUM_TO_PROTOCOL`
* Fee to Protocol: `FLASHLOAN_PREMIUM_TO_PROTOCOL`

At initialization, `FLASHLOAN_PREMIUM_TO_PROTOCOL` is set to 0.

### Step by step <a href="#step-by-step" id="step-by-step"></a>

#### 1. Setting Up <a href="#1.-setting-up" id="1.-setting-up"></a>

Your contract that receives the flash loaned amounts **must** conform to the IFlashLoanSimpleReceiver.sol or IFlashLoanReceiver.sol interface by implementing the relevant `executeOperation()` function. Also note that since the owed amounts will be _pulled_ from your contract, your contract must give allowance `Pool` to pull those funds to pay back the flash loan amount + premiums.

#### 2. Calling flashLoan() or flashLoanSimple() <a href="#2.-calling-flashloan-or-flashloansimple" id="2.-calling-flashloan-or-flashloansimple"></a>

To call either of the two flash loan methods on the Pool, we need to pass in the relevant parameters. There are 3 ways you can do this.

1. **From an EOA ('normal' ethereum account)**To use an EOA, send a transaction to the relevant `Pool` calling the `flashLoan()` or `flashLoanSimple()` function. See Pool api docs for parameter details, ensuring you use your contract address from step 1 for the `receiverAddress`.\\
2. **From a different contract**Similar to sending a transaction from an EOA as above, ensure the `receiverAddress` is your contract address from step 1.\\
3. **From the **_**same**_** contract**If you want to use the same contract as in step 1, use `address(this)` for the `receiverAddress` parameter in the flash loan method.

Never keep funds permanently on your `FlashLoanReceiverBase` contract as they could be exposed to a 'griefing' attack, where the stored funds are used by an attacker.

#### Completing the flash loan <a href="#completing-the-flash-loan" id="completing-the-flash-loan"></a>

Once you have performed your logic with the flash loaned assets (in your `executeOperation()` function), you will need to pay back the flash loaned amounts if you used `flashLoanSimple() or` `interestRateMode=0` in `flashLoan()`for any of the assets in `modes` parameter.

* **Paying back a flash loaned asset:** Ensure your contract has the relevant amount + premium to pay back the borrowed asset. You can calculate this by taking the sum of the relevant entry in the `amounts` and `premiums` array passed into the `executeOperation()` function.\You **do not** need to transfer the owed amount back to the `Pool`. The funds will be automatically _pulled_ at the conclusion of your operation.
* **Incurring a debt (i.e., not immediately paying back):** If you initially used a `mode=1` or `mode=2` for any of the assets in the `modes` parameter, then the address passed in for `onBehalfOf` will incur debt **if** the `onBehalfOf` the address has previously approved the `msg.sender` to incur debts on their behalf. This means you can have some assets paid back immediately while other assets incur a debt.
