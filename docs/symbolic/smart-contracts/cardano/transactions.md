# Transactions with Symbolic Smart Contracts

## Building Transactions

Symbolic Framework provides two ways of constructing smart contract transactions: through a backend component API or through JavaScript library functions.

Transaction building routine proceeds as follows:

1. Build an unbalanced transaction satisfying the smart contract.
2. Estimate the fees, including the proof verification script.
3. Balance the transaction using the mock redeemer for the proof verification script.
4. Calculate the proof.
5. Modify the redeemer to include the correct proof.
6. Submit the transaction.

ZKFold off-chain APIs cover steps 2-5 of this process. Step 1 is usually implemented either by DApp developers or 3rd-party tools that build smart contract transactions from schemas.

<!-- ## Composing Smart Contracts

ZKFold Symbolic supports an easy smart contract composition within a transaction.

Suppose you want to mint two different kinds of tokens, each kind with its own minting policy. In the case of zkFold Symbolic, those minting policies will be just _forwarding policies_ that delegate all checks to the verification script. As they are extremely cheap, a transaction could have many such policies.

Our transaction-building APIs compose proofs for each policy into a single _final proof_ with a fixed verification cost irrespective of the number of policies. The verification script runs once per transaction and only verifies the final proof. -->