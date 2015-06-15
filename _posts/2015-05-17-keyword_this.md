---
title: How to use ‘this’ keyword in JavaScript
---
I just completed Week One of Hack Reactor (cohort 28: woop, woop!), and I thought I’d clear up some of the confusion around the keyword ‘this’. If you are new to JavaScript, you might have experienced the temptation of throwing the (seemingly) magical keyword ‘this’ into your code and hoping it sticks to the object you intended. However, using ‘this’ without a firm grasp of how it works in different contexts can have unexpected and frustrating results.

Thankfully, there are only five circumstances you need to understand when using the keyword ‘this’, and I’ve outlined them below. By the end of the post, you should be able to rock ‘this’ with confidence!

### 1. Global Scope

    console.log(this); // logs window;

When ‘this’ is referenced in the global scope, outside of any function body, it refers to the global object. In the case of the Chrome browser, this is ‘window’. You might be wondering why you’d need the keyword ‘this’ in the global scope if you have access to the global object directly. The answer is: you don’t. It simply binds to the global object for lack of a better alternative.

### 2. Free Function Invocation


    var fn = function() {
      console.log(this);
    };
    fn(); // logs window;


As in the global scope, referencing the keyword ‘this’ inside a free function invocation — a function not assigned to an object as a method — refers to the global object.

### 3. When using .call() or .apply() methods

    var obj1 = {
      name: "obj1", 
      fn: function(){console.log(this.name)}
    };
    var obj2 = {
      name: "obj2", 
      fn: function(){console.log(this.name)}
    };
    obj1.fn(); // logs obj1
    obj1.fn.call(obj2); // logs obj2


The .call() and .apply() methods allow you to invoke a function and specify the context for any references to ‘this’ in the function’s body. When you invoke the .call() or .apply() method on the function and pass in an argument, any references to ‘this’ in the function’s body will be re-bound to the context of the first argument.

### 4. Method Invocation

    var obj = {
      name: 'obj',
      fn:function(){console.log(this.name)}
    };
    obj.fn(); // logs obj

When calling a method on an object, any references to ‘this’ in the method’s function definition will refer to the object to the left of the dot at invocation.

### 5. When using ‘new’ in class construction

    var Class = function(value){
      this.value = value;
    };
    var instanceOfClass = new Class('sweet!');
    console.log(instanceOfClass.value); // logs sweet!

The final way the ‘this’ keyword can be used is in pseudoclassical-style class construction. When referenced in the constructor function body, every time we instantiate the class, the ‘this’ keyword will be bound to that particular instance of the class.

