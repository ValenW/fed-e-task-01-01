# 王文茏｜Part 1｜模块一

## 简答题

### 第一题

结果为10。`a[6]()`执行时：

1. 执行`console.log(i)`
   1. function内部未定义i，往上层定义域找
   2. 找到for循环中定义了i，此时for循环结束，`i = 10`
   3. 执行`console.log`，输出i

### 第二题

会报错。简单来说let定义的变量不能在定义前使用。

`if (true) {...}`内部形成一个块，块中的`let tmp`会将tmp的定义提升，覆盖外部定义的`tmp`，故`console.log(tmp)`中的tmp指向的是块内部的tmp。又let不会将变量的初始化提升，故此时的tmp还未初始化，故报错

### 第三题

`arr.reduce((acc, cur) => cur < acc ? cur : acc, arr[0])`

### 第四题

const和let区别在于const定义的变量必须初始化，并且初始化后不能进行赋值操作，其他和let没区别

let和var区别在于

1. 在块中的let声明变量会绑定到块作用域中，而var会提升到外层的函数作用域或全局作用域
2. let变量必须在声明之后才能使用，var没有这个限制
3. let不允许重复声明，var可以

### 第五题

输出20。箭头函数的this是从作用域链的上一层继承的。

具体到题目，箭头函数被定义在obj.fn内，上层定义域为fn的函数定义域。

又fn是通过`obj.fn`的形式调用，调用时fn内的this指向obj对象。

故箭头函数的this指向obj对象，`this.a => obj.a`，故输出20

### 第六题

Symbol可用于Object的key，每次创建都是全新的symbol。

适合定义一些需要保证唯一性的属性，相比较于string类型，symbol可以避免冲突。

### 第七题

浅拷贝就是只管复制值。如果拷贝的是object，就是只拷贝了对象的地址，指向的还是同一个对象。这样更改复制的对象会同时影响到源对象。

深拷贝就是真正的全部复制，会产生一份和源对象一样的新对象，这样对复制对象的更改就不会影响到源对象

### 第八题

js异步编程是为了在单线程的环境下避免耗时任务阻塞程序运行而引入的程序运行模式。

Event Loop是js的程序运行调度机制。js运行过程中会调用各种外部API，通常是异步的，即调用后不等返回就继续执行下句js代码。而等外部api执行完毕，就会往js的事件队列中push相应的事件等待回调。

每当js的执行栈清空后就会从事件队列中先进先出地取出一个事件执行回调。

这样不断清空执行栈和从事件队列pop事件回调放入执行栈的循环，就是Event Loop

宏任务包括一般script代码，setTimeout等，微任务包括Promise，MutationObserver，process.nextTick等。

在当前宏任务执行完毕后，event loop会不断寻找等待执行的微任务并将其放入执行栈执行，直到没有等待执行的微任务。之后才会寻找等待执行的宏任务并入栈执行，这样不断循环。

可以理解为宏任务和微任务是优先级队列，微任务优先级高，只有微任务清空后才会执行宏任务

### 第九题

```js
function delay(fn, time) {
    return new Promise(resolve => {
        setTimeout(() => resolve(fn()), time)
    })
}

delay(() => 'hello', 10)
    .then(res => delay(() => res + 'lagou', 10))
    .then(res => delay(() => res + 'I ❤ U', 10))
    .then(console.log)
```

### 第十题

JavaScript是一门动态类型的编程语言。

TypeScript是JavaScript的超集，通过在JavaScript基础上增加新语法的形式，给JavaScript添加了类型系统，接口等，将其从动态语言变成了静态语言，从而更好支持类型检查，智能提示，接口定义等功能，方便了程序开发。其本质是一套生成JavaScript代码的语法，最终要通过tsc编译成JavaScript代码运行。

### 第十一题

TypeScript优点在于：

1. 静态类型，支持静态类型检查，代码智能提示，方便代码重构
2. 接口定义，方便类型判断
3. 是JavaScript超集，支持所有ECMAScript标准语法，在执行环境没有支持的情况下方便使用上最新的ECMAScript语法

缺点在于

1. 额外学习成本，需要学习TypeScript自身的语法规则
2. 额外的复杂度，比如需要配置文件，需要一次编译才能执行，不能直接贴到console上执行
3. 使用的框架，库等未必支持TypeScript，或者支持得不好，需要做些额外的工作



