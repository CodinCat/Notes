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

用Spread operator來複製物件或陣列

```js
let ary1 = [0, 1, 2]
let ary2 = [...ary1]

let msg1 = { text: 'hello' }
let msg2 = {...msg1}

// 用於方法傳值
function add({...obj}) {
  obj.n++
  console.log(obj.n) // 6
}

let obj = { n: 5 }
add(obj)
console.log(obj.n) // 5

```

組合陣列（push可接受多個參數）

```js
ary1.push(...ary2) // [0, 1, 2, 0, 1, 2]
```

## iterator / generator / symbol

實作`Symbol.iterator`後便能使用 for ... of

Generator: 
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
```

Or: 
```js
let bar = {}

bar[Symbol.iterator] = function () {
    return {
        i: 0,
        next() {
            if (this.i > 10) return { done: true }
            return { value: this.i++, done: false }
        }
    }
}

for (let val of bar) {
    console.log(val)
}
```

fibonacci generator: 
```js
function* fibonacci() {
    let [prev, curr] = [1, 1]
    while (true) {
        [prev, curr] = [curr, prev + curr]
        yield curr
    }
}

for (let n of fibonacci()) {
    if (n < 100) {
        console.log(n)
    } else {
        break
    }
}
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
