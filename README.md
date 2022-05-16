# JavaScript Extension Methods Proposal

This is a proposal to add extension methods to JavaScript.

## What are extension methods?

Extension methods are a way of adding new methods to a an existing class without
modifying the class itself.

The name and precise details of this feature vary across languages. It is called
extension methods in C#. A similar feature in Ruby is called module
augmentation, and there are likely others as well.

## Why add extension methods?

In a word, expressiveness. Adding new methods to existing classes allows
developers to write code that is more readable, and often, easier to write.

Early JavaScript libraries like [Prototype.js][prototype] and
[MooTools][mootools] added extensively to the prototypes of JavaScript's
built-in classes for the sake of productivity and clarity.

The downside, we eventually learned, was the problem of clashing names when
more than one library attempted to augment the built-in classes. This could be
especially confusing if the clashing methods were similar, but not identical
in functionality.

Extension methods allow us to have the greater expressivity we gain from
modifying prototypes, but without actually modifying them.

## How does it work?

The proposed syntax for extension methods is almost identical to that for
creating a new class.

```
class #FooExtensions extends Foo {
    someMethod() { }
}
```

The `#` prefixing the class name indicates that rather than inheriting, we are creating
an extension class.

Within that module's scope, the extension methods are in effect. And if you
import a extension into another module, the importing module also gains access
to those extensions within its lexical scope.

```
import { #FooExtensions } from 'foo.js';
```

However, extension methods are not "viral." They do not spread beyond the
specific modules that import them. So if there is a module `c.js` which imports
`b.js` which then imports an extension method from `a.js`, `a.js` and `b.js`
will have access to the extension methods, but `c.js` will not.

## Example

```js
// string-extensions.js
export class #StringExtensions extends String {
    toCamelCase() {
        // CamelCasing logic ommitted
        return camelCasedString;
    }
}
```

```js
// array-utils.js
import { #StringExtensions } from 'string-extensions.js';

function camelCaseAll(arrayOfStrings) {
    // We can use the toCamelCase() method because we imported #StringExtensions
    return arrayOfStrings.map(s => s.toCamelCase());
}
```

```js
// process-names.js
import 'array-utils.js'

const names = ['Spider-Man', 'Captain Marvel'];

// We can safely use camelCaseAll() even without importing #StringExtensions
console.log(camelCaseAll(names));
// ['spiderMan', 'captainMarvel']

// But we cannot write code that uses the toCamelCase() method
console.log(names.map(s => s.toCamelCase()))
// TypeError: "s".toCamelCase is not a function
```

[prototype]:http://prototypejs.org/
[mootools]: https://mootools.net/