编译后
```typescript
var Color;
(function (Color) {
    Color[Color["Red"] = 0] = "Red"; // Color对象赋值的时候会返回该值
    Color[Color["Green"] = 1] = "Green";
    Color[Color["Blue"] = 2] = "Blue";
})(Color || (Color = {}));
var c = Color.Green;
var colorName = Color[2];
console.log('c:::', c); // 输出 2
console.log('colorName:::', colorName); // 输出 Blue

// 看看编译后打印出来的的Color对象
Color: {
  0: "Red",
  1: "Green",
  2: "Blue",
  Blue: 2,
  Green: 1,
  Red: 0
}
```

#### void类型: void

用于表示方法返回值的类型,表示该方法没有返回值.

```typescript
function hello(): void {
  alert("Hello Scott");
}
```

#### null类型: null

表示对象值缺失.

#### undefined类型: undefined

用于初始化变量为一个未定义的值

#### never类型: never

never是其他类型(包括 null 和 undefined)的子类型, 代表从不会出现的值

#### any类型: any

任意值是 `TypeScript` 针对编程时类型不明确的变量使用的一种数据类型, 它常用于以下三种情况.

1. 变量的值会动态改变时, 比如来自用户的输入, 任意值类型可以让这些变量跳过编译阶段的类型检查, 实例代码如下:

```typescript
let x: any = 1; // 数字类型
x = 'I am who I am'; // 字符串类型
x = false; // 布尔类型
```

2.改写现有代码时, 任意值允许在编译时可选择地包含或移除类型检查, 实例代码如下:

```typescript
let a: any = '100';
aa.toFixed(2); // 编译器不会检查 实际上程序运行会报错

let b: string = '200';
b.toFixed(2); // 编译器会检查并报错: 'toFixed' does not exist on type 'string'.
```
