---
layout: post
title: Destructuring
date: 2012-05-31
comments: true
categories: ruby coffeescript
---

One feature, of the functional programming languages, which I like and which can be useful in Ruby is Destructuring.
Ruby already has Destructuring Assignment, but only for arrays not for hashes.
More information [here](http://tony.pitluga.com/2011/08/08/destructuring-with-ruby.html).

But destructuring for hashes is available in CoffeeScript. ([Destructuring assignment in CoffeeScript.](http://coffeescript.org/#destructuring))

``` ruby
position = {x: 1, y: 2, z: 3}
{x, y, z} = position
x # => 1
```

Possible to do in Ruby in this way:

``` ruby
1.9.3p125 :001 > position = {x: 1, y: 2, z: 3}
 => {:x=>1, :y=>2, :z=>3} 
1.9.3p125 :003 > x, y, z = position.values_at(:x, :y, :z)
 => [1, 2, 3] 
1.9.3p125 :004 > x
 => 1 
```

But you need to write x, y, x twice, it's bad I think :)

Also nice thing to have it's "hashes constructing" (It just how I call it):

``` ruby
first_name = "Edward"
last_name  = "Tsech"
{first_name, last_name} # equal to {first_name: first_name, last_name: last_name}
# => {first_name: "Edward", last_name: "Tsech"}
```

Pseudo real example of usage:

``` ruby
user = ...
user_info = ...
render partial: "form", locals: { user, user_info }
```

I was really surprised, when I found this feature available in CoffeeScript.
Check it out:

``` ruby
$ coffee
coffee> first_name = "Edward"
'Edward'
coffee> last_name = "Tsech"
'Tsech'
coffee> {first_name, last_name}
{ first_name: 'Edward', last_name: 'Tsech' }
coffee> 
```

If you are interested in these features and would like to have it in Ruby, welcome to
[Ruby issue tracker](http://bugs.ruby-lang.org/issues/6414).

## Links
[Destructuring Assignment In CoffeeScript](http://coffeescript.org/#destructuring)
[Destructuring with Ruby](http://tony.pitluga.com/2011/08/08/destructuring-with-ruby.html)

## Peace!

