---
layout: post
title: The Minlos-Bochner theorem and infinite-dimensional Gaussians
subtitle: It's not *that* field theory, it's the other one
---

$$
\newcommand\N{\mathbb{N}}
\newcommand\R{\mathbb{R}}
\newcommand\C{\mathbb{C}}
\newcommand\E{\mathbb{E}}
\newcommand\eps{\varepsilon}
\newcommand\into{\hookrightarrow}
\newcommand\norm[1]{\lVert {#1} \rVert}
\newcommand\inn[2]{\left\langle {#1} , {#2} \right\rangle}
\renewcommand\cl[1]{\mathcal{#1}}
\renewcommand\Re{\operatorname{Re}}
\DeclareMathOperator\tr{tr}
\DeclareMathOperator\Sym{Sym}
$$

Here's another pull from deep in the drawer.

A while ago I became invested in (quantum & classical) field theory, mostly via connections to homotopy theory: the cobordism hypothesis, elliptic genera, and in particular the Stolz-Teichner program which proposes a quantum-field-theoretic interpretation of cocycles in $TMF$, generalizing all the known connections between theoretical physics and topological $K$-theory. Quantum field theories are notoriously difficult to construct rigorously, and there's a lot of contemporary research currently being done about this.

More recently I stumbled on some notes that I wrote at the time and completely forgot about. They discuss the arguably hardest step of the construction, which is the infinite Gaussian measure, and I treat it from my own slightly category-pilled perspective. So that they won't go to waste, this post is essentially a copy-pasted version of them. My main reference for constructive QFT is Jiasheng Lin's PhD thesis[^1], and for measure theory Yamasaki's book[^2], but beware that the following is likely riddled with my own mistakes!

### Motivation from quantum field theory
Perhaps the most basic example is the Euclidean QFT of free bosonic fields. Let's think how one might formalize this into the functorial framework. Let $\mathbf{Cob}^{Riem}_{d-1,d}(B)$ be the category of Riemannian cobordisms, possibly equipped with a $B$-valued background field (take $B=pt$ if you don't want that). Heuristically:
- Objects are $(d-1)$-manifolds without boundary, compact and oriented, equipped with a Riemannian metric, and a continuous map to $B$.
- Morphisms are $d$-manifolds with boundary, compact and oriented, equipped with a Riemannian metric, and a continuous map to $B$, both of which are compatible with those of the boundary.

Making this construction precise requires some work, the main subtleties being:
- Due to the Riemannian requirement there are no identity morphisms, in other words this is only a semi-category rather than a category. In theory one could very easily adjoin identities formally, though this loses some geometric niceties. In practice this would not be necessary, since we will only consider semi-functors on this semi-category whose target is a category, so by adjunction the identities don't add any extra information.
- Composition should be given by gluing manifolds along their boundaries, but this is not always possible in geometric contexts, e.g. due to the metric. One common solution is to require the metric to be "nice" near the boundary -- it should look like the product metric of the boundary with some small collar neighborhood. Another common solution is to encode collars in the objects themselves, so instead of being a $(d-1)$-manifold, it would be a "germ" of such.

I am interested in the case where $B$ is a classifying space for vector bundles with a metric and flat connection (which is not really a space but a stack)

$$B \approx \coprod_{n\in\N}{BO_n(\R)^{conn}}$$

For every $\Sigma$ a $(d-1)$- or $d$-dimensional manifold let $V_\Sigma$ be the vector bundle classified by its background map to $B$, with metric $\eta_\Sigma$ and flat connection $\nabla_\Sigma$ satisfying compatibility ($\nabla_\Sigma(\eta_\Sigma) = 0$).

Let $\Gamma^\infty_c(V_\Sigma^\vee)$ be the vector space of smooth sections *of the dual bundle* with compact support (this requirement is technically superfluous since we are only considering $\Sigma$ compact anyways). This is made into a topological vector space, in fact a Fréchet space, using the following family of semi-norms: for each $A\subseteq\Sigma$ compact, and for each $k\in\N$,

$$\nu_{k,A}(f) = \max_{0\leq j\leq k}\sup_A{\norm{\nabla_\Sigma^{(j)}f}_{\eta_\Sigma}}$$

Here $\nabla_\Sigma^{(j)}$ denotes the $j$th order covariant derivative, and the norm is the one determined by $\eta_\Sigma$ on sections of $V_\Sigma$, and by the Riemannian metric of $\Sigma$ on sections of $T\Sigma^{\otimes(-j)}$ (i.e. differential $j$-forms valued in $V_\Sigma$).

The space of *distributional sections* of $V_\Sigma$ is now defined as

$$\cl{F}_\Sigma := \cl{D}'(V_\Sigma) := \Gamma^\infty_c(V_\Sigma^\vee)'$$

where $'$ on the RHS denotes the *continuous* dual vector space of all continuous functionals. This is made into a topological vector space via the weak topology (i.e. the coarsest topology that makes every evaluation map $$\mathrm{ev}_f : \cl{D}'(V_\Sigma) \to \R$$ continuous). It is well known that this topology turns out to be locally convex.

This space $\cl{D}'(V_\Sigma)$ is going to be the space of *classical* fields aka classical configurations for our field theory, and the notation $\cl{F}_\Sigma$ will be used when we want to emphasize this role. To quantize it, we'd like to consider a space of "wave-functions" on these configurations. Following Lin, I will opt to encoding this in a *real* Hilbert space (unlike the usual complex Hilbert space of quantum mechanics, where complex values encode probability amplitudes). I am not entirely sure why this convention was chosen but I'd rather stick to it.

Thus we make the definition

$$\cl{H}_\Sigma := L^2_\R(\cl{F}_\Sigma,\hat\gamma_\Sigma)$$

Of course we must discuss where the measure $\hat\gamma_\Sigma$ comes from, and this is by a long shot the main challenge in rigorously constructing non-perturbative QFTs. Let's start by thinking conceptually what this measure "should" look like.

For any field configuration $$\phi \in \cl{F}_\Sigma$$ we define the *free action*

$$S_0(\phi) := \int_\Sigma{\frac{1}{2}\phi(\Delta_\Sigma + m^2)\phi\; dg}$$

Here $$\Delta_\Sigma := -\tr_\eta\nabla^2_\Sigma$$ is the so-called positive Laplacian operator, induced by the dual connection on $$V_\Sigma^\vee$$ (which we still denote $$\nabla_\Sigma$$), and extended to $$\cl{F}_\Sigma$$ through the standard "distributional derivative" formula

$$\inn{\nabla_\Sigma\phi}{f} := -\inn{\phi}{\nabla_\Sigma f}$$

where $f$ is a test function and $\inn{}{}$ is the evaluation pairing. Keep in mind that this formula relies on $\Sigma$ having no boundary, and will have to be modified to apply in full generality.

The "Feynman path integral" (in Euclidean form) is easily well-definable in more classical physical setups, but in QFT it's merely a heuristic expression established by physicists that tells us what the value of $$\cl{Z}_\Sigma$$ should be:

$$\cl{Z}_\Sigma \approx \int_{\cl{F}_\Sigma}{\exp(-S_0(\phi))[D\phi]}$$

This is only a heuristic, because the measure $$[D\phi]$$ on the infinite dimensional vector space $$\cl{F}_\Sigma$$ does not have a precise definition. To overcome this, mathematicians have realized that although the measure itself is not well-defined, the whole expression $$\exp(-S_0(\phi))[D\phi]$$ actually can be interpreted rigorously. Roughly this is because the exponential term at the front makes this into a *Gaussian* measure, which by the steepest-descent principle is highly concentrated around the exterma of $S_0$ -- so much so that its integral converges. We are going to construct this Gaussian measure rigorously, and call it $$\gamma_\Sigma$$. The measure $$\hat\gamma_\Sigma$$ above is just a renormalization of that.

### Gaussian measures in finite dimensions
Let $V$ be a finite dimensional vector space over $\R$, say $\dim V = d$. Suppose $B : V^{\otimes 2} \to \C$ is a symmetric bilinear form which is non-degenerate, and such that its real part $\Re B$ is positive-semidefinite (aka non-negative definite). Let $dx$ be a Haar measure on $V$.

Recall that a *Schwartz function* on $V$ is a $C^\infty$-function $f:V\to\R$ such that $Df \in L^2(V)$ for every differential operator $D$ in the Weyl algebra of $V$ (i.e. a polynomial combination of functions on $V$ and partial directional derivatives). The space of Schwartz functions is denoted $$\mathscr{S}(V)$$ and it becomes a Fréchet space through the usual set of seminorms: $\norm{D f}_{L^2}$ for every $D$. The space of tempered distributions on $V$ is then $\mathscr{S}'(V)$, the continuous dual.

Connecting back to the previous paragraph, we note that $\exp(-\frac{1}{2}B(x,x)) \in \mathscr{S}'(V)$ is a well-defined tempered distribution (beware, unless $B$ is actually *positive definite*, this is strictly a distribution, not represented by an actual function). This distribution is called the *(complex) Gaussian* with covariance $B$. The key property of Gaussians is the ability to integrate/Fourier transform them:

$$\cl{F}\left[\exp\left(-\frac{1}{2}B(x,x)\right)\right](\xi) = (\det B)^{-\frac{1}{2}} \exp\left(-\frac{1}{2}B^{-1}(\xi,\xi)\right)$$

In other words the Fourier transform of a Gaussian with covariance $B$ is another Gaussian, with some scaling factor, and with covariance $B^{-1}$.


### Gaussian free fields
Denote by $$C = \Delta_\Sigma + m^2$$ the operator that determines the kinetic/free part of the action, so for a section $\phi$ of $$V_\Sigma$$ (could be an $L^2$-section or a $$C^\infty_c$$-section) its free action functional is

$$S_0(\phi) = \frac{1}{2}\inn{\phi}{C\phi}_{L^2(\Sigma,dg)}$$

Recall that our aim is to construct a measure $$d\gamma_C$$ on $$\cl{F}_\Sigma = \cl{D}'(V_\Sigma)$$ which heuristically behaves like

$$d\gamma_C(\phi) \approx e^{-S_0(\phi)}[D\phi]$$

If $$\cl{F}_\Sigma$$ were finite dimensional, so $$\cl{F}_\Sigma = V'$$ for some finite dimensional vector space $V$, $\dim V = d < \infty$, then a Lebesgue measure $[D\phi]$ on $V'$ actually does exist, and the complex-valued function $$e^{-S_0(\phi)}$$ actually is square-integrable, and its integral can be computed explicitly as a Gaussian integral:

$$\int_{V'}{e^{-\frac{1}{2}\inn{\phi}{C\phi}}[D\phi]} = (2\pi)^{d/2}(\det C)^{-1/2}$$

where $C$ is just some symmetric positive-definite real matrix. Thus in the finite dimensional case we can define a Gaussian measure literally as $e^{-\frac{1}{2}\inn{\phi}{C\phi}}[D\phi]$. In practice we want this to be a probability measure, i.e. the total integral should be equal to $1$, so we just divide by the remaining factors on the right:

$$d\gamma_C := (2\pi)^{-d/2}(\det C)^{-1/2} e^{-\frac{1}{2}\inn{\phi}{C\phi}}[D\phi]$$

The key property that this measure should satisfy is that it behaves probabilistically like a normal distribution, i.e. gives the correct covariance structure; for fixed vectors $x,y$,

$$\E_\gamma[x] := \int_{V'}{(\phi,x) e^{-\frac{1}{2}\inn{\phi}{C\phi}}[D\phi]} = 0 \qquad\qquad \E_\gamma[xy] := \int_{V'}{(\phi,x)(\phi,y)e^{-\frac{1}{2}\inn{\phi}{C\phi}}[D\phi]} = \inn{x}{Cy}$$

where on the RHS of the second equation, the expression $\inn{x}{Cy}$ identifies $x,y$ with their dual vectors.

**Remark:** These computations are generalized by *Wick's theorem* from quantum mechanics: given $x_1,\cdots,x_n$,

$$\E_\gamma[x_1\cdots x_n] = \sum_{\text{pairings }\pi}\prod_{j=1}^{n}{\inn{x_j}{x_{\pi j}}_C}^{1/2}$$

Here a *pairing* $\pi$ is a permutation on $\{1,\cdots,n\}$ such that $\pi^2 = \mathrm{id}$ and $\pi$ has no fixedpoints. In other words, we pair up all the elements in the set, and $\pi$ just exchanges the two (distinct) members of each pair. The exponent $1/2$ in each factor is just to compensate for the fact that every pair would be counted twice. Observe that this sum is vacuously zero when $n$ is odd.

### The Milnor-Bochner approach
Let's go on a brief digression.

Suppose $G$ is a LCA group with Pontrjagin dual $\widehat G$. The Fourier-Stieltjes transform sends every finite measure on $\widehat G$ to a complex-valued function on the original group $G$:

$$\mu(\xi) \longmapsto \hat\mu(x) := \int_{\widehat G}{(\xi,x) \mu(dx)}$$

When $\mu$ is thought of as a random variable, $\hat\mu$ is often called its *characteristic function*. There is a very useful property satisfied by this transformed function: it is *positive-semidefinite*. The meaning of positive-semidefinite in this context is as follows: a *kernel* over $G$ is a map $$\kappa : G\times G \to \C$$ and (in complete analogy to kernels of integral operators) we like to think of it as a matrix, except the rows & columns are not indexed by numbers, but rather by the points of $G$. Every function $f : G \to \C$ defines an *invariant kernel* by $$\kappa(x,y) := f(xy^{-1})$$, i.e. a kernel which depends only on the relative position of the parameters, and conversely every invariant kernel is obtained in this way.

We make some analogies to the usual theory of finite matrices: a kernel $\kappa$ is called *symmetric* if $$\kappa(x,y) = \kappa(y,x)$$. It is called *positive-semidefinite* if, for every finite subset $I \hookrightarrow G$, the ordinary finite matrix $\kappa\vert_I$ is positive-semidefinite. This means that the induced quadratic form $\kappa(x,x)$ is always non-negative.

So the Fourier-Stieltjes transform of a finite measure on $\widehat G$ is positive-semidefinite.

**Theorem (Bochner):** Modulo some technical conditions, every positive-semidefinite function on $G$ arises from a unique finite measure on $\widehat G$ in such way.

TVSs are typically not locally compact, so the LCA framework does not apply anymore. But there's still a variant of this, which works under an extra technical hypothesis on the TVS $\cl{E}$ -- we require that it be *nuclear* in the sense of Grothendieck. So suppose now $\cl{E}$ is a nuclear space and $\mu$ a finite measure on its dual $\cl{E}'$. Then it has a similarly-defined Fourier-Stieltjes transform which yields a function $\hat\mu$ on $\cl{E}$.

**Theorem (Minlos):** Modulo some technical conditions, every positive-semidefinite function on $\cl{E}$ arises from a unique finite measure on $\cl{E}'$ in such way.

Thus to construct a Gaussian measure on $\cl{E}'$ we just need to specify what we'd like its covariance to be, and that will determine the characteristic function, and hence the measure itself!
I would like to sketch a proof of Minlos's theorem -- this will require some technical tools.

### Two perspectives on Cameron-Martin spaces

1. Let's say you have a real Hilbert space $H$, and you want to define on it a "Gaussian function", or more precisely a Gaussian (Borel) measure $d\gamma$. Turns out that this is possible to define only as a "cylinder measure" i.e. measure on a cylinder algebra -- a certain proper subalgebra of the Borel $\sigma$-algebra. Instead one can enlarge $H$ into a Banach space $B \supseteq H$ and this actually does admit a well-defined Gaussian *Borel* measure which restricts to the original one on cylinder sets. The pair $(H\into B)$ is then called an *abstract Wiener space*, and the subspace $H$ is called the *Cameron-Martin space* associated to the Gaussian on $B$.

2. Conversely, let's say you have a Banach space $B$ and you want to construct Gaussian measures on the dual $B'$. As in the finite-dimensional case, a Gaussian (centered at the origin) is classified uniquely by its covariance, which is a certain symmetric bilinear form on $B$. It would've been nice if this bilinear form was an inner product, but that's not possible for general Banach spaces -- instead, it only defines an inner product on some subspace $H$ of $B$ which we call the *Cameron-Martin space* of the Gaussian. It turns out that the Cameron-Martin space encodes pretty much everything you want to know about the Gaussian: indeed if you just start from a Cameron-Martin space $H$ then it extends uniquely to an abstract Wiener space $(H\into B)$ as in (1).

So studying Gaussian measures $(B',d\gamma)$ is roughly equivalent to studying Cameron-Martin spaces $(H\into B)$. In our current context, dealing rigorously with Gaussian measures is hard, but dealing rigorously with Hilbert subspaces is much easier! It'd be very convenient if we could access measure-related constructions directly from the Cameron-Martin space, i.e. without the middle step of construction $d\gamma$.

For example, if you start from a Gaussian measure and want to construct the Hilbert space $L^2(B',d\gamma)$ of square-integrable functions, then this turns out to be exactly isomorphic to the symmetric algebra (what physicists call a "Fock space") of the (dualized) Cameron-Martin space $\Sym^* H'$.
In other words, suppose our initial data is the Hilbert space $H$. Say we want to define on it a Gaussian $d\gamma$ which is really defined on some larger space $B'$, and then consider the $L^2$ functions wrt this Gaussian. Then the measure can be completely circumvented, by just going directly to the Fock space!

In our situation, we are interested in defining a Gaussian measure on $B' = \cl{D}'$, some space of distributions, where $\cl{D} = C^\infty_c$ is a space of test functions.

**Proof sketch (Minlos):** Suppose we wanted to construct a Gaussian measure on $B$. What would it mean for a measure on an infinite-dimensional space to be Gaussian? Most reasonably, at the very least we should require that its restriction to any finite-dimensional subspace is a Gaussian, in the classical sense.
So suppose $V \subseteq B$ is a finite dimensional subspace, and $E \subseteq V$ is a Borel subset. Then restricting our covariance operator to just $V$, we get a covariance matrix for a unique Gaussian measure on $V$, and we use this to define the target measure on the "cylinder" of $E$, i.e.

$$\gamma_C(E\times V^\perp) := \gamma_{C|V}(E)$$

One can show that this definition is independent on the representation of the cylinder. So we get a "Gaussian cylindrical measure" on $B$ but not a full Borel measure. More conceptually, a cylindrical measure on an infinite-dimensional vector space is precisely a "compatible" family of Borel measures on all of its finite dimensional subsets, where compatibility is in the sense of (categorical / projective) limits.


### Minlos's theorem - more details
I now describe a proof inspired from Yamasaki's book.

Intuitively, if we wanted to construct a Gaussian measure on an infinite-dimensional vector space $B$, we might naïvely try to start from a Gaussian on each finite-dimensional subspace, impose on them some compatibility conditions, and then hope that they glue up to a measure on the total space. In other words, we'd want to express $B$ as a colimit of finite-dimensional measure spaces.

Unfortunately this does not work (try!) because measures and colimits don't play so well together. In contrast, *limits* do play well with measures, so if we could write our space as a limit of finite-dimensional subspaces, each of which endowed with an appropriate Gaussian measure, we'd be happy. But this makes another issue: $B$ is typically not going to be a limit of finite-dimensional subspaces.

Instead, we can rely on the fact that algebraic duality turns colimits into limits, therefore, since $B$ is certainly the colimit of its finite-dimensional subpaces, then its algebraic dual $B^\sharp$ is the limit of their finite-dimensional duals. This allows us to construct Gaussian measures on the algebraic dual.
Next we'd like to restrict such measure to the continuous dual $B' \subseteq B^\sharp$. If $B'$ was itself a measurable subset, then we could easily restrict the measure to it and be done (this is just a basic fact on measure spaces). But we don't know how to prove $B'$ is measurable, and actually in general it's just not. The next best option is if we know that the subspace $B'$ *supports* the measure: this means that $B'$ itself might not be measurable, but every measurable subset of its complement is null. In this situation, we can also restrict the Gaussian measure to $B'$ in a well-defined manner. But, is every Gaussian measure supported on $B'$?

The support of a measure on $B^\sharp$ turns out to be very closely related to the regularity of its characteristic function / Fourier-Stieltjes transform. For an extreme instance, the Dirac measure is supported on a tiny subspace -- the $0$-dimensional origin -- and its Fourier transform is constant.
Now I can be a bit more specific about the "technical conditions" in the Bochner-Minlos theorems: they say that if the Fourier transform is continuous in some nuclear topology on $B$, then the measure is indeed supported on $B'$.

More generally, suppose $M \subseteq B$ is a linear subspace. Rigorously, we assume the topology on $B$ is given by an inner product $\inn{}{}$, while the topology on $M$ is given by a different inner product $\inn{}{}_T$ such that, there exists some Hilbert-Schmidt operator $T : M \to M$ satisfying $\inn{x}{y}_T = \inn{Tx}{Ty}$ for all $x,y\in M$. We also require the inclusion $M \into B$ to be continuous[^3] though not necessarily an embedding or isometry.

Anyways, by a sinful abuse of notation, write $M' \subseteq B^\sharp$ for the space of linear functionals on all of $B$ which become continuous upon restriction to $M$ with its own topology. Let's think what it would mean for a measure $\mu$ to be supported on $M'$? Roughly, pretend $M'$ is measurable (this is not too far from the truth), so it'd suffice to verify it has the same measure as the entire algebraic dual: $\mu(M') = \mu(E^\sharp)$. Therefore our interest is in the integral

$$\mu(M') = \int_{E^\sharp}{\mathbf{1}_{M'}\; d\mu}$$

In order to get a handle on this, we might want to convolve the indicator function $$\mathbf{1}_{M'}$$ with some Gaussian/bump to make it smooth, and then get our hands dirty with some analysis to get a lower bound. This is problematic, however, because how can we convolve with a Gaussian if our entire goal is to construct such Gaussian to begin with?!

Instead we observe that $\mathbf{1}_{M'}$ admits a very similar description, in terms of "cylindrical Gaussians"

$$\mathbf{1}_{M'}(\xi) = \lim_{\alpha\searrow 0}\lim_{N\to M}\exp\left(-\frac{\alpha}{2}\norm{\pi_N\xi}_{N^\sharp}^2\right)$$

Here the notation $N \to M$ means we are taking a limit over the net of finite dimensional subspaces of $M$, and $\pi_N$ is the restriction map on functionals. Strictly speaking $$\norm{\pi_N \xi}_{N^\sharp}$$ is a well-defined (non-infinite) real number only if $\xi$ is bounded, but that's exactly the same thing as being continuous. So if $\xi$ is continuous on $M$ (hence on $N$), the term inside the $\exp$ will be finite, and as we take $\alpha\searrow0$ it will become $\exp(-0) = 1$.
In contrast, if $\xi$ is not continuous then $$\norm{\pi_N\xi}_{N^\sharp} = \infty$$ grows way too quickly and $\alpha$ cannot overcome this. Hence this time the limit will be $\exp(-\infty) = 0$. That's the neat trick -- $M'$ is defined in terms of continuity, meaning finiteness of the norm, and we can use the exponential function to distinguish between infinite and finite quantities in the limit.

When we integrate this thing, we are free to exchange the integral with the limits (the exponents under considerations are always non-positive, so the $\exp$ is dominated by $1$, and we may apply the dominated convergence theorem). Thus,

$$I_{\alpha,N} := \int_{E^\sharp}{\exp\left(-\frac{\alpha}{2}\norm{\pi_N\xi}^2_{N^\sharp}\right)d\mu(\xi)} \qquad\qquad \mu(M') = \lim_{\alpha\searrow0}\lim_{N\to M}I_{\alpha,N}$$

To bound $I_{\alpha,N}$ we need to shuffle some things around. First and foremost, this integral is really begging us to make a change of variables $s = \pi_N\xi$. Rigorously, consider the restriction map $E^\sharp \to N^\sharp$ and push the measure $\mu$ forward along it. We denote the resulting measure by $\mu_N$, but also note that if $\mu$ comes from a limit of measure spaces as was planned in our strategy, $\mu_N$ was already part of the input data.
With this the integral becomes

$$I_{\alpha,N} = \int_{N^\sharp}{\exp\left(-\frac{\alpha}{2}\norm{s}^2_{N^\sharp}\right)d\mu_N(s)}$$

Denote the integrand by $g_{\alpha,N^\sharp}$ -- it's a Gaussian on $N^\sharp$ (still finite dimensional) with covariance $\alpha$. Normally we are able to integrate Gaussians on finite dimensional spaces, however this time the measure is not the Lebesgue measure, so it's not immediate. To get around this we observe that the integral is exactly the Fourier transform evaluated at $0$, that is $I_{\alpha,N} = \hat g_{\alpha,N^\sharp}(0)$. The Fourier transform of the integrand is described more easily: the Gaussian's covariance gets inverted, the measure becomes its characterstic function (by definition), and some scalar factors are added at the front

$$\hat g_{\alpha,N^\sharp}(x) = (2\pi\alpha)^{-N/2}\exp\left(-\frac{1}{2\alpha}\norm{x}^2_{N}\right)\hat\mu(x)dx$$

I allow myself to write here $\hat\mu$ instead of $\hat\mu_N$ because they're a restriction of one another. We use this to rewrite the integral. On the same go, let's also take only the real part (the final value of the integral is real so it doesn't matter... in fact the only part that's potentially not real is $\hat\mu(x)$):

$$I_{\alpha,N} = (2\pi\alpha)^{-N/2}\int_{N}{\exp\left(-\frac{1}{2\alpha}\norm{x}^2_N\right)\Re\hat\mu(x)dx}$$

The reason we took this whole detour is because now we can relate $I_{\alpha,N}$ to the continuity of $\hat\mu$. As a starting point, we have the following inequalities which are all consequences of $\hat\mu$ being positive-semidefinite

$$\left\vert\hat\mu(x)\right\vert \leq \hat\mu(0) \qquad\qquad \Re\hat\mu(x) \geq -\hat\mu(0)$$

Additionally the continuity of $\hat\mu$ with respect to (the topology induced by) $\norm{}_T$ implies that for every $\eps>0$ there exists $\delta>0$ such that

$$\norm{x}_T<\delta \implies |\hat\mu(x)-\hat\mu(0)|<\eps$$

All of this tells us something about the behavior of $\Re\hat\mu(x)$ as a "function" of $\norm{x}_T$ (the norm does not actually determine this value, but it's good enough to set our bounds):

- In a $\delta$-neighborhood of $0$, $\Re\hat\mu(x)$ is bounded from below by $\hat\mu(0)-\eps$.

- Outside of the $\delta$-neighborhood, $\Re\hat\mu(x)$ is bounded from below by $-\hat\mu(0)$.

Motivated by this, suppose we had a function $\Omega : \R \to \R$ such that

$$\begin{cases}
	\Omega(y)\leq 1 & \text{on }|y|<1 \\
	\Omega(y)<-1 & \text{on }|y|\geq 1
\end{cases}$$

Then it would yield us the following lower bound

$$\Re\hat\mu(x) \geq \Omega(\norm{x}_T/\delta)\hat\mu(0) - \eps$$

In theory this bound may be very very crude. Actually, we are going to choose such crude bound: $\Omega(y) := 1-2y^2$. This becomes very negative for large $\vert y\vert$, but overall this won't have much effect due to the Gaussian's rapid decay. By plugging this bound back into the integral, and undoing the Fourier transform, I ended up with

$$I_{\alpha,N} > \hat\mu(0) - \eps - \hat\mu(0)\cdot\E_\alpha[2\norm{x}_T^2/\delta^2]$$

where $\E_\alpha$ means integration (or, expectation value) against a Gaussian $g_\alpha$.

The constant $2/\delta^2$ can be pulled outside of it by linearity, so we are just left with needing to determine $$\E_\alpha[\norm{x}^2_T]$$ which by assumption equals $$\E_\alpha[\norm{Tx}^2]$$. Keep in mind $x$ is not an arbitrary vector in $E$ but specifically one in $N$. Computing this expectation involves some ugly work with integrals, so I won't write here the final answer but just denote it by

$$\E_\alpha[\norm{x}^2]\cdot\norm{T|_N}_{HS}^2$$

The first factor is, essentially by definition, the covariance of the Gaussian measure $g_\alpha$, which is $\alpha$. The second term is like the Hilbert-Schmidt norm, but only a finite sum of it, corresponding to the subspace $N$. Hence this is what our bound looks like

$$I_{\alpha,N} > \hat\mu(0) - \eps - \frac{2\alpha\hat\mu(0)}{\delta^2}\norm{T|_N}_{HS}^2$$

When we take $N$ larger and larger, the Hilbert-Schmidt norm converges to something finite, because that's literally how Hilbert-Schmidt-ness is defined. Subsequently when we take $\alpha\to 0$ the entire last term in the bound will vanish, and we'd be left with just

$$\mu(M') \geq \hat\mu(0)-\eps$$

Lastly, recall that this holds for arbitrary $\eps$, so in fact

$$\mu(M') \geq \hat\mu(0) = \mu(E^\sharp)$$

which completes the proof! $\square$


#### Footnotes
[^1]: Jiasheng Lin. (2025). Constructive Quantum Field Theory on Curved Surfaces and Related Topics. [arxiv:2507.21655](https://arxiv.org/pdf/2507.21655).

[^2]: Yamasaki, Y. (1985). Measures on Infinite Dimensional Spaces. doi:10.1142/0162.

[^3]: I feel like continuity should be automatic from our other assumptions, but haven't spent much time thinking about this.