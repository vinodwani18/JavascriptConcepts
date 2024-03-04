What is call, aaply and bind in Javascript?
====================================
Reference: https://dev.to/kirteshbansal/call-apply-and-bind-javascript-methods-their-polyfills-k4e
https://medium.com/nerd-for-tech/polyfill-part-3-for-call-apply-and-bind-169a05d33d02
----------

1. call(object, arguments) - invokes the function on passed object along with passed arguments if there
2. apply(object, [arguments]) - invokes the function on passed object along with passed array of arguments if there
3. bind(object, arguments) - returns a new function with referencing passed object and arguments

Example: 

```
let person = {
  firstname: "Vinod",
  lastname: "Wani"
}

let printName = function (country) {
  console.log(this.firstname + " " + this.lastname + " from " 
  + country);
}
```

Call:
--------------------
```
printName.call(person, "India");
```
Output: 
"Vinod Wani from India"
---------------------------------

Apply:
-----------------------
```
printName.apply(person, ["India"]);
```
Output: 
"Vinod Wani from India"
---------------------------------------

Bind:
-----------------------
```
let newPrintName = printName.bind(person, "India");
newPrintName();
```
Output: 
"Vinod Wani from India"
---------------------------------------



Prototype for Call:
-----------------------
```
Function.prototype.myCall = function(obj, ...args) {
    if( typeof this !=="function"){ 
		throw error console.log("not a func");
	}
    obj.context = this;
    let result = obj.context(...args);
    delete obj.context;
    return result;
};
```


Prototype for Apply:
----------------------------------
```
Function.prototype.myApply = function(obj, args) {
    if( typeof this !=="function"){ 
		throw error console.log("not a func");
	}
    obj.context = this;
    let result = obj.context(...args);
    delete obj.context;
    return result;
};
```


Prototype of Bind:
---------------------------------
```
Function.prototype.myBind = function (obj, ...args) {
    if( typeof this !=="function"){ 
		throw error console.log("not a func");
	}
    obj.callback = this;
    return function(){
        let result = obj.callback(...args);
        return result;
    }
    
}
```