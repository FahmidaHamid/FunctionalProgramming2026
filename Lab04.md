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

g(y) = g(y/2) + log_n \\\\
\end{gather*}

```

Recursion is important to Haskell because unlike imperative languages (e.g., C, Java), you do computations in **Haskell** by **declaring what something is** instead of declaring how you get it. That’s why there are no `while` loops or `for` loops in Haskell and instead we many times have to use recursion to declare what something is.
