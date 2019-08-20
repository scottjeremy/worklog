# 老生常谈之TypeScript（二）接口

接口是一系列抽象方法的声明，是一些方法特征的集合，这些方法都应该是抽象的，需要由具体的类去实现，然后第三方就可以通过这组抽象方法调用，让具体的类执行具体的方法。

## 基本例子

```typescript
// 定义一个接口 IPersion
interface IPersion {
    name: string;
    sayHi: () => string;
}

// 定义一个变量 customer 它的类型是 IPersion
const cunstomer: IPersion = {
    name: "Scott Jeremy",
    sayHi: (): string => "Hi!";
}
```

## 可选参数

```typescript
interface IPersion {
    name: string;
    age?: number;
    sayHi: () => string;
}

// age 为可选属性， 在声明时可不赋值
const cunstomer: IPersion = {
    name: "Scott Jeremy",
    sayHi: (): string => "Hi!";
}

function logAge(cunstomer: IPersion) {
    console.log(cunstomer.age); // 编译器会报错 提示 age 值可能为 undefined
    if (cunstomer.age) {
        console.log(cunstomer.age); // 编译器就不会报错
    }
};

// 执行一个函数，输出 age 值
logAge(cunstomer);
```

## 只读参数

```typescript
// 定义一个接口 IPersion
interface IPersion {
    readonly name: string;
}

// 定义一个变量 customer 它的类型是 IPersion
let cunstomer: IPersion = {
    name: "Scott Jeremy",
}

cunstomer.name = 'Scott'; // 编译器会报错 提示该属性状态为只读
```

## 函数接口

```typescript
interface ISearchFunc {
    (source: string, subString: string): boolean;
}

let mySearch: ISearchFunc;

mySearch = function(src: string, sub: string) {
    let result = src.search(sub);
    // 如果return result 编译器会报错 因返回值不是boolean
    return result > -1;
}

```

## 类接口

```typescript
// 实例接口
interface IClockInterface {
    setTime(d: Date);
}

// 构造器接口
interface IClockConstructor {
    new(hour: number, minute: number): IClockInterface;
}
```

## 继承接口

```typescript
interface IName {
    name: string;
}

interface IAge {
    age: number;
}

// IPerson 里就会有 name 和 age
interface IPerson extends IName, IAge {
    sayHi: (): string => "Hi!";
}
```
