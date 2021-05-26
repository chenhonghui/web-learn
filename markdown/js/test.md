```javascript

var a = {
  keyName: '3',
  name:{
    first: 2,
  },
  rule:function(item, configdata) { 
   console.log(this.keyName)
	},
  changeName:function(name){
    this.name.first = name
  }
};
var c = Object.create(a);


```

https://www.javascriptc.com/

https://github.com/yygmind/blog/issues/43

Http2: https://www.javascriptc.com/books/http2-explained/

