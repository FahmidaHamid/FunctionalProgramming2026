# COP 2930: Functional Programming

## Spring 2026

## Topic: Recursion

### Week 05, Lab 04

---

# What is Recursion?

**Recursion** is actually a way of defining functions in which the function is applied inside its own definition.

Definitions in mathematics are often given recursively.

```math
\begin{gather*}
f(x) = 2 * f(x-1) + c \\\\

g(y) = g(y/2) + log n \\\\
\end{gather*}

```

Recursion is important to Haskell because unlike imperative languages (e.g., C, Java), we do computations in **Haskell** by **declaring what something is** instead of declaring how you get it.

- That’s why there are no `while` loops or `for` loops in Haskell and instead we many times have to use recursion to declare what something is.

For this lab, let us create a **source file** called `lab04<LASTNAME>.hs`, where `<LASTNAME>` must be replaced with your last name. We will be defining all the functions in this file.

### Example 01:

```haskell

-- sumList function

sumList [] = 0
sumList (x: xs) = x + sumList xs

```

If we load it with the **ghci**, and test with following test cases, we might understand what function `sumList` does.

```haskell
fhamid@NSCHNS172 Codes % ghci lab04.hs

ghci> sumList []
0
ghci> sumList [1]
1
ghci> sumList [-1]
-1
ghci> sumList [-1, 1]
0
ghci> sumList [-1, 1, 2 , 3]
5
ghci> sumList [-1.5, 1, 2.5 , 3.33]
5.33
ghci> :t sumList
sumList :: Num a => [a] -> a
ghci>

```

- So what does `sumList` do?

- It takes a list containing `Num` type data as input and returns the summation of those number.

- If we try to understand the definition of the function, we should read it like the following:
  - **Base Case:** If the list is **empty**, then return **0**
  - **Recursive Case:** If the list is **non-empty** and the first element in the list is $x$ and the rest of the list is $xs$ then **add $x$ to the `sumList` of $xs$**.

### How does the process work:

```haskell

[step 0]: sumList [-1, 1, 2 , 3]

    [step 1]: -1 + sumList [1, 2 , 3]

            [step 2]: 1 +  sumList [2 , 3]

                [step 3]: 2 + sumList [3]

                    [step 4]: 3 + sumList []

                    [step 5]: 3 + 0       <-- base case, check step 4 -->

                [step 6]: 2 + 3   <-------check step 3 -------->

            [step 7]: 1 + 5   <-------check step 2 -------->

        [step 8]: -1 + 6  <-------check step 1 -------->

    [step 9]: 5   <-------check step 0 -------->

-- The final computed result is 5

```

- I hope the basic idea is clear; here is my explanation:
  - The input is broken down to smaller parts until it reaches/hits possible base cases.

  - Once the data hits the base cases, the function immidiately knows what to return.

  - Then the function uses the outcome of the latest stage to compute the result for the next stage using specified formula.

- Example: The base case is when the list is empty, return `0`. Then it adds the returned value from the immediate previous stage to compute the result for the current stage. Once the function reaches the top stage, it alredy has the outcome computed.

### Example 02:

```
-- minimum' function

-- base case
minimum' [x] = x

-- recursive case

minimum' (x: y : rest)
     | (x < y) = minimum' (x: rest)
     | otherwise = minimum' (y : rest)

```

- If we load it with the **ghci**, and test with following test cases, we might understand what function `minimum'` does.

```haskell

ghci> minimum' [3]
3

ghci> minimum' [3, 1]
1

ghci> minimum' [3, 1, 2]
1

ghci> minimum' [3, 1, -2]
-2

ghci> minimum' [-3, 1, -2]
-3

ghci> minimum' [-3/3, 1, -2]
-2.0

ghci> minimum' [-3/3, 1, -2, 0, 11, -11]
-11.0

ghci> :t minimum'
minimum' :: Ord a => [a] -> a
ghci>

```

- So what does `minimum'` do?

- It takes a list containing `Ord` type data (values that belong to `Ord` type class, in other words, values that are comparable) as input and returns the minimum of them.

- If we try to understand the definition of the function, we should read it like the following:
  - **Base Case:** If the list is has **only one element**, then return that element as minimum.

  - **Recursive Case:** If the list is non-empty and the first two elements in the list are $x$ and $y$, and the rest of the list is $rest$ then compare $x$ to $y$ and depending on the smaller one between the two, call the same function `minimum'` on a new list that has the smaller one and $rest$.

- note that Prelude has already a defined function called `minimum` which does the same task. Hence we used a slightly different name for our function.

Now that we have seen a few examples, let's start solving some problems on our own:

### Exercise 01:

- Define a function `productList` using a recursive approach that takes a list of numbers and returns their product. If the list is empty, the function should return 1. Ensure it handles both integers and floats.

```haskell
ghci> productList []
1
ghci> productList [5]
5
ghci> productList [5, 3]
15
ghci> productList [5, 3, 2]
30
ghci> productList [5, -3, 2]
-30
ghci> productList [-5, -3, 2]
30
ghci> productList [-5, -3, 2/3]
10.0
ghci> productList [-5, -3, 2/11]
2.727272727272727
ghci>


```

### Exercise 02:

- Define a function `reverseList` that takes a list of any type and returns a new list with the elements in reverse order. Use a recursive approach and ensure the original list remains unchanged.

```haskell
ghci> reverseList []
[]

ghci> reverseList [2]
[2]

ghci> reverseList ['a']
"a"

ghci> reverseList ['a', 'b']
"ba"

ghci> reverseList "hello"
"olleh"

ghci> reverseList "hello 111222333"
"333222111 olleh"

ghci> reverseList [5, 4,3,2,1]
[1,2,3,4,5]

ghci> reverseList ([100, 20] ++ [1..5])
[5,4,3,2,1,20,100]

```

### Exercise 03:

In the last class/ lab, you handled lists and used list comprehension to produce new lists with various properties. `doubleList` is one such example that takes a list of numbers as input and produces a new list where each number in the original list is doubled.

```haskell
ghci> let doubleMyList xs = [2 * x | x <- xs]
ghci> doubleMyList [1,2,3]
[2,4,6]
ghci> doubleMyList [1]
[2]
ghci> doubleMyList [-1, 3]
[-2,6]
ghci>

```

Now, define a new function `doubleListRecursive` that does the same thing but uses a **recursive approach**. Ensure your function handles the empty list as the base case.

```haskell

ghci> doubleListRecursive []
[]
ghci> doubleListRecursive [2]
[4]
ghci> doubleListRecursive [1,2,3]
[2,4,6]
ghci> doubleListRecursive [-1,-2,-3]
[-2,-4,-6]
ghci> doubleListRecursive [-1.5,-2.5,-3.33]
[-3.0,-5.0,-6.66]

```

### Exercise 04:

Given the following function, write 6 test cases and add them to your `lab04.hs` file as multiline comments (right before the definition):

```haskell

factorial p
   | (p < 0) = error "pls no negative input!"
   | (p == 0) = 1
   | otherwise = p * factorial (p-1)

```

Answer the additional questions after the test cases as well:

    - a) Is `factorial` a recursive function?
    - b) What does it do?
    - c) What is/are the base case(s) [if any]?

### Exercise 05:

Here is another similar function definition (exercise 04).

```haskell

factorialTR p = go p 1

         where
                 go 0 n = n
                 go p n
                   | p > 0 = go (p-1) (p * n)
                   | otherwise = error "pls, no negative input!"

```

Answer the following questions:

- a) Does `factorial` and `factorialTR` do the same thing?

- b) Do you notice any fundamental difference between the two approaches?

[Hint: Tail Recursion, will discuss it after the exam].
