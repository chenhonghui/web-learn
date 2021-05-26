****

|          |                                            |      |
| -------- | ------------------------------------------ | ---- |
| 逻辑结构 | 线性结构: 栈，队列，链表，线性表。         |      |
|          | 非线性结构 二维数组，树等。                |      |
| 储存结构 | 顺序存储、链式存储、索引存储以及散列存储。 |      |
|          |                                            |      |
|          |                                            |      |
|          |                                            |      |
|          |                                            |      |

* import es6

另外，`export`语句输出的接口，与其对应的值是**动态绑定**关系，即通过该接口，可以取到模块内部实时的值。

```javascript
export var foo = 'bar';
setTimeout(() => foo = 'baz', 500);
```

`import`命令是**编译阶段执行**的，在代码运行之前。

import是静态执行，所以**不能**使用表达式和变量，这些只有在运行时才能得到结果的语法结构。

不允许运行时改变

[ES2020提案](https://github.com/tc39/proposal-dynamic-import) 引入`import()`函数，支持**动态加载模块。**



```javascript
const main = document.querySelector('main');

import(`./section-modules/${someVariable}.js`)
  .then(module => {
    module.loadPageInto(main);
  })
  .catch(err => {
    main.textContent = err.message;
  });
```



* Rxjs

基于观察者队列实现了对异步和基础事件的编程。

**惰性求值的**特性使得 Observable 可以在它仅被需要的地方进行计算。

Subject的作用——作为单路Observable转变为多路Observable的桥梁。

特殊的`Subject` 类型 : BehaviorSubject`，`ReplaySubject`，和 `AsyncSubject 

pipe 

```javascript
pipe(...operations: OperatorFunction<any, any>[]): Observable<any> {
  if (operations.length === 0) {
    return this as any;
  }
  if (operations.length == 1) {
     return operation[0];
  }
  
  return operations.reduce((prev, fn) => fn(prev), this);
}
```



![image-20210510195136152](/Users/cindychen/Library/Application Support/typora-user-images/image-20210510195136152.png)

