% Introduction to functional programming with Haskell
% Winter Term 2015

# 1. Theoretical Part
  - $\lambda$-calculus
  - category theory 

# 2. Practical Part
  - syntax of Haskell
  - lists and lists comprehension
  - types and type classes
  - recursion
  - higher order functions


# Books
[1] Richard Bird:   Thinking Functionally with Haskell, 2014 \newline
[2] Miran Lipovača: [Learn you a Haskell for Great Good](http://learnyouahaskell.com)

\pagebreak

#Introduction (12.10.2015)
|       Imperative programming      |         Functional programming        |
|---|---|
|             $\uparrow$            |               $\uparrow$              |
|           Turing machine          |           $\lambda$-calculus          |
| ```int product = 0;```            | ```factorial(0) = 1```                |
| ```for(int i = 2; i <= n; ++i)``` | ```factorial(n) = factorial(n-1)*n``` |
| ```    product *= i;```           | Haskell: ```product[1..n]```          |
| ```return product;```             |                                       |

$$
  f(x) = x^2 \quad\quad\quad f:D \rightarrow F
$$

___


####Three keypoints of functional progamming:
 - FP is a method of progam constructions that empasize functions and their application rather than commands and their executions
 - PF uses "simple" mathematical notation that allows concise description of problems
 - PF has strong mathemathical basis

___


####The most important properties of Haskell:

1. High Order Functions (HOF)
  If functions are treated as first class values in a language - allowing them to be stored in data-structures, passed as arguments $\rightarrow$ return as results $\rightarrow$ referred as HOF.
  Function map takes a function and approximates it to a list: \newline
  Haskell: `(a -> a) -> [a] -> [a]` \newline
  Example: consider the following function twice $f(x) = f(f(x))$

2. Nonstrict Semantic (Lazy Evaluation)
  Lazy evaluation or call by need is an evaluation strategy which delays the evaluation of an expression until its value is needed, and which also avoids repeated evaluations \newline
  $f(2,\frac{3}{0})$ // something

3. Data abstraction
4. Equation and pattern matching

####Further features
- pure functional
    - `"Hello" ++ "World"`
    - `"Hello" ++ getLine     // compiler Error -> getLine has type IO-String
- type inference
- something
- lazy
- packages

\pagebreak

#$\lambda$-calculus

What is a foundation of mathematics?

- Set theory was introduced by Georg Cantor in 1874-1884
    - $A=\{1,2,3,...\} \rightarrow$ IN
    - $A=\{x | x \in F \}$  //A contains x for $x \in F$ \newline
      $\{x | x < 10 \&\& x > 2 , x\in Z\}$ \newline
      $\rightarrow \{3..9\}$
- Russel Paradox founded in 1901
    - shows that the naive set theory is inconsistent
    - let $R$ be a set of all sets that are not member of themselves
    - 'The barber is a man in town who shaves all those, and only those, men in town who do not shave themselves'
- Axiomatic set theory
    - ZFC(1908-1922) and NBG(1925-1945)
- $\lambda$-calculus introduced in 1930 by Alonso Church
- category theory by Eilenberg and MacLane (1942-1945)
    - Paper [A Short introduction to $\lambda$-calculus](http://pastuhova.ucoz.ru/_ld/0/78_lambda-calculus.pdf) by A. Jung

