# Plonk Verifier Tokens

## Overview
Plonk Verifier script is a Plutus script (minting policy) that enables minting of tokens based on the verification of a Plonk proof. The statement that is being verified is encoded into the script parameter: different statements correspond to different minting policies. This statement must be expressed as a Plonk arithmetic circuit and must contain a single public parameter belonging to the scalar field of BLS12_381 elliptic curve. The Plonk Verifier script execution succeeds in two cases:
- when the tokens are being burned, or
- when the Plonk proof is valid and the minted token's name is the byte representation of the public input.

## Type Signature 

Plonk Verifiers allow developers to ask the network to verify essentially any statement. Using the zkFold Symbolic framework, developers can express these statements as Haskell functions with the following type signature:

```Haskell
statement :: (Symbolic c, SymbolicData x) => FieldElement c -> x -> Bool c
```

## Usage
A Plonk Verifier token corresponds to a combination of a statement (minting policy) and a public input (token name). The mere existence of such a token on the blockchain is a proof that the statement with the corresponding public input has been verified by the network.

These tokens can be used in various scenarios, such as gating access to a service or a resource, both off-chain or on-chain. For example, a token can be minted if a user has completed a registration process on a platform. In this case, the public input could be the hash of user data. The token can then allow the user to prove (parts of) their data selectively to other parties.