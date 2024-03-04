
ForEach, Map, Filter, Reduce polyfill.
=================================
Reference: https://medium.com/nerd-for-tech/polyfill-for-array-map-filter-and-reduce-e3e637e0d73b
https://blog.reeversedev.com/polyfills-for-map-filter-and-reduce-in-javascript
----------

ForEach:
----------
```
Array.prototype.myForEach = function(callback) {
  // callback here is the callback function
  // which actual .forEach() function accepts
  for (var i = 0; i < this.length; i++) {
    callback(this[i], i, this) // currentValue, index, array
  }
}

```

--------------------------

Map:
----------

Array.map function takes a callback function as an argument and that callback function can have three arguments passed into it :
a. current value
b. index of the current value [optional]
c. array [optional]

```
Array.prototype.myMap = function(callback){
	let arr =[];
	for(let i=0; i<this.length; i++){
		arr.push(callback(this[i], i, this));
	}
	return arr;
};
```

----------------------------------------


Flter:
------------
Array.filter function takes a callback function as an argument and that callback function can have three arguments passed into it :
a. current value
b. index of the current value [optional]
c. array [optional]

```
Array.prototype.myFilter = function(callback){
	let arr =[];
	for(let i=0; i<this.length; i++){
		if(callback.call(this[i], i, this)){
			arr.push(this[i]);
		}
	}
	return arr;
};
```

----------------------------------------

Reduce:
------------
Array.reduce function takes two arguement :
1. A callback function as an argument and that callback function can have four arguments passed into it :
	a. accumulator
	b. current value
	c. index of the current value [optional]
	d. array [optional]

2. An initial value.

```
Array.prototype.myReduce = function (callback, initialValue) {
	var accumulator = initialValue;
	for (var i = 0; i < this.length; i++) {
		if (accumulator !== undefined) {
			accumulator = callbackFn.call(undefined, accumulator, this[i],   i, this);
		} else {
			accumulator = this[i];
		}
	}
	return accumulator;
}
```