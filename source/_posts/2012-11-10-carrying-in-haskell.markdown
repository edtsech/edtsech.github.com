---
layout: post
title: Carrying in Haskell
date: 2012-11-10
comments: true
categories: haskell
---

Carrying in Haskell is enabled by default. It means each function takes one argument and returns result or other function.

``` haskell
    Prelude> :type (+)
    (+) :: Num a => a -> a -> a
```

In fact it's the same as:

``` haskell
    (+) :: Num a => (a -> (a -> a))
```

This expression means we have function that takes on argument of type Num and returns another 
function which takes one argument of type Num and return element of type Num.

These expressions are equal:

``` haskell
((+) 1 2)
(((+) 1) 2)
```

``` haskell 
Prelude> let inc = (+) 1
Prelude> inc 2
3
```

And these definitions are also equal:

``` haskell
let sum x y = x + y 
let sum = \x y -> x + y
let sum = \x -> \y -> x + y
```

## Peace!
