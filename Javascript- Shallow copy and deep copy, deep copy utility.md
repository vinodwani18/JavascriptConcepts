What is Deep copy and shallow copy in javacript?
=================================================
Reference: https://medium.com/version-1/cloning-an-object-in-javascript-shallow-copy-vs-deep-copy-fa8acd6681e9

https://medium.com/@manjuladube/understanding-deep-and-shallow-copy-in-javascript-13438bad941c

Deep Copy:
-------------
A deep copy means that all of the values of the new variable are copied and disconnected from the original variable. 
Deep copy means that all levels of the object are copied. This is a true copy of the object.

Shallow Copy:
--------------
A shallow copy means that certain (sub-)values are still connected to the original variable.
Shallow copy means that only the first level of the object is copied. Deeper levels are referenced.
That means deeper level object points to same memory location(address).


Example:
-----------

```
var employeeDetailsOriginal = {  name: 'Vinod', age: 33, Profession: 'Software Engineer' };

var employeeDetailsDuplicate = employeeDetailsOriginal; //Shallow copy!

// If we change a value:   
employeeDetailsDuplicate.name = 'NameChanged';

// This statement will also change name from employeeDetailsOriginal, since we have a shallow copy, or a reference to var employeeDetailsOriginal.
// This means, you’re losing the original data as well.


var employeeDetailsDuplicate = { name: employeeDetailsOriginal.name, age: employeeDetailsOriginal.age, Profession: employeeDetailsOriginal.Profession}; //Deep copy!
```

Shallow copy
-------------
A shallow copy can be achieved using the spread operator (…) or using Object.assign():

```
var employeeDetailsOriginal = {age: 25, Profession: 'Software Engineer', name: {fname:"vinod", lname: "wani"}, sayHi: function() {console.log("Hi" + this.name.fname + this.name.lname)}};

const employeeDetailsDuplicate = { ...employeeDetailsOriginal };
const employeeDetailsDuplicate2 = Object.assign({}, employeeDetailsOriginal);

employeeDetailsDuplicate.name.fname = 'nameChanged';
employeeDetailsDuplicate.age= 25;

employeeDetailsDuplicate2.name.fname = 'nameChanged2';
employeeDetailsDuplicate2.age= 27;

console.log(employeeDetailsOriginal); // {
    "age": 25,
    "Profession": "Software Engineer",
    "name": {
        "fname": "nameChanged2",
        "lname": "wani"
    },
	"sayHi": f ()
}
console.log(employeeDetailsDuplicate); // {
    "age": 25,
    "Profession": "Software Engineer",
    "name": {
        "fname": "nameChanged2",
        "lname": "wani"
    },
	"sayHi": f ()
}
console.log(employeeDetailsDuplicate2); // {
    "age": 27,
    "Profession": "Software Engineer",
    "name": {
        "fname": "nameChanged2",
        "lname": "wani"
    },
	"sayHi": f ()
}
```

Conclusion:
-------------
After updating a property in the first level of the cloned objects, the original property is not updated.

After updating a property in a deeper level, the original property is also updated. This happens because, in this case, deeper levels are referenced, not copied.


Deep copy:
--------------
A deep copy can be achieved using JSON.parse() + JSON.stringify():

```
var employeeDetailsOriginal = {age: 25, Profession: 'Software Engineer', name: {fname:"vinod", lname: "wani"}, sayHi: function() {console.log("Hi" + this.name.fname + this.name.lname)}};

const employeeDetailsDeepCopy = JSON.parse(JSON.stringify(employeeDetailsOriginal));

employeeDetailsDeepCopy.name.fname = 'new Name';
employeeDetailsDeepCopy.age = 23;

console.log(employeeDetailsOriginal); // {
    "age": 25,
    "Profession": "Software Engineer",
    "name": {
        "fname": "vinod",
        "lname": "wani"
    }
}
console.log(employeeDetailsDeepCopy); // {
    "age": 23,
    "Profession": "Software Engineer",
    "name": {
        "fname": "new Name",
        "lname": "wani"
    }
}
```

We can also create our own utility to create deep copy of the object as shown below:
------------------------------------------------------------------------------------

```
function keepCloning(objectpassed) {
  if (objectpassed === null || typeof objectpassed !== 'object') {
     return objectpassed;
  }
    // give temporary-storage the original obj's constructor
	var temporary_storage = objectpassed.constructor(); 
	  for (var key in objectpassed) {
		temporary_storage[key] = keepCloning(objectpassed[key]);
	  }
	  return temporary_storage;
}
var employeeDetailsOriginal = {age: 25, Profession: 'Software Engineer', name: {fname:"vinod", lname: "wani"}, sayHi: function() {console.log("Hi" + this.name.fname + this.name.lname)}};
var employeeDetailsDuplicate = (keepCloning(employeeDetailsOriginal));
employeeDetailsDuplicate.name.lname = "NameChanged";
employeeDetailsDuplicate.sayHi();    // HivinodNameChanged
console.log(employeeDetailsOriginal); // {
    "age": 25,
    "Profession": "Software Engineer",
    "name": {
        "fname": "vinod",
        "lname": "wani"
    }
}
console.log(employeeDetailsDuplicate); // {
    "age": 25,
    "Profession": "Software Engineer",
    "name": {
        "fname": "vinod",
        "lname": "NameChanged"
    }
}
employeeDetailsOriginal.sayHi();   //  Hivinodwani
```