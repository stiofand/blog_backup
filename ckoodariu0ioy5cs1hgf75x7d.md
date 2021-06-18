## Foundational functional programming, part II

In part [1](https://thebarefootdev.com/foundational-functional-programming-part-i) of this overview, we looked briefly at the character of the functional programming paradigm, what it is, and what it isn't. We saw its complexity has often been misconstrued and confused with somewhat heavier implementations, usually within more scientific domains. We outlined some basic symptoms that provide a functional perspective, and it is these that we will investigate in this section in more detail.


### JavaScript ###
In the examples, I choose to use Javascript. This is for a number of reasons, predominantly for its popularity and recognition. It's so widely used that it is easier to show examples to avoid having to explain the nuances of a different language. Next javascript is a rather flexible language, it's constructs allow a wider approach to programming; its lack of opinionative structure, it's dynamic typing, and prototypical inheritance chain means one can be Object Orientated, Functional, or, as is common, a  mix of both. It is also widely applicable to both browser environments and windowless, server environments, it can be written and tested with minimal setup and requires no boilerplate or client-server architecture to get it running, certainly in the examples we provide.

#### Note
One side note, however, is that whereas, Javascript's benefits I have pointed out above, can at times prove also detrimental in certain contexts. Dynamic typing also means a lack of types, and this could lead to a whole range of issues in themselves, it's flexibility also means that one needs to be cautious of implementations that could cause memory leaks for example. Of course, we need not be too cognizant of these examples, but it is nonetheless an important consideration should you choose a functional approach to your domain problems in JavaScript


### Examples
So let us take a small peek into what these functional programming symptoms and features are. In case you have not read the first section of this precis, I provided the following as facets to programming with the functional paradigm.

- Expressions over Statements. (+)
- Declarative programming.
- Purity (avoiding side effects). (+)
- First-class  & Higher-order functions. (+)
- Currying, and partial application.
- Function Composition.

 ** (+) Particularly representative of functional programming**

**ƛ Expressions over Statements.**

In the functional paradigm, the form works on the data, that is data in, data out to all functions. to follow the functional paradigm, all your functions should return a value. There is more to this we describe on this later, but this means avoid writing statements, (a declarative form which does something but does not necessarily return anything after that work) and provide an expression, a form that takes in data and returns data.

```javascript

// Statement (nothing returned)
function myFunction(){
  console.log('I dont return anything!');
}

// Function expression (returns value)
function betterRound(num){
  return +(Math.round(num + "e+2")  + "e-2");
}

// Function expression (returns value)
function radius(r){
  const { PI, pow } = Math
  return betterRound(PI * pow(r,2))
}

// Arrow function expression (returns value)
const rad = r => betterRound(Math.PI * Math.pow(r,2))

```
---

**ƛ Declarative Programming (paradigm)**

Ok, so this is a little verbose to exemplify, but in its simplest form, it is the approach to writing data transformation functions with an intended outcome regardless of how it is achieved. For example, if you are looking to make a cake, the declarative paradigm would be, "make a cake, it doesn't matter how you do it". Whereas in a more "imperative" form you would follow recipe directions, step by step. How do we illustrate such an approach in code? Here we will use the concept of handling a  browser button click and changing the color of text the first example shows a step-by-step, imperative approach, the second a more declarative approach. 

#### Note
The more informed amongst you may notice that this isn't entirely functional as we are using a global state and manipulating it, however, we shall ignore this for the purposes of this particular example, though it does show, that an absolute functional paradigm is not truly achievable in many aspects, particularly in web programming! 

-- Imperative approach (step by step) (assume all references are valid)


%[https://codepen.io/thebarefootdev/pen/WNpwZpX]

-- declarative approach, abstract the functionality so it doesn't matter.

%[https://codepen.io/thebarefootdev/pen/xxqVXmb]

Ok, so these are rather involved examples (remember you can see the javaScript by selecting the JS tab), and I had to mimic react a little, but the point here is the first example is using an imperative approach whilst the second a declarative one, which is a feature in the functional paradigm.

* __imperative__  -> step by step (recipie like)
* __declarative__ -> indicate intention, but not implementation

___

**ƛ Purity (avoiding side effects).**

This is probably one of the most important features of the functional paradigm. It has long been debated as to what this really means, and how far one should strive to achieve functional purity if indeed its benefits would be seen at all in the context of the domain in which it is being used. Yet what is it, what does it mean if a function is pure? Fundamentally, it refers to the absence of any "side-effects" caused by the transformation in the function itself. Side-effects refer to changes caused by the functions (mutations) (commonly, global references outside the function scope, app state, or any other resource reference that does not return a value from the call, for example, any I.O functionality such as console.log in javaScript. The following examples outline these main credentials to be pure, and whats "impure" 

```javascript

let appState = { count: 0 };
const myArray = [1,2,3];

/********************
* impure examples 
********************/

// 1 > Some AppState change in place
function updateAppState(){
   appState.count++
}

// 2 > Mutates Original Array
function addToArray(n){
  myArray.push(n)
}

// 3 IO operation (no value returned and IO is affected)
function soSomething(){
   console.log('appState');
}

/********************
*pure(r) examples 
********************/

// 1 >  returns new updated AppState (with incremented count) E
function updateAppState(_appState){
  return  Object.assign(null,{ count: _appState.count +1})
}

// 1a > (using ES6 arrow fn +  spread operator) returns new updated AppState (with incremented count) E
const updateAppState = _appState => ({
     ...._appState,
     count: _appState.count + 1
 });

// 2 > returns new array with extra item
function add(arr,n){
  const a = arr.slice()
  a.push(n)
  return a
}

// 2a > (Using ES6 arrow fn +  rest operator) returns new array with extra item
const add = (arr, n) => [...arr,n]

// There is no functional alternative to console.log or any IO, it's a necessary side-effect for the most part, but usually only part of debugging code, it should never be provided in production for any reason.
```

---
**ƛ First-class  & Higher-order functions.**

This is another fundamental feature of the functional paradigm. First-class functions are functions that can be moved about the code and reused like regular object and object references, they can be assigned to other functions, returned from functions, and passed as function parameters. This is significant because the ability to do this in a language is often limited and can be a decisive factor when choosing a technology if there is a need to go functional. Higher-order functions (HOC) relate to this as these are functions that can receive other functions as arguments.

```javascript
// Declare a core function
function greeter(name, greeting){
  return greeting + name
}

// Assign a partially applied function expression
function sayHello(name){
  return greeter(name, "Hello ")
}

// assigns function to  a new reference
const myGreeter = function (){
  return sayHello("John Smith")
}

// assigns function to  a new reference
const helloJohnGreeter = myGreeter

console.log(helloJohnGreeter()) // "Hello John Smith"


// functions as array items
const f1 = () => 1;
const f2 = () => 2;
const f3 = () => 3;
const f4 = () => 4;
const f5 = () => 5;

function callAll(funcArray){
 // map is a HOC as it can take a function as a parameter
  return funcArray.map(fn => fn())
}

const fnArray = [f1,f2,f3,f4,f5]

const results = callAll(fnArray);

console.log(results) // [1,2,3,4,5]

```

These are very derived examples but are used to show the concept of First class (as an object) functions and HOC (take functions as parameters). From the example above we use the inbuilt javaScript function "map" which we will come to see represents all the primary traits of functional programming, as well as reduce and filter. These we will see in the final installment of this series, as a representation of the functional paradigm.

---

** ƛ Currying, and partial application**

Partial application is the ability to *partially apply * a function to a new reference or function so that "function composition" is better constructed, and the DRY principle is met (Do not repeat yourself). Often, currying and partial application are conflated and confused. Currying could be said to be merely a more involved derivate of the partial application function, though the primary difference between a curried function and a partially applied function is that the partially applied function usually returns almost immediately, rather than reducing any further steps down as in currying. Often currying can look like a range of partially applied functions.

Currying is a technique that isn't a code application in itself. but merely a method to transform functions themselves rather than data. Wikipedia, states that in computer science and mathematics,

> currying is the technique of converting a function that takes multiple arguments into a sequence of functions that each takes a single argument.

This can be a little confusing at first so we will relate to the examples here to exemplify. Currying can often be complicated in theory, but in code things often are less involved.

Partial function application is the basis for currying and both are a very comprehensive way to compose functions which we will look at later.  Within these features, is the concept of a *closure* is applied. A closure is a variable scope available to an inner scope or function that has been given from its outer parent function

##### Partial function application

```javascript
const add = (a,b,c) => a + b +c;
const addToNumber = n1 => (n2,n3) => adder (n1,n2,n3) // Partially applied (via closure)
const add2toNumber = addToNumber(2)
add5toNumber(3,10) // 15
```

##### Currying

```javascript
const add = (a,b,c) => a + b +c;
const addToNumber = n1 => n2 => n3 => add(n1,n2n3);
addToNumber(2)(3)(10) // 15
```

In both Partial function application and currying, closures, allow the scope to return another function as needed with access to the outer scope arguments and variables, and to take in new parameters. For Partial application, these can be set on the assignment to the reference holding the partially applied function, which gives it the "partial" application character

```const add2toNumber = addToNumber(2)```

for the curried function, extra params are commonly passed via the return function scope passed into the closure from the call chain.

```javascript
// ES6
const addToNumber = n1 => n2 => n3 => add(n1,n2n3);
 
// Regular syntax // creating inner closure scope each call
function addToNumber(n1){
  return function(n2){
    return function(n3){
       return n1 + n2 + n3
    }
  }
}

```
---

OK, that's all for this installment. I hope you were able to follow along, if not drop me a line or have a good google about it, there is tons of information out there. Remember Functional programming paradigm, is not exclusive to javascript, many languages functional and not provide the ability to construct these approaches. 

In the next installment, we will look at function composition and how several in-built javascript functions fulfill the criteria for functional programming, we will see these in action and then provide a final brief discussion on the core benefits of functional programming, and where to go from there. Thanks for reading.


