---
title: "Operations Research and Optimization"
collection: teaching
type: "Undergraduate"
permalink: /teaching/000-ORO-2025-Spring  
venue: "JUST, ChangShan Campus"
date: 2025-02-17
location: "Zhenjiang, China"
---

From basic to advance with your small steps    

======      

  



Linear Programming and its Dual Linear Programming
======
Primal Standard Linear programming:      

$$
\begin{aligned}
	\max \quad & z = c^\top x\\
	\rm{s.t.} &~
	\begin{cases} 
		A x =  b  \\
		 ~x \geq  0
	\end{cases} 
\end{aligned}
$$

Its dual linear programming

$$
    \begin{aligned}
        \min_{y \in \mathbb{R}^{m} }~& w = b^\top \lambda\\
	    \rm{s.t.} &~ A^{\top} \lambda \geq  c.
    \end{aligned}
$$

Simplex Method in Table \ref{InitialSimplexTableKP1}.

\begin{table}[!htb]  
    \centering
    \begin{tabular}{|c||c|c|c|c|c|c|c|c|c|c|c|c||c|}
    \hline    
        $\sigma^{k}$ & $0$ & $0$ & $\cdots$ & $0$ & $\cdots$ & $0$ & $\sigma_{i_{m+1}}^{k}$ & $\sigma_{ i_{m+2} }^{k}$ & $\cdots$ & $\sigma_{ i_{q} }^{k}$ & $ \cdots $ & $\sigma_{ i_{n} }^{k}$ & $\mathring{-z_{k} }$ \\ \hline \hline
          $c_{\mathcal{B}_{k+1}}$ & $x_{i_{1}}$ & $x_{i_{2}}$ & $\cdots$ & $x_{i_{p}}$ & $\cdots$ & $x_{i_{m}}$ & $x_{i_{m+1}}$ & $x_{i_{m+2}}$ & $\cdots$ & $x_{i_{q}}$ & $\cdots$ & $x_{i_{n}}$ & $b$ \\ \hline 
        $0$ & $1$ & $0$ & $\cdots$ & $-\frac{y_{1,q}^{k}}{y_{p,q}^{k}}$ & $\cdots$ & $0$ & $y_{1,m+1}^{k+1}$ & $y_{1,m+2}^{k+1}$ & $\cdots$ & $0$ & $\cdots$ & $y_{1,n}^{k+1}$ & $d_{1}^{k+1}$ \\  
        $0$ & $0$ & $1$ & $\cdots$ & $-\frac{y_{2,q}^{k}}{y_{p,q}^{k}}$ & $\cdots$ & $0$ & $y_{2,m+1}^{k+1}$ & $y_{2,m+2}^{k+1}$ & $\cdots$ & $0$ & $\cdots$ & $y_{2,n}^{k+1}$ & $d_{2}^{k+1}$ \\  
        $\vdots$ & $\vdots$ & $\vdots$ & $\ddots$ & $\vdots$ & $\vdots$ & $\vdots$ & $\vdots$ & $\vdots$ & $\ddots$ & $\vdots$ & $\vdots$ & $\vdots$ & $\vdots$ \\  
        $\sigma_{ i_{q} }^{k}$ & $0$ & $0$ & $\cdots$ & $\frac{1}{y_{p,q}^{k}}$ & $\cdots$ & $0$ & $\frac{y_{p,m+1}^{k}}{y_{p,q}^{k}}$ & $\frac{y_{p,m+2}^{k}}{y_{p,q}^{k}}$ & $\cdots$ & $\boxed{1}$ & $\cdots$ & $\frac{y_{p,n}^{k}}{y_{p,q}^{k}}$ & $\frac{d_{p}^{k}}{y_{p,q}^{k}}$ \\  
        $\vdots$ & $\vdots$ & $\vdots$ & $\vdots$ & $\vdots$ & $\ddots$ & $\vdots$ & $\vdots$ & $\vdots$ & $\vdots$ & $\vdots$ & $\ddots$ & $\vdots$ & $\vdots$ \\  
        $0$ & $0$ & $0$ & $\cdots$ & $-\frac{y_{m,q}^{k}}{y_{p,q}^{k}}$ & $\cdots$ & $1$ & $y_{m,m+1}^{k+1}$ & $y_{m,m+2}^{k+1}$ & $\cdots$ & $0$ & $\cdots$ & $y_{m,n}^{k+1}$ & $d_{m}^{k+1}$ \\ \hline \hline
        $\sigma^{k+1}$ & $0$ & $0$ & $\cdots$ & $-\frac{\sigma_{ i_{q} }^{k}}{y_{p,q}^{k}}$ & $\cdots$ & $0$ & $\sigma_{i_{m+1}}^{k+1}$ & $\sigma_{i_{m+2}}^{k+1}$ & $\cdots$ & $0$ & $\cdots$ & $\sigma_{i_{n}}^{k+1}$ & $-z_{k+1}$ \\ \hline
    \end{tabular}
    % $\sigma_{i_{m+1}}^{k} - \frac{y_{p,m+1}^{k}}{y_{p,q}^{k}}\sigma_{ i_{q} }^{k}$
    \caption{经过一次\textbf{入基}和\textbf{出基}的操作后得到基可行解$x^{k+1}$的单纯形表}
    \label{InitialSimplexTableKP1}
\end{table}

Mixed Integer Linear Programming
======

Graph and Network
======

Nonlinear Programming
======
