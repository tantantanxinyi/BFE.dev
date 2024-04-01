# Create a pipe()



The link: https://bigfrontend.dev/problem/what-is-composition-create-a-pipe

what is Composition? It is actually not that difficult to understand, see [@dan_abramov 's explanation](https://whatthefuck.is/composition).

Here you are asked to create a pipe() function, which chains multiple functions together to create a new function.

Suppose we have some simple functions like this

```plain
const times = (y) =>  (x) => x * y
const plus = (y) => (x) => x + y
const subtract = (y) =>  (x) => x - y
const divide = (y) => (x) => x / y
```

Your pipe() would be used to generate new functions

```plain
pipe([
  times(2),
  times(3)
])  
// x * 2 * 3

pipe([
  times(2),
  plus(3),
  times(4)
]) 
// (x * 2 + 3) * 4

pipe([
  times(2),
  subtract(3),
  divide(4)
]) 
// (x * 2 - 3) / 4
```

**notes**

1. to make things simple, functions passed to pipe() will all accept 1 argument



Answer:

```javascript
const times = (y) =>  (x) => x * y
const plus = (y) => (x) => x + y
const subtract = (y) =>  (x) => x - y
const divide = (y) => (x) => x / y



function pipe(funcs){
  return function(x) => {
    let result = x;
    for(let func of funcs){
      result = func.call(this,result)
    }
    return result;
  }
}


pipe([
  times(2),
  times(3)
])  
// x * 2 * 3

pipe([
  times(2),
  times(3)
])(2)
// 2 * 2 *3

pipe([
  times(2),
  plus(3),
  times(4)
]) 
// (x * 2 + 3) * 4

pipe([
  times(2),
  subtract(3),
  divide(4)
]) 
// (x * 2 - 3) / 4
```



The pipe function accept the parameter which is the function array, and return a new function that accept 'x' parameter, and we define a result variable equals the x,  next we use for in loop to iterate over the  funcs,  and func will be called and pass to the next func,  lastly, return the result.