---
layout: post
title: Javascript object
subtitle: A short introduction or knowledge refresh
bigimg: ../img/analog.jpg
---

## Javascript Objects

To get the most of this go to https://jsbin.com/ or https://codepen.io/ and type the below to see the result, you can console.log the results to make sure you understand what is happening.

## Object literals
This is the basic way of creating objects in Javascript
```
const person = { 
                  name: 'Mac',
                  'second-name': 'Wasilewski',
                  getName: function() {
                      return this.name;
                  }
                };
```

Objects consist of:
- properties, which are key-value pairs, in the above example it is `name: 'Mac`.

Notice that `name` is written with no quotes, it is because it is a [valid JS variable name](https://stackoverflow.com/a/9337047/4587598). In the second case we have to wrap the property in quotes, but it doesn't matter if these are single or double quotes.

A property of an object can be accessed using so called dot notation `person.name` of bracket notation if you used invalid name `person['second-name']`.

- methods, which are function which perform some kind of actions on the object itself.

In the above example the `getName()` method return the name of the person. Notice the usage of `this`, in objects `this` refers to the object itself, so calling `this.name` will return the property called `name`. If the property would not exist we would not get any errors, just `undefined`.

## Object constructors
Obviously when we create several persons, we do not want to copy/paste the above code each time we create a new person. The older versions of JS support object Constructors.
```
function Person(name) {
    this.name = name;
}
```
The above can be used to create new people:
```
const p1 = new Person('Bob');
const p2 = new Person('Mac');
```
It is important to notice that if you created an objet and missed the `new` keyword and wasn't in `"use strict"` mode then JS would not tell you you missed it but weird thing could have happened as `this` would not reference the newly created error but it might have use the global object or window.

Now I can lowercase a property, but notice it will not update the object property itself which remains uppercased.
```
p1.name.toLowerCase();
```

I want to add a method which lowercases the name before sending them back to the databse, but I already created so many people in multiple places in my app and need to be able to lowercase all withoud looking through the codebase to manually lowercase the properties. What do I do?

Javascript has a very cool inheritance method called prototypal inheritance. I'll show how it works solving the issue above.
```
Person.prototype.toLower = function() {
  this.name = this.name.toLowerCase();
}
```
Now every object created using the `new Person` will gain a new method called `toLower()`. How it works?
Every object has a property called prototype, and when a method is called on an object the Javascript engine first checks the current object prototype property in a search for that method, if it doesn't exist then it checks the parent until it gets to the root and if it doesn't find the method there in the prototype then it returns undefined. This is the reason why we can call `toLowerCase()` on the name string property. This method sits on the root String object which containst the `toLowerCase` method so Javascript just searches for it up the tree until it gets to the [String prototype](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String).

Now we can fix the issue and lowercase the property name by running:
```
p1.toLower();
```

## ES6 and the class introduction
Not all developers liked the object constructor and due to the issues when missed the `new` keyword JS introduced `class` keyword. It works the same way as the above constructor function.
```
class Person {
  constructor(name){
       this.name = name; 
  }
  getName() {
    return this.name;
  }
}

const p1 = new Person('Bob');
const p2 = new Person('Mac');

// calling a method
p1.getName();
```
We can even add new methods using the prototype property.
```
Person.prototype.toLower = function() {
  this.name = this.name.toLowerCase();
}

p1.toLower();
```

The class is more of a syntactic sugar but it introduces a fix to the `new` bug. If you try creating instances and ommit the `new` keyword Javascript will return an error
` Class constructor Person cannot be invoked without 'new'`.

Interesting feature is the constructor method, as you already noticed it is used to create an instance but if we return something in the constructor that what the class will return.
```
class Person {
  constructor(name){
       return {name: name}; 
  }

  
}
```
The above will just return an object literal, but adding a prototype propperty to it won't be so easy. A more interesting example would be: 
```
class Person {
  constructor (name){
    return () => {
      return name.toLowerCase();
    }
  }
}
```
We could then invoke an instance of a class like a function:
```
const p1 = new Person('Mac');
// note we call a p1 function
console.log(p1()) // => "mac"
```

The above was just a short introduction to Objects in Javascript but hopefully it shows how objects and new instances of objects can be created.
