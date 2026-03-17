---
created: 2026-03-16T15:55
updated: 2026-03-16T15:55
tags:
  - math
---
---
This is me studying for Topology final by doing a brain dump/reviewing everything. Topics in here are point set topology.  

---
### Metrics and Metric Spaces

Given points, something useful is determining how to measure dissimilarity/distance. This is what gives rise to a metric. 

We define a metric $d$ as something that satisfies 3 axioms over a set $X$:
1. Non-negativity, for all $x, y \in X, d(x, y) \geq 0$ and $d(x,y) = 0 \iff x = y$
2. Symmetry, for all $x, y \in X, d(x, y) = d(y, x)$
3. Triangle Inequality, for all $x, y, z \in X, d(x, z) \leq d(x, y) + d(y, z)$

A metric space is just when you define a set $X$ and the metric $d$ over that set.
#### Some definitions:
- If we have $(X, d_{X}), (Y, d_{Y})$ with a map $f: X \to Y$, then $f$ is continuous at a point $x_{0} \in X$ if given $\epsilon > 0$ there exists $\delta > 0$ such that $d_{Y}(f(x), f(x_{0})) < \epsilon$ whenever $d_{X}(x, x_{0}) < \delta$. 
- $f$ is continuous if $f$ is continuous at all $x \in X$

#### Some example metrics:
- $d_{1}(x, y) = \sum_{i \in I} |x_{i} - y_{i}|$
- $d_{2}(x, y) = \sqrt{ \sum_{i \in I} (x_{i} - y_{i})^{2}}$
- $d_{\infty}(x, y) = \max(|x_{i} - y_{i}|)$
- $d_{\text{discrete}}(x, y) = \begin{cases} 1 \text{ if } x \neq y \\ 0 \text{ if } x = y\end{cases}$


#### Bounded Subsets:
- A set $S \subseteq X$ is bounded if there exists $x_{0} \in X$ and $K \in \mathbb{R}$ such that $d(x, x_{0}) \leq K$ for all $x \in S$. 
- Diameter is $\sup \{ d(x, y) : x, y \in S \}$. 

#### Open Balls:
- Given metric space $(X, d)$ and $x_{0} \in X$, $r > 0$, we define an open ball as:
$$
B_{r}(x_{0}) = \{ x \in X : d(x, x_{0}) < r \}
$$
- $f: X \to Y$ is continuous at a point $x_{0} \in X$ iff given $\epsilon > 0$ there exists $\delta > 0$ such that $f(B_{\delta}^{d_{X}}(x_{0})) \subseteq B_{\epsilon}^{d_{Y}}(f(x_{0}))$
- A useful prop(5.31) is that for $B_{r}(x)$ and for any $y \in B_{r}(x)$ there exists $\epsilon$ such that $B_{\epsilon}(y) \subseteq B_{r}(x)$

#### Open sets in metric spaces:
- More general than open balls. Given $U \subseteq X$, we say $U$ is open if $\forall x \in U$, there exists $\epsilon_{x}$ such that $B_{\epsilon_{x}}(x) \subseteq U$. 
- With discrete metric, any subset is open. 
- Finite intersection of open sets is open and union of collections of open sets is also open.

#### Maps between metric spaces:
- A map $f: X \to Y$ between metric spaces is continuous iff $f^{-1}(U)$ is open in $X$ anytime $U$ is open in $Y$

#### Closed sets in metric spaces:
- $U$ is closed in $X$ if $X \setminus U$ is open in $X$
- Intersection of closed sets is closed 
- $f:X \to Y$ is continuous iff $f^{-1}(V)$ is closed whenever $V$ is closed in $Y$. 

#### Closure:
- If $A$ is a subset of a metric space $X$, then the closure of $A$, denoted as $\overline{A}$, is 
$$
\overline{A} = \{ x \in X : \exists\epsilon > 0, B_{\epsilon}(x) \cap A \neq \emptyset \}
$$
- Points in $\overline{A}$ are called points of closure
- $A \subseteq \overline{A}$, they are equal when $A$ is closed 
- Subset $A$ is dense in $X$ when $\overline{A}  = X$, $\mathbb{Q}$ is dense in $\mathbb{R}$
$$
\begin{align}
\overline{\bigcup_{i=1}^{m} A_{i}} &= \bigcup_{i=1}^{m} \overline{A_{i}} \\
\overline{\bigcap_{i=1}^{m} A_{i}} &\subseteq \bigcap_{i=1}^{m} \overline{A_{i}}
\end{align}
$$

#### Limit Points:
- These are the points $\overline{A} \setminus A$
- Contained in closure

#### Interior:
- If $A$ is a subset of a metric space $X$, then the interior of $A$, denoted as $\mathring{A}$, is 
$$
\mathring{A} = \{ a \in A : \exists \epsilon > 0, B_{\epsilon}(a) \subseteq A \} \}
$$
- $\mathring{A} \subseteq A$, they are equal when $A$ is open

#### Boundary:
- $\overline{A} \setminus A = \partial A$ 


---
### Topological Spaces

These are the generalization of metric spaces.  
A topological space is defined as $(X, \mathcal{T})$, where $\mathcal{T}$ is a family of subsets in $X$. Three axioms:
1. $\emptyset, X \in \mathcal{T}$ 
2. Intersection of two sets in $\mathcal{T}$ is in $\mathcal{T}$
3. Unions of any collection of sets in $\mathcal{T}$ is also in $\mathcal{T}$

Sets in $\mathcal{T}$ are called open. Metric spaces lead to topologies through the definition of open sets in metric spaces.  

Discrete topology is all subsets of $X$, indiscrete is $\{ \emptyset, X \}$. Coarser means that a topology is contains less. Given $\mathcal{T_{1}}, \mathcal{T_{2}}$, $\mathcal{T}_{1}$ is coarser if $\mathcal{T}_{1} \subseteq \mathcal{T}_{2}$. 

Sierpinski space $\mathbb{S} = \{ 0, 1 \}$ with the topology $\{ \emptyset, \{ 0 \}, \{ 0, 1 \} \}$.

Co-finite topology $\mathcal{T}_{\text{cofinite}}$ is empty set together with every subset $U$ of $X$ such that $X\setminus U$ is finite. 

#### Maps:
- $f: X \to Y$ if $U$ is open in $Y$ and $f^{-1}(U)$ is open in $X$.
- At a point $x \in X$ if $f(x) \in U'$, where $U'$ is open in $Y$, there exists $U$ that is open in $X$ with $x \in U$ and $f(U) \subseteq U'$. 
- Continuity of maps for metric spaces makes the same maps continuous for the underlying topological spaces 
- Composition of continuous maps is continuous
- Identity map is continuous

#### Homeomorphisms:
- Two spaces, $X, Y$ are homeomorphic if there exists a bijective map such that $f$ and its inverse function are continuous. 

#### Bases:
- Subfamily, $\mathcal{B} \subseteq \mathcal{T}$ such that any set in $\mathcal{T}$ can be made from a union of sets in $\mathcal{B}$
- We can prove continuity by only looking at basis elements
