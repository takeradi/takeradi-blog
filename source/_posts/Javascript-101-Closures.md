title: Javascript - Closures
date: 2015-12-11 06:16:01
tags: ['javascript','closures']
categories: ['Javascript']
---

There are a plethora of articles, tutorials and courses on Javascript and I am pretty sure that most of them have been written by amazing web developers who have a vast amount of knowledge on this subject. I plan on writing this [Javascript](http://takeradi.github.io/categories/Javascript/) series with a two-fold reason in mind:
1. Check my understanding on Javascript
2. Explain the concepts in this series in a way that I feel is easy to understand

Before I start, I want to mention that the I find the [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) to be very useful in understanding most of the concepts. I am going to link the MDN documentation wherever possible to help you easily find additional information on the topics that I plan to cover.

I am going to start this series off with [Closure](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) but to understand closure, one must have a good understanding of [Variable Scope](https://msdn.microsoft.com/en-us/library/bzt2dkta.aspx) in Javascript. The important thing to remember about Variable Scope is that Javascript DOES NOT have `block-level` scope. Javascript has `function-level` scope (Remembering this alone can save you from so much pain). As long as you understand that, this article should be quite easy to understand.
<!--more-->
# What the heck is a Closure?
Imagine the following scenario - You have an inner function which tries to access the local variables of its outer function. If this inner function, which has access to the outer functions variables, is made accessible outside of the outer function, a closure is formed.

Confused yet? Let's try to grasp this concept with the help of an example.

# Closure in Action
```
function incrementCounter(){
  var counter=0;

  function increment(){
   counter++;
   return counter;
  }

  return increment;
}

var add1 = incrementCounter();

alert(add1()); //alerts 1
alert(add1()); //alerts 2
alert(add1()); //alerts 3

//counter is now 3
```

If you notice carefully, you will see 3 things over here:
1. The inner function - `increment` has access to the outer function's local variable - `counter`
2. The inner function is returned when the outer function - `incrementCounter` is called, making it accessible outside of the outer function - `incrementCounter`
3. When the inner function is called from outside of the outer function, it remembers the variables (`counter` in this case) that it had access to while it was created. Hence the value that you get when calling this inner function - `increment` or `add1` is 1 greater than the previous call.

Hope that clears the main concept.

# Practical Examples of Closure
You will see many theoretical examples of Closure being thrown around to understand the concept of closure. But we all know that practically applying the concept contributes the most actually understanding it.

You will find this [Stackoverflow question](http://stackoverflow.com/questions/2728278/what-is-a-practical-use-for-a-closure-in-javascript) to be very useful for this.

The example that I really like is this one:

```
var person = function () {
	// Private variable
	var name = "Taker";
	return {
		getName : function () {
			return name;
		},
		setName : function (newName) {
			name = newName;
		}
	};
}();
alert(person.name); // Undefined
alert(person.getName()); // "Taker"
person.setName("Takeradi");
alert(person.getName()); // "Takeradi"
```

This is actually the [Javascript Module Pattern](http://yuiblog.com/blog/2007/06/12/module-pattern/). In this example, you cannot access the variable `name` directly. The only way that it can be interacted with is the two functions `getName()` and `setName()`. You alone decide what IS and IS NOT accessible to everyone. Remember OOP anyone?

And that's about it! I hope this article helps you understand what Javascript Closure is. As always, the MDN documentation that I have linked above is an amazing read.
