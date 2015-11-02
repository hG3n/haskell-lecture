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

#Introduction
#### Lecture 1 (12.10.2015)

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
      $\{x | x < 10\ \&\&\ x > 2 , x\in \mathbb{Z} \}$ \newline
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


___


#### Lecture 2 (19.10.15)

### Typed and untyped:
- $\lambda$-calculus developed by Anlonzo Church in 1930s
- One of original goals was to construct a formal system for the foundation of mathematics by having a system of functions together with a set of logical notions
- When it tuned out that the constructed system was inconsistent Church this program was forgotten by him.
- Then later Church separated the consistent subsystem and focussed on comptability.
- known as untyped $\lambda$-calculus
- Systems using $\lambda$-calculus:
    - LISP (not based on $\lambda$-calculus)
    - ML
    - Haskell

___


### untyped $\lambda$-calculus
- The $\lambda$-calculus is a calculus of pure functions
- Let us consider the following function: $f(x) = x^2 + x + 1$
- We speak in terms of a name the argument and the result:
    - $f$ is a function which, when applied to any argument $x$ returns $x^2 + x + 1$
    - $g(x) = x^2 + x + 1$  $\quad \widehat{=} \quad$  $g(y) = y^2 + y + 1$
- can we describe and define functions without giving them names?
- $\lambda$-calculus allows us to do so
- $\lambda$-calculus is a notation for functions (short but cryptic) which takes its origin in mathematical logic
- Expressions in $\lambda$-calculus are written in the strict prefix form, that is, there are no infix and postfix operations.
- Furthermore functions and their arguments are simply written next to each other
    - examples: 
        - $sin(x) \longrightarrow sin\ x$
        - $x+4 \longrightarrow + x\ 4$
        - $x^2 \longrightarrow *\ x\ x$ 
- Brackets are used only to enforce a special grouping:
    - example: 
        - $sin(x) + 4 \longrightarrow (sin\ x\ ) 4\ $
- If an expression contains a variable $(x)$, then one can form the function which obtains by considering the relationship between concrete values of $x$ and the resulting value of expression
- In mathematics, function formation is sometimes written as an equation, $f(x)=3x$, or sometimes as a mapping $f:x \rightarrow 3x$
- In the $\lambda$-calculus a special notation is available which dispenses the need to give a name to the function and which easily scales up to more complicated function definitions.
- In the example above, we will write $3x$ as $*\ 3\ x\ $ and turn it into a function by preceding $\lambda x .  \rightarrow \lambda x. *\ 3\ x\ $
- The letter $\lambda$ has a role similar to keyword `function` in some programming languages
- The variable which comes after $\lambda$ is not part of an expression, but a formal parameter.
- The $.$ tells that here starts the function body.
    - We have $\lambda$ \underline{variable} . \underline{function body}


- Let us consider a function $x^2 + y$
- This can be thought of as a function on $x$ (y is fixed in this case), or it can be a function on $y$(x is fixed), and it can be a function on $x$ and $y$
- To make a distinction between these cases, $\lambda$-calculus provides the so called abstraction.
- To see how it works, let us consider a function $x \mapsto x^2 + y$
- To make a clear distinction between the \underline{bound} variable $x$ and the \underline{unbounded} variable $y$ we introduce an explicit variable binder, and we write:
    - $\lambda x . + (*\ x\ x)y$ // x $\rightarrow$ bounded variable
    - $\lambda z . + (*\ z\ z)y$


___


### The pure $\lambda$-calculus
- The funciton which has been $\lambda$ notation can itself be used in an expression.
- For example, the application of the function $3x$ to a value $4$ is written as $(\lambda x. *\ 3\ x) 4$
- As we already mentioned the representation by means of $\lambda$ bindings offers a general way to write functions.
- In case a function takes several arguments we need to use several bound variables.
    - example: $\lambda x.\lambda y. +(*\ x\ x)y$
    - $(\lambda x.\lambda y. +(*\ x\ x)y)3$  $\rightarrow \lambda y. _(*\ 3\ 3) y$
- For applying a function to its argument we use juxtaposition:
    - if $F$ is a function expression and $A$ is an argument expression, then $(F\ A)$ denotes the application of $F$ to $A$.
        - example: $f(x)=x^2+1 \quad\quad A = sin y$
        - $f(A) = (sin y)^2 + 1$ 
- Although it is not strictly necessary, it will be convenient to introduce an abbreviation for $\lambda$ terms.
- If we abbreviate our function term to $F$.
    - $F =^{def} \lambda x. *\ 3\ x$
- now we write $F\ 4$, instead of (3. formel)
- Suppose the body of a function consists of another function:
    - $N =^{def} \lambda y.*(\lambda x.*\ y\ x)$
- If we apply this function to the value $3$ then we get back $\lambda x. *\ 3\ y$
- In other words $N$ is a function which when applied to a number returns another function.
- If we want to underline that $N$ is a function of two arguments then we should leave the brackets out
- That means we have $\lambda x. \lambda y. *\ y\ x$ or, as typically used we can omit the second $\lambda$:
    - $\lambda y\ x. *\ y\ x$
- Function formation and function application are all there is in pure $\lambda$-calculus.
- They can be mixed freely and used as often as desired or needed
- Which is another way of saying that $\lambda$ terms are constructed according to the grammar
    - $M::=c\ |\ x\ |\ M\ N\ |\ \lambda x.\ M$
    - where $c$ represents any constant we might use in a $\lambda$-term, such as numbers or arithmetic operations (a term without a constant is called pure $\lambda x. x$), the letter $x$ represents any of inifinitely manay variables $M\ N$ is an application of one term $M$ to another term $N$
    - $\lambda x.\ M$ is an abstraction


___


### The evaluation of $\lambda$-expressions
- We have seen how the $\lambda$-notations can be used to represent functional expressions and we are going to define conversion rules of $\lambda$-calculus which will describe how to evaluate an expression.
- or how to transform an expression from its initial state into final state
- The simplest type of $\lambda$-expression is a constant.
- Constants are self-defining, meaning that they cannot be transformed into any simpler expression
- The expression $5$ produces the number $5$
- The following table provides predefined constants:

| Constant          | Meaning                           |
|-------------------|-----------------------------------|
| $0,1,-1,-2,2,...$ | The set of integers               |
|  `TRUE, FALSE`    | Boolean constants                 |
| $+, -, *$         | mathematic operations             |
| $=, \neq, < , >$  | boolean functions                 |
| `SUCC, PRED`      | successor and predecessor one int |
| `EQ0`             | returns `TRUE` if $int = 0$       |
| `COND`            | conditional functions             |
| `CONS`            | list constructor                  |
| `NIL`             | empty list                        |
| `HD`              | function returning head of a list |
| `TL`              | function returning tail of a list |
| `IE` = NULL       | if list is `NIL` returns `TRUE`   |
| `TUPLE`           | builds a n-Tuple of expressions   |
| `INDEX`           | tuple indexing function           |


___


#### Lecture 3 (26.10.2015)

- An application of a constant function can be tranformed by using the builtin rules if a sufficient amount of arguments is provided for that constant.
- These builtin rules are often referred to as $\delta$-rules.
    - Example: $+\ 1\ 3$ // read as  "$+\ 1\ 3$ reduces to $4$"
    - to evaluate this expression we need to apply a $\delta$-rule for arithmetic function $+$ as follows:
    - $+\ 1\ 3 \rightarrow_{\delta} 4$
    - This process of simplification is called \underline{reduction}
- In general the arguments of such a function may not be in the required form for the reduction to take place immediately
    - Example:
    - $*\ (+\ 1\ 2)(-4\ 1)$
    - to reduce this expression we must first reduce the argument expression of the multiplication function
    - It can be done as follows: $*\ (+\ 1\ 2)(-4\ 1) \rightarrow_{\delta} -x(+\ 1\ 2)B \rightarrow_{\delta} *\ 3\ 3 \rightarrow_{\delta} 9$
    - The most interesting reduction rule describes how to apply lambda abstraction.
- Let us consider the following application:
    - $(\lambda x. *\ x\ x)2$
    - In the LC the evaluation of such expressions consists in the textual replacement of a formal parameter in the body of a function by the actual parameter supplied.
    - In the above example we get: $(\lambda x. *\ x\ x)2 \rightarrow_{\beta} *\ 2\ 2\ \rightarrow_{\delta} 4$
    - \underline{Def:} The process of copying the body of an abstraction, replacing all occurence of the bound variable by the argument expression is known as $\beta$-reduction
    - The term 'reduction' is used in a sense of simplification since we notionally cancel the $\lambda$, the bound variable and the argument expression and return just a modified form of a body.
- The reduction of an abstraction applied to an argument may yield another abstraction, in that case the process can maybe repeated
    - Example: In the folloring Expression :
        - $((\lambda x. \lambda y. + x\ y )7)8$
    - we start by substituting the $7$ for $x$ in the body of outermost abstraction $i.e\ \lambda y. +\ x\ y$ yields:
        - $(\lambda y. +\ z\ y)8$
    - and end up with another abstraction to an argument expression.
    - We can reduce
    - The expression being reduced is called the \underline{redex}(short for reducable expression), and for the time being we will state that the process of reducing a $\lambda$-expression consists of repeatedly reducing the redexes of the expression until no more redexes exist.
- We will sometimes qualify the word "redex" according to the type of the rule which can be used to simplify it $\delta$-redex -- $\delta$-rule, $\beta$-redex -- $\beta$-reduction
- Let us consider the following expression:
    - $(\lambda x.\ x)(+\ 2\ x)$
- This is clear thta the $x$ within the inner abstraction $(\lambda x.x)$ refers to a different bound variable, than in its argument expression $(+\ 1\ x)$.
- If we apply this expression to an argument, (lets say $1$) then it would be wrong to perform $\beta$-reduction als follows:
    - $(\lambda x.(\lambda x. x)(+\ 1\ x))1 \rightarrow (\lambda x. 1)(+\ 1\ 1) \rightarrow 1$
- When we apply a $\beta$-reducion, we must be careful not to substitute inside an abstraction if the bound variable of that abstraction has the same name as the variable being substituted.
- If it does have the same name, then we must leave this (inner) abstraction unchanged . It is possible to avoid such type of name clash by renaming the variables concerned - in this case one of $x$'s - so as to make each name unique.
- Such renaming is called $\alpha$-conversion
- And expressions which are $\alpha$-convertable, it means equal up to variable renaming, are called alphabetically equivalent.
- Let us consider the following example of $\beta$-reduction:
    - $(\lambda f. \lambda x. f\ 4\ x)(\lambda y. \lambda x. +\ x\ y) 3$
- Step 1: Reduce the (only) redex by substituting the argument $(\lambda .(\lambda x\ x. x\ y))$ for $f$ to the body of the abstraction $(\lambda f.\ \lambda x.\ f\ y\ x) \rightarrow (\lambda x(\lambda y.\ \lambda x.\ x\ x\ y)4x)3$
- Step 2: (Arbitory) chose redex which which results in $3$ being substituted for $x$ to the body expression $(\lambda y.\\lambda x.\ +\ x\ y)4x$, but do not substitute beyond the $\lambda x)$written the inner abstraction $\rightarrow(\lambda y.\ \lambda x.\ +\ x\ y)4\ 3$ 
- Step 3: Reduce the (only) redex $(\lambda y.\ \lambda x.\ +\ x\ y)4 \rightarrow (\lambda x.\ x\ x\ 4) 3$
- Step 4: Reduce the (only) redex:
    - $\rightarrow +\ 3\ 4$
- Step 5: Apply the DELTA-rule for $"+"$
    - $\rightarrow 7$
- Notice that the first reduction applied substituting f with the function $(\lambda x. \lambda y.\ +\ x\ y)$
- The abstraction containing $f$ corresponds to a higher order function in the equivalent source program.
- At Step 2 there was a choice of two redexes to reduce and we arbitrarily chose chose to reduce the outer one first.
- However we could have chosen to do a $\beta$-reduction on the inner redex first as follows  $(\lambda x (\lambda y.\ \lambda x.\ +\ x\ y)4x) 3 \rightarrow (\lambda x.(\lambda x.\ +\ x\ 4)x)3 \rightarrow (\lambda x.\ +\ x\ 4)3 \rightarrow +\ 3\ 4 \rightarrow 7$


### Reduction order and normal forms
- \underline{Def:} A $\lambda$-expression is said to be in the normal form if it cannot be further reduced.
- In other words, it is in normal form if it contains no redexes.
- Normal form corresponds to the idea of the "end" of computation in the programming sense.
- This immediately suggests a naive evaluation scheme \newline
  `while there are more redexes; do` \newline
  `reduce one of the redexes` \newline
  `end;`

- The expression now is in normal form
- The problem with it is that there may be more than one redex within an expression
- This leads us to the question:
    - Which redex to reduce next?
    - Let us consider the following expression: 
        - $(\lambda x.\ \lambda y.\ y)((\lambda z.\ z\ z)(\lambda z.\ z\ z))$
    - Here wre have to redexes:
        - $(\lambda x.) OANA FRAGEN$
    - and
        - $(\lambda z.\ z\ z)(\lambda z.\ z\ z)$
    - If we pick the second of these two to reduce first we get the following reduction sequence:
        - $(\lambda z.\ z\ z)(\lambda z.\ z\ z) \rightarrow (\lambda z.\ z\ z)(\lambda z.\ z\ z) \rightarrow$ ... which is not terminated
    - Which is not terminating
    - In the other hand if we chose the first redex we get
        - $((\lambda x.\ \lambda y\ y)(\lambda z.\ z\ z)(\lambda z.\ z\ z)) \rightarrow \lambda y.\ y$ ... which terminates in first step
    - Before a discussion of reduciton order let us introduce some definitions
    - \underline{Def:}
        - The leftmost redex is that redex whose $\lambda$ (or primitive function identifier in the case of DELTA-redex) is textually to the left of all other redexes within the expression Yeah, (Similary for the rightmost redex) AhaAha
    - \underline{Def:}
        - An outermost redex is defined to be a redex which is not contained within any other redex.
    - \underline{Def:}
        - An innermost redex is defined to be a redex which containes no other redex.
        - these are two of the most important reduction strategies:
        - \underline{Normal order:}
            - Under this strategy the leftmost outermost redex is always reduced first. Normal order of reduction is normalizing strategy in the sense that a term as a normal form then this order of reduction will find it.

### Applicative Order:
- Under this strategy the leftmost innermost redex is always reduced first.
- It turns out that applicative order of reduction is not normalization

#### Lecture (02.11.2015)
- Let us look again at our example
    - BLATT 1
- The leftmost innermost redex is:
    - BLATT 2
- and the leftmost outermost redex is:
    - BLATT 3
- Applicative order of reduction will therefor evaluate the redex BLATT 4 first and will fail to terminate, whereas the normal order reduction will evaluate the outermost redex first, and will terminate in one step.
- The function of such $\lambda x.\ \lambda y.\ y$ is a classical example of a function which discards its argument.
- Normal order reduction delays the evaluation of any redex within the argument expression until there is no alternative redex available, just in case such reduction is proof redundant
- The leftmost outermost selection policy therefor chooses to substite an expression for $x$ in $\lambda y.\ y$ before attempting any reduction within the argument expression.
- It thus leads to the normal form $\lambda y.\ y$ in one step.
- Applicative order of reduction in this case at first evaluates the argument expression and leads in the example to a non-termination.
- These two strategies lead us to the two concepts of evaluation in modern programming languages

### Call-by-name:
- This is a restriction of normal order where no reductions are allowed inside abstractions.
- Let us consider the term:
    - BLATT 6
- for simplicity we will write BLATT 7
- This term has three redexes:
    - BLATT 8 YALLA OANA!!!!!!!!!!!!!!!!!
- With call by name strategy we get 
    - BLATT 9 
    $$$
        \lambda formula shit
    $$$
- Haskell is even a more efficient variant known as \emph{call-by-need} where instead of re-evaluating an argument each time is used, all occurrences of the argument are overwritten with its value the first time its evaluated.
- I FUCKING HATE THIS LECTURE
- MONKEY WORK DRIVES ME CRAZY
- blah blah blah 
- This requires that we have a runtime representation of terms that allows sharing of subexpressions leading to a terms becoming graph rather than trees.


### Call-by-value 
- Most languages use this strategy, where again no reduction are allowed inside abstractions and a redex is only reduced when its argument part has already been reduced to a value.
- BLATT 10 
- The call-by-value strategy represents eager evaluation, and call-by-need(name) represents Lazy evaluation.


- As we have seen it may be that the LAMBDA-term offers many opportunities for reduction at the same time.
- In order for the whole calculus to make sense it is necessary that the ruslut of a computation is independent form the order of reduction.
- We would like to express this property for all terms, not just for those which have a normal form. 
- This is possible by the following theorem:
    - __Theorem (Church-Rosser)__
        - If a term $M$ can be reduced (in several steps) to terms $N$ and $P$, then there exists a term $Q$ to which both $N$ and $P$ can be reduced (in several steps).
- This theorem 'provides' the so called diamond property whis is illustrated by the following diagram
    - FIGURE 1
- we use the symbol $\rightarrow *$ to denote an arbitrary number BLATT 11 of reductions (i.e. $\rightarrow *$ is the reflexive transitive of $\rightarrow$. The 'reflexive' part means that $E$ can be reduced to itself by doing nothing, $n=o$). Formally therefore, the diamond property states that: BLATT 12
- We say that the reduction relation $\rightarrow$ is emph{Church Rosser} if $\rightarrow *$ satisfies the diamond property, and it can be proofed that BETA-reduction is \emph{Church-Rosser}.


### Consequence of \emph{Church-Rosser}
- If an expression $E$ can be reduced in two different ways to normal forms, then this normal forms are the same (up to alphabetical equivalence)

#### Corollo-something y
- Every LAMBDA-term has at most one normal form.
#### Proof
- For the sake of contradiction, assume that there are normal forms $N$ and $P$ to which a certain term is reduced:
    - FIGURE 2
- By the Church-Rosser theorem there is a term $Q$ to which both $P$ and $N$ can be reduced. 
- However $N$ and $P$ are assumed to be in normal form, so no further reduction is possible.
- Therefore the only possibility is thath $N=P=Q$. \box

### BETA reduction and the name clash problem:
- Let us consider the following expression:
    - BLATT 13
- We say that $x$ is bound in the whole expression, since there is an occurence of a $\lambda x$ within it. Equivalently we say that there is a binding occurence of $x$ within the expression.
- Now let us have a look at the body of the outermost abstraction:
    - BLATT 14 
- ALthough $x$ appears in this expression there is no binding occurence of $x$ (i.e. there is no $\lambda x$ outside it)
- We therefor say that the variable $x$ is three in the expression.
- The variable $y$ is still bound by $\lambda y$.
- If we now consider the body of the innermost abstraction ($x\ y\ y$) then both $x$ and $y$ are free.
- We will sometimes refer to the set of expression free variables of an expression $E$ by $FV(E)$
    - For example: $FV(\lambda x.\lambda y. x\ y\ y) = \{\}$
    - $FV(\lambda y. x\ y\ y) = \{x\}$
    - $FV(x\ y\ y) = \{x,y\}$
- $FV$ an be defined more formally as follows: $FV(k) = \diameter $, $k$ is a constant
- $FV(x) = \{x\}$ $x$ is a variable
- $FV(E_1,E_2) = FV(E_1) \cup FV(E_2)$
- $FV(\lambda x. E) = FV(E) - x$
- Where $FV$ denotes the set $S$ with any occurence of $x$ removed. 
    - _DEF:_ A LAMBDA-expression $E_1$ which contains no free variables (i.e. $FV(E)=\diameter$) is said to be closed
- Using this notion of bound and free variables we can now formalize the definition of BETA-reduction:
    - _DEF:_ to BETA-reduce an expression $(\lambda x. E)\ A$ we return a modified form of $E$ in which all free occurences of $x$ are replaced by $A$
- Unfortunately this leads to a potential problem with BETA-reduction which can be illustrated by the following example:

    - $\lambda x(\lambda y.\lambda x.\ +\ y\ x)$ BLATT 17
- This expression contains a single BETA-redex
- If we attempt to reduce this redex we will get $(\lambda x.\ +\ x\ x)$ which is quiet clearly wrong.
- The problem is, that in this example the argument expression contains a free variable which has the same name as one of the bound variables within the abstraction body $(\lambda y. \lambda x.\ +\ x\ y)$ where $x$ is bound and $y$ is free
