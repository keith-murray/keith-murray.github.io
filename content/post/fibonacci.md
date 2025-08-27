---
title: Computing Fibonacci
date: 2025-07-30
tags:
   - math
   - programming
---

## Linear Algebra Done Right
Computing the Fibonacci sequence is a common exercise in your typical 'Intro to Coding' course. The exercise involves an introduction of concepts in dynamic programming in memoization. While the resulting recursive program is efficient, you can actually compute Fibonacci numbers directly with linear algebra.

This exposition was inspired by Excerise 5.C(16) in the Third Eidtion of Sheldon Axler's [_Linear Algebra Done Right_](https://linear.axler.net) textbook.

## The Fibonacci sequence
The Fibonacci sequence $F_1,F_2,\ldots$ is defined by
$$
F_1=1,\quad F_2=1,\quad\text{and}\quad F_n=F_{n-2}+F_{n-1}\text{ for }n\geq 3.
$$
You may have seen the Fibonacci sequence in the context of the so-called "golden spiral".

## Computing Fibonacci numbers
Notice that to compute a Fibonnaci number $F_n$, we have to compute all Fibonnaci numbers $[3,n-1]$. To perform this computation, we can make a simple _recursive_ program.


```python
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)
```

Now let's perform some tests.


```python
for n in [2,5,10,25,40,41]:
    start_time = time.time()
    print(f"Fibonacci({n}) = {fibonacci(n)}")
    print(f"Execution time: {time.time() - start_time:.5f} seconds")
```

    Fibonacci(2) = 1
    Execution time: 0.00002 seconds
    Fibonacci(5) = 5
    Execution time: 0.00000 seconds
    Fibonacci(10) = 55
    Execution time: 0.00001 seconds
    Fibonacci(25) = 75025
    Execution time: 0.00705 seconds
    Fibonacci(40) = 102334155
    Execution time: 9.58250 seconds
    Fibonacci(41) = 165580141
    Execution time: 15.58907 seconds


As you can see, computing Fibonacci numbers $F_1,F_5,F_{10},$ and $F_{25}$ are relatively painless. But computing $F_{40}$ $F_{41}$ takes much longer, with the difference between the two execution times being $>5$ seconds. Why?

This is because our program is highly redundant. To compute $F_n$, we compute $F_{n-1}$ and $F_{n-2}$, but in computing $F_{n-1}$ we also compute $F_{n-2}$. Thus, we are computing $F_{n-2}$ twice. The problem only becomes worse as $n$ approaches $0$ in our program.

To remedy this redundancy, we employ _dynamic programming_. While an exposition of dynamic programming is outside the scope of this notebook, the idea is to create a dictionary, also called a _memo_, that stores the results of computing $F_j$ for $j<n$ and then to return those results when asked.


```python
def fibonacci_memo(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fibonacci_memo(n - 1, memo) + fibonacci_memo(n - 2, memo)
    return memo[n]
```

Now let's rerun our tests from before.


```python
for n in [2,5,10,25,40,41]:
    start_time = time.time()
    print(f"Fibonacci({n}) = {fibonacci_memo(n)}")
    print(f"Execution time: {time.time() - start_time:.5f} seconds")
```

    Fibonacci(2) = 1
    Execution time: 0.00002 seconds
    Fibonacci(5) = 5
    Execution time: 0.00000 seconds
    Fibonacci(10) = 55
    Execution time: 0.00000 seconds
    Fibonacci(25) = 75025
    Execution time: 0.00001 seconds
    Fibonacci(40) = 102334155
    Execution time: 0.00000 seconds
    Fibonacci(41) = 165580141
    Execution time: 0.00000 seconds


Cool right? That took barely any time, and all we did was add a dictionary.

But can we do better? Is there a closed form solution to computing Fibonnaci numbers?

## Linear maps
Let's define the linear map $T\in\mathcal{L}(\mathbf{R}^2)$ by 
$$
T(x,y)=(y,x+y).
$$
Now suppose we had to compute $T^n(0,1)$ for some positive integer $n$. For $n=1,2,3,4,5$, we have
$$T^1(0,1)=(1,1),\quad T^2(0,1)=(1,2),\quad T^3(0,1)=(2,3),\quad T^4(0,1)=(3,5),\quad T^5(0,1)=(5,8).$$
Notice that the $1^{\text{st}}$ coordinate of $T^n(0,1)$ exactly matches $F_n$ and the second coordinate matches $F_{n+1}$. We can even see that $T^6(0,1)$ will produce $8=F_6$. So far, it looks like $T^n(0,1)=(F_n,F_{n+1})$, but can we prove it?

We can prove it with induction. We know that $T^1(0,1)=(F_1,F_2)$, so let our induction hypothesis be 
$$
T^{n-1}(0,1)=(F_{n-1},F_n).
$$
Applying $T$ to both sides, we get 
$$
T^{n}(0,1)=T(F_{n-1},F_n)=(F_n,F_{n-1}+F_n)=(F_n,F_{n+1}).
$$

## Using matrices
So given that we know our linear map $T$ computes Fibonnaci numbers, could we simplify the process of iteratively applying $T$ $n$-times? Consider the following matrix $A\in\mathbf{R}^{2\times 2}$ defined by
$$
A=\begin{bmatrix}0 & 1\\1 & 1\end{bmatrix}.
$$
It's easy to see that for the vector $x^T=\begin{bmatrix}0 & 1\end{bmatrix}$, we can write
$$
A^nx=\begin{bmatrix}0 & 1\\1 & 1\end{bmatrix}^n\begin{bmatrix}0 \\ 1\end{bmatrix}=\begin{bmatrix}F_n \\ F_{n+1}\end{bmatrix}.
$$
Wouldn't it be nice if our matrix $A$ were diagonalizable so that 
$$
A=Q\Lambda Q^{-1}\quad\text{and}\quad A^n=Q\Lambda Q^{-1}Q\Lambda Q^{-1}\cdots Q\Lambda Q^{-1}=Q\Lambda^nQ^{-1}
$$
since $QQ^{-1}=I$. Given $\Lambda$ is a diagonal matrix, $\Lambda^n$ is simply obtained by raising each diagonal entry to the $n$-th power. This would make the computing of Fibonnaci numbers near trivial. Lucky for us, $A$ is indeed diagonalizable. Let's start by findind the eigenvalues of $T$.

### Eigenvalues

To compute the eigenvalues of $T$, we can write
$$
T(x,y)=(\lambda x, \lambda y)\quad\text{and}\quad (y,x+y)=(\lambda x, \lambda y).
$$
Combining $y=\lambda x$ and $x+y=\lambda y$, we have
$$
x+\lambda x=\lambda^2 x
$$
which becomes
$$
0=\lambda^2-\lambda-1
$$
leaving us to find the roots of the polynomial $f(\lambda)=\lambda^2-\lambda-1$. Via the tried and true quadratic formula, it follows that
$$
\lambda=\frac{1\pm\sqrt{5}}{2}.
$$
Hence, the eigenvalues of $T$ are $\lambda_1=\frac{1+\sqrt{5}}{2}$ and $\lambda_2=\frac{1-\sqrt{5}}{2}$. In particular, our eigenvalue $\lambda_1$ is the so-called "golden ratio".

### Eigenvectors

Now let's find the eigenvectors. For $\lambda_1$, we can set $x=1$ and write
$$T(1,y)=(\lambda_1, \lambda_1 y)\quad\text{and}\quad (y,1+y)=(\lambda_1, \lambda_1 y)$$
suggesting that $y=\lambda_1$ and $1+\lambda_1=(\lambda_1)^2$. While initially unbelievable, it is indeed the case that
$$
1+\frac{1+\sqrt{5}}{2}=\Big(\frac{1+\sqrt{5}}{2}\Big)^2,
$$
$$
\frac{3+\sqrt{5}}{2}=\frac{(1+\sqrt{5})^2}{4},
$$
$$
\frac{3+\sqrt{5}}{2}=\frac{6+2\sqrt{5}}{4},
$$
$$
\frac{3+\sqrt{5}}{2}=\frac{3+\sqrt{5}}{2}.
$$
Notice that the same result also holds for $1+\lambda_2=(\lambda_2)^2$. Hence, the eigenvectors of $T$ are
$$q_1=(1,\lambda_1)\quad\text{and}\quad q_2=(1,\lambda_2).$$

### Putting linear algebra to work
At this point, we now have the following algorithm for computing Fibonacci numbers
$$
Q\Lambda^nQ^{-1}x=\frac{1}{\lambda_2-\lambda_1}\begin{bmatrix}1 & 1\\\lambda_1 & \lambda_2\end{bmatrix}\begin{bmatrix}(\lambda_1)^n & 0\\0 & (\lambda_2)^n\end{bmatrix}\begin{bmatrix}\lambda_2 & -1\\-\lambda_1 & 1\end{bmatrix}\begin{bmatrix}0 \\ 1\end{bmatrix}=\begin{bmatrix}F_n \\ F_{n+1}\end{bmatrix}
$$
where $\lambda_2 - \lambda_1 = \det Q$. Let's sanity check this algorithm by writing a python function.


```python
def fibonacci_matrix(n):
    sqrt5 = np.sqrt(5)
    lambda1 = (1 + sqrt5) / 2
    lambda2 = (1 - sqrt5) / 2
    
    Q = np.array([[1, 1], [lambda1, lambda2]])
    Lambda_n = np.diag([lambda1**n, lambda2**n])
    Q_inv = np.array([[lambda2, -1], [-lambda1, 1]]) / (lambda2 - lambda1)
    x = np.array([[0], [1]])
    
    result = Q @ Lambda_n @ Q_inv @ x
    return result[0, 0].item()
```

Like before, let's rerun those tests.


```python
for n in [2,5,10,25,40,41]:
    start_time = time.time()
    print(f"Fibonacci({n}) = {fibonacci_matrix(n)}")
    print(f"Execution time: {time.time() - start_time:.5f} seconds")
```

    Fibonacci(2) = 0.9999999999999999
    Execution time: 0.00020 seconds
    Fibonacci(5) = 5.000000000000001
    Execution time: 0.00003 seconds
    Fibonacci(10) = 55.00000000000002
    Execution time: 0.00002 seconds
    Fibonacci(25) = 75025.00000000006
    Execution time: 0.00001 seconds
    Fibonacci(40) = 102334155.00000013
    Execution time: 0.00001 seconds
    Fibonacci(41) = 165580141.00000024
    Execution time: 0.00001 seconds


While `fibonacci_matrix` is much faster our original `fibonacci` program, it's still beat by `fibonacci_memo` in speed. Also notice that the numbers are not integers as there are small remainders. These remainders occur due to _floating-point precision errors_ in computing with $\sqrt{5}$ in our eigenvalues.

With these issues in mind, we can do better.

From our expression for $Q\Lambda^nQ^{-1}x$ from before, we can write
$$
\frac{1}{\lambda_2-\lambda_1}\begin{bmatrix}1 & 1\\\lambda_1 & \lambda_2\end{bmatrix}\begin{bmatrix}(\lambda_1)^n & 0\\0 & (\lambda_2)^n\end{bmatrix}\begin{bmatrix}\lambda_2 & -1\\-\lambda_1 & 1\end{bmatrix}\begin{bmatrix}0 \\ 1\end{bmatrix}
$$
$$
\frac{1}{\lambda_2-\lambda_1}\begin{bmatrix}1 & 1\\\lambda_1 & \lambda_2\end{bmatrix}\begin{bmatrix}(\lambda_1)^n & 0\\0 & (\lambda_2)^n\end{bmatrix}\begin{bmatrix}-1 \\ 1\end{bmatrix}
$$
$$
\frac{1}{\lambda_2-\lambda_1}\begin{bmatrix}1 & 1\\\lambda_1 & \lambda_2\end{bmatrix}\begin{bmatrix}-(\lambda_1)^n \\ (\lambda_2)^n\end{bmatrix}
$$
$$
\frac{1}{\lambda_2-\lambda_1}\begin{bmatrix}-(\lambda_1)^n + (\lambda_2)^n \\ -(\lambda_1)^{n+1} + (\lambda_2)^{n+1}\end{bmatrix}
$$
implying that
$$
F_n=\frac{-(\lambda_1)^n + (\lambda_2)^n}{\lambda_2-\lambda_1}.
$$
Substituting in the exact values of $\lambda_1$ and $\lambda_2$, we have
$$
F_n=\frac{2}{(1-\sqrt{5})-(1+\sqrt{5})}\Big[-\Big(\frac{1+\sqrt{5}}{2}\Big)^n+\Big(\frac{1-\sqrt{5}}{2}\Big)^n\Big]
$$
which is equivalently expressed as
$$
F_n=\frac{1}{\sqrt{5}}\Big[\Big(\frac{1+\sqrt{5}}{2}\Big)^n-\Big(\frac{1-\sqrt{5}}{2}\Big)^n\Big].
$$
Doesn't it look much nicer? Let's make a new program.


```python
def fibonacci_expression(n):
    sqrt5 = np.sqrt(5)
    lambda1 = (1 + sqrt5) / 2
    lambda2 = (1 - sqrt5) / 2
    
    result = (lambda1**n - lambda2**n)/sqrt5
    return result
```

You know the drill.


```python
for n in [2,5,10,25,40,41]:
    start_time = time.time()
    print(f"Fibonacci({n}) = {fibonacci_expression(n)}")
    print(f"Execution time: {time.time() - start_time:.5f} seconds")
```

    Fibonacci(2) = 1.0
    Execution time: 0.00020 seconds
    Fibonacci(5) = 5.000000000000001
    Execution time: 0.00001 seconds
    Fibonacci(10) = 55.000000000000014
    Execution time: 0.00001 seconds
    Fibonacci(25) = 75025.00000000006
    Execution time: 0.00000 seconds
    Fibonacci(40) = 102334155.00000013
    Execution time: 0.00000 seconds
    Fibonacci(41) = 165580141.00000024
    Execution time: 0.00000 seconds


As you can see, this new program is much quicker, but we still have those pesky floating-point precision errors. The obvious solution would be to simply _round_ those errors off, but if we are going to resort to rounding, we can actually make an _even_ better program.

## Approximating Fibonacci
Let's take another look at our expression for Fibonacci numbers
$$
F_n=\frac{1}{\sqrt{5}}\Big[\Big(\frac{1+\sqrt{5}}{2}\Big)^n-\Big(\frac{1-\sqrt{5}}{2}\Big)^n\Big]=\frac{1}{\sqrt{5}}\Big(\frac{1+\sqrt{5}}{2}\Big)^n-\frac{1}{\sqrt{5}}\Big(\frac{1-\sqrt{5}}{2}\Big)^n.
$$
Do you notice something interesting about the term $\frac{1}{\sqrt{5}}\Big(\frac{1-\sqrt{5}}{2}\Big)^n$? Computing the term for $n=1,2,3,4$, we have
$$
\frac{1}{\sqrt{5}}\Big(\frac{1-\sqrt{5}}{2}\Big)^1=-0.2763\ldots,\quad \frac{1}{\sqrt{5}}\Big(\frac{1-\sqrt{5}}{2}\Big)^2=0.1708\ldots,\quad \frac{1}{\sqrt{5}}\Big(\frac{1-\sqrt{5}}{2}\Big)^3=-0.1055\ldots,\quad \frac{1}{\sqrt{5}}\Big(\frac{1-\sqrt{5}}{2}\Big)^4=0.0652\ldots
$$
The absolute value of each of these terms is less than $\frac{1}{2}$. So if we are going to round our expression of the Fibonacci number, then we don't even need to compute the term $\frac{1}{\sqrt{5}}\Big(\frac{1-\sqrt{5}}{2}\Big)^n$ since rounding will always make up for what we lost. Hence, we can write
$$
F_n=\frac{1}{\sqrt{5}}\Big(\frac{1+\sqrt{5}}{2}\Big)^n.
$$

Are you skeptical? Let's make a fifth and final program to compute Fibonacci numbers.


```python
def fibonacci_approximation(n):
    sqrt5 = np.sqrt(5)
    lambda1 = (1 + sqrt5) / 2    
    result = (lambda1**n)/sqrt5
    return round(result)
```


```python
for n in [2,5,10,25,40,41]:
    start_time = time.time()
    print(f"Fibonacci({n}) = {fibonacci_approximation(n)}")
    print(f"Execution time: {time.time() - start_time:.5f} seconds")
```

    Fibonacci(2) = 1
    Execution time: 0.00005 seconds
    Fibonacci(5) = 5
    Execution time: 0.00001 seconds
    Fibonacci(10) = 55
    Execution time: 0.00001 seconds
    Fibonacci(25) = 75025
    Execution time: 0.00001 seconds
    Fibonacci(40) = 102334155
    Execution time: 0.00000 seconds
    Fibonacci(41) = 165580141
    Execution time: 0.00000 seconds


Isn't that just wonderful? We now have a simple closed-form approximation of Fibonacci numbers with an execution time that rivals our memoization method.

## The power of linearity
In this notebook, we explored how computing the Fibonacci sequence can be performed with brute-force recursion, memoizaiton, linear maps, matrices, eigenvalues, and rounding. I bet you won't be surprised, but there are [even more methods](https://www.nayuki.io/page/fast-fibonacci-algorithms) one can implement to go faster.

From our work, I believe the most striking takeaway is how powerful linearity is. While nonlinear methods have seen widespread adoption in machine learning, the Fibonacci sequence shows us that a great deal can be achieved by finding elegant linear approximations to complex mathematical objects. For more examples of the power of linearity and linear algebra, checkout [my solutions to exercises](https://github.com/keith-murray/linear-algebra-done-right) in Sheldon Axler's _Linear Algebra Done Right_ textbook.
