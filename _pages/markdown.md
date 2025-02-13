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

### [BARON](https://minlp.com/)    
 BARON was the first branch-and-bound solver for global optimization of nonlinear programming (NLP) and mixed-integer nonlinear programming (MINLP) problems. <img src='/images/baron.png'>
 
### [HiGHS](https://highs.dev/) 
HiGHS is high performance serial and parallel software for solving large-scale sparse linear programming (LP), mixed-integer programming (MIP) and quadratic programming (QP) models.

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

### [SCIP](https://scipopt.org/)  
SCIP is currently one of the fastest non-commercial solvers for mixed integer programming (MIP) and mixed integer nonlinear programming (MINLP). It is also a framework for constraint integer programming and branch-cut-and-price. 


## Primal-Dual Simplex Method
> From the \\( k \\)-th iteration of Simplex Table to the next \\( k+1 \\)-th iteration of Simplex Table for solving the Standard Linear Programming
> 
> $$
 	\begin{split}
		&\min_{ x \in \mathbb{R}^{n}}~  c^{\top} x\\
		&\quad \text{s.t.}  
		\begin{cases}
		     Ax = b, \\
		     x \geq 0,
		\end{cases}
	\end{split}
$$
> where \\( \sigma^{k} \\) is the \\( k \\)-th Reduced Cost.

<img src='/images/pdsimplexK.png'>

 
```julia        
struct SimplexAbc{T <: Real}  
A :: Matrix{T};
b :: Vector{T};
c :: Vector{T};
end

function GetSimplexTable(Abc <: SimplexAbc{T <: Real})
	# Dimension of A
	m,n = size(Abc.A);
	# Augmented matrix                 
	augAB = [Abc.A Abc.b];
	# Translate A into DataFrame
	matdf = DataFrame(augAB,[Symbol.(:X,1:n);Symbol.(:B)]);    
	# Add check vector or coefficient below the last row of matdf
	push!(matdf,[Abc.c' 0]);
	return matdf;
end
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

