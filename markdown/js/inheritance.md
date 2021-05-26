

###  寄生继承 

已经继承了的实例，不再改变父类改变；

实例可以从写，不影响父类；

```javascript
//“传统的 JavaScript 类”Vehicle 
function Vehicle() {
	this.engines = 1;
}
Vehicle.prototype.ignition = function() { 
  console.log( "Turning on my engine." );
};
Vehicle.prototype.drive = function() {
	this.ignition();
	console.log( "Steering and moving forward!" );
};
//“寄生类”Car 
function Car() {
	// 首先，car 是一个 Vehicle 
  var car = new Vehicle();
  this.wheels = 3;
	// 接着我们对 car 进行定制
  car.wheels = 4;
	// 保存到 Vehicle::drive() 的特殊引用
  var vehDrive = car.drive;  // 得到对象引用地址
  var ignition = car.ignition; // 得到对象引用地址
  // 拿到drive函数地址，并保存
  
	// 重写 Vehicle::drive()， 脱离原型
  car.drive = function() {
		vehDrive.call( this );
    ignition();
  	console.log(
		"Rolling on all " + this.wheels + " wheels!" );
  }
	return car;
}
var myCar = new Car();
myCar.drive();

//Turning on my engine.
//VM39038:10 Steering and moving forward!
//VM39038:23 Rolling on all 4 wheels!

// Vehicle.prototype.drive指向新的地址；
Vehicle.prototype.drive = function() {
	this.ignition();
	console.log( "Steering and moving forward!222" );
};
myCar.drive(); // not change
var myCar2 = new Car();
myCar2.drive();
```

New 得到的实例随类改变 **单向改变**

```js
var myVe = new Vehicle();
myVe.drive(); // no change
Vehicle.prototype.drive = function() {
	this.ignition();
	console.log( "Steering and moving forward!22" );
};
myVe.drive(); // change
var myVe2 = new Vehicle();

myVe2.drive = function(){
	console.log('new')
}

Vehicle.prototype.drive = function() {
	this.ignition();
	console.log( "S" );
};
// myVe2 与 Vehicle 脱离
myVe2.drive(); // nochange

```



### 隐式混入

```js
var Something = { 
  	cool: function() {
      this.greeting = "Hello World";
      this.count = this.count ? this.count + 1 : 1;
    }
};
Something.cool();
Something.greeting; // "Hello World" Something.count; // 1
var Another = {
  cool: function() {
    // 隐式把 Something 混入 Another
    Something.cool.call( this );
  }
};
Another.cool();
Another.greeting; // "Hello World" Another.count; // 1(count 不是共享状态)
```

### 原型继承

**子类型的原型为父类型的一个实例对象。**

```javascript
//父类型
function Person(name, age) {
   this.name = name,
   this.age = age,
   this.play = [1, 2, 3]
   this.setName = function () { }
}
Person.prototype.setAge = function () { }
//子类型
function Student(price) {
   this.price = price
   this.setScore = function () { }
}
Student.prototype = new Person() // 子类型的原型为父类型的一个实例对象
var s1 = new Student(15000)
var s2 = new Student(14000)
console.log(s1,s2)
```

**缺点**：

- 无法实现多继承
- 来自原型对象的所有属性被所有实例共享
- 创建子类实例时，无法向父类构造函数传参
- 要想为子类新增属性和方法，必须要在`Student.prototype = new Person()` 之后执行，不能放到构造器中

### 构造函数模式

