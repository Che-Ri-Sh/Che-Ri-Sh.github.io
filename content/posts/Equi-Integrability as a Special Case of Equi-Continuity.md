---
date: '2026-03-14T17:00:00+08:00'
draft: false
title: 'Equi-Integrability as a Special Case of Equi-Continuity'
author: 'CHERISH'
---

 > *Originally written on Nov 1, 2023, this post came from some thoughts that arose during my undergraduate study of real analysis.*

---

In real analysis, **equi-integrability** is usually introduced as a technical condition on a family of integrable functions. At first sight, it looks quite different from the notion of **equi-continuity** in metric spaces.

But in fact, with the right point of view, equi-integrability can be interpreted as a very concrete instance of equi-continuity.

The key idea is simple: instead of viewing integration as acting on functions only, we view it as a functional acting on **measurable subsets** of a fixed set $E$. Once those subsets are equipped with a suitable metric, the analogy becomes exact.

---

## Two familiar definitions

Let us begin with the two notions we want to compare.

> **Definition (Equi-integrability).**  
> Let $\mathcal{F}$ be a family of measurable functions on a measurable set $E$ of finite measure. We say that $\mathcal{F}$ is **equi-integrable over $E$** if for every $\epsilon > 0$, there exists a $\delta > 0$ such that for every $f \in \mathcal{F}$,
> $$
> \text{if } A \subseteq E \text{ is measurable and } m(A) < \delta,\text{ then } \int_A \lvert f \rvert < \epsilon.
> $$

> **Definition (Equi-continuity).**  
> Let $(X,d_X)$ and $(Y,d_Y)$ be metric spaces, and let $\mathcal{F}$ be a family of functions from $X$ to $Y$. We say that $\mathcal{F}$ is **equi-continuous at a point $x_0 \in X$** if for every $\epsilon > 0$, there exists a $\delta > 0$ such that for every $f \in \mathcal{F}$,
> $$
> \text{for all } x \in X,\ \text{if } d_X(x_0,x)<\delta,\text{ then } d_Y\bigl(f(x_0),f(x)\bigr)<\epsilon.
> $$

The two definitions already look strikingly similar:

- in equi-continuity, a point $x$ close to $x_0$ forces $f(x)$ to be close to $f(x_0)$;
- in equi-integrability, a set $A$ with small measure forces $\int_A \lvert f\rvert$ to be small.

This suggests that “small measurable sets” may be playing the role of “points near a base point”.

---

## A metric on measurable sets

To make this precise, we need a metric space whose points are measurable sets.

Let $\mathcal{M}$ denote the collection of all measurable subsets of $\mathbb{R}$ with finite measure. Define
$$
d(A,B):=m(A\triangle B),
$$
where
$$
A\triangle B := (A\setminus B)\cup(B\setminus A)
$$
is the symmetric difference.

Intuitively, two sets are close when they differ only on a set of small measure.

> **Remark.**  
> If two measurable sets differ by a null set, then integrating the same function over them gives the same value. So in this discussion, it is natural to identify sets $A$ and $B$ whenever
> $$
> d(A,B)=m(A\triangle B)=0.
> $$
> We write this relation as
> $$
> A\doteq B.
> $$

The next fact is standard.

> **Lemma.**  
> The function
> $$
> d(A,B)=m(A\triangle B)
> $$
> defines a metric on $\mathcal{M}$, modulo the identification of sets that differ by a null set.

> **Proof.**  
> Nonnegativity and symmetry are immediate. Also,
> $$
> d(A,B)=0
> $$
> exactly when $A$ and $B$ differ by a null set.
>
> For the triangle inequality, it suffices to observe that
> $$
> A\triangle C \subseteq (A\triangle B)\cup(B\triangle C).
> $$
> Taking measures yields
> $$
> m(A\triangle C)\le m(A\triangle B)+m(B\triangle C),
> $$
> i.e.
> $$
> d(A,C)\le d(A,B)+d(B,C).
> $$
> $\square$

Now fix a measurable set $E$ of finite measure, and consider the subspace
$$
\mathcal{M}_E:=\lbrace S\subseteq E : S \text{ is measurable}\rbrace.
$$
This is simply the collection of measurable subsets of $E$, equipped with the same metric $d$.

---

## Integration as a functional on sets

Now let $f$ be an integrable function on $E$. Instead of thinking of $\int_S \lvert f\rvert$ merely as “an integral over a subset”, we package it into a functional:

${\Phi}_{f} :  {\mathcal{M}}_{E} \rightarrow {\mathbb{R}}$

$$
\Phi_f(S):=\int_S \lvert f\rvert
$$

This is well-defined with respect to our identification of sets modulo null sets.

> **Well-definedness.**  
> If $S_1\doteq S_2$, that is, $m(S_1\triangle S_2)=0$, then
> $$
> \int_{S_1}\lvert f\rvert = \int_{S_2}\lvert f\rvert.
> $$
> Hence $\Phi_f(S)$ depends only on the equivalence class of $S$.

Now let $\mathcal{F}$ be a family of integrable functions on $E$, and define the corresponding family of functionals
$$
\mathbf{\Phi}_{\mathcal{F}}
:=
\lbrace \Phi_f \mid f\in\mathcal{F}\rbrace.
$$

The right notion of equi-continuity here is equi-continuity at the point $E \in \mathcal{M}_E$.

> **Definition (Equi-continuity at the set $E$).**  
> We say that the family $\mathbf{\Phi}_{\mathcal{F}}$ is **equi-continuous at $E$** if for every $\epsilon>0$, there exists a $\delta>0$ such that for every $f\in\mathcal{F}$,
> $$
> \text{for all } S\in\mathcal{M}_E,\ \text{if } d(S,E)<\delta,\text{ then }
> \lvert \Phi_f(E)-\Phi_f(S)\rvert<\epsilon.
> $$

This definition should already feel close to equi-integrability: if $S$ is close to $E$, then $E\setminus S$ has small measure, so the integral over the “missing part” should be small.

---

## Main result

We can now state the equivalence precisely.

> **Corollary.**  
> Let $E$ be a measurable set of finite measure. Then
> $$
> \mathcal{F}\text{ is equi-integrable on }E
> \quad\Longleftrightarrow\quad
> \mathbf{\Phi}_{\mathcal{F}}\text{ is equi-continuous at }E.
> $$

> **Interpretation.**  
> In this sense, equi-integrability is a special case of equi-continuity: it is equi-continuity of a family of integration functionals on a metric space of measurable sets.

---

## Proof of the equivalence

We prove the two implications separately.

### From equi-continuity to equi-integrability

Assume that $\mathbf{\Phi}_{\mathcal{F}}$ is equi-continuous at $E$. Then for every $\epsilon>0$, there exists a $\delta>0$ such that for every $f\in\mathcal{F}$,
$$
d(S,E)<\delta
\quad\Longrightarrow\quad
\lvert \Phi_f(E)-\Phi_f(S)\rvert<\epsilon.
$$

Unpacking the definition of $\Phi_f$, we get

$$
\lvert \Phi_f(E)-\Phi_f(S)\rvert < \epsilon \ \iff \ \left\lvert \int_E \lvert f\rvert - \int_S \lvert f\rvert \right\rvert < \epsilon \ \iff \ \left\lvert \int_E \lvert f\rvert (\chi_E-\chi_S)\right\rvert < \epsilon \ \iff \ \int_{E\setminus S}\lvert f\rvert < \epsilon.
$$

Now take any measurable set $A\subseteq E$ such that $m(A)<\delta$, and define

$$
\tilde{S}:=E\setminus A.
$$

Since $\tilde{S}\subseteq E$, we have

$$
d(\tilde{S},E)=m(\tilde{S}\triangle E)=m(E\setminus \tilde{S})=m(A)<\delta.
$$

Therefore,

$$
\int_A \lvert f\rvert = \int_{E\setminus \tilde{S}}\lvert f\rvert < \epsilon.
$$

This is exactly the definition of equi-integrability.

---

### From equi-integrability to equi-continuity

Conversely, assume that $\mathcal{F}$ is equi-integrable on $E$. Then for every $\epsilon>0$, there exists a $\delta>0$ such that for every $f\in\mathcal{F}$ and every measurable $A\subseteq E$,
$$
m(A)<\delta
\quad\Longrightarrow\quad
\int_A \lvert f\rvert<\epsilon.
$$

Now let $S\in\mathcal{M}_E$ satisfy $d(S,E)<\delta$. Because $S\subseteq E$,

$$
d(S,E)=m(S\triangle E)=m(E\setminus S).
$$

So $m(E\setminus S)<\delta$, and by equi-integrability,

$$
\int_{E\setminus S}\lvert f\rvert<\epsilon.
$$

Hence

$$
\lvert \Phi_f(E)-\Phi_f(S)\rvert = \left\lvert \int_E \lvert f\rvert-\int_S \lvert f\rvert \right\rvert = \int_{E\setminus S}\lvert f\rvert <\epsilon
$$

Therefore $\mathbf{\Phi}_{\mathcal{F}}$ is equi-continuous at $E$.

This completes the proof. $\square$

---
## Final remark

Whether this observation is actually useful, I am honestly not sure. It may simply be a harmless little reinterpretation, worth reading with a smile rather than with too much seriousness.

---
## References

1. Royden, H. L. (1988). Real analysis (No. 6). Krishna Prakashan Media.


