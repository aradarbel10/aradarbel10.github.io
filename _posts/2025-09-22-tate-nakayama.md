---
layout: post
title: The Tate-Nakayama theorem
subtitle: Taking the scenic route
---

Nowadays the most common approach to proving class-field theory, and in particular for constructing the Artin reciprocity map, is via Galois cohomology. This roughly consists of two steps:
1. Define the notion of "class formations", and prove Tate's theorem for them.
2. Prove that your objects of interest satisfy all the axioms of a class formation, by explicit computations.

The object of this post is to explain the first step. I will begin by stating Tate's theorem. Recall that $\hat H^\*$ denotes the *Tate cohomology groups*, which are obtained by patching together group homology and cohomology.

**Theorem (Tate):** Let $G$ be a finite group and $A$ a $G$-module. Suppose there exists an element $u \in \hat H^2(G,A)$ such that for every subgroup $H\leq G$,
- $\hat H^1(H,A) = 0$.
- $\hat H^2(H,A)$ is a cyclic group of order $\|H\|$, in which $\mathrm{res}_{G/H}(u)$ is a generator.

Then taking cup products with $u$ induces isomorphisms

$$u\cup- : \hat H^*(G,\mathbb{Z}) \xrightarrow{\qquad\sim\qquad} \hat H^{*+2}(G,A)$$

Without getting into too much detail, a *class formation* is essentially just a $G$-module satisfying the assumptions of Tate's theorem. For purposes of class-field theory this needs to be generalized to infinite and pro-finite groups, but that's beyond my scope for today.

I think it's fair to say that Tate's theorem looks pretty ugly at first sight. My goal is to show you how, with a little detour to deeper theory, Tate's theorem actually falls out quite naturally. Namely we will explore how to detect vanishing of cohomology via local criteria -- 'local' here meaning at each prime. Then we will see that checking vanishing locally is surprisingly easy.

**References:** I will mainly be following Atiyah-Wall's chapter on group cohomology from Cassels-Frolich, in particular sections 9 and 10 of their chapter. Serre's book on local fields is another fantastic resource where I originally learned a lot of group co/homology from. Lastly, Koya has a cute paper titled *A Generalization of Tate-Nakayama Theorem by Using Hypercohomology*, that the more advanced readers would surely enjoy. Be warned that some of my statements and proofs may deviate from these.

### Working prime-locally
We are interested in studying vanishing results by working one prime at a time. Vanishing is best understood in the following sense:

**Definition:** A $G$-module $A$ is *cohomologically trivial* if $\hat H^q(H,\mathrm{Res}^G_HA)=0$ for all integers $q$ and all subgroups $H\leq G$.

**Example:** It should be easy to verify that induced modules (obtained by induction from plain abelian groups, without any action) are cohomologically trivial.

The starting point is the following basic fact: if $G$ is a finite group, then restriction to the trivial group followed transfer back to $G$ induces on Tate cohomology multiplication by $\|G\|$ (I'm currently writing another series of posts on the analogous phenomenon in higher algebra, though it might take some time to finish). At the same time this must induce zero, since we're passing through the trivial group. Therefore the order of the group annihilates its cohomologies. Namely if $G$ is a $p$-group, i.e. its order is a power of $p$, then all its cohomology is $p$-power-torsion.

Now if $G$ is an arbitrary finite group, let $G_p$ be a choice of $p$-Sylow subgroup for each $p$. From the above, the restriction $\hat H^\*(G,A) \xrightarrow{\mathrm{res}} \hat H^\*(G\_p,\operatorname{Res}^G\_{G\_p}A)$ must kill all the non-$p$-power-torsion. Moreover if we restrict only to the $p$-power-torsion parts, then the restriction-transfer composite

$$\hat H^*(G,A) \xrightarrow{\mathrm{res}} \hat H^*(G_p,\operatorname{Res}^G_{G_p}A) \xrightarrow{\mathrm{tr}} \hat H^*(G,A)$$

is an isomorphism (it's multiplication by the index $\|G/G\_p\|$ which is coprime to $p$, hence invertible in $\mathbb{Z}\_p$). Consequently, restriction must be injective on the $p$-power-torsion.

**Corollary:** If $\hat H^\*(G\_p,\operatorname{Res}^G\_{G\_p}A)=0$ for all $p$ then $\hat H^\*(G,A)=0$.

**Corollary:** $A$ is cohomologically trivial iff $\operatorname{Res}^G\_{G\_p}A$ is cohomologically trivial for all $p$.

### Group co/homology over finite fields
Just for fun, let's recall Maschke's theorem from representation theory of finite groups:
**Theorem (Maschke):** If $k$ is a field and $G$ a finite group whose order is divisible in $k$ (that is, $\|G\|$ is not divisible by $p = \operatorname{char} k$), then every $k[G]$-module is semisimple -- a sum of irreducibles.

The proof is based on an averaging method, which of course requires being able to divide by the group's order. Using Maschke's theorem we can easily figure out $V^G$ and $V\_G$ for any given $k[G]$-module $V$; the trivial summands are preserved, and the nontrivial summands are killed.

The case where $\|G\|$ is not invertible in the ground field falls under the subject of *modular representation theory*, which is more intricate. Compared to the above, something strange happens: let $G$ be a finite $p$-group and $A$ a finitely generated $\mathbb{F}_p[G]$-module (finite generation can be easily avoided)

**Proposition:** $A=0$ iff $A^G=0$.

**Proof:** Certainly if $A=0$ then $A^G = 0$. Conversely, suppose $A\neq 0$. $A$ is a finite dimensional $\mathbb{F}_p$-vector space and hence has $p^d$ elements for some $d>0$. By the class equation, $\|A^G\|$ is either zero or $\geq p$, but a vector space can't have cardinality zero, so it's $\geq p$. Therefore $A^G \neq 0$. $\square$.

**Corollary:** Under the same assumptions, $A=0$ iff $A\_G=0$. Indeed, since we're working over a field, $A^G$ and $A\_G$ are dual, so one is zero iff the other is.

**Corollary:** If $\varphi\_G : A\_G \to B\_G$ is an isomorphism and $H\_1(G,B)=0$ then $\varphi : A \to B$ is an isomorphism. Indeed, right exactness gives $(\operatorname{coker}\varphi)\_G = \operatorname{coker}(\varphi\_G) = 0$ so by the previous corollary $\operatorname{coker}\varphi = 0$, which is surjectivity. Injectivity follows from the long exact sequence.

So in this $p$-local situation, we can detect vanishing of $A$, and thus all of its co/homology, by only looking at its $0$th co/homology, and for isomorphism-ness we only have to look at $0$th and $1$st homologies. All the following results will be of a similar ilk: over $\mathbb{F}_p$, if co/homology vanishes even just a little bit, then it must vanish completely.

**Proposition:** If $H\_1(G,A) = 0$ then $A$ is a free $\mathbb{F}\_p[G]$-module, hence induced, so in particular cohomologically trivial.

**Proof:** $A\_G$ is an $\mathbb{F}_p$-vector space, so has a basis. This lifts to a set of generators of $A$ as an $\mathbb{F}\_p[G]$-module, so gives a surjection $\varphi : F \to A$ where $F$ is free. By assumption, the long exact sequence in homology reduces to a short exact sequence of coinvariants:

$$0 \xrightarrow{\qquad} K_G \xrightarrow{\qquad} F_G \xrightarrow{\qquad} A_G \xrightarrow{\qquad} 0$$

But we specifically chose $F$ in such a way that $\varphi\_G$ bijects bases, and so it's an isomorphism. By the previous corollary $\varphi$ itself must be an isomorphism, meaning $A$ is free. $\square$

### Tate cohomology over finite fields
From the previous proposition, we deduce (under the same assumptions as the previous section):

**Corollary:** If $\hat H^q(G,A)=0$ for some $q$ then $A$ is a free $\mathbb{F}_p[G]$-module, hence induced, thus cohomologically trivial. This follows by dimension-shifting $A$ as to turn the $q$th Tate cohomology into $(-2)$th Tate cohomology, which is the same as $1$st homology.

Next we will give a sort of morphism-version of this corollary, like we had for the vanishing of coinvariants, but specifically for the multiplication-by-$p$ morphism. We still assume $G$ is a finite $p$-group, but now suppose $A$ is $p$-torsionfree (as an abelian group). This is like saying $\operatorname{Tor}^{\mathbb{Z}}\_1(A,\mathbb{F}_p)$.

**Proposition:** If $\hat H^q(G,A)=0$ for some two consecutive indices then $A$ is cohomologically trivial.

**Proof:** The gist is to apply the previous corollary on the "derived cokernel" $A/p \approx A \otimes_{\mathbb{Z}}^L \mathbb{F}_p$. The short exact sequence $0 \to \mathbb{Z} \xrightarrow{p} \mathbb{Z} \to \mathbb{F}_p \to 0$ induces a long exact sequence on $\operatorname{Tor}$'s which, by the $p$-torsionfree-ness assumption, reduces to a short exact sequence $0 \to A \xrightarrow{p} A \to A/p \to 0$. This now gives a long exact sequence in Tate cohomology:

$$\cdots \xrightarrow{\qquad} \hat H^q(G,A) \xrightarrow{\qquad} \hat H^q(G,A/p) \xrightarrow{\qquad} \hat H^{q+1}(G,A) \xrightarrow{\qquad} \cdots$$

Our assumption says that for some $q$, the middle object is sandwiched between two $0$'s, hence it itself must be $0$. By the corollary then $A/p$ has trivial Tate cohomology in all degrees, so multiplication-by-$p$ on $A$ induces an isomorphism through all Tate cohomologies. In contrast, since $G$ is a $p$-group, all Tate cohomologies are also annihilated by some uniform power of $p$.

This is a very restrictive situation: on the one hand, multiplication by some power of $p$ should kill everything, while on the other hand it should be an isomorphism. Therefore the Tate cohomologies must themselves be $0$'s. $\square$.

**Remark:** If $A$, still $p$-torsionfree, is cohomologically trivial, then combining the last corollary and proposition shows that $A/p$ is free over $\mathbb{F}_p[G]$.

### Vanishing results in general
From now on, let $G$ be an arbitrary finite group. In the case of a $p$-group we've seen that a $p$-torsionfree module is cohomologically trivial iff its Tate cohomology vanishes in some two consecutive degrees. To get something analogous for general $G$, we should look at torsionfree modules ($p$-torsionfree at every $p$).

**Corollary:** If $G$ is a finite group and $A$ a torsionfree $G$-module, then $A$ is cohomologically trivial iff for each prime $p$ the Tate cohomology $\hat H^\*(G\_p,\operatorname{Res}^G\_{G\_p}A)$ vanishes in some two consecutive degrees.

With a little creativity we can drop the torsionfree-ness assumption and extract the following result, which already looks quite close to the usual statement of Tate-Nakayama:

**Proposition (twin number criterion):** If $G$ is a finite group and $A$ is a $G$-module, then $A$ is cohomologically trivial iff for each prime $p$ the Tate cohomology $\hat H^\*(G\_p,\operatorname{Res}^G\_{G\_p}A)$ vanishes in some two consecutive degrees.

**Proof:** For arbitrary $A$ let $\varphi : F \to A$ be a surjection from a free $\mathbb{Z}[G]$-module, and $K$ its kernel. $F$ is also free over $\mathbb{Z}$, hence it's torsionfree, and $K$ being a subgroup of a torsionfree group is itself torsionfree. The free module $F$ is clearly cohomologically trivial, so by the long exact sequence $A$ and $K$ have the same Tate cohomology up to a shift in indices. This shows that $K$ also satisfies the twin number assumption, but unlike $A$, $K$ is torsionfree, and the previous corollary applies to yield that $K$ is cohomologically trivial. Now $A$ must also be cohomologically trivial, again by the long exact sequence. $\square$


The last general result we will see, before starting to specialize towards Tate's theorem, is the following morphism-verion of the above criterion.

**Proposition (triplet number criterion):** Let $G$ be a finite group, $A,B$ be $G$-modules, and $\varphi:A\to B$ some morphism between them. Then $\varphi$ induces an isomorphism on Tate cohomologies iff for each prime $p$ there exists some integer $q$ such that the homomorphism $\operatorname{Res}^G\_{G\_p}\varphi : \hat H^{q-1}(G\_p,\operatorname{Res}^G\_{G\_p}A) \to \hat H^{q-1}(G\_p,\operatorname{Res}^G\_{G\_p}B)$ is
- surjective at $q-1$,
- an isomorphism at $q$, and
- injective at $q+1$.

**Proof:** Form the "mapping cone" or "homotopy cofiber" of $\varphi$ in the derived category -- this completes it to an exact triangle. Looking at the resulting long exact sequence, our assumptions on $\varphi$ are precisely equivalent to saying that its cofiber satisfies the twin number criterion, so it must be cohomologically trivial. Again the long exact sequence yields that $\varphi$ is actually an isomorphism in all degrees. $\square$

Note that when I say $\varphi$ induces an isomorphism on Tate cohomologies I really mean this in the sense of cohomological triviality: it's not only an isomorphism on the cohomologies of $G$, but also of any subgroup of $G$.

**Remark:** I'm being a bit cheeky here, because I'm applying the previous results on an object in the derived category, i.e. some chain complex of $G$-modules. You may verify for yourself that everything still goes through pretty much as-is, or consult Koya's paper mentioned in the introduction.


### Tate-Nakayama-style consequences
It is time to specialize the general developments performed until now. The first specialization is to look not at some arbitrary $\varphi$, but specifically at morphisms induced by a cup product.

We take $G$ to be a finite group and $A\otimes B\to C$ some bilinear pairing of $G$-modules, with respect to which all cup products shall be taken.

**Corollary (Tate-Nakayama):** Have a cohomology class $u \in \hat H^q(G,A)$. If for each prime $p$, the cup product $\mathrm{res}^G\_{G\_p}u \cup -$ satisfies the triplet number criterion, then cupping with $\mathrm{res}^G\_Hu$ induces an isomorphism for all subgroups $H\leq G$

$$\hat H^*(H,B) \xrightarrow{\quad\sim\quad} \hat H^{*+q}(H,C)$$

The precise proof of this corollary depends on your framework: working with plain $G$-modules, you have to use some annoying dimension shifting arguments. But if you are willing to trust that everything works for chain complexes of $G$-modules this is not super necessary.

We finally reach Tate's theorem. I remind its statement (like before, I'm only stating this with $G$ for simplicity, but it really works for any subgroup too):

**Theorem (Tate):** Let $G$ be a finite group and $A$ a $G$-module. Suppose there exists an element $u \in \hat H^2(G,A)$ such that for every subgroup $H\leq G$,
- $\hat H^1(H,A) = 0$.
- $\hat H^2(H,A)$ is a cyclic group of order $\|H\|$, in which $\mathrm{res}_{G/H}(u)$ is a generator.

Then taking cup products with $u$ induces isomorphisms

$$u\cup- : \hat H^*(G,\mathbb{Z}) \xrightarrow{\qquad\sim\qquad} \hat H^{*+2}(G,A)$$

The proof is now easy:

**Proof:** For any module $A$ we have a pairing $\mathbb{Z}\otimes A \to A$. Consider cupping the class $u$ given in the theorem, which lives in degree $2$. We use the triplet number criterion for indices $(-1,0,1)$:
- In degree $-1$, we need surjectivity of $\hat H^{-1}(G\_p,\mathbb{Z}) \to \hat H^1(G\_p,A)$. This is clear as the codomain is $0$.
- In degree $1$, we need injectivity of $\hat H^1(G\_p,\mathbb{Z}) \to \hat H^3(G\_p,A)$. Since $\mathbb{Z}$ is taken with the trivial action, the domain is $0$, and injectivity is trivial.
- In degree $0$, we need $\hat H^0(G\_p,\mathbb{Z}) \to \hat H^2(G\_p,A)$ to be an isomorphism. The domain is the cokernel of the norm map on $\mathbb{Z}$, which is multiplication by the order of $G\_p$, so it's a cyclic group of order $\|G\_p\|$. The codomain is identical, by assumption. $\square$

### Outlook
Tate's theorem followed easily from the local criteria developed above, but still it may not seem so motivated. As unintuitive as number theory may be, here is my attempt at explaining *why* we expect this to work:

One perspective is from explicit computations, of cohomology of units for local fields, and of idéles ("local units") for global number fields. In those computations you find that the first cohomology indeed does vanish, while the second cohomology is cyclic given by the "Brauer invariants" map. So Tate's theorem just encodes a mysterious pattern which arises in practice.

Perhaps another way to understand this is by identifying Galois cohomology with étale cohomology. From this cohomological perspective, finite fields behave like "1-dimensional things" -- their étale fundamental group (absolute Galois group) is (pro-)cyclic, like that of a topological circle. Then local fields behave like "2-dimensional gadgets", so you might wonder whether they satisfy a form of Poincaré duality between $\hat H^\*$ and $\hat H^{2-\*}$. This is realized formally by the so-called "Tate-Nakayama duality" or "local Tate duality", and it's essentially equivalent to class-field theory. For the global case, you may think of idéles as "a bunch of 2-dimensional gadgets patched-up together" and again you get a similar duality, known as "Poiteu-Tate duality" or "global Tate duality". In fact you may even try to consider global fields themselves as sort of "3-dimensional gadgets", and thus obtain a duality between $\hat H^\*$ and $\hat H^{3-\*}$ -- this is *Artin-Verdier duality*.

Observe that these dualities, in analogy with topological Poincaré duality, are given by cupping with a "fundamental class" which generates the top-dimensional cohomology.

A final perspective of my own, which is much more speculative and not at all rigorous, is by making tighter analogies to algebraic topology: a field in algebraic geometry is meant to behave like a point, but fields can still have interesting Galois groups / étale fundamental groups. So fields are better thought of as "points with automorphisms" or perhaps "stacky quotients" of the form $k \approx [pt/\mathrm{Gal}(\overline{k}/k)]$. In the context of homotopy theory, the (homotopy) quotient of a point by a group action is precisely the classifying space $BG$. This even makes sense cohomologically: the ordinary co/homology of $BG$ coincides with the group co/homology of $G$, in the same way that étale co/homology of a field coincides with the group co/homology of its absolute Galois group.

From this perspective it should also not be so surprising that first homology gives the abelianization of the fundamental group.

The above story might also lead you to another natural question: when does a finite group have periodic cohomology? Finite cyclic groups have $2$-periodic cohomology, where the periodicity is given by the same $2$-dimensional fundamental classes discussed earlier. This turns out to be closely related to another question: which finite groups can act freely on spheres? I might write a separate post about this in the future.