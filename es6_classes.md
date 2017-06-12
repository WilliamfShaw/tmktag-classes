# ES6 Classes

### Learning Objectives
- Compare and Contrast ES5 constructor funtions to ES6 class declarations
- Identify the important key words in ES6 classes
- Convert legacy constructor functions to modern ES6 classes
- Implement inheritance using ES6 classes


# Out with the old, in with the new

### ES5 Constructor function

```js
function Employee(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.clockedIn = false;
}

Employee.prototype.fullName = function () {
    return `${this.firstName} ${this.lastName}`
}

Employee.prototype.clockIn = function () {
    this.clockedIn = true;
}

Employee.prototype.clockOut = function () {
    this.clockedIn = false;
}


var will = new Employee('William', 'Shaw');
will.fullName(); // 'William Shaw'
will.clockedIn // false
will.clockIn();
will.clockedIn // true
will.clockOut();
will.clockedIn // false
```

### ES6 Class

```js
class Employee {
    constructor(firstName, lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.clockedIn = false;
    }

    fullName () {
        return `${this.firstName} ${this.lastName}`
    }

    clockIn () {
        this.clockedIn = true;
    }

    clockOut () {
        this.clockedIn = false;
    }
}
```

---
# Turn and Talk - (4 mins)

- What are some of the differences between the old syntax and the new?
- Does this mean Javascript is now an OO language in the traditional sense?

# Constructor and Static Keywords

<details>
<summary>Constructor</summary>

- The `constructor` keyword is a special method reserved for creating and initializing an object with ES6 classes. This method may only be used once inside of a class, if it is used twice it will throw a reference error. The context of `this` in reference to the `contructor` is the specific instance of the resulting object.

```js
//BAD
class FooBar {
    constructor () {
        this.foo = 'FOO';
    }

    constructor () {
        this.bar = 'BAR';
    }
}

const fooBar = new FooBar(); // Uncaught SyntaxError: A class may only have one constructor
```
</details>

<details>
<summary>Static</summary>

- The `static` keyword is used to call `class` methods. These methods can be called without the need to instantiate the object and can not be called from an instance of a new object.

```js
class Foo {
    static bar () {
        return 'This is Foo.bar()';
    }
}
```

- The `this` in a static method refers to the class contructor `Foo` itself. Some good use cases for this might be comparison functions, or a factory function.

```js
class TodaysNews {
    constructor (headline, date) {
        this.headline = headline
        this.date = date
    }

    static createTodaysNews () {
        return new this('Todays news headline', new Date());
    }

    static compareArticleDates(articleA, articleB) {
        return articleA.date - articleB.date;
    }
}

TodaysNews.createTodaysNews(); // TodaysNews {headline: "Todays news headline", date: Mon Jun 12 2017 15:02:54 GMT-0400 (EDT)}

var oldArticle = TodaysNews.createTodaysNews();
var newArticle = TodaysNews.createTodaysNews();

TodaysNews.compareArticleDates(oldArticle, newArticle); // -35869
```
</details>


# Inheritance

### ES5 Inheritance

```js
function Foo () {
    this.bar = 'BAR';
}

function Bar () {};
Bar.prototype = new Foo();

var bar = new Bar();
bar.bar = 'BAR'
```

### ES6 Inheritance
```js
class Foo {
    constructor () {
        this.bar = 'BAR';
    }
}

class Bar extends Foo {
    constructor() {
        super();
    }
}

let bar = new Bar();
bar.bar = 'BAR';
```

# Extends and Super Keywords

<details>
<summary>Extends</summary>

- The `extends` keyword is used to create a class which is the child of another.
- The parent class must be an `Object` or `null`

</details>

<details>
<summary>Super</summary>

- The `super` keyword is used to call methods from the parent class.

```js
//BAD
class Foo {
    constructor () {
        this.bar = 'BAR';
    }

	sayBar() {
		return `I'm saying ${this.bar}`;
    }
}

class Bar extends Foo {
    constructor() {
		super();
		this.foo = 'FOO';
    }
}

let bar = new Bar();
bar.sayBar(); // 'I'm saying BAR'
```
</details>

# Turn and Talk - (2 mins)

- What would happen if we removed the `super` keyword from the child class?

# Exercise

### Convert the following to ES6 classes P1

```js
function Car(color, make, horsepower) {
    this.color = color;
    this.make = make;
    this.horsepower = horsepower;
    this.fuel = 5;
};

Car.prototype.drive = function() {
    if (this.fuel > 0) {
        this.fuel--;
        return 'Vroom!';
    } else {
        return 'out of gas';
    }
};

Car.prototype.refuel = function() {
    this.fuel = 5;
};

Car.prototype.paint = function(color) {
    this.color = color;
}

Car.prototype.tuneup = function() {
    this.horsepower += 10;
}
```


```js
function Bicycle (make, color){
    this.make = make;
    this.color = color;
}

Bicycle.prototype.paint = function (color) {
    this.color = color;
}

Bicycle.prototype.ride = function () {
    return 'Weeeeee this is fun';
}
```


# Exercise P2

- Using the new ES6 inheritance features, clean up the two constructors we just converted


