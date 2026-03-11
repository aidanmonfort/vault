---
created: 2026-03-09T13:01
updated: 2026-03-09T15:14
tags:
  - algorithms
  - "#compbio"
  - video
featured_image: imgs/youtube/8CN6kbjKn6c.webp
thumbnail: imgs/resized/485c0cc25b4b8b9104c8f9dacfc6cb00_86cf658e.webp
---
---
This is a super beautiful algorithm designed for computing suffix arrays in $O(n)$ time. 
![Link](https://youtu.be/8CN6kbjKn6c?si=dAYKpg54RxAophyE)

---
## Input/Output Definition: 
As input, we take some arbitrary string $S$ and compute the suffix array which is a sorted array of all suffixes of string $S$. 
Example: $S=\text{abcdabcd}$

| index | string   | suffix index |
| ----- | -------- | ------------ |
| 0     | abcd     | 4            |
| 1     | abcdabcd | 0            |
| 2     | bcd      | 5            |
| 3     | bcdabcd  | 1            |
| 4     | cd       | 6            |
| 5     | cdabcd   | 2            |
| 6     | d        | 7            |
| 7     | dabcd    | 3            |

In practice a terminal character(usually $, in these notes I use @) is appended to $S$. 

Naively, something like mergesort would take $O(n^{2}\log n )$ since comparison is going to be an $O(n)$ operation.

---
## Algorithm Details:

Instead of computing the suffix array directly, this algorithm solves an inverse problem. We solve the rank array construction which is the inverse of the suffix array. Let $R$ be the rank array induced by $S$, $R[i] = r, \text{SuffixArray[r] = i}$. $R[i] = r$ means that the suffix at index $i$ has $r$ suffixes before it in the suffix array. 

At a high level:

```python
def DC3(string S):
	R_12 = DC3(suffixes of S starting at i % 3 != 0)# 2/3 rank array(ish)
	R_0 = build from R_12 #1/3 rank array(ish) O(n)
	R = merge from R_12 and R_3 #full rank array O(n)
	return R 

```

---
### Inducing $R_{0}$ in linear time
Let's first assume that $R_{12}$ is computed correctly as in line 1. Then, we want to sort the suffixes of $S_{0}, S_{3}, \dots$ in linear time(suffixes starting at index $i$ where $i(\text{mod } 3) = 0$).

We can do this with a radix sort! Using the information from $R_{12}$, we can rewrite:
$$
\begin{align}
S_{0} &= S[0]R_{12}[1] \\
S_{3} &= S[0]R_{12}[4] \\
&\vdots
\end{align}
$$
Essentially instead of having to sorting strings $S_{0}$ and $S_{3}$ in $\Theta(n\log n)$ time, we can use the ranks we have found to make this sorting $\Theta(n)$ by using first character as first radix, and rank information as second radix. 

So, inducing the ranks of suffixes at indices $i(\text{mod } 3) = 0$ is done in $\Theta(n)$ time. 

---
### Merging
For merging, we use this very similar trick of using our known suffixes to induce rank. Given that we have two partial suffix arrays that are sorted, we can begin to merge them. 

Let $A$ be the suffix array induced by $R_{0}$, and $B$ be the suffix array induced by $R_{12}$. We want to merge $A$ and $B$ such that the result is the suffix array for $S$. 

To do this, we use the standard merge sort merge with some special comparison logic. 

Observation 1:
Comparing 2 strings from $R_{12}$ is easy. 

Observation 2:
Using the same technique from inducing $R_{0}$, we can force a comparison between two strings in $B$. 

There is only two cases. 
First case, say we wanted to compare $S_{0}$ and $S_{1}$(suffixes starting at 0 and 1 respectively), using the same trick:
$$
\begin{align}
S_{0} &= S[0]R_{12}[1] \\
S_{1} &= S[1]R_{12}[2] \\
\end{align}
$$
From observation 1, this is now an easy comparison since we only need to compare first character and then rank. 

Second case, if we wanted to compare $S_{0}$ and $S_{2}$, when we use the trick:

$$
\begin{align}
S_{0} &= S[0]R_{12}[1] \\
S_{2} &= S[2]R_{0}[3] \\
\end{align}
$$
Now this does not work since $R_{0}[3]$ is not a part of $R_{12}$. This sounds like a problem, but actually, we can just do this again.
$$
\begin{align}
S_{0} &= S[0]S[1]R_{12}[2] \\
S_{2} &= S[2]S[3]R_{12}[4] \\
\end{align}
$$
Now in this case, we only need two character comparisons and one rank comparison(int comparison). This makes comparisons an $O(1)$ operation. 

Since we can make our comparisons $O(1)$, we can merge the two in $\Theta(n)$.

---
## Creating $R_{12}$ 
Now is the hard part, creating $R_{12}$. The first question is what do we pass in recursively such that we can actually only process $R_{12}$ from the original string. To answer this, we use a few tricks. 

First, instead of passing in $S$, we will create:
$$
\begin{align}
S' &= [\text{bcd}][\text{abc}][\text{d@@}][\text{@@@}][\text{cda}][\text{bcd}][\text{@@@}] \\
S' &= S[1 \dots n)[\text{@@@}]S[2\dots n)

\end{align}
$$
If we look at the triples, each triplet becomes *approximately* a suffix from $S$ that starts at an index that is not a multiple of 3. 

Then, we can make our recursive call on this! Well, not actually, if our original alphabet is $\sigma$, then forming these triples creates an explosion on our alphabet. 

This is where our second trick comes in, since we have static sized triples, we can use a counting sort and simply map each triplet to its frequency. This maintains our alphabet size as being strictly less than $n$ and approximately $\frac{2n}{3}$. 

---
## Runtime
Then overall, 
$$
T(n) = T\left( \frac{2n}{3} \right) + \Theta(n)
$$

You can choose your favorite method to solve this, but it will result in $\Theta(n)$ in runtime. 

---
#### Side notes
- DC refers to difference cover, a concept in math.
- Overall, very nice!

