# Clean-Code

I recall one time I was working on adding a new feature to a project that I have never worked on before, and I read the file that I will add the new feature in, but unfortunately I understood nothing, so I read it one more time, then I asked my colleagues to read it with me, but the guy who wrote that file made sure that no one can understand it ever. So we redeveloped all the file from scratch !!
All that could have been easily avoided if & only if the code was written in a clean way from the first place.


## Functions

Functions are the most important concept in programming, writing it well from the beginning, & making it self-documented "which means that reading the function should be as if you’re reading its documentation" will save you hundreds of hours later when solving an issue or adding a new feature. 

### Small
> the first rule is that functions should be small, & the second rule is that they should be smaller 

It’s advisable to make your functions from 5 lines of code to 20 lines of code maximum,
This will help you in a lot of ways , first it assure that each function does only one task, and it will prevent you from duplicating your code.
And in order to assure that, we try to make the indent level of the functions only one or two at most. so the if else statments should only contain one level of indent, may be a single call function, this also helps with making the function more self-documented.

For example the following 2 code segments are doing the same functionality "Validating a phone number":

``` javascript

```
### Do One Thing

> Functions should do on thing, they should do it well, they should do it only

The main usage of the function is to decompose a large concept into smaller concepts, so it will make no sense to put all your logic in a single function !
one way to know  if your function is doing more than one thing, if you can extract another function from it with a name that is not merely restatement of the main function name  

### One level of abstraction 

In order to keep our functions doing only one thing, we try to maintain all the function calls within our functions to be at the same abstraction level, so you can’t have a high order function , of order four for instance, and another one of order one.
Having a lot of levels of abstractions at the function, it will not only prevent the function of doing only one thing , but also it will confuse the reader, he won’t be able to know to the essential concepts, from the details   

### Descriptive names

> You know you are working on clean code when each routine you read turns out to be pretty much what you expected

Using descriptive names is an essential for establishment the previous rule, don’t be afraid to choose a large name as long as it describes what the function does. 
And  always remember, long descriptive name , is better than short enigmatic name, and also  long descriptive name is better than long descriptive comment   

Take your time choosing the names, and also you should try different names , then try to read the whole file, and see what you understand, then modify the names, and so on.Always remember that writing a clean code , is an iterative process    
  
### Function Argument

Functions can be niladic, monadic, dyadic, triadic, or polyadic,the main rule when it comes to choosing the number of arguments is that  the less the arguments the function takes the better the function is.
Arguments are hard. They take a lot of conceptual power, the reader of the code won't be able to interpret the meaning of the arguments, or why they are important to the code.
Arguments are even harder from a testing point of view. Imagine the difficulty of writing all the test cases to ensure that all the various combinations of arguments work properly.
When a function seems to need more than two or three arguments, it is likely that some of those arguments ought to be wrapped into a class of their own.
For exapmple 
``` javascript
const makeCircle = (x, y, radius)=>{}; // bad 
const makeCircle = (center, radius)=>{}; // good
```

### Command Query Seperation

### Don't repeat yourself

