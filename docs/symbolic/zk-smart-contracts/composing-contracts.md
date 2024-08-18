# Composing Smart Contracts

ZKFold Symbolic supports an easy smart contract composition within a transaction.

Suppose you want to mint two different kinds of tokens, each kind with its own minting policy. In the case of zkFold Symbolic, those minting policies will be just _forwarding policies_ that delegate all checks to the verification script. As they are extremely cheap, a transaction could have many such policies.

Our transaction-building APIs compose proofs for each policy into a single _final proof_ with a fixed verification cost irrespective of the number of policies. The verification script runs once per transaction and only verifies the final proof.