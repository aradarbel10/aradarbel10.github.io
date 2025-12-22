---
layout: post
title: Fiberwise arguments made easy
subtitle: And a HoTT-ish proof of the Thom isomorphism
---

$$
\renewcommand\S{\mathbb{S}}
\DeclareMathOperator\Map{Map}
$$

In my [previous post]({% post_url /2025-12-06-thom-index-shift %}) I talked about the Thom isomorphism and some subtle mistake I've made while using it. In retrospect that mistake seems so silly, but as they say, hindsight is 20/20. Something nice did come out of it though, because it got me thinking! Last time I made this remark:

> "There's a few good ways to prove this identity; I think the most conceptual one is just by proving it locally. Indeed, any bundle is locally trivial so the Thom space is locally a suspension. The Thom isomorphism is usually stated more specifically, by saying that the isomorphism is defined as multiplication with the Thom class $t$ of $\xi$."

The proof outline I describe here *can* be made precise: the way I was familiar with is by choosing a trivializing cover, and using Mayer-Vietoris to turn the local isomorphisms into global ones by gradually gluing up subsets in the cover.

My goal today is to show another way of making this outline rigorous -- the underlying concepts are basically identical, but the details are a good excuse to talk about fun math. I have to admit, after having this idea I couldn't quite work out the details on my own. Maybe I could've gotten there with more patience, but instead I ended up taking inspiration from [Guillaume Brunerie's legendary PhD thesis](https://arxiv.org/abs/1606.05916), where a good chunk of homotopy theory is developed synthetically in HoTT. See his section 6.1 in particular.

### Locally: suspension isomorphisms
Since the Thom isomorphism is a globalization of the suspension isomorphism, we should start from here. Let $R$ be a ring spectrum; I will use notation $R_i := \Omega^{\infty-i}R$ for its constituent spaces, so if you model $R$ as a sequential spectrum it'd just be $(R_0,R_1,R_2,\cdots)$. If you're not familiar with spectra, just keep in mind the example of Eilenberg-MacLane spaces $R_i = K(A,i)$, where $A$ is some ordinary ring.

Being a ring spectrum means:
- You have a multiplication map[^1] $\mu : R\otimes R\to R$. It's required to satisfy an associativity axiom that I won't be needing here.
- You have a unit map $\eta:\S \to R$, required to satisfy unitality axioms: namely the composite

$$R \simeq R\otimes\S \xrightarrow{\qquad \mathrm{id}\otimes\eta \qquad} R\otimes R\xrightarrow{\qquad\mu\qquad} R$$

should be the identity morphism, and likewise for unitality from the left.

These give analogous maps on infinite loop spaces:
- Multiplication maps $\mu : R_n \wedge R_m \to R_{n+m}$ satisfying various compatibilities.
- Unit maps $\eta_n : S^n \to R_n$.

Spectra represent cohomology with coefficients in $R$ in the sense that cohomology classes in $H^i(Y;R)$ homotopy classes of maps $Y \to R_i$. The *suspension isomorphism* in cohomology $H^i(Y) \cong H^{i+n}(\Sigma^nY)$ is then obtained abstraclty as:

$$\Map(Y,R_i) \simeq \Map(Y,\Omega^n R_{i+n}) \simeq \Map(\Sigma^n Y, R_{i+n})$$

The first equivalence here is obtained from the "structure maps" $\Omega^n R_{i+n} \simeq R_i$ which exist for any spectrum, and the second equivalence is simply the adjunction $\Sigma^n\dashv\Omega^n$.

Since $R_i$ represents cohomology, and $S^n$ co-represents homotopy, we can identify:

$$H^i(S^n;R) \cong \pi_0\Map(S^n,R_i) \cong \pi_n(R_i)$$

In particular, $\eta_n : S^n \to R_n$ from earlier defines a cohomology class, called the *fundamental class* $\eta_n \in H^n(S^n;R)$. My point in this opening section is to show how the suspension isomorphism is given naturally by taking "external" cup products with this fundamental class.

Precisely, suppose we have a map $\beta : Y \to R_i$ representing some cohomology class. The *external cup product* with $\eta_n :S^n \to R_n$ is defined using the ring structure

$$\beta\cup\eta_n : Y\wedge S^n \xrightarrow{\qquad\beta\wedge\eta_n\qquad} R_i\wedge R_n \xrightarrow{\qquad\mu\qquad} R_{i+n}$$

Overall we have constructed a morphism $-\cup\eta_n : \Map(Y,R_i) \to \Map(Y\wedge S^n,R_{i+n})$, and what I'm trying to argue is that this coincides with the suspension isomorphism derived just above. Let us deal with the universal case: $Y = R_i$ and $\beta = \mathrm{id}$. Then cupping with $\eta_n$ simplifies into the following

$$R_i\wedge S^n \xrightarrow{\qquad\mathrm{id}\wedge\eta_n\qquad} R_i\wedge R_n \xrightarrow{\qquad\mu\qquad} R_{i+n}$$

This looks an awful lot like the unitality axiom we had for the spectrum $R$. Indeed we can obtain the analogous axiom on spaces by applying the functor $\Omega^\infty$, while keeping in mind that it is only right-lax monoidal[^2]:
<center><iframe class="quiver-embed" src="https://q.uiver.app/#q=WzAsOSxbMCwxLCJcXFNpZ21hXmlSIFxcb3RpbWVzIFxcU2lnbWFeblxcbWF0aGJie1N9Il0sWzIsMSwiXFxTaWdtYV5pUlxcb3RpbWVzXFxTaWdtYV5uUiJdLFsyLDMsIlxcU2lnbWFee2krbn1SIl0sWzMsMiwiXFxyaWdodHNxdWlnYXJyb3ciXSxbNCwxLCJcXE9tZWdhXlxcaW5mdHkoXFxTaWdtYV5pUlxcb3RpbWVzXFxTaWdtYV5uXFxtYXRoYmJ7U30pIl0sWzQsMCwiUl9pXFx3ZWRnZSBTXm4iXSxbNiwxLCJcXE9tZWdhXlxcaW5mdHkoXFxTaWdtYV5pUlxcb3RpbWVzXFxTaWdtYV5uUikiXSxbNiwwLCJSX2lcXHdlZGdlIFJfbiJdLFs2LDMsIlJfe2krbn0iXSxbMCwxLCJcXG1hdGhybXtpZH1cXG90aW1lc1xcU2lnbWFeblxcZXRhIl0sWzEsMiwiXFxTaWdtYV57aStufVxcbXUiXSxbMCwyLCJcXG1hdGhybXtpZH0iLDJdLFs1LDRdLFs0LDZdLFs1LDcsIlxcbWF0aHJte2lkfVxcd2VkZ2VcXGV0YV9uIl0sWzcsNl0sWzYsOF0sWzQsOCwiXFxtYXRocm17aWR9IiwyXSxbNyw4LCJcXG11IiwwLHsib2Zmc2V0IjotNSwiY3VydmUiOi01fV1d&embed" width="900" height="300" style="border-radius: 8px; border: none;"></iframe></center>

The triangle on the right commutes by functoriality, and the little rectangle above it commutes by naturality of the lax monoidal structure. I'm also being a little liberal with what I'm calling identity, but that's not too big of a deal. The upshot is that our cup product map is precisely the composite appearing in this diagram! More specifically if we adjunct the resulting map $R_i\wedge S^n \to R_{i+n}$, we will get the "identity" $R_i \to \Omega^n R_{i+n}$, which literally becomes identity after we identify $\Omega^nR_{i+n}\simeq R_i$.

But hey, that's how we defined the suspension isomorphism; the spectrum's structure map and the suspension-loop adjunction!


### Globally: working on a fiber
Now let's try to globalize.

Suppose $S^n \xrightarrow{\iota} Q \xrightarrow{\pi} B$ is a fiber sequence, whose fiber space is a sphere. This means we have a family of spheres parameterized by the points of $B$ in a continuous fashion, at least up to homotopy. For simplicity I assume $B$ is path-connected, but everything can be adjusted to the general situation.

Now in place of the fundamental class, suppose we have some cohomology class on the total space, $c : Q \to R_n$ such that, when restricted along the fiber inclusion $\iota$, gives the actual fundamental class: $c\circ\iota = \eta_n$. This sort of cohomology class is sometimes called an *orientation class*[^3] for the sphere bundle. My claim, if so, is that the following map is an isomorphism

$$H^i(B) \to H^{i+n}(Q) : \beta \mapsto \pi^*\beta\cup c$$

Actually it will even be true on the level of mapping spaces, i.e. $\Map(B,R_i) \simeq \Map(Q,R_{i+n})$. Observe that the cup product this time is not external anymore but internal, which simply means it's pulled back along the diagonal. Overall, the definition of our candidate map is

$$\Map(B,R_i) \xrightarrow{\quad\pi^*\quad} \Map(Q,R_i) \xrightarrow{\quad-\cup c\quad} \Map(Q,R_{i+n})$$


The globalization can be performed using a very nice Yoneda trick. This chain of maps can be upgraded to a chain of natural transformations between functors defined on $\mathcal{T}\_{/B}$ spaces over $B$. I will write $U$ for the forgetful functor $\mathcal{T}\_{/B} \to \mathcal{T}$.

$$\Map(U(-),R_i) \xrightarrow{\quad\pi_{-}^*\quad} \Map(-\times_B Q,R_i) \xrightarrow{\quad-\cup c_{-}\quad} \Map(-\times_BQ,R_{i+n})$$

To explain the notation used here, note that given any space $b \in \mathcal{T}\_{/B}$ over $B$ we obtain by pullback a new projection $\pi_R : b\times_B Q \to b$ and a new cohomology class $c_R : b\times_B Q \to Q \xrightarrow{c} R_n$. The original sequence is retrieved upon plugging in $b = B$ (as a space over itself).

Thanks to Yoneda, if we can show that this whole ugly thing is a natural isomorphism, then it will be also an isomorphism for our particular choice of interest. At first glance this does not seem useful at all, because we've reduced our problem from checking just one space to checking all the spaces in the whole category... worry not, for that is only the "Yoneda" part of my "Yoneda trick"...

Here's the "trick" itself: it's a standard fact that, just like the category $\mathbf{Set}$ is generated under colimits from the singleton set $\\{\star\\}$, analogously the $\infty$-category of spaces $\mathcal{T}$ is generated under homotopy colimits from the one-point space $pt$. This is actually not as deep as it may sound, because we can just take the set/space itself as the diagram:

$$S \simeq \mathop{\operatorname{hocolim}}_{S}{pt}$$

Now, again analogously to the $1$-categorical situation, the forgetful functor $\mathcal{T}\_{/B} \to \mathcal{T}$ creates and reflects colimits, so also for any space $S$ over $B$ we can form the very same colimit in $\mathcal{T}\_{/B}$ and get the correct space as the result. Put succinctly, $\mathcal{T}\_{/B}$ is generated under colimits by $pt$, regarded as the basepoint of $B$.[^4]

You may also observe that all the functors in our sequence of natural transformations preserve colimits:
- $U$ is a left adjoint of $B\times-$.
- $-\times\_BQ$ is a left adjoint of $\Map\_B(Q,-)$.
- $\Map(-,R\_*)$ in general turns colimits into limits.

So we don't need to check that our composite is an equivalence for *all* spaces, we actually only need to check it for the basepoint $b = pt$ of $B$! And by our very assumption, the fiber of $Q$ over the basepoint is $pt\times_BQ \simeq S^n$ a sphere -- we get literally the suspension isomorphism!

The core of the argument is behind us, but to get the actual Thom isomorphism there's just one last bit of the formulation we need to massage. In short, all of the above applies for bundles of *pointed* spheres, though I quietly glanced over most of this. For a general bundle *unpointed* spheres, one can form the fiberwise suspensions, which are naturally pointed.

Recall that the suspension of a space $Y$ can be obtained as the homotopy cofiber of the map to the terminal space, i.e. there is a cofiber sequence $Y \to pt \to \Sigma Y$. This can be relativized to the category $\mathcal{T}\_{/B}$: the terminal object is now $B$ itself (each fiber has one point), and the *Thom space* of our sphere fibration $Q \to B$ is defined as the cofiber of the unique map to it

$$Q \xrightarrow{\quad\quad\quad} B \xrightarrow{\quad\text{cofib}\quad} \operatorname{Th}(Q)$$

This description can be refined slightly, by pasting homotopy pushout squares:
<center><iframe class="quiver-embed" src="https://q.uiver.app/#q=WzAsNixbMCwwLCJRIl0sWzIsMCwiQiJdLFswLDIsIkIiXSxbMiwyLCJcXFNpZ21hX0JRIl0sWzQsMCwicHQiXSxbNCwyLCJcXG9wZXJhdG9ybmFtZXtUaH1RIl0sWzAsMSwiXFxwaSJdLFswLDIsIlxccGkiLDJdLFsyLDNdLFsxLDMsInMiXSxbMywwLCIiLDEseyJzdHlsZSI6eyJuYW1lIjoiY29ybmVyIn19XSxbMSw0XSxbMyw1XSxbNCw1XSxbNSwxLCIiLDEseyJzdHlsZSI6eyJuYW1lIjoiY29ybmVyIn19XV0=&embed" width="700" height="300" style="border-radius: 8px; border: none;"></iframe></center>

One can think of the left-hand square precisely as a fiberwise suspension teased earlier; the section $s$ selects the "south pole" of each suspension. The right-hand square amounts to collapsing this section to a point, thus retrieving the usual Thom construction.

However since the fibers of $Q$ are themselves spheres, then their suspensions are spheres of one dimension higher, so everything we've done so far applies to it too, and we finally recover the Thom isomorphism. $\square$


#### Footnotes
[^1]: I write $\otimes$ for the smash product of spectra.
[^2]: I am following Lurie's terminology, where "right-lax" is what's usually called "lax", and "left-lax" is what's usually called "oplax".
[^3]: Traditionally the orientation class has to restrict to $\eta_n$ on *all* fibers. As we show here, since $B$ is path-connected, it's enough to require this just on the one fiber through $\iota$. If $B$ has multiple path-components, it's enough to check one point from each.
[^4]: This is another place where path-connectedness is necessary. For general $B$, you could say that $\mathcal{T}_{/B}$ is generated under homotopy colimits by $\pi\_0(B) \subseteq \mathrm{ob}\mathcal{T}\_{/B}$ i.e. one basepoint for each path-component.
[^5]: Meaning every sequence of three consecutive objects form a fiber sequence in the usual sense. This might be more appropriately called a "long fiber sequence", or occasionally an $h$-coexact sequence (e.g. tom Dieck's book).