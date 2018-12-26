# 类

ECMAScript 2015 中引入的 Javascript 类本质上是 JavaScript 现有的基于原型的继承的语法糖。类语法不会为 JavaScript 引入新的面向对象的继承模型。

----

## 定义类

类实际上是个“特殊的函数”，就像定义的函数表达式和函数声明一样，类语法有两个组成部分：类声明和类表达式。

### 类声明

定义一个类的一种方法是使用一个类声明，要声明一个类，可以使用带有 class 关键字的类名。

```js
class Rectangle {
    constructor(height, width) {
        this.height = height;
        this.width = width;
    }
}
```

#### 提升

函数声明和类声明之间有一个重要区别就是函数声明会提升，类声明不会。首先需要声明类，然后访问它，否则像下面的代码会抛出一个 ReferenceError:

```js
let p = new Rectangle();
// ReferenceError

class Rectangle {}
```

### 类表达式

一个 类表达式 是定义一个类的另一种方式。类表达式可以是被命名或匿名的。赋予一个命名类表达式的名称是类的主体的本地名称。

```js
/* 匿名类 */
let Rectangle = class {
    constructor(height, width) {
        this.height = height;
        this.width = width;
    }
};

/* 命名的类 */
let Rectangle = class Rectangle {
    constructor(height, width) {
        this.height = height;
        this.width = width;
    }
}
```

注意： 类表达式也同样受到类声明中提到的提升问题的困扰

----

## 类体和方法定义

一个类的雷体是一对花括号/大括号 {} 中的部分。这是定义类成员的位置，如方法或构造函数。

### 严格模式

类声明和类表达式的主体都执行在严格模式下。比如，构造函数，静态方法，原型方法，getter 和 setter 都在严格模式下执行。

### 构造函数

constructor 方法是一个特殊的方法，其用于创建和初始化使用 class 创建一个对象。一个类只能拥有一个名为 "constructor" 的特殊方法。如果类包含多个 constructor 的方法，则将抛出一个 SyncaxError。

一个构造函数可以使用 super 关键字来调用一个父类的构造函数。

----

### 原型方法

```js
class Revtangle {
    // constructor
    constructor(height, width) {
        this.height = height;
        this.width = width;
    }
    // Getter
    get area() {
        return this.calcArea()
    }
    // Method
    calcArea() {
        return this.height * this.width;
    }
}
const square = new Rectangle(10, 10);

console.log(square.area);
// 100
```

### 静态方法

static 关键字用来定义一个类的一个静态方法。调用静态方法不需要实例化该类，但不能通过一个类的实例调用静态方法。静态方法通常用于为一个应用程序创建工具函数。

```js
class Point {
    constructor(x, y) {
        this.x = x;
        this.y = y;
    }

    static distance(a, b) {
        const dx = a.x - b.x;
        const dy = a.y - b.y;

        return Math.hypot(dx, dy)
    }
}

const p1 = new Point(5, 5);
const p2 = new Point(10, 10);

console.log(Point.distance(p1, p2));
```

### 用原型和静态方法包装

当一个对象调用静态或原型方法时，如果该对象没有"this"

(https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Classes)[https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Classes]