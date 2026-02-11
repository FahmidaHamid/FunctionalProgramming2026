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

### Task 04:

For this problem, your goal is to define a function called **maxAmongThree** that will take 
three numbers as input and return the maximum among them. While doing so, you __must not__ use the 
built-in max function or maxAmong3 or maximum function.


```
ghci> maxAmongThree (-6) (-6) (-6)
???
ghci> maxAmongThree (-6) (-6) 6
???
ghci> maxAmongThree 12 (-6) 6
???

```

### Task 05:
Define a function to help me generate the grades. Name it as gradeBookCalculator. 

- Following is my rubric:
+ 0≤score<60,then grade="F" 
+ 60≤score<70,then grade=D
+ 70≤score<80,then grade=C
+ 80≤score<90,then grade=B
+ 90≤score<100,then grade=A

```
-- Sample Test cases:
ghci> gradeBookCalculator 45
"F"
ghci> gradeBookCalculator 90
"A"
ghci> gradeBookCalculator 80
"B"
ghci> gradeBookCalculator 90
"A"
ghci> gradeBookCalculator 100
"A"
ghci> gradeBookCalculator 75
"C"
ghci> gradeBookCalculator 85
"B"
ghci> gradeBookCalculator 66
"D"
ghci>

```

### Task 06:

Define a function, **squareXY**, that replicates the behavior of the following function: $f(x,y)=x^2+y^2$

```
ghci> squareXY 3 3
18
ghci> squareXY 3 (-2)
13
ghci> squareXY 4 3
25
ghci> sqrt 25
5.0
ghci> squareXY 4 0
16
ghci>

```

### Task 07:

Task 07:

Implement/Define a function called `getTheHeadsTogether` that takes two lists as input and gets 
the heads of each of the lists and returns them as a new list.

```
-- sample test cases and corresponding outputs

ghci> getTheHeadsTogether [1..100] [10, 9 .. 0]
[1,10]

ghci> getTheHeadsTogether "Hello" "World"
"HW"
ghci> getTheHeadsTogether "Hello" "12345"
"H1"

ghci> getTheHeadsTogether "Hello" (reverse "12345")
"H5"

ghci> getTheHeadsTogether "Hello" (head ["Hello", "There", "Funny", "Man"])
"HH"

ghci> getTheHeadsTogether "Hello" (head (reverse(tail ["Hello", "There", "Funny", "Man"])))
"HM"

```
+ Note: Strings (written with double quotes, “”), are also lists. They are lists of characters.

### Task 08:

Define a function, whoIsLonger, that compares two lists and returns the one with more elements. 

```
ghci> whoIsLonger "Hi there! Don't go too fast" "Hi"

"Hi there! Don't go too fast"

ghci> whoIsLonger [1..10] [1..100]

[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,67,68,69,70,71,72,73,74,75,76,77,78,79,80,81,82,83,84,85,86,87,88,89,90,91,92,93,94,95,96,97,98,99,100]
ghci> 


```

### Task 09:

Define a function, `isPalindrome` that takes a single string as input and 
returns True or False based on whether the input string is a palindrome or not.

```
-- Sample Test Cases:
ghci> isPalindrome "racecar"
True
ghci> isPalindrome "racingcar"
False
ghci> isPalindrome ""
True
ghci> isPalindrome "#"
True

```


### Task 10:

Without testing the following function (by just looking at the definition), describe what it does. 

Do not test it on GHCi. We just want to check you can parse the instructions/statements and make some sense out of it.

Record your  response in the same .hs file as a multi line comment.

Mention {-  response to Task 10  …. -} at the beginning of  the explanation block so I can understand.

