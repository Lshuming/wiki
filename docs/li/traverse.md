# JS数组遍历
## for循环
最简单的一种，也是使用频率最高的一种，使用临时变量，将长度缓存起来，避免重复获取数组长度。  
### 1，return
```javascript
for (let i = 0; i < 10; i++) {
  let newArr = []
  newArr.push(arr[i])
  return newArr // Uncaught SyntaxError: Illegal return statement
}
```
当我们直接在`for`循环中使用`return`，会报错 `Uncaught SyntaxError: Illegal return statement`，意思是非法捕获的返回语句，原因是因为`return`只能出现在函数体内，出现在代码中的其他任何地方都会造成语法错误！
### 2，break
```javascript
for (let i = 0; i < 10; i++) {
  if ( i === 5) {
    break
  }
  console.log(i) // 0,1,2,3,4
}
```
当`i===5`时，使用`break`跳出了了当前循环，不在继续往下执行，故结果为`0,1,2,3,4`
### 3，continue
```javascript
for (let i = 0; i < 10; i++) {
  if ( i === 5) {
    continue
  }
  console.log(i) // 0,1,2,3,4,6,7,8,9
}
```
当`i===5`，使用`continue`后，不执行后续代码，但循环扔在执行，故结果为`0,1,2,3,4,6,7,8,9`。
## for in
for in 是ES5标准，遍历的是key。return break continue在其中的用法与for循环相同。
::: warning tips 
  for...in循环是为了遍历对象而设计的，并不适合遍历数组，切记！切记！切记！重要的事情说三遍！！！
:::
## map()
`map`不会改变原数组，他以`fn`函数返回值组成新的数组
### 1，return
```javascript
let arr = [1, 2, 3, 4, 5]
let newArr = arr.map((index, item) => {
  return 10
})
console.log(newArr) // [10, 10, 10, 10, 10]
console.log(arr) // [1, 2, 3, 4, 5]
```
在`map`中使用`return`，等于是把原数组重新`clone`一份，并不改变原数组，改变的是`clone`数组的对应项
### 2，break
```javascript
let arr = [1, 2, 3, 4, 5]
arr.map((index, item) => {
  if ( item === 5) {
    break
  }
  console.log(item) // Uncaught SyntaxError: Illegal break statement
})
```
`map`中无法使用`break`
### 3，continue
```javascript
let arr = [1, 2, 3, 4, 5]
arr.map((index, item) => {
  if ( item === 5) {
    continue
  }
  console.log(item) // Uncaught SyntaxError: Illegal continue statement: no surrounding iteration statement
})
```
`map`中无法使用`continue`
## filter()
`filter`返回数组中满足`filter`函数中条件的集合(不改变原数组)，return break以及continue在改方法内的用法与map()相同。
语法： 
```javascript
let arr = [1, 2, 3, 4, 5]
let result = arr.filter( currentValue =>{
  return currentValue > 4
})
console.log(result)   // [5] 只有5满足条件
// 当为map()时 返回值为 [false, false, false, false, true]
console.log(a)        // [1, 2, 3, 4, 5]
```
## forEach()
`forEach`遍历数组，不会改变原数组。
### 1，return
```javascript
let arr = [1, 2, 3, 4, 5]
let newArr = arr.forEach((index, item) => {
  return 10
})
console.log(newArr) // undefined
console.log(arr) // [1, 2, 3, 4, 5]
```
在`forEach`中使用`return`，返回值是`undefined`，故无法在其循环体内部使用`return`，但不会改变原数组。
### 2，break
```javascript
let arr = [1, 2, 3, 4, 5]
arr.forEach((index, item) => {
  if ( item === 5) {
    break
  }
  console.log(item) // Uncaught SyntaxError: Illegal break statement
})
```
`forEach`中无法使用`break`
### 3，continue
```javascript
let arr = [1, 2, 3, 4, 5]
arr.forEach((index, item) => {
  if ( item === 5) {
    continue
  }
  console.log(item) // Uncaught SyntaxError: Illegal continue statement: no surrounding iteration statement
})
```
`forEach`中无法使用`continue`
## for of
::: tip tips
  for of 语句创建一个循环来迭代可迭代的对象。在 ES6 中引入的 for of 循环，以替代 for in 和 forEach() ，并支持新的迭代协议。for of 允许你遍历 Arrays（数组）, Strings（字符串）, Maps（映射）（键值对）等可迭代的数据结构等。
:::
语法：
```javascript
for (variable of iterable) {
    // do something
}
```
`variable`：每个迭代的属性值被分配给该变量。指的是数组中的每一个item
`iterable`：一个具有可枚举属性并且可以迭代的对象。具体就是指可遍历的数据结构
### 1，return
```javascript
demo () {
  let arr = [1, 2, 3, 4, 5]
  for (let value of arr) {
    if (value === 3) {
      return value
    }
    console.log(value) // 1,2
  }
}
```
当我们在函数体内使用for of，return可以正常响应，跳出当前循环
### 2，break
```javascript
let arr = [1, 2, 3, 4, 5]
for (let value of arr) {
  if ( value === 5) {
    break
  }
  console.log(value) // 0,1,2,3,4
}
```
当`value===5`时，使用`break`跳出了了当前循环，不在继续往下执行，故结果为`1,2,3,4`
### 3，continue
```javascript
let arr = [1, 2, 3, 4, 5]
for (let value of arr) {
  if ( value === 2) {
    continue
  }
  console.log(value) // 1,3,4,5
}
```
当`value===2`，使用`continue`后，不执行后续代码，但循环扔在执行，故结果为`1,3,4,5`