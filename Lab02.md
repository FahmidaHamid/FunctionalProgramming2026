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
[5,10,15,20]

ghci> show x
"[5,10,15,20]"
--	Get the first item of the list

ghci> head x
5
--	Get the rest of the items from the list

ghci> tail x
[10,15,20]
--	Get the total number of items in the list
ghci> length x
4

--	Reverse the list
ghci> reverse x
[20,15,10,5]
--	Append a list with another list

ghci> x ++ [25, 30, 35, 40]
[5,10,15,20,25,30,35,40]

-- Create a list by using pattern (arithmetic series)
	ghci> let p = [1..100]
	ghci> p
	[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,67,68,69,70,71,72,73,74,75,76,77,78,79,80,81,82,83,84,85,86,87,88,89,90,91,92,93,94,95,96,97,98,99,100]

	ghci> let q = [3, 6..90]
	ghci> q
	[3,6,9,12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,72,75,78,81,84,87,90]
 

	ghci> let r = [2, 0..(-20)]

	ghci> r
	[2,0,-2,-4,-6,-8,-10,-12,-14,-16,-18,-20]

	-- Test the following:
	ghci> let t = [1..]
	ghci> t 


```



## Functions 


In Haskell, a function is a fundamental building block that operates on input parameters and returns a result without causing side effects (it is a "pure" functional language). 
Functions are defined by specifying an optional type signature and the function body. 


