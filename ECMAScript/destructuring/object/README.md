## 对象的解构赋值

<br>

解构不仅可以用于数组，还可以用于对象
```
let { foo, bar } = { foo: 'aaa', bar: 'bbb' };
foo //'aaa'
bar //'bbb'
```
<br>

对象的解构不同于数组的在于：数组按次序排列，变量的取值由位置决定；对象的取值没有次序，变量必须与属性同名才能取到争取的值。
```
let { idiot } = { foo: 'aaa', bar: 'bbb' };
idiot // undefined
```
<br>

对象的解构赋值内部机制，是先找到同名属性，再赋给对应的变量。真正被赋值的是后者，而不是前者。同时对象的结构复制也可以用于嵌套结构的对象。
```
let { foo: baz } = { foo: 'aaa', bar: 'bbb' };
baz // 'aaa'
foo // ReferenceError

let obj = {
    p: [
        'Hello',
        { y: 'World' }
    ]
};
let { p: [x, { y }] } = obj;
x // 'Hello'
y // 'World'

let node = {
    loc: {
        start: {
            line: 1,
            column: 5
        }
    }
};
let { loc, loc: { start }, loc: { start: { line } } } = node;
line // 1
start // Object { line: 1, column: 5 }
loc // Object { start: Object }
```
>上方最后一个例子中一共进行了对`loc`,`start`,`line`对三次解构赋值。需要注意在最后一次对line的解构赋值中，只有`line`是变量，`loc`和`start`都是模式。同样对象的解构也可以指定默认值。

<br>

对象的解构赋值可以很方便地讲现有对象的方法赋值到某个变量
```
let { log, sin, cos } = Math;
// 将Math的对数、正弦、余弦三个方法赋到对应的变量上方便使用
```

由于数组本质是特殊的对象，所以可以对数组使用对象的解构赋值
```
let arr = [1, 2, 3];
let { 0: first, [arr.length - 1]: last } = arr;
first // 1
last // 3
```

对象的解构赋值也可以指定默认值
```
let { message: msg = 'Something went wrong' } = {};
msg // 'Something went wrong'
```
>默认值的生效条件同样是，对象的属性值 `===` 严格等于 `undefined`