# Const

<br>

`const`声明一个只读的常量。一旦声明，常量的值将不能被改变。<br>
```
const PI = 3.1415;
PI //3.1415
PI = 3; //TypeError: Assignment to constant variable.
```
`const`实际上保证的，并不是变量的值不得改动，而是变量指向的内存地址不得改动。对于简单的数据类型(如 `Number`,`String`,`Boolean`)，值保存在变量指向的内存地址，因此等同于常量。但对于复合类型的数据(如 `Object`,`Array`)，`const`只能保证指针的固定，至于数据结构是否变化是不可控制的。
```
const foo = {};
// 为foo添加一个属性
foo.prop = 7;
foo.prop //7

const a = [];
a.push('Angela'); //right
a.length = 0; //right
a = ['Louis']; //wrong
```
故如果想要将对象冻结，可以使用`Object.freeze()`方法。
```
const foo = Object.freeze({});
// 常规模式时，下一行不起作用
// 严格模式时，下一行将会报错
foo.prop = 7;
```