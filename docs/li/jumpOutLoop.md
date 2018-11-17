# JS中的return，break，continue的区别
::: tip tips
  javaScript中有三种方法可以跳出循环或者终止循环，分别为`break`、`return`、`continue`。
:::
## return
::: warning tips 
  `return`语句就是用于指定函数返回的值。`return`语句只能出现在函数体内，出现在代码中的其他任何地方都会造成语法错误！
:::
```javascript
for (let i = 1;i <= 10; i++) {
　　if ( i === 6 ) {
　　　　return
　　 }
　　console.log(i)
}

// 执行结果Uncaught SyntaxError: Illegal return statement(…) 
// 意思是非法捕获的查询返回语句。
```
当执行`return`语句时，即使函数主体中还有其他语句，函数执行也会停止。
```javascript
if ( username === "" ){
  console.log('请输入用户名')
　return false
}

if (phone ==="" ){
  console.log('情输入手机号')
　return false;
}
```
在上面的例子里，当`username`为`''`时，就不会再向下执行
## break
`break` 会使得整个程序终止执行或者包含了最内层的循环或者退出一个`switch`的循环。 

由于它是用来终止循环或者跳出`switch`循环的，所以只有当它出现在这些语句时，才是合法的。 

如果一个循环的终止条件非常复杂，那么使用`break`语句来实现某些条件比用一个循环表达式来表达所有的条件容易得多。 

这里写一个`for`循环为例
```javascript
for (let i = 1; i <= 10; i++) {
　if (i === 6) {
  　break
  }
  console.log(i)
}

// 当i=6的时候，直接退出for这个循环。这个循环将不再被执行！

// 输出结果：12345

```
## continue
`continue`语句和`break`语句相似。所不同的是，它不是退出一个循环，而是开始循环的一次新迭代。
::: warning tips 
  `continue`语句只能用在`while`语句、`do/while`语句、`for`语句、或者`for/in`语句的循环体内，在其它地方使用都会引起错误！
:::
```javascript
for ( let i = 1; i <= 10; i++) {
　if( i=== 6) {
　　　continue
　}
　console.log(i)
}

// 当i=6的时候，直接跳出本次for循环。下次继续执行。

// 输出结果：1234578910 输出结果没有6。
```