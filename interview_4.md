# 面试 - 未知点(4)

[面试 - 未知点(1)](https://github.com/Krryxa/WORK-LEARNING/issues/26)<br>
[面试 - 未知点(2)](https://github.com/Krryxa/WORK-LEARNING/issues/35)<br>
[面试 - 未知点(3)](https://github.com/Krryxa/WORK-LEARNING/issues/37)<br>
[面试 - 未知点(4)](https://github.com/Krryxa/WORK-LEARNING/issues/39)


## 题目
1. 程序输出结果
```js
let i = 0;
var k = 0;
var j = 0;

for(;i<10,j<6;i++,j++){
  setTimeout(()=>{
    k = i+j;
  },0);
}

setTimeout(()=>{
  console.log(k);
},200);

// 输出结果 12
```
分析：明显最后的 setTimeout 最后执行，首先执行 for 循环里的代码，由于设置于了定时器为 0 ，里面的代码延迟执行，所以会等到 j++ 到 6 的时候，for 循环结束退出后执行 k = i+j; 所以是 12

2. 
实现：
 * 按照 class 从小到大排列
 * 如果 class 相同，则按照 score 从大到小排列
 * 如果 class 和 score 都相同，则按照原顺序排列

### sort 函数
简单的说，sort() 在没有参数时，返回的结果是按升序来排列的。即字符串的Unicode码位点（code point）排序。 
如果指明了参数：compareFunction(a,b) ，那么数组会按照调用该函数的返回值排序。记 a 和 b 是两个将要被比较的元素：
- 如果 compareFunction(a, b) 返回值 < 0 ，a 会被排列到 b 之前，即参数a, b的顺序保存原样；
- 如果 compareFunction(a, b) 返回值 = 0 ，a 和 b 的相对位置不变。备注： ECMAScript 标准并不保证这一行为，而且也不是所有浏览器都会遵守（例如 Mozilla 在 2003 年之前的版本）；
- 如果 compareFunction(a, b) 返回值 > 0 ，b 会被排列到 a 之前。即交换参数a, b的顺序
```js
function compare(name1, name2) {
  // 这里的参数 a, b 是比较的第一个元素 a，第二个元素 b
  return function (a, b) {
    let fir1 = a[name1];
    let sec1 = b[name1];
    if (fir1 === sec1) {
      let fir2 = a[name2];
      let sec2 = b[name2];
      if (fir2 === sec2) {
        return 0; // 表示位置不变
      } else {
        return fir2 > sec2 ? -1 : 1; // 表示从大到小排序 
      }
    } else {
      return fir1 > sec1 ? 1 : -1; // 表示从小到大排序
    }
  }
}


function sortStudents(students) {
	return students.sort(compare('class', 'score'));
}

let _students = JSON.parse(`[
  {"name":"张三","class":2,"score":64},
  {"name":"李四","class":1,"score":80},
  {"name":"王五","class":1,"score":90},
  {"name":"赵六","class":4,"score":94}]`);

let res = sortStudents(_students);
console.log(res);
```

## 真正实现用同步的方式写异步代码的是：
async await
```js
async await
function load () {
  return new Promise((resolve, reject) => {
    // 异步处理
  });
}
load().then(..);
```

## HTTP请求方法
1. get
2. post
3. head：类似于get请求，只不过返回的响应中没有具体的内容，用于获取报头
4. put：从客户端向服务器传送的数据取代指定的文档的内容
5. delete：请求服务器删除指定的页面
6. connect：HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器
7. options：允许客户端查看服务器的性能
8. trace：回显服务器收到的请求，主要用于测试或诊断