# Symbolic Smart Contract Type Signature

All zkFold Symbolic smart contracts are Haskell pure functions of transaction data and some auxiliary data. This auxiliary data usually consists of private information available to the parties involved in the transaction. It does not need to be posted on the blockchain.

```Haskell
smartContract :: Transaction a -> AuxiliaryData a -> Bool a
```

Type `Transaction` is a part of our Cardano Type Library. On the other hand, `AuxiliaryData` is a type defined by the smart contract developer.