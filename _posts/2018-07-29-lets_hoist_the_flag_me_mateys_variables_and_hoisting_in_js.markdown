---
layout: post
title:      "Lets Hoist the Flag me Mateys (Variables and Hoisting in JS)"
date:       2018-07-29 18:32:03 +0000
permalink:  lets_hoist_the_flag_me_mateys_variables_and_hoisting_in_js
---


You are a captain of a ship, sailing the seven seas with your crew. The first thing the crew does before you set sail, is hoist the good ole’ Jolly Roger to the top of the flag pole. This is a job for your crew, since you are too busy counting your Dubloons, and fortunately, they do it automatically, and you do not need to tell them to do so. There are also many variables around you while you sail through the JavaScript ocean, at the global scope, functional scope, and block scope. I want to have you prepared and understand how your crew works, and understand variables at a deeper level before you have your crew hoist the good ole' Jolly Roger.    


## Variables

### Global Scope

In the seven seas, there are multiple ships. You can see each ship as its own function, as each ship has its own mission. Within the global scope of a JavaScript Program(the seven seas), you have access to the functions(ships) and variables, such as dubloons, coconuts, and fish, as long as they are declared.  

```
let coconuts = 50;
function yourShip(){
let yourCoconuts = coconuts;
console.log(yourCoconuts)
//50
coconuts = 0
console.log(coconuts)
//0
}

yourShip()
```


### Function Scope

Inside each function(ship), there is a crew that performs a specific job, as well as resources inside of this ship. The resources are Variables, and you can not have access to those resources(variables), unless you are inside of that particular ship. 

```
function pirateShip() {
let theirDubloons = 1000;
}
console.log(theirDubloons)
// Uncaught ReferenceError: theirDubloons is not defined 
```

### Block Scope

Let and const are also block scoped. 

```
If (true){explaining this js

Const flag = “Jolly Roger”;
Let coconuts = 50
}
Console.log(flag)
// Uncaught ReferenceError: flag is not defined

Console.log(coconuts)
// Uncaught ReferenceError: coconuts is not defined
```

Var is NOT block scoped! 

``` 
If (true){
var dubloons = 42;
}
Console.log(dubloons)
// 42
```

It is a good practice to avoid using var whenever possible. 


### Global Variables

If you do not lock up your precious Dubloons, then other pirates will be able to use and take them. If you forget to use var, let, or const when you are declaring a variable, it will make it global, and other functions will have access to it.  

```
function yourShip() {
dubloons = 1000;
}

function pirates(){
let stolenDubloons = dubloons;
console.log(stolenDubloons);
//1000
dubloons = 0;
}

yourShip()
pirates()
console.log(dubloons)
// 0
```

If you forget to include var, let, or const when you declare the variable, that variable is a global variable, and your dubloons are free for the taking. 

## Hoisting

### Hoisting Functions

You would think that before a function is called, it must be defined. It may be the case in most programming languages, but not in JavaScript. 

```
goFish()
function goFish() {
console.log(“I caught a fish!”)
}
// I caught a fish!
```

What? How can you go fish, if you do not know how to fish yet? In Javascript, when you run a program, it goes through 2 phases. The Compliation phase, and the execution phase. In the compliation phase, JavaScript reads the entire program, and stores the functions and variables into memory. It then goes through the execution phase, and executes the functions that you called. 
We call this hoisting because it is as if the declarations are being hoisted to the top of the current scope. 

As soon as you and your crew set sailing, the first thing your crew does is hoist the flag, allowing your Jolly Rodger to flap in the wind. There is no need to tell the crew to do so, as they know it is their responsibility to do it as soon as you begin sailing. JavaScript functions do the same thing! As soon as you run a function, they immediately raise the variable declarations to the top of the scope. 

### Variable Hoisting

Variables also get hoisted to the top of their current scope. To avoid confusion, you need to declare your variables on top of the scope they are in. 
When variables are hoisted, the variable gets initialized at the top of the function, but no value is assigned to it. 
```
function hello(){
console.log(greeting + “ lets get some dubloons!)
var greeting = ‘Ahoy me mateys’
}
greeting()
// undefined lets get some dubloons!
```

When you use var, it hoists the declaration of the variable to the top, and lets you run the program, and when you call the variable, it just comes up as undefined. This is another reason why we want to avoid using var. if you use let or const, it still gets hoisted, however, the JavaScript engine does not allow them to be referenced before they are initialized.

```
function hello(){
console.log(greeting + “ lets get some dubloons!)
let greeting = ‘Ahoy me mateys’
}
Hello()
// ERROR: Uncaught ReferenceError: greeting is not defined
```

## What is THIS?

This refers to the object that owns the space that this is currently in. If you console.log this at the global scope, it refers to the window object. 

```
Console.log(this)
// Window
```
However, if you put this into a function, it comes back as an object.

```
Function afunction() {
Console.log(this)
}
//Object
```
```
class Pirate {
  constructor(name, ship) {
    this.name = name;
    this.ship = ship;
  }
 
  piratesName() {
    console.log(`The Pirates name is ${this.name}`);
  }
}
captain.piratesName()
// The Pirates name is Hook
Davey.piratesName()
// The Pirates name is Davey Crockett
```

Using this in the constructor for the Pirate Class, this is referring to the owner of that space, which is the class Pirate. Lets create some pirates. 

```
var captain = new Pirate("Hook", "pirate ship")
var davey = new Pirate("Davey Crockett", "pirate ship")
```

When you create a new pirate, with the name and ship as the parameters, it assigns the name to “this” name, which belongs to the Pirate. Now if we use the function piratesName()

```
class Pirate {
  constructor(name, ship) {
    this.name = name;
    this.ship = ship;
  }
 
  piratesName() {
    console.log(`The Pirates name is ${this.name}`);
  }
}
captain.piratesName()
// The Pirates name is Hook
Davey.piratesName()
// The Pirates name is Davey Crockett
```

When you call captain.piratesName(), the function is calling on ${this.name}. the owner of ‘this’ is the captain. ${this.name} refers to the captains name, which is Hook. 
It is the same with davey.piratesName(). It is calling on ${this.name}, which in this context, ‘this’ is referring to davey. Davey’s name is “Davey Crockett.  
This can be confusing, but the great takeaway of all of ‘this’, is that if ‘this’ is referenced inside of a function or method, it equals the object that ‘this’ is inside of. If it is in the global scope, this is global. 

I hope you enjoyed! Don’t forget to lock up your dubloons by claiming your variable as const or let, and avoid using var at all costs to prevent confusing yourself and your crew.  Happy Coding and Happy Sailing!

