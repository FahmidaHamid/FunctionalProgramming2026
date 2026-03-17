# COP 2930, Functional Programming
## Spring 2026
## Lab 05: Higher-Order Functions and more Recursion


# Higher Order Function

Functions can take functions as parameters and also return functions. The functions that take other functions as parameters are known as Higher order functions. 

## Example:

```haskell
-- map 
-- a higher order function
-- it takes a function and a list and applies that function to every element in the list, producing a new list. 

-- test it

map (+ 1) [1..5]
???

``` 
