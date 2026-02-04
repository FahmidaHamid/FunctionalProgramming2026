# COP 2930: Functional Programming
# Spring 2026
# 02/04/2026 (Day 02, Lab 01)

*********************************************************************************************

### Note: 
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

+ To clear the screen, type ** :! clear ** (for mac/linux) or ** :! cls ** (for windows)

+ To change the prompt to ``cop2930'', type **:set prompt “cop2930> ”**

```

ghci> :set prompt "cop2930>"

cop2930>


```
** note: we changed the prompt just for fun, in case you want to change it to something you like

----------------------------------------------------------------------------------------

## A) Writing Arithmetic Expressions
 
Haskell can deal with numbers and common arithmetic operations (add, subtract, multiply, divide, modulo). First, we practice writing some of those.

	
### Lesson: An expression evaluates to a value and has a static type. 

Example: 3 + 4 is an expression which is evaluated to a value 7

Note: A static type is a property of an expression determined at compile-time, before the program is run. 

----------------------------------------------------------

	
+ Try the following instructions and record your output (copy each instruction and the result in a file named lab01<LASTNAME>.txt)

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

