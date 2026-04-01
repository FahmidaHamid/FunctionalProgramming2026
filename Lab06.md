# COP 2930, Functional Programming

## Spring 2026

## Modules, User Defined Types (25 points)

### Reminder: Exam 02, next week (Apr 08, 2026)

---

### Reading: Chapter 6 \& 7

---

- A Haskell **module** is a collection of related functions, types and typeclasses.

- A Haskell **program** is a collection of modules where the main module loads up the other modules and then uses the functions defined in them to do something.

```haskell

fhamid@NSCHNS*** 2100Code % ghci recursion.hs
GHCi, version 9.6.7: https://www.haskell.org/ghc/  :? for help
[1 of 2] Compiling Main             ( recursion.hs, interpreted )
Ok, one module loaded.

ghci> :browse

factorial :: (Eq t, Num t) => t -> t
sumList :: Num a => [a] -> a
productList :: Num a => [a] -> a
reverseList :: [a] -> [a]
countFrequency :: (Num a, Eq t) => [t] -> t -> a
findMinimum :: Ord a => [a] -> a
zip1 :: [a] -> [b] -> [(a, b)]

ghci>

```

- Note:
  - Prelude is also a module, which is imported by default.

* The syntax for importing modules in a Haskell script is `import <module name>`. This must be done before defining any functions, so imports are usually done at the top of the file.

## Practice Problem 01: Function Composition & Importing Module

- `Data.List` is a module that has a bunch of useful functions for working with lists.

- You may check the module details here: https://hackage-content.haskell.org/package/base-4.22.0.0/docs/Data-List.html

* Create a file called `lab06<lastname>.hs` and add the following statements. Note that `lastname` should be your last name.

```haskell

import Data.List

-- declare the type signature

numUniques :: (Eq a) => [a] -> Int

-- function definition

numUniques = length . nub


{-

This is an example of defining a function (numUniques) by using function composition
(notice the dot '.' sign)

The numUniques function
1. takes a list as input
2. calls the nub function that removes the duplicates from the input list and returns a new list with only unique items
3. then it calls the length function on returned list (at stage 2) to count the length of the new list

 So, the numUniques function returns the total number of unique items in a given list.

-}


```

Let's test it.

```haskell

ghci> nub [1,2,3,5,2,3,1,5,-5]
[1,2,3,5,-5]

-- same as our function
ghci> length (nub [1,2,3,5,2,3,1,5,-5])
5

ghci> (length . nub) [1,2,3,5,2,3,1,5,-5]
5

ghci> numUniques [1,2,3,5,2,3,1,5,-5]
5

```

- Note that we had to specify the type signature of `numUniques` by ourselves (`numUniques :: (Eq a) => [a] -> Int`); if we comment this line out and try to reload, the `ghci` will complain and say something like ` Ambiguous type variable ... arising from a use of ‘nub’`.

- It you check the type signatures of `nub` and `length` separately, you will find the follwing information:

```haskell

ghci> :type nub
nub :: Eq a => [a] -> [a]

ghci> :type length
length :: Foldable t => t a -> Int
```

- the type signature `length :: Foldable t => t a -> Int` tells us that `length` is a generic function that can count elements in many different types of `containers`, not just `lists`.
  - type structure `t`: `t` could be a `list`, a `tree`, a `set`, or some other foldable structure.
  - `a`: The type of items stored inside that structure

* `length` deals with `Foldable` (a typeclass) whereas `nub` deals with `[a]`, i.e. lists.

* Every list is foldable but every foldable is not a list.

* example: `foldr` is a higher order function and it deals with `Foldable` instances/structures; not everything that is of `Foldable` is a `list`.

* example: `sum` is another function that deals with `Foldable` instances/structures.

* A List is one specific kind of `Foldable container`.

```haskell
ghci> :type sum

sum :: (Foldable t, Num a) => t a -> a

-- interpretation: if some numbers are placed in a foldable structure, sum can work with those and return the summation of the numbers.

ghci> :type foldr

foldr :: Foldable t => (a -> b -> b) -> b -> t a -> b


```

### Practice Problem 02: Using Parenthesis

```haskell

countUniqueItems xs = (length . nub) xs
```

- Now we can test it:

```haskell
ghci> :r
[1 of 2] Compiling Main             ( lab06Hamid.hs, interpreted )
Ok, one module loaded.
ghci> :browse
numUniques :: Eq a => [a] -> Int
countUniqueItems :: Eq a => [a] -> Int
ghci> numUniques [1,2,3,4,1,3,2,3,1,5,1,4,2,1]
5
ghci> countUniqueItems  [1,2,3,4,1,3,2,3,1,5,1,4,2,1]
5
ghci>
```

- Note that though we didn't define the type signature of `countUniqueItems`, GHCi was able to detect/define it. Why?

* `nub` only works on lists

* `length` works on any structure `t` that implements the `Foldable` typeclass

* GHCi looks at the input to the whole chain:
  - Since nub is the first function to receive `xs`, and nub requires a list `[a]`, `xs` must be a list.
  - Because nub requires the elements to be comparable for `equality`, it adds the constraint `Eq a`.

  So, here is the task for you:
  - Define a function that returns the subsequences from a given string (which is also a list of characters) where the subsequences are palindromes.
  - Note: use composition while defining the function.
  - You may use the built-in function `subsequences` [defined in `Data-List` module]

## Exercise 01:

- Define a new function `maxSum` by **composing** maximum and (map sum).
- Call the function on several lists to check the output.

```haskell
ghci> maxSum [[1,2], [4,5], [7,1], [2,4]]
9
ghci> maxSum [[1,2], [4,-5], [7,1], [2,4]]
8
ghci> maxSum [[1,12], [4,-5], [-7,1], [-2,14]]
13
ghci> maxSum [[1,12], [4,-5], [-7,1], []]
13

```

## Exercise 02:

- Define a new function `maxSum2` by using parenthesis as needed. `maxSum2` should do exactly the same operation as `maxSum`.
- Call the function on several lists to check the output.

```haskell
ghci> maxSum2 [[1,2], [5], [-10, 100]]
90
ghci> maxSum [[1,2], [5], [-10, 100]]
90
```

## Practice Problem 03: Function application with `$`

- `$` is called the function application. The `$` function has the lowest precedence. Function application with a space is left-associative (so f a b c is the same as ((f a) b) c)), function application with `$` is right-associative. `$` helps us getting rid of parenthesis.

```haskell
ghci> sqrt 4 + 3 + 9
14.0

ghci> sqrt $ 4 + 3 + 9
4.0

ghci> sqrt (4 + 3 + 9)
4.0

```

- In the first instance, ghci calls `sqrt` on 4 and then adds the result to the rest of the numbers (left-associative: left to right).

- In the second instance, we specify to add the numbers first and then apply the `sqrt` function (same as writing `sqrt (4 + 3 + 9)`). Hence the outcome of the second and third expressions are different from the first one.

- Apart from getting rid of parentheses, `$` means that function application can be treated just like another function. That way, we can, for instance, map function application over a list of functions.

```haskell

ghci> map ($ 9) [(2 +), (10 *), (^ 2), sqrt]

[11.0,90.0,81.0,3.0]

```

## Exercise 03:

- Guess the result for each of the following expressions, then test it with ghci, and note if your guessed answer matched with ghci's interpretation. Put your answers as multi-line comments in the same file.

```haskell
-- a
ghci> map ($ 100) [(10 + ), (10 - ), (10 * ), (10 /)]
???

-- b
ghci> map ($ [10, 20, -10]) [sum, maximum, minimum, head]


```

## Exercise 04:

Like the stated example in (https://learnyouahaskell.github.io/modules.html), create a file, `Geometry.hs`. Compile and test. If everything works fine then do the following:

1. import Geometry module from lab06<lastname>.hs
2. add this line/function: exercise04 xs = map sphereVolume xs
3. test it.

```haskell

ghci> :r
[1 of 3] Compiling Geometry         ( Geometry.hs, interpreted )
[2 of 3] Compiling Main             ( lab06Hamid.hs, interpreted ) [Source file changed]
Ok, two modules loaded.

ghci> exercise04 [1,2,3]
[4.1887903,33.510323,113.097336]

ghci> exercise04 [1,0, -1]
[4.1887903,0.0,-4.1887903]

```

## Exercise 05:

Given the same setup as in Exercise 04, try to add the following function definition to lab06.hs.

```haskell

exercise05 xs = map rectangleArea xs

```

Once done, load/reload and see what happens. Explain the case (as multi-line comments).
