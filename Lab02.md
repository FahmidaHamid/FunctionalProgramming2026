# COP 2930: Functional Programming
# Spring 2026
# 02/11/2026 (Day 03, Lab 02)
# Topic: Functions, Lists, and Haskell Scripts

*********************************************************************************************

## Note: 
	-- We will use Terminal (Mac User) / Command Line Prompts (Windows User) to perform tasks.
	-- Commands are short text instructions you type into a CLI (Command Line Interface) like Windows Command Prompt or macOS/Linux Terminal to perform tasks directly on your system
	-- The lab has two parts: practice and test. You get 20 points each for completing them. 
	-- Submit the practice notes as lab02<LASTNAME>.hs <LASTNAME> should be replaced by your last name. 
	-- The test part is on paper; you will complete the test after submitting the practice part. The test part will be closed book, closed note, no computer; just on paper.

*******************************************************************************************


## Part 01: Getting to Know the Lists

- We have  used ‘let’ to  declare variables that stores a single value. Sometimes we need to store a collection of them, like we need to store the titles of all the classes offered at NCF this Spring. 
In those cases, having individual variables is not ideal. We need to store them in one place, under a single name so we can easily access them. A common and useful data structure to hold multiple values of the same type is list.


- Like many programming languages, Haskell gives us built in data structures using which we can store a collection of similar items. GHCi (or I should say, Prelude, the standard library) also provides some useful functions to handle lists. 
First, we will practice them and then use them for our experiments.



```
--	Declare a list, print/show it
ghci> let x = [5, 10, 15, 20]
ghci> print x
???

ghci> show x
???

--	Get the first item of the list

ghci> head x
???
--	Get the rest of the items from the list

ghci> tail x
???
--	Get the total number of items in the list
ghci> length x
???

--	Reverse the list
ghci> reverse x
???
--	Append a list with another list

ghci> x ++ [25, 30, 35, 40]
???

-- Create a list by using pattern (arithmetic series)
ghci> let p = [1..100]
ghci> p
???

ghci> let q = [3, 6..90]
ghci> q
???
 

ghci> let r = [2, 0..(-20)]
ghci> r
???

-- Test the following:
ghci> let t = [1..]
ghci> t 


```



## Part 02: Functions 


In Haskell, a function is a fundamental building block that operates on input parameters and returns a result without causing side effects (it is a "pure" functional language). 
Functions are defined by specifying an optional type signature and the function body. 

- Create a file **lab02<lastname>.hs**  where <lastname> should be your lastname. 
- Create/Define functions in the file and test them. Save the sample test cases (along with output) as multiline comments, right below the same function.
- I might have given some test cases for some problems. You will have to test your functions on those as well as three new test cases (for each problem/function), making a total of at least 6 distinct test cases per function. Your functions output must match with mine.
- For each problem: you get 4 points for writing/solving the problem and then 6 points for the test cases.
- You will submit the source file (lab02<lastname>.hs) as your work for today.
- There is no need to submit anything for part 01.


### Task 01

Use the definition of **doubleMe** and **doubleUs** discussed in class for this experiment.

Define a function (say, **quadMe**) to replicate the behavior of the following function using only doubleMe $f(x)=4x$.

- Note that doubleMe is not available with standard prelude; so please define the function first and then define quadMe; otherwise, your program will not work.

 ```
- Sample Test Cases:

ghci> quadMe 1
4
ghci> quadMe 2
8
ghci> quadMe 10
40
ghci> 

```

### Task 02:

Define another function, **quadMe2**, that replicates the same behavior  as **quadMe**, this time, only use __doubleUs__. 
- Again, note that doubleUs is not available with the standard prelude; so please define the function first
- Don’t forget to add the test cases.


### Task 03:

We have seen that the standard PRELUDE has already a defined function calle **max** that can help us find the 
maximum value between two inputs. But max directly cannot handle three inputs. Your task is to define a function called 
**maxAmong3** that will take three numbers as input and return the maximum among them. While doing so, you must use the built-in max function.

```
-- Sample Test Cases
ghci> maxAmong3 2 6 1
???
ghci> maxAmong3 2 (-6) 1
???
ghci> maxAmong3 (-6) (-6) (-6)
???
ghci> 

```
