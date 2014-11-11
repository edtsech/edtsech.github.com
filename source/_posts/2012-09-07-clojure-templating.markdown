---
layout: post
title: "Clojure Templating"
date: 2012-09-07
comments: true
categories: clojure
---

In this note I would like to describe current situation of dealing with templates in Clojure.
We have four most known options:

* [Clostache](https://github.com/fhd/clostache")
* [Enlive](https://github.com/cgrand/enlive")
* [Fleet](https://github.com/Flamefork/fleet")
* [Hiccup](https://github.com/weavejester/hiccup)

Let's start with Fleet. Fleet is pretty similar to old ERB or JSP way of working with templates:

``` clj
<p><(post :body)></p>
```

In fact it's not so popular in Clojure world probably because main philosophy of Lisp is
"code as data". And it's also true for templates. It's where Hiccup shines:

``` clj
[:p (post :body)]
```

As you can see, it's just Clojure vector, first element of this vector is tag name and second one is content.
You can add attributes to the tag:

``` clj
[:link {:href "www.example.com"} "Example"]
```

We can easily make abstraction on it and keep it as a helper:

``` clj
(defn link [href name] [:link {:href href} name])
(link "www.example.com" "Example")
; => [:link {:href "www.example.com"} "Example"]
```

For converting it to html you need to pass it to `html` function:

``` clj
(html (link "www.example.com" "Example"))
; => "<a href=\"www.example.com\">Example</a> "
```

You can make your own collection of helpers and partials which will be easy to embed in your code.
lso you can find basic low-lewel helpers as `link-to` and `form-to` and so on in Hiccup
[itself](https://github.com/weavejester/hiccup/blob/master/src/hiccup/element.clj).
Hiccup is quite popular in Clojure comunity and it's used as part of
[Noir framework](webnoir.org).
You don't have to write Hiccup templates by yourself if you already have HTML file from a designer, there are some
[tools](https://github.com/weavejester/hiccup/wiki/Converting-html-to-hiccup) which can help you to convert HTML file to Hiccup.

If you are sceptic about all this stuff like \"code as data\" in templates you're able to choose Clostache.
It's just [Mustache](http://mustache.github.com/)
implementation in Clojure. I think you already know that. This how it looks in Clojure.

``` clj
(render "Hello, {{name}}!" {:name "Felix"})
```

Also we have some pretty interesting approach which calls Enlive, it's similar to XSLT transformation,
but instead of noisy XML we have Clojure which is Lisp which is executable XML :)
The main idea is keep our html for a designer. Just do nothing with it.
No ERB templates, Mustache or any other templates. Just plain HTML and transformations.
There is a little bit more code for explanation how it works that is why I've placed this code to the
[gist](https://gist.github.com/3672297).

I think it will be unuseful try to describe pros and cons of each of these template libraries,
because it's really depends on which process you use to work with your templates.

Also there is fifth hidden option is use templating on the front-end :)

## Peace!
