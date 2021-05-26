For in 类似 prototype 查找

**查找对象的整条原型链(无论属性是否可枚举):**

因此，当你通过**各种语法**进行属性查找时**都**会查找 **[[Prototype]] 链**，直到找到属性或者

查找完整条原型链。

```javascript

var anotherObject = { a:2
};
var myObject = Object.create( anotherObject );
anotherObject.a; // 2 myObject.a; // 2
anotherObject.hasOwnProperty( "a" ); // true 
myObject.hasOwnProperty( "a" ); // false
myObject.a++; // 隐式屏蔽! anotherObject.a; // 2
myObject.a; // 3
myObject.hasOwnProperty( "a" ); // true


```

