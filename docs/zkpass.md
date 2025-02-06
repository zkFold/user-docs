---
title: "zkpass"
description: "The zkPass verifier on Cardano."
author: "zkFold"
date: "2024-10"
PUBLIC: true
---

# zkPass Verifier on Cardano

## Overview

zkPass is a protocol for verification of Web2 data in Web3. Specifically, zkPass's Transgate extension and Transgate SDK allow a DApp to verify the result and authenticity of a user's HTTPS communication with a Web2 server. The result, i.e., the HTTPS responses from the server, can then be verified on a blockchain. In this document we introduce zkPass Verifier, a Plutus smart contract that verifies and stores the results of the zkPass protocol on the Cardano blockchain.

## Specification

Verifying computations on Cardano using zero-knowledge cryptography is fairly straightforward. In order to prove that a computation was performed correctly and produced the expected result, one needs to mint a token that is associated with the hash of the computation result. The token is minted if and only if the computation result is verified in a non-interactive zero-knowledge proof protocol. Thus, the token is the proof that the computation was performed correctly. The biggest advantage of this approach is that the Cardano's off-chain infrastructure facilitates querying for the existence of particular tokens on the blockchain making it extremely cheap and efficient to use and re-use the results of the computations.

Applying this approach to the zkPass protocol, it makes sense to store the whole zkPass result object as transaction metadata so that it too can be easily fetched by various applications.

Below we give the list of conditions that must be satisfied in order to verify the zkPass result on Cardano:

1. Allocator signature on the task metadata must be correct.
2. The hash of `publicFields` must be equal to the `publicFieldsHash` field.
3. Validator signature on the result must be correct.

The zkPass Verifier transactions also include a fee to cover the costs of running zkFold's off-chain infrastructure and zkPass's validator network.

The arithmetic circuit expects that the zkPass result object is hashed into a token name using the _Poseidon hash function_.

The zkPass Verifier minting policy is based on the zkFold's _Plonk Verifier_ script.

For more information about the zkPass protocol, see the [zkPass documentation](https://zkpass.gitbook.io/zkpass/overview/introduction).

## API
The zkPass Verifier API provides functionality for posting and verifying results of zkPass queries on the Cardano blockchain. Below we give the reference implementation of the zkPass Verifier API in Haskell.

The following data types are used in the zkPass Verifier API:

- `ZKPassResult`: A zkPass result object.

The main data type that is used in the zkPass Verifier API is `ZKPassResult`. It is defined as follows:
```Haskell title="Haskell"
data ZKPassResult = ZKPassResult
  { allocatorAddress   :: ByteString
  , allocatorSignature :: ByteString
  , publicFields       :: ZKPassPublicFields
  , publicFieldsHash   :: ByteString
  , taskId             :: ByteString
  , uHash              :: ByteString
  , validatorAddress   :: ByteString
  , validatorSignature :: ByteString
  }
```

To construct a transaction that verifier and posts a zkPass result on Cardano, use the following function:

```Haskell title="Haskell"
zkPassTransaction :: ZKPassResult -> IO Transaction
```

The transaction mints **zkPass** tokens with the hash of the `ZKPassResult` as the token name. The tokens are minted if and only if the `ZKPassResult` object integrity is verified in a non-interactive zero knowledge proof protocol. The transaction can be submitted to the blockchain by normal means.

Alternatively, one may use the following function to post a zkPass result on Cardano in a single function call:

```Haskell title="Haskell"
postZKPassResult :: ZKPassResult -> IO ()
```