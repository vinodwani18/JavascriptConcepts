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

---------------------------------------

- In Javascript we can see we have access to some of the properties on Object for ex. obj.toString()
How we will get these properties on object? or how we get access for array.length ?

- In javascript whenever we will create an object or array or function, javascript engine attaches all these properties or function to it without let us know.
And these properties are added on prototype.

For ex. if we have below object.
const object = {
	name: "Vinod",
	city: "Pune",
	getUserInfo: function(country) {
		console.log( "NAME: " + this.name + " CITY: " + this.city + " COUNTRY: " + country);
	}
};

Javascript engine will attach name, city, getUserInfo properties to object but along with that it will have more inbuild prperties which can be see in its proto.

![objectWithItsProperties](https://github.com/vinodwani18/JavascriptConcepts/blob/main/Images/objectWithItsProperties.png)

Lets create one more object as below and add object to its __proto__

const object2 = {
	name: "Jonn",
}

![object2WithItsProperties_inheritance](https://github.com/vinodwani18/JavascriptConcepts/blob/main/Images/object2WithItsProperties_inheritance.png)

This is called prorotypal inheritance in javascript. Where object2 is child and it can access properties and methods of its parent object.

