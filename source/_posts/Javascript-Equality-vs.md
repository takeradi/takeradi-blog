title: Javascript - Equality Comparison Operators (== vs ===)
date: 2015-12-17 02:17:09
tags: ['javascript','dev']
categories: ['Javascript']
---

# Introduction

Let's look at a few equality tests:
```
console.log(true==1); // true
console.log(1=="1"); // true

console.log(true===1); // false
console.log(1==="1"); // false

var a = [1,2,3];
var b = [1,2,3];
var c = a;

console.log(a==b); // false
console.log(a==c); // true

var d = new String("text");
var e = "text";

console.log(d==e); // true
console.log(d===e); // false
```

If you understand why the [equality comparison operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness) return what they return above, then turn around and never look back :D. If not then continue reading...
<!--more-->

# What do `==` and `===` represent?
In Javascript, `==` represents to the **equality operator** and `===` represents to the **identity operator**.

I think this topic in Javascript confuses one and all. The rules are too many and too complex to memorize.
To counter this confusion, some people say - *When in doubt, ask Javascript*.
While the others ask you to - *Always use the identity operator instead of the equality operator*.
And then, there are a few nasty people who ask you to go through the [documentation](http://www.ecma-international.org/ecma-262/5.1/#sec-11.9.3) :D.

So then, how do we get rid of this confusion? We don't. We test it on Javascript when we are confused and we try to use the identity operator `===` unless we really really have to resort to using its evil twin (the `==` equality operator).

Here are a few basic rules that you should remember:
1. The `==` operator does the necessary type conversion before comparison. For eg:
    ```
    2=="2" //returns true
    ```
2. The `===` operator does no type conversion and directly compares. For eg:
    ```
    2==="2" //returns false
    ```
And of course, to understand how the `==` equality operator functions, you have to know what [Truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) and [Falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) values are in Javascript

# Reference Types
For reference types - `==` and `===` behave the same (except in one special case).

```
var a = [1,2,3];
var b = [1,2,3];

var c = { x: 1, y: 2 };
var d = { x: 1, y: 2 };

var e = "takeradi";
var f = "taker" + "adi";

a == b            // false
a === b           // false

c == d            // false
c === d           // false

e == f            // true
e === f           // true
```

The special case is:

```
var a = "abc"; // a String literal
var b = new String("abc"); // a String object

a == b            // true because after type conversion only the value is compared
a === b           // false because of the identity comparison. a and b are not of the same type

```

A String literal comparison with a String object comparison is a bit tricky. Hopefully the above example helps you to handle such comparisons.

# "===" DOES NOT mean "equal and of the same type"

The identity operator `===` DOES NOT always mean `equal and of the same type`.

The general rule to follow for indentity comparisons is:

1. For value types (numbers):
    `a === b` returns `true` if `a and b have the same value and are of the same type`

2. For reference types:
    `a === b` returns `true` if `a and b reference the exact same object`

3. For strings:
    `a === b` returns `true` if `a and b are both strings and contain the exact same characters`

# Interesting Examples:
There are a few interesting examples that you should be aware of. Just have a glance at the examples mentioned below. You should be able to understand most of them if you understood the article.

```
'' == '0'           // false
0 == ''             // true since '' is falsy and 0 is considered as falsy too
0 == '0'            // true because of type conversion done by the equality operator

false == 'false'    // false
false == '0'        // true

false == undefined  // false
false == null       // false
null == undefined   // true

' \t\r\n ' == 0     // true
```

# Closing Thoughts
I know this is very confusing but I hope that after reading this article, the MDN documentation and this [Stackoverflow question](http://stackoverflow.com/questions/359494/does-it-matter-which-equals-operator-vs-i-use-in-javascript-comparisons) will answer most of your questions.

*Note: Most of the examples mentioned in this article are from the Stackoverflow question linked above. They were exceptionally good examples and I thought it would help more if I used the same examples.*
