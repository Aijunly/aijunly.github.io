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

A **Char** value represents a single character: it is just a 32-bit primitive type with a special literal representation and appropriate arithmetic behaviors, and which can be converted to a numeric value representing a Unicode code point. **Strings** are finite sequences of characters. 


## Optimization Solvers


| Solver                                                 | Year | Description                                                  | 
| ------------------------------------------------------ | ---- | :----------------------------------------------------------- | 
| [BARON](https://minlp.com/)                            | 2001 | The world's fastest and most powerful MINLP solver. | 
| [COPT](https://www.cardopt.com/copt)                   | 2019 | Optimization solver for (MI) LP, SDP, SOCP, convex QP, convex QCP and exponential cone programming. | 
| [CPLEX](https://www.ibm.com/analytics/cplex-optimizer) | 1988 | High-performance optimization solver for linear, mixed-integer and quadratic programming. | 
| [GUROBI](https://www.gurobi.com/)                      | 2008 | The best optimization solver in the world, along with outstanding support and straightforward pricing. | 
| [HiGHS](https://highs.dev/)                            | 2019 | Freely high performance software for linear optimization.   | 
| [IPOPT](https://github.com/coin-or/Ipopt)              | 2002 | Ipopt (Interior Point OPTimizer) is a software package for large-scale nonlinear optimization. | 
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


## Primal Simplex Method

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

## Resources                    
 * [Liquid syntax guide](https://shopify.github.io/liquid/tags/control-flow/)     
 * [MathJax Documentation](https://docs.mathjax.org/en/latest/)  

## MathJax 

Support for MathJax Version 3.0 is included in the template:

$$
\displaylines{
\nabla \cdot E= \frac{\rho}{\epsilon_0} \\\
\nabla \cdot B=0 \\\
\nabla \times E= -\partial_tB \\\
\nabla \times B  = \mu_0 \left(J + \varepsilon_0 \partial_t E \right)
}
$$

The default delimiters of `$$...$$` and `\\[...\\]` are supported for displayed mathematics, while `\\(...\\)` should be used for in-line mathematics (ex., \\(a^2 + b^2 = c^2\\))

**Note** that since Academic Pages uses Markdown which cases some interference with MathJax and LaTeX for escaping characters and new lines, although [some workarounds exist](https://math.codidact.com/posts/278763/278772#answer-278772).

## Markdown guide

Academic Pages uses [kramdown](https://kramdown.gettalong.org/index.html) for Markdown rendering, which has some differences from other Markdown implementations such as GitHub's. In addition to this guide, please see the [kramdown Syntax page](https://kramdown.gettalong.org/syntax.html) for full documentation.  

### Header three

#### Header four

##### Header five

###### Header six

## Blockquotes

Single line blockquote:

> Quotes are cool.

## Tables

### Table 1

| Entry            | Item   |                                                              |
| --------         | ------ | ------------------------------------------------------------ |
| [John Doe](#)    | 2016   | Description of the item in the list                          |
| [Jane Doe](#)    | 2019   | Description of the item in the list                          |
| [Doe Doe](#)     | 2022   | Description of the item in the list                          |

### Table 2

| Header1 | Header2 | Header3 |
|:--------|:-------:|--------:|
| cell1   | cell2   | cell3   |
| cell4   | ce
ll5   | cell6   |
|-----------------------------|
| cell1   | cell2   | cell3   |
| cell4   | cell5   | cell6   |
|=============================|
| Foot1   | Foot2   | Foot3   |

## Definition Lists

Definition List Title
:   Definition list division.

Startup
:   A startup company or startup is a company or temporary organization designed to search for a repeatable and scalable business model.

#dowork
:   Coined by Rob Dyrdek and his personal body guard Christopher "Big Black" Boykins, "Do Work" works as a self motivator, to motivating your friends.

Do It Live
:   I'll let Bill O'Reilly [explain](https://www.youtube.com/watch?v=O_HyZ5aW76c "We'll Do It Live") this one.

## Unordered Lists (Nested)

  * List item one 
      * List item one 
          * List item one
          * List item two
          * List item three
          * List item four
      * List item two
      * List item three
      * List item four
  * List item two
  * List item three
  * List item four

## Ordered List (Nested)

  1. List item one 
      1. List item one 
          1. List item one
          2. List item two
          3. List item three
          4. List item four
      2. List item two
      3. List item three
      4. List item four
  2. List item two
  3. List item three
  4. List item four

## Buttons

Make any link standout more when applying the `.btn` class.

## Notices

Basic notices or call-outs are supported using the following syntax:

```markdown
**Watch out!** You can also add notices by appending `{: .notice}` to the line following paragraph.
{: .notice}
```

which wil render as:

**Watch out!** You can also add notices by appending `{: .notice}` to the line following paragraph.
{: .notice}

### Footnotes

Footnotes can be useful for clarifying points in the text, or citing information.[^1] Markdown support numeric footnotes, as well as text as long as the values are unique.[^note]

```markdown
This is the regular text.[^1] This is more regular text.[^note]

[^1]: This is the footnote itself.
[^note]: This is another footnote.
```

[^1]: Such as this footnote.
[^note]: When using text for footnotes markers, no spaces are permitted in the name.

## HTML Tags

### Address Tag

<address>
  1 Infinite Loop<br /> Cupertino, CA 95014<br /> United States
</address>

### Anchor Tag (aka. Link)

This is an example of a [link](http://github.com "Github").

### Abbreviation Tag

The abbreviation CSS stands for "Cascading Style Sheets".

*[CSS]: Cascading Style Sheets

### Cite Tag

"Code is poetry." ---<cite>Automattic</cite>

### Code Tag

You will learn later on in these tests that `word-wrap: break-word;` will be your best friend.

You can also write larger blocks of code with syntax highlighting supported for some languages, such as Python:

```python
print('Hello World!')
```

or R:

```R
print("Hello World!", quote = FALSE)
```

### Details Tag (collapsible sections)

The HTML `<details>` tag works well with Markdown and allows you to include collapsible sections, see [W3Schools](https://www.w3schools.com/tags/tag_details.asp) for more information on how to use the tag.

<details>
  <summary>Collapsed by default</summary>
  This section was collapsed by default!
</details>

The source code:

```HTML
<details>
  <summary>Collapsed by default</summary>
  This section was collapsed by default!
</details>
```

Or, you can leave a section open by default by including the `open` attribute in the tag:

<details open>
  <summary>Open by default</summary>
  This section is open by default thanks to open in the &lt;details open&gt; tag!
</details>


### Emphasize Tag

The emphasize tag should _italicize_ text.

### Insert Tag

This tag should denote <ins>inserted</ins> text.

### Keyboard Tag

This scarcely known tag emulates <kbd>keyboard text</kbd>, which is usually styled like the `<code>` tag.

### Preformatted Tag

This tag styles large blocks of code.

<pre>
.post-title {
  margin: 0 0 5px;
  font-weight: bold;
  font-size: 38px;
  line-height: 1.2;
  and here's a line of some really, really, really, really long text, just to see how the PRE tag handles it and to find out how it overflows;
}
</pre>

### Quote Tag

<q>Developers, developers, developers&#8230;</q> &#8211;Steve Ballmer

### Strike Tag

This tag will let you <strike>strikeout text</strike>.

### Strong Tag

This tag shows **bold text**.

### Subscript Tag

Getting our science styling on with H<sub>2</sub>O, which should push the "2" down.

### Superscript Tag

Still sticking with science and Isaac Newton's E = MC<sup>2</sup>, which should lift the 2 up.

### Variable Tag

This allows you to denote <var>variables</var>.

***
**Footnotes**

The footnotes in the page will be returned following this line, return to the section on <a href="#footnotes">Markdown Footnotes</a>.

