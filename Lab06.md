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
