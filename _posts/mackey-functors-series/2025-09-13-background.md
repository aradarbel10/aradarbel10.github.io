---
layout: post
title: Mackey functors in (naïve) equivariant homotopy theory
subtitle: "Part 0: Background & motivating question"
is_hidden: true
---

Some time ago I became interested in the *Nishida nilpotence theorem*, the historical predecessor of the Devinatz-Hopkins-Smith nilpotence theorem lying at the heart of chromatic homotopy theory. Specifically, I've been studying the approach of May et al via a general framework of $\mathbb{H}\_\infty$-ring spectra. May's treatment appears in the book "*$\mathbb{H}\_\infty$ Ring Spectra and their Applications*", and it's very nice and systematic, but in my opinion leaves a taste for more. Many of the statements and proofs are highly unsatisfying (to me) on an intuitive level, so it took a bit of effort to decipher what May probably had in mind when he was writing them. During this process I came up with an interesting question, leading to an even more interesting answer, and that's what this current post is about. For completeness, I begin with some background on May's proof. The full details might deserve their own blogpost so for now allow me to just sketch the general idea.

Given a spectrum $E$, we define its *$j$th extended power* as $D\_jE := (E^{\otimes j})\_{h\mathfrak{S}\_j}$. Here $\mathfrak{S}\_j$ denotes the symmetric group of permutations on $j$ elements. This acts on the tensor power $E^{\otimes j}$ simply by permuting the factors, and $(-)\_{h\mathfrak{S}\_j}$ denotes the (homotopy) quotient of this action. Roughly speaking, we may think of "elements" of $D_jE$ as unordered collections of $j$ "elements" from $E$. In particular if we have a commutative multiplication map $E^{\otimes 2} \to E$ with sufficiently coherent multiplicative structure (higher commutators & associators), we expect it to extend to $j$-ary multiplication maps $D_jE \to E$ satisfying some mundane compatibilities with each other.

Of course, in practice not every ring spectrum can be furnished with such structure. An $\mathbb{H}_\infty$-ring spectrum is precisely one equipped with all such $j$-ary multiplication maps, satisfying all their compatibilities. Fortunately many familiar spectra (the sphere spectrum, Eilenberg-MacLane spectra, topological K-theory, Thom spectra) indeed possess this structure or certain variants of it. In this situation we are able to construct *power operations* in $E$-cohomology. These are "external" operations $\mathcal{P}_j$ defined as follows: consider a cohomology class $h \in E^n(Y)$, represented by $h : \Sigma^{-n}Y \to E$, we take $\mathcal{P}_j(h) \in E^n(\Sigma^nD_j\Sigma^{-n}Y)$ represented simply by the composite

$$D_j\Sigma^{-n}Y \xrightarrow{D_j(h)} D_jE \xrightarrow{\qquad} E$$

We aim to understand how such power operations interact with the additive structure. First, recall the classical *multinomial theorem*:

$$(h_1+\cdots+h_k)^j = \sum_{J}{\binom{j}{J} h^J}$$

Here $J$ ranges over all partitions of $j$ of size $k$, the symbol $\binom{j}{J} = \binom{j}{j_1,\cdots,j_k} = \frac
{j!}{j_1!\cdots j_k!}$ is the multinomial coefficient, and $h^J = h_1^{j_1}\cdots h_k^{j_k}$ is exponentiation in multiindex notation.

As their name and definition suggest, we expect power operations $\mathcal{P}^j$ to behave similarly to the operations $(-)^j$. It turns out that there is indeed a similar-looking formula, which in the universal case looks like this:

$$D_j(h_1+\cdots+h_k) = \sum_J{(\alpha_J\circ\tau_J)^* D_J(h)}$$

where again $J$ ranges over partitions. This time we use the notation $D_J(h) = D_{j_1}(h_1)\otimes\cdots\otimes D_{j_k}(h_k)$ analogous to multiindex exponentiation. Lastly I should explain what are the two maps $\alpha_J$ and $\tau_J$.

The former is easy: $\alpha_J : D_{j_1}Y\otimes\cdots\otimes D_{j_k}Y \to D_jY$ is conceptually just concatenation of unordered collections. The latter map $\tau_J : D_jY \to D_{j_1}Y\otimes\cdots\otimes D_{j_k}Y$ is known as a *transfer*, which is a bit more intricate. By analogy to tensor products in classical algebra, we shouldn't think of elements in $D_jY$ as unordered collections, but rather as *formal linear combinations* of unordered collections. The transfer map then sends any unordered collection to the sum of all possible ways to partition it according to $J$. For instance if $J = (2,2)$ then $\tau_J : D_4Y \to D_2Y\otimes D_2Y$ acts heuristically by the rule:

$$\begin{align*}
\tau_J(\{h_1,h_2,h_3,h_4\})
&= \{h_1,h_2\}\otimes\{h_3,h_4\} + \{h_1,h_3\}\otimes\{h_2,h_4\} + \{h_1,h_4\}\otimes\{h_2,h_3\} \\
&+ \{h_2,h_3\}\otimes\{h_1,h_4\} + \{h_2,h_4\}\otimes\{h_1,h_3\} + \{h_3,h_4\}\otimes\{h_1,h_2\}
\end{align*}$$

Observe that the number of summands in the result is $\binom{4}{2,2} = 6$. Overall the composite $\alpha_J\circ\tau_J : D_jY \to D_jY$ takes an unordered collection, sends it to the sum of all possible ways to partition it as $J$, and then re-concatenates each possibility, so conceptually we expect to get a bunch of copies of the original thing we started from.

You may have encountered various other transfer maps in classical algebra (representation theory, group co/homology, etc), defined exactly as I just sketched. I shall remind how they are defined in group homology (which is a special case of our homotopy quotient construction $(-)_{h\mathfrak{S}_j}$). There, these maps are also known as *corestrictions*. If $G$ is a finite group acting linearly on a vector space $V$, we write $V_G$ for the quotient by this action. If furthermore $H \leq G$ is a subgroup, there is an obvious map $\alpha_H^G : V_H \to V_G$ given by identity on representatives, along with a slightly less obvious map $\tau_H^G : V_G \to V_H$ given by

$$\tau_H^G(v) = \sum_{g \in G/H}{g\cdot v}$$

Here $g$ ranges over all (finitely many) cosets of $H$ in $G$. Note that if we let $G$ act on the vector $v$ it will, in effect, permute the sum. Since addition is commutative-associative, this is equal to the original sum, and so we clearly see that $\alpha_H^G\circ\tau_H^G$ is just multiplication by the number of terms in the sum, which is the index $\|G/H\| = [G:H]$.

**Intuition:** It might be easier to imagine the case where $V$ is just a set with $G$-action. Then $V$ is partitioned into $G$-orbits, and each $G$-orbit is partitioned further into $H$-orbits. An element of $V\_G$ is a $G$-orbit, and it is sent to the formal sum of all its constituent $H$-orbits. Then each $H$-orbit is sent back to the $G$-orbit that contains it.

In the particular case $G = \mathfrak{S}\_j$, subgroups correspond (up to conjugacy) to partitions $J$: specifically, to each $J$ we associate the subgroup $\mathfrak{S}\_J := \mathfrak{S}\_{j\_1}\times\cdots\times\mathfrak{S}_{j_k}$, and the index of this subgroup is the multinomial coefficient $\binom{j}{J}$.

This is very nice for vector spaces, or abelian group, or many more classical algebraic structures, however for spectra this *"elementary"* proof (that is, proof by manipulating elements) won't cut. In fact it's not even so clear how to define the transfer map at all. But let's leave this for later. The point is:

<h4 style="text-align: center; font-style:italic"> We can sort of think of $\alpha_J\circ\tau_J$ as multiplication by $\binom{j}{J}$. Huzzah! </h4>

and then our additivity formula for power operations is completely analogous to the multinomial theorem (I had to insert the word *'huzzah'* to avoid an accidental factorial).

May in his proof then goes on to specializing the above addition formula to more and more intricate relations, which eventually boil down to something of the form: if $h \in \pi_*\mathbb{S}$ is $p^m$-torsion i.e. $p^m h = 0$, then there exists a sufficiently large $s$ such that $h^{p^s}$ is $p^{m-1}$-torsion. Applying this step repeatedly shows that all prime-power-torsion in the stable stem is nilpotent. By Serre's finiteness theorem this implies everything in positive degree is nilpotent. But this is not what I'm here to write about.

One of May's central results along the way is that $\alpha_J\circ\tau_J$ indeed induces multiplication by $\binom{j}{J}$ *on ordinary homology theories*. His proof of this fact is arguably quite sketchy, relying on chain-level arguments and skipping a few details. It also begs the question: what excatly goes wrong for *extra*ordinary homology theories? Does the theorem actually hold in general, perhaps via a harder proof? And if not, how would one go about producing counterexamples? In the rest of this blogpost series I intend to resolve this question in a manner which to me feels very satisfying, by introducing a much more general theory of transfer maps on spectra.


- Next [Part 1: Where do transfers come from?]({% post_url /mackey-functors-series/2025-09-14-transfers %})