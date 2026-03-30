# COP 2930, Functional Programming

## Spring 2026

## Modules, User Defined Types

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

* Example: `Data.List` is a module that has a bunch of useful functions for working with lists and use a function that it exports to create a function that tells us how many unique elements a list has.
  - You may check the module details here: https://hackage-content.haskell.org/package/base-4.22.0.0/docs/Data-List.html

* Create a file called lab06<lastname>.hs and white the following statements. Note that lastname should be your last name.

```haskell
import Data.List

-- type signature

numUniques :: (Eq a) => [a] -> Int

-- function definition

numUniques = length . nub


{-

This is an example of defining a function (numUniques) by using function composition
(notice the dot '.' sign)

numUniques function
1. takes a list as input
2. calls the nub function that removes the duplicates from the list and returns a list with only unique items
3. then calls the length function on the list returned at stage 2 with to count the length of the new list

-}


```

Let's test it.

```haskell

ghci> nub [1,2,3,5,2,3,1,5,-5]
[1,2,3,5,-5]

ghci> length (nub [1,2,3,5,2,3,1,5,-5])
5

ghci> (length . nub) [1,2,3,5,2,3,1,5,-5]
5

ghci> numUniques [1,2,3,5,2,3,1,5,-5]
5

```

- Note that we had to specify the type signature of `numUniques` by ourselves (`numUniques :: (Eq a) => [a] -> Int`); if we comment this line and try to reload, the `ghci` will complain and say something like ` Ambiguous type variable ... arising from a use of ‘nub’`.
- It you check the type signatures of `nub` and `length` separately, you will get the follwing:

```haskell
ghci: :t nub
nub :: Eq a => [a] -> [a]

ghci> :t length
length :: Foldable t => t a -> Int

ghci>

```

- Note:
  - `length` deals with `Foldable` (a typeclass) whereas `nub` deals with `[a]`, i.e. lists.
  - Every list is foldable but every foldable is not a list.
  - Simple example: `foldr` is a higher order and deals with `Foldable` objects. So not everything that is of `Foldable` is a `list`.
  - A List is one specific kind of Foldable container.
