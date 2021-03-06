# Math Plus
____

## Why

There are dozens of math libraries out there. Why use this one?

No good reason, personal preference. It's a lightweight Math library that extends
the standard Math object with some overridden functionality, added methods and classes.

## Usage

The main reason I use this package is because I like the rest/spread syntax in
es6.

Rather than this:

```js
const { random, floor, ceil } = Math
```

I can do this:
```js
import { random, floor, ceil } from 'math-plus'
```

## Overridden Methods

The ```round()```, ```floor()``` and ```ceil()``` methods is overridden to take a second parameter
*place*.

```js
import { round, ceil, floor } from 'math-plus'

round(10.575, 0.1) // rounds to the nearest 0.1 = 10.6
ceil(109.10, 10) // ceil to the nearest 10 = 110
floor(86.5, 100) // floor to the nearest 100 = 0
```


The ```random()``` method is overridden to take up to three parameters:
*min, max and seed*.

```js
import { random } from 'math-plus'

random(2, 5) // random value between 2 and 5

random(-10, 10, 1000) // Third argument acts as a seed, providing the same number

```

`random` can also be used to return a random element from an array, string, or array-like.
Min and max are treated as index ranges.
```js
import { random } from 'math-plus'

const string = 'letters-are-cool'

// Returns a letter between index 0 (min) and array.length(max) (non-inclusive)
const randomChar = random(0, string.length, string)

const array = [ 'one', 2, { three: 3 } ]
// undefined as max will default to array.length
const randomItem = random(0, undefined, array)

// array-likes must have have number indexes and a length property
const arrayLike = { 0: 'one', 1: 'two', 2: 'three', length: 3 }
const randomArrayLikeItem = random(0, undefined, arrayLike)

// iterables also work (Set, Map, any Object with Symbol.iterator)
const iterable = new Set([1, 2, 3, 4])
const randomIterable = random(0, undefined, iterable)

```

See the [Bindable Methods](#bindable-methods) section for a cleaner syntax for the `random` method.

## Added Methods

The ```lerp()``` method, which interpolates one value to another:

```js
import { lerp } from 'math-plus'

// lerp(from, to, interpolator)
lerp(5, 10, 0.5) // 7.5
lerp(2, 1, 0.5) // 1.5
lerp(3, 6, 2) // 9
```


The ```clamp()``` method, which is self explanatory

```js
import { clamp } from 'math-plus'

// clamp(value, min = 0, max = 1)
clamp(2) // 1
clamp(0, 1, 2) // 1
```

The ```isPrime()``` method, also self explanatory

```js
import { isPrime } from 'math-plus'

// isPrime(value)
isPrime(5) // true
isPrime(4) // false
```

The ```primes()``` method, which returns a generator that iterates prime numbers

```js
import { primes } from 'math-plus'

const to10 = [...primes(9)] // [2,3,5,7,9]

for (const prime of primes(50, 100))
  console.log(prime) //logs every prime between 50 and 100
```

## Bindable Methods ``::``

I don't know if you have heard of the bind operator, but I LOVE the bind operator.
Read more here: https://babeljs.io/docs/plugins/transform-function-bind/
Where-ever prudent, the overridden and custom methods allow numbers to be bound
to them:

```js

import { round, random, primes } from 'math-plus'

10.4::round() //10

1000::random(-10, 10) // binding a value to random gives it a seed

// You can also bind arrays, iterables, array-likes or strings to the random method

'string'::random() // random char
[1,2,3,4]::random() // random item

// primes isn't bindable, but it does return an iterator
primes(1000)::random() // random prime number between 0 and 1000

```

List of all bindable methods:

``lerp``, ``clamp``, ``isPrime``, ``round``, ``floor``, ``ceil``, ``pow``, ``abs``, ``acos``, ``acosh``, ``asin``, ``asinh``, ``atan``, ``atanh``, ``cbrt``, ``clz32``, ``cos``, ``cosh``, ``exp``, ``expm1``, ``fround``, ``log``, ``log10``, ``log1p``, ``log2``, ``sign``, ``sin``, ``sinh``, ``sqrt``, ``tan``, ``tanh``, ``trunc``
