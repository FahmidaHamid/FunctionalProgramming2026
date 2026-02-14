*********************************************************
# COP 2930:: Functional Programming                     
## Spring 2026                                          
### Lab 03                                              
*********************************************************


### Topic 01: Types and Typeclasses

Each type is a set of values.

Some standard data types in Haskell are: Bool, Char, String, Int, Integer, Float, Double.

- Bool: True, False
- Int: A fixed precision integer, value ranges from $-2^(63)$ to ($2^(63) - 1$)
- Integer:  An arbitrary precision integer (infinite range of integers)
- Char: Single character, represented with single quotes
- String: An array of characters, represented with double quotes
- Float: Haskell's Float corresponds to single-precision (32-bit) types. 
	- maximum: $3.4 x 10^{38}$ 
	- minimum value $-3.4 x 10^{38}$
- Double: Haskell's Double to double-precision (64-bit) floating-point types.
	- maximum: $1.8 x 10^{308}$
	- minimum: $-1.8 x 10^{308}$

```haskell

fhamid@NSCHNS172 Codes % ghci  -- loading glassgow haskell compiler

GHCi, version 9.6.7: https://www.haskell.org/ghc/  :? for help

ghci> :t True -- checking the type 
True :: Bool

ghci> :t False
False :: Bool

ghci> :t 'a'
'a' :: Char

ghci> :t '*'
'*' :: Char

ghci> :t "COP2930"
"COP2930" :: String

ghci> 


```

#### Checking the maximum and minimum possible value for Int types

```haskell

ghci> maxBound :: Int -- what is the maximum value for Int type?
9223372036854775807

ghci> minBound :: Int -- what is the minimum value for Int type?
-9223372036854775808

```
#### Assigning a Data Type:

```haskell

ghci> let x = 45 :: Int -- this is how we specify the data type to a variable
ghci> :t x
x :: Int

ghci> let p = 10^101 :: Int
ghci> p  
0    -- note: Int is too small to hold the value we tried to specify
 
ghci> let q = 10^101 :: Integer
ghci> q
100000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000

ghci> let z = 10/3 :: Float
ghci> z
3.3333333

ghci> let q = 10/3 :: Double
ghci> q
3.3333333333333335

ghci> 

``` 
- A rational number may be constructed using the % operator.
	- Arbitrary-precision rational numbers, represented as a ratio of two Integer values. 

```haskell

ghci> let r = 10 / 7 :: Rational
ghci> r
10 % 7

ghci> let m = 22 / 6 :: Rational
ghci> m
11 % 3
ghci> 

```
