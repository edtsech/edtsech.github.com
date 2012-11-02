---
layout: post
title: Rubyists, Clojure Is Your Friend
date: 2012-07-08
comments: true
categories: clojure
---

Some infantile, spontaneous and subjective info about Clojure for Rubyists.

* Clojure is your friend
* Clojure is dynamically typed, as Ruby
* Clojure is like Ruby :) But everything isn't an object it's a function: [Clojure data structures](http://clojure.org/data_structures)

``` clj
; Usual function call (if you forgot how lispy syntax looks like):
(+ 1 2) ; => 3

; Clojure's Keyword is like Ruby's Symbol and it's a function:
(:text {:text "Hello"}) ; => "Hello"

; Clojure's Maps is like Ruby's Hashes and it's functions too:
({:text "Hello"} :text) ; => "Hello"
```

* Falsy values in Clojure like in Ruby: nil and false [Clojure: Truthy and Falsey](http://blog.jayfields.com/2011/02/clojure-truthy-and-falsey.html)

``` clj
(boolean nil)   ; => false
(boolean false) ; => false
(boolean 0)     ; => true
(boolean [])    ; => true
(boolean '())   ; => true
```

* I know, all Rubyists like metaprogramming and awesome DSLs [Compojure](https://github.com/weavejester/compojure/wiki/Getting-Started)

``` clj
; Sinatra like DSL
(defroutes main-routes
  (GET "/" [] "Hello World Wide Web!")
  (route/resources "/")
  (route/not-found "Page not found"))
```

[Korma](http://sqlkorma.com/)

``` clj
; SQL DSL
(defdb prod (postgres {:db "korma"
                       :user "db"
                       :password "dbpass"}))

(defentity address)
(defentity user
  (has-one address))

(select user
  (with address)
  (fields :firstName :lastName :address.state)
  (where {:email "korma@sqlkorma.com"}))
```

Or you can write your own language "conditional expression" (thanks to Lisp's homoiconicity, parentheses and macros):

``` clj
(defmacro unless [expr form]
  (list 'if expr nil form))

(def good-cop true)

(unless good-cop (println "I say everything"))
; nil
(unless (not good-cop) (println "I say everything!"))
; I say everything!
```

Use dashes for naming things, I know you like underscores, but dashes aren't bad too

``` clj
(def good-cop)
; instead of
(def good_cop)

; You can use "?" and "!", actually it came to Ruby from Lisp
(keyword? :key) ; => true

; But sometimes you can do smth crazy, when noboby's watching:
(def X__X "I'm die")
```

* Clojure has good ecosystem
* Clojure is concurrency
* Clojure is immutability
* Clojure is simple syntax
* Clojure is simple, but not easy (" [Simple Made Easy](http://www.infoq.com/presentations/Simple-Made-Easy) ")
* Clojure is data, not objects
* Clojure is composable libraries, not full-stack frameworks, not looking for Rails here, but there is some [Conjure](https://github.com/macourtney/Conjure)
* Ruby and Clojure are influenced by Lisp, of course Clojure is more influenced, you get all power of homoiconicity and more addicted to FP language
* Even if you don't love parentheses, parentheses love you!
* Clojure is your friend, isn't it?

## Links

* [Try Clojure](http://tryclj.com/)
* [Try ClojureScript](http://himera.herokuapp.com/index.html)
* [How Emacs changed my Life - matz](http://www.slideshare.net/yukihiro_matz/how-emacs-changed-my-life)
* [Ruby's lisp features](http://blade.nagaokaut.ac.jp/cgi-bin/scat.rb/ruby/ruby-talk/179642)
* [Lisp (vs Ruby) Metaprogramming](http://www.slideshare.net/antoniogarrote/lisp-vs-ruby-metaprogramming-3222908)
* [Ruby Creator Yukihiro 'matz' about Ruby, Functional Programming and Programming Languages Design](http://www.infoq.com/interviews/yukihiro-matz-language-design/)

## Peace!


