# COP 2930: Functional Programming
# Spring 2026
# 02/04/2026 (Day 02, Lab 01)
# Topic: Writing Basic Expressions

*********************************************************************************************

## Note: 
	-- We will use Terminal (Mac User) / Command Line Prompts (Windows User) to perform tasks.
	-- Commands are short text instructions you type into a CLI (Command Line Interface) like Windows Command Prompt or macOS/Linux Terminal to perform tasks directly on your system
	-- The lab has two parts: practice and test. You get 20 points each for completing them. 
	-- Submit the practice notes as lab01<LASTNAME>.txt <LASTNAME> should be replaced by your last name. 
	-- The test part is on paper; you will complete the test after submitting the practice part. The test part will be closed book, closed note, no computer; just on paper.

*******************************************************************************************


## Practice Sheet

## Basic Commands:

+ To load **GHCi** (latest version of Glassgow Haskell Compiler), type the following on your command prompt:

```
fhamid@NSCHNSXYZ ~ % ghci
```
If the compiler was installed properly, the prompt would show something like the following:

```
GHCi, version 9.6.7: https://www.haskell.org/ghc/  :? for help

ghci> 

```

+  To quit the ghci, type **:q** on the terminal

```
ghci> :q

Leaving GHCi.

```

+ To clear the screen, type __:! clear__ (for mac/linux) or __:! cls__ (for windows)

+ To change the prompt to ``cop2930'', type **:set prompt “cop2930> ”**

```

ghci> :set prompt "cop2930>"

cop2930>


```
** note: we changed the prompt just for fun, in case you want to change it to something you like

+ Standard Prelude: 

-- Prelude is a module that contains a small set of standard definitions and is included automatically into all Haskell modules.

-- The standard Prelude is automatically loaded every time you start GHCi, providing all the basic, commonly used functions and types without requiring an explicit import.

-- In GHC version 9.x and later, the default prompt is simply ghci>, but the Prelude is still implicitly loaded.
 
----------------------------------------------------------------------------------------

## A) Writing Arithmetic Expressions
 
Haskell can deal with numbers and common arithmetic operations (add, subtract, multiply, divide, modulo). First, we practice writing some of those.

	
### Lesson: An expression evaluates to a value and has a static type. 

Example: 3 + 4 is an expression which is evaluated to a value 7

Note: A static type is a property of an expression determined at compile-time, before the program is run. 

----------------------------------------------------------

### i) Basic Arithmetic Operators (+. -, *, /):
	
Try the following instructions and record your output (copy each instruction and the result in a file named lab01LASTNAME.txt)

```
	cop2930>45 + 44
	?

	cop2930>19 - 111 - 12 + 17
	?

	cop2930>45.6 - 55.12 + 11
	?

	cop2930>66
	?

	cop2930> 25 / 5
	?

	cop2930>23 / 2
	?

	cop2930>22 / 7
	?

	cop2930>66 * 0.1
	?

	cop2930>2 ** 3
	?

```


You may have noticed that Haskell Compiler/GHCi can handle real numbers (integers and rational numbers). 

Later we will learn how Haskell handles complex/imaginary numbers.

#### Type Checking: command **:t**

```
cop2930>:t 4 + 6

4 + 6 :: Num a => a

```

** GHCi’s interpretation of the instruction in plain English:**
 
You gave me an expression which contains some a (something that I recognize as a Num, short of Number and I will return you something like an a, meaning some Num).
 
“=>” usually means “returns” and

“::” means “given the left-hand-side as input”

You may also use **:type** to ask for the type of the expression

```
cop2930>:t (34 + 99) * 5

(34 + 99) * 5 :: Num a => a

cop2930>:t (34 + 99) * 5.1

(34 + 99) * 5.1 :: Fractional a => a

```

In next class, will talk about Type and Type-classes; for now, you may assume that 

"Fractional" is used to indicate rational numbers and Num is used to indicate any type of Numbers.
 
Hence, Fractional is a subtype of Num.

Here's the set of numbers we usually use: 

+ Natural Numbers (N): {1, 2, 3, ...} (Used for counting).
+ Whole Numbers (W): {0, 1, 2, 3, ...} (Natural numbers plus zero).
+ Integers (Z): {..., -2, -1, 0, 1, 2, ...} (All whole numbers and their negatives).
+ Rational Numbers (Q): Numbers expressible as a fraction (e.g., 1/2, -3/4).
+ Real Numbers (R): All rational and irrational numbers (like  { … , √2, 2√3,  𝜋, ….}, etc.), representing all points on a number line. 


### ii) Expressions with Parenthesis:

In Haskell, square brackets [] are reserved for Lists, and curly braces {} are used for Record syntax or layout blocks. For mathematical grouping, only parentheses () are valid. 
Test each of the following expressions:

```
cop2930> (3 + 3)
?
cop2930>(3 - (-3)) 
?
cop2930>(3 - (-3 + 5))
?
cop2930>3 - -3 + 5
?
cop2930>3 - (-3) + 5?

```
In second expression, (-3) is used to negate a value. 

The 4th expression 4 is supposed to produce an error. Carefully go over the error message.


### Infix, Prefix, Postfix Notation

``` 

+	Infix notation: 3 + 5 
+	Prefix notation:  (+) 3 5 
+	Postfix Notation: 3 5 (+)

Infix Notation (Standard for operators): Functions whose names consist entirely of symbols (like +, *, ==, etc.) are used with infix notation by default, where the operator is placed between its two arguments.  

Haskell uses both prefix and infix notation, with the notation used depending on how a function is defined and called. 

Postfix notation (example: 3 5 (+)) is generally not part of standard Haskell syntax.


```

###  iii) Variables:

-- In programming, a variable is a named storage location in a computer's memory that holds a value or data, 
which can be changed during the execution of a program.
 
-- Variables are fundamental building blocks that allow programs to store, retrieve, 
and manipulate information dynamically.

```
cop2930>let x = 4 + 3**2

cop2930>x
?

```

We may declare variables without the **keyword** `let`:

```

ghci> x = 10
ghci> y = 5
ghci> z = x + 2 * y
ghci> z
?
ghci> x
?
ghci> y
?

```

In Haskell, "variables" are names for expressions that hold immutable values; 
once a value is bound to a name within a specific scope, it cannot be changed or reassigned. 
This concept is closer to mathematical variables or constants in imperative languages (C).

Test the following:

```
ghci> x = 15
ghci> x = 22
ghci> x
?

```

Now, try the following:

```
ghci> x = 2 * x
ghci> x
?

```
-- Try to explain the behavior.
-- You may use Google/other sources. It's okay if you don't/cant explain it now.


### iv) Comments:

Sometimes we write some statements not for the compiler to execute but for ourselves to remember some clues or to explain the idea. We call them commands. 
Haskell considers ```--``` as an indication of a comment.

```
ghci> x = 3**2 + 9 - 2* 10 -- a complicated expression
ghci> x

```


## B) Writing Boolean (Logical) Expressions

A Boolean expression is a logical formula used in programming and digital circuits that evaluates to one of two values: true (1) or false (0).
 
Composed of Boolean constants, variables, and operators (AND, OR, NOT, XOR), 
these expressions are essential for decision-making and controlling program flow. 

They are fundamental in constructing conditions for loops, If statements, 
and digital logic gates. 


 + and operator: `&&`
 + or operator: `||`
 + not operator: `not` (unary operator)

Truth table for `&&` and `||` operations:

|  **x**  |  **y**  |  `&&`    |  `||` |
 
|:-----:|:-----:|:------:|:-------:|

| False | False | False  | False   |   
| False | True  | False  | True    |   
| True  | False | False  | True    |    
| True  | True  | True   | True    | 


Truth table or not operation:

| **x** | not |
|:-----:|:--------:|
| False | True     |
| True  | False    |


Try the following expressions and record the responses:

```
ghci> (True || False)
?
ghci> True && False
?
ghci> (True || False) && False
?
ghci> (True || False) && (not False)
?
ghci> (True || False) && (not (not False))
?
ghci> (not (True || False)) &&  (not False)
?
ghci> (not (True || False)) && (not  (not False))
?

```

#### Testing Equality:

```
ghci> 1 == 600
?
ghci> 1 == (600 / 100)/6
?
ghci> 5 /= 5 --not equal
?
ghci> 5 /= 6 --not equal
?

```

#### Comparison:

```
ghci> 5 >= (6 * 23)
?
ghci> (5**10) >= (6 * 23)
?
     ghci> -3 < -100
?

```

### Functions

In Haskell, a function is a mathematical concept that maps a set of inputs to a set of outputs, without producing side effects or modifying global state. They are defined by a type signature (optional but recommended) and one or more bindings (equations) that specify their logic. 

In Haskell, functions are called by writing the function name, a space and then the parameters, separated by spaces.

We will check some built-in functions today, learn more later:

```
ghci> succ 1
?
ghci> succ 4
?
ghci> pred 4
?
ghci> pred (-1)
?
ghci> pred 100
?

ghci> max 4 5
?
ghci> max 4 (-5)
?
ghci> min 3 1
?
ghci> min (min 3 1) (-2)
?
ghci> min (max 4 5) (min 34 24)
?


```


# That’s it for today. 

# We will learn more in the next session.

# Please collect the second part of the lab from your professor, complete it, submit and then you are done for the day :)

