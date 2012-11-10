---
layout: post
title: Haskell Operators
date: 2012-11-07
comments: true
categories: haskell
---

Haskell operators are just functions like in Lisp.

``` clj
    (+ 1 2)
    (+ 1 2 3)
```

To get a type of the `+` operator we should use parentheses.

``` haskell
    Prelude> :type (+)
    (+) :: Num a => a -> a -> a
```

It's just a function, it takes two arguments of type Num and return something of type Num.
Let's try.

``` haskell
    Prelude> (+) 1 2
    3
```

To use it with more that two arguments we should use list and fold.

``` haskell
    Prelude> foldl1 (+) [1,2,3]
    6
```

## Carrying

If it's just a function we can use carrying.

``` haskell
    Prelude> let inc = (+1)
    Prelude> inc 1
    2
```

We can use it everywhere.

``` haskell
    Prelude> map inc [1,2,3]
    [2,3,4]
```

or just

``` haskell
    Prelude> map (+1) [1,2,3]
    [2,3,4]
```

I mean no magic here, `(+1)` is just a carried function.

It's also true not only for arithmetic operators.

``` haskell
    Prelude> :type (||)
    (||) :: Bool -> Bool -> Boo
    Prelude> (||) True Falsel
    True
```

## Peace!
