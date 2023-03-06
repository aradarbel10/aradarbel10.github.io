# Two ways to do closure conversion
While exploring compilation of functional programming language, I encountered a lot the terms "closure conversion" and "lambda lifting". People seem to have different definitions for those terms, so let's clear it up.
Our goal is to translate lambda calculus to a restricted version fragment where all functions are defined in the top-level program, making it easier to emit through a C or LLVM backend.

As an example, let's compile this raw lambda term:
```hs
let a = 5 in (\x y. x + a * y) 1 2
```
You could think of `\x y.` as a multiparameter lambda or as a nested (curried) lambda. It's less relevant for this specific example.

## First way
The first way is much more complicated, but arguably more intuitive and explicit, and also opens up some optimization opportunities.
### A-normalization
It's always a good idea to start with normalization. This converts our lambda term to ANF, where every subexpression has an explicit name and the evaluation order is fixed. I believe CPS can also be used here but haven't tried it yet.
Note, normally the `x + a * y` part will also be factored out to subexpressions, but for brevity's sake I left it whole here.
```hs
let a = 5 in
let f = \x y. x + a * y in    <--- factor out lambdas
let d = f 1 2 in              <--- factor out applications
return d
```
Now the lambda has as explicit name `f`, and the application `d`. 

### Closure Conversion
For this version of closure conversion, we need to do two things: close all the function definitions, and adjust their call sites.
To close the function definition `f`, we turn it to a "real" version `f'` but with an added extra parameter: the closure tuple `clos`. Its first component is expected to be a pointer to the "real" function, and the rest is all the free variables captured by the function (in this case just `a`).
Additionlly, we define the "fake" function `f`, which is the closure itself of the original `f`. Here we pack a tuple containing the pointer to the "real" function, and store the current value of the captured `a` at the place of definition.

Now when `f` is called, it's no longer a function. We need to modify the call site to first unpack the pointer to the "real" function `f_ptr` out of the "fake" closure `f`, and then call `f_ptr` with the closure `f`. This allows `f'` to use the values stored in its closure.

```hs
let a = 5 in

let f' = \clos x y. (         <--- add a closure parameter
  let a = clos[1] in          <--- now `a` is defined inside
  return x + a * y
) in
let f = (&f', a) in           <--- original function just becomes a closure

let f_ptr = f[0] in           <--- modify call site to unpack closure
let d = f_ptr f 1 2 in        <--- give `f` access to its own free vars
return d
```

### Hoisting
Now that the function definition doesn't have free variables, we can move it to the top level. What's left can be thought of as the entry point, or `main` function.
```hs
def f' = \clos x y. {         <--- closed function can be moved freely
  let a = clos[1] in
  return x + a * y
}
def main = {
  let a = 5 in
  let f = (&f', a) in
  
  let f_ptr = f[0] in
  let d = f_ptr f 1 2 in
  return d
}
```

## Second way
The first way was pretty complicated. Now I will show another, much easier way to transform the expression. This one is simpler because call sites don't have to be modified.
Additionally, we don't even need to perform A-normalization. This version of closure conversion can work directly on raw lambda terms, but you can still transform to ANF or CPS first for optimization purposes.

### Closure Conversion
We begin with some eta expansions: that's where `f` gets rewritten to `\x. f x`. obviously both expressions are equivalent. The latter has the advantage that, if we eta expand with all the free variables, `f` becomes closed. In this case we only need to eta-expand with `a`:
```hs
let a = 5 in ((\a x y. x + a * y) a) 1 2
                ^-----------------^
                        eta
```

### lambda lifting
Ta-da! Now the function is completely closed, and we can just pull it up to the top level.
```hs
       extract closed lambda
        v-----------------v
def f = (\a x y. x + a * y) in
def a = 5 in (f a) 1 2
              ^
        just gets named
```
notice in the call site `f` is already applied on its free variable `a` because that's where it originally came from, before being lifted.

## Which is better?
No idea! I'm still learning. if you want to know more about these techniques you'll have to ask google, or find someone smater than me. I've been trying to grasp this stuff for a while but sadly there aren't very many resources online. Hopefully my insights can help future learners.
