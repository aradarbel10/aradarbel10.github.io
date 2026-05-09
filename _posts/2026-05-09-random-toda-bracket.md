---
layout: post
title: Computing one arbitrary Toda bracket for absolutely no reason at all
subtitle: And some other incomplete thoughts
---

I really intended to blog more, yet my past few weeks have been mostly learning lots of cool new stuff while feeling guilty for not writing about any of them. But the previous post I wrote was about the joy of going into little unexpected deep dives, so I figured I'd rather write about something small & mundane than not-write about something deep and polished.


It all started when I was perusing through Mahowald & Tangora's paper doing computations in the Adams spectral sequence[^1], as one does, and pondered some of their results. Right off the bat, in Theorem 2.1 they resolve the extension problem in $\pi_{23}$ through a fairly standard Toda bracket argument which seemed not too hard to reproduce. A key point in their argument is the following bracket:

$$\eta \bar\kappa = \langle \nu,2\nu,\kappa \rangle$$

They attribute this fact to Michael Barratt, so me, as an experienced rabbit-hole explorer and obsessive pdf hoarder, went straight to the list of references only to find this disappointing citation:

<h4 style="text-align: center; font-style:bold"> 3. M. G. Barratt, Seattle Conference notes, 1963. </h4>

and after a while of digging around, I found a scan of the lecture notes[^2] hosted by John Rognes, with annotations and a handwritten appendix by Paul Shick, including fairly detailed EHP tables for (unstable!) homotopy groups of spheres up to the 21st stem. After glancing through these tables a few times over I could find no trace of the homotopy classes $\kappa$ or $\bar\kappa$, but I was already too committed and too stubborn, and this whole set of notes looked way too cool to leave behind.

### The beginning of a family
Allow me to get started at the first neat pattern that I noticed: it's probably known to experts, and indeed was a major point in Barratt's 1963 lecture, that various interesting families of elements in the homotopy groups of spheres can be constructed by recursive use of Toda brackets: this generalizes the $\mu_{8k+1}$-family which I mentioned in passing in my [post]({% post_url /2025-11-16-adams-alpha-family %}) on Adams's $\alpha$-family. There are also the well-known periodicity operators of Adams and Mahowald which can be expressed neatly using Toda brackets.
Beyond that, Barratt lists the following examples defined mutually-recursively:

| Family name 	| First member	| Recursive step |
|:----------:|:--------:|:------:|
| $\mu$ | $\mu[0] = \eta$ | $\mu[n] = \langle\eta,2,a[n-1] \rangle$ |
| $\bar\mu$ | N/A | $\bar\mu[n] = \langle \eta,2,\mu[n] \rangle$ |
| $\zeta$ | ???[^3] | $\zeta[n] = \langle\nu,8,c[n] \rangle$ |
| $a$ | $a[0] = \langle\nu,8,\nu\rangle$ | $a[n] = \langle a[1],2,a[n-1]\rangle$ |
| $b$ | $$b[0]=\left\langle\nu\;\;\begin{matrix} \omega & 2 \\ \eta & \eta^2 \end{matrix}\right\rangle$$ | $b[n] = \langle b[1],4,b[n-1]\rangle$ |
| $c$ | $c[0] = \;<\\!\\!\iota,\iota\\!\\!>$ | $c[n] = \langle c[1],8,c[n-1]\rangle$ |
| $d$ | $d[0] = \sigma$ | $d[n] = \langle d[1],16,d[n-1]\rangle$ |

Barratt also lists multiplicative relations and Hopf invariant computations of most elements appearing here.

Visibly, some of Barratt's notations are different from the "standard" ones used by Toda. For instance, what Barratt calls $a[0]$ and also denotes $\tau''$ is what Toda calls $\sigma'''$; in the stable range this just becomes $8\sigma$.

**Remark:** About indexing: these families are all $8$-periodic, and if you read my post on the $\alpha$-family this shouldn't be too surprising. In general the notation should be interpreted as something like $x[k] = x_{8k+\ell}$. I'm less certain about what's going on with the last four families, their recursive definition doesn't really make sense -- I suspect the $a[1]$ should be replaced by $a[0]$ etc. This would be consistent for example with Barratt's definition of $$a^{17}_5 = \langle \tau'',2,\tau''\rangle$$ in the $15$-stem[^4]. I can already tell that these families are related to some intricacies that occur in the EHP computations of the 8-stem and onwards, though I'll have to look deeper into this in the future before I can promise anything definitive.

It may be noteworthy that, as far as I can tell, Barratt's use of the generalized bracket in $b[0]$ was the first written-down instance of a generalized Toda bracket, beyond the original secondary composition.

Anyways after this table, he remarks that "other members can be defined depending on the composition of $n$", which is quite vague, but it definitely made me wonder how far can this method be pushed? Can we get similar infinite families using 4-fold Toda brackets? Or higher? This brings me back to my observation: the element $\kappa$ was defined by Toda via an elaborate bracket construction, but nowadays we can re-interpret that construction much more conceptually as a 4-fold bracket:

$$\kappa = \langle\nu,\eta,2,\bar\nu\rangle$$

and $\bar\kappa$ is typically defined via an analogous process, which boils down to the 4-fold bracket:

$$\bar\kappa = \langle\nu,\eta,2,\kappa\rangle$$

Thus we recognize that Barratt's notation for $\kappa$ is "$\widetilde{\nu}$". What I like about this notation is the fact that it naturally fits into the sequence $\nu \mapsto \bar\nu \mapsto \widetilde\nu$ and, although Barratt doesn't give any special notation to the next member of this sequence, our $\bar\kappa$ fits perfectly. It can be interesting to think about how the sequence continues.

### Background bracket blabber
I admittedly cannot see how the bracket claimed by Tangora & Mahowald follows from Barratt's notes. There are some other scans of the lecture notes circulating online which are missing some of the pages that appear in the copy I linked[^2], so maybe there are even more pages I don't know about. As the next best alternative I resort to a similar proof by Mimura[^5] (Lemma 6.1).

In his paper, Mimura lays much of the theoretical groundwork necessary for computing stems $21$ through $23$, and in particular developed 4-fold Toda brackets. So I found it quite funny that in the proof of Lemma 6.1, he still employs to the more indirect type of construction like the one used by Toda to define $\kappa$; perhaps this is because he wanted to use a certain "juggling identity" for 3-fold Toda brackets that doesn't really work for 4-fold ones. In the next subsection I will show an alternative identity that makes the proof nicer, but for now let's see what Mimura says.

There are two relevant juggling relations relevant here, both proved originally by Toda:
1. the "internal juggling" $\langle \alpha\beta,\gamma,\delta \rangle \subseteq \langle \alpha,\beta\gamma,\delta \rangle$.
2. the "external juggling" $\alpha\langle\beta,\gamma,\delta\rangle = \langle\alpha,\beta,\gamma\rangle\delta$.

These identities all hold whenever all the brackets are defined (at least up to signs and suspensions which I sacrificed for the sake of over-simplicity). Although I don't wanna get into proving these identities here, it may be beneficial to at least recall how Toda brackets are defined.

**Construction:** Suppose $W \xrightarrow{f} X \xrightarrow{g} Y \xrightarrow{h} Z$ is a sequence of composable maps, where the composite of every consecutive pair is null-homotopic. The *extension set* of $h$ (by $g$) is the set of all maps $\operatorname{cofib}(g) \to h$ whose restriction back to $Y$ recovers $h$. Sort of dually, the *coextension set* of $f$ (by $g$) is the set of all maps $\Sigma W \to \operatorname{cofib}(g)$ whose projection along $\operatorname{cofib}(g) \to \Sigma X$ recovers $\Sigma f$. We denote these sets by $\operatorname{ext}(h)$ and $\operatorname{coext}(f)$ respectively, with the map $g$ remaining implicit from the notation.

In pictures, co/extensions are all the possible maps fitting into these squares[^7]:
<center><iframe class="quiver-embed" src="https://q.uiver.app/#q=WzAsOCxbMCwwLCJXIl0sWzIsMCwiWCJdLFs0LDAsIlkiXSxbNiwwLCJaIl0sWzQsMiwiXFxvcGVyYXRvcm5hbWV7Y29maWJ9KGcpIl0sWzIsMSwiXFxvcGVyYXRvcm5hbWV7Y29maWJ9KGYpIl0sWzIsMiwiXFxTaWdtYSBXIl0sWzYsMiwiWiJdLFswLDEsImYiXSxbMSwyLCJnIl0sWzIsMywiaCJdLFsyLDRdLFsxLDVdLFs1LDZdLFs2LDQsIlxcb3BlcmF0b3JuYW1le2NvZXh0fShmKSIsMix7ImNvbG91ciI6WzMwMCw2MCw2MF19LFszMDAsNjAsNjAsMV1dLFszLDcsIiIsMCx7ImxldmVsIjoyLCJzdHlsZSI6eyJoZWFkIjp7Im5hbWUiOiJub25lIn19fV0sWzQsNywiXFxvcGVyYXRvcm5hbWV7ZXh0fShoKSIsMix7ImNvbG91ciI6WzI0MCw2MCw2MF19LFsyNDAsNjAsNjAsMV1dXQ==&embed" width="700" height="300" style="border-radius: 8px; border: none;"></iframe></center>

Observe that $\operatorname{ext}(h)$ is nonempty iff a null-homotopy $hg\simeq 0$ exists, and $\operatorname{coext}(f)$ is nonempty iff $gf \simeq 0$ exists. Now we define the *Toda bracket* $\langle h,g,f \rangle$ to be the set of all possible maps $\Sigma W \to Z$ obtained as a composite of an extension and a coextension. One can show that this set is in fact a coset of some subgroup in $[\Sigma W,Z]$ called the *indeterminacy* of the bracket[^6]. We often abusively treat these sets as actual elements, especially when they are singleton sets (aka when there's "no indeterminacy").

Conceptually, the reason Toda brackets exist is because the two null-homotopies $gf\simeq 0$ and $hg\simeq 0$ induce two (usually distinct) null-homotopies of the whole composite $hgf$, and these can be used to form a "loop"

$$0 \simeq (hg)f = h(gf) \simeq 0$$

Rigorously that is an element of $\pi_1\operatorname{Map}(W,Z)$ or equivalently an element of $[\Sigma W,Z]$, just like we've defined. The premise of higher brackets is to generalize this, either to longer sequences of maps, or to more intricate shapes of diagrams.

An ad-hoc definition for 4-fold brackets can be given as

$$\langle h,g,f,e \rangle := \langle h,\operatorname{ext}(g),\operatorname{coext}(e)\rangle$$

where the co/extension sets are implicitly with respect to $f$. Of course for this to be nonempty various null-homotopies must exist. Now I can tell you more officially that Toda's original definition of

$$\kappa = \langle \nu,\operatorname{ext}(\eta),\operatorname{coext}(\bar\nu)\rangle$$

which is just a spelled-out form of the $4$-fold bracket mentioned earlier. Similarly,

$$\bar\kappa = \langle \nu,\operatorname{ext}(\eta),\operatorname{coext}(\kappa)\rangle$$

### Proof of the bracket a la Mimura
In order to prove the claim $\eta\bar\kappa \in \langle\nu,2\nu,\kappa\rangle$, thanks to internal juggling it'd suffice to prove instead $\eta\bar\kappa \in \langle\nu^2,2,\kappa\rangle$. This is what Mimura does. Beware that I'm being very uncautious about keeping track of indices and which sphere each element is supported on. Let's begin by just plugging in the definition of $\bar\kappa$ discussed a moment ago

$$\begin{align*}
\eta\bar\kappa
&= \eta\circ\langle \nu,\operatorname{ext}(\eta),\operatorname{coext}(\kappa)\rangle \\
&= \langle\eta,\nu,\operatorname{ext}(\eta)\rangle\circ\operatorname{coext}(\kappa) \\
&\subseteq \operatorname{ext}(\nu^2)\circ\operatorname{coext}(\kappa) \\
&= \langle\nu^2,2,\kappa\rangle
\end{align*}$$

All co/extension sets are implicitly taken wrt $2$. This is what we wanted to show! The only non-obvious part is the containment in the 3rd row. That is, $\langle \eta,\nu,\operatorname{ext}(\eta)\rangle \subseteq \operatorname{ext}(\nu^2)$? If we let $p : \mathbb{S} \to \mathbb{S}/2$ denote the cofiber projection, then this amounts to showing

$$\langle\eta,\nu,\operatorname{ext}(\eta)\rangle\circ p \stackrel{?}{=} \nu^2$$

Now using another form of the internal juggling formula, we can push this $p$ into the bracket and obtain

$$\langle \eta,\nu,\operatorname{ext}(\eta)\rangle\circ p \subseteq \langle \eta,\nu,\operatorname{ext}(\eta)\circ p\rangle = \langle \eta,\nu,\eta\rangle = \nu^2$$

as desired. The last equality here is one of Toda's classical bracket computations; it may seem arbitrary at first, but actually follows a general pattern. Namely in the Adams spectral sequence we have the Massey product identity $\langle h_n,x,h_n\rangle = h_{n+1}x$ where $h_n$ is the $n$th Hopf element -- so we should expect that bracketing from both sides with a Hopf element is the same as multiplying by the next Hopf element. But famously the only Hopf elements that actually survive through the spectral sequence are $h_0,h_1,h_2,h_3$ represented by the classical Hopf fibrations $2,\eta,\nu,\sigma$ respectively.

This sort of heuristic argument relies on a central theorem in computational homotopy theory: *Moss's convergence theorem*, which roughly states that, under nice circumstances, Massey products converge to Toda brackets in the Adams spectral sequence. Actually, the bracket I'm trying to prove can also be obtained directly from the Moss convergence theorem, as is done by Isaksen[^10] (Lemma 3.3.58)[^11].

But rather than rewrite $\bar\kappa$ as a $3$-fold bracket, as in Mimura's proof, it may be tempting to apply the corresponding juggling formula on the $4$-fold bracket itself:

$$\eta\bar\kappa = \eta\langle\nu,\eta,2,\kappa\rangle = \langle\eta,\nu,\eta,2\rangle\kappa$$

The problem with this idea is that the RHS is not even defined! We already know now the sub-bracket $\langle\eta,\nu,\eta\rangle$ contains $\nu^2$, making it nonzero. The correct juggling identity for higher brackets looks like so:

$$\alpha\langle \beta,\gamma,\delta,\epsilon\rangle \subseteq \langle\langle \alpha,\beta,\gamma\rangle,\delta,\epsilon\rangle$$

and indeed, once we apply this and use Toda's classical bracket, we directly get what we wanted

$$\eta\bar\kappa = \eta\langle \nu,\eta,2,\kappa\rangle = \langle \langle\eta,\nu,\eta\rangle 2,\kappa\rangle = \langle \nu^2,2,\kappa\rangle \subseteq \langle \nu,2\nu,\kappa\rangle$$

The juggling formula is listed as Theorem 2.35(6) in the review article of Isaksen-Wang-Xu[^8], who further reference us to Kochman's book[^9] where it appears as Theorem 2.3.6. However Kochman uses a slightly different formalism of Toda brackets, dealing explicitly with "defining system" analogously to Massey products. I guess my argument above (which is glanced over even by Mimura) should generalize quite easily to a proof of the general case.


#### Footnotes
[^1]: Mark Mahowald, and Martin Tangora (1967). Some differentials in the Adams spectral sequence. Topology, 6(3), p.349-369. [Available here](https://www.uio.no/studier/emner/matnat/math/MAT9580/gamle-undervisningsressurser/varen-2015/undervisningsmateriale/mahowald-tangora-topology-1967.pdf).

[^2]: [Available here](https://www.mn.uio.no/math/personer/vit/rognes/articles/barratt/barratt-notes----seattle-1963.pdf).

[^3]: For some reason this is blank in Barratt's notes, and I'm not sure if it's intentional or some scanning defect. Typically the first element in the $\zeta$-family is defined as $\langle \nu,8,2\sigma \rangle$ which resembles the recursion step. On the other hand, Barratt's list says this element is supported on $S^4$ and yet $\zeta$ is only born on $S^5$.

[^4]: This appears in the second row under the "constructions" title from page 12 of his notes (footnote 2).

[^5]: Mamoru Mimura (1964). On the generalized Hopf homomorphism and the higher composition, Part I. Journal of Mathematics of Kyoto University, 4(1), 171 – 190. [Available here](https://projecteuclid.org/journalArticle/Download?urlId=10.1215%2Fkjm%2F1250524712).

[^6]: $[\Sigma W,Z]$ denotes the collection of homotopy classes of maps $\Sigma W \to Z$. This obtains a group structure due to $\Sigma W$ being a cogroup -- a generalization of the fact that $\pi_1(Z) = [\Sigma S^0,Z]$ is a group. This is described in a bit more detail in one of my [previous posts]({% post_url /2025-10-13-yoneda-lemma-perspectives %}) on the Yoneda lemma.

[^7]: Coextension maps are also required to satisfy a commutativity condition with a square not shown here. Obviously the displayed left-hand square commutes automatically: the vertical composite on the left face is null, and the composite of the top and right faces is also null.

[^8]: Isaksen, D.C., Wang, G. & Xu, Z. Stable homotopy groups of spheres: from dimension 0 to 90. Publ.math.IHES 137, 107–243 (2023)

[^9]: Stanley O. Kochman, Stable homotopy groups of spheres: A Computer-Assisted Approach, Lecture Notes in Mathematics, vol. 1423, Springer-Verlag, Berlin, 1990.

[^10]: Isaksen, D. (2014). Stable Stems. Memoirs of the American Mathematical Society.

[^11]: The reason I insist on not using this is because all the other articles I referenced seem to suggest there's a different proof, and obviously I care more about the proof than the actual result. I have a feeling the proof I presented here is fairly close to the original!