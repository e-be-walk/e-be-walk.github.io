---
layout: post
title:      "Variable and Function Hoisting in JavaScript"
date:       2018-09-29 23:07:25 +0000
permalink:  variable_and_function_hoisting_in_javascript
---


It’s important to understand how hoisting can affect scope. There's two parts to hoisting that affect how are declarations are scoped- *variable hoisting* and *function hoisting*. Starting with variable declaration, it is important to note that with ES6 and the introduction of `let` and `const`, variable hoisting also had new, unique behavior. When using `var` to declare your variables, the  JavaScript engine treats all declarations as though they are within the global scope regardless of where they were actually declared. This is essentially hoisting the variable to the top level and it doesn't matter whether the `var` variable is within or outside the function. This means that the variable is actually available before it is declared.  Let’s take a look at an example:

![](https://imgur.com/RtSTUmS.jpg)

Notice that the first `console.log(salary);` doesn’t throw and error- it returns `undefined`. This means that the JavaScript engine found the `var salary` declared below but during this first console.log did not yet have the value of that variable. It’s been hoisted to the top. This powerful behavior can lead to bugs in our code if we’re not careful about how we declare variables.

If we use `let` or `const` instead of `var` within this example, the behavior for this example is essentially the same- the JavaScript Engine sees the declaration but does not know the value returning `undefined` for the first console.log. It is important to remember that `const` declarations cannot be reassigned and must be declared at the time they are initialized. Otherwise, in this particular example we’re not operating on the data and all three behavior relatively the same. It gets a bit more complicated when we throw functions into the mix. 

## Block level scoping
Block-level scoping helps to provide more control over a variable’s lifecycle. Block-level declarations were introduced with ES6 and are made within a `{ }` block. We’re going to demonstrate block-level declarations using `let` and `const` to see how that affects the availability of the variable. 

## let Declarations
The syntax of `let` is very similar to `var`. You want to place your `let` declarations a the top within a block so they’ll be available within that entire block. Let’s take a look at an example that uses `if` to evaluate for a condition.

![](https://imgur.com/hBrl5mP.jpg)

This throws an error because at the first `console.log` on line 2, the Javascript engine does not see `salary` defined and nor does it see the `let` declarations within the `if/else` blocks. The error won’t allow us to call the function on line 13- `getRaise(yearsEmployed = 6);`. If we simply comment out that console.log, our function will fire and output the predicted result to the console. 

![](https://imgur.com/CIdMFIa.jpg)

We can’t use `const` for this example because the value of the variable `salary` changes with the condition of `yearsEmployed`. Using `const `for any `salary` in this example will cause an error.

## Function Hoisting
Variable hoisting is not the same as function hoisting- it is unique in ways of its own. Remember there are 2 ways of creating functions- ***Function Declaration*** and ***Function Expression.***

In Javascript, *function declarations* hoist the function definitions. This means that these functions can be used even *before* they are declared. The syntax for function declaration is simple and the console.log is interpreted even though the function is called prior to the function definition:

![](https://imgur.com/2W8hXsq.jpg)

A ***function expression*** refers to a function defined within an expression. A function expression can be anonymous so we are free to use arrow function syntax in function expressions. They are not, however, hoisted and cannot be used before they are defined. 

![](https://imgur.com/NNnXWIn.jpg)

## Breakdown
Let’s break this down looking at another example. We’re going to essentially use the same example switching sequence of execution, variable declarations, or function declarations to see how these impact hoisting. In our first example we will use var for our variable declarations and for a function expression as well.

![](https://imgur.com/dlCnMv5.jpg)

Interesting, right? In this example we have a `var salary` in the global scope but within the function the first time it is called it is undefined. What gives? Well, because of the way the JavaScript engine runs the code it is looking for `salary` within the function block. Since there is a `var salary` within the block it recognizes it is there with the first console.log but does not yet know it’s value. The `var salary ='$1000';`  is in the global and the console.log isn’t looking for it. Look at how it changes the outcome by simply removed the `var` declaration within the block:

![](https://imgur.com/adf2dyX.jpg)

Crazy, right? Now it knows that we are adjusting the value of the `var` in the global scope when we execute the block. It shows the value of the first `salary` and changes the value. It would have the same result of moving the first `var salary` to within the block.

![](https://imgur.com/Ds0v4JW.jpg)

Now this is also a function expression- we are assigning the `var hoisting` a function definition. Remember- we can’t execute a function expression before it is defined: 
 
 ![](https://imgur.com/ky1vlgT.jpg)

If we change it to a function declaration though…

![](https://imgur.com/ChQhjcG.jpg)

It works! 

So now let’s return the example to it’s original format, but change out the vars with the new, fantastic variable declarations `let` or `const`.   If we change that first `var salary` to `const salary` we shouldn’t be able to overwrite the value in our block, right? 

![](https://imgur.com/1sf6YNr.jpg)

Wrong! It still has the same behavior it did in our first example because `const salary` is in the global scope. The block recognizes there is a `salary` variable within it and ignores the global `salary`. If we were to use `let` in this same context, it would give the same result. If we put it within our block we get the expected behavior- it throws an error when we try to overwrite the value: 

![](https://imgur.com/8ItMav2.jpg)

Now, if we try to use `let` within the block what do you think will happen? You might expect it to have the same behavior- returning undefined in the first call and logging the `’$5000’` as part of the second console.log, right? 

![](https://imgur.com/DkMNoA7.jpg)

Surprisingly- no! It doesn’t recognize the variable declaration within the block if you use let and it will throw and error halting further execution. It’s the same if you switch that `let` in the 7th line to `const`. If you are using `let` or `const` within the block the only way this will work is if it is declared in the top line within the block, and omitting the keyword when you try to overwrite the value:

![](https://imgur.com/kKDyvsT.jpg)

Pretty neat, huh? Little differences in the way we make declarations— in both functions AND variables can make a big difference in the way JavaScript reads our code. This is so important to keep in mind because it also affects the scope in which these declarations are hoisted.  

