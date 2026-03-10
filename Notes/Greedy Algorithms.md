---
created: 2025-03-06T09:36
updated: 2025-03-13T09:07
tags:
  - "#algorithms"
featured_image: imgs/Pasted image 20260310013938.png
thumbnail: imgs/resized/d93b2da479431da7d3cd007e06aaf091_86cf658e.webp
---
---
Greedy algorithms, in my experience, are the topic that people have the easiest time finding solutions for, but the hardest time proving. 

In essence, a greedy algorithm is one that makes *locally* optimal choices to come up with a *globally* optimal solution. A popular first example is the activity scheduling problem.

---
![[Pasted image 20260310013938.png]]

In this problem, we are given a set of activities, each of which has an associated start and end time. The goal is to maximize the number of activities that we can do such that they do not overlap.

In symbols, given a set $S$, we want to find a subset $A$, such that $A \subseteq S$, $\max |A|$, and $x, y \in A, x \neq y, x \cap y = \emptyset$. 

I think sometimes people can get a little tripped up with some of this notation, but it is good to get used to. $A \subseteq S$ just means we are selecting elements from the set $S$. $\max |A|$ just means we are maximizing the number of tasks we put in $A$. $x, y \in A, x \neq y, x \cap y = \emptyset$ just means that no two elements in $A$ intersect. 

Our greedy choice is selecting the option with the earliest finish time first. 
### Proving the Greedy Choice Property(GCP)
---
The GCP sometimes is a little misunderstood, but the general definition of it is:

> [!NOTE] GCP
> We can get to a *globally* optimal solution by making *locally* optimal choices. 


The general strategy for proving the GCP is as follows:
1. Define necessary variables
2. State greedy choice property: There *exists* an optimal solution that contains *insert greedy choice here*
3. Assume we have *an* optimal solution that does not contain our greedy choice. This does not necessarily mean that it is the *only* optimal solution, just that it exists in the solution space. 
4. Select some element/choice from optimal solution. 
5. Replace that with our greedy choice + show it's valid to do so. 
6. Show that it the result is *at least* as good. In some case, this may mean showing that we make something more optimal which contradicts that the original was optimal, this is fine and just means the only way to make it to globally optimal is through greedy choice. 

Hard steps tend to be 4 and 5. Once we define our elements and make the replacement, it tends to be fairly easy to show that it is optimal. 

For this problem:
1. Let $S$ be the set of activities, and $a_{1} \in S$ be the activity with the earliest finish time. 
2. There exists an optimal solution that contains $a_{1}$(our greedy choice). 
3. Assume we have $A$, which is an optimal solution for $S$ that does not contain $a_{1}$. 
4. Let $b_{1}$ be the activity with the earliest finish time from $A$.
5. Let $A' = (A \setminus b_{1}) \cup a_{1}$(this is just $A$ minus $b_{1}$ plus $a_{1}$, replacement). This is valid because $a_{1}$ must not intersect with any other element since is has an earlier finish time than $b_{1}$ so it can not intersect with any others.  
6. Then, $|A'| = |A|$. Since they both have the same size, $A'$ must also be optimal for $S$. 

---
### Proving the OSP
The general idea between the optimal substructure property is that, given a problem space $S$ and a solution $A$, our solution $A$ must be composed of a decision and an optimal answer to the resulting subproblem after that decision. 

The general strategy for proving the OSP is as follows:
1. Define large problem space and optimal solution
2. "Choose" greedy choice and make changes to both problem space and optimal solution
3. State(WTS) resulting solution is optimal for resulting problem space
4. Prove(usually by contradiction) that resulting solution is actually optimal for problem space. 

For this problem:
1. Let $S$ be the set of activities and $A$ be an optimal solution that contains $a_{1} \in S$, the activity with the earliest finish time. 
2. Let $A' = A - \{ a_{1} \}$ and $S'$ be the resulting set of activities after removing $a_{1}$ and any activities that conflict with it. 
3. We want to show that $A'$ must be an optimal solution to $S'$. 
4. Assume $A'$ is not an optimal solution for $S'$ and there exists an optimal solution $B$ such that $|B| > |A'|$. Then let $B' = B \cup a_{1}$. $|B'| > |A|$ which contradicts that $A$ was an optimal solution for $S$. Thus, $B$ must not exist and so $A'$ must be an optimal solution for $S$. 