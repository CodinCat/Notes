# ES2015

## Object Destructuring

```js
let person = {
    first: 'John',
    last: 'Cena'
};

let { first, last } = person;

console.log(first, last); // "John" "Cena" 

// =====

function printLastName({ last }) {
    console.log(last);
}

printLastName(person); // "Cena"

```
