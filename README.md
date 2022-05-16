# JavaScript Extension Methods Proposal

This is a proposal to add extension methods to JavaScript.

## What are extension methods?

Extension methods are a way of adding new methods to a an existing class without
modifying the class itself.

The name and precise details of this feature vary across languages. It is called
extension methods in C#. A similar feature in Ruby is called module
augmentation, and there are likely others as well.

## Why add extension methods?



## Example

```js
// string-extensions.js
class StringExtensions #extends String {
    toCamelCase() {
        // CamelCasing logic ommitted
        return camelCasedString;
    }
}
```

```js
// array-utils.js
import string-extensions.js;

function camelCaseAll(arrayOfStrings) {
    return arrayOfStrings.map(s => s.toCamelCase());
}
```

```js
// process-names.js
import array-utils.js

const names = ['Spider-Man', 'Captain Marvel'];

console.log(camelCaseAll(names));
// ['spiderMan', 'captainMarvel']

console.log(names.map(s => s.toCamelCase()))
// TypeError: "s".toCamelCase is not a function
```

