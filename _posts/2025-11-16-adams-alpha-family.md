---
layout: post
title: Adams's alpha family in stable homotopy
subtitle: A historical review
---

Periodicity phenomena are a **big deal** in modern stable homotopy theory, and chromatic homotopy in particular. The first periodic family, which largly inspired the development of the chromatic perspective to begin with, is the $\alpha$-family constructed by Adams (and partially by Toda). This is carried out in his monumental 1965 paper, "On the groups $J(X) - IV$" -- a very enjoyable paper in my opinion, and one of the absolute classics that every homotopy theorist should read. Later, the construction of the $\alpha$-family was generalized to what we now call the *Greek letter construction*.

More specifically, periodicity arises from the existence of $v_n$-self maps: these are maps of the form $\Sigma^k Y \to Y$ (where $Y$ is some finite spectrum) which induce an isomorphism on the Morava $K$-theory of height $n$. Indeed, if a map induces an isomorphism on *any* cohomology theory, then that map must be nontrivial, and all of its iterates will also induce isomorphisms on cohomology, whence they are also nontrivial, and so we get an interesting periodic family of maps. If moreover you compose these with a map from a sphere to $Y$ and then from $Y$ back to a sphere, you'd get a periodic family of elements in the stable stem -- however nothing guarantees that these elements will be nonzero!

Unfortunately the reality is not so friendly to us. The spectra $Y$ used in the Greek letter construction are the elusive *Smith-Toda complexes* or more generally *Generalized Moore complexes*. The Smith-Toda complex used in constructing specifically the $\alpha$-family is actually really simple, it's just the classical Moore complex (or spectrum) $\mathbb{S}/p$. For $p\geq 3$ this complex does admit a $v_1$-periodic map of minimal periodicity, meaning that the isomorphism it induces on $K(1)$-theory is precisely multiplication by the generator $v_1$. In contrast, at $p=2$ the minimal periodicity is only $v_1^4$. This is the topic of the current post.

**Remark:** As a rule of thumb, construction of Smith-Toda complexes gets harder for the lower primes. For instance, the next self-map at $p=2$ is $v_2^{32}$. Similarly at the prime $p=3$, at height $1$ there actually does exist a $v_1$-self map, but at height $2$ the best we can do is $v_2^9$. Not much is known beyond those, and proving existence/non-existence of Smith-Toda complexes is one of the greatest mysteries of the field.

Nowadays, Greek letter elements are studied primarily via the classical Adams spectral sequence, or the Adams-Novikov spectral sequence, but when Adams originally constructed his $\alpha$-family this fancy language was not yet available. So if you try reading Adams's paper you will not find any mention of $v_n$-maps or anything like that. My goal here is to explicitly connect his construction to the modern perspective.


### Strategy
In the above, I started from saying how we want periodic families in the stable stem, and to get those we look for self-maps on some auxilary complex. I remind: we seek a map $A : \Sigma^k Y \to Y$ such that $A,A^2,A^3,\cdots$ are all nontrivial, and once we have that we can define the elements $\alpha_t \in \pi_{kt}\mathbb{S}$ by

$$\Sigma^{kt}\mathbb{S} \xrightarrow{i} \Sigma^{kt}Y \xrightarrow{A^r} Y \xrightarrow{j} \mathbb{S}$$

where $i,j$ are some other maps. As mentioned earlier, the case I have in mind will use the Moore spectrum $Y = \mathbb{S}/p$, and the maps $i : \mathbb{S} \to \mathbb{S}/p$ and $j : \mathbb{S}/p \to \mathbb{S}^1$ will be respectively the bottom-cell inclusion and the top-cell projection.

**Remark:** At the prime $2$, most of Adams's attention is on the case where $i$ is, still, the bottom-cell inclusion, but where $j$ is a map $\overline\eta$, a certain lift of the Hopf fibration. The resulting families of elements are his famous $\mu_r$-families (for $r\equiv 1,2\mod 8$)[^3].

But notice that the existence of a self-map on $\mathbb{S}/p$ is equivalent to that of a self-map on $\mathbb{S}$ whose order in the homotopy group is $p$. So to construct the family $\alpha_t$, Adams started from just finding an appropriate $\alpha_1$, then recovering $A$ from that, and only then extending $\alpha_t$ to all $t\geq 1$.

### Details for arbitrary $p$
Before carrying out this plan, I must mention a well-known simplification: the spectrum $K(1)$ at a prime $p$ (which is commonly implicit in the notation) may be identified with a wedge of $p-1$ copies of the $p$-local topological $K$-theory spectrum, $KU_{(p)}$, so they really contain the same information. The element $v_1$ in $K(1)$ corresponds to the Bott element of $KU$. In this sense, the chromatic height $1$ is "just" topological $K$-theory, in the same way that height $0$ is just rational homotopy.

Adams's $d$-invariant[^1] of a morphism is merely a fancy name for the induced morphism on cohomology (or in this case, $KU$-theory), and requiring multiplication by $v_1$ amounts to having $d$-invariant equal to $1$. The $e$-invariant is a bit more intricate to define, so I'll refer you to the paper for that (or any textbooks on homotopy theory). Starting from $\alpha$, we get $A$ using the following lemma, whose proof is straightforward:

**Lemma (Adams, 12.5):** Assume $k$ is odd, and have $\alpha \in \pi_k\mathbb{S}$. Fix any integer $m$, and suppose $\alpha$ satisfies the following criteria:
1. $\alpha$ has order dividing $m$, i.e. $m\alpha = 0$.
2. $\\{m,\alpha,m\\} = 0 \mod m$ (the Toda bracket is defined thanks to the first criterion).

Then there's a self-map $A$ making the following square commute (where $i,j$ are the inclusion and projection):
<center><iframe class="quiver-embed" src="https://q.uiver.app/#q=WzAsNCxbMCwwLCJcXG1hdGhiYntTfV5rL20iXSxbMiwwLCJcXG1hdGhiYntTfV57LTF9L20iXSxbMCwyLCJcXG1hdGhiYntTfV5rIl0sWzIsMiwiXFxtYXRoYmJ7U30iXSxbMiwzLCJcXGFscGhhIiwyXSxbMCwxLCJBIl0sWzEsMywiaiJdLFsyLDAsImkiXV0=&embed" width="600" height="250" style="border-radius: 8px; border: none;"></iframe></center>

Since we aim for the $d$-invariant of $A$ (equivalently of $jA$) to be $1$, the following relation will be found fruitful (Adams, Proposition 3.2.b, Proposition 12.2):

$$d(jA) = -m\cdot e(\alpha)$$

Hence we seek $\alpha$ with $e$-invariant equal to $-\frac{1}{m}$. All that remains is to actually find such $\alpha=\alpha_1$ in the stable stem satisfying the criteria of the lemma. Once we have that, we use the recipe to construct the whole family $\alpha_t$.

**Remark:** The lemma only works for $\alpha$ whose degree $k$ is odd, hence $A$'s degree is even. This does not restrict us, as $v_n$-self maps are necessarily of even degree.

### Specifics at odd primes
Adams proves (Lemma 12.4) that when $p$ is an odd prime, and $m$ is a power of $p$, then the desired element $\alpha$ exists. For simplicity I focus on the case $m=p$.

Recall Serre's torsion result: for each prime $p$, the groups $\pi_*\mathbb{S}$ do not contain any $p$-torsion in degree $\ast < 2p-3$. The first $p$-primary part occurs in degree $2p-3$, and it's precisely a cyclic summand of the form $\mathbb{Z}/p$. One can show[^2] that any nonzero element here satisfies the criteria.

Therefore, at odd $p$, we are able to obtain a $v_1$-self map on $\mathbb{S}/p$ of degree $2p-3+1 = 2(p-1)$ and hence $\alpha_t \in \pi_{2t(p-1)-1}\mathbb{S}$. These are all nontrivial since they have nonzero $e$-invariant.

### Specifics at $p=2$
Now for the more interesting case. This will rely on the structure of the $J$-homomorphism as studied by Adams. Recall that this is the map $J : \pi\_\*{SO} \to \pi\_\*\mathbb{S}$ defined by sending any orthogonal automorphism of $\mathbb{R}^m$ to the induced self-equivalence of $S^m = \mathbb{R}^m\cup\infty$, and then stabilizing. Upon this stabilization, Bott periodicity says $\pi_{4k-1}{SO} \cong \mathbb{Z}$ for all $k$. This will map onto some cyclic subgroup of $\pi_{4k-1}\mathbb{S}$, and Adams incredibly determined the order of this subgroup:

**Theorem (Adams):** $\|\operatorname{Im}J\_{4k-1}\| = m(2k)$ where $m(2k)$ is the denominator of $\frac{B\_{2k}}{4k}$ written as a reduced fraction, where $B\_{2k}$ is the $2k$-th Bernoulli number.

The case I'm interested in is $k=2$ hence $4k-1 = 7$. The corresponding Bernoulli number is $B_4 = -\frac{1}{30}$, hence $m(4) = 30\cdot 8 = 240$. On the other hand, explicit computations of the stable stem already show $\pi_7\mathbb{S} \cong \mathbb{Z}/240$ generated by the octonionic Hopf fibration, usually denoted $\sigma$. Thus the image of $J$ in degree $7$ is the whole thing! As a matter of fact, the isomorphism $\pi_7\mathbb{S} \to \mathbb{Z}/240$ is given precisely by the $e$-invariant.

All that hints for us to take $\alpha = 120\sigma$. This indeed has order $2$. As for its $e$-invariant, this is just the class of $120$ mod $240$. After identifying $\mathbb{Z}/240$ as a subgroup of $\mathbb{Q}/\mathbb{Z}$, this just becomes $\frac{1}{2}$. The element we are after should actually have $e$-invariant $-\frac{1}{2}$, but this is defined modulo $\mathbb{Z}$ and so $\frac{1}{2} \equiv -\frac{1}{2}$.

The last criterion we have to verify is the Toda bracket. This follows from one of Toda's most basic identities: if $\alpha$ is divisible by $2$ (as it is in our case) then

$$\{2,\alpha,2\} = \alpha\eta = \frac{\alpha}{2}\cdot 2\eta = 0$$

as desired. Note that $\sigma$ is in degree $7$, so the resulting self map of $\mathbb{S}/2$ will be in degree $8$. Hence we only get from here a $v_1^4$-self map at $p=2$.

### Minimality
Does $\mathbb{S}/2$ admit a $v_1$ map of lower periodicity than $4$? If it did, then by the previous argument, it should come from some element of $\pi_*\mathbb{S}$ with $e$-invariant equal to $\frac{1}{2}$. The computation of the stable stem in degrees up to $7$ is classical, and can be found e.g. in Toda's book. Here are all the elements of order $2$:

$$\begin{array}{c | c}
  \ast & \text{order $2$ elements in $\pi_*\mathbb{S}$} \\ \hline
  0 & \tiny{\text{N/A}} \\
  1 & \eta \\
  2 & \eta^2 \\
  3 & 12\nu \\
  4 & \tiny{\text{N/A}} \\
  5 & \tiny{\text{N/A}} \\
  6 & \nu^2 \\
  7 & 120\sigma \\
\end{array}$$

Let's compute all their $e$-invariants. In degrees $2$ and $6$ the image of $J$ is trivial, and recall that the linear complement to the image of $J$ is precisely the kernel of the $e$-invariant. That is to say, $\eta^2$ and $\nu^2$ must have trivial $e$-invariant, and not $\frac{1}{2}$.

The other interesting cases $\eta$ and $\nu$ do indeed belong to the image of $J$. The whole point of Adams's paper is in fact to compute the image of $J$, so along the way he computed all the $e$-invariants of everything there. $e(\eta)$ actually does happen to be $\frac{1}{2}$, but the Toda bracket criterion fails; again from the fundamental Toda identity,

$$\{2,\eta,2\} = \eta^2$$

This time we cannot divide $\eta$ by $2$ so the result is nonzero.

Lastly in degree $3$, the $e$-invariant defined with respect to *real* $KO$-theory defines an isomorphism $\pi_3\mathbb{S} \to \mathbb{Z}/24$ similarly to what happened in degree $7$. Consequently the real $e$-invariant of $12\nu$ is indeed $\frac{1}{2}$. However we are only considering $e$-invariants against the *complex* $KU$-theory. It turns out that the complex version equals double the real version, so the actual (complex) $e$-invariant of $12\nu$ is $1\equiv 0\mod\mathbb{Z}$.

This completes the proof of minimality for the periodicity of $v_1^4$ at $p=2$.


#### Footnotes
[^1]: All $d$- and $e$-invariants in this post are with respect to the spectrum $KU$.
[^2]: I think this should be pretty easy with the EHP sequence, though I haven't checked.
[^3]: Adams described his $\mu$-family as something "every homotopy theorist know and love, but need not concern anyone else."