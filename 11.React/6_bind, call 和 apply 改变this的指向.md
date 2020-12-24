6.bind, call 和 apply 改变this的指向  
20201201

```
let obj = {
    x : 12345
}

function display(a, b){
    console.log(this.x + " " + a + " " + b)
}

//bind会改变方法(display)中this的指向，到传入的参数(obj), 不会立即执行
//第一个参数后的参数，会作为方法的参数
//bind有返回值，返回被改变this指向后的函数的引用
//注意：bind不会修改原函数的this指向
// let displayMethod = display.bind(obj , 1 , 2);
// displayMethod();

//call也会改变方法(display)中this的指向，到传入的参数(obj)，但会立即执行
//第一个参数后的参数，会作为方法的参数
//call没有返回值
// display.call(obj , 11 , 22)

//apply也会改变方法(display)中this的指向，到传入的参数(obj)，但会立即执行
//第一个参数后的参数，会作为方法的参数，但必须是数组的形式
//apply没有返回值
// display.apply(obj , [ 111 , 222 ])
```