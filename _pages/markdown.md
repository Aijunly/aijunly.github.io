---
permalink: /markdown/
title: "The Julia Programming Language"
author_profile: true
redirect_from: 
  - /md/
  - /markdown.html  
---

## What is the Julia?
**[Julia](https://julialang.org/)** is a flexible dynamic language, appropriate for **scientific and numerical computing**.   
<br/><img src='/images/juliagood.png'>



## Numeric Types and Strings in Julia  

A type tree for all subtypes of Number in Base is shown below. 

<img src='/images/numericaltypes.png'>

A **Char** value represents a single character. **Strings** are finite sequences of characters. 


## Optimization Solvers


| Solver                                                 | Year | Description                                                  | 
| ------------------------------------------------------ | ---- | :----------------------------------------------------------- | 
| [BARON](https://minlp.com/)                            | 2001 | The world's fastest and most powerful MINLP solver. | 
| [COPT](https://www.cardopt.com/copt)                   | 2019 | Optimization solver for (MI) LP, SDP, SOCP, convex QP, convex QCP and exponential cone programming. | 
| [CPLEX](https://www.ibm.com/analytics/cplex-optimizer) | 1988 | High-performance optimization solver for linear, mixed-integer and quadratic programming. | 
| [GUROBI](https://www.gurobi.com/)                      | 2008 | The best optimization solver in the world, along with outstanding support and straightforward pricing. | 
| [HiGHS](https://highs.dev/)                            | 2019 | Freely high performance software for linear optimization.   | 
| [IPOPT](https://github.com/coin-or/Ipopt)              | 2002 | Ipopt (Interior Point OPTimizer) is a software package for large-scale nonlinear optimization. | 
| [LindoAPI](https://www.lindo.com)                      | 2001 | Powerful solvers for (MI) Stochastic, Linear, Nonlinear, Quadratic, Second Order Cone programming. | 
| [MOSEK](https://www.mosek.com/)                        | 1999 | Powerful software of solving large-scale optimization problems of (MI) Linear, Quadratic and Conic.| 
| [SCIP](https://scipopt.org/)                           | 2005 | Fast and flexible solver for MIP, MINLP, and CP problems. | 


One want to study and research Mathematical Programming and its applications, and then I strongly recommend you the following Open-Source Solvers of [HiGHS](https://highs.dev/) for LP, QP and MILP, [Ipopt](https://github.com/coin-or/Ipopt)  for NLP and [SCIP](https://github.com/scipopt/scip)  for MIQP and MINLP. If you want to use others solvers in Julia, please click [Support Solvers](https://jump.dev/JuMP.jl/stable/installation/#Supported-solvers).



### [HiGHS](https://highs.dev/)                          
HiGHS is high performance serial and parallel software for solving large-scale sparse linear programming (LP), mixed-integer programming (MIP) and quadratic programming (QP) models with [Online Document](https://ergo-code.github.io/HiGHS/dev/).

$$
 	\begin{split}
		&\min_{ x \in \mathbb{R}^{n}}~ \frac{1}{2}x^{\top} Q x + c^{\top} x\\
		&\quad \text{s.t.}  
		\begin{cases}
			L \leq Ax \leq U, \\
			l \leq x \leq u.
		\end{cases}
	\end{split}
$$


### [Ipopt](https://github.com/coin-or/Ipopt) 
[Ipopt](https://github.com/coin-or/Ipopt) is a software package for large-scale nonlinear optimization with [Online Document](https://coin-or.github.io/Ipopt/index.html).. It is designed to find (local) solutions of mathematical optimization problems of the form

$$
 	\begin{split}
		&\min_{ x \in \mathbb{R}^{n}}~f(x)\\
		&\quad \text{s.t.}  
		\begin{cases}
			g_L \leq g(x) \leq g_U, \\
			x_L \leq x \leq x_U.        
		\end{cases}    
	\end{split}
$$

where The functions \\( f(x) \\) and \\( g(x) \\) can be nonlinear and nonconvex, but should be **twice continuously differentiable**. 


### [SCIP](https://github.com/scipopt/scip)  
[SCIP](https://github.com/scipopt/scip) is currently one of the fastest academically solvers for mixed integer programming (MIP) and mixed integer nonlinear programming (MINLP) with [Online Document](https://scipopt.org/doc/html/index.php). It is also a framework for constraint integer programming and branch-cut-and-price. 


## Primal-Dual Simplex Method    
> From the \\( k \\)-th iteration of Simplex Table to the next \\( k+1 \\)-th iteration of Simplex Table for solving the Standard form of Linear Programming
> 
> $$
 	\begin{split}
		&\max_{ x \in \mathbb{R}^{n}}~  c^{\top} x\\
		&\quad \text{s.t.}  
		\begin{cases}
		     Ax = b, \\
		     x \geq 0,
		\end{cases}
	\end{split} 
$$
> 
> where \\( A \in \mathbb{R}^{m \times n} \\) , \\( b \in \mathbb{R}^{m} \\) and \\( c \in \mathbb{R}^{n} \\) is **reduced cost**.


<img src='/images/pdsimplexK.png'>      
In the above Table, \\( \sigma^{k} \\) and \\( \sigma^{k+1} \\) is the \\( k \\)-th and \\( k + 1 \\)-th **reduced cost**, respectively.
<img src='/images/oro2025/simplexkk.png'>



### First, we define some struct 


```julia
### IMPORT PACKAGES
## LINEAR ALGEBRA
using LinearAlgebra                    
## DATA FRAMES
using DataFrames

                       
struct SimplexAbc{T <: Real}         
A :: Matrix{T};                    
b :: Vector{T};
c :: Vector{T};  
end

function GetSimplexTable(Abc :: SimplexAbc{T}) where T <: Real
	# Dimension of A
	m,n = size(Abc.A);
	# Augmented matrix                 
	augAB = [Abc.A Abc.b];
	# Translate A into DataFrame
	matdf = DataFrame(augAB,[Symbol.(:X,1:n);Symbol.(:RHS)]);    
	# Add check vector or coefficient below the last row of matdf
	push!(matdf,[Abc.c' 0]);
	return matdf;
end

### EXAMPLES
A = [3 5 1 0 0;6 2 0 1 0;1 2 0 0 1]
b = [15;12;6]
c = [2;3;0;0;0]


st = SimplexAbc(A,b,c);

GetSimplexTable(st)
4×6 DataFrame
 Row │ X1     X2     X3     X4     X5     RHS
     │ Int64  Int64  Int64  Int64  Int64  Int64
─────┼──────────────────────────────────────────
   1 │     3      5      1      0      0     15
   2 │     6      2      0      1      0     12
   3 │     1      2      0      0      1      6
   4 │     2      3      0      0      0      0

```



 
## My Example     

```julia
using JuMP 

using HiGHS
wjModel = Model(HiGHS.Optimizer)  
 
@variable(wjModel,x1 >= 0)
@variable(wjModel,x2 >= 0) 

@constraint(wjModel,3*x1 + 5*x2 <= 15) 
@constraint(wjModel,3*x1 +   x2 <= 6)      

@objective(wjModel,Max,2*x1 + 3*x2)

print(wjModel)

## Solving...
optimize!(wjModel)

@show JuMP.value(x1)
@show JuMP.value(x2)
@show JuMP.objective_value(wjModel)  
```

## Continous...


