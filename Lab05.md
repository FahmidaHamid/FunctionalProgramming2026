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

## Exercise 01:

- Write an expression in Haskell that multiplies 10 with every element of the list, given a list of integers and returns the new list.
- Test the expression with three different lists.
- Copy and paste your tested result as multi-line comments in a file called `Lab05<LASTNAME>.hs`.
- Please don't forget to add the exercise number at the beginning of each comment.
 
```haskell
{-
exercise 01

ghci> let exercise01 = map (* 10)

ghci> exercise01 [1..10]

[10,20,30,40,50,60,70,80,90,100]

-}

```

## Exercise 02:


- Write an expression in Haskell that divides every element of the list by 2, given a list of integers and returns the new list.
- Test the expression with three different lists.
- Copy and paste your tested result as multi-line comments in a file called `Lab05<LASTNAME>.hs`.
- Please don't forget to add the exercise number at the beginning of each comment.


## Exercise 03: Recursion

- Can we define our own map function? Let's try. Assume, we call it `myMap`. While
defining the solution, we need to think of two questions:

	- What will be the base cases?

	- What will be the recursive cases?

```
- hint: save in the lab05<LASTNAME>.hs file
 
- 1. the list may be empty? (base case)

myMap func [] = []

- 2. the list is not empty? (recursive case)

myMap func (x:xs) = (func x) : myMap func xs


```
Once defined, test $myMap$ with three different functions (e.g., pred, succ, length, (* 10))
and record their responses right below the definition of myMap as multi-line comment.


## Exercise 04: Our first HoF

```haskell

-- exercise 04: save it in lab05<LASTNAME>.hs

applyTwice f x = f (f x)

```

Answer the following questions:

- How many parameters does applyTwice take?
- What is the type signature? (you may check it with the :t or :type command)
- Test applyTwice with three distinct test cases and record the responses as multi-line comment right below the function definition.
- Predict the output of the following expression and record it as well: applyTwice (map (* 3)) [1..5]

