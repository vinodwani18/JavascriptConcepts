Prototype(__proto__) and prorotypal inheritance in Javascript.

---------------------------------------------------------------

Everything in JS is object.
So when we will check for Object prototype in console we can see below result(As shown in below image).
And when we will dig till the end of prototype chaining we can see null. 
That means nothing is there to inherit after that and its end of prototype chaining.
![ObjectPrototype](https://github.com/vinodwani18/JavascriptConcepts/blob/main/Images/ObjectPrototype.png)

If we will check for the Array prototype and Function prototype we will get below result(As shown in below image).
Here firstly we can see Array __proto__ then we can see Object __proto__ because Array is inherited from Object.
![ArrayPrototype](https://github.com/vinodwani18/JavascriptConcepts/blob/main/Images/ArrayPrototype.png)

Same will be the case for Function.
![FunctionPrototype](https://github.com/vinodwani18/JavascriptConcepts/blob/main/Images/FunctionPrototype.png)


