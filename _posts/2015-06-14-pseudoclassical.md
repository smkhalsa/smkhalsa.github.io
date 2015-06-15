---
title: Prototypical vs Pseudoclassical Pattern
---

Classes are a core feature of Javascript which make it easier to write complex and powerful functionality. However, Javascript has four different patterns for creating and instantiating classes, and it can sometimes be easy to confuse them. 

The four patterns are:
1.  Functional
2.  Functional-shared
3.  Prototypical
4.  Pseudoclassical

In this post, I will compare two of the most popular patterns: Prototypical and Pseudoclassical.

### Prototypical

    var Animal = function(name) {
      var animal = Object.create(Animal.prototype);
      animal.name = name;
      return animal;
    }
    Animal.prototype.shout = function(message) {
      alert(message);
    };

    var lion = Animal('Scar');
    console.log(lion.name); // logs 'Scar'
    lion.shout('Roar!!!!'); // alerts 'Roar!!!!'

### Pseudoclassical

    var Animal = function(name) {
      this.name = name;
    }
    Animal.prototype.shout = function(message) {
      alert(message);
    };

    var lion = new Animal('Scar');
    console.log(lion.name); // logs 'Scar'
    lion.shout('Roar!!!!'); // alerts 'Roar!!!!'

As you can see, these patterns are very similar. When defining the class, you may have noticed that the prototypical pattern has a few extra steps. Namely, you must call the Object.create function with the class's prototype object to pass in all the associated methods. Then we must assign any properties that are passed in at instantiation. Finally, we must return our new object. 

The pseudoclassical pattern bypasses most of these steps. By including the 'new' keyword when we instantiate a new class, the interpreter will automatically inject the code that creates a new object and then will return it. Furthermore, it will bind the keyword 'this' to the new instance of the class, allowing us to assign properties in the class constructor function body using 'this'.

For these reasons, many engineers (including myself) prefer the pseudoclassical pattern. 