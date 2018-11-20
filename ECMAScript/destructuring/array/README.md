## 数组的解构赋值(基本用法)

<br>

```
let [a, b, c] = [1, 2, 3];
a // 1
b // 2
c // 3
```
<br>

用正则表达式提取值
```
let url = "https://developer.mozilla.org/en-US/Web/JavaScript";

let parsedURL = /^(\w+)\:\/\/([^\/]+)\/(.*)$/.exec(url);
let [, protocol, fullhost, fullpath] = parsedURL;

parsedURL // ["https://developer.mozilla.org/en-US/Web/JavaScript", "https", "developer.mozilla.org", "en-US/Web/JavaScript"]

protocol // "https"
```
<br>

同时可以嵌套解构或不完全结构
```
let [a, , c] = [1, 2, 3];
a // 1
c // 3

let [head, ...tail] = [1, 2, 3, 4];
head // 1
tail // [2, 3, 4]

let [x, y, z] = ['a'];
x // 'a'
y // undefined
z //[]

let [a, [b], c] = [1, [2, 3], 4];
a // 1
b // 2
c // 4
```
<br>
同时对于Set结构，也可以用数组的解构赋值

```
let [x, y, z] = new Set(['a', 'b', 'c']);
x // 'a'
```
即只要某种数据结构具有Iterator接口，都可以使用数组形式的解构赋值。

---

## 默认值

解构赋值允许指定默认值<br>
*ES6内部使用严格相等运算符 `===` 判断一个位置是否有值，所以如果一个数组成员不严格等于undefined，默认值不会生效！*
```
let [x, y = 'b'] = ['a']; // y = 'b'

let [x, y = 'b'] = ['a', null]; // y = null

let [x, y = 'b'] = ['a', undefined]; // y = 'b'
```
>因为`null == undefined`成立，但 ~~`null === undefined`~~ 不成立

<br>
默认值可以饮用解构赋值的其他变量，但该变量必须已被声明

```
let [x = 1, y = x] = []; // y = 1
let [x = 1, y = x] = [2]; // y = 2
let [x = 1, y = x] = [1, 2]; // y = 2
let [x = y, y = 1] = []; // ReferenceError
```
>`x`用到默认值`y`时,`y`还没有声明