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
  - **Base Case:** If the list is empty, then return 0
  - **Recursive Case:** If the list is non-empty and the first element in the list is $x$ and the rest of the list is $xs$ then add $x$ to the `sumList` of $xs$.

### How does the process work:

```haskell

sumList [-1, 1, 2 , 3]

    -> -1 + sumList [1, 2 , 3]

            -> 1 +  sumList [2 , 3]

                -> 2 + sumList [3]

                    -> 3 + sumList []

                    -> 3 + 0

                -> 2 + 3

            -> 1 + 5

        -> -1 + 6
    -> 5

- The final computed result is 5

```
