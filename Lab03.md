*********************************************************
# COP 2930:: Functional Programming                     
## Spring 2026                                          
### Lab 03                                              
*********************************************************


### Topic 01: Types and Typeclasses

#### a) Types:

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

	- Arbitrary-precision rational numbers are represented as a ratio of two Integer values. 

```haskell

ghci> let r = 10 / 7 :: Rational
ghci> r
10 % 7

ghci> let m = 22 / 6 :: Rational
ghci> m
11 % 3
ghci> 

```

- Haskell has **type inference**.
	
	- If we write a number, Haskell (i.e. ghci) recognizes it as a number.

	- If we write a logical expression, it recognizes that as `Bool`.

```haskell

ghci> let exp = (5 >= 23)
ghci> :t exp
exp :: Bool

ghci> let d = 22 * (11 + 6.7)
ghci> :t d
d :: Fractional a => a
ghci> 

```

#### Checking the Function Types:


```haskell
ghci> [1, 2, 3] ++ [4, 5]
[1,2,3,4,5]
 
ghci> :t (++)
(++) :: [a] -> [a] -> [a] 

-- interpretation: ++  takes 2 list inputs of the same type (say, a) and produces a list of the same type 

```

Here is another example:

```haskell

ghci> aSampleFunction input1 input2 = [input1, input2]
ghci> aSampleFunction 2 3
[2,3]

ghci> aSampleFunction 2 3.5
[2.0,3.5]

ghci> aSampleFunction '2' '3'
"23"

ghci> aSampleFunction [1,2,3] [4,5]
[[1,2,3],[4,5]]

ghci> :t aSampleFunction 
aSampleFunction :: a -> a -> [a]
ghci> 

-- interpretation: aSampleFunction takes two parameters of the same type (let’s call it a) and 
-- makes a list containing values of a type. 

```
**Polymorphic Function:**
 
- A polymorphic function in Haskell is a function that can work with values of different types. 
	- This is achieved using type variables, which are lowercase identifiers in a type signature that can represent any type.

Example:
+  `aSampleFunction` is a polymorphic function that can deal with characters, numbers, lists.

+ `++` is also a polymorphic function that can deal with lists of any type.

#### b) Typeclass:

- Typeclasses are sets of types. 

- The point of type classes is to ensure that certain operations will be available for values of chosen types

- Classes are not types, but categories of types, and so the instances of a class are types instead of values.

- Let's try to understand the idea via this example:

```haskell

class  Eq a  where
   (==), (/=) :: a -> a -> Bool

-- Minimal complete definition:
--      (==) or (/=)

   x /= y     =  not (x == y)
   x == y     =  not (x /= y)

```

+ The definition states that if a type `a` is to be made an instance of the class `Eq`, it must support the functions (==) and (/=) 

+ the class methods (`==` and `/=`),  have type a -> a -> Bool which means the two inputs are of type `a` and the output is a `Bool`.
 
+ Additionally, the class provides default definitions for (==) and (/=) in terms of each other.
 
	+ As a consequence, there is no need for a type in `Eq` to provide both definitions - given one of them, the other will be generated automatically.


Here are some common typeclasses in Haskell:

- typeclass: Num 
    
    - types: Int, Integer, Float, Double

- typeclass: Fractional

	- types: Float, Double

- typeclass: Integral

	- types: Int, Integer

- typeclass: RealFloat

        - types: Float, Double

- typeclass: Ord

        - types: all except IO, IOError, and functions

If interested, you may check this information out: https://en.wikibooks.org/wiki/Haskell/Classes_and_types#/media/File:Base-classes.svg

### Practice Exercise: What does it mean?

```haskell

ghci> check x y = (x+1) == y
ghci> :t check
check :: (Eq a, Num a) => a -> a -> Bool

```

+ As you notice, `check` is a function that takes two parameters (`x` and `y`) as input and returns the result of a comparison `==` between `x+1` and `y`.

+ If we carefully analyze the type signature, what do we see?

	+ x and y must belong to the `Num` and `Eq` typeclasses, i.e., they are not only numbers but also comparable for the equality operations (`==`, `/=`).

+ Finally, we may summarize that the `check` function takes two Nums as input and tests their Equality and returns a Bool (True/False) decision.
 

### Topic 02: Conditionals

- Example 01: Let's define a function `sillyTask1` in a file (definition below), named `lab03.hs`

Notice how each condition composes multi-line instructions.
 
```haskell

sillyTask1 x y =
    if (x > y) then do
       print x
       print "is greater than "
       print y
    else if (y > x) then do
       print y
       print "is greater than "
       print x
    else
       print "they are equal"


```
Here is how we can test it:

```haskell

fhamid@NSCHNS172 Codes % ghci lab03.hs 
GHCi, version 9.6.7: https://www.haskell.org/ghc/  :? for help
[1 of 2] Compiling Main             ( lab03.hs, interpreted )
Ok, one module loaded.

ghci> sillyTask1 3 5
5
"is greater than "
3

ghci> sillyTask1 3 (-5)
3
"is greater than "
-5

ghci> sillyTask1 3 (3)
"they are equal"

```
- Example 02: conditionals with the **guarded expressions** (another and more concise way of writing functions with conditions)

- note: we will use the same source file, `lab03.hs`, for all the exercises for this lab.

```haskell

sillyTask2 x y
    | (x > y) = do
          show x ++ " is greater than " ++ show y
    | (y > x) = do
          show y ++ " is greater than " ++ show x
    | otherwise = "they are equal"

```

Here is how we test it:

```haskell

ghci> sillyTask2  5 4
"5 is greater than 4"

ghci> sillyTask2  4 4
"they are equal"

ghci> sillyTask2  (-4) 4
"4 is greater than -4"

```
- Exercise 01:
$
f(x)= {█(3,x is divisible by 3@5,x is divisible by 5@7,x is divisible by 7@2,for every other case)┤
 $
a)	Write an equivalent function of f(x) in Haskell (all_mods_g), using guarded expressions.
b)	Write an equivalent function of f(x) in Haskell (all_mods_f), using if-else expressions. 
c)	Test both of your functions for at least 5 distinct values of x (e.g. 1, -7, 48, 19, 200). Copy and paste your test results in the file as multiline comments. It is better to place it right after a and b.



## Topic 03: List Comprehension

Haskell list comprehensions provide a concise and expressive way to create lists based on existing lists, 
using a syntax inspired by mathematical set-builder notation.

To continue the lab, let's reuse the same, `lab03.hs`, file.

+ Exercise 02:

```haskell

-- task 01: square all the elements from a list and return a list

squareList xs = [x^2 | x <- xs]

```

Now, let's reload the source file (`lab03.hs`) and try the following test cases:

```haskell

ghci> :t squareList
squareList :: Num a => [a] -> [a]

ghci> squareList []
[]

ghci> squareList [2]
[4]

ghci> squareList [-2]
[4]

ghci> squareList [-2.5]
[6.25]

ghci> squareList [1,2,3,4,5]
[1,4,9,16,25]

ghci> squareList [1,(-2),3,(-4),5]
[1,4,9,16,25]

``` 
I assume you can guess what this function (`squareList`) does. Here is my explanation:

- from the `:t ` command, we get the idea that, `squareList` takes a list of numbers (hint: `Num` and square bracket `[]`) 
as input and produces/returns a list of numbers.

- from the definition of the function (`squareList xs = [x^2 | x <- xs]`), we get the idea that for every element `x` that we
take from the input list `xs`, the function produces `x^2` and put that in a new list.

	- eventually the new list is returned as the output.

	- notice that the input list and output list are of the same length.

	- it is a convention that when we use lists, we usually name the variables like plural words: `xs`, `myList`, etc.


+ Exercise 03:

```haskell

-- what does zip1 do?
-- what are possible input types?
-- save it in the same lab03.hs file 

zip1 xs ys = [(x, y) | x <- xs, y <- ys]


```

Let's test `zip1`:

```haskell

ghci> :t zip1
zip1 :: [a] -> [b] -> [(a, b)]

ghci> zip1 [] []
[]

ghci> zip1 [1] []
[]

ghci> zip1 [1] ['a']
[(1,'a')]

ghci> zip1 [1] ['a', 'b']
[(1,'a'),(1,'b')]

ghci> zip1 [1, 2] ['a', 'b']
[(1,'a'),(1,'b'),(2,'a'),(2,'b')]

ghci> zip1 [1, 2, 3] ['a', 'b']
[(1,'a'),(1,'b'),(2,'a'),(2,'b'),(3,'a'),(3,'b')]

ghci> zip1 [1, 2, 3] ['a', 'b', 'c']
[(1,'a'),(1,'b'),(1,'c'),(2,'a'),(2,'b'),(2,'c'),(3,'a'),(3,'b'),(3,'c')]

```
Answer the following questions (write the responses to the questions right above the function definition in `lab03.hs` as 
multi-line comment):

Questions for you:

 + What does `zip1` do?
	 + Note: in Haskell, and also in many other programming languages, `(a,b)` means a tuple (ordered pair).
 + Do the two input lists have to be of same length for `zip1`?
 + Is `zip1` a polymorhic function?


+ Exercise 04:

Given the definition,

```haskell

tryMe xs = [(x-1, x, x+1)| x <- xs, x `mod` 2 == 0]


```
answer the questions below:

	+ Write 6 test cases for the `tryMe` function.
	+ What type of data can this function handle?
	+ Is `tryMe` a polymorphic function?
	+ What does `tryMe` do?

+ Exercise 05:

Given the following definition,

```haskell

trial_and_error10 xs ys = 
       [(x, y) | x <-xs, y <- ys, (x + y) `mod` 10 == 0 ]


```
answer the questions below:

        + Write 6 test cases for the `trial_and_error10` function.
        + What type of data can this function handle?
        + Is `trial_and_error` a polymorphic function?
        + What does `trial_and_error10` do?

+ Exercise 06:

Define a function (`crazy_10_3`) that takes two lists (`xs` and `ys`) as input and produces tuples `(a, b)` such that 
	+ a is an element from xs
	+ b is an element from ys
	+ (a + b) is divisible by 10 or (a+ b) is divisible by 3

Write 6 test cases for the function, and save the tests as multiline comment right above the `crazy_10_3` function definition 
in the `lab03.hs` file.



