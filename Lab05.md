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

ghci> map (+ 1) [1..5]
???

ghci> map (* 2) [3,2, (-5), 7]
???

ghci> map length ["hello", "hi", "pat"]
??????

ghci> map succ [1..5]
???

ghci> map pred [1..5]
???


ghci> map (3: ) [[1], [1, 2], []]
???

ghci> map (++ [2]) [[1], [1, 2], [3]]
???

``` 
Note:

- __map (+ 1) [1..5]__: map applies function (+ 1) on every element of the list [1,2,3,4,5]
- __map (* 2) [3,2, (-5), 7]__: map applies function (* 2) on every element of the list [3,2, (-5), 7]
- __map length ["hello", "hi", "pat"]__: map applies the length (available with Prelude) function on every string of the list (["hello", "hi", "pat"])

