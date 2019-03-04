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

As you can see, if we step into our interior fence and ask the console to log the tree, it will return Oak, remember when I said that everything within our first fence is global? Think of it like this. Inside our interior fence, we have no tree, and we ask, "Hey console? what tree do we have?". Console will first look locally in our interior fence and see no tree, then he steps out of the interior fence and back into our global yard and points and says "Over there! it's an Oak! Did I do good? Please tell me I did good". Ok you did good console. Put the Maple tree back within the interior fence and ask console again. He'll look locally and point to the Maple tree immediately. 

### Hoisting

Hoisting is the process in javascript that is essentially "Moving to the beginning of a scope". Functions, or our inner fences, are hoisted completely; however, variable declarations are only hoisted partially. Imagine your application, when you first run it, it will scan your scopes, and it will say "Ok interior fence, I see a tree". Great! but it will not go up to that tree and actually define it, or know what that tree is, it will just know that a tree is there. For example.

```javascript
function innerFence(){
  console.log(tree + " tree exists!");
  var tree = "Oak";
}
innerFence();
// undefined tree exists!
```

Our console is saying essentially, I see a tree, I don't know what it is though so it's undefined, but its there! This is what console actually did.

```javascript
function innerFence(){
  var tree; //Ok letme glance at EVERYTHING in this scope! Oh look there's a tree, let me remember that
  console.log(tree + " tree exists!"); //Ok now I'm suppose to log this, Ok I see the tree, but I dont know what it is yet, let me just say its undefined, yea thats good
  tree = "Oak"; //Tree is an Oak! oops! already logged it was undefined 
}
innerFence();
// undefined tree exists!
```

In order for console to do his job correctly, you must help him by always declaring your variables at the top of the scope he is in, and since he hoists functions as well, put them at the top as well if possible. So in order for him to correctly identify the tree the function should be written as so.

```javascript
function innerFence(){
  var tree = "Oak";
  console.log(tree + " tree exists!");
}
innerFence();
// Oak tree exits!
```

## Let and Const

There is another form of scope, and that is block scope. Think of a block as posts with a string tied around them within an inner fence. Not quite a full fence but a boundary. So lets imagine the following.

```javascript
function innerFence(){
  var tree = "Oak";
}
tree;
// Uncaught ReferenceError: tree is not defined
```

Tree is defined within the function, therefore, it is not available or seen outside the function, because var is locally scoped to the function, and if not declared within a function then it is globally scoped within our global fence. So if we did the following... 

```javascript
var tree = "Oak"

if (tree = "Oak"){
    var treeHeight = "tall"
    console.log(tree + " is " + treeHeight)
}
```




#### _-John Espinosa_  