---
layout: post
title: Complex Numbers Are Matrices
---

Here are some cool things you can do with complex numbers. Say you have $z=a+ib$ and $w=c+id$. Then:

- Addition: $$z+w = (a+ib) + (c+id) = (a+c) + i(b+d)$$
- Multiplication: $$z\cdot w = (a+ib)(c+id) = (ac-bd) + i(ad+bd)$$
- Complex conjugation: $$\overline{z} = \overline{a+ib} = a-ib$$
- Absolute value: $$\vert z\vert^2 = \vert a+ib\vert^2 = a^2+b^2$$

And many more.

Now here's a totally unrelated thing you can do with matrices, specifically with matrices of the form
\\(\begin{pmatrix}a & b \\\ -b & a\end{pmatrix}\\):
- Addition: $$\begin{pmatrix}a & -b \\ b & a\end{pmatrix} + \begin{pmatrix}c & -d \\ d & c\end{pmatrix} = \begin{pmatrix}a+c & -(b+d) \\ b+d & a+c\end{pmatrix}$$
- Matrix multiplication: $$\begin{pmatrix}a & -b \\ b & a\end{pmatrix}\times \begin{pmatrix}c & -d \\ d & c\end{pmatrix} = \begin{pmatrix}ac-bd & -(ad+bc) \\ ad+bc & ac-bd\end{pmatrix}$$
- Matrix transposition: $$\begin{pmatrix}a & -b \\ b & a\end{pmatrix}^T = \begin{pmatrix}a & -(-b) \\ -b & a\end{pmatrix}$$
- Determinant: $$\begin{vmatrix}a & -b \\ b & a\end{vmatrix}=a^2+b^2$$

Hopefully you can see the similarity I'm hinting at. Suspecious, isn't it? In the rest of this post I'd like to explain why it's happening and a little bit on how to generalize it

## Field extensions
Yes! Our story, like many other beautiful stories in mathematics, begins with field extensions. Before proceeding, make sure you know what a field is.

Let's take the field $$\mathbb{Q}$$. We can extend it with the new number $$\sqrt{5}$$, which satisfies $$(\sqrt{5})^2=5$$. Remember, our base field doesn't have square roots so $$\sqrt{5}$$ is just a symbol. After some thinking, you can verify no number aleady in $$\mathbb{Q}$$ can satisfy this "square-equals-five" criteria, so our added number is actually new.

Adding just that number itself isn't enough though. $$\mathbb{Q}\cup\{\sqrt{5}\}$$ is not a field anymore! What we need to do is add any expression formed by $$+,-,\cdot,\div$$ with rationals and the new $$\sqrt{5}$$.
But it's easy to prove that using some algebraic manipulation, any such expression can be transformed to the form $$a+b\sqrt{5}$$, where $$a,b\in\mathbb{Q}$$.

If you start from $$\mathbb{R}$$, there already is a number satisfying "square-equals-five" - the number $$\sqrt{5}$$ itself. But there isn't a number for "square-equals-negative-one", so we can add that under the name $$i$$ and get in return the complex numbers $$\mathbb{C}$$.

In both cases we started from a base field and we extended it with a number satisfying some condition. We are especially interested in conditions arising from polynomials:
- Rather than "square-equals-five", we can say "a root of $$x^2-5$$".
- And rather than "square-equals-negative-one", say "a root of $$x^2+1$$".

Those are already much more mathematical.

## A small problem of uniqueness
When we extend the field $$\mathbb{Q}$$ with a root of $$x^2-5$$, we have a choice to make. Both roots $$\sqrt{5}$$ and $$-\sqrt{5}$$ are equally reasonable. And in fact, choosing the one automatically gives us the other.

There's a very deep subtlety here: the roots of the polynomial $$x^2-5$$ embody some notion of *symmetry*. If you're interested in this symmetry, and happen to be a 19-year-old boy dying in the french revolution, I'd point you to the amazing world of [Galois theory](https://en.wikipedia.org/wiki/Galois_theory). For now though let's get back to linear algebra.

## Embedding fields in matrices
Given some field $$\mathbb{F}$$ we can build $$\mathrm{Mat}_n(\mathbb{F})$$, the set of square matrices of size $$n$$ with entries in $$\mathbb{F}$$.
There's a natural embedding $$\mathbb{F} \hookrightarrow \mathrm{Mat}_n(\mathbb{F})$$ given by $$x \mapsto xI$$. In other words, each number in the field is sent to the diagonal matrix where all the entries on the diagonal are that number, and all other entries are zero.

Notice we can add diagonal matrices and the resulting matrix is still diagonal. Same with subtraction, and matrix multiplication. Division is a bit harder, because we need to make sure the matrix is invertible. But since it's diagonal, that becomes true as well. All in all, the embedding from $$\mathbb{F}$$ is in fact a *field homomorphism*; a function preserving the field structure. The field we're embedding into is not the set of all matrices, but only the set of those of the form $$xI$$. Are there any other subsets of matrices that also admit a field structure?

## Plugging matrices in polynomials
Back to polynomials, it might be worth thinking "what do we need to put things inside polynomials?". Concretely, when we have a polynomial with coefficients in $$\mathbb{F}$$ and one variable $$x$$ (written $$p\in\mathbb{F}[x]$$), when does the expression $$p(A)$$ make sense?

As we know, if $$A\in\mathbb{F}$$, that's just treating the polynomial as a regular function.
But what about $$n\times n$$ matrices over $$\mathbb{F}$$? They can be added, subtracted, and multiplied, hence raised to a power. Matrices can also be multiplied by a scalar. So it's not so absurd to try plugging a matrix into a polynomial.

> If the polynomial contains a constant $a_0$, it will have to become $a_0I$ to be compatible with the other matrices.

We are especially interested in a specific polynomial. Given a matrix $$A\in \mathrm{Mat}_n(\mathbb{F})$$, we define its *characteristic polynomial* $$\chi_A := \det(A-xI)$$. The $$x$$ there is the variable, and if you try to actually compute the determinant you will see it is indeed a polynomial in $$x$$.

Intuitively, if we plug $$x=A$$ we get $$\det(A-AI)=\det(0)=0$$, but formally proving $$\chi_A(A)=0$$ is a bit harder. This is called the *Cayley-Hamilton Theorem*, and it is one of the most important theorems in linear algebra.

> It turns out that the characteristic polynomial basically encodes half the information of the matrix. The other half found in the minimal polynomial, which I won't talk about.

> All of this becomes actually interesting when we consider not just matrices but *linear transformations*, and try plugging them in their own characteristic polynomial. But again, that's outside the scope of this post.

Now we have a simple procedure, given a matrix $$A$$, to find a polynomial $$\chi_A$$ which becomes zero when we plug the matrix into it. Can we go the other direction?

## The other direction
Sometimes, we can do it very easily.
Given a polynomial $$p$$, if you have some root $$x$$ such that $$p(x) = 0$$, you can just take the matrix $$xI$$ and verify that plugging it into $$p$$ also results in a zero matrix.

But there's another more interesting construction to discover. Let's write our polynomial as

$$p(x) = x^n + a_{n-1}x^{n-1} + \cdots + a_1x^1 + a_0$$

Without loss of generality, the coefficient of $$x^n$$ is $1$ (otherwise we simply divide by it). Now look at this weird matrix:

$$
A_p := \begin{pmatrix}
0 &   & & & -a_0 \\
1 & 0 & & & -a_1 \\
  & \ddots & \ddots & & -a_2 \\
  &   & 1 & 0 & \vdots \\
  &   & & 1 & -a_{n-1}
\end{pmatrix}
\in \mathrm{Mat}_n(\mathbb{F})
$$

The rightmost column of this matrix consists of the coefficients of $$p$$. The rest of the main diagonal is filled with $$0$$'s, and the one below that diagonal is filled with $$1$$'s.

This matrix is suspiciously specific, and if you know how to compute general determinants (for example, using the definition with permutations) you can see that the characteristic polynomial, $$\det(A_p - xI)$$ becomes precisely $$p(A)$$.

So the characteristic polynomial of $$A_p$$ is $$p$$, and by Cayley-Hamilton plugging a matrix in its characteristic polynomial gives zero! Magic!

We can also notice that the new matrix is never diagonal, because there are always $$1$$'s below the main diagonal. Hence it is truly a new matrix.

## The complex numbers
Take the specific polynomial $$p(x) := x^2+1$$, which is a polynomial over $$\mathbb{R}$$.
Solving for its roots will require finding an $$x$$ such that $$x^2 = -1$$, and as we know that doesn't exist within $$\mathbb{R}$$. But we can look at the isomorphic field $$\{xI \mid x\in\mathbb{R}\}$$ of $$2\times 2$$ matrices. Additionally, we can look at the adjoint matrix $$A_p=\begin{pmatrix}0 & -1 \\ 1 & 0\end{pmatrix}$$, which makes $$p(A_p)=0$$. From now on, we shall call this matrix $$i$$. We get this new set,

$$\left\{aI+bi \mid a,b\in\mathbb{R}\right\} = \left\{
a\begin{pmatrix}1 & 0 \\ 0 & 1\end{pmatrix} + b\begin{pmatrix}0 & -1 \\ 1 & 0\end{pmatrix}
\bigg| a,b\in\mathbb{R} \right\}
= \left\{
\begin{pmatrix}a & -b \\ b & a\end{pmatrix}
\bigg| a,b\in\mathbb{R} \right\}$$

We can give this set the very suggestive name $$\mathcal{C}$$. This set $$\mathcal{C}$$ turns out to even be a field, with $$\mathbb{R}$$ as a subfield. Alternatively, you can think of $$\mathcal{C}$$ as isomorphic to the original $$\mathbb{C}$$.

> As sets, there isn't an actual containment, $$\mathbb{R}\nsubseteq\mathcal{C}$$, but there is a subfield of $$\mathcal{C}$$ which is *isomorphic* to $$\mathbb{R}$$. The word "isomorphic" implies that for all intents and purposes, they are the same. If this point bothers you, think of how $$\mathbb{R},\mathbb{Q},\mathbb{Z},\mathbb{N}$$ are defined traditionally in set theory, and whether they are actually subsets of one another over there. If you feel like you've been lied to all these years, you are right. But as much as I'd love to talk about this more, it will have to be left for another time.

So, this roughly explains it. The $$2\times2$$ matrices of the form we explored behave just like complex numbers, because they *are* complex numbers. You shouldn't be surprised anymore if you see more connections!

One of the important connections to notice is that we made a choice here too! we could have used the transposed version $$\begin{pmatrix}0 & 1 \\ -1 & 0\end{pmatrix}$$, and still get a matrix that zeros $$p$$. This is equivalent to the choice of $$i$$ vs $$-i$$ from the beginning.

## More than the complex numbers
Can we now pick another polynomial and repeat this whole process to get a field yet larger than $$\mathbb{C}$$?

Sadly, no. But also happily, no! Any polynomial over $$\mathbb{C}$$ already has all of its roots contained within $$\mathbb{C}$$, so it doesn't matter which polynomial we try adding we won't get anything new.

This property of $$\mathbb{C}$$ is called *algebraic closedness*, and $$\mathbb{C}$$ being algebraically closed is called *the fundamental theorem of algebra*.

But maybe there are other ways to extend fields, not by polynomials but by just adjoining new numbers, with properties like "square-equals-five" without looking at polynomials at all. This direction can lead to very interesting structures, that I will leave for you to explore.


## More than the complex numbers... anyway?
Another way to expand on this idea is by looking at other matrices. We've only considered $$\begin{pmatrix}a & -b \\ b & a\end{pmatrix}$$, but maybe other subsets of matrices form fields? Sets of matrices turn out to be a wonderful place to do algebra, as demonstrated by representation theory.

But forget subsets, we can go even further than that. In fact, similar intuitions for complex numbers can be generalized to any matrix. One of my favorite examples is the polar decomposition for matrices: Every (square) matrix $$A$$ can be decomposed to $$A=RU$$ where $$U$$ is a "unitary" matrix and $$R$$ is a "definite positive" symmetric matrix.

I won't define those formally here, but to give some intuition: the unitary matrix plays the role of a complex number lying on the unit circle, which encodes a direction, and the positive matrix plays the role of a length.

In this context, operations like the complex conjugate (transpose in the matrix world) get a whole new meaning, and finally understanding transposition is one of the most satisfying rewards from studying linear algebra.

## The end
To conclude, we looked at this mathematical structure called "complex numbers" and tried to represent it as a set of special matrices. Along the way we met polynomials as well. This journey exposed unexpected connections between the worlds of field theory, linear algebra, and polynomials.

The act of reducing problems to matrices or polynomials is a useful repeating theme in mathematics. In truth, those are the only simple things that exist. Even in much more advanced topics, like calculus, we spend most of the time estimating non-linear functions with linear ones, so we can use the tools of linear algebra to study them. Everything else is too complicated for us humans to work with! So maybe next time you encounter an alien concept, try thinking if it behaves like a matrix ;)