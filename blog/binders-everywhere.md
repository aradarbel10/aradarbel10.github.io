---
layout: post
title: Binders Here, Binders There, Binders Everywhere
---

Why do we need so many different binders in type theory? And why are there so many different ways to write them??! If you've ever tried to study system F or system Fω then you certainly encountered this issue. This post is meant to shed some light as to what are the differences and similarities between all the binders out there.

## Lambdas: from terms to terms
The simplest binder that you probably know is a *lambda abstraction*, written as $\lambda x. e$, where $x$ is the bound name and $e$ is the function's body.

What's the purpose of a lambda function? It allows us to express some dependency between values or "terms". In other words, lambdas take in a term and spit out another term. This is embodied by the rule of *function application*, $(\lambda x. e)\;a \longmapsto_\beta e[x := a]$, which replaces all occurances of the bound variable $x$ in $e$ with the new term $a$.

Now we have to think - what is the type of a lambda function? All we need to know about a lambda (in the simply-typed lambda calculus) is what's the type of its input, and what's the type of the output that it returns. We write this as the arrow type $\tau_1\to\tau_2$, and sometimes even add an annotation to the lambda itself $\lambda(x:\tau_1). e$.

Sometimes you'd see lambdas define explicitly in a `let`-binding, for example
```hs
let foo = \x y z. e
(* equivalently *)
let foo x y z = e
```

| language 	| abstraction	| application | formation |
|:----------:|:--------:|:------:|:------:|
| type theory | $\lambda x. e$ | $f\;a$ | $\tau_1\to\tau_2$ |
| Haskell	| `\x -> e`	| `f a` | `T1 -> T2` |
| OCaml | `fun x -> e` | `f a` | `t1 -> t2` |
| [Styff](https://github.com/aradarbel10/Styff/tree/master) | `λx. e` | `f a` | `t1 → t2` |
| Agda | `λx → e` | `f a` | `τ₁ → τ₂` |

## Capital lambdas & forall: from types to terms
But what if we want our language to support *parametric polymorphism*? This is when a term can depend on a type. The running example is the identity function: which takes on *type parameter* and one *term parameter* of the type that was given to it, then returns the same term that it was given. We can write this using our brand new capital lambda:
$$id \;\;:=\;\;\Lambda \alpha.\lambda (x: \tau). x$$
Notice how the type of the parameter has to be given before the parameter itself.

When we invoke this function then, we must *instantiate* the type parameter. The notation for this is a bit messy, but in type theory you'd often encounter the square-brackets one: $id\;[\mathtt{int}]\; 5$. Advise the table below for more ways to write it.

The type of $\Lambda \alpha. e$ is written as $\forall\alpha. \tau$, where $\tau$ is the type of $e$ (which is allowed to use $\alpha$!). The way to think about $\Lambda$ is as a function that takes in a type and returns a term. $\forall$ is the type of such function, but unlike a regular function type ($\to$) we have to specify the name of the parameter *inside the type*, so it can be referred to in the rest of the type. This is conveyed perfectly in Styff's syntax, and even better in Agda.

In languages based on HM, the syntax situation is very weird. Haskell and OCaml allow you to write $\forall$ explicitly, but they can insert it for you if you needed. There is no way at all to explicitly specify a $\Lambda$.[^1]

Similarly, those languages usually don't have the same syntactic sugar in `let`-bindings. This is actually one aspect where mainstream languages do a better job, here's how we can write the identity function in C#:
```cs
public static T id<T>(T x) {
  return x;
}
```
The `<T>` there stands for the $\Lambda$ in our syntax. C#'s syntax is less successful by being a bit confusable with polymorphic types, which we look at next.

| language 	| abstraction	| instantiation | formation |
|:----------:|:--------:|:------:|:------:|
| type theory | $\Lambda \alpha. e$ | $f\;[\sigma]$ | $\forall \alpha.\tau$ |
| Haskell	| N/A	| `f @t`[^2] | `forall a. t` |
| OCaml | N/A | N/A | `'a. t` |
| Styff | `λ{a}. e` | `f {s}` | `{a} → t` |
| Agda | `λα → e` | `f σ` | `(α : Set) → τ` |

## Type-level lambdas: from types to types
In the previous section we saw terms (functions) that depend on types or, informally, "functions from types to terms". Next we look at "functions from types to types". These rarely have explicit syntax in programming languages, but we can still write them explicitly by defining a type with parameters. Here's a random Haskell example:
```hs
type Foo a b = Either String (a, b)
```
The same type parameters can also appear in a `data` declaration, like
```hs
data Bar a b
  = Bar1 Int a
  | Bar2 String b
```
which is roughly equivalent to
```hs
type Bar a b = Either (Int, a) (String, b)
```

In the example, `Foo` expects to receive two type parameters, and as a result return a new type. This is unlike the $id$ function which takes a type and returns a term.

The example contains in fact another "function from types to types", the `Either`, which already demonstrates type application.

Due to technical reasons, Haskell and OCaml do not allow you to write explicit type-level lambdas, but if they did, they'd probably look just like regular lambdas $\lambda\alpha.\tau$. Such function is already on the type level so it won't have a type, but a *kind*, `* -> *`.[^3] In those cases, we can annotate type parameters with their kinds, as in `type (a :: Type) (b :: Type) = ...` for Haskell. Last section's $\forall$ can also accept types of higher kinds, this would look like $\forall(\alpha:k).\tau$.

Thus, in the Haskell examples above, we would have `Bar :: Type -> Type -> Type`. More generally[^5], anything parameterized by a type can take/return a type of a higher kind, in which case the kind of a type-level function will be $k_1\to k_2$.

As usual, in Agda all of these are nothing but regular functions, that happen to be taking and returning types.

| language 	| abstraction	| application | formation |
|:----------:|:--------:|:------:|:------:|
| type theory | $\lambda \alpha. \tau$ | $f\;s$ | $\ast\to\ast$ |
| Haskell	| N/A	| `f s` | `* -> *` |
| OCaml | N/A | `t s`[^4] | N/A |
| Styff | `λa. t` | `f s` | `Type → Type` |
| Agda | `λα → τ` | `f σ` | `(α : Set) → τ` |

## Pi types: from terms to types
All this type-level stuff is starting to look very similar to the layer of lambdas we started with. There's one last type of dependency we haven't considered yet, which will completely erase the distinction between terms and types and unify all levels. This is *dependent functions*.

All it means is, a function where return type is allowed to use (to depend on) the *value* of the parameter. We've already seen something similar with $\Lambda$: the return type of $\Lambda \alpha. e$ is allowed to depend on the type parameter, *even though $\Lambda$'s are instantiated on the term level*. This cross-level behavior is what dependent types generalize.

In this context, we only need one type of lambda, $\lambda x. e$ and one type of application $f\;x$. instead of separate $\to$ and $\forall$, we now combine them to just one type former $\Pi(x:\sigma).\tau$, or `(x : σ) → τ` in Agda. This is the type of lambdas which take $\sigma$ and return $\tau$, *and* the $\tau$ may depend on the parameter $x$.

Since this subsumes all the previous syntax constructs, we stop distinguishing terms and types. This is the correct way to think about polymorphism, even in non-dependently typed languages: generic functions ($\Lambda$) are merely dependent functions from types to terms, and generic types are functions from types to types.

| language 	| abstraction	| application | formation |
|:----------:|:--------:|:------:|:------:|
| type theory | $\lambda x. e$ | $f\;a$ | $\Pi(x:\sigma).\tau$ |
| Agda | `λx → e` | `f a` | `(x : σ) → τ` |

## Quick reference
Here's a convenient summary table for ya

| name | slogan | abstraction | application | type formation |
|:------:|:------:|:------:|:------:|:------:|
| lambda | "from terms to terms" | $\lambda(x:\tau). e$ | $f\;a$ | $\tau_1\to\tau_2$ |
| capital lambda | "from types to terms" |  $\Lambda(\alpha:k). e$ | $f\;[\sigma]$ | $\forall \alpha.\tau$ |
| type-level lambda | "from types to types" | $\lambda(\alpha:k). \tau$ | $f\;s$ | $k_1\to k_2$ |
| lambda (dependent) | "from anything to anything" | $\lambda(x:\tau). e$ | $f\;a$ | $\Pi(x:\sigma).\tau$ |



[^1]: Instead, Haskell opts in for the much weirder and inconsistent solution of [`ScopedTypeVariables`](https://wiki.haskell.org/Scoped_type_variables).

[^2]: Enabled via the `TypeApplications` langauge extension. See [GHC's docs](https://ghc.gitlab.haskell.org/ghc/doc/users_guide/exts/type_applications.html) for more.

[^3]: Both GHC and Styff support the alternative syntax `Type -> Type`.

[^5]: This generalization is sometimes called "higher kinded types".

[^4]: You're seeing it right: OCaml's type application is postfix.