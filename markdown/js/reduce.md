Reduce

reduce  

第一个参数传迭代函数 ，第二个为初始化的res；

返回 ：res为**初始化的第二个参数**，可更改；**cur 为当前迭代的item**；

1. 判断每个字母出现的次数

```javascript
var arrString = 'abcdaabc';

arrString.split('').reduce(function(res, cur) {
  console.log(res,cur)
    res[cur] ? res[cur] ++ : res[cur] = 1
    return res;
}, {})

> {a: 3, b: 2, c: 2, d: 1}
```

2. 取对象里面指定的keys

```javascript
var only = function(obj, keys){
  obj = obj || {};
  if ('string' == typeof keys) keys = keys.split(/ +/);
  return keys.reduce(function(ret, key){
    if (null == obj[key]) return ret;
    ret[key] = obj[key];
    return ret;
  }, {});
};
```


3. 多维度计算

```javascript
var reducers = {  
  totalInEuros : function(state, item) {
    return state.euros += item.price * 0.897424392;
  },
  totalInYen : function(state, item) {
    return state.yens += item.price * 113.852;
  }
};

var manageReducers = function(reducers) {
  return function(state, item) {
    // state 需要更新的initialState
    // item  每次迭代的items；
    // ['totalInEuros','totalInYen']，每次迭代item，
    // 返回 新的state
    return Object.keys(reducers).reduce(
      function(nextState, key) {
        // 执行更新函数：totalInEuros，totalInYen
        // 传入item,更新state的euros && yens
        reducers[key](state, item);
        // 返回state
        return state;
      },
      {} // 传{}和传state一样
    );
  }
};

var bigTotalPriceReducer = manageReducers(reducers);
var initialState = {euros:0, yens: 0};
var items = [{price: 10}, {price: 120}, {price: 1000}];
var totals = items.reduce(bigTotalPriceReducer, initialState);
console.log(totals);
// {euros: 1014.08956296, yens: 128652.76}
// {euros: 1014.08956296, yens: 128652.76}
```



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




