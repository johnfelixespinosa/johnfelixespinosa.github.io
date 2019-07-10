---
layout: post
title: "React Fundamentals"
date:  2019-07-10 15:30:35
categories: code
---
// Arrow Functions 
// Detail of setState
// State vs props - what is state, what is props, what can I do to both?

### Arrow Functions

Prior to the introduction of Arrow functions in ES6, we had the following, commonly referred to as an anonymous function, or in this case a named function.

```javascript
------------ES5------------
function something() {
  return "I am named"
}
```

The introduction of the arrow function in ES6 allows the same function to be written as so

```javascript
------------ES6------------
const something = () => {
  "Named arrow function"
}
```

The key takeaway to using ES6 arrow functions, is it can be more concise to read, as well as easier and shorter to type. In addition, the arrow functions make the ever confusing usage of 'this' easier to handle. This is because 'this' within an arrow function is bound within the context in which it was created. For example. 

```javascript
------------ES5------------
var obj = {
  id: 42,
  counter: function counter() {
    setTimeout(function() {
      console.log(this.id);
    }.bind(this), 1000);
  }
};
```

Here the binding of this is required in order to pass the context to the function, without, this would be undefined. With the usage of an arrow function this function could be written as so. 

```javascript
------------ES5------------
var obj = {
  id: 42,
  counter: function counter() {
    setTimeout(() => {
      console.log(this.id);
    }, 1000);
  }
};
```

The arrow function cannot be bound to a this keyword itself, so it will go up a scope and use the context of this in which it was defined. In this example 'this.id' can be interpreted in pseudocode as "this id, in the context of the scope from which this function was called, which is the variable obj, therefore this.id is obj's id which is 42". Hopefully, that makes sense.  

### setState





#### _-John Espinosa_  