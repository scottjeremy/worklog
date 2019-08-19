### 老生常谈之TypeScript（一）基础类型

写这系列就是想系统地再学一遍TypeScript

#### TypeScript 基础类型

##### 数字类型： number

双精度64位浮点值。它可以用来表示整数和分数。

```typescript
let binaryLiteral: number = 0b1010; // 二进制
let octalLiteral: number = 0o744;    // 八进制
let decLiteral: number = 6;    // 十进制
let hexLiteral: number = 0xf00d;    // 十六进制
```

##### 字符串类型： string

一个字符系列，支持模板字符串

```typescript
let name: string = "Scott";
let age: number = 24;
let words: string = `Hello， my name is ${name}. I'm ${age} year old`;
```

##### 布尔类型： boolean

表示逻辑值： true 和 fale。

```typescript
let isDone: boolean = true;
```

##### 数组类型： Array

声明变量为数组。

```typescript
// 在元素类型后面加上[]
let arr: number[] = [1, 2];

// 或者使用数组泛型
let arr: Array<number> = [1, 2];
```

##### 元组： 无

元组类型用来表示已知元素数量和类型的数组，各元素的类型不必相同，对应位置的类型需要相同。

```typescript
let x: [string, number];
x = ['Scott', 24]; // 运行正常
x = [24, 'Scott']; // 报错
console.log(x[0]); // 输出 Scott
```

##### 枚举类型： enum

枚举类型用户定义数值集合。

```typescript
enum Color {
    Red,
    Green,
    Blue
}
let c: Color = Color.Blue; // 获取枚举值
console.log(c); // 输出 2

// 我们还可以改变枚举的起始编号、更改每个枚举的值、根据枚举值反获取名字
enum Color {
    Red = 1,
    Green,
    Blue
}
let colorName: string = Color[2];
console.log(colorName); // 输出 Green
```

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

#### any类型: any

任意值是 `TypeScript` 针对编程时类型不明确的变量使用的一种数据类型, 它常用于以下三种情况.

1.变量的值会动态改变时, 比如来自用户的输入, 任意值类型可以让这些变量跳过编译阶段的类型检查, 实例代码如下:

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

3.定义存储各种类型数据的数组时，示例代码：

```typescript
let arrayList: any[] = [1, false, 'fine'];
arrayList[1] = 100; // 不会报错，因编译器不会检查
```

#### never类型: never

never是其他类型(包括 null 和 undefined)的子类型, 代表从不会出现的值。这意味着声明为never类型的变量只能被 never 类型所赋值， 在函数中它通常表现为抛出异常或无法执行到终止点（例如无限循环），示例代码：

```typescript
let x: never;
let y: number;

// 运行错误，数字类型不能转为never类型
x = 123;

// 运行正确， never类型可以赋值给never类型
x = (()=> { throw new Error("exception") })();
```

```typescript
// 返回值为never的函数可以是抛出异常的情况
function error(message: string): never {
  throw new Error(message);
}

// 返回值为never的函数可以是无法被执行到的终止点的情况
function loop(): never {
  while (true) {}
}
```
