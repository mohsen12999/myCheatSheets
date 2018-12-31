# Java Script

## Variable

* var   -> can accessable everywhere in function
* let   -> can access to variable in the block
* const -> read-only variable and access in block

## Object

```js
const person = {
    name: "Mosh", // property
    walk: function() { console.log(this) }, // method, old way define
    talk() {} // new way
}

person.talk(); // access with dot
person['name'] = 'John'; // access with bracket

const targetMember = 'name';
person[targetMember.value] = 'Joe';
```

## this

* this: show who call function
* if we call function as stand alone object and outside a object, by default this return window object
* callback function like setTimeout return window object
* we can bind this to function -> person.work.bind(person)

```js
const walk = person.walk.bind(person);
walk();
```

## Arrow Function

```js
const squre = number => number * number;
```

*this not reset or or rebind in arrow method (in callback)

## Array.filter

do for all input member and return it if function return true

## Array.map

return new output for every member

```js
const colors = ['red', 'green', 'blue'];
const items = color.map(color =>'<li>'+color+'</li>');
const items = color.map(color =>`<li>${color}</li>`);
```

## Object Destructuring

```js
const address = {
    street: '',
    city: '',
    country: ''
}

const street = address.street;
const city = address.city;
const country = address.country;

//all tree
const { street, city, country } = address;

//only two
const { city, country } = address;

//alias
const { street: st } = address;
```

## Spread Operator

```js
const first = [1, 2, 3];
const second = [4, 5, 6];

const combined = first.concat(second);
const combined = [...first, ...second];

const clone = [...first];
```

```js
const first = { name: 'Mosh'};
const second = { job: 'Instructor' };

const combine = { ...first, ...second, location: 'Australia'};
const clone = [...first];
```

## Classes

```js
class Person {
    constroctor(name) {
        this.name = name;
    }
    walk() {
        console.log(this);
    }
}

const person = new Person('Mosh');
```

* move code with `alt` + `arrow-key`

## Inheritance

```js
class Teacher extends Person {
    constroctor(name, degree) {
        super(name);
        this.degree = degree;
    }
    teach() {
        console.log("teach");
    }
}

const teacher = new Teacher('Mosh', 'MSc');
```

## Modules

* splite code in multiple file -> Modularity and each file -> Module
* need to export classes or properties in files
in person.js

```js
export class Person {
    ...
}
```

in teacher.js

```js
import { Person } from './person';

export class Teacher extends Person {
    ...
}
```

## Named and Default Export

* one or multiple function or class can export from file -> Named Export
* if only one object export -> Default Export

```js
export default class Teacher {}
```

```
import Teacher from 'teacher'
```

* we can both default and name in a file like React

```js
import React, { Component } from 'react';
```
