---
layout: post
title: "React Fundamentals"
date:  2019-07-10 15:30:35
categories: code
---

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

State is what allows React components to have values that can be changed over time through things such as user actions. 

setState() is the method provided by the React library that allows for defining and manipulating state.

As a rule of thumb, mutating state directly is never recommended. Using setState() is the only reliable way to update a components state after initialization. 

```javascript
------------Right------------
setState({ username: event.target.value })
```

```javascript
------------Wrong------------
this.state.username = { event.target.value }
```

When React updates state, it does so by merging the new state object you provide with the current state object. This is also known as a shallow merge, therefore other variables of state can be left intact, and only the provided variables are mutated.

```javascript
------------Shallow------------
state = {
  userId: 001,
  username: "Mike",
  userAge: 25,
  userVerified: false,
}

this.setState({
  userVerfied: true, 
})

\\state = {
  userId: 001,
  username: "Mike",
  userAge: 25,
  userVerified: true,
}
```

### State vs. Props

State = data that changes over the lifetime of a React component

Props = Properties of an object that a React component accepts

Say we create a parent component and then render a child from it

```javascript
<ChildComponent />
```

A prop can be passed to this child component from the parent like so

```javascript
<ChildComponent color=green />
```

Once inside the child component we could access this prop

```javascript
class ChildComponent extends Component {
  constructor(props) {
    super(props)
    console.log("Color:", props.color)
  }
}
//Color: green
```

You could even use props to set the internal state of the child component like so

```javascript
class ChildComponent extends Component {
  constructor(props) {
    super(props)
    this.state.colorName = props.color
  }
}
```

As a rule of thumb, props should never be altered within a child component, therefore, if there is a need to alter some variable, that variable should live within component state. 

Methods defined within the parent component can also be passed as props to child components, allowing the children access to these methods. 

In conclusion, state keeps track of values that can be mutated. These values can be passed to child components as props, and the child components can then render these props to the UI, or in the case of methods, use these methods without the need to having their own state. 







#### _-John Espinosa_  