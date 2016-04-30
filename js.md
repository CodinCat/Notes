# ES2015

## Destructuring

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

// =====

let x = [0, 1, 2, 3];
let [y, z] = x;

console.log(y, z) // 0 1

```

## Spread operator

```js
function myFunction(x, y, z) {
    console.log(x, y, z);
}

let args = [0, 1, 2];
myFunction(...args);

```

