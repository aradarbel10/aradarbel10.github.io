---
layout: post
title: Four proofs of the four lemma
---

<div style="display:none">
$$
\let\eqq\equiv
\let\iso\cong
\let\equiv\simeq
\let\cong\eqq

\newcommand{\clA}{\mathcal{A}}
\newcommand{\op}{\mathsf{op}}

\DeclareMathOperator{\ker}{ker}
\DeclareMathOperator{\coker}{coker}
\DeclareMathOperator{\im}{im}

\newcommand{\qed}{\square}
\newcommand{\xto}[1]{\xrightarrow{#1}}
\newcommand{\xot}[1]{\xleftarrow{#1}}
\newcommand{\too}{\xrightarrow{\qquad}}
\newcommand{\down}{\downarrow}
$$
</div>


The four lemma is one of the classic results in homological algebra.

**Lemma (four):** In an abelian category $\clA$, consider the following diagram with exact rows

<center><iframe class="quiver-embed" src="https://q.uiver.app/#q=WzAsOCxbMCwyLCJBIl0sWzIsMiwiQiJdLFs0LDIsIkMiXSxbNiwyLCJEIl0sWzAsMCwiQSciXSxbMiwwLCJCJyJdLFs0LDAsIkMnIl0sWzYsMCwiRCciXSxbNCw1LCJmJyJdLFs1LDYsImcnIl0sWzYsNywiaCciXSxbMCwxLCJmIiwyXSxbMSwyLCJnIiwyXSxbMiwzLCJoIiwyXSxbNCwwLCJhIiwwLHsic3R5bGUiOnsiaGVhZCI6eyJuYW1lIjoiZXBpIn19fV0sWzUsMSwiYiIsMCx7InN0eWxlIjp7InRhaWwiOnsibmFtZSI6Im1vbm8ifX19XSxbNiwyLCJjIl0sWzcsMywiZCIsMCx7InN0eWxlIjp7InRhaWwiOnsibmFtZSI6Im1vbm8ifX19XV0=&macro_url=https%3A%2F%2Fgist.githubusercontent.com%2Faradarbel10%2Fb00a36db72c3910b28e445ec79e330a7%2Fraw%2Fef764c249491d2e2be0039c5886810973b50ed72%2Fpreamble.sty&embed" width="600" height="300" style="border-radius: 8px; border: none;"></iframe></center>

If $b$ and $d$ are monic, and $a$ is epic, then $c$ is monic.

Today I embark on an educational journey to present four different proofs for this innocent-looking statement.


## Four different proofs

### Proof \#1 - elementary approach
When I say the word "elementary" in math, I don't necessarily mean that it's simple, but rather that it relies on elements in sets (often these two properties correlate). Indeed, it is a well-known result of Peter Freyd and Barry Mitchell that any small abelian category is (equivalent to) a full-subcategory of a category of modules over a unital ring.

In our case, since we are talking about a very finite diagram in $\clA$, we are allowed to assume that we're working only in a small subcategory of $\clA$. In particular, one which contains all the objects and morphisms in the four lemma's diagram, along with all their co/products, co/kernels, and everything else needed for a subcategory to be abelian.

Hence it would suffice to prove the four lemma in the case where all the objects are modules and the morphisms between them are linear maps.

Note, throughout this proof I will write function application by juxtaposition: If $X,Y$ are sets (or modules), $f:X\to Y$ a function, and $x\in X$ an element, then we have an element $fx \in Y$ which is usually denoted by $f(x)$. The reason for my peculiar choice of notation will become clear later.

Before finally seeing the proof, here is the diagram again for reference.
<center><iframe class="quiver-embed" src="https://q.uiver.app/#q=WzAsOCxbMCwyLCJBIl0sWzIsMiwiQiJdLFs0LDIsIkMiXSxbNiwyLCJEIl0sWzAsMCwiQSciXSxbMiwwLCJCJyJdLFs0LDAsIkMnIl0sWzYsMCwiRCciXSxbNCw1LCJmJyJdLFs1LDYsImcnIl0sWzYsNywiaCciXSxbMCwxLCJmIiwyXSxbMSwyLCJnIiwyXSxbMiwzLCJoIiwyXSxbNCwwLCJhIiwwLHsic3R5bGUiOnsiaGVhZCI6eyJuYW1lIjoiZXBpIn19fV0sWzUsMSwiYiIsMCx7InN0eWxlIjp7InRhaWwiOnsibmFtZSI6Im1vbm8ifX19XSxbNiwyLCJjIl0sWzcsMywiZCIsMCx7InN0eWxlIjp7InRhaWwiOnsibmFtZSI6Im1vbm8ifX19XV0=&macro_url=https%3A%2F%2Fgist.githubusercontent.com%2Faradarbel10%2Fb00a36db72c3910b28e445ec79e330a7%2Fraw%2Fef764c249491d2e2be0039c5886810973b50ed72%2Fpreamble.sty&embed" width="600" height="300" style="border-radius: 8px; border: none;"></iframe></center>

**Proof (1):**
We'd like to show $c$ is injective. Have any $z\in C'$ such that $cz = 0$.
Then $0 = hcz = dh'z$ so injectivity of $d$ implies $h'z = 0$, hence $z \in \ker h' = \im g'$.
Hence there is $y \in B'$ such that $g'y = z$.
So $0 = cz = cg'y = gby$ meaning $by \in \ker g = \im f$.
Therefore there exists $x\in A$ such that $fx=by$.
By surjectivity, there is $x' \in A'$ so that $ax' = x$, then $fax' = fx = by = bf'x'$, then by injectivity of $b$ we get $y = f'x'$.
Namely $y \in \im f' \subseteq \ker g'$ which means $g'y = z = 0$. $\qed$

Sadly, many mathematicians consider the embedding theorem somewhat frowned upon, and they wouldn't be satisfied with my proof. Let's see if we can make them feel better in the next proof.

### Proof \#2 - diagram chasing
Our next strategy will be very similar to the first proof, except we will not need to rely on the use of any elements. Instead, we will use some *universal properties magic*. In case you forgot the universal properties of monomorphisms, epimorphisms, pullbacks, etc, now would be a good time to remind yourself of them.

Note, throughout this proof I will write function composition by juxtaposition: If $X,Y,Z$ are objects and $X\xto{f}Y\xto{g}Z$ are morphisms between them, then we have a morphism $gf : X \to Z$ which is usually denoted by $g\circ f$. The reason for my peculiar choice of notation from earlier should now become clearer.

In this proof we start from the four lemma's diagram, and gradually add a few more pieces around it. The final monstrosity is depicted below, but please glance over it for now and only look at the relevant parts of the diagram as they become relevant during the proof.

<center><iframe class="quiver-embed" src="https://q.uiver.app/#q=WzAsMTQsWzEsNCwiQSJdLFszLDQsIkIiXSxbNSw0LCJDIl0sWzcsNCwiRCJdLFsxLDIsIkEnIl0sWzMsMiwiQiciXSxbNSwyLCJDJyJdLFs3LDIsIkQnIl0sWzUsMCwiWiJdLFs0LDEsIlxcaW0gZyciXSxbMywwLCJCJ1xceF97XFxpbSBnJ30gWiJdLFsyLDMsIlxcaW0gZiJdLFswLDAsIkFcXHhfe1xcaW0gZn0oQidcXHhfe1xcaW0gZyd9IFopIl0sWzEsMSwiWSJdLFs0LDUsImYnIl0sWzUsNiwiZyciXSxbNiw3LCJoJyJdLFswLDEsImYiLDJdLFsxLDIsImciLDJdLFsyLDMsImgiLDJdLFs0LDAsImEiLDAseyJzdHlsZSI6eyJoZWFkIjp7Im5hbWUiOiJlcGkifX19XSxbNSwxLCJiIiwwLHsic3R5bGUiOnsidGFpbCI6eyJuYW1lIjoibW9ubyJ9fX1dLFs2LDIsImMiXSxbNywzLCJkIiwwLHsic3R5bGUiOnsidGFpbCI6eyJuYW1lIjoibW9ubyJ9fX1dLFs4LDYsInoiXSxbNSw5LCIiLDAseyJzdHlsZSI6eyJoZWFkIjp7Im5hbWUiOiJlcGkifX19XSxbOSw2LCIiLDAseyJzdHlsZSI6eyJ0YWlsIjp7Im5hbWUiOiJtb25vIn19fV0sWzgsOV0sWzEwLDUsInkiLDJdLFsxMCw4LCJpIiwwLHsic3R5bGUiOnsiaGVhZCI6eyJuYW1lIjoiZXBpIn19fV0sWzAsMTEsIiIsMCx7InN0eWxlIjp7ImhlYWQiOnsibmFtZSI6ImVwaSJ9fX1dLFsxMSwxLCIiLDAseyJzdHlsZSI6eyJ0YWlsIjp7Im5hbWUiOiJtb25vIn19fV0sWzEwLDExLCJ5JyIsMl0sWzEyLDEwLCJwIiwwLHsic3R5bGUiOnsiaGVhZCI6eyJuYW1lIjoiZXBpIn19fV0sWzEyLDAsIngiLDJdLFsxMCw5LCIiLDIseyJzdHlsZSI6eyJuYW1lIjoiY29ybmVyIn19XSxbMTIsNCwiIiwwLHsic3R5bGUiOnsibmFtZSI6ImNvcm5lciJ9fV0sWzEzLDQsIngnIl0sWzEzLDEyLCJxIiwyLHsic3R5bGUiOnsiaGVhZCI6eyJuYW1lIjoiZXBpIn19fV1d&macro_url=https%3A%2F%2Fgist.githubusercontent.com%2Faradarbel10%2Fb00a36db72c3910b28e445ec79e330a7%2Fraw%2Fef764c249491d2e2be0039c5886810973b50ed72%2Fpreamble.sty&embed" width="800" height="400" style="border-radius: 8px; border: none;"></iframe></center>

**Proof (2):**
We will show $c$ is monic. Have any $z : Z \to C'$, and suppose $cz=0$.
Then $0 = hcz = dh'z$ so monicity of $d$ implies $h'z = 0$, so by the universal property of $\ker h' = \im g'$ there's a unique factorization through $Z \to \im g'$.
Take the pullback $y : B' \times_{\im g'} Z \to B'$. Clearly the new square with corners $Z,C',B',B'\times_{\im g'}Z$ is commutative, so $zi = g'y$.
Then $0 = czi = cg'y = gby$, hence by the universal property of $\ker g = \im f$ there's a unique $y' : B'\times_{\im g'} Z \to \im f$.
We take yet another pullback $x : A\times_{\im f}(B' \times_{\im g'} Z) \to A$, such that $fx = byp$.
The pullback of $x$ along $a$ yields $x' : Y \to A$ with $ax' = xq$. Then $fax' = fxq = bypq = bf'x'$ then by monicity of $b$ we get $ypq = f'x'$.
Then clearly $g'ypq = g'f'x' = 0$, and since $p,q$ are epic we get $g'y = 0$.
This implies $zi = 0$, and $i$ is also epic, so $z = 0$, as desired. $\qed$


Our second version of the proof is not much nicer than the first one. Arguably, it's a lot uglier and more tedious. However it does demonstrate a deeper point (actually if you haven't realized, this whole post is meant to demonstrate deeper points). There is no doubt the second proof is suspeciously similar to the first one: We just had to replace the elements of modules by morphisms into those modules, use universal properties of mono/epimorphisms instead of using injectivity/surjectivity, and we had to take categorical pullbacks instead of elements in the preimage.

This approach is sometimes called "generalized elements" in logical and algebraic contexts, or "generalized points" in geometric contexts.

For example in the category of sets, the elements of a set $X$ correspond to functions $\{\ast\} \to X$ from the singleton set. A function $A \to X$ may be thought of as an "$A$-shaped element of $X$", and these behave a lot like usual elements.  A function $f:X\to Y$ being a monomorphism means that for any two generalized elements $a,b:A\to X$ we will have that $fa = fb$ implies $a=b$. The similarity to regular injectivity of functions between sets is uncanny, and there is actually a whole "internal language" of working with the generalized elements of categories which reflects the outside world in interesting ways.

Sets are so simple, that most (all) of their properties can be discussed by using just their "global elements", i.e. functions $\{\ast\} \to X$. Many other structures in math are similar. However in some more exotic contexts, like categories of sheaves (aka topoi), or various algebro-geometric categories, working with just global elements is not enough. In other cases like abelian categories, we barely even have a very good notion of global elements to begin with, and then generalized elements are our tool of choice.

### Proof \#3 - the snake lemma
With the first two ugly proofs, and their life lesson, behind us, we can move on to a slightly more elegant approach. This proof will be a bit longer, but it's a nice exercise in homological algebra and uses one of the best tools it provides: the snake lemma.

Personally I like to think of the snake lemma like some sort of an "automatic element chaser". If you recall the proof of the snake lemma, you'll see there's a funny chase there, starting from the top-right of the diagram and gradually making your way to the bottom-left, in order to construct the connecting morphism. Now if you look back at our first (or second) proof of the four lemma, you may be able to spot a similar "sanke-y" chasing pattern, $A \xto{f} B \xot{b} B' \xto{g'} C'$. So if we can get our diagram into a form where the snake lemma is applicable, we could just plug it in and the snake shall do our chasing for us. Here is how it's going to look.

**Proof (3):**
#### Step 1 - Turning it into a snake.

<center><img width=200 height=200 src="https://i.gifer.com/B5Jn.gif" alt="turning it into a snake" /></center>

To prepare the diagram, we split $f$ and $g'$ to their epi-mono factorizations

<center><iframe class="quiver-embed" src="https://q.uiver.app/#q=WzAsMTIsWzAsMywiQSJdLFsyLDMsIkIiXSxbNCwzLCJDIl0sWzAsMSwiQSciXSxbMiwxLCJCJyJdLFs0LDEsIkMnIl0sWzEsNCwiXFxpbSBmJyJdLFsyLDQsIlxca2VyIGcnIl0sWzMsMCwiXFxpbSBnJyJdLFs0LDAsIlxca2VyIGgnIl0sWzYsMSwiRCciXSxbNiwzLCJEIl0sWzMsNCwiZiciXSxbNCw1LCJnJyJdLFswLDEsImYiLDJdLFsxLDIsImciLDJdLFszLDAsImEiLDAseyJzdHlsZSI6eyJoZWFkIjp7Im5hbWUiOiJlcGkifX19XSxbNCwxLCJiIiwwLHsic3R5bGUiOnsidGFpbCI6eyJuYW1lIjoibW9ubyJ9fX1dLFs1LDIsImMiXSxbMCw2LCJcXHRpbGRle2Z9IiwyLHsic3R5bGUiOnsiaGVhZCI6eyJuYW1lIjoiZXBpIn19fV0sWzYsMSwiaSIsMix7InN0eWxlIjp7InRhaWwiOnsibmFtZSI6Im1vbm8ifX19XSxbNyw2LCIiLDIseyJsZXZlbCI6Miwic3R5bGUiOnsiaGVhZCI6eyJuYW1lIjoibm9uZSJ9fX1dLFs4LDksIiIsMix7ImxldmVsIjoyLCJzdHlsZSI6eyJoZWFkIjp7Im5hbWUiOiJub25lIn19fV0sWzQsOCwiXFx0aWxkZXtnfSciLDAseyJzdHlsZSI6eyJoZWFkIjp7Im5hbWUiOiJlcGkifX19XSxbOCw1LCJqIiwwLHsic3R5bGUiOnsidGFpbCI6eyJuYW1lIjoibW9ubyJ9fX1dLFs1LDEwLCJoJyJdLFsyLDExLCJoIiwyXSxbMTAsMTEsImQiLDAseyJzdHlsZSI6eyJ0YWlsIjp7Im5hbWUiOiJtb25vIn19fV1d&macro_url=https%3A%2F%2Fgist.githubusercontent.com%2Faradarbel10%2Fb00a36db72c3910b28e445ec79e330a7%2Fraw%2Fef764c249491d2e2be0039c5886810973b50ed72%2Fpreamble.sty&embed" width="600" height="400" style="border-radius: 8px; border: none;"></iframe></center>

This yields a snakeable situation
<center><iframe class="quiver-embed" src="https://q.uiver.app/#q=WzAsOCxbMiwwLCJBJyJdLFs0LDAsIkInIl0sWzYsMCwiXFxrZXIgaCciXSxbNiwyLCJDIl0sWzQsMiwiQiJdLFsyLDIsIlxca2VyIGciXSxbMCwyLCIwIl0sWzgsMCwiMCJdLFswLDUsIlxcdGlsZGV7Zn1hIiwwLHsic3R5bGUiOnsiaGVhZCI6eyJuYW1lIjoiZXBpIn19fV0sWzEsNCwiYiIsMCx7InN0eWxlIjp7InRhaWwiOnsibmFtZSI6Im1vbm8ifX19XSxbMiwzLCJjaiJdLFswLDEsImYnIl0sWzEsMiwiXFx0aWxkZXtnfSciLDAseyJzdHlsZSI6eyJoZWFkIjp7Im5hbWUiOiJlcGkifX19XSxbNSw0LCJpIiwyLHsic3R5bGUiOnsidGFpbCI6eyJuYW1lIjoibW9ubyJ9fX1dLFs0LDMsImciLDJdLFs2LDVdLFsyLDddXQ==&macro_url=https%3A%2F%2Fgist.githubusercontent.com%2Faradarbel10%2Fb00a36db72c3910b28e445ec79e330a7%2Fraw%2Fef764c249491d2e2be0039c5886810973b50ed72%2Fpreamble.sty&embed" width="700" height="300" style="border-radius: 8px; border: none;"></iframe></center>

#### Step 2 - Letting the snake loose
Applying the snake lemma yields an exact sequence

$$\ker \tilde{f}a \too \ker b \too \ker cj \too \coker \tilde{f}a \too \coker b \too \coker cj$$

Specifically, we know $\ker b = 0$ and $\coker \tilde{f}a = 0$, so exactness implies that the object inbetween them, $\ker cj$, is also zero. $\ker cj = 0$ implies $cj : \ker h' \xto{j} C' \xto{c} C$ is monic.

#### Step 3 - conclusion
Ponder the following diagram
<center><iframe class="quiver-embed" src="https://q.uiver.app/#q=WzAsNixbMiwyLCJDJyJdLFsyLDQsIkMiXSxbNCwyLCJEJyJdLFs0LDQsIkQiXSxbMCwyLCJcXGtlciBoJyJdLFsyLDAsIloiXSxbMSwzLCJoIiwyXSxbMCwyLCJoJyJdLFs1LDAsInUiXSxbMCwxLCJjIl0sWzIsMywiZCIsMCx7InN0eWxlIjp7InRhaWwiOnsibmFtZSI6Im1vbm8ifX19XSxbNCwwLCJqIiwwLHsic3R5bGUiOnsidGFpbCI6eyJuYW1lIjoibW9ubyJ9fX1dLFs1LDQsInYiLDJdXQ==&macro_url=https%3A%2F%2Fgist.githubusercontent.com%2Faradarbel10%2Fb00a36db72c3910b28e445ec79e330a7%2Fraw%2Fef764c249491d2e2be0039c5886810973b50ed72%2Fpreamble.sty&embed" width="600" height="400" style="border-radius: 8px; border: none;"></iframe></center>

We still need to make use of the one assumption we so far ignored: monicity of $d$.

Indeed, to prove $c$ is monic have any $u: Z \to C'$ such that $cu=0$. That would imply $hcu = 0 = dh'u$, thus $h'u = 0$. Hence there's a unique $v : Z \to \ker h'$ such that $jv = u$. But then $cu = cjv = 0$, and since we've seen the composite $cj$ is monic, we get $v = 0$. So $u = jv = 0$, as desired. $\qed$

### Proof \#4 - spectral sequences
Now it's time to take out the *actual* big guns. The life lesson I want you to get out of this proof is: spectral sequences are fun.
Without further ado, let's start proving.

**Proof (4):** We will develop a spectral sequence corresponding to the double complex of the four lemma. We draw the diagram here again for reference:
<center><iframe class="quiver-embed" src="https://q.uiver.app/#q=WzAsOCxbMCwyLCJBIl0sWzIsMiwiQiJdLFs0LDIsIkMiXSxbNiwyLCJEIl0sWzAsMCwiQSciXSxbMiwwLCJCJyJdLFs0LDAsIkMnIl0sWzYsMCwiRCciXSxbNCw1LCJmJyJdLFs1LDYsImcnIl0sWzYsNywiaCciXSxbMCwxLCJmIiwyXSxbMSwyLCJnIiwyXSxbMiwzLCJoIiwyXSxbNCwwLCJhIiwwLHsic3R5bGUiOnsiaGVhZCI6eyJuYW1lIjoiZXBpIn19fV0sWzUsMSwiYiIsMCx7InN0eWxlIjp7InRhaWwiOnsibmFtZSI6Im1vbm8ifX19XSxbNiwyLCJjIl0sWzcsMywiZCIsMCx7InN0eWxlIjp7InRhaWwiOnsibmFtZSI6Im1vbm8ifX19XV0=&macro_url=https%3A%2F%2Fgist.githubusercontent.com%2Faradarbel10%2Fb00a36db72c3910b28e445ec79e330a7%2Fraw%2Fef764c249491d2e2be0039c5886810973b50ed72%2Fpreamble.sty&embed" width="600" height="300" style="border-radius: 8px; border: none;"></iframe></center>

The rest of the double complex is padded with zeros, but we will not draw them as long as they aren't relevant. I will use an indexing convention going rightward and downward, to be consistent with the diagram's arrows.

Starting with the rightward orientation $\_\to E_\bullet^{\bullet,\bullet}$, the first page $\_\to E_1^{\bullet,\bullet}$ of the spectral sequence is constructed by taking cohomologies of the rows, which are both exact. We must just be careful at the endoints though, where we will get some kernels and cokernels, so that the page $\_\to E_1^{\bullet,\bullet}$ looks like so
<center><iframe class="quiver-embed" src="https://q.uiver.app/#q=WzAsOCxbMCwwLCJcXGtlciBmJyJdLFswLDIsIlxca2VyIGYiXSxbMiwwLCIwIl0sWzIsMiwiMCJdLFs0LDAsIjAiXSxbNCwyLCIwIl0sWzYsMCwiXFxjb2tlciBoJyJdLFs2LDIsIlxcY29rZXIgaCJdLFswLDFdLFsyLDNdLFs0LDVdLFs2LDddXQ==&macro_url=https%3A%2F%2Fgist.githubusercontent.com%2Faradarbel10%2Fb00a36db72c3910b28e445ec79e330a7%2Fraw%2Fc2014446ec78f96d5302f7ecf59c2234a54b14c2%2Fpreamble.sty&embed" width="600" height="300" style="border-radius: 8px; border: none;"></iframe></center>

The next page $\_\to E_2^{\bullet,\bullet}$ is construced by taking cohomologies of these new vertical morphisms, which looks like so
<center><iframe class="quiver-embed" src="https://q.uiver.app/#q=WzAsMjAsWzQsMiwiXFxhc3QiXSxbNCw0LCJcXGFzdCJdLFs2LDIsIjAiXSxbNiw0LCIwIl0sWzgsMiwiMCJdLFs4LDQsIjAiXSxbMTAsMiwiXFxhc3QiXSxbMTAsNCwiXFxhc3QiXSxbMiw0LCIwIl0sWzAsNiwiMCJdLFswLDQsIjAiXSxbOCwwLCIwIl0sWzE0LDAsIjAiXSxbMTIsMCwiMCJdLFsxMCwwLCIwIl0sWzE0LDIsIjAiXSxbMTIsMiwiMCJdLFsyLDYsIjAiXSxbNCw2LCIwIl0sWzYsNiwiMCJdLFs2LDNdLFs0LDFdLFsyLDhdLFsxLDldLFswLDEwXSxbMTEsMF0sWzEyLDZdLFsxMyw0XSxbMTQsMl0sWzE1LDddLFsxNiw1XSxbMywxN10sWzUsMThdLFs3LDE5XV0=&macro_url=https%3A%2F%2Fgist.githubusercontent.com%2Faradarbel10%2Fb00a36db72c3910b28e445ec79e330a7%2Fraw%2Fc2014446ec78f96d5302f7ecf59c2234a54b14c2%2Fpreamble.sty&embed" width="800" height="400" style="border-radius: 8px; border: none;"></iframe></center>

The objects $\ast$ here just represent some nonzero objects whose specific values don't matter. All the morphisms here (and in any page onwards) are zero morphisms, so the spectral sequence already converges. In particular, if we denote by $i,j$ the coordinates corresponding to the object $C'$ in the original diagram, then we deduce $\_\to E_\infty^{i,j} = 0$.

Next consider the downward orientation $\_\down E_\bullet^{\bullet,\bullet}$. The first page $\_\down E_1^{\bullet,\bullet}$ is constructed by taking cohomologies of columns, which are all just the co/kernels of the vertical maps in our original diagram
<center><iframe class="quiver-embed" src="https://q.uiver.app/#q=WzAsOCxbMCwwLCJcXGtlciBhIl0sWzAsMiwiMCJdLFsyLDAsIjAiXSxbMiwyLCJcXGNva2VyIGIiXSxbNCwwLCJcXGtlciBjIl0sWzQsMiwiXFxjb2tlciBjIl0sWzYsMCwiMCJdLFs2LDIsIlxcY29rZXIgZCJdLFswLDJdLFsxLDNdLFsyLDRdLFszLDVdLFs0LDZdLFs1LDddXQ==&macro_url=https%3A%2F%2Fgist.githubusercontent.com%2Faradarbel10%2Fb00a36db72c3910b28e445ec79e330a7%2Fraw%2Fc2014446ec78f96d5302f7ecf59c2234a54b14c2%2Fpreamble.sty&embed" width="600" height="300" style="border-radius: 8px; border: none;"></iframe></center>

We take the cohomologies of this page to get the next one, $\_\down E_2^{\bullet,\bullet}$, and here are the results
<iframe class="quiver-embed" src="https://q.uiver.app/#q=WzAsMjAsWzQsMiwiXFxhc3QiXSxbNCw0LCIwIl0sWzYsMiwiMCJdLFs2LDQsIlxcYXN0Il0sWzgsMiwiXFxrZXIgYyJdLFs4LDQsIlxcYXN0Il0sWzEwLDIsIjAiXSxbMTAsNCwiXFxhc3QiXSxbMTIsMCwiMCJdLFsxNCwwLCIwIl0sWzEyLDIsIjAiXSxbMTQsMiwiMCJdLFs2LDYsIjAiXSxbNCw2LCIwIl0sWzIsNiwiMCJdLFs4LDAsIjAiXSxbMTAsMCwiMCJdLFswLDQsIjAiXSxbMiw0LCIwIl0sWzAsNiwiMCJdLFsxLDRdLFszLDZdLFs0LDhdLFs2LDldLFs1LDEwXSxbNywxMV0sWzE0LDNdLFsxMyw1XSxbMTIsN10sWzIsMTZdLFswLDE1XSxbMTcsMF0sWzE4LDJdLFsxOSwxXV0=&macro_url=https%3A%2F%2Fgist.githubusercontent.com%2Faradarbel10%2Fb00a36db72c3910b28e445ec79e330a7%2Fraw%2Fc2014446ec78f96d5302f7ecf59c2234a54b14c2%2Fpreamble.sty&embed" width="800" height="400" style="border-radius: 8px; border: none;"></iframe>

Now looking at this page $\_\down E_2^{\bullet,\bullet}$ and beyond, we can see every morphism is a zero morphism, hence we have converged.
This time around we got $\_\down E_\infty^{i,j} = \ker c$. Combine this with the rightward development from earlier, and we conclude the desired result, that $\ker c = 0$ meaning $c$ is monic. $\qed$

The simplicity is mesmerising.

Jokes aside, once getting over the technical challenge of wielding spectral sequences, this proof is quite reasonable. In fact it's a lot more beautiful than our first three proofs, because it shows a lot more clearly why each of our assumptions was needed: We just need a few of the objects surrounding $C'$ to vanish in cohomology, so that the sequence converges only after a couple of pages.


## Background
This post was meant to be just a bit of fun, experimenting with ideas in homological algebra and seeing where they can get us. However I'd feel guilty posting this without saying at least something about the bigger picture. Granted, the four lemma seems like a rather arbitrary result at first glance, and it's not so clear when or why it will be useful. So here is my favorite application.

It begins with yet another lemma, which is just as arbitrary looking.

**Lemma (co-four):** In an abelian category $\clA$, consider the following diagram with exact rows

<center><iframe class="quiver-embed" src="https://q.uiver.app/#q=WzAsOCxbMCwwLCJCJyJdLFswLDIsIkIiXSxbMiwwLCJDJyJdLFsyLDIsIkMiXSxbNCwwLCJEJyJdLFs0LDIsIkQiXSxbNiwwLCJFJyJdLFs2LDIsIkUiXSxbMCwyLCJnJyJdLFsyLDQsImgnIl0sWzQsNiwiayciXSxbMSwzLCJnIiwyXSxbMyw1LCJoIiwyXSxbNSw3LCJrIiwyXSxbMCwxLCJiIiwwLHsic3R5bGUiOnsiaGVhZCI6eyJuYW1lIjoiZXBpIn19fV0sWzIsMywiYyJdLFs0LDUsImQiLDAseyJzdHlsZSI6eyJoZWFkIjp7Im5hbWUiOiJlcGkifX19XSxbNiw3LCJlIiwwLHsic3R5bGUiOnsidGFpbCI6eyJuYW1lIjoibW9ubyJ9fX1dXQ==&macro_url=https%3A%2F%2Fgist.githubusercontent.com%2Faradarbel10%2Fb00a36db72c3910b28e445ec79e330a7%2Fraw%2Fef764c249491d2e2be0039c5886810973b50ed72%2Fpreamble.sty&embed" width="600" height="300" style="border-radius: 8px; border: none;"></iframe></center>

If $b$ and $d$ are epic, and $e$ is monic, then $c$ is epic.

**Proof:** Since $\clA$ is an abelian category, then so is its opposite $\clA^\op$. In the opposite category the co-four lemma becomes the four lemma, which we already proved. $\qed$

Using the four and co-four lemmas, we get another well known lemma which looks slightly less made-up.

**Lemma (five):** In an abelian category $\clA$, consider the following diagram with exact rows

<center><iframe class="quiver-embed" src="https://q.uiver.app/#q=WzAsMTAsWzIsMCwiQiciXSxbMiwyLCJCIl0sWzQsMCwiQyciXSxbNCwyLCJDIl0sWzYsMCwiRCciXSxbNiwyLCJEIl0sWzgsMCwiRSciXSxbOCwyLCJFIl0sWzAsMCwiQSciXSxbMCwyLCJBIl0sWzAsMiwiZyciXSxbMiw0LCJoJyJdLFs0LDYsImsnIl0sWzEsMywiZyIsMl0sWzMsNSwiaCIsMl0sWzUsNywiayIsMl0sWzAsMSwiYiJdLFsyLDMsImMiXSxbNCw1LCJkIl0sWzYsNywiZSJdLFs5LDFdLFs4LDBdLFs4LDksImEiXSxbOCw5LCJcXHNpbSIsMix7InN0eWxlIjp7ImJvZHkiOnsibmFtZSI6Im5vbmUifSwiaGVhZCI6eyJuYW1lIjoibm9uZSJ9fX1dLFswLDEsIlxcc2ltIiwyLHsic3R5bGUiOnsiYm9keSI6eyJuYW1lIjoibm9uZSJ9LCJoZWFkIjp7Im5hbWUiOiJub25lIn19fV0sWzIsMywiXFxzaW0iLDIseyJzdHlsZSI6eyJib2R5Ijp7Im5hbWUiOiJub25lIn0sImhlYWQiOnsibmFtZSI6Im5vbmUifX19XSxbNCw1LCJcXHNpbSIsMix7InN0eWxlIjp7ImJvZHkiOnsibmFtZSI6Im5vbmUifSwiaGVhZCI6eyJuYW1lIjoibm9uZSJ9fX1dLFs2LDcsIlxcc2ltIiwyLHsic3R5bGUiOnsiYm9keSI6eyJuYW1lIjoibm9uZSJ9LCJoZWFkIjp7Im5hbWUiOiJub25lIn19fV1d&macro_url=https%3A%2F%2Fgist.githubusercontent.com%2Faradarbel10%2Fb00a36db72c3910b28e445ec79e330a7%2Fraw%2Fef764c249491d2e2be0039c5886810973b50ed72%2Fpreamble.sty&embed" width="600" height="300" style="border-radius: 8px; border: none;"></iframe></center>

If $a,b,d,e$ are isomorphisms, then so is $c$.

**Proof:** Recall abelian categories are *balanced*, which means a morphism is iso iff it is monic and epic. Now the four and co-four lemmas together imply the result in an obvious manner. $\qed$

Now why do we care about the five lemma? The answer is, there is a very common situation in algebraic topology and homological algebra, where you'd end up with a short exact sequence (SES) whose objects are themselves chain complexes:

$$0 \too A^\bullet \too B^\bullet \too C^\bullet \too 0$$

In such scenario, one of the most important (if not most important) homological constructions is the induced long exact sequence (LES) of cohomologies

$$\cdots \to H^n(A^\bullet) \to H^n(B^\bullet) \to H^n(C^\bullet) \xto{\partial} H^{n+1}(A^\bullet) \to H^{n+1}(B^\bullet) \to H^{n+1}(C^\bullet) \to \cdots$$

This kind of LES is unreasonably abundant throughout mathematics, and it always has that curious three-long period of repetition. Moreover, this whole construction is functorial in the following sense: If we start with a morphism of SESs

<center><iframe class="quiver-embed" src="https://q.uiver.app/#q=WzAsMTAsWzAsMCwiMCJdLFsyLDAsIkFeXFxidWxsZXQiXSxbNCwwLCJCXlxcYnVsbGV0Il0sWzYsMCwiQ15cXGJ1bGxldCJdLFs4LDAsIjAiXSxbMCwyLCIwIl0sWzIsMiwiWF5cXGJ1bGxldCJdLFs0LDIsIlleXFxidWxsZXQiXSxbNiwyLCJaXlxcYnVsbGV0Il0sWzgsMiwiMCJdLFszLDgsImgiLDFdLFswLDFdLFsxLDJdLFsyLDNdLFszLDRdLFs1LDZdLFs2LDddLFs3LDhdLFs4LDldLFsxLDYsImYiLDFdLFsyLDcsImciLDFdXQ==&macro_url=https%3A%2F%2Fgist.githubusercontent.com%2Faradarbel10%2Fb00a36db72c3910b28e445ec79e330a7%2Fraw%2Fc2014446ec78f96d5302f7ecf59c2234a54b14c2%2Fpreamble.sty&embed" width="600" height="250" style="border-radius: 8px; border: none;"></iframe></center>

then the resulting LESs will also have a morphism between them:

<center><iframe class="quiver-embed" src="https://q.uiver.app/#q=WzAsMTYsWzIsMCwiSF5uKEFeXFxidWxsZXQpIl0sWzQsMCwiSF5uKEJeXFxidWxsZXQpIl0sWzYsMCwiSF5uKENeXFxidWxsZXQpIl0sWzgsMCwiSF57bisxfShBXlxcYnVsbGV0KSJdLFsxMCwwLCJIXntuKzF9KEJeXFxidWxsZXQpIl0sWzEyLDAsIkhee24rMX0oQ15cXGJ1bGxldCkiXSxbMCwwLCJcXGNkb3RzIl0sWzE0LDAsIlxcY2RvdHMiXSxbMCwyLCJcXGNkb3RzIl0sWzIsMiwiSF5uKFheXFxidWxsZXQpIl0sWzQsMiwiSF5uKFleXFxidWxsZXQpIl0sWzYsMiwiSF5uKFpeXFxidWxsZXQpIl0sWzgsMiwiSF57bisxfShYXlxcYnVsbGV0KSJdLFsxMCwyLCJIXntuKzF9KFleXFxidWxsZXQpIl0sWzEyLDIsIkhee24rMX0oWl5cXGJ1bGxldCkiXSxbMTQsMiwiXFxjZG90cyJdLFs2LDBdLFswLDFdLFsxLDJdLFsyLDMsIlxccGFydGlhbCJdLFszLDRdLFs0LDVdLFs1LDddLFs4LDldLFs5LDEwXSxbMTAsMTFdLFsxMSwxMiwiXFxwYXJ0aWFsIiwyXSxbMTIsMTNdLFsxMywxNF0sWzE0LDE1XSxbMCw5XSxbMSwxMF0sWzIsMTFdLFszLDEyXSxbNCwxM10sWzUsMTRdXQ==&macro_url=https%3A%2F%2Fgist.githubusercontent.com%2Faradarbel10%2Fb00a36db72c3910b28e445ec79e330a7%2Fraw%2Fc2014446ec78f96d5302f7ecf59c2234a54b14c2%2Fpreamble.sty&embed" width="900" height="200" style="border-radius: 8px; border: none;"></iframe></center>

At this point the pattern of the five lemma becomes completely apparent; the five-wide diagram fits exactly in our LESs to cover slightly less than two periods. So, if any two out of the three morphisms $f,g,h$ are quasi-isomorphisms (that is, induce an isomorphism on the level of cohomology) then so will be the third one.

It is quite surprising for me to see those elegant results in homological algebra that relate seemingly unrelated parts of huge diagrams. Feels like real magic.