# Use cases

## Complex on-chain smart contracts
Similar to Plutus smart contracts, zkFold Symbolic contracts are specifications. They are boolean predicates that answer the question: does this transaction conform to the rules specified by the developer?

zkFold Symbolic allows developers to implement arbitrary complex smart contract logic and verify smart contract transactions on-chain for a fixed, predictable cost.

## Large-scale decentralized applications
Are you running a decentralized application with lots of daily users? Then, you may benefit from the batching capabilities of zkFold Symbolic smart contracts. You can bundle user transaction requests into a single zkFold Symbolic transaction, thus splitting the fees between all users participating in the batch.

The batch size is only limited by the transaction size limits imposed by the blockchain. The more concurrent users you have, the lower the fees you can charge!

## Privacy-preserving applications
Are you building an application that stores or manipulates private user data? Zero knowledge proof protocols might be the best solution to ensure users have complete control of their data and share only the bits they wish to.

With zkFold Symbolic, you can easily design your own data-sharing protocols in a high-level programming language. Plus, you get access to the state-of-the-art proving systems that can do most (if not all) of the work on edge devices such as smartphones.

## Verifier circuits in recursive proof protocols
Thinking of the easiest way to implement your own recursive proving system? We've got something for you! Implement your verifier algorithm in our high-level functional programming language and get the corresponding circuit for free.

Our framework already includes the implementation of Protostar-like folding and the Plonk verifier as an arithmetic circuit (currently in development).