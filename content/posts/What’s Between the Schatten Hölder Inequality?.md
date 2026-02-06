---
date: '2026-02-06T22:00:00+08:00'
draft: false
title: 'What’s Between the Schatten Hölder Inequality?'
description: 'Another perspective on the von Neumann trace inequality'
author: 'CHERISH'
---

\[TL;DR\] In this blog, I explain the following chain of inequalities, as well as other related concepts.

$$
\underbrace{
\overbrace{
\bigl|\mathrm{tr}(A^{\ast}B)\bigr|
\le
\lVert A^{\ast}B\rVert_{S_1} \le
}^{\text{von Neumann}}
\sum_{i=1}^r \sigma_i(A) \sigma_i(B)
\overbrace{
\le
\lVert A\rVert_{S_p} \lVert B\rVert_{S_q}
}^{\text{vector Hölder }}
}_{\text{Schatten Hölder}}.
$$

---

*Tighter or looser? That is the question for inequalities.* Usually, judging whether an inequality is “good” involves a trade-off. If a bound for the inequality is **too tight**, it is often too restrictive, working only under strong conditions and becoming hard to reuse in other arguments. On the other hand, if a bound is **too loose**, it is often too weak, giving a correct statement but one that does not meaningfully constrain the quantity of interest. This trade-off is why people often look for something "between" the inequalities: an estimate that is **tight enough to retain the right information**, while still **flexible enough to be reusable** across different contexts. That is exactly the motivation behind the question in the title of this post.

In particular, this post is about a instructive example of this tradeoff: bounding the trace pairing
$|\mathrm{tr}(A^*B)|$, for matrices $A,B\in\mathbb{C}^{m\times n}$. To my knowledge, there are at least two famous bounds:

1. **Schatten Hölder inequality**.
2. **von Neumann trace inequality**.

What are their connections? How to use them properly? We set out to answer these questions in this post.

{{< figure
    src="/images/von_Neumann.jpg"
    caption="Memorial plaque marking the birthplace of John von Neumann (1903–1957), photographed by the author during a solo trip to Budapest in 2024."
    style="max-width:60%; margin: 0 auto; text-align: center;"
>}}

---

Here are some notations we will adopt in this blog. Let matrices $A,B \in \mathbb{C}^{m \times n}$. By default, we assume that the singular values (denoted by $\sigma$) of those matrices are listed in descending order, i.e. 

$$
\sigma_1(A)\ge \sigma_2(A)\ge \cdots \ge \sigma_r(A)\ge 0,\qquad r:=\min\lbrace m,n\rbrace.
$$


## 1. Schatten norms and Schatten Hölder Inequality

Defining a meaning norm for a matrix is not that trivial (at least not as trivial as vector cases). Basically, there are three natural perspectives towards the matrix norms, each rooted in classical vector norms:
* vectorizing the matrix, which leads to **entry-wise norm**,
* inducing from vector norms, which leads to **operator norms**,
* applying vector norms to the spectra (singular values vectors), which leads to **Schatten norms**.

Here I want to clarify that the above three are "perspectives" instead of "categories". They can overlap (for instance, the spectral norm is both an operator norm and a Schatten norm), and they certainly do not exhaust all matrix norms of interest. Still, the motivations behind these perspectives are, in my opinion, genuinely distinct; and keeping them separate helps explain why different norms arise naturally in different settings. In this article, we mainly focus on Schatten norms (we may discuss others in future posts, though).

> **Definition 1.1 (Schatten $p$-norm).**  
> Let $A\in\mathbb{C}^{m\times n}$ and let $\sigma_1(A)\ge \cdots \ge \sigma_r(A)\ge 0$ denote the singular values of $A$, where $r=\min\lbrace m,n\rbrace$. The Schatten $p$-norm (denoted as $\lVert \cdot\rVert_{S_p}$) is defined as follows: When $1\le p<\infty$:
>
> $$
> \lVert A\rVert_{S_p}:=\left(\sum_{i=1}^r \sigma_i(A)^p\right)^{1/p},
> $$
>
> when $p=\infty$:
>
> $$
> \lVert A\rVert_{S_\infty} =\sigma_1(A).
> $$
  
There are several useful special cases of Schatten norms:

- $p=1$: **nuclear / trace / Ky Fan norm**

  $$
  \lVert A\rVert_{S_{1}}=\lVert A\rVert_{\ast}=\sum_{i=1}^{r} \sigma_{i}(A).
  $$

- $p=2$: **Frobenius norm**

  $$
  \lVert A\rVert_{S_2}=\lVert A\rVert_F=\sqrt{\mathrm{tr} \left(A^{\ast}A\right)}.
  $$

- $p=\infty$: **spectral norm**

  $$
  \lVert A\rVert_{S_{\infty}}=\lVert A\rVert_2=\sigma_1(A).
  $$

  
---
### The Schatten Hölder inequality

In measure spaces, we have the famous Hölder inequality
$\lVert fg\rVert_1\le \lVert f\rVert_p \lVert g\rVert_q$ with $1/p+1/q=1$.
Fortunately, an analogous property is inherited by Schatten norms.

> **Theorem 1.2 (Schatten Hölder Inequality).**  
> Let $1\le p,q\le\infty$ satisfy $\frac1p+\frac1q=1$. For all conformable matrices $A,B$,
>
> $$
> \bigl|\mathrm{tr}(A^{\ast}B)\bigr|
> \le
> \lVert A\rVert_{S_{p}}\lVert B\rVert_{S_{q}}.
> $$

\[Remark\] Indeed, the direct form of the inequality should be $\lVert A^{\ast}B\rVert_{S_1}\le \lVert A\rVert_{S_p} \lVert B\rVert_{S_q}$. However, since $\bigl|\mathrm{tr}(A^{\ast}B)\bigr|\le \lVert A^{\ast}B\rVert_{S_1}$, we often use the trace form above, which is usually more convenient in applications.

It's worthwhile to note the following three famous special cases of this inequality:

- $p=q=2$ gives **Frobenius Cauchy--Schwarz**:

  $$
  \bigl|\mathrm{tr}(A^{\ast}B)\bigr|
  \le
  \lVert A\rVert_F \lVert B\rVert_F.
  $$

- $p=1,q=\infty$ gives **nuclear--spectral duality**:

  $$
  \bigl|\mathrm{tr}(A^{\ast}B)\bigr| \le \lVert A\rVert_{S_{1}} \lVert B\rVert_{S_{\infty}} = \lVert A\rVert_{\ast} \lVert B\rVert_2.
  $$

- $A=B$ gives a **Schatten norm inequality**:

  $$
  \lVert A\rVert_F^2
  \le
  \lVert A\rVert_{S_{p}}\lVert A\rVert_{S_{q}}.
  $$


---

## 2. The von Neumann trace inequality

As one of the most useful theorems in matrix analysis, the von Neumann trace inequality establishes a sharp connection between the trace inner product of two matrices and the alignment of their singular-value spectra. While most textbooks state this theorem for square matrix, the results are correct for rectangular ones as well.

> **Theorem 2.1 (von Neumann trace inequality).**  
> For $A,B\in\mathbb{C}^{m\times n}$ and $r=\min \\{m,n\\}$,
>
> $$
> |\mathrm{tr}(A^*B)| \le \sum_{i=1}^r \sigma_i(A)\sigma_i(B). \tag{VN}
> $$

Note that the right-hand side is the inner product of singular-value vectors:

$$
\sum_{i=1}^r \sigma_i(A)\sigma_i(B) = \langle \sigma(A),\sigma(B)\rangle.
$$

As pointed out in the book *Topics in Matrix Analysis* (where, unfortunately, the von Neumann trace inequality is presented only as an exercise, in page 182-183), the inequality is the immediate consequence of following two classical singular-value inequalities.

> **Lemma 2.2 (Eigenvalues vs singular values).**  
> Let $A \in M_n$ have eigenvalues $\{\lambda_1(A),\dots,\lambda_n(A)\}$ ordered such that $|\lambda_1(A)| \ge \cdots \ge |\lambda_n(A)|$, and singular values $\sigma_1(A) \ge \cdots \ge \sigma_n(A) \ge 0$.  Then, for every $k=1,\dots,n$,
> $$
> \sum_{i=1}^k |\lambda_i(A)| \le \sum_{i=1}^k \sigma_i(A).
> $$
>
> In particular,
>
> $$
> |\mathrm{tr}(A)| \le \sum_{i=1}^n \sigma_i(A).
> $$


> **Lemma 2.3 (Singular values of product).**  
> Let $A \in M_{n,t}$ and $B \in M_{t,m}$, and set $r = \min\lbrace n,t,m\rbrace$. Denote the ordered singular values of $A$, $B$, and $AB$ by $\sigma_1(A) \ge \cdots \ge \sigma_{\min(n,t)}(A)$, $\sigma_1(B) \ge \cdots \ge \sigma_{\min(t,m)}(B)$, and $\sigma_1(AB) \ge \cdots \ge \sigma_r(AB)$. Then, for every $k=1,\dots,r$,
> $$
> \sum_{i=1}^k \sigma_i(AB) \le \sum_{i=1}^k \sigma_i(A) \sigma_i(B).
> $$

While **Lemma 2.2** can be proved directly from the SVD, the proof of **Lemma 2.3** is more subtle. A standard route is to view it as a weak majorization statement for singular values,

$$
\sigma(AB)\ \prec_w\ \sigma(A)\odot\sigma(B),
$$

and then derive the partial-sum inequalities from majorization theory. However, we will not pursue the full proof here.


---

## 3. The connection

As you can see, the von Neumann trace inequality and the Schatten Hölder inequality both seek for a bound of $|\mathrm{tr}(A^*B)|$. Then the problem arises:

**What are their connections?**

Well, actually the answer is simple but nontrivial. Applying the (vector) Hölder inequality to $\langle \sigma(A),\sigma(B)\rangle$, we have

$$
\sum_{i=1}^r \sigma_i(A) \sigma_i(B) \le \lVert\sigma(A)\rVert_p \lVert\sigma(B)\rVert_q = \lVert A\rVert_{S_p} \lVert B\rVert_{S_q}.
$$

In other words, Schatten Hölder is a corollary of von Neumann trace inequality, obtained by applying the classical Hölder inequality to the singular-value vectors. Since
$|\mathrm{tr}(A^{\ast}B)| \le \lVert A^{\ast}B\rVert_{S_1}$
and
$\lVert A^{\ast}B\rVert_{S_1} = \sum_i \sigma_i(A^{\ast}B)$,
for $\frac{1}{p}+\frac{1}{q}=1$, we have the following important inequality chain:

> **Corollary 3.1**
>
> $$
> \underbrace{
> \overbrace{
> \bigl|\mathrm{tr}(A^{\ast}B)\bigr|
> \le
> \lVert A^{\ast}B\rVert_{S_1} \le
> }^{\text{von Neumann}}
> \sum_{i=1}^r \sigma_i(A) \sigma_i(B)
> \overbrace{
> \le
> \lVert A\rVert_{S_p} \lVert B\rVert_{S_q}
> }^{\text{vector Hölder }}
> }_{\text{Schatten Hölder}}.
> $$

I believe the inequalities in **Corollary 3.1** is enough to answer the questions in the title of this blog, i.e. **What’s Between the Schatten Hölder Inequality?**  However, to better understand the intrinsic properties of these inequalities, it is natural to go one step further: **when is the inequality strict, and when do we have equality?**

---
### A quick strictness example

Here is a simple one: Let $A=I_r$ and let $B$ be a rank-one matrix with singular values $\sigma(B)=(1,0,\dots,0)$. Then
$|\mathrm{tr}(A^{\ast}B)|=|\mathrm{tr}(B)|\le 1$,
and we also have $\sum_i \sigma_i(A)\sigma_i(B)=1$. Therefore, the von Neumann trace inequality can be tight.

However,
$\lVert A\rVert_F \lVert B\rVert_F=\sqrt{r}\cdot 1=\sqrt{r}$,
so the second inequality (vector Hölder) is loose.

The key takeaway message is, Schatten Hölder can be weaker than von Neumann trace inequality, especially in high dimensions. The intuitive reason is that Schatten Hölder forgets where the spectrum is concentrated.

---

## 4. Equality conditions for Schatten Hölder

A more interesting question, however, is: when does the entire chain become tight? In what follows, we examine the equality conditions for each inequality in the chain.

### 4.1. Equality in von Neumann: **singular vector alignment**

Equality in von Neumann trace inequality, i.e.

$$
|\mathrm{tr}(A^*B)|=\sum_{i=1}^q \sigma_i(A)\sigma_i(B),
$$

holds (informally) if and only if $A$ and $B$ share a common singular vector basis. Mathematically, the condition will be: there exist unitary matrices $U\in \mathbb{U}(m)$ and $V\in \mathbb{U}(n)$ such that

$$
A = U \Sigma_A V^{\ast} ,\qquad B = U \Sigma_B V^{\ast},
$$

where $\Sigma_A,\Sigma_B$ are rectangular diagonal with the singular values on the diagonal in the same order. Specifically, we can choose $\tilde{\Sigma}_A = \mathrm{diag}(\sigma_1(A),\cdots,\sigma_r(A))$ and $\tilde{\Sigma}_B = \mathrm{diag}(\sigma_1(B),\cdots,\sigma_r(B))$; and $\Sigma = [\tilde{\Sigma}, 0]$, or $\Sigma = [\tilde{\Sigma}, 0]^\top$, depending on the dimension of $\mathbb{C}^{m\times n}$.

\[Remark\] Interestingly, I find another equivalent condition, which seems to be more "clean": Equality holds if and only if $\lambda_i(A^*B)=\sigma_i(A)\sigma_i(B)$.

Another related theorem can be found in Theorem (7.4.10) of the book *Matrix Analysis* by Roger A. Horn, which states as follows:

> **Theorem 4.1 (Exact spectral pairing).**  
> Let $A, B \in \mathbb{C}^{m\times n}$, and denote $r := \min\{m,n\}$. Let $\sigma_1(A)\ge \cdots \ge \sigma_r(A)$ and $\sigma_1(B)\ge \cdots \ge \sigma_r(B)$ be the singular values of $A$ and $B$, respectively.  If both products $A^*B$ and $B^*A$ are positive semidefinite, then there exists a permutation $\tau$ of $\{1,\dots,r\}$ such that
> $$
> \mathrm{tr}(A^*B) = \mathrm{tr}(B^*A) = \sum_{i=1}^r \sigma_i(A) \sigma_{\tau(i)}(B).
> $$

### 4.2. Equality in the vector Hölder step: **singular value proportionality**

Now consider the second inequality:

$$
\sum_{i=1}^{r} \sigma_i(A) \sigma_i(B) = \langle \sigma(A),\sigma(B) \rangle \le \lVert A\rVert_{S_p}\lVert B\rVert_{S_q}.
$$

Well, this case is rather simple. For $1<p<\infty$, equality in vector Hölder occurs exactly when the sequences are proportional in the Hölder sense. Mathematically, the equality condition will be:
there exists $c>0$ such that

$$
\sigma_i(A)^p = c \sigma_i(B)^q
\quad \text{for all } i \text{ on the common support},
$$

or equivalently,

$$
\sigma(B)\ \propto\ \sigma(A)^{p-1}.
$$

\[Remark\] The case $p=1,q=\infty$ will be a bit different. It has something like “support on maximizers” condition, but the idea is the same.

### 4.3. Equality in Schatten Hölder: direction + magnitude

By the sandwiching in Corollary 3.1, we conclude the following simple but important result:

> **Corollary 4.2 (Equality in Schatten Hölder).**  
> The equality $\bigl|\mathrm{tr}(A^{\ast}B)\bigr|  = \lVert A\rVert_{S_p} \lVert B\rVert_{S_q}$
> holds if and only if both inequalities in §4.1 (von Neumann trace inequality)
> and §4.2 (vector Hölder inequality) are equalities, or equivalently,
>
> $$
> B = c A|A|^{p-2}, \quad \text{for some } c\in\mathbb{C}.
> $$

Intuitively, the equality in Schatten Hölder requires:

1. **Geometric alignment** (von Neumann equality): singular vectors match.
2. **Spectral proportionality** (vector Hölder equality): proportional singular values.

This might also explain why Schatten Hölder seems “rarer” than von Neumann equality: it demands not only the matrices point in the same singular directions, but also their singular values have the correct *shape* (w.r.t $p$).

---

## 5. Further discussions

### 5.1. Is von Neumann trace inequality always more preferable?

We have seen that the von Neumann trace inequality is generally tighter than the Schatten–Hölder inequality. However, *being tighter does not mean being universally more useful*. In practice, the two inequalities serve different analytical purposes, and neither strictly dominates the other. Here is a practical example:

In matrix-parameter gradient discent, we usually consider the trace pairing between a (stochastic) gradient-like matrix $G$ and an update direction $\Delta W$:

$$
\langle G,\Delta W\rangle_F = \mathrm{tr}(G^*\Delta W).
$$

In many algorithms, the update is designed or analyzed under a constraint of the form

$$
\|\Delta W\|_{S_p} \le \eta,
$$

where $p$ depends on the geometry we want to enforce (e.g., low-rank bias via nuclear norm, stability via spectral norm, or others). In this setting, Schatten--Hölder gives an immediate and modular bound:

$$
\bigl|\mathrm{tr}(G^{\ast}\Delta W)\bigr|
\le
\lVert G\rVert_{S_q} \lVert \Delta W\rVert_{S_p},
\qquad
\frac{1}{p}+\frac{1}{q}=1.
$$

hence $|\mathrm{tr}(G^*\Delta W)| \le \eta \|G\|_{S_q}$.

As far as I can conclude, this is often preferable for at least the following reasons:
	
- **Specific norm control.**  
  You can adjust $(p,q)$ to match what you control. For instance, if your update is nuclear-norm bounded ($p=1$), then $q=\infty$ and
  $$
  \bigl|\mathrm{tr}(G^{\ast}\Delta W)\bigr|
  \le
  \lVert G\rVert_{S_{\infty}} \lVert \Delta W\rVert_{S_1}.
  $$
  If your update is spectral-norm bounded ($p=\infty$), then $q=1$ and
  $$
  \bigl|\mathrm{tr}(G^{\ast}\Delta W)\bigr|
  \le
  \lVert G\rVert_{S_1} \lVert \Delta W\rVert_{S_{\infty}}.
  $$
  By contrast, the von Neumann form
  $$
  \bigl|\mathrm{tr}(G^{\ast}\Delta W)\bigr|
  \le
  \sum_i \sigma_i(G) \sigma_i(\Delta W)
  $$
  is sharper but has less built-in information when you need to interface with norm constraints.
	
- **Duality.**

  Schatten--Hölder is exactly the mechanism behind dual norms. A canonical identity is the duality between nuclear norm and spectral norm:
  $$
  \sup_{\lVert X\rVert_{S_1}\le 1}\mathrm{tr}(G^{\ast}X) =\lVert G\rVert_{S_{\infty}}.
  $$
  This is the standard bridge that turns trace objectives into norm bounds in analysis of regularization and primal--dual derivations.

### 5.2 “What’s between” revisited

At the end of this blog, I would like to revisit the problem "What’s Between the Schatten Hölder Inequality?" from a perspective of "information" (not those in information theory, though). Let recap the upper bound for $|\mathrm{tr}(A^*B)|$ that we've discussed:

- von Neumann trace inequality provides the **spectral inner product** $\langle \sigma(A),\sigma(B)\rangle$,
- Schatten Hölder inequality replaces it by **norm summaries** $\lVert \sigma(A)\rVert_{\ell_{p}} \lVert \sigma(B)\rVert_{\ell_{q}}$.

Therefore, the gap between them measures how much information you lose by compressing the spectrum into a single scalar.

## (Exercises)

Here is an exercise that I leave for my dear readers (if you are patient enough to read this far):

* Can you find an example of matrices $(A,B)$ such that all the three inequalities in **Corollary 3.1** are strict?

---
## References

1. Horn, R. A., & Johnson, C. R. (1994). _Topics in matrix analysis_. Cambridge university press.
2. Horn, R. A., & Johnson, C. R. (2012). _Matrix analysis_. Cambridge university press.
3. Fan, K. (1951). Maximum properties and inequalities for the eigenvalues of completely continuous operators. _Proceedings of the National Academy of Sciences_, _37_(11), 760-766.
4. Demmel, J. W. (1997). _Applied numerical linear algebra_. Society for Industrial and Applied Mathematics.
5. Boyd, S., & Vandenberghe, L. (2004). _Convex optimization_. Cambridge university press.
6. Lan, G. (2013). The complexity of large-scale convex programming under a linear optimization oracle. _arXiv preprint arXiv:1309.5550_.
7. Yuan, Y. X. (2000, July). A review of trust region algorithms for optimization. In _Iciam_ (Vol. 99, No. 1, pp. 271-282).
8. Braun, G., Carderera, A., Combettes, C. W., Hassani, H., Karbasi, A., Mokhtari, A., & Pokutta, S. (2022). Conditional gradient methods. _arXiv preprint arXiv:2211.14103_.
9. Jordan, K., Jin, Y., Boza, V., You, J., Cesista, F., Newhouse, L., and Bernstein, J. Muon: An optimizer for hidden layers in neural networks, 2024. URL https://kellerjordan.github.io/posts/muon/.
10. Bernstein, J. Deriving muon, 2025. URL https://jeremybernste.in/writing/deriving-muon.
11. Pethick, T., Xie, W., Antonakopoulos, K., Zhu, Z., Silveti-Falls, A., & Cevher, V. (2025). Training deep learning models with norm-constrained lmos. arXiv preprint arXiv:2502.07529.
12. Xu, C., Yan, W., & Zhang, Y. J. A. (2026). FISMO: Fisher-Structured Momentum-Orthogonalized Optimizer. arXiv preprint arXiv:2601.21750.

---

CHERISH

2026.2.6, in Hong Kong