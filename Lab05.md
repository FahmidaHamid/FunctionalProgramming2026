# COP 2930, Functional Programming
## Spring 2026
## Lab 05: Higher-Order Functions and more Recursion

**************************************************************

 - Points: 13 * 6 = 78

 - Submit: lab05<LASTNAME>.hs [LASTNAME must be your last name]

****************************************************************


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

- Write an expression in Haskell that multiplies 10 with every element of the list, given a list of integers.
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


- Write an expression in Haskell that divides every element of the list by 2.
- Test the expression with three different lists.
- Copy and paste your tested result as multi-line comments in a file called `Lab05<LASTNAME>.hs`.
- Please don't forget to add the exercise number at the beginning of each comment.


## Exercise 03: Recursion

- Can we define our own map function? Let's try. Assume, we call it `myMap`. While
defining the solution, we need to think of two questions:

	- What will be the base cases?

	- What will be the recursive cases?

```
-- hint: save in the lab05<LASTNAME>.hs file
 
-- 1. the list may be empty? (base case)

myMap func [] = []

-- 2. the list is not empty? (recursive case)

myMap func (x:xs) = (func x) : myMap func xs


```
Once defined, test $myMap$ with three different functions (e.g., pred, succ, length, (* 10))
and record their responses right below the definition of myMap as multi-line comment.


## Exercise 04: Our First HoF

```haskell

-- exercise 04: save it in lab05<LASTNAME>.hs

applyTwice f x = f (f x)

```

Answer the following questions:

- How many parameters does `applyTwice` take?
- What is the type signature of the `applyTwice` function? (you may check it with the :t or :type command)
- Test `applyTwice` with three distinct test cases and record the responses as multi-line comment right below the function definition.
- Predict the output of the following expression and record it as well: `applyTwice (map (* 3)) [1..5]`

## Exercise 05: Filter

- **filter** is a higher-order function used to extract elements from a list that satisfy a specific condition. 

- It iterates through a list and returns a new list containing only the elements for which a provided "predicate" function 
evaluates to True.

```haskell

-- test the following

ghci> filter even [1..10]
???
ghci> filter odd [1..10]
???
ghci> filter (> 5) [1..10]
???

```
Note: `even` and `odd` are already defined in the standard Prelude.

Try filter for three unique test cases (exclude the ones provided here) and record the responses as multi-line comments.

## Exercise 06: Lambda Function (aka Anonymous Function)

Lambda function is a way to define a function anonymously (without a name).

** When and why?**

Lambda functions are most useful when you need a quick, one-off logic that doesn't deserve its own name. 
In Haskell, they are primarily used to keep code "local" and readable. They are often used with higher-order functions.



```haskell

-- example
-- condition: find all the values that are greater than 20 and less than 50

ghci> filter (\x -> x > 20 && x < 50) [1..70]
???

```

- Write a valid expression in Haskell to extract (find/filter) all the elements from a list that are divisible by 3 and greater than 20.
- Test it with three different lists.
- Record each test cases as multi-line comments.


## Exercie 07: More filtering with anonymous functions

 

- Write a valid expression in Haskell to extract (find/filter) all the strings from a list of string that are at least 3 characters long.$
- Test it with three different lists.
- Record each test cases as multi-line comments.

## Exercise 08: Filtering on a list of tuples


```haskell

-- note: sometimes we give a temporary name to an expression, like, tuple10
-- tuple10 takes a tuple (x,y) as input and returns True/False based on the specified condition

ghci> let tuple10 = \(x,y) -> x + y == 10 

-- note: now we filter a list of tuples based on the condition

ghci> filter tuple10 [(10, 0), (9, 2), (2,3), (7,3), (12, 2), (12, -2)]

-- sample output

[(10,0),(7,3),(12,-2)]

-- the following will be the same expression


ghci> filter (\(x, y) -> x + y == 10) [(10, 0), (9, 2), (2,3), (7,3), (12, 2), (12, -2)]

[(10,0),(7,3),(12,-2)]

```

- Write a Haskell expression using filter to find all pairs in a list of pairs (aka tuples) where the product of the two numbers is exactly 15.
- Test it with three different list of tuples.
- Record each test cases as multi-line comments.


## Exercise 09: Recursion

- Define our own version of the filter function. Let's call it  ourFilterFunction.
- Test it in five different ways.
- Record each test cases as multi-line comments. 

```
-- sample test cases,
-- please exclude my test cases

ghci> ourFilterFunction (>= 2) [1, -1, 2,-2, 3,-3]
[2,3]

ghci> ourFilterFunction (/= 2) [1, -1, 2,-2, 3,-3]
[1,-1,-2,3,-3]

ghci> ourFilterFunction (\x -> mod x 2 == 0) [1, -1, 2,-2, 3,-3]
[2,-2]

```

## Exercise 10: foldl/foldr 

- Both folds a list into a single value using an accumulating function and an initial value.

- In Haskell, the primary differences between `foldl` and `foldr` are their associativity (left vs. right), 
their behavior with lazy evaluation (ability to work with infinite lists), and 
their performance characteristics regarding memory use


- Consider folding the list [1, 2, 3] with an initial value 0 and a function f (e.g., subtraction -). 

- foldl f z [x1, x2, x3] expands to f (f (f z x1) x2) x3

	- Example: foldl (-) 0 [1, 2, 3] results in (((0 - 1) - 2) - 3), which evaluates to -6.

- foldr f z [x1, x2, x3] expands to f x1 (f x2 (f x3 z))
	
	- Example: foldr (-) 0 [1, 2, 3] results in (1 - (2 - (3 - 0))), which evaluates to 2. 

Example:
```haskell
ghci> foldr (+) 0 [1,2,3,4]
10

ghci> foldr (+) 0 [1,2,3,4]
10

ghci> foldl (-) 0 [1,2,3]
-6

ghci> foldr (-) 0 [1,2,3]
2

```
- Note: Use **foldr** by __default__ in Haskell, especially when working with potentially infinite lists or when the result can be 
produced lazily (e.g., building a new list).

- Avoid using `foldl` due to its tendency to create performance issues with thunks in a lazy language like Haskell.


```haskell

ghci> foldr (+) 0 [1..]
*** Exception: stack overflow

ghci> foldl (+) 0 [1..]
^Zzsh: suspended (signal)

```

- Using a fold function define an expression that decides whether a list contains at least one value greater than 100. Here is how we can define it:


```haskell

ghci> let exprGreaterThan100 = foldr (\x rest -> if x >= 100 then True else rest) False

ghci> exprGreaterThan100 [10, 150, 122, -900, 90, 123, 55, 009]

True


```

Given the idea, define an expression (say, `allGreaterThan100`) that checks if all the elements from a list are greater than or equal to 100.


```haskell

-- sample test cases

ghci> allGreaterThan100 [10, 150, 122, -900, 90, 123, 55, 009]
False

ghci> allGreaterThan100 [110, 150, 122, 900, 190, 123, 155, 1009]
True

ghci> allGreaterThan100 [110, 150]
True

ghci> allGreaterThan100 [110, -150]
False

ghci> allGreaterThan100 []
True

ghci> allGreaterThan100 [1]
False
```

## Exercise 11: Recursion

- Define our own version of foldr function (say, `ourFoldR`).
- Test ite with at least 3 different test cases.
- Record all the test cases along with the results as multi-line comments.

```haskell
-- sample test cases
-- please exclude these

ghci> ourFoldR (+) 0 [1]
1
ghci> ourFoldR (+) 0 [1, 2]
3
ghci> ourFoldR (+) 0 [1, 2, 3]
6
ghci> ourFoldR (+) 0 [1, 2, 3, 4]
10
ghci> ourFoldR (-) 0 [1, 2, 3, 4]
2
ghci> ourFoldR (\x rest -> if x >= 3 then True else rest) False [1, 2, 3, 4]
True
ghci> ourFoldR (\x rest -> if x >= 3 then True else rest) False [1, 2, -3, -4]
False
ghci> 

```

## Exercise 12: zipWith

The `zipWith` function in Haskell combines two lists into a single list by applying a given binary function to corresponding elements from each list. 
It is part of the standard Prelude library and does not require any additional imports. 

```haskell
ghci> zipWith (+) [1,2,3,4] [-1, -2, -3, -4]
[0,0,0,0]

ghci> zipWith (*) [1,2,3,4] [-1, -3, -5, -7]
[-1,-6,-15,-28]

ghci> zipWith (/) [1,2,3,4] [-1, -3, -5, -7]
[-1.0,-0.6666666666666666,-0.6,-0.5714285714285714]

ghci> zipWith (/) [1,2,3,4] [1..10]
[1.0,1.0,1.0,1.0]

```
- Write an expression that uses `zipWith` and some other higher order function to check if two lists (list of numbers or strings) are exactly the same or not.
- Test your expression like the following.

```haskell
ghci> someExpression [1..5] [10,3,2,5,4]
False

ghci> someExpression [1..5] [1..5]
True

ghci> someExpression "Hello" "Hello"
True

ghci> someExpression "Hello" "Hello World"
True

```

## Exercise 13: Recursion

- Implement our own version of the `zipWith` function using recursion. Let's call it `ourZipWithFunc`.
- Test it for at least 3 different test cases.

```haskell
-- please exclude these test cases
ghci> ourZipWithFunc (+) [1..5] [1..10]
[2,4,6,8,10]

ghci> ourZipWithFunc (+) [1..5] [1,1,1,1]
[2,3,4,5]

ghci> ourZipWithFunc (*) [1..5] [1,0,1,0]
[1,0,3,0]

```
