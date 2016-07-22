# ES2015

## Destructuring

```js
let person = {
    first: 'John',
    last: 'Cena'
}

let { first, last } = person

console.log(first, last) // "John" "Cena" 

// =====

function printLastName({ last }) {
    console.log(last)
}

printLastName(person) // "Cena"

// =====

let x = [0, 1, 2, 3]
let [y, z] = x

console.log(y, z) // 0 1

```

## Spread operator

```js
function myFunction(x, y, z) {
    console.log(x, y, z)
}

let args = [0, 1, 2]
myFunction(...args)

```

## iterator / generator / symbol

實作`Symbol.iterator`後便能使用 for ... of
```js
let foo = {}

foo[Symbol.iterator] = function* () {
    let i = 0
    yield ++i
    yield ++i
    yield ++i
}

for (let val of foo) {
    console.log(val)
}
// 1 2 3
```

# Misc

### bind

```js
const D = document
const $1 = D.getElementById

$1('foo') // error!

const $2 = D.getElementById.bind(D)

$2('foo') // correct
```

```js
const OBJ = {}

OBJ.foo = function () {
    console.log(this)
}

let myFoo = OBJ.foo

OBJ.foo() // Object {}
myFoo() // Window
```
