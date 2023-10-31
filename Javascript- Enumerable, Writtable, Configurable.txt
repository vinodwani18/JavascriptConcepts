What is Enumerable in Javascript?
====================================
Reference: https://blog.reeversedev.com/enumeration-in-javascript
----------
An enumerable property in JavaScript means that a property can be viewed if it is iterated using the for…in loop or Object.keys() method.
for ex. var emp = { name: "vinod", lastname: 'wani" };
 Object.keys(emp) // ['name', 'lastname']
 
Every property set on object is non-enumerable when set as below:
var emp = { name: "vinod", lastname: 'wani" };

By defaule proerties on object is enumerable(enumerable: false) when set using defineProperty. 

Object.defineProperty(emp, 'age', {
        value: 22,
        enumerable: false,
    });
	
To make is non-enumerable we need to set it to true as below.

Object.defineProperty(emp, 'age', {
        value: 22,
        enumerable: true,
    });
	
	
propertyIsEnumerable() method is used to check if the property is enumerable.

emp.propertyIsEnumerable(name);  // true
emp.propertyIsEnumerable(age);  // false


What is Writable in Javascript?
====================================
If writable prerty set to true then the value associated with the property may be changed with an assignment operator. 
Defaults to false

const emp = {};
emp.defineProperty(emp, 'property1', {
  value: 42,
  writable: false,
})

What is configurable in javascript?
===================================
Reference: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty
---------
If a configurable is set to true on property then that property can be deleted from the object.

Object.defineProperty( emp, 'a', {
   value: "some value",
   configurable: true,
});
// Object {a: "some value"}
delete emp.a;
// true
emp
// Object {}

If a configurable is set to false on property then that property can not be deleted from the object.

Object.defineProperty( emp, 'a', {
   value: "some value",
   configurable: false,
});
// Object {a: "some value"}
delete emp.a;
// false
emp
// Object {a: "some value"}

