---
layout: post
title: Mackey functors in (naïve) equivariant homotopy theory
subtitle: "Part 1: Where do transfers come from?"
is_hidden: true
---

Last time we've seen how transfers can be defined explicitly in ordinary algebra, where the core idea was being able to sum over the (finite) set of cosets $G/H$. Abstractly, let $\mathcal{C}$ be a semiadditive category, i.e. a category which admits all finite products & coproducts, and such that they coincide. The standard example to keep in mind is the category $\mathbf{Ab}$ of abelian groups (more generally, any abelian category) where finite direct sums are both the products and coproducts.

This structure allows us to take sums of finite families of morphisms: if $I$ is a finite set and $\phi_i$ an $I$-indexed family of morphisms in $\operatorname{Hom}(X,Y)$, then we can form their sum as follows:

$$\sum_{i\in I}{\phi_i} : X \xrightarrow{\Delta} \prod_I{X} \xrightarrow{(\phi_i)} \prod_I{Y} \xrightarrow{\cong} \coprod_I{Y} \xrightarrow{\nabla} Y$$

where $\Delta$ is the "constant tuple map" and $\nabla$ is the "fold map" which sends every copy of $Y$ to $Y$ itself. This defines a summation homomorphism $\sum_I : \prod_I{\operatorname{Hom}(X,Y)} \to \operatorname{Hom}(X,Y)$.

For convenience, we may slightly generalize this by making the whole thing "relative". Namely let $f:I\to J$ be a map whose fibers (preimages of each element of $J$) are all finite. Then we'd like to be able to "sum along fibers", so given an $I$-indexed family $(\phi_i)$ we can obtain a $J$-indexed family $(\psi_j)$ where $\psi_j = \sum_{i\in f^{-1}(j)}{\phi_i}$.

In the $\infty$-categorical context, such summations fit into a the more general story of *ambidexterity* and *higher semiadditivity*, which I'd like to very briefly describe. Rather than just summing over finite sets we can actually try "integrating" over $\infty$-groupoids (aka *Kan complexes*, aka *spaces*) or analogously, integrating along fibers, under appropriate finiteness assumption. Specifically:

**Definition:** An $\infty$-groupoid $I$ is called *$m$-finite* if it is $m$-truncated and its homotopy groups are finitely generated (including $\pi_0$ is a finite set). Recall that being $m$-truncated means your homotopy groups are trivial in degree $>m$. A functor of $\infty$-groupoids $I \to J$ is called *$m$-finite* if its homotopy fibers are $m$-finite.

Now let's work through what it means to be $m$-finite for each $m$, and see how those integrations arise.

**Case -2:** By convention, $I$ is called "$(-2)$-finite" iff it is contractible, so it's essentially just a single-point space. In any category, we can always sum over a single-point: a family indexed by a single-point is just a single map, and the "singleton sum" of this single map is again that same map.

In the relative case, $I \to J$ is $(-2)$-finite iff all its fibers are contractible, which means it's an equivalence. Again we always send any given map to itself.

**Case -1:** $I$ is $(-1)$-finite iff it's simply connected, so either contractible or empty. We already covered the contractible case. In the empty case, we need to be able to have "empty sums" which are typically expected to be zero. Of course in general there is no good notion of "zero maps". But suppose your category $\mathcal{C}$ is *pointed*, which means it has an initial object $0$ and a final object $1$, and the unique map $0 \to 1$ is an isomorphism. For instance, the category of pointed sets is pointed, and the category of unital monoids is pointed.  

In a pointed category, we can form between any two objects a "zero map":

$$X \xrightarrow{\exists!} 1 \xrightarrow{\cong} 0 \xrightarrow{\exists!} Y$$

and this is thought of as the "empty sum" that we needed. In the relative case, $f : I \to J$ is $(-1)$-finite iff its fibers are either empty or contractible, so it may be thought of as a subset inclusion. The "integration along fibers" of a subset takes some family of functions indexed by the small set $I$, and extends it to a family on the larger set $J$ by adding zero maps to all the missing indices. Notice that we don't need all our morphisms to be between the same objects; given any $J$-indexed families of objects $X = (X\_j)\_{j\in J}$ and $Y = (Y\_j)\_{j\in J}$, we obtain a map

$$\int_f : \operatorname{Map}_{\mathcal{C}^I}(X|_I,Y|_I) \xrightarrow{\qquad\qquad} \operatorname{Map}_{\mathcal{C}^J}(X,Y)$$

Here's a boring observation that might hint at how the next steps will proceed: the initial object $0$ is the *colimit* over the empty diagram, while the terminal object $1$ is the *limit* over the empty diagram. Under this perspective, the zero map is defined quite similarly to the summation map from earlier, since it relies on having a way to go from a limit (product) to a colimit (coproduct) -- the wrong direction from how such morphisms typically go!

**Case 0:** $I$ is $0$-truncated iff it's discrete, i.e. equivalent to a set. It is then $0$-finite if it's equivalent to a finite set. In this case we can define integration over finite sets just like before, just in a somewhat fancier language.

Suppose still that our category is pointed. Then, analogously to the initial-to-terminal map $0 \to 1$, I shall construct a coproducts-to-products map

$$\mathrm{Nm}_I : \coprod_I{X} \to \prod_I{X}$$

whose name "norm" will be clarified later.

Recall that defining a map out of a coproduct amounts to defining a map out of each summand, and defining a map into a product amounts to defining a map into each factor. Altogether, our "norm" map amounts to an $I\times I$-collection of maps:
- If $i=j$ we let $\mathrm{Nm}_I^{i,i}$ be the identity map.
- Otherwise we let $\mathrm{Nm}_I^{i,j}$ be the zero map, which exists by our pointedness assumption.

Thus we get something looking like a diagonal identity matrix. It is not a coincidence that the "entries" of this "matrix", identities and zero maps, are precisely the "singleton sums" and "empty sums" from the $(-1)$-case -- I will explain this coincidence shortly.

Now, similarly to how pointedness means that the colimit-to-limit map (over empty diagrams) is an isomorphism, we call our category *semiadditive* if the coproduct-to-product map defined above is an isomorphism. Finally we can construct our desired integration map using its inverse:

$$\int_I\phi : X \xrightarrow{\Delta} \prod_I X \xrightarrow{\prod_{i\in I}{\phi_i}} \prod_I Y \xrightarrow{\mathrm{Nm}_I^{-1}} \coprod_I Y \xrightarrow{\nabla} Y$$


**Case 0, again:** If you thought this wasn't abstract enough already, you're in for a treat. We can think of $I$ as a discrete $\infty$-category, and an $I$-indexed collection of objects in $\mathcal{C}$ is simply a functor from $I$ to $\mathcal{C}$. These assemble into a functor category $\mathcal{C}^I$.

This time I will even treat the relative case. Let $f : I \to J$ be a $0$-finite map, so essentially a map whose fibers are finite sets. Existence of finite co/products means that the restriction functor $f^\* : \mathcal{C}^J \to \mathcal{C}^I$ has a left adjoint $f\_!$ and a right adjoint $f\_\*$. In the special case where $J=1$ is the one-object category, $f:I\to 1$ is the unique possible morphism, $f\_!$ sends a finite family to its coproduct, and $f\_\*$ sends it to its product. In general, we may refer to $f\_!$ as "coproduct along fibers" and $f\_\*$ as "product along fibers". Our desired coproduct-to-product map then should be a natural transformation

$$\mathrm{Nm}_f : f_! \to f_*$$

But how do we obtain such map? How do we formalize our idea of using the "identity matrix"?

Instead of constructing $\mathrm{Nm}_f$ directly we will try to construct its adjunct $\nu_f : f^\*f\_! \to \mathrm{id}$, sometimes referred to as a "wrong-way unit". Let's think conceptually what the functor $f^\*f\_!$ does: given a finite family of objects $C = C_1,\cdots,C_n$ (possibly varying over some base space), $f\_!X$ is their coproduct (along fibers) and $f^\*f\_!X$ is the finite family of a bunch of copies of $f\_!X$. So we took our objects, summed them up (along fibers), and duplicated:

$$C_1,\cdots,C_n \quad\mapsto\quad C_1\amalg\cdots\amalg C_n \quad\mapsto\quad \begin{matrix} C_1\amalg\cdots\amalg C_n \\ \vdots \\ C_1\amalg\cdots\amalg C_n \end{matrix}$$

The "identity matrix" would be the map from this thing, which sends the $i$th coproduct to the copy of $C_i$ inside it. To make this precise, note that we can get the same result by a more "spread out" process. Namely instead of first taking coproducts and then duplicating, let's first duplicate and then sum each row:

$$C_1,\cdots,C_n \quad\mapsto\quad \begin{matrix} C_1,\cdots, C_n \\ \vdots \\ C_1,\cdots, C_n \end{matrix} \quad\mapsto\quad \begin{matrix} C_1\amalg\cdots\amalg C_n \\ \vdots \\ C_1\amalg\cdots\amalg C_n \end{matrix}$$

Rigorously, this is given by the functor $q\_!p^*$ where $p,q$ are the projection maps from the pullback:

<center><iframe class="quiver-embed" src="https://q.uiver.app/#q=WzAsNCxbMCwyLCJJIl0sWzIsMiwiSiJdLFsyLDAsIkkiXSxbMCwwLCJJXFx0aW1lc19KIEkiXSxbMCwxLCJmIiwyXSxbMiwxLCJmIl0sWzMsMiwicCJdLFszLDAsInEiLDJdLFszLDEsIiIsMSx7InN0eWxlIjp7Im5hbWUiOiJjb3JuZXIifX1dXQ==&embed" width="600" height="300" style="border-radius: 8px; border: none;"></iframe></center>

Saying "summing-then-duplicating and duplicating-then-summing are equivalent" is like saying that the pullback square gives a natural equivalence of functors $f^\*f\_! \simeq q\_!p^\*$. Indeed, this holds much more generally for any pullback square whose induced restriction maps have the appropriate adjoints.

The nice thing about $q\_!p^\*$ is that it actually goes through a "matrix", i.e. a family of objects indexed by the product $I\times_J I$. Given such matrix $M$, what we want to do is send the diagonal entries to themselves and the off-diagonal entries to the zero object.

So let $\delta : I \to I\times_J I$ be the diagonal map. The pullback functor $\delta^\* M$ will keep only the diagonal entries of a "matrix", and the colimit-along-fibers of that $\delta\_!\delta^* M$ will put these entries back on the diagonal, but fill everything else with zeros. To see why this last part works, note that the diagonal inclusion $\delta$ is, well, an inclusion. In other words, it's $(-1)$-finite, so from the previous case we inductively have a norm $\mathrm{Nm}_\delta : \delta\_! \to \delta\_\*$, which is an isomorphism (we're still assuming our category is pointed). From that we can construct a "wrong-way counit" $\omega : \mathrm{id} \to \delta\_!\delta^\*$ and "interject" it into the intermediate matrix from our previous process:

$$\nu_f : f^*f_! \simeq q_!p^* \xrightarrow{\qquad q_!\omega p^* \qquad} q_!\delta_!\delta^*p^* = \mathrm{id}$$

The equality at the end follows simply because $\delta$ is a section of each projection $p,q$. Now we can finally define the coproduct-to-product map $\mathrm{Nm}\_f : f\_! \to f\_\*$ as the adjunct. Huzzah! Finally, being semiadditive precisely means that $\mathrm{Nm}\_f$ is an equivalence for all $0$-finite maps $f$, so in a semiadditive category we can define integration along $f$ in terms of $\mathrm{Nm}\_f^{-1}$ just as before.

**Case 1:** $I$ is $1$-finite iff it's a finite disjoint union of finite groups (each group regarded as a one-object groupoid). A map $f:I\to J$ is $1$-finite iff its fibers are such. The same construction as before turns out to work:

- We want to construct $\mathrm{Nm}\_f : f\_! \to f\_\*$. Instead, we will construct its adjunct $\nu_f : f^\*f\_! \to \mathrm{id}$.
- By abstract nonsense, the same pullback square as before gives a natural isomorphism $f^\*f\_! \simeq q\_!p^\*$.
- In general, if $f$ is $m$-finite then its diagonal $\delta$ can be shown to be $(m-1)$-finite. In the current case, $\delta$ would be $0$-finite. In a semiadditive category, this means $\mathrm{Nm}\_\delta$ is an equivalence, and we can use it to define $\nu_f : f^\*f\_! \simeq q\_!p^\* \to q\_!\delta\_!\delta^\*p^\* = \mathrm{id}$ as desired.
- An $\infty$-category is called *$m$-semiadditive* if $\mathrm{Nm}\_f$ is an equivalence for all $m$-finite maps $f$, and we can use its inverse to define integration.

Hopefully the inductive process is now clear. Note that even if our category is not $1$-semiadditive but just $0$-semiadditive (i.e. semiadditive in the usual sense), we can still define norm maps for finite groups & groupoids, or finite disjoint unions thereof. They just may not be invertible in general.


**Remark:** Invertibility is measured by the homotopy cofiber of the norm map $\mathrm{Nm} : X_{hG} \to X^{hG}$, which is called the *Tate construction* $X^{tG}$, generalizing the classical Tate cohomology groups used in class-field theory. This generalization plays a critical role in some exciting parts of math like chromatic homotopy and algebraic $K$-theory. For instance, it's an important result that the $K(n)$-local and $T(n)$-local categories of spectra are $\infty$-semiadditive, which means the norm map is always an equivalence, which means the Tate construction is always trivial.


I promised transfer maps, and I can deliver: rather than focusing on the norm itself, its adjunct $\nu_f : f^\*f\_! \to \mathrm{id}$ is precisely the transfer map we were interested in! Specifically, if $f:BG\to 1$ then the "colimit along fibers" is the homotopy quotient $(-)\_{hG}$ and the adjunct is the transfer $X\_{hG} \to X$.

For the relative case, if $H\leq G$ is a finite index subgroup we get an inclusion $i : BH \to BG$ whose homotopy fiber is the finite set $G/H$. Denote $g:BG\to 1$ and $h:BH\to 1$. Then we have

**Another example:** if $H \leq G$ is a subgroup then we get $g : BH \to BG$. The restriction $g^\*$ forgets the $G$-action, only remembering the $H$-action. The adjoints $f\_\*,f\_\!$ are co/induction in the sense of representation theory. Note that the fibers of $g$ are copies of $G/H$ which is a set, that is to say, $g$ is $0$-finite. Since our category is ($0$-)semiadditive, we really do expect induction and coinduction to be isomorphic, which is a standard fact.

We can also repeat this whole story, replacing the adjunction $f\_! \dashv f^\*$ by the adjunction $f^\* \dashv f\_\*$. This will give rise to transfers on homotopy fixed points $X^{hH} \to X^{hG}$.

**Reminder:** Recall how colimits exhibit *contravariant* functoriality in the diagram: let $\mathbf{I},\mathbf{I}'$ be small categories and $h : \mathbf{I} \to \mathbf{I}'$ a functor. If $F : \mathbf{I}' \to \mathcal{C}$ is a diagram (in any target category) and $\lambda : F \Rightarrow c'$ a cocone, then $Fh$ is a diagram of shape $\mathbf{I}$ and $\lambda h : Fh \Rightarrow c'$ is a cocone under it. Thus any colimit $c$ of $Fh$ will have a unique morphism $c \to c'$. In particular if $c'$ is a colimit of $F$, we obtain a comparison map

$$\mathop{\rm colim}_{\mathbf{I}'}Fh \to \mathop{\rm colim}_{\mathbf{I}'}F$$

We specialize this to the case of a functor $BG \to BG'$ arising from a subgroup inclusion $G \hookrightarrow G'$. The result is a natural transformation between homotopy orbits: $F_{hG} \to F_{hG'}$.


In the next part I will introduce the notion of *Mackey functors*; a nice gadget that helps organizing all the transfer data.

**Warning:** As far as I can tell, Mackey functors in practice are not typically constructed using the method presented here, but I'm not acquainted enough with equivariant homotopy to say for sure. Regardless, I hope the same rough ideas & intuitions would carry over to any similar setup.

- Previous [Part 0: Background & motivating question]({% post_url /mackey-functors-series/2025-09-13-background %})
- Next [Part 2: Introducing Mackey functors]({% post_url /mackey-functors-series/2025-09-19-mackey %})