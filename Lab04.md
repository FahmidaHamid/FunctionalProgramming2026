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

                    [step 5]: 3 + 0 --base case

                [step 6]: 2 + 3

            [step 7]: 1 + 5

        [step 8]: -1 + 6

    [step 9]: 5

- The final computed result is 5

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

- It takes a list containing `Ord` type data (values that belong to Ord type class, in other words, values that are comparable) as input and returns the minimum of them.

- If we try to understand the definition of the function, we should read it like the following:
  - **Base Case:** If the list is has **only one element**, then return that element as minimum.

  - **Recursive Case:** If the list is non-empty and the first two elements in the list are $x$ and $y$, and the rest of the list is $rest$ then compare $x$ to $y$ and depending on the smaller one between the two, call the same function `minimum'` on a new list that has the smaller one and $xs$.

- note that Prelude has already a defined function called `minimum` which does the same task. Hence we used a slightly different name for our function.
