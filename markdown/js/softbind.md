```javascript
if (!Function.prototype.softBind) {
  Function.prototype.softBind = function(obj) {
		var fn = this;  // foo > bound
    console.log(fn)
		// 捕获所有 curried 参数
		var curried = [].slice.call( arguments, 1 );
    
    var bound = function() {
      console.log('bound---:',this,obj) // bind 几次调几次
			return fn.apply(
				(!this || this === (window || global)) ?
				obj : this
				, curried.concat.apply( curried, arguments )
			);
		};
    // 修正 prototype
		bound.prototype = Object.create( fn.prototype );
    
    // 返回一个新函数
		return bound;
  };
}
```

```javascript
function foo() {
	console.log("name: " + this.name,arguments);
}
var obj = { name: "obj" }, obj2 = { name: "obj2" }, obj3 = { name: "obj3" };
foo.softBind(obj,1,2).softBind(obj3,3,4).softBind(obj3,3,4).softBind(obj2)(5) // name: obj3 <---- 看!

obj2.foo = foo.softBind(obj); 
obj2.foo(); // name: obj2 <---- 看!!!
setTimeout( obj2.foo, 10 );
```



硬bind

```javascript
Function.prototype.hardBind = function(obj) {
  const fn = this;
  var curried = [].slice.call( arguments, 1 );
  var bound = function() {
      console.log('bound---:',this,obj,arguments) // bind 几次调几次
			return fn.apply(obj, curried.concat.apply( curried, 										 arguments ));
	};
	return bound;
}
function foo() {
	console.log("name: " + this.name,arguments);
}
foo.hardBind(obj,1,2)     // retun bound1 

												 // bound1闭包, fn.apply(obj); fn = foo

   .hardBind(obj2)       // bound1.hardBind(obj2) -> bound2;

												 // bound2闭包, fn.apply(obj2); fn=bound1;
	 (5)                  // bound2(5) 执行

//  bound2(5) -> bound1.apply(obj2) -> foo.apply(obj)

// name: obj 
```

