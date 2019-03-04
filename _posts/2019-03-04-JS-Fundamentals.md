---
layout: post
title: "Fundamentals of JS"
date:  2019-03-04 15:30:35
categories: code
---

## Scopes

I was recently asked to explain the types of scope within Javascript, and admittedly while I was familiar with the concepts, regurgitating their nuances was problematic. So, much like many other instances in my life where I've tried to really understand a concept, I came up with a metaphor that I could easily fall back to when asked this question again. 

First, lets identify the types of scope in javascript. *Global* and *Local*

### Global Scope

Think of a house, not just any house, but this house has a huge green yard, it sits right smack directly in the middle of the property, and surrounding the entire house and yard is a white picket fence. This is the only thing in existence, nothing else. Actually don't even imagine a house yet, just a huge green rectangular yard surrounded by that white picket fence. See it? ok good. This is what we will call Global space. Every javascript file has a global scope. In fact, as soon as you give the file the **.js** extension, and begin writing code, you are within the global scope. You are within the fence, on the grass. Everything that you define within the global scope is accessible everywhere else within our yard. So if the first thing you were to code in your new javascript file was...

```javascript
var tree = "Oak" // this tree is now lives in the yard, in the global scope
console.log(tree);
// Oak
```
You have now defined a global variable, this tree lives directly within the global scope, everything within the yard can touch it.

### Local Scope

Now imagine this, within our yard, surrounded by our white picket fence, with our single Oak tree, we were to construct another 4 corner white picket fence yard. Everything we define within this interior fence will have a local scope. So if we were to add to our code the following...

```javascript
var tree = "Oak" // this tree is now lives in the yard, in the global scope
console.log(tree); // Oak

function interiorFence(){
  var tree = "Maple" // this second tree lives locally within the interior fence
  console.log(tree); // Maple
}

console.log(tree); // Oak
```

The most important part of the code above is the last line, the last log. Once we step outside of the interior fence, back into our first open yard, we are now back in the global scope, and when we ask what our tree is. Well our tree is Oak again. If we step within our interior fence and ask, "Hey what tree do I have?" well it's a Maple in here locally, because we are within the interior fences local scope. Well, what about if we never define a tree within our interior fence?  

```javascript
var tree = "Oak" // this tree is now lives in the yard, in the global scope
console.log(tree); // Oak

function interiorFence(){
  console.log(tree); // Oak
}

console.log(tree); // Oak
```

As you can see, if we step into our interior fence and ask the console to log the tree, it will return Oak, remember when I said that everything within our first fence is global? Think of it like this. Inside our interior fence, we have no tree, and we ask, "Hey console? what tree do we have?". Console will first look locally in our interior fence and see no tree, then he steps out of the interior fence and back into our global yard and points and says "Over there! it's an Oak! Did I do good? Please tell me I did good". Ok you did good console. 





#### _-John Espinosa_  