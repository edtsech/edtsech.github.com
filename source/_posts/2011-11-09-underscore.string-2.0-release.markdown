---
layout: post
title: Underscore.string 2.0 release
date: 2011-11-09
comments: true
categories: underscore js
---

## Why 2.0?

In this version we moved Underscore.string library to separate namespace <b>_.string</b>
for solve name conflicts with Underscore library. There are some functions that available in
both libraries, for ex. <b>include</b> and <b>reverse</b>. In 1.1.6 and lower Underscore.string provided <b>includes</b>
function, but we decided that two function <b>include</b> and (<b>includes</b> or <b>includeString</b>) in one namespace
and with same functionality but one function for collections another for strings, it's a little bit ugly.

## Do we always need to write _.string?

Nope. Underscore.string provide <b>exports</b> function <b>_.string.exports()</b>, this function returns only non-conflict functions and we can mix in these functions to Underscore scope if you want.

``` js
_.mixin(_.string.exports());

// Access to Underscore.string and Underscore functions
_.include([1,2,3], 1)
_.trim('  asd  ')

// Access to conflict Underscore.string functions
_.string.include('foobar', 'bar')
// or
_.str.include('foobar', 'bar')
// "str" it's just alias for "string"
```

## Problems
We lose two things for <b>include</b> and <b>reverse</b> methods from <b>_.string:</b>

* Calls like `_('foobar').include('bar')` aren't available;
* Chaining isn't available too.

But if you need this functionality you can create aliases for conflict functions which will be convnient for you.

``` js
_.mixin({
    includeString: _.str.include,
    reverseString: _.str.reverse
})

// Now wrapper calls and chaining are available.
_('foobar').chain().reverseString().includeString('rab').value()
```

## Standalone Usage
If you are using Underscore.string without Underscore. You also have _.string namespace for it. And current version number you can find through <b>VERSION</b> constant <b>_.string.VERSION.</b> If you want you can just reassign _ variable with <b>_.string</b>

``` js
_ = _.string

_.VERSION // => 1.2.0
```

## Node.js Installation

``` js
npm install underscore.string
```

### Standalone usage:

``` js
var _s = require('underscore.string');
```

### Integrate with Underscore.js:

I recommend you this way for integrating with Underscore.js:

``` js
var _  = require('underscore');

// Import Underscore.string to separate object, because there are conflict functions (include, reverse, contains)
_.str = require('underscore.string');

// Mix in non-conflict functions to Underscore namespace if you want
_.mixin(_.str.exports());

// All functions, include conflict, will be available through _.str object
_.str.include('Underscore.string', 'string'); // => true
```

## Upgrade
In new version function <b>includes</b> has been removed, you should replace this function by <b>_.str.include</b> or create alias <b>_.includes = _.str.include</b> and all will work fine.

## Peace!

