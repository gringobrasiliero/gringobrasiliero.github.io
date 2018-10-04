---
layout: post
title:      "Higher Order Functions"
date:       2018-10-04 10:16:47 +0000
permalink:  higher_order_functions
---


JavaScript Arrays have a few methods that are Higher Order Functions. A higher order function is one that accepts another function as an argument. Today, we are going to take a look at a few of the popular ones, which are: .map(), .filter(), and .sort().

## .map()
When you use .map(), It transforms an array by applying a function to each of the elements within that array, and returns a new array with the returned values. For example, lets say you have an array of peoples ages, and it is everyone’s birthday. We now want to increase everyone’s age by one. 

```
const ages = [3, 5, 7, 94, 24, 6, 28];

let newAge = ages.map(age => age + 1);

console.log(ages)

// [3, 5, 7, 94, 24, 6, 28]

console.log(newAge)

//[3, 5, 7, 94, 24, 6, 28]
```

As you can see, we mapped over each one of the elements, and now we have everybody’s new age. We also kept the original values of the array. 
You use .map() when you want to transform every element of an array.
## .filter()
Another array method you can use is .filter(). This allows you to return a new array that filters out values that come out to be false. Lets say you want the get the ages of people who are legal to drink.

```
let ages = [3, 5, 7, 94, 24, 6, 28]
let legal = ages.filter(age => age >= 21);

console.log(legal)
//[94, 24, 28]
```

We called filter on the array of ages, and for each element in the array, we pass the arrow function that implicitly returns a Boolean value. If the returned value is true, it stores the element into the new array. If not, it skips over that element. 

## .sort()
Lets say that you wanted to sort all of the ages in order from youngest to oldest. Using .sort() would do the trick for you. When you use sort, it does not create a new array, but edits the existing array. For example:
 
```
ages = [3, 5, 7, 94, 24, 6, 28]
console.log(ages)
//[3, 5, 7, 94, 24, 6, 28]
ages.sort()
console.log(ages)
//[3,5,6,7,24,28,94]
```

It was also really easy to implement right? It does work in this case, however, if you include uppercase and lowercase values, want to sort in descending order, or objects within the array that you are sorting…

```
let people = [ { name: 'Nolan', age: 28 },
  { name: 'Buzz', age: 6 },
	{ name: 'Woody', age: 50 },
  { name: 'Mr. Potato Head', age: 18 } ]
										
ages.sort()

console.log(ages)

// [ { name: 'Nolan', age: 28 },
  { name: 'Buzz', age: 6 },
  { name: 'Woody', age: 50 },
  { name: 'Mr. Potato Head', age: 18 } ]
```
It does not sort them at all. In this case, sort does not know what to sort within the object, so we need to compare the age value by including your own comparing function. We pass a function within the sort function, which makes it a higher order function. 

```
let people = [ { name: 'Nolan', age: 28 },
  { name: 'Buzz', age: 6 },
	{ name: 'Woody', age: 50 },
  { name: 'Mr. Potato Head', age: 18 } ]

people.sort((a, b) => (a.age-b.age))

//[ { name: 'Buzz', age: 6 },
  { name: 'Mr. Potato Head', age: 18 },
  { name: 'Nolan', age: 28 },
  { name: 'Woody', age: 50 } ]
```

Passing this function within sort, we are able to sort the objects based on the properties of the object. 
It also works with strings, but we will have to use localeCompare to make sure there isn't confusion between capital and lowercase letters.

*Note: localeCompare() returns a number indicating whether a reference string comes before or after or is the same as the given string in sort order. It returns 0 if the strings are a match, 1 if the parameter value comes before the string object value, and -1 if the parameter value comes after the string object value.*


```
let people = [{name: “Nolan”, age: 28},
              {name: “buzz”, age: 6},
		      {name: “woody”, age: 50},
		      {name: “Mr. Potato Head”, age: 18},
		      {name: “Chelsea”, age: 30},
		      {name: “mr. Potato Head”, age: 18},
			  {name: “Evan”, age: 26}]
													
people.sort((a, b) => (a.name.localeCompare(b.name))
console.log(ages)

//[ { name: 'buzz', age: 6 },
  { name: 'Chelsea', age: 30 },
  { name: 'Evan', age: 26 },
  { name: 'mr potato head', age: 21 },
  { name: 'Nolan', age: 28 },
  { name: 'rex', age: 18 },
  { name: 'woody', age: 50 } ]
```


## Chaining
As you can see, it put the names in alphabetical order, but it is annoying to see how some of the names are not capitalized. We can fix this chaining the .map() and .sort() together, mapping over each one of the peoples names, making sure that their name is capitalized, and then sort them by their names in alphabetical order.

```
let people = [{name: “Nolan”, age: 28},
              {name: “buzz”, age: 6},
		      {name: “woody”, age: 50},
		      {name: “Mr. Potato Head”, age: 18},
		      {name: “Chelsea”, age: 30},
		      {name: “mr. Potato Head”, age: 18},
			  {name: “Evan”, age: 26}]
													
let capitalNamesSorted = people.map(person => ({name: (person.name.charAt(0).toUpperCase() + person.name.slice(1)), age: person.age}))
.sort((a,b) => (a.name.localeCompare(b.name)));

console.log(capitalNamesSorted)

// [ { name: 'Buzz', age: 6 },
  { name: 'Chelsea', age: 30 },
  { name: 'Evan', age: 26 },
  { name: 'Mr potato head', age: 21 },
  { name: 'Nolan', age: 28 },
  { name: 'Rex', age: 18 },
  { name: 'Woody', age: 50 } ]
```
 

Using ES6 arrow functions makes it a lot easier to chain these functions together. This is what our code would look like if we were using ES5 functions to achieve the same result, but also filtering out the ones that are not 21 and up.

```
let capitalNames = people.map(function(person) {
  return {name: (person.name.charAt(0).toUpperCase() + person.name.slice(1)), age: person.age}
}).sort(function(a,b) {
  return (a.name.localeCompare(b.name))
}).filter(function(person){
  return (person.age >= 21)
})
console.log(capitalNames)

// [ { name: 'Chelsea', age: 30 },
     { name: 'Evan', age: 26 },
     { name: 'Mr. potato head', age: 21 },
     { name: 'Nolan', age: 28 },
     { name: 'Woody', age: 50 } ]

```
Compare the code above, to the function below written in ES6.

```
let capitalNames = people.map(person => ({name: (person.name.charAt(0).toUpperCase() + person.name.slice(1)), age: person.age}))
.sort((a,b) => (a.name.localeCompare(b.name))).filter(person => person.age >= 21);
```
Much cleaner and easier to read right? The only issue that you may run into is that Internet Explorer does not support ES6 arrow functions. Who uses IE anyways?


