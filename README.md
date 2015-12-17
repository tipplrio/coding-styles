# Tipplr JavaScript Style Guide() {

*A mostly reasonable approach to JavaScript, forked from [Airbnb's JavaScript Style Guide](http://airbnb.io/projects/javascript/)*

Other Style Guides

- [React](react/)
- [CSS & Sass](https://github.com/airbnb/css)


## Table of Contents

1. [Types](#1-types)
2. [References](#2-references)
3. [Objects](#3-objects)
4. [Arrays](#4-arrays)
5. [Destructuring](#5-destructuring)
6. [Strings](#6-strings)
7. [Functions](#7-functions)
8. [Arrow Functions](#8-arrow-functions)
9. [Constructors](#9-constructors)
10. [Modules](#10-modules)
11. [Iterators and Generators](#11-iterators-and-generators)
12. [Properties](#12-properties)
13. [Variables](#13-variables)
14. [Hoisting](#14-hoisting)
15. [Comparison Operators & Equality](#15-comparison-operators--equality)
16. [Blocks](#16-blocks)
17. [Comments](#17-comments)
18. [Whitespace](#18-whitespace)
19. [Commas](#19-commas)
20. [Semicolons](#20-semicolons)
21. [Type Casting & Coercion](#21-type-casting--coercion)
22. [Naming Conventions](#22-naming-conventions)
23. [Accessors](#23-accessors)
24. [Events](#24-events)
25. [jQuery](#25-jquery)
26. [ECMAScript 5 Compatibility](#26-ecmascript-5-compatibility)
27. [ECMAScript 6 Styles](#27-ecmascript-6-styles)
28. [Testing](#28-testing)
29. [Directory Structure](#29-directory-structure)
30. [Performance](#30-performance)
31. [Resources](#31-resources)
32. [Contributors](#32-contributors)
33. [License](#33-license)


## 1. Types

- [1.1](#1.1) <a name='1.1'></a> **Primitives**: When you access a primitive type you work directly on its value.

  + `string`
  + `number`
  + `boolean`
  + `null`
  + `undefined`

  ```javascript
  const foo = 1;
  let bar = foo;

  bar = 9;

  // => 1, 9
  console.log(foo, bar);
  ```

- [1.2](#1.2) <a name='1.2'></a> **Complex**: When you access a complex type you work on a reference to its value.

  + `object`
  + `array`
  + `function`

  ```javascript
  const foo = [1, 2];
  const bar = foo;

  bar[0] = 9;

  // => 9, 9
  console.log(foo[0], bar[0]);
  ```

**[⬆ back to top](#table-of-contents)**


## 2. References

- [2.1](#2.1) ([**ES6**](#27-ecmascript-6-styles)) <a name='2.1'></a> Use `const` for all of your references; avoid using `var`.

  > Why? This ensures that you can't reassign your references, which can lead to bugs and difficult to comprehend code.

  ```javascript
  // bad
  var a = 1;
  var b = 2;

  // good
  const a = 1;
  const b = 2;
  ```

- [2.2](#2.2) ([**ES6**](#27-ecmascript-6-styles)) <a name='2.2'></a> If you must reassign references, use `let` instead of `var`.

  > Why? `let` is block-scoped rather than function-scoped like `var`.

  ```javascript
  // bad
  var count = 1;
  if (true) {
    count += 1;
  }

  // good, use the let.
  let count = 1;
  if (true) {
    count += 1;
  }
  ```

- [2.3](#2.3) ([**ES6**](#27-ecmascript-6-styles)) <a name='2.3'></a> Note that both `let` and `const` are block-scoped.

  ```javascript
  // const and let only exist in the blocks they are defined in.
  {
    let a = 1;
    const b = 1;
  }

  // ReferenceError
  console.log(a);
  // ReferenceError
  console.log(b);
  ```

**[⬆ back to top](#table-of-contents)**


## 3. Objects

- [3.1](#3.1) <a name='3.1'></a> Use the literal syntax for object creation.

  ```javascript
  // bad
  const item = new Object();

  // good
  const item = {};
  ```

- [3.2](#3.2) ([**ES5**](#26-ecmascript-5-compatibility)) <a name='3.2'></a> If your code will be executed in browsers in script context, don't use [reserved words](http://es5.github.io/#x7.6.1) as keys. It won't work in IE 8. [More info](https://github.com/airbnb/javascript/issues/61). It’s OK to use them in ECMAScript 6 modules and server-side code.

  ```javascript
  // bad
  const superman = {
    default: { clark: 'kent' },
    private: true,
  };

  // good
  const superman = {
    defaults: { clark: 'kent' },
    hidden: true,
  };
  ```

- [3.3](#3.3) <a name='3.3'></a> Use readable synonyms in place of reserved words.

  ```javascript
  // bad
  const superman = {
    class: 'alien',
  };

  // bad
  const superman = {
    klass: 'alien',
  };

  // good
  const superman = {
    type: 'alien',
  };
  ```

- [3.4](#3.4) ([**ES6**](#27-ecmascript-6-styles)) <a name='3.4'></a> Use computed property names when creating objects with dynamic property names.

  > Why? They allow you to define all the properties of an object in one place.

  ```javascript

  function getKey(k) {
    return `a key named ${k}`;
  }

  // bad
  const obj = {
    id: 5,
    name: 'San Francisco',
  };
  obj[getKey('enabled')] = true;

  // good
  const obj = {
    id: 5,
    name: 'San Francisco',
    [getKey('enabled')]: true,
  };
  ```

- [3.5](#3.5) ([**ES6**](#27-ecmascript-6-styles)) <a name='3.5'></a> Use object method shorthand.

  ```javascript
  // bad
  const atom = {
    value: 1,

    addValue: function (value) {
      return atom.value + value;
    },
  };

  // good
  const atom = {
    value: 1,

    addValue(value) {
      return atom.value + value;
    },
  };
  ```

- [3.6](#3.6) ([**ES6**](#27-ecmascript-6-styles)) <a name='3.6'></a> Use property value shorthand.

  > Why? It is shorter to write and descriptive.

  ```javascript
  const lukeSkywalker = 'Luke Skywalker';

  // bad
  const obj = {
    lukeSkywalker: lukeSkywalker,
  };

  // good
  const obj = {
    lukeSkywalker,
  };
  ```

- [3.7](#3.7) <a name='3.7'></a> Group your shorthand properties at the beginning of your object declaration.

  > Why? It's easier to tell which properties are using the shorthand.

  ```javascript
  const anakinSkywalker = 'Anakin Skywalker';
  const lukeSkywalker = 'Luke Skywalker';

  // bad
  const obj = {
    episodeOne: 1,
    twoJediWalkIntoACantina: 2,
    lukeSkywalker,
    episodeThree: 3,
    mayTheFourth: 4,
    anakinSkywalker,
  };

  // good
  const obj = {
    lukeSkywalker,
    anakinSkywalker,
    episodeOne: 1,
    twoJediWalkIntoACantina: 2,
    episodeThree: 3,
    mayTheFourth: 4,
  };
  ```

**[⬆ back to top](#table-of-contents)**


## 4. Arrays

- [4.1](#4.1) <a name='4.1'></a> Use the literal syntax for array creation.

  ```javascript
  // bad
  const items = new Array();

  // good
  const items = [];
  ```

- [4.2](#4.2) <a name='4.2'></a> Use Array#push instead of direct assignment to add items to an array.

  ```javascript
  const someStack = [];

  // bad
  someStack[someStack.length] = 'abracadabra';

  // good
  someStack.push('abracadabra');
  ```

- [4.3](#4.3) ([**ES6**](#27-ecmascript-6-styles)) <a name='4.3'></a> Use array spreads `...` to copy arrays.

  ```javascript
  // bad
  const len = items.length;
  const itemsCopy = [];
  let i;

  for (i = 0; i < len; i++) {
    itemsCopy[i] = items[i];
  }

  // good
  const itemsCopy = [...items];
  ```

  ([**ES5**](#26-ecmascript-5-compatibility)) When you need to copy an array use Array#slice. [jsPerf](http://jsperf.com/converting-arguments-to-an-array/7)

  ```javascript
  var len = items.length;
  var itemsCopy = [];
  var i;

  // bad
  for (i = 0; i < len; i++) {
    itemsCopy[i] = items[i];
  }

  // good
  itemsCopy = items.slice();
  ```

- [4.4](#4.4) ([**ES6**](#27-ecmascript-6-styles)) <a name='4.4'></a> To convert an array-like object to an array, use Array#from.

  ```javascript
  const foo = document.querySelectorAll('.foo');
  const nodes = Array.from(foo);
  ```

  ([**ES5**](#26-ecmascript-5-compatibility)) To convert an array-like object to an array, use Array#slice.

  ```javascript
  var foo = document.querySelectorAll('.foo');
  var nodes = Array.prototype.slice.call(foo);
  ```

**[⬆ back to top](#table-of-contents)**


## 5. Destructuring

- [5.1](#5.1) ([**ES6**](#27-ecmascript-6-styles)) <a name='5.1'></a> Use object destructuring when accessing and using multiple properties of an object.

  > Why? Destructuring saves you from creating temporary references for those properties.

  ```javascript
  // bad
  function getFullName(user) {
    const firstName = user.firstName;
    const lastName = user.lastName;

    return `${firstName} ${lastName}`;
  }

  // good
  function getFullName(obj) {
    const { firstName, lastName } = obj;
    return `${firstName} ${lastName}`;
  }

  // best
  function getFullName({ firstName, lastName }) {
    return `${firstName} ${lastName}`;
  }
  ```

- [5.2](#5.2) ([**ES6**](#27-ecmascript-6-styles)) <a name='5.2'></a> Use array destructuring.

  ```javascript
  const arr = [1, 2, 3, 4];

  // bad
  const first = arr[0];
  const second = arr[1];

  // good
  const [first, second] = arr;
  ```

- [5.3](#5.3) ([**ES6**](#27-ecmascript-6-styles)) <a name='5.3'></a> Use object destructuring for multiple return values, not array destructuring.

  > Why? You can add new properties over time or change the order of things without breaking call sites.

  ```javascript
  // bad
  function processInput(input) {
    // then a miracle occurs
    return [left, right, top, bottom];
  }

  // the caller needs to think about the order of return data
  const [left, __, top] = processInput(input);

  // good
  function processInput(input) {
    // then a miracle occurs
    return { left, right, top, bottom };
  }

  // the caller selects only the data they need
  const { left, right } = processInput(input);
  ```

**[⬆ back to top](#table-of-contents)**


## 6. Strings

- [6.1](#6.1) <a name='6.1'></a> Use single quotes `''` for strings.

  ```javascript
  // bad
  const name = "Capt. Janeway";

  // good
  const name = 'Capt. Janeway';
  ```

- [6.2](#6.2) <a name='6.2'></a> Strings longer than 100 characters should be written across multiple lines using string concatenation.

- [6.3](#6.3) <a name='6.3'></a> Note: If overused, long strings with concatenation could impact performance. [jsPerf](http://jsperf.com/ya-string-concat) & [Discussion](https://github.com/airbnb/javascript/issues/40).

  ```javascript
  // bad
  const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

  // bad
  const errorMessage = 'This is a super long error that was thrown because \
  of Batman. When you stop to think about how Batman had anything to do \
  with this, you would get nowhere \
  fast.';

  // good
  const errorMessage = 'This is a super long error that was thrown because ' +
    'of Batman. When you stop to think about how Batman had anything to do ' +
    'with this, you would get nowhere fast.';
  ```

- [6.4](#6.4) ([**ES6**](#27-ecmascript-6-styles)) <a name='6.4'></a> When programmatically building up strings, use template strings instead of concatenation.

  > Why? Template strings give you a readable, concise syntax with proper newlines and string interpolation features.

  ```javascript
  // bad
  function sayHi(name) {
    return 'How are you, ' + name + '?';
  }

  // bad
  function sayHi(name) {
    return ['How are you, ', name, '?'].join();
  }

  // good
  function sayHi(name) {
    return `How are you, ${name}?`;
  }
  ```

  ([**ES5**](#26-ecmascript-5-compatibility)) When programmatically building up a string, use Array#join instead of string concatenation. Mostly for IE: [jsPerf](http://jsperf.com/string-vs-array-concat/2).

  ```javascript
  // bad
  function sayHi(name) {
    return 'How are you, ' + name + '?';
  }

  // good
  function sayHi(name) {
    return ['How are you, ', name, '?'].join();
  }
  ```

- [6.5](#6.5) <a name='6.5'></a> Never use `eval()` on a string, it opens too many vulnerabilities.

**[⬆ back to top](#table-of-contents)**


## 7. Functions

- [7.1](#7.1) <a name='7.1'></a> Use function declarations instead of function expressions.

  > Why? Function declarations are named, so they're easier to identify in call stacks. Also, the whole body of a function declaration is hoisted, whereas only the reference of a function expression is hoisted. This rule makes it possible to always use [Arrow Functions](#arrow-functions) in place of function expressions.

    ```javascript
    // bad
    const foo = function () {
    };

    // good
    function foo() {
    }
    ```

- [7.2](#7.2) ([**ES6**](#27-ecmascript-6-styles)) <a name='7.2'></a> Function expressions:

  ```javascript
  // immediately-invoked function expression (IIFE)
  (() => {
    console.log('Welcome to the Internet. Please follow me.');
  })();
  ```

  ([**ES5**](#26-ecmascript-5-compatibility)) Function expressions:

  ```javascript
  // immediately-invoked function expression (IIFE)
  (function() {
    console.log('Welcome to the Internet. Please follow me.');
  })();
  ```

- [7.3](#7.3) <a name='7.3'></a> Never declare a function in a non-function block (if, while, etc). Assign the function to a variable instead. Browsers will allow you to do it, but they all interpret it differently, which is bad news bears.

- [7.4](#7.4) <a name='7.4'></a> **Note:** ECMA-262 defines a `block` as a list of statements. A function declaration is not a statement. [Read ECMA-262's note on this issue](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf#page=97).

  ```javascript
  // bad
  if (currentUser) {
    function test() {
      console.log('Nope.');
    }
  }

  // good
  let test;
  if (currentUser) {
    test = () => {
      console.log('Yup.');
    };
  }
  ```

- [7.5](#7.5) <a name='7.5'></a> Never name a parameter `arguments`. This will take precedence over the `arguments` object that is given to every function scope.

  ```javascript
  // bad
  function nope(name, options, arguments) {
    // ...stuff...
  }

  // good
  function yup(name, options, args) {
    // ...stuff...
  }
  ```

- [7.6](#7.6) ([**ES6**](#27-ecmascript-6-styles)) <a name='7.6'></a> Never use `arguments`, opt to use rest syntax `...` instead.

  > Why? `...` is explicit about which arguments you want pulled. Plus rest arguments are a real Array and not Array-like like `arguments`.

  ```javascript
  // bad
  function concatenateAll() {
    const args = Array.prototype.slice.call(arguments);
    return args.join('');
  }

  // good
  function concatenateAll(...args) {
    return args.join('');
  }
  ```

- [7.7](#7.7) ([**ES6**](#27-ecmascript-6-styles)) <a name='7.7'></a> Use default parameter syntax rather than mutating function arguments.

  ```javascript
  // really bad
  function handleThings(opts) {
    // No! We shouldn't mutate function arguments.
    // Double bad: if opts is falsy it'll be set to an object which may
    // be what you want but it can introduce subtle bugs.
    opts = opts || {};
    // ...
  }

  // still bad
  function handleThings(opts) {
    if (opts === void 0) {
      opts = {};
    }
    // ...
  }

  // good
  function handleThings(opts = {}) {
    // ...
  }
  ```

- [7.8](#7.8) ([**ES6**](#27-ecmascript-6-styles)) <a name='7.8'></a> Avoid side effects with default parameters.

  > Why? They are confusing to reason about.

  ```javascript
  var b = 1;
  // bad
  function count(a = b++) {
    console.log(a);
  }
  count();  // 1
  count();  // 2
  count(3); // 3
  count();  // 3
  ```

- [7.9](#7.9) ([**ES6**](#27-ecmascript-6-styles)) <a name='7.9'></a> Always put default parameters last.

  ```javascript
  // bad
  function handleThings(opts = {}, name) {
    // ...
  }

  // good
  function handleThings(name, opts = {}) {
    // ...
  }
  ```

- [7.10](#7.10) <a name='7.10'></a> Never use the Function constructor to create a new function.

  > Why? Creating a function in this way evaluates a string similarly to eval(), which opens vulnerabilities.

  ```javascript
  // bad
  var add = new Function('a', 'b', 'return a + b');

  // still bad
  var subtract = Function('a', 'b', 'return a - b');
  ```

- [7.11](#7.11) <a name="7.11"></a> Spacing in a function signature.

  > Why? Consistency is good, and you shouldn’t have to add or remove a space when adding or removing a name.

  ```javascript
  // bad
  const f = function(){};
  const g = function (){};
  const h = function() {};

  // good
  const x = function () {};
  const y = function a() {};
  ```

**[⬆ back to top](#table-of-contents)**


## 8. Arrow Functions

- [8.1](#8.1) ([**ES6**](#27-ecmascript-6-styles)) <a name='8.1'></a> When you must use function expressions (as when passing an anonymous function), use arrow function notation.

  > Why? It creates a version of the function that executes in the context of `this`, which is usually what you want, and is a more concise syntax.

  > Why not? If you have a fairly complicated function, you might move that logic out into its own function declaration.

  ```javascript
  // bad
  [1, 2, 3].map(function (x) {
    const y = x + 1;
    return x * y;
  });

  // good
  [1, 2, 3].map((x) => {
    const y = x + 1;
    return x * y;
  });
  ```

- [8.2](#8.2) ([**ES6**](#27-ecmascript-6-styles)) <a name='8.2'></a> If the function body consists of a single expression, feel free to omit the braces and use the implicit return. Otherwise use a `return` statement.

  > Why? Syntactic sugar. It reads well when multiple functions are chained together.

  > Why not? If you plan on returning an object.

  ```javascript
  // good
  [1, 2, 3].map(number => `A string containing the ${number}.`);

  // bad
  [1, 2, 3].map(number => {
    const nextNumber = number + 1;
    `A string containing the ${nextNumber}.`;
  });

  // good
  [1, 2, 3].map(number => {
    const nextNumber = number + 1;
    return `A string containing the ${nextNumber}.`;
  });
  ```

- [8.3](#8.3) ([**ES6**](#27-ecmascript-6-styles)) <a name='8.3'></a> In case the expression spans over multiple lines, wrap it in parentheses for better readability.

  > Why? It shows clearly where the function starts and ends.

  ```javascript
  // bad
  [1, 2, 3].map(number => 'As time went by, the string containing the ' +
    `${number} became much longer. So we needed to break it over multiple ` +
    'lines.'
  );

  // good
  [1, 2, 3].map(number => (
    `As time went by, the string containing the ${number} became much ` +
    'longer. So we needed to break it over multiple lines.'
  ));
  ```

- [8.4](#8.4) ([**ES6**](#27-ecmascript-6-styles)) <a name='8.4'></a> If your function only takes a single argument, feel free to omit the parentheses.

  > Why? Less visual clutter.

  ```javascript
  // good
  [1, 2, 3].map(x => x * x);

  // good
  [1, 2, 3].reduce((y, x) => x + y);
  ```

**[⬆ back to top](#table-of-contents)**


## 9. Constructors

- [9.1](#9.1) ([**ES6**](#27-ecmascript-6-styles)) <a name='9.1'></a> Always use `class`. Avoid manipulating `prototype` directly.

  > Why? `class` syntax is more concise and easier to reason about.

  ```javascript
  // bad
  function Queue(contents = []) {
    this._queue = [...contents];
  }
  Queue.prototype.pop = function() {
    const value = this._queue[0];
    this._queue.splice(0, 1);
    return value;
  };

  // good
  class Queue {
    constructor(contents = []) {
      this._queue = [...contents];
    }
    pop() {
      const value = this._queue[0];
      this._queue.splice(0, 1);
      return value;
    }
  }
  ```

  ([**ES5**](#26-ecmascript-5-compatibility)) Assign methods to the prototype object, instead of overwriting the prototype with a new object. Overwriting the prototype makes inheritance impossible: by resetting the prototype you'll overwrite the base!

  ```javascript
  function Queue(contents = []) {
    this._queue = [...contents];
  }

  // bad
  Queue.prototype = {
    pop: function pop() {
      var value = this._queue[0];
      this._queue.splice(0, 1);
      return value;
    }
  };

  // good
  Queue.prototype.pop = function() {
    const value = this._queue[0];
    this._queue.splice(0, 1);
    return value;
  };
  ```

- [9.2](#9.2) ([**ES6**](#27-ecmascript-6-styles)) <a name='9.2'></a> Use `extends` for inheritance.

  > Why? It is a built-in way to inherit prototype functionality without breaking `instanceof`.

  ```javascript
  // bad
  const inherits = require('inherits');
  function PeekableQueue(contents) {
    Queue.apply(this, contents);
  }
  inherits(PeekableQueue, Queue);
  PeekableQueue.prototype.peek = function() {
    return this._queue[0];
  }

  // good
  class PeekableQueue extends Queue {
    peek() {
      return this._queue[0];
    }
  }
  ```

- [9.3](#9.3) <a name='9.3'></a> Methods can return `this` to help with method chaining.

  ```javascript
  // bad
  Jedi.prototype.jump = function() {
    this.jumping = true;
    return true;
  };

  Jedi.prototype.setHeight = function(height) {
    this.height = height;
  };

  const luke = new Jedi();
  // => true
  luke.jump();
  // => undefined
  luke.setHeight(20);

  // good
  class Jedi {
    jump() {
      this.jumping = true;
      return this;
    }

    setHeight(height) {
      this.height = height;
      return this;
    }
  }

  const luke = new Jedi();

  luke.jump()
    .setHeight(20);
  ```

- [9.4](#9.4) <a name='9.4'></a> It's okay to write a custom toString() method, just make sure it works successfully and causes no side effects.

  ```javascript
  class Jedi {
    constructor(options = {}) {
      this.name = options.name || 'no name';
    }

    getName() {
      return this.name;
    }

    toString() {
      return `Jedi - ${this.getName()}`;
    }
  }
  ```

**[⬆ back to top](#table-of-contents)**


## 10. Modules

- [10.1](#10.1) ([**ES6**](#27-ecmascript-6-styles)) <a name='10.1'></a> Always use modules (`import`/`export`) over a non-standard module system. You can always transpile to your preferred module system.

  > Why? Modules are the future, let's start using the future now.

  ```javascript
  // bad
  const TipplrStyleGuide = require('./TipplrStyleGuide');
  module.exports = TipplrStyleGuide.es6;

  // ok
  import TipplrStyleGuide from './TipplrStyleGuide';
  export default TipplrStyleGuide.es6;

  // best
  import { es6 } from './TipplrStyleGuide';
  export default es6;
  ```

- [10.2](#10.2) ([**ES6**](#27-ecmascript-6-styles)) <a name='10.2'></a> Do not use wildcard imports.

  > Why? This makes sure you have a single default export.

  ```javascript
  // bad
  import * as TipplrStyleGuide from './TipplrStyleGuide';

  // good
  import TipplrStyleGuide from './TipplrStyleGuide';
  ```

- [10.3](#10.3) ([**ES6**](#27-ecmascript-6-styles)) <a name='10.3'></a>And do not export directly from an import.

  > Why? Although the one-liner is concise, having one clear way to import and one clear way to export makes things consistent.

  ```javascript
  // bad
  // filename es6.js
  export { es6 as default } from './tipplrStyleGuide';

  // good
  // filename es6.js
  import { es6 } from './TipplrStyleGuide';
  export default es6;
  ```

- ~~[10.4](#10.4) ([**ES5**](#26-ecmascript-5-compatibility)) <a name='10.4'></a>The module should start with a `!`. This ensures that if a malformed module forgets to include a final semicolon there aren't errors in production when the scripts get concatenated. [Explanation](https://github.com/airbnb/javascript/issues/44#issuecomment-13063933)~~

- ~~[10.5](#10.5) ([**ES5**](#26-ecmascript-5-compatibility)) <a name='10.5'></a>The file should be named with camelCase, live in a folder with the same name, and match the name of the single export.~~

- ~~[10.6](#10.6) ([**ES5**](#26-ecmascript-5-compatibility)) <a name='10.6'></a>Add a method called `noConflict()` that sets the exported module to the previous version and returns this one.~~

- ~~[10.7](#10.7) ([**ES5**](#26-ecmascript-5-compatibility)) <a name='10.7'></a>Always declare `'use strict';` at the top of the module.~~

  ```javascript
  // fancyInput/fancyInput.js

  !function(global) {
    'use strict';

    var previousFancyInput = global.FancyInput;

    function FancyInput(options) {
      this.options = options || {};
    }

    FancyInput.noConflict = function noConflict() {
      global.FancyInput = previousFancyInput;
      return FancyInput;
    };

    global.FancyInput = FancyInput;
  }(this);
  ```

**[⬆ back to top](#table-of-contents)**


## 11. Iterators and Generators

- [11.1](#11.1) ([**ES6**](#27-ecmascript-6-styles)) <a name='11.1'></a> Don't use iterators. Prefer JavaScript's higher-order functions like `map()` and `reduce()` instead of loops like `for-of`.

  > Why? This enforces our immutable rule. Dealing with pure functions that return values is easier to reason about than side-effects.

  ```javascript
  const numbers = [1, 2, 3, 4, 5];

  // bad
  let sum = 0;
  for (let num of numbers) {
    sum += num;
  }

  sum === 15;

  // good
  let sum = 0;
  numbers.forEach((num) => sum += num);
  sum === 15;

  // best (use the functional force)
  const sum = numbers.reduce((total, num) => total + num, 0);
  sum === 15;
  ```

- [11.2](#11.2) ([**ES6**](#27-ecmascript-6-styles)) <a name='11.2'></a> Don't use generators for now.

  > Why? They don't transpile well to ES5.

**[⬆ back to top](#table-of-contents)**


## 12. Properties

- [12.1](#12.1) <a name='12.1'></a> Use dot notation when accessing properties.

  ```javascript
  const luke = {
    jedi: true,
    age: 28,
  };

  // bad
  const isJedi = luke['jedi'];

  // good
  const isJedi = luke.jedi;
  ```

- [12.2](#12.2) <a name='12.2'></a> Use subscript notation `[]` when accessing properties with a variable.

  ```javascript
  const luke = {
    jedi: true,
    age: 28,
  };

  function getProp(prop) {
    return luke[prop];
  }

  const isJedi = getProp('jedi');
  ```

**[⬆ back to top](#table-of-contents)**


## 13. Variables

- [13.1](#13.1) ([**ES6**](#27-ecmascript-6-styles)) <a name='13.1'></a> Always use `const` (or `var` in [**ES5**](#26-ecmascript-5-compatibility)) to declare variables. Not doing so will result in global variables. We want to avoid polluting the global namespace. Captain Planet warned us of that.

  ```javascript
  // bad
  superPower = new SuperPower();

  // good
  const superPower = new SuperPower();
  ```

- [13.2](#13.2) ([**ES6**](#27-ecmascript-6-styles)) <a name='13.2'></a> Use one `const` (or `var` in [**ES5**](#26-ecmascript-5-compatibility)) declaration per variable.

  > Why? It's easier to add new variable declarations this way, and you never have to worry about swapping out a `;` for a `,` or introducing punctuation-only diffs.

  ```javascript
  // bad
  const items = getItems(),
      goSportsTeam = true,
      dragonball = 'z';

  // bad
  // (compare to above, and try to spot the mistake)
  const items = getItems(),
      goSportsTeam = true;
      dragonball = 'z';

  // good
  const items = getItems();
  const goSportsTeam = true;
  const dragonball = 'z';
  ```

- [13.3](#13.3) ([**ES6**](#27-ecmascript-6-styles)) <a name='13.3'></a> Group all your `const`s and then group all your `let`s.

  > Why? This is helpful when later on you might need to assign a variable depending on one of the previous assigned variables.

  ```javascript
  // bad
  let i, len, dragonball,
      items = getItems(),
      goSportsTeam = true;

  // bad
  let i;
  const items = getItems();
  let dragonball;
  const goSportsTeam = true;
  let len;

  // good
  const goSportsTeam = true;
  const items = getItems();
  let dragonball;
  let i;
  let length;
  ```

- [13.4](#13.4) ([**ES6**](#27-ecmascript-6-styles)) <a name='13.4'></a> Assign variables where you need them, but place them in a reasonable place.

  > Why? `let` and `const` are block scoped and not function scoped.

  ```javascript
  // good
  function() {
    test();
    console.log('doing stuff..');

    //..other stuff..

    const name = getName();

    if (name === 'test') {
      return false;
    }

    return name;
  }

  // bad - unnecessary function call
  function(hasName) {
    const name = getName();

    if (!hasName) {
      return false;
    }

    this.setFirstName(name);

    return true;
  }

  // good
  function(hasName) {
    if (!hasName) {
      return false;
    }

    const name = getName();
    this.setFirstName(name);

    return true;
  }
  ```

  ([**ES5**](#26-ecmascript-5-compatibility)) Assign variables at the top of their scope. This helps avoid issues with variable declaration and assignment hoisting related issues.

  ```javascript
  // bad
  function() {
    test();
    console.log('doing stuff..');

    //..other stuff..

    var name = getName();

    if (name === 'test') {
      return false;
    }

    return name;
  }

  // good
  function() {
    var name = getName();

    test();
    console.log('doing stuff..');

    //..other stuff..

    if (name === 'test') {
      return false;
    }

    return name;
  }

  // bad - unnecessary function call
  function() {
    var name = getName();

    if (!arguments.length) {
      return false;
    }

    this.setFirstName(name);

    return true;
  }

  // good
  function() {
    var name;

    if (!arguments.length) {
      return false;
    }

    name = getName();
    this.setFirstName(name);

    return true;
  }
  ```

- [13.5](#13.5) ([**ES5**](#26-ecmascript-5-compatibility)) <a name='13.5'></a> Declare unassigned variables last. This is helpful when later on you might need to assign a variable depending on one of the previous assigned variables.

  ```javascript
  // bad
  var i, len, dragonball,
      items = getItems(),
      goSportsTeam = true;

  // bad
  var i;
  var items = getItems();
  var dragonball;
  var goSportsTeam = true;
  var len;

  // good
  var items = getItems();
  var goSportsTeam = true;
  var dragonball;
  var length;
  var i;
  ```

**[⬆ back to top](#table-of-contents)**


## 14. Hoisting

- [14.1](#14.1) <a name='14.1'></a> `var` declarations get hoisted to the top of their scope, their assignment does not. `const` and `let` declarations are blessed with a new concept called [Temporal Dead Zones (TDZ)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Temporal_dead_zone_and_errors_with_let). It's important to know why [typeof is no longer safe](http://es-discourse.com/t/why-typeof-is-no-longer-safe/15).

  ```javascript
  // we know this wouldn't work (assuming there
  // is no notDefined global variable)
  function example() {
    console.log(notDefined); // => throws a ReferenceError
  }

  // creating a variable declaration after you
  // reference the variable will work due to
  // variable hoisting. Note: the assignment
  // value of `true` is not hoisted.
  function example() {
    // => undefined
    console.log(declaredButNotAssigned);
    var declaredButNotAssigned = true;
  }

  // The interpreter is hoisting the variable
  // declaration to the top of the scope,
  // which means our example could be rewritten as:
  function example() {
    let declaredButNotAssigned;
    // => undefined
    console.log(declaredButNotAssigned);
    declaredButNotAssigned = true;
  }

  // using const and let
  function example() {
    // => throws a ReferenceError
    console.log(declaredButNotAssigned);
    // => throws a ReferenceError
    console.log(typeof declaredButNotAssigned);
    const declaredButNotAssigned = true;
  }
  ```

- [14.2](#14.2) <a name='14.2'></a> Anonymous function expressions hoist their variable name, but not the function assignment.

  ```javascript
  function example() {
    // => undefined
    console.log(anonymous);

    // => TypeError anonymous is not a function
    anonymous();

    var anonymous = function() {
      console.log('anonymous function expression');
    };
  }
  ```

- [14.3](#14.3) <a name='14.3'></a> Named function expressions hoist the variable name, not the function name or the function body.

  ```javascript
  function example() {
    // => undefined
    console.log(named);

    // => TypeError named is not a function
    named();

    // => ReferenceError superPower is not defined
    superPower();

    var named = function superPower() {
      console.log('Flying');
    };
  }

  // the same is true when the function name
  // is the same as the variable name.
  function example() {
    // => undefined
    console.log(named);

    // => TypeError named is not a function
    named();

    var named = function named() {
      console.log('named');
    }
  }
  ```

- [14.4](#14.4) <a name='14.4'></a> Function declarations hoist their name and the function body.

  ```javascript
  function example() {
    // => Flying
    superPower();

    function superPower() {
      console.log('Flying');
    }
  }
  ```

- [14.5](#14.5) <a name='14.5'></a> For more information refer to [JavaScript Scoping & Hoisting](http://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting/) by [Ben Cherry](http://www.adequatelygood.com/).

**[⬆ back to top](#table-of-contents)**


## 15. Comparison Operators & Equality

- [15.1](#15.1) <a name='15.1'></a> Use `===` and `!==` over `==` and `!=`.

- [15.2](#15.2) <a name='15.2'></a> Conditional statements such as the `if` statement evaluate their expression using coercion with the `ToBoolean` abstract method and always follow these simple rules:

  + **Objects** evaluate to **true**
  + **Undefined** evaluates to **false**
  + **Null** evaluates to **false**
  + **Booleans** evaluate to **the value of the boolean**
  + **Numbers** evaluate to **false** if **+0, -0, or NaN**, otherwise **true**
  + **Strings** evaluate to **false** if an empty string `''`, otherwise **true**

  ```javascript
  if ([0]) {
    // true
    // An array is an object, objects evaluate to true
  }
  ```

- [15.3](#15.3) <a name='15.3'></a> Use shortcuts.

  ```javascript
  // bad
  if (name !== '') {
    // ...stuff...
  }

  // good
  if (name) {
    // ...stuff...
  }

  // bad
  if (collection.length > 0) {
    // ...stuff...
  }

  // good
  if (collection.length) {
    // ...stuff...
  }
  ```

- [15.4](#15.4) <a name='15.4'></a> For more information see [Truth Equality and JavaScript](http://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108) by Angus Croll.

**[⬆ back to top](#table-of-contents)**


## 16. Blocks

- [16.1](#16.1) <a name='16.1'></a> Use braces with all multi-line blocks.

  ```javascript
  // bad
  if (test)
    return false;

  // good
  if (test) return false;

  // good
  if (test) {
    return false;
  }

  // bad
  function() { return false; }

  // good
  function() {
    return false;
  }
  ```

- [16.2](#16.2) <a name='16.2'></a> If you're using multi-line blocks with `if` and `else`, put `else` on the same line as your `if` block's closing brace.

  ```javascript
  // bad
  if (test) {
    thing1();
    thing2();
  }
  else {
    thing3();
  }

  // good
  if (test) {
    thing1();
    thing2();
  } else {
    thing3();
  }
  ```

**[⬆ back to top](#table-of-contents)**


## 17. Comments

- [17.1](#17.1) <a name='17.1'></a> Use `/** ... */` for multi-line comments. Include a description, specify types and values for all parameters and return values.

  ```javascript
  // bad
  // make() returns a new element
  // based on the passed in tag name
  //
  // @param {String} tag
  // @return {Element} element
  function make(tag) {

    // ...stuff...

    return element;
  }

  // good
  /**
   * make() returns a new element
   * based on the passed in tag name
   *
   * @param {String} tag
   * @return {Element} element
   */
  function make(tag) {

    // ...stuff...

    return element;
  }
  ```

- [17.2](#17.2) <a name='17.2'></a> Use `//` for single line comments. Place single line comments on a newline above the subject of the comment. Put an empty line before the comment unless it's on the first line of a block.

  ```javascript
  // bad
  const active = true;  // is current tab

  // good
  // is current tab
  const active = true;

  // bad
  function getType() {
    console.log('fetching type...');
    // set the default type to 'no type'
    const type = this._type || 'no type';

    return type;
  }

  // good
  function getType() {
    console.log('fetching type...');

    // set the default type to 'no type'
    const type = this._type || 'no type';

    return type;
  }

  // also good
  function getType() {
    // set the default type to 'no type'
    const type = this._type || 'no type';

    return type;
  }
  ```

- [17.3](#17.3) <a name='17.3'></a> Prefixing your comments with `FIXME` or `TODO` helps other developers quickly understand if you're pointing out a problem that needs to be revisited, or if you're suggesting a solution to the problem that needs to be implemented. These are different than regular comments because they are actionable. The actions are `FIXME -- need to figure this out` or `TODO -- need to implement`.

- [17.4](#17.4) <a name='17.4'></a> Use `// FIXME:` to annotate problems.

  ```javascript
  class Calculator extends Abacus {
    constructor() {
      super();

      // FIXME: shouldn't use a global here
      total = 0;
    }
  }
  ```

- [17.5](#17.5) <a name='17.5'></a> Use `// TODO:` to annotate solutions to problems.

  ```javascript
  class Calculator extends Abacus {
    constructor() {
      super();

      // TODO: total should be configurable by an options param
      this.total = 0;
    }
  }
  ```

**[⬆ back to top](#table-of-contents)**


## 18. Whitespace

- [18.1](#18.1) <a name='18.1'></a> Use soft tabs set to 2 spaces.

  ```javascript
  // bad
  function() {
  ∙∙∙∙const name;
  }

  // bad
  function() {
  ∙const name;
  }

  // good
  function() {
  ∙∙const name;
  }
  ```

- [18.2](#18.2) <a name='18.2'></a> Place 1 space before the leading brace.

  ```javascript
  // bad
  function test(){
    console.log('test');
  }

  // good
  function test() {
    console.log('test');
  }

  // bad
  dog.set('attr',{
    age: '1 year',
    breed: 'Bernese Mountain Dog',
  });

  // good
  dog.set('attr', {
    age: '1 year',
    breed: 'Bernese Mountain Dog',
  });
  ```

- [18.3](#18.3) <a name='18.3'></a> Place 1 space before the opening parenthesis in control statements (`if`, `while` etc.). Place no space before the argument list in function calls and declarations.

  ```javascript
  // bad
  if(isJedi) {
    fight ();
  }

  // good
  if (isJedi) {
    fight();
  }

  // bad
  function fight () {
    console.log ('Swooosh!');
  }

  // good
  function fight() {
    console.log('Swooosh!');
  }
  ```

- [18.4](#18.4) <a name='18.4'></a> Set off operators with spaces.

  ```javascript
  // bad
  const x=y+5;

  // good
  const x = y + 5;
  ```

- [18.5](#18.5) <a name='18.5'></a> End files with a single newline character.

  ```javascript
  // bad
  (function(global) {
    // ...stuff...
  })(this);
  ```

  ```javascript
  // bad
  (function(global) {
    // ...stuff...
  })(this);↵
  ↵
  ```

  ```javascript
  // good
  (function(global) {
    // ...stuff...
  })(this);↵
  ```

- [18.6](#18.6) <a name='18.6'></a> Use indentation when making long method chains. Use a leading dot, which emphasizes that the line is a method call, not a new statement.

  ```javascript
  // bad
  $('#items').find('.selected').highlight().end().find('.open').updateCount();

  // bad
  $('#items').
    find('.selected').
      highlight().
      end().
    find('.open').
      updateCount();

  // good
  $('#items')
    .find('.selected')
      .highlight()
      .end()
    .find('.open')
      .updateCount();

  // bad
  const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').class('led', true)
      .attr('width', (radius + margin) * 2).append('svg:g')
      .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
      .call(tron.led);

  // good
  const leds = stage.selectAll('.led')
      .data(data)
    .enter().append('svg:svg')
      .classed('led', true)
      .attr('width', (radius + margin) * 2)
    .append('svg:g')
      .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
      .call(tron.led);
  ```

- [18.7](#18.7) <a name='18.7'></a> Leave a blank line after blocks and before the next statement.

  ```javascript
  // bad
  if (foo) {
    return bar;
  }
  return baz;

  // good
  if (foo) {
    return bar;
  }

  return baz;

  // bad
  const obj = {
    foo() {
    },
    bar() {
    },
  };
  return obj;

  // good
  const obj = {
    foo() {
    },

    bar() {
    },
  };

  return obj;

  // bad
  const arr = [
    function foo() {
    },
    function bar() {
    },
  ];
  return arr;

  // good
  const arr = [
    function foo() {
    },

    function bar() {
    },
  ];

  return arr;
  ```

- [18.8](#18.8) <a name='18.8'></a> Do not pad your blocks with blank lines.

  ```javascript
  // bad
  function bar() {

    console.log(foo);

  }

  // also bad
  if (baz) {

    console.log(qux);
  } else {
    console.log(foo);

  }

  // good
  function bar() {
    console.log(foo);
  }

  // good
  if (baz) {
    console.log(qux);
  } else {
    console.log(foo);
  }
  ```

- [18.9](#18.9) <a name='18.9'></a> Do not add spaces inside parentheses.

  ```javascript
  // bad
  function bar( foo ) {
    return foo;
  }

  // good
  function bar(foo) {
    return foo;
  }

  // bad
  if ( foo ) {
    console.log(foo);
  }

  // good
  if (foo) {
    console.log(foo);
  }
  ```

- [18.10](#18.10) <a name='18.10'></a> Do not add spaces inside brackets.

  ```javascript
  // bad
  const foo = [ 1, 2, 3 ];
  console.log(foo[ 0 ]);

  // good
  const foo = [1, 2, 3];
  console.log(foo[0]);
  ```

  - [18.11](#18.11) <a name='18.11'></a> Add spaces inside curly braces.

    ```javascript
    // bad
    const foo = {clark: 'kent'};

    // good
    const foo = { clark: 'kent' };
    ```

**[⬆ back to top](#table-of-contents)**


## 19. Commas

- [19.1](#19.1) <a name='19.1'></a> Leading commas: **Nope.**

  ```javascript
  // bad
  const story = [
      once
    , upon
    , aTime
  ];

  // good
  const story = [
    once,
    upon,
    aTime,
  ];

  // bad
  const hero = {
      firstName: 'Ada'
    , lastName: 'Lovelace'
    , birthYear: 1815
    , superPower: 'computers'
  };

  // good
  const hero = {
    firstName: 'Ada',
    lastName: 'Lovelace',
    birthYear: 1815,
    superPower: 'computers',
  };
  ```

- [19.2](#19.2) ([**ES6**](#27-ecmascript-6-styles)) <a name='19.2'></a> Additional trailing comma: **Yup.**

  > Why? This leads to cleaner git diffs. Also, transpilers like Babel will remove the additional trailing comma in the transpiled code which means you don't have to worry about the [trailing comma problem](es5/README.md#commas) in legacy browsers.

  ```javascript
  // bad - git diff without trailing comma
  const hero = {
       firstName: 'Florence',
  -    lastName: 'Nightingale'
  +    lastName: 'Nightingale',
  +    inventorOf: ['coxcomb graph', 'modern nursing']
  };

  // good - git diff with trailing comma
  const hero = {
       firstName: 'Florence',
       lastName: 'Nightingale',
  +    inventorOf: ['coxcomb chart', 'modern nursing'],
  };

  // bad
  const hero = {
    firstName: 'Dana',
    lastName: 'Scully'
  };

  const heroes = [
    'Batman',
    'Superman'
  ];

  // good
  const hero = {
    firstName: 'Dana',
    lastName: 'Scully',
  };

  const heroes = [
    'Batman',
    'Superman',
  ];
  ```

  ([**ES5**](#26-ecmascript-5-compatibility)) Additional trailing comma: **Nope.** This can cause problems with IE6/7 and IE9 if it's in quirksmode. Also, in some implementations of ES3 would add length to an array if it had an additional trailing comma. This was clarified in ES5 ([source](http://es5.github.io/#D)):

    > Edition 5 clarifies the fact that a trailing comma at the end of an ArrayInitialiser does not add to the length of the array. This is not a semantic change from Edition 3 but some implementations may have previously misinterpreted this.

  ```javascript
  // bad
  var hero = {
    firstName: 'Kevin',
    lastName: 'Flynn',
  };

  var heroes = [
    'Batman',
    'Superman',
  ];

  // good
  var hero = {
    firstName: 'Kevin',
    lastName: 'Flynn'
  };

  var heroes = [
    'Batman',
    'Superman'
  ];
  ```

**[⬆ back to top](#table-of-contents)**


## 20. Semicolons

- [20.1](#20.1) <a name='20.1'></a> **Yup.**

  ```javascript
  // bad
  (function() {
    const name = 'Skywalker'
    return name
  })()

  // good
  (() => {
    const name = 'Skywalker';
    return name;
  })();

  // good (guards against the function becoming an argument when two files with IIFEs are concatenated)
  ;(() => {
    const name = 'Skywalker';
    return name;
  })();
  ```

  [Read more](http://stackoverflow.com/questions/7365172/semicolon-before-self-invoking-function/7365214%237365214).

**[⬆ back to top](#table-of-contents)**


## 21. Type Casting & Coercion

- [21.1](#21.1) <a name='21.1'></a> Perform type coercion at the beginning of the statement.

- [21.2](#21.2) <a name='21.2'></a> Strings:

  ```javascript
  //  => this.reviewScore = 9;

  // bad
  const totalScore = this.reviewScore + '';

  // good
  const totalScore = String(this.reviewScore);
  ```

- [21.3](#21.3) <a name='21.3'></a> Numbers: Use `Number` for type casting and `parseInt` always with a radix for parsing strings.

  ```javascript
  const inputValue = '4';

  // bad
  const val = new Number(inputValue);

  // bad
  const val = +inputValue;

  // bad
  const val = inputValue >> 0;

  // bad
  const val = parseInt(inputValue);

  // good
  const val = Number(inputValue);

  // good
  const val = parseInt(inputValue, 10);
  ```

- [21.4](#21.4) <a name='21.4'></a> If for whatever reason you are doing something wild and `parseInt` is your bottleneck and need to use Bitshift for [performance reasons](http://jsperf.com/coercion-vs-casting/3), leave a comment explaining why and what you're doing.

  ```javascript
  // good
  /**
   * parseInt was the reason my code was slow.
   * Bitshifting the String to coerce it to a
   * Number made it a lot faster.
   */
  const val = inputValue >> 0;
  ```

- [21.5](#21.5) <a name='21.5'></a> **Note:** Be careful when using bitshift operations. Numbers are represented as [64-bit values](http://es5.github.io/#x4.3.19), but Bitshift operations always return a 32-bit integer ([source](http://es5.github.io/#x11.7)). Bitshift can lead to unexpected behavior for integer values larger than 32 bits. [Discussion](https://github.com/airbnb/javascript/issues/109). Largest signed 32-bit Int is 2,147,483,647:

  ```javascript
  2147483647 >> 0 //=> 2147483647
  2147483648 >> 0 //=> -2147483648
  2147483649 >> 0 //=> -2147483647
  ```

- [21.6](#21.6) <a name='21.6'></a> Booleans:

  ```javascript
  const age = 0;

  // bad
  const hasAge = new Boolean(age);

  // good
  const hasAge = Boolean(age);

  // good
  const hasAge = !!age;
  ```

**[⬆ back to top](#table-of-contents)**


## 22. Naming Conventions

- [22.1](#22.1) <a name='22.1'></a> Avoid single letter names. Be descriptive with your naming.

  ```javascript
  // bad
  function q() {
    // ...stuff...
  }

  // good
  function query() {
    // ...stuff...
  }
  ```

- [22.2](#22.2) <a name='22.2'></a> Use camelCase when naming objects, functions, and instances.

  ```javascript
  // bad
  const OBJEcttsssss = {};
  const this_is_my_object = {};
  function c() {}

  // good
  const thisIsMyObject = {};
  function thisIsMyFunction() {}
  ```

- [22.3](#22.3) <a name='22.3'></a> Use PascalCase when naming constructors or classes.

  ```javascript
  // bad
  function user(options) {
    this.name = options.name;
  }

  const bad = new user({
    name: 'nope',
  });

  // good
  class User {
    constructor(options) {
      this.name = options.name;
    }
  }

  const good = new User({
    name: 'yup',
  });
  ```

- [22.4](#22.4) <a name='22.4'></a> Use a leading underscore `_` when naming private properties.

  ```javascript
  // bad
  this.__firstName__ = 'Panda';
  this.firstName_ = 'Panda';

  // good
  this._firstName = 'Panda';
  ```

- [22.5](#22.5) ([**ES6**](#27-ecmascript-6-styles)) <a name='22.5'></a> Don't save references to `this`. Use arrow functions or Function#bind.

  ```javascript
  // bad
  function foo() {
    const self = this;
    return function() {
      console.log(self);
    };
  }

  // bad
  function foo() {
    const that = this;
    return function() {
      console.log(that);
    };
  }

  // good
  function foo() {
    return () => {
      console.log(this);
    };
  }
  ```

  ~~([**ES5**](#26-ecmascript-5-compatibility)) When saving a reference to `this` use `_this`.~~

  ```javascript
  // bad
  function() {
    var self = this;
    return function() {
      console.log(self);
    };
  }

  // bad
  function() {
    var that = this;
    return function() {
      console.log(that);
    };
  }

  // good
  function() {
    var _this = this;
    return function() {
      console.log(_this);
    };
  }
  ```

- [22.6](#22.6) <a name='22.6'></a> If your file exports a single class, your filename should be exactly the name of the class.

  ```javascript
  // file contents
  class CheckBox {
    // ...
  }
  export default CheckBox;

  // in some other file
  // bad
  import CheckBox from './checkBox';

  // bad
  import CheckBox from './check_box';

  // good
  import CheckBox from './CheckBox';
  ```

- [22.7](#22.7) ([**ES6**](#27-ecmascript-6-styles)) <a name='22.7'></a> Use camelCase when you export-default a function. Your filename should be identical to your function's name.

  ```javascript
  function makeStyleGuide() {
  }

  export default makeStyleGuide;
  ```

- [22.8](#22.8) ([**ES6**](#27-ecmascript-6-styles)) <a name='22.8'></a> Use PascalCase when you export a singleton / function library / bare object.

  ```javascript
  const TipplrStyleGuide = {
    es6: {
    }
  };

  export default TipplrStyleGuide;
  ```

- [22.9](#22.9) <a name='22.9'></a> Name your functions. This is helpful for stack traces.

  ```javascript
  // bad
  var log = function(msg) {
    console.log(msg);
  };

  // good
  var log = function log(msg) {
    console.log(msg);
  };
  ```

  ([**ES5**](#26-ecmascript-5-compatibility)) **Note:** IE8 and below exhibit some quirks with named function expressions.  See [http://kangax.github.io/nfe/](http://kangax.github.io/nfe/) for more info.

**[⬆ back to top](#table-of-contents)**


## 23. Accessors

- [23.1](#23.1) <a name='23.1'></a> Accessor functions for properties are not required.

- [23.2](#23.2) <a name='23.2'></a> If you do make accessor functions use getVal() and setVal('hello').

  ```javascript
  // bad
  dragon.age();

  // good
  dragon.getAge();

  // bad
  dragon.age(25);

  // good
  dragon.setAge(25);
  ```

- [23.3](#23.3) <a name='23.3'></a> If the property is a `boolean`, use `isVal()` or `hasVal()`.

  ```javascript
  // bad
  if (!dragon.age()) {
    return false;
  }

  // good
  if (!dragon.hasAge()) {
    return false;
  }
  ```

- [23.4](#23.4) <a name='23.4'></a> It's okay to create get() and set() functions, but be consistent.

  ```javascript
  class Jedi {
    constructor(options = {}) {
      const lightsaber = options.lightsaber || 'blue';
      this.set('lightsaber', lightsaber);
    }

    set(key, val) {
      this[key] = val;
    }

    get(key) {
      return this[key];
    }
  }
  ```

**[⬆ back to top](#table-of-contents)**


## 24. Events

- [24.1](#24.1) <a name='24.1'></a> When attaching data payloads to events (whether DOM events or something more proprietary like Backbone events), pass a hash instead of a raw value. This allows a subsequent contributor to add more data to the event payload without finding and updating every handler for the event. For example, instead of:

  ```javascript
  // bad
  $(this).trigger('listingUpdated', listing.id);

  ...

  $(this).on('listingUpdated', function(e, listingId) {
    // do something with listingId
  });
  ```

  prefer:

  ```javascript
  // good
  $(this).trigger('listingUpdated', { listingId: listing.id });

  ...

  $(this).on('listingUpdated', function(e, data) {
    // do something with data.listingId
  });
  ```

  **[⬆ back to top](#table-of-contents)**


## 25. jQuery

- [25.1](#25.1) <a name='25.1'></a> Prefix jQuery object variables with a `$`.

  ```javascript
  // bad
  const sidebar = $('.sidebar');

  // good
  const $sidebar = $('.sidebar');

  // good
  const $sidebarBtn = $('.sidebar-btn');
  ```

- [25.2](#25.2) <a name='25.2'></a> Cache jQuery lookups.

  ```javascript
  // bad
  function setSidebar() {
    $('.sidebar').hide();

    // ...stuff...

    $('.sidebar').css({
      'background-color': 'pink'
    });
  }

  // good
  function setSidebar() {
    const $sidebar = $('.sidebar');
    $sidebar.hide();

    // ...stuff...

    $sidebar.css({
      'background-color': 'pink'
    });
  }
  ```

- [25.3](#25.3) <a name='25.3'></a> For DOM queries use Cascading `$('.sidebar ul')` or parent > child `$('.sidebar > ul')`. [jsPerf](http://jsperf.com/jquery-find-vs-context-sel/16)

- [25.4](#25.4) <a name='25.4'></a> Use `find` with scoped jQuery object queries.

  ```javascript
  // bad
  $('ul', '.sidebar').hide();

  // bad
  $('.sidebar').find('ul').hide();

  // good
  $('.sidebar ul').hide();

  // good
  $('.sidebar > ul').hide();

  // good
  $sidebar.find('ul').hide();
  ```

**[⬆ back to top](#table-of-contents)**


## 26. ECMAScript 5 Compatibility

- [26.1](#26.1) <a name='26.1'></a> Refer to [Kangax](https://twitter.com/kangax/)'s ES5 [compatibility table](http://kangax.github.io/es5-compat-table/).

- [26.2](#26.2) <a name='26.2'></a> You should always use ECMAScript 6 and transform your code to ECMAScript 5 using transpilers like [Babel](http://babeljs.io/).

**[⬆ back to top](#table-of-contents)**


## 27. ECMAScript 6 Styles

- [27.1](#27.1) <a name='27.1'></a> This is a collection of links to the various ECMAScript 6 features.

  + [Arrow Functions](#8-arrow-functions)
  + [Classes](#9-constructors)
  + [Object Shorthand](#3.5)
  + [Object Concise](#3.6)
  + [Object Computed Properties](#3.4)
  + [Template Strings](#6.4)
  + [Destructuring](#5-destructuring)
  + [Default Parameters](#7.7)
  + [Rest](#7.6)
  + [Array Spreads](#4.3)
  + [Let and Const](#2-references)
  + [Iterators and Generators](#11-iterators-and-generators)
  + [Modules](#10-modules)

**[⬆ back to top](#table-of-contents)**


## 28. Testing

- [28.1](#28.1) <a name='28.1'></a> **Yup.**

  ```javascript
  function () {
    return true;
  }
  ```

- [28.2](#28.2) <a name='28.2'></a> **No, but seriously**:
  + Whichever testing framework you use, you should be writing tests!
  + Strive to write many small pure functions, and minimize where mutations occur.
  + Be cautious about stubs and mocks - they can make your tests more brittle.
  + We primarily use [`mocha`](https://www.npmjs.com/package/mocha) at Tipplr. [`tape`](https://www.npmjs.com/package/tape) is also used occasionally for small, separate modules.
  + 100% test coverage is a good goal to strive for, even if it's not always practical to reach it.
  + Whenever you fix a bug, _write a regression test_. A bug fixed without a regression test is almost certainly going to break again in the future.

**[⬆ back to top](#table-of-contents)**


## 29. Directory Structure

- [29.1](#29.1) <a name='29.1'></a> A top-level directory layout:

        .
        ├─ build      # Compiled and transpiled files
        ├─ docs       # Documentation files
        ├─ src        # Source files
        ├─ tests      # Automated tests
        ├─ bin        # Tools and utilities
        ├─ LICENSE
        └─ README.md

- [29.2](#29.2) <a name='29.2'></a> For some samples refer to [Folder Structure Conventions](https://github.com/kriasoft/Folder-Structure-Conventions) by Konstantin Tarkus

**[⬆ back to top](#table-of-contents)**


## 30. Performance

- [On Layout & Web Performance](http://www.kellegous.com/j/2013/01/26/layout-performance/)
- [String vs Array Concat](http://jsperf.com/string-vs-array-concat/2)
- [Try/Catch Cost In a Loop](http://jsperf.com/try-catch-in-loop-cost)
- [Bang Function](http://jsperf.com/bang-function)
- [jQuery Find vs Context, Selector](http://jsperf.com/jquery-find-vs-context-sel/13)
- [innerHTML vs textContent for script text](http://jsperf.com/innerhtml-vs-textcontent-for-script-text)
- [Long String Concatenation](http://jsperf.com/ya-string-concat)
- Loading...

**[⬆ back to top](#table-of-contents)**


## 31. Resources

**Learning ES6**

- [Draft ECMA 2015 (ES6) Spec](https://people.mozilla.org/~jorendorff/es6-draft.html)
- [ExploringJS](http://exploringjs.com/)
- [ES6 Compatibility Table](https://kangax.github.io/compat-table/es6/)
- [Comprehensive Overview of ES6 Features](http://es6-features.org/)

**Read This**

- [Standard ECMA-262](http://www.ecma-international.org/ecma-262/6.0/index.html)

**Tools**

- Code Style Linters
  + [ESlint](http://eslint.org/) - [Tipplr Style .eslintrc](https://github.com/tipplrio/styleguides/blob/master/linters/.eslintrc)

**Other Style Guides**

- [Google JavaScript Style Guide](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml)
- [jQuery Core Style Guidelines](http://contribute.jquery.org/style-guide/js/)
- [Principles of Writing Consistent, Idiomatic JavaScript](https://github.com/rwaldron/idiomatic.js)

**Other Styles**

- [Naming this in nested functions](https://gist.github.com/cjohansen/4135065) - Christian Johansen
- [Conditional Callbacks](https://github.com/airbnb/javascript/issues/52) - Ross Allen
- [Popular JavaScript Coding Conventions on Github](http://sideeffect.kr/popularconvention/#javascript) - JeongHoon Byun
- [Multiple var statements in JavaScript, not superfluous](http://benalman.com/news/2012/05/multiple-var-statements-javascript/) - Ben Alman

**Further Reading**

- [Understanding JavaScript Closures](http://javascriptweblog.wordpress.com/2010/10/25/understanding-javascript-closures/) - Angus Croll
- [Basic JavaScript for the impatient programmer](http://www.2ality.com/2013/06/basic-javascript.html) - Dr. Axel Rauschmayer
- [You Might Not Need jQuery](http://youmightnotneedjquery.com/) - Zack Bloom & Adam Schwartz
- [ES6 Features](https://github.com/lukehoban/es6features) - Luke Hoban
- [Frontend Guidelines](https://github.com/bendc/frontend-guidelines) - Benjamin De Cock

**Books**

- [JavaScript: The Good Parts](http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742) - Douglas Crockford
- [JavaScript Patterns](http://www.amazon.com/JavaScript-Patterns-Stoyan-Stefanov/dp/0596806752) - Stoyan Stefanov
- [Pro JavaScript Design Patterns](http://www.amazon.com/JavaScript-Design-Patterns-Recipes-Problem-Solution/dp/159059908X)  - Ross Harmes and Dustin Diaz
- [High Performance Web Sites: Essential Knowledge for Front-End Engineers](http://www.amazon.com/High-Performance-Web-Sites-Essential/dp/0596529309) - Steve Souders
- [Maintainable JavaScript](http://www.amazon.com/Maintainable-JavaScript-Nicholas-C-Zakas/dp/1449327680) - Nicholas C. Zakas
- [JavaScript Web Applications](http://www.amazon.com/JavaScript-Web-Applications-Alex-MacCaw/dp/144930351X) - Alex MacCaw
- [Pro JavaScript Techniques](http://www.amazon.com/Pro-JavaScript-Techniques-John-Resig/dp/1590597273) - John Resig
- [Smashing Node.js: JavaScript Everywhere](http://www.amazon.com/Smashing-Node-js-JavaScript-Everywhere-Magazine/dp/1119962595) - Guillermo Rauch
- [Secrets of the JavaScript Ninja](http://www.amazon.com/Secrets-JavaScript-Ninja-John-Resig/dp/193398869X) - John Resig and Bear Bibeault
- [Human JavaScript](http://humanjavascript.com/) - Henrik Joreteg
- [Superhero.js](http://superherojs.com/) - Kim Joar Bekkelund, Mads Mobæk, & Olav Bjorkoy
- [JSBooks](http://jsbooks.revolunet.com/) - Julien Bouquillon
- [Third Party JavaScript](https://www.manning.com/books/third-party-javascript) - Ben Vinegar and Anton Kovalyov
- [Effective JavaScript: 68 Specific Ways to Harness the Power of JavaScript](http://amzn.com/0321812182) - David Herman
- [Eloquent JavaScript](http://eloquentjavascript.net/) - Marijn Haverbeke
- [You Don't Know JS: ES6 & Beyond](http://shop.oreilly.com/product/0636920033769.do) - Kyle Simpson
- [Learning Behavior-driven Development with JavaScript](https://www.packtpub.com/application-development/learning-behavior-driven-development-javascript) - Enrique Amodeo

**Blogs**

- [DailyJS](http://dailyjs.com/)
- [JavaScript Weekly](http://javascriptweekly.com/)
- [JavaScript, JavaScript...](http://javascriptweblog.wordpress.com/)
- [Bocoup Weblog](https://bocoup.com/weblog)
- [Adequately Good](http://www.adequatelygood.com/)
- [NCZOnline](https://www.nczonline.net/)
- [Perfection Kills](http://perfectionkills.com/)
- [Ben Alman](http://benalman.com/)
- [Dmitry Baranovskiy](http://dmitry.baranovskiy.com/)
- [Dustin Diaz](http://dustindiaz.com/)
- [nettuts](http://code.tutsplus.com/?s=javascript)

**Podcasts**

- [JavaScript Jabber](https://devchat.tv/js-jabber/)

**[⬆ back to top](#table-of-contents)**


## 32. Contributors

- [View Contributors](https://github.com/tipplrio/styleguides/graphs/contributors)

**[⬆ back to top](#table-of-contents)**


## 33. License

The MIT License (MIT)

Copyright (c) 2014 Airbnb
Copyright (c) 2015 Tipplr

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

**[⬆ back to top](#table-of-contents)**


# };
