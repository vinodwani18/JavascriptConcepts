What is Javascript- this with Call, Apply, Bind and arrow function?
====================================
Reference: 
https://www.youtube.com/watch?v=hwoU8NCICSE

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions

https://www.freecodecamp.org/news/javascript-arrow-functions-in-depth/#:~:text=Arrow%20Functions%20Don't%20Have%20this%20Binding,-One%20significant%20difference&text=In%20a%20regular%20function%2C%20the,which%20you%20define%20the%20function.
----------

When we console below statement it will give us window object. That means on global scope 'this' is nothing but window object.

```
console.log(this); // window
```

```
function gfFunction() {
	console.log(this);
}

gfFunction();
// We can also call above fn as below which will give us window object as fn is in global scope.
window.gfFunction();
```

```
let bfObject = {
	name: "Atul Jha",
	age: "21",
	gfFunction: function() {
    	console.log(this); //bfObject
    }
}

bfObject.gfFunction();
```
// In Above code console log will give us bfObject as we are callig gfFunction with object itself.

//When Called wrt window by passing reference it will give us window object as no object present while calling fn.

```
const gfRefFunction = bfObject.gfFunction;

gfRefFunction(); // window
```

Thumbrule: If there is no oject present while calling function then it will point to window object only
In strict mode if there is no object present while calling function then it will be undefined object.

```
const bf1object = {
	name: "Rahul",
	age: "30",
	car: "Ola Auto",
	gfFunction: function(a,b) {
		console.log(a,b, this); //
	}

}

const bf2object = {
	name: "Amit",
	age: "24",
	car: 'Mercedez",
	gfFunction: function(a,b) {
		console.log(a, b, this); //
	}

}

bf1object.gfFucntion(2, 3); // Rahul obj as called with bf1object

bf1object.gfFucntion.call(bf2object, 2, 3); // Amit obj - because changed the object reference
```
In above code we are calling function of bf1object and while calling providing reference of bf2object thats why console will show bf2object details.

If we dont want to change the reference then we have to bind the bf1object with it as shown below

```
const wifeFunction = bf1object.gfFucntion.bind(bf1object);
wifeFunction(); // Rahul obj
```

Advance:
========
When this present inside async method.

```
const obj ={
	value: "42",
	regularMethod: function(){
		setTimeOut(function() {
			console.log("Regular method this", this.value);
			
		}, 1000);
	},
	arrowMethod: function() {
		setTimeOut(() => {
			console.log("Arrow method this", this.value);
			
		}, 1000);
	}
}

obj.regularMethod(); // "Regular method this", undefined
obj.arrowMethod(); // "Arrow method this", 42

```

Why undefined? : Callbacks or async or setTimeOut will always be called wrt global object
Arrow function always get the parent scope which is reffred at the time of creation does not wait for execution.

```
const obj2 ={
	value: "42",
	regularMethod: function(){
		let innerFun = function() {
			console.log("Regular method this", this.value);
			
		}
		innerFun();
	},
	arrowMethod: function() {
		let innerFun = () => {
			console.log("arrow method this", this.value);
			
		}
		innerFun();
	}
}

obj2.regularMethod(); // Regular method this undefined
obj2.arrowMethod(); // arrow method this 42
```

Arrow method:
============

The call(), apply(), and bind() methods are not useful when called on arrow functions, because arrow functions establish this based on the scope the arrow function is defined within, and the this value does not change based on how the function is invoked.

Arrow functions are typically preferred over standard functions, but there are a few situations when you shouldn't use the arrow function.

One of these situations is when you define an object method. Back to our person object example above, suppose you write the showSkills() method as an arrow function like this:

```
const person = {
  name: 'Nathan',
  skills: ['HTML', 'CSS', 'JavaScript'],

  showSkills: () => {
    this.skills.forEach(skill => {
      console.log(`${this.name} is skilled in ${skill}`);
    });
  },
};

person.showSkills();
```
Running the above code will cause an error:

TypeError: Cannot read properties of undefined (reading 'forEach')

```
const bf1Object = { 
 value: "BF1", 
 gfFunction: () => { 
 console.log("Result: ", this.value)
 }, 
 } 

const bf2Object = {
 value: "BF2"
}

const gfFunctionRef = bf1Object.gfFunction.bind(bf2Object);
gfFunctionRef(); // undefined
```


Class fields are defined on the instance, not on the prototype, so every instance creation would create a new function reference and allocate a new closure, potentially leading to more memory usage than a normal unbound method.

```
class C {
  a = 1;
  constructor() {
    this.method = this.method.bind(this);
  }
  method() {
    console.log(this.a);
  }
}

```

Arrow function properties are often said to be "auto-bound methods".

```
class C {
  a = 1;
  autoBoundMethod = () => {
    console.log(this.a);
  };
}

const c = new C();
c.autoBoundMethod(); // 1
const { autoBoundMethod } = c;
autoBoundMethod(); // 1
// If it were a normal method, it should be undefined in this case
```