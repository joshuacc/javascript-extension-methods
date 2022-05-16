# JavaScript Extension Methods

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

