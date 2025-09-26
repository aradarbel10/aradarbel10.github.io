---
layout: post
title: Homology and cohmology of categories
subtitle: With an application to K-theory
---

### Motivating case: group co/homology
I'll begin with some standard stuff; forgive me if it seems too elementary, but I will ramp it up soon enough.

Let $G$ be a group. A *$G$-module* is an abelian group $M$ with a $G$-action. Typically the group action is made precise by making $M$ into a module over the "group algebra" $\mathbb{Z}[G]$, compatibly with its pre-existing structure as a $\mathbb{Z}$-module. This approach is really nice for homological algebra since it allows us to reuse everything we know about categories of modules.

Another (equivalent) way to describe the action is by giving a homomorphism $G \to \mathrm{End}(M)$, where endomorphisms are taken in the sense of abelian groups. Stated in a slightly fancier language, we may consider any group $G$ as a one-object groupoid, denoted $BG$. This has a unique object $\star$, and a morphism $g:\star\to\star$ for every element $g\in G$. Composition is just given by the group's multiplication. Now let $\mathcal{C}$ be any category (e.g. $\mathbf{Ab}$) and $C$ any object in $\mathcal{C}$. A $G$-action on $C$ is precisely a functor $BG \to \mathcal{C}$ which sends the unique object $\star$ to $C$.

The category of functors $[BG,\mathbf{Ab}]$ has the correct morphisms; natural transformations between such functors correspond precisely to $G$-equivariant maps. Moreover, as with any functor category, it inherits the abelian structure from its codomain. Therefore we can again perform homological algebra.