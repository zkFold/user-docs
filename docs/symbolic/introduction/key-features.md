# Key Features

## High-level language with a performance of a low-level one
zkFold Symbolic compiler generally produces near-optimal arithmetic circuits from the high-level Haskell code. Developers are free to implement their custom optimizations and introduce new arithmetizable types using code snippets written in the lower-level eDSL.

## Correct-by-construction arithmetic circuits from your code
Coding arithmetic circuits in a low-level language bears a significant probability of introducing errors that invalidate the security of the underlying business logic.

zkFold Symbolic provides built-in tests for any user-generated function. In particular, the tests verify that the function and its circuit representation implement the same map from inputs to the output. Besides, the zkFold Symbolic compiler is very compact, spanning just a few thousand lines of code, making it easy to audit.

## No experience in zero knowledge protocols is required
In zkFold Symbolic, developers implement statements to prove and verify as pure, polymorphic Haskell functions. The complementing zero knowledge proof protocols are provided as easy-to-use APIs. Thus, in-depth knowledge of the underlying cryptography is not required.

## Support for the state-of-the-art ZKP protocols
zkFold Symbolic comes with several state-of-the-art zero knowledge proof protocols that work out of the box. We are constantly upgrading and adding new supported protocols as new research comes out.