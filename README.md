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

the main usage of the function is to decompose a large concept into smaller concepts, so it will make no sence to put all your logic in a single function !
one way to know  if your function is doing more than one thing, if you can extract anthor  function from it with a name that is not merely restatment of the main function name  

### One level of abstraction 

### Descriptive names

### Function Argument

### Command Query Seperation

### Don't repeat yourself

