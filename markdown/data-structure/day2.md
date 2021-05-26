* Rxjs

```js
// RxJS v6+
import { withLatestFrom, map } from 'rxjs/operators';
import { interval } from 'rxjs';

// 每5秒发出值
const source = interval(5000);
// 每1秒发出值
const secondSource = interval(1000);
const example = source.pipe(
  withLatestFrom(secondSource),
  map(([first, second]) => {
    return `First Source (5s): ${first} Second Source (1s): ${second}`;
  })
);
/*
  输出:
  "First Source (5s): 0 Second Source (1s): 4"
  "First Source (5s): 1 Second Source (1s): 9"
  "First Source (5s): 2 Second Source (1s): 14"
  ...
*/
const subscribe = example.subscribe(val => console.log(val));

```

```js
var worklist = [];
var isWorking = false;
var bTime = 1000;
var index = 0;
function buffertime(fn){
  index++;
  if(!isWorking){
    isWorking = true;
    fn();
    setTimeout(loopWork,bTime);
  }else{
    worklist.unshift(fn);
  }
}
function loopWork(){
   isWorking = false;
   if(!worklist.length) return;
    var cur = worklist.pop();
    buffertime(cur);
}

function fn1(param){
  console.log(param)
}
buffertime(()=>{
   fn1(1)
});// 马上执行
buffertime(()=>{
   fn1(2)
});// 2秒后执行
buffertime(()=>{
   fn1(3)
});// 4秒后执行
buffertime(()=>{
   fn1(4)
});// 4秒后执行

```

