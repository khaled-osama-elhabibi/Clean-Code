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
For exapmle 

``` javascript
const flag = () =>!firstname || !lastname || !telephone ; // bad
const AreAllFieldsAreEntered = () =>!firstname || !lastname || !telephone ; // good
```
  
### Function Argument

Functions can be niladic, monadic, dyadic, triadic, or polyadic,the main rule when it comes to choosing the number of arguments is that  the less the arguments the function takes the better the function is.
Arguments are hard. They take a lot of conceptual power, the reader of the code won't be able to interpret the meaning of the arguments, or why they are important to the code.
Arguments are even harder from a testing point of view. Imagine the difficulty of writing all the test cases to ensure that all the various combinations of arguments work properly.
When a function seems to need more than two or three arguments, it is likely that some of those arguments ought to be wrapped into a class of their own.
For exapmle 
``` javascript
const makeCircle = (x, y, radius)=>{}; // bad 
const makeCircle = (center, radius)=>{}; // good
```
### Have No Side Effects

> Side effects are lies. Your function promises to do one thing, but it also does other hidden things.

Functions can't do a hidden side effects, that will make it very hard in debugging for an issue, it will help you achieve the rule that we already established , "You know you are working on clean code when each routine you read turns out to be pretty much what you expected"
``` javascript
function checkPassword(userName,password) {
   const user = UserGateway.findByName(userName);
   if (user !== null) {
     const codedPhrase = user.getPhraseEncodedByPassword();
     const phrase = cryptographer.decrypt(codedPhrase, password);
     if ("Valid Password".equals(phrase)) {
       Session.initialize();
       return true;
     }
   }
   return false;
 }
```
the previous function said that it will only check the password, so it will supposed to return only true or false, but instead it ``` Session.initialize() ``` when the password  is valid.
This side effect creates a temporal coupling. That is, checkPassword can only be called at certain times (in other words, when it is safe to initialize the session).
In order to fix the previous function, we can rename it to be ```checkPasswordAndInitializeSession``` 

### Command Query Seperation
 
> Functions should either do something or answer something, but not both. 

The previous has another problem even after the renaming, it answers a question, which is whether the password is  valid or not, and it  does a thing which is initialization of the seesion
We can improve it by seperate between the checking, & the initialization
``` javascript
function intializeSession(){
  if (checkPassword(userName,password))
    Session.initialize();   
}
function checkPassword(userName,password) {
   const user = UserGateway.findByName(userName);
   if (user !== null) {
     const codedPhrase = user.getPhraseEncodedByPassword();
     const phrase = cryptographer.decrypt(codedPhrase, password);
     if ("Valid Password".equals(phrase)) {
       return true;
     }
   }
   return false;
 }
```
### Prefer Exceptions to Returning Error Codes

Functions should do one thing. Error handing is one thing. Thus, a function that handles errors should do nothing else.

For example :
``` javascript
// bad code -->
  const Delete = () => {
    if (deletePage(page) === E_OK) {
      if (registry.deleteReference(page.name) === E_OK) {
        if (configKeys.deleteKey(page.name.makeKey()) === E_OK) {
          console.error("page deleted");
        } else {
          console.error("configKey not deleted");
        }
      } else {
        console.error("deleteReference from registry failed");
      }
    } else {
      console.error("delete failed");
      return E_ERROR;
    }
  };
  
// a better code would be -->
const deletePageAndAllReferences = (page) => {
  deletePage(page);
  registry.deleteReference(page.name);
  configKeys.deleteKey(page.name.makeKey());
}
const delete = (page) => {
  try {
    deletePageAndAllReferences(page);
  }
  catch (Exception e) {
    console.error(e);
  }
}
```
Try/catch blocks are ugly in their own right. They confuse the structure of the code and mix error processing with normal processing. So we extracted the bodies of the try and catch blocks out into functions of their own.

### Don't repeat yourself

Duplication may be the root of all evil in software. Many principles and practices have been created for the purpose of controlling or eliminating it
And as a web developers, using the modern frameworks we have a state management systems we can use to eliminate any duplication in our application, 
so if we have a function for fetching data about a user cart - for an Ecommerce App - in the cart screen, and we need also to get that data in the checkout screen, or in the store screen, then we have to put that function as a method  in our store.

Invention of the subroutine in software development have been an ongoing attempt to eliminate duplication from our source code. So don't let it go to waste!!

### Final Advise 
 
**Writing software is like any other kind of writing. When you write a paper or an article, you get your thoughts down first, then you massage it until it reads well. The first draft might be clumsy and disorganized, so you wordsmith it and restructure it and refine it until it reads the way you want it to read.**

So First We make it work, then we make it right  


















