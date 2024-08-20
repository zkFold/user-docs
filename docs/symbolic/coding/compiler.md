# Advanced: Symbolic Compiler

Symbolic computations are functions polymorphic in a type `a` that belongs to a class `Symbolic`. This class places several requirements on the type `a` (see the definition). Most importantly, it must be a finite field.

When a Symbolic function `f` is instantiated with a type `Zp p`,  we can evaluate the function by plugging some concrete value of the input type to get a concrete value of the output type.

```Haskell
x :: Zp BLS12_381_Scalar

f :: Symbolic a => a -> a

f x :: Zp BLS12_381_Scalar
```

However, we can also instantiate such a function with an `ArithmeticCircuit` type. Then, plugging an arithmetic circuit representing the symbol `x`, we get the arithmetic circuit representing `f x`.

```Haskell
-- A circuit representing a "free variable" `x` of type `Zp BLS12_381_Scalar`.
x :: ArithmeticCircuit (Zp BLS12_381_Scalar)

f :: Symbolic a => a -> a

-- A circuit representing `f x`.
f x :: ArithmeticCircuit (Zp BLS12_381_Scalar)
```