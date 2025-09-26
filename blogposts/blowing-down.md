---
layout: post
title: Blowing DOWN (not UP!)
---


### Motivation
One of the basic constructions in complex / algebraic geometry is *blow-ups* (also known as the "$\sigma$-process" or "monoidal construction"): roughly speaking, this is when you take a point in your variety and "replace" it by its "space of directions", in an appropriate sense. The newly-added subvariety is called the *exceptional divisor*, and it's isomorphic to a copy of projective space; this makes sense, as projective spaces are precisely "spaces of directions".

The process of blowing-up is immensly useful for resolving singularities: the affine plane curve $\{xy=0\}$ is singular at the origin -- it is the union of the $x$-axis and $y$-axis. If we blow-up this point on the plane (pro tip: don't say this at an airport), then there will now be two distinct "points" corresponding to the two different "directions" at the origin, so the two branchs of our curve will get separated. Singularities that locally look like the union of axes are called *normal crossings*, and they can always be resolved by a simple blow-up. Such intersections between the axes are also called *transverse*.

A fundamental fact about blow-ups is that they do not affect the field of (rational or meromorphic) functions on your variety. In experts' lingo, we'd say that the blown-up variety is *birationally equivalent* (or *birational* for short) to the original one. Of course we can keep blowing-up points and get larger and larger varieties.

### Minimality
Now the goal of the *minimal model program* is to find a "minimal" representative for each birational class. For curves the problem is fairly elementary, and for surfaces there is a successful definition of minimality: we simply require it to not be the blow-up of anything else. The definition in higher dimensions is a bit more intricate.

Of course, this definition for minimality of surfaces really sucks, because we have no idea how to verify it. Do you really have to consider *all surfaces ever*, and blow them up in *every possible way*, and check if each blow-up is isomorphic to your surface? Luckily, Castelnuovo found a more computation-friendly criterion:

**Theorem (Castelnuovo):** Let $X$ be a surface. If $X$ contains a *$(-1)$-curve* $E$, that is, a copy of the projective line $E \simeq \mathbb{P}^1$ with self-intersection $(E\cdot E) = -1$, then $X$ is the blow-up of another surface with $E$ being the exceptional divisor.

**Warning:** I will always implicitly work over $\mathbb{C}$ with complex analytic varieties or complex manifolds. Throughout this post I'll often neglect various crucial assumptions on our varieties, such as nonsingular-ness, normality, projectivity, reduced-ness, etc... This should not distract you from the main ideas.

Requiring $E$ to be a $\mathbb{P}^1$ is obvious, because the exceptional divisor of any blow-up is always isomorphic to a $\mathbb{P}^1$. Requiring its self intersection to be $-1$ is a bit more intricate, so I'll show it soon. The full proof of Castelnuovo's criterion is not too challenging, and can be found in Hartshorne (Theorem V.5.7).

You might think this is still tough to verify, because we need to check for *every curve on the surface* whether it's a $(-1)$-curve, but this is not the case. Indeed, being a $(-1)$-curve is evidently invariant under algebraic equialence of divisors, so we only need to look at the finite Néron-Severi group. Moreover each blow-down decreases the size of the Néron-Severi group, so the process must terminate.

### Self-intersections
Just for the sake of intuition, I'd like to partially prove here the "easy" direction of Castelnuovo's criterion. More specifically I'd like to compute the self-intersection of the exceptional divisor in a blow-up. I begin with some general observations.

Recall that a priori, the intersection number of two curves only makes sense when they intersect transversely, but self-intersections couldn't be further from transverse. In general, if the curves have non-transversal intersection points, we have to "perturb" or "deform" at least one of them so as to make the intersection transversal. It is a standard fact that the deformation theory of an embedded curve is controlled by its *normal bundle*: a section of the normal bundle is analogous to a choice of normal vector at each point on the curve, which dictates how much this point will move during the deformation.

The points of intersection of the original curve with the slightly deformed ones will be precisely those where the chosen normal vector is zero, i.e. the zeros of the corresponding section. But the number of zeros of a general section of a bundle is precisely its degree, so we informally predict the formula:

$$(C\cdot C) = \operatorname{deg}_C(\mathscr{N}_{C/X})$$

This formula turns out to be rigorously true so long as $C$ is smooth. To apply this on the exceptional divisor of a blow-up, we should determine its normal bundle.

Given a blow-up $\sigma : X \to Y$, we think of the exceptional divisor $E$ as a copy of $\mathbb{P}^1$, replacing the original point $y$ that we blew-up. A "point" on $E$ is a "line" through $y$, so a "tangent vector" on $E$ is an "infinitesimal rotation" of such line. Therefore a "normal vector" on $E$ is precisely a vector which is *parallel* to the line through $y$. In other words, we expect to get the tautological bundle of $\mathbb{P}^1$:

$$\mathscr{N}_{E/X} = \mathcal{O}_E(-1)$$

Again under some smoothness assumptions, this can be proven rigorously. The two formulas together immediately give us the expected result

$$\boxed{(E\cdot E) = -1}$$


There is another way to prove this identity, which is actually a bit closer to what we will do later in the general case, so I'll show that next. But first I must remind of some standard terminology: if $D$ is a divisor on $Y$, we call $\sigma^{-1}(D)$ the *total transform* of $D$. Away from $y$, the blow-up map is a biholomorphism, so that case is not so interesting. But if $D$ passes through $y$, then its total transform will contain some copies of the exceptional divisor $E$. By removing these copies of $E$, the remaining divisor is called the *strict transform* of $D$ and typically denoted $\overline{D}$.

Now for the second proof. Let $D_1,D_2$ be two smooth divisors crossing transversely at the point of blow-up $y$ (e.g. the coordinate axes in a local coordinate system). Then their intersection number is simply $(D_1\cdot D_2) = 1$. Their total transforms are then $\sigma^{-1}(D_i) = E + \overline{D_i}$, so we can compute the intersection number of their total transforms by

$$\begin{align*}
(\sigma^{-1}(D_1)\cdot\sigma^{-1}(D_2))
&= (E\cdot E) + (E\cdot\overline{D_2}) + (\overline{D_1}\cdot E) + (\overline{D_1}\cdot\overline{D_2}) \\
&= (E\cdot E) + 1 + 1 + 0
\end{align*}$$

On the other hand, intersection numbers should be invariant under perturbations, so if we nudge both $D_1,D_2$ such that they still intersect transversely, but not at $y$, then their total and strict transforms would coincide, and we'd get

$$(\sigma^{-1}(D_1)\cdot\sigma^{-1}(D_2)) = 1$$

Overall, we conclude

$$\boxed{(E\cdot E) = -1}$$


### Contractibility in general
Blow-ups are nice and all, but they're not the whole story. Here's another interesting definition:
**Definition:** A subvariety $E \subseteq X$ is called *exceptional* if it can be *contracted* to a point in the following sense: there exists a birational map $f : X \to Y$ which maps $E \subseteq X$ down to a single point $y \in Y$, and maps $X\setminus E$ *biholomorphically* onto $Y\setminus\{y\}$.

Clearly exceptional divisors of blow-ups are exceptional in this sense. If we had an analogue for Castelnuovo's criterion for arbitrary exceptional subvarieties, maybe we could use this as a definition for minimality in higher dimensions?

**Warning:** This is *not* the same as the general definition of minimality that I mentioned earlier. As a non-expert in this field, I don't know if this alternative definition is actually used in the minimal model program. Perhaps my definition is equivalent to the standard one, but I didn't bother thinking about this in much detail yet.

**Remark:** Contractions which are not blow-ups are not strictly necessary in the minimal model program, thanks to some of its deepest results: *weak factorization* states that every birational equivalence is some composition of blow-ups and blow-downs (possibly mixed among one another). *Strong factorization* states that every birational equivalence is some composition of blow-ups followed by some composition of blow-downs. Weak factorization is now a theorem, while strong factorization is still conjectural except for some cases. Surfaces are indeed known to satisfy strong factorization, and in fact this was one of the original motivations for stating these conjectures in the first place!

Nevertheless, general contractions are still interesting in their own right. My goal in this post is to sketch a proof of Grauert's criterion, which generalizes Castelnuovo's criterion from $(-1)$-curves to arbitrary exceptional curves.

**Theorem (Grauert):** Let $X$ be a surface. Let $C \subseteq X$ be a compact & connected curve, and $C_1,\cdots,C_n$ its irreducible components. Then $C$ is exceptional if and only if the intersection matrix $((C_i\cdot C_j))$ is negative-definite.

The compactness assumption here is crucial. Connectedness could be relaxed, if you are willing to contract your curve not to a single point but to finitely many points (one for each connected component).

### Necessity
Let's start with the easy direction, which was already known before Grauert's work: the intersection matrix of an exceptional curve is negative-definite. Before seeing the general case, let's look what happens when there's only one irreducible component: if $X$ is a surface and $C \subseteq X$ is an exceptional *irreducible* compact curve, do we have $(C\cdot C) < 0$?

We've seen earlier that $(E\cdot E) = -1$ for the exceptional divisor of a blow-up. There's a similar argument here: let $g$ be a nonzero holomorphic function on $Y$ which vanishes at $y$, so that $D = (g)$ is a positive principal divisor passing through $y$. The total transform decomposes to a strict transform, plus a few copies of the exceptional curve $C$: $\sigma^{-1}(D) = mC + \overline{D}$. Moreover, the total transform is still a positive principal divisor (it's just $(\sigma^*g)$), hence $m>0$ and $\overline{D}$ is positive.

But now let's compute the intersection number of $C$ with $\sigma^{-1}(D)$. On the one hand, since the latter is principal, it is (linearly and geometrically) equivalent to $0$, so $(C\cdot\sigma^{-1}(D)) = (C\cdot0) = 0$. On the other hand,

$$\begin{align*}
0
&= (C\cdot\sigma^{-1}(D)) \\
&= m(C\cdot C) + (C\cdot\overline{D}) \\
&> m(C\cdot C)
\end{align*}$$

This implies the desired negativity.

The general case is quite similar. This time the total transform will be written as $\sigma^{-1}(D) = \sum_{i=1}^{n}{m_iC_i} + \overline{D}$ for some non-negative and not-all-zero integers $m_1,\cdots,m_n$, and $\overline{D}$ a positive divisor. Intersecting this total transform with each irreducible component $C_j$ looks as follows:

$$\begin{align*}
0
&= (C_j\cdot\sigma^{-1}(D)) \\
&= \sum_{i=1}^{n}{m_i(C_j\cdot C_i)} + (C_j\cdot\overline{D}) \\
&\geq \sum_{i=1}^{n}{m_i(C_j\cdot C_i)}
\end{align*}$$

and moreover this inequality must be strict for at least one $j$ (otherwise $\overline{D}$ wouldn't intersect the exceptional curve at all, which doesn't make sense). Note that for $i\neq j$ the divisors $C_i,C_j$ are just two curves, and by resolution of singularities we may assume they have at worst normal crossings. This means $(C_j\cdot C_i) \geq 0$. Therefore the self-intersection $(C_j\cdot C_j)$ cannot be positive.

We conclude that the intersection matrix $((C_i\cdot C_j))$ is non-negative off the diagonal, and "sufficiently non-positive" on the diagonal (sufficiently = enough to make the whole row sum to $\leq 0$). Such matrix is negative-definite, by the following linear-algebraic statement (which I won't prove here):

**Linear-algebraic proposition:** Have a matrix $B = (b_{ij})$ satisfying the following conditions:
1. The off-diagonal entries $b_{ij},i\neq j$ are non-negative.
2. Each $b_{jj}$ is sufficiently non-positive in the sense that $\sum_{i=1}^{n}{b_{ij}} \leq 0$.
3. $B$ is *not* congruent to a block-diagonal matrix.

Then $B$ is negative-semidefinite. If in condition 2 the inequality is strict for some $j$, then $B$ is negative-definite.

**Remark:** The third condition precisely corresponds to the connectedness of $C$.

This proposition also has a converse, that we will use later:
**Linear-algebraic converse:** Have a matrix $B = (b_{ij})$ satisfying condition 3. If $B$ is negative-semidefinite, then there are positive integers $m_1,\cdots,m_n$ such that, for each $j$,

$$\sum_{i=1}^{n}{m_i b_{ij}} \leq 0$$

and if $B$ is negative-definite, then we can make this inequality strict for some $j$.


### How to prove contractibility?
The main bulk of the proof is actually a more general result by Grauert, which gives an analytic criterion for contracting arbitrary subvarieties in arbitrary dimension. After discussing this result I will get back to the case of surfaces, and show how to re-express it in terms of the intersection matrix.

Let's begin with some hand-waving. Suppose you have a variety $X$ and a compact analytic subvariety $E \subseteq X$, and you want $E$ to be exceptional, i.e. be able to contract $E$ to a point. Our approach to the proof relies on two key facts:
- *Remment's proper mapping theorem* is a famous result in complex geometry, which says the direct image of an analytic subvariety through a *proper* map is again an analytic subvariety.
- If a *holomorphically separated* variety is compact, then I claim it must be finite & discrete. Recall that a variety is holomorphically separated if every two points $x,y$ can be distinguished by a holomorphic function $f$, i.e. $f(x)\neq f(y)$. On a compact variety all holomorphic functions are locally constant (essentially by the maximum principle), so my claim follows.

Combining these two facts allows us to plan the following route: find a proper map from the original variety to a holomorphically separated one, so for each (compact!) exceptional curve its image is a compact holomorphically separated subvariety -- thus must be a single point. It only remains to ensure that our map doesn't "collapse too much", e.g. it's not the constant map to a point. Seemingly, the idea I just described will contract *any* compact subvariety to a point. To fix that we will try to look only at a small neighborhood of the exceptional curve, small enough that this curve is itself the maximal compact subvariety (excluding individual points). This is where the next important notion comes in:
- In any *holomorphically convex* variety, there is a maximal compact nowhere-discrete subvariety.
So what we really want for our $E$ is to admit arbitrarily small holomorphically convex neighborhoods AKA a holomorphically convex neighborhood basis.

I'll wait a little more before giving the precise definition of holomorphic convexity. Until then I encourage you to think of it as a tiny tubular nighborhood of $E$ that doesn't deviate too much from $E$, and has roughly the same shape & thickness all throughout. Once we know how to contract $E$ within such tubular neighborhood, we could simply glue it back into the ambient variety.

The combination of holomorphic separatedness and holomorphic convexity is actually very well-studied; spaces satisfying both these criteria go under the name *Stein spaces*. They are central in complex geometry for various concrete and abstract reasons. From the perspective of algebraic geometry they are analogous to affine schemes, for instance, all their higher cohomologies vanish. We won't need all those fancy words.

Any holomorphically convex variety $X$ can be turned into a Stein space in a universal manner, i.e. there is a morphism $\varphi : X \to Y$ where $Y$ is Stein, and any other morphism to a Stein space factors uniquely through it. This morphism $\varphi$ is called the *Remment reduction* of $X$, and it satisfies some important properties:
1. $\varphi$ is proper (we need this to apply Remment's mapping theorem!).
2. $\varphi$ has nonempty connected fibers.
3. $\varphi_*\mathcal{O}_X \cong \mathcal{O}_Y$.
4. If it exists, the Remment reduction is unique up to unique isomorphism (as with any universal proeprty).
5. Remment reductions always exist. They have a very intuitive explicit construction, due to Cartan: define an equivalence relation on $X$ by "holomorphic indistinguishability", i.e. $x \sim y$ iff $f(x) = f(y)$ for any holomorphic $f$, and take $Y := X/\sim$. The hard part is to show that the quotient exists on the level of complex analytic spaces (not just topological spaces), and that it's proper.

Overall, we see that the Remment reduction contracts every compact connected subvariety to a point, and in particular if $E \subseteq X$ is the maximal compact nowhere-discrete subvariety, then $\varphi$ restricts to a biholomorphism from $X\setminus E$ to $Y\setminus \varphi(E)$. If our $E$ of interest is not the maximal such set, we shrink to a sufficiently small sub-neighborhood in which it *is* so. The conclusion is as follows:
**Theorem:** Let $X$ be a complex analytic variety and $E \subseteq X$ a complex analytic subvariety. Then $E$ is exceptional if and only if it has a holomorphically convex neighborhood basis.

### Notions of convexity
To apply this theorem we should know how to construct, or at least detect, holomorphically convex neighborhoods. Apparently convexity is a really big deal in the theory of several complex variables, so I'd like to spend some time discussing it in a general context.

You are probably familiar with *geometric convexity*: a subset $A \subseteq \mathbb{R}^n$ is called (geometrically) convex if, for two points $x,y\in A$ satisfy $[x,y] \subseteq A$. That is, the line segment between them is entirely contained in $A$. More generally, if for any subset contained in $A$, its convex hull is also contained in $A$.

There is a more function-y way to phrase this property: let $f$ be any *convex* function on $\mathbb{R}^n$ (its graph looks like a bowl). If $p \in [x,y]$ is a point on the line segment, then it must be "lower" than at least one of the endpoints, more specifically $f(p) \leq \max(f(x),f(y))$. Conversely, if $p$ is lower than at least one of the endpoints on (the graph of) any convex function, then it must lie on the line segment.

**Remark:** Personally I find it easier to think about the contrapositive: if $p$ is not on the line segment, then you can always find a convex function $f$ such that $f(p) > \max(f(x),f(y))$.

This discussion generalizes from line segments to any convex hulls, and we end up with:
**Lemma:** The convex hull of $K$ can be expressed by

$$\widehat{K} = \left\{p\,\middle|\,\forall f\text{ convex, } f(p) \leq \sup_{x \in K}{f(x)}\right\}$$

If we also require $K$ to be compact, then the supremum is guaranteed to exist. This new characterization of the convex hull is amenable to generalization.

**Definition:** Let $\mathcal{F}$ be a collection of real valued functions on $A$, and $K \subseteq A$ a compact subset. The *$\mathcal{F}$-hull* of $K$ is defined by

$$\widehat{K}_\mathcal{F} := \left\{p\,\middle|\,\forall f\in\mathcal{F}, f(p)\leq \sup_{x\in K}{f(x)}\right\}$$

I won't write the $\mathcal{F}$ in this notation when it's understood from context. Now $A$ is called *$\mathcal{F}$-convex* if, for every compact subset $K$ of $A$, its $\mathcal{F}$-hull $\widehat{K}$ is also a compact subset of $A$. In particular, we finally get the promised definition of *holomorphic convexity* by taking $A$ to be a complex domain and letting $\mathcal{F}$ be the collection of all functions of the form $\|f\|$ where $f$ is holomorphic on $A$.

Much of the interest in holomorphically convex domains stems from the *Cartan-Thullen theorem*, which states that a domain $A\subseteq\mathbb{C}^n$ is holomorphically convex if and only if it is a *domain of holomorphy*:
**Definition:** $A$ is called a *domain of holomorphy* if there are no open sets $U,V\subseteq\mathbb{C}^n$ satisfying both of the following conditions
1. $U\subseteq A$ and $U\subseteq V$, but $V\nsubseteq A$.
2. For any holomorphic function $f$ on $A$ there exists a holomorphic function $F$ on $V$ such that $f\|_U = F\|_U$.

You can also think of this more intuitively as: $A$ is *not* a domain of holomorphy if any function holomorphic on $A$ can be extended to some set outside of $A$. For instance in dimensions $n\geq 2$, Hartogs's theorem tells us that isolated singularities are always removable, i.e. every holomorphic function on $A\setminus\{a\}$ can be extended to $a$. Therefore such punctured domains are not domains of holomorphy.

In $\mathbb{C}$ every domain is a domain of holomorphy, since we can always architect a holomorphic function with a pole on some boundary point $a \in \partial A$ (just take $f(z) = \frac{1}{z-a}$; this could never be extended past $a$). So interest in domains of holomorphy, and by Cartan-Thullen's theorem, holomorphically convex domains, really only appears in several variables.

### How to construct convex domains?
Recall that Grauert's criterion was trying to give a "numerical" condition (positivity of the intersection matrix) to a curve being exceptional, but so far we only have a very "analytic" condition (existence of a holomorphically convex neighborhood basis). The crux of Grauert's proof is to give a better method for systematically constructing holomorphically convex neighrborhood basis.

The intuition is quite simple: suppose we start with some subset $E \subseteq \mathbb{R}^n$ and would like to construct for it a geometrically convex neighborhood basis. What we shall do is find a convex function $f$ defined on a neighborhood of $E$ such that $f\|\_E = 0$, and as our neighborhood basis take its sublevel-sets $U_\varepsilon = \\{f<\varepsilon\\}$.

We would like to have something analogous notion of convexity for functions of several complex variables. To gain some inspiration, recall that a $C^2$-differentiable function on $\mathbb{R}$ is:
- harmonic if $\Delta f = \frac{d^2 f}{dx^2} = 0$,
- convex if $\Delta f \geq 0$, and
- concave if $\Delta f \leq 0$.

**Remark:** Convexity on $\mathbb{R}$ can also be defined for non-$C^2$ functions, but then we wouldn't have the second derivative criterion. Similarly, the analogous notions defined below can be defined more generally for some functions with mild discontinuities, but I will only focus on the $C^2$ case.

**Definition:** A $C^2$ function $f$ on an open domain $A \subseteq \mathbb{C}$ is called *subharmonic* if $\Delta f \geq 0$. A $C^2$ function on an open domain $A \subseteq \mathbb{C}^n$ is called *plurisubharmonic* if its restriction to every $1$-dimensional affine subspace of $\mathbb{C}$ is subharmonic.

It is not too hard to provide a second derivative criterion for plurisubharmonic functions, we just have to find a nice complex-analytic analogue of second derivatives. The answer turns out to be: $f$ is plurisubharmonic if and only if the complex Hessian matrix $\bar\partial \partial f = \left(\frac{\partial^2 f}{\bar\partial x_i \partial x_j}\right)_{i,j}$ is positive-semidefinite. We also say $f$ is *strictly pseudoconvex* if the Hessian matrix is positive-definite (not semi!).

Now we can give an analogous notion of convexity via sublevel-sets of plurisubharmonic functions.
**Definition:** A domain $A\subseteq\mathbb{C}^n$ is called *(strictly) pseudoconvex* if there exists an open set $U \supseteq \partial A$ and a (strictly) plurisubharmonic function $f$ on $U$ such that $A\cap U = \\{f<0\\}$.

**Example:** The function $\Vert x\Vert^2$ is plurisubharmonic on $\mathbb{C}^n$. By translating this up or down, we see that open balls are pseudoconvex. In particular we get a pseudoconvex neighborhood basis of the origin.

We've seen that exceptional subvarieties admit a holomorphically convex neighborhood basis. Now we also see that they admit a pseudoconvex neighborhood basis: in local coordinates, consider $E$ contracted to the origin, and then pull back the function from the example. Constructing a pseudoconvex neighborhood basis is much easier though, because you just need to write down an appropriate plurisubharmonic function defined near $E$. This begs the question:

> Does pseudoconvexity imply holomorphic convexity?

This question, known as the *Levi problem*, is one of the deepest results in complex analysis of several variables. Its proof is difficult, and uses some nice methods from functional analysis, but I might have to dedicate a separate blogpost to discuss it in detail. I will just say that the converse implication, holomorphic convexity implies pseudoconvexity, is a lot easier, and so all our notions of convexity (including being a domain of holomorphy) are equivalent.

The final version of our general theorem is
**Theorem:** Let $X$ be a complex analytic variety and $E \subseteq X$ a complex analytic subvariety. Then $E$ is exceptional if and only if it has a pseudoconvex neighborhood basis.

### From line bundles to plurisubharmonic functions
To find pseudoconvex neighborhood bases we need a reliable source of plurisubharmonic functions defined on a neighborhood of a curve.

<!-- I think the main idea is that negative line bundles admit negative metrics, and taking log of those gives plurisubharmonic functions? -->


### Back to surfaces
Finally let's go back to the special case where $X$ is a surface and $E$ is a curve embedded in it. For convenience I copy-and-paste the goal
**Theorem (Grauert):** Let $X$ be a surface. Let $C \subseteq X$ be a compact & connected curve, and $C_1,\cdots,C_n$ its irreducible components. Then $C$ is exceptional if and only if the intersection matrix $((C_i\cdot C_j))$ is negative-definite.

Grauert's criterion actually works for arbitrary curves, but we can make some reductions: by resolution of singularities of curves on surfaces, we can perform some blow-ups to ensure $C$ is a normal crossing divisor. In the proof we will have some condition involving the existence of a line bundle, and one can show that this existence is preserved under blow-ups. All that is to say, let's assume without loss of generality that $C$ has normal crossings.

Since the intersection matrix is negative-definite, by the linear-algebraic proposition from before we can choose positive integers $m_1,\cdots,m_n$ such that

$$\sum_{i=1}^{n}{m_i(C_i\cdot C_j)} \leq 0$$

for all $j$, and strictly for some $j$. Another way to say this is, if we denote $D := \sum_{i=1}^{n}{m_i C_i}$, then $(C_j\cdot D) \leq 0$ for all $j$. Re-interpreting $D$ as a line bundle $\mathscr{L}$, we can say that $\mathscr{L}|_{C_j}$ is negative for each $j$.

This assumption allows us to take an open cover of $X$ by polydiscs $\\{P_\alpha\\}$ such that, in the local coordinates of each polydisc, $C$ is either just the $x$-axis, or the union of the $x$-axis and $y$-axis.