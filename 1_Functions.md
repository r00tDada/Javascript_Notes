# Functions

1. Functions in Javascript are objects.
2. Objects are collections of name/value pairs having hidden link to a prototype object.
3. Functions objects are linked to **Function.prototype** which is itself linked to **Object.prototype**
4. Functions can be stored in variables, objects, and arrays. Functions can be passed as arguments to functions, and functions can be returned from functions. Also, since functions are objects, functions can have methods.
5. Every function is also created with two additional hidden properties: the function’s context and the code that implements the function’s behavior.
6. Every function object is also created with a prototype property. Its value is an object with a constructor property whose value is the function. This is distinct from the hidden link to Function.prototype.

### Function Literal

1. Functions can be defined inside of other functions. An inner function, of course, has access to its parameters and variables. An inner function also enjoys access to the parameters and variables of the functions it is nested within.
   The function object created by a function literal contains a link to that outer context. This is called **closure**

### Invocation

1. Every function receives two additional parameters: this, arguments. The this parameter’s value is different base on the invocation pattern.
   There are four patterns of invocation in JavaScript:

- the method invocation pattern
- the function invocation pattern
- the constructor invocation pattern
- the apply invocation pattern

#### The Method Invocation Pattern

this is bound to that object (eg: fooObject in the example below).
The binding of this to the object happens at invocation time. This very late binding makes functions that use this highly reusable. Methods that get their object context from this are called public methods.

    var fooObject = {  
    value: 0,  
    increment: function (inc) {  
    this.value += typeof inc === 'number' ? inc : 1;   }  
    };  
    fooObject.increment();  
    document.writeln(fooObject.value); // 1   
    fooObject.increment(2);  
    document.writeln(fooObject.value); // 3  

#### The Function Invocation Pattern

If a function is not the property of an object, then it is invoked as a function. In this case the this is bound to the global object (Window object in browser). The expectation is that when the inner function is invoked, this would still be bound to the this variable of the outer function. Solution for this case: the method defines a variable and assigns it the value of this, the inner function will have access to this through that variable.


        // Augment myObject with a double method.  
        myObject.double = function () {  
        var that = this; // Workaround.  
        var helper = function () {   
        that.value = add(that.value, that.value);  
        };  
        helper(); // Invoke helper as a function. };  
        // Invoke double as a method.  
        myObject.double( ); document.writeln(myObject.getValue()); // 6  

#### The Constructor Invocation Pattern

**JavaScript is a prototypal inheritance language. That means that objects can inherit properties directly from other objects. The language is class-free.**

If a function is invoked with the new prefix, then a new object will be created with a hidden link to the value of the function’s prototype member, and this will be bound to that new object.

    // Create a constructor function called Boo.  
    // It makes an object with a status property.  
    var Boo = function (string) { this.status = string; };   
    // Give all instances of Boo a public method  
    // called get_status  
    Boo.prototype.get_status = function () {  
        return this.status;  
    };  
    // Make an instance of Boo.  
    var myBoo = new Boo("I dont know");  
    document.writeln(myBoo.get_status()); // I dont know  

Functions that are intended to be used with the new prefix are called constructors. By convention, they are kept in variables with a capitalized name. If a constructor is called without the new prefix, very bad things can happen without a compile-time or runtime warning, so the capitalization convention is really important.


#### The Apply Invocation Pattern

**Because JavaScript is a functional object-oriented language, functions can have methods.**

The apply method lets us construct an array of arguments to use to invoke a function. It also lets us choose the value of this. The apply method takes two parameters. The first is the value that should be bound to this. The second is an array of parameters.

    // Make an array of 2 numbers and add them.
        var array = [3, 4];
        var sum = add.apply(null, array);    // sum is 7
        // Make an object with a status member.
        var statusObject = {
            status: 'A-OK'
    };
        // statusObject does not inherit from Quo.prototype,
        // but we can invoke the get_status method on
        // statusObject even though statusObject does not have
        // a get_status method.
        var status = Quo.prototype.get_status.apply(statusObject);
            // status is 'A-OK'
