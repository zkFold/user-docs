# Building Transactions

We support two ways of constructing zkFold Symbolic smart contract transactions: through a backend component API or through JavaScript library functions.

Transaction building routine proceeds as follows:

1. Build an unbalanced transaction satisfying the smart contract.
2. Estimate the fees, including the proof verification script.
3. Balance the transaction using the mock redeemer for the proof verification script.
4. Calculate the proof.
5. Modify the redeemer to include the correct proof.
6. Submit the transaction.

ZKFold off-chain APIs cover steps 2-5 of this process. Step 1 is usually implemented either by DApp developers or 3rd-party tools that build smart contract transactions from schemas.