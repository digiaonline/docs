# Nord Software JavaScript Style Guide

## Table of Contents

1. [General](#general)
1. [Strings](#strings)
1. [Functions](#functions)
1. [Arrays](#arrays)
1. [Type Coercion](#type-coercion)
1. [Comments](#comments)

## General

- **Set tabs to 2 spaces**

```javascript
// Bad

if (isAdmin) {
    handleAdmin();
}

// Good

if (isAdmin) {
  handleAdmin();
}
```

- **Use semicolons**

```javascript
// Bad

const username = 'tiff'
return username

// Good

const username = 'tiff';
return username;
```

- **Use triple equals**

```javascript
// Bad

if (name == 'Tiffany') {}
if (age == 21) {}
if (name != 'Caleb') {}

// Good

if (name === 'Tiffany') {}
if (age === 21) {}
if (name !== 'Caleb') {}
```

- **Space before leading brace**

```javascript
// Bad

function foo(){
}

// Good

function foo() {
}
```

- **Space after `switch` keyword**

```javascript
// Bad

switch(action.type) {}

// Good

switch (action.type) {}
```

- **Blank line between switch cases**

```javascript
// Bad

case ADMIN:
  return 'You are an admin.';
case MODERATOR:
  return 'You are a moderator.';

// Good

case ADMIN:
  return 'You are an admin.';

case MODERATOR:
  return 'You are a moderator.';
```

- **Space after `if` keyword**

```javascript
// Bad

if(isAuthenticated) {}

// Good

if (isAuthenticated) {}
```

- **Simply return instead of using `else if` and `else` conditions**

```javascript
// Bad

if (isAdmin) {
  return 'You are an admin.';
} else if (isModerator) {
  return 'You are a moderator.'
} else {
  return 'You are a user.';
}

// Good

if (isAdmin) {
  return 'You are an admin.';
}

if (isModerator) {
  return 'You are a moderator.'
}

return 'You are a user.';
```

- **Always use braces with `if` blocks**

```javascript
// Bad

if (isAdmin)
  return handleAdmin();

// Good

if (isAdmin) {
  return handleAdmin();
}
```

- **Place `else if` and `else` on the same line as the previous closing brace**

```javascript
// Bad

if (isAdmin) {
  func1();
}
else if (isModerator) {
  func2();
}
else {
  func3();
}

// Good

if (isAdmin) {
  func1();
} else if (isModerator) {
  func2();
} else {
  func3();
}
```

- **Use `const` instead of `var` and `let`**

```javascript
// Bad

var accessToken = getAccessToken();
let user = getUser(accessToken);

// Good

const accessToken = getAccessToken();
const user = getUser(accessToken);
```

- **No padding inside functions**

```javascript
// Bad

function foo() {

  return true;

}

// Good

function foo() {
  return true;
}
```

- **No padding inside objects**

```javascript
// Bad

const foo = {

  bar: 'bar',
  baz: 'baz',
  quux() {
    return 'quux';
  }

};

// Good

const foo = {
  bar: 'bar',
  baz: 'baz',
  quux() {
    return 'quux';
  }
};
```

## Strings

- **Use single quotes**

```javascript
// Bad

const foo = "bar";

// Good

const foo = 'bar';
```

- **Use template strings for interpolation**

```javascript
// Bad

const name = 'Tiffany';
return 'Hi, I\'m ' + name + '.';

// Good

const name = 'Tiffany';
return `Hi, I'm ${name}.`;
```

## Functions

- **Use function declarations**

```javascript
// Bad

const func = function() {};

// Good

function func() {}
```

- **Use default parameters**

```javascript
// Bad

function log(message, level) {
  level = level || 'info';
}

// Good

function log(message, level = 'info') {
}
```

- **Use arrow functions for callbacks**

```javascript
// Bad

fetch('http://api.example.com/posts').then(function(response) {
  return response.json();
});

// Good

fetch('http://api.example.com/posts').then(response => response.json());
```

- **Use the object method shorthand**

```javascript
// Bad

const foo = {
  bar: function() {
    console.log('You called foo.bar.');
  }
};

// Good

const foo = {
  bar() {
    console.log('You called foo.bar.');
  }
};
```

## Arrays

- **Use trailing commas**

```javascript
// Bad

const names = [
  'Tiffany'
  , 'Caleb'
  , 'Mark'
];

// Good

const names = [
  'Tiffany',
  'Caleb',
  'Mark'
];
```

- **Use Array.prototype.map instead of Array.prototype.forEach**

```javascript
const oldArray = [
  {name: 'Foo'},
  {name: 'Bar'},
  {name: 'Baz'}
];

// Bad

const newArray = [];

oldArray.forEach(item => {
  item.isVisible = true;

  newArray.push(item);
});

// Good

const newArray = oldArray.map(item => Object.assign({}, {
  isVisible: true
}, item));
```

- **Use Array.prototype.filter instead of Array.prototype.forEach**

```javascript
const oldArray = [
  {name: 'Foo'},
  {name: 'Bar', isVisible: true},
  {name: 'Baz'}
];

// Bad

const newArray = [];

oldArray.forEach(item => {
  if (item.isVisible) {
    newArray.push(item);
  }
});

// Good

const newArray = oldArray.filter(item => item.isVisible);
```

- **Use Array.prototype.reduce instead of Array.prototype.forEach**

```javascript
const array = [
  {id: 1, name: 'Foo'},
  {id: 2, name: 'Bar'},
  {id: 3, name: 'Baz'}
];

// Bad

const map = {};

array.forEach(item => {
  map[item.id] = item;
});

// Good

const map = array.reduce((accumulator, item) => Object.assign({}, {
  [item.id]: item
}, accumulator), {});
```

## Type Coercion

- **Use `parseInt` with a radix for numbers**

```javascript
const input = '21';

// Bad

const age = new Number(input);


// Good

const age = parseInt(input, 10);
```

- **Use `parseFloat` for floating point numbers**

```javascript
const input = '99.5';

// Bad

const percentage = new Number(input);


// Good

const percentage = parseFloat(input);
```

- **Use `!!` for booleans**

```javascript
const age = 0;

// Bad

const hasAge = new Boolean(age);

// Good

const hasAge = !!age;
```

- **Use `String` for strings**

```javascript
const age = 21;

// Bad

const text = age + '';

// Good

const text = String(age);
```

## Comments

- **Doc blocks**

```javascript
/**
 * Logs an application message.
 *
 * @param {string} message
 * @param {string} [level]
 *
 * @return {string}
 */
function log(message, level = 'info') {
}
```

## Modules

- **Separate third-party imports**

```javascript
// Bad

import React, {Component, PropTypes} from 'react';
import Navbar from './navbar';
import classnames from 'classnames';
import Button from '../common/button';

// Good

import React, {Component, PropTypes} from 'react';
import classnames from 'classnames';

import Navbar from './navbar';
import Button from '../common/button';
```

- **Reference named imports**

```javascript
// Bad

import React from 'react';

class Navbar extends React.Component {
    static propTypes = {
        items: React.PropTypes.array.isRequired
    };
}

// Good

import React, {Component, PropTypes} from 'react';

class Navbar extends Component {
    static propTypes = {
        items: PropTypes.array.isRequired
    };
}
```
