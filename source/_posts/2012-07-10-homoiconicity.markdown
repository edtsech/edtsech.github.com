---
layout: post
title: Homoiconicity
date: 2012-07-10
comments: true
categories:
---

## Ruby's part

Sometimes before to go to the next step in your code you need to check "previous result". I mean:

``` ruby
value = hash[:key]
res = value ? value.do_smth : nil
```

As you can see, we created not so usuful variable `value` in the external scope
Okay, we can fix it with `try`:

``` ruby
res = hash[:key].try(:do_smth)
```

But if we need to do smth with result of `do_smth`:

``` ruby
res = SMTH + hash[:key].try(:do_smth)
```

It will cause error if we got `nil` and we need to go back to the first solution or create a method on returned object,
if it's language built-in object it's not make sence. It means we go back to this:

``` ruby
value = hash[:key]
res = value ? SMTH + value.do_smth : nil
```

Cons of that are: <b>extra variable</b> `value` and <b>two expressions</b> instead of one.

We can convert it to one expression:

``` ruby
res = if value = hash[:b]
  SMTH + value.do_smth
end
```

But it's not so easy to read and `value` variable still in external scope, and some programmers prefer to avoid conditional expressions with assignment:

``` ruby
if value = hash[:b]
# And in Python for example it throws an exception
```

## Clojure's part
Lets write this example on Clojure and try to solve this cons.
Lets use local binding:

``` clj
(def res (let [s (:key hash)]
           (when s
             (str smth s)))</b>)

; `when` in Clojure is like if but w/o else clause
```

`s` isn't available in the external scope, we've defined it only in this expression:

``` clj
(when s
  (str smth s))
```

But `let` and `when` are a little bit verbose, will be better if we will compose them in one construct. Tadam!

``` clj
(def res (when-let [s (:key hash)]
           (str smth s)))
```

We have here <b>one expression</b> and <b>no extra variables</b> in external scope and `when-let` is just macro not language construction or smth,
it [built-in into Clojure](https://github.com/clojure/clojure/blob/d0c380d9809fd242bec688c7134e900f0bbedcac/src/clj/clojure/core.clj#L1687)
, but lets say we don't have it in Clojure and we would like to write our own simplified version.

``` clj
(defmacro our-when-let [bindings expr]
      (let [fst (bindings 0) snd (bindings 1)]
          `(let [~fst ~snd]
              (when ~fst
                   ~expr))))

(macroexpand '(our-when-let [a 1]
  (+ a 1)))
; => (let* [a 1] (clojure.core/when a (+ a 1)))

(our-when-let [a 1]
  (+ a 1)) ; => 2

(our-when-let [a nil]
  (+ a 1)) ; => nil
```

It works!
This part is kind of template:

``` clj
`(let [~fst ~snd]
    (when ~fst
        ~expr))
```

You can read it as:

``` clj
"""
(let [#{fst} #{snd}]
    (when #{fst}
        #{expr}))
"""
```

But remember:

* Macros arn't strings, they are lists
* They are compiling at macro expansion time, not at runtime
* Which means we don't need parse code at runtime

What I would like to say..

* Local binding is good
* Macros are good (when they aren't overused of course)
* Homoiconicity helps to write readable, expressive code and make useful abstractions

## Links
[Clojure: if-let and when-let](http://blog.jayfields.com/2011/03/clojure-if-let-and-when-let.html)

## Peace!

