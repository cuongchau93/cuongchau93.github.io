---
title: What is this in JavaScript?
layout: post
excerpt_separator: "<!--more-->"
categories:
- javascript
---

Wondering how this works in JavaScript?
This post contains my findings that I found best explained.

<!--more-->
<h4>'this' is the execution context when u call the function. Let's go through some examples</h4>
<h5>
	Example 1: 
</h5>

```prettyprint
function foo() {
	console.log(this.a);
}
var a = '123';
foo (); // 123
```
`foo`  function refers  to `this.a`. When we call `foo` without explicit context, it will refer to global context where it is executed, in this case the `a` we just defined

<h5>
	Example 2: 
</h5>

```prettyprint
var personA = {
		name: 'A',
		greet: function() {
				console.log('hi! my name is ', this.name);
		},
};
personA.greet(); // hi! my name is A

var personB = {
	name :'B',
	greet: personA.greet,
}

personB.greet(); // hi! my name is B
```

In this case, we have the context is the object `personA`, which have property `name`.
How about `personB`? Well, when we call `personB.greet()`, it means to execute the function greet in context of object `personB`  

<h5>
	Example 3: When using with `new`  
</h5> 

```prettyprint
function Person() {
	var personName = 'Ryan';
	this.address = 'USA';
	console.log(personName, this.personName); 
	console.log(address, this.address); 
}
var fakePerson = Person(); // fakePerson = undefined, 
// console will print 
// Ryan undefined
// USA USA

var newPerson = new Person(); // newPerson = { address: 'USA' }
```
When we call without `new`, we execute the function with the global context
When we call with `new`,  we make a new object and assign it to `newPerson`. The new keyword will create a prototype link from `newPerson`  to Person function 
In this case, the object only has one property `address` 




There are ways to pass the context for the function using one of the following 
1. <a href='https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply'>apply</a>
2.  <a href='https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind'>bind</a>
3.  <a href='https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call'>call</a>


**Reference:**
 1. https://codeburst.io/all-about-this-and-new-keywords-in-javascript-38039f71780c
 2. You dont know JS book
 3. Many other sources
