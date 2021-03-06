JS重点关注：作用域，变量提升，闭包，this，原型，继承，ES6等

### ES6有什么内容？ES7？ES8？

ES6：

- let和const，块级作用域，不会变量提升
- 解构，箭头函数（无this，this是定义时所在的对象，不能做构造函数）
- 模板字符串
- Object.assign（浅拷贝，所有可枚举）
- 原始数据类型Symbol（Symbol值都是唯一的）
- Set（类似数组，成员的值都是唯一的）、Map（类似对象，‘键’可以是各种类型的值）数据解构，WeakSet（类似Set，成员都是对象，弱引用），WeakMap（类似Map，只接受对象作为键名（null除外），WeakMap的键名所指向的对象，不计入垃圾回收机制）
- Promise（三种状态：pending（进行中）、fulfilled（已成功）和rejected（已失败））
- Class（类）（有静态属性，没有静态方法，不存在变量提升，extends继承，super（子类没有自己的this，必须在constructor中调用super方法））
- 模块（export、import；CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用）
- ...

ES7：

- 求幂运算符（**）(效果同Math.pow(3, 2)   // 9)
- Array.prototype.includes()

ES8：

- 异步函数(Async functions)
- Decorator修饰器
- Object.entries()和Object.values()
- padStart和padEnd
- Object.getOwnPropertyDescriptors()
- 函数参数列表与调用中的尾部逗号
- 共享内存和原子

### let，const，var有什么区别？

1. var定义的变量没有块级作用域，会出现变量提升，相同作用域内可以重复声明
2. let和const是ES6引入，块级作用域，不会出现变量提升（声明之前就使用这些变量会报错，“暂时性死区”），相同作用域内不能重复声明
3. const声明创建一个只读的常量（引用类型的引用地址不变，值可以改变），声明就必须立即初始化

### JavaScript 中不同类型以及不同环境下变量的内存都是何时释放?

引用类型是在没有引用之后, 通过 v8 的 GC 自动回收, 值类型如果是处于闭包的情况下, 要等闭包没有引用才会被 GC 回收, 非闭包的情况下等待 v8 的新生代 (new space) 切换的时候回收.

### 箭头函数 与 function 的区别？

箭头函数：

- 函数体内的`this`对象，就是定义时所在的对象，而不是使用时所在的对象。
- 不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。
- 不可以使用`arguments`对象，该对象在函数体内不存在。如果要用，可以用 `rest` 参数代替。
- 不可以使用`yield`命令，因此箭头函数不能用作 `Generator` 函数

> 箭头函数this指向的固定化，并不是因为箭头函数内部有绑定this的机制，实际原因是箭头函数根本没有自己的this，导致内部的this就是外层代码块的this。正是因为它没有this，所以也就不能用作构造函数。

### 什么是闭包？闭包应用的场景？

闭包是指有权访问另一个函数作用域中的变量的函数。

主要场景是：

- 模拟私有成员
- 函数的柯里化
- 单例模式
- ...

另外，闭包不一定会造成内存泄漏，大多数情况可能是因为循环引用

### new 关键字做了什么？

1. 创建一个新的对象，这个对象的类型是 object；
2. 设置这个新的对象的内部、可访问性和[[prototype]]属性为构造函数（指prototype.construtor所指向的构造函数）中设置的；
3. 执行构造函数，当this关键字被提及的时候，使用新创建的对象的属性； 返回新创建的对象（除非构造方法中返回的是‘无原型’）。
4. 在创建新对象成功之后，如果调用一个新对象没有的属性的时候，JavaScript 会延原型链向止逐层查找对应的内容。这类似于传统的‘类继承’。

> 注意：在第二点中所说的有关[[prototype]]属性，只有在一个对象被创建的时候起作用，比如使用 new 关键字、使用 Object.create 、基于字面意义的（函数默认为 Function.prototype ，数字默认为 Number.prototype 等）。它只能被Object.getPrototypeOf(someObject) 所读取。没有其他任何方式来设置或读取这个值。

### null和undefined的区别

null是一个表示"无"的对象，转为数值时为0；undefined是一个表示"无"的原始值，转为数值时为NaN。

当声明的变量还未被初始化时，变量的默认值为undefined。 null用来表示尚未存在的对象，常用来表示函数企图返回一个不存在的对象。

undefined表示"缺少值"，就是此处应该有一个值，但是还没有定义。典型用法是：

- 变量被声明了，但没有赋值时，就等于undefined。
- 调用函数时，应该提供的参数没有提供，该参数等于undefined。
- 对象没有赋值的属性，该属性的值为undefined。
- 函数没有返回值时，默认返回undefined。

null表示"没有对象"，即该处不应该有值。典型用法是：

- 作为函数的参数，表示该函数的参数不是对象。
- 作为对象原型链的终点

### 变量怎么存储？

- 基本类型有Undefined、Null、Boolean、Number、String、Symbol，这些类型在内存中分别占有固定大小的空间，它们存储在栈内存中
- 引用类型，值大小不固定，保存在堆内存中的，然后在栈内存中保存一个对堆内存中实际对象的引用

为什么基础数据类型存在栈中，而引用数据类型存在堆中呢?

- 堆比栈大，栈比堆速度快。
- 基础数据类型比较稳定，而且相对来说占用的内存小。
- 引用数据类型大小是动态的，而且是无限的。
- 堆内存是无序存储，可以根据引用直接获取。

### js延迟加载的方式有哪些？

- defer和async
- 动态创建DOM方式（创建script，插入到DOM中，加载完毕后callBack）
- 按需异步载入js

### `<script>`标签defer与async的区别

- defer要等到整个页面在内存中正常渲染结束（DOM 结构完全生成，以及其他脚本执行完成），才会执行；
- async一旦下载完，渲染引擎就会中断渲染，执行这个脚本以后，再继续渲染。

defer是“渲染完再执行”，async是“下载完就执行”。另外，如果有多个defer脚本，会按照它们在页面出现的顺序加载，而多个async脚本是不能保证加载顺序的

### javascript对象的几种创建方式

- 工厂模式
- 构造函数模式
- 原型模式
- 混合构造函数和原型模式
- 动态原型模式
- 寄生构造函数模式
- 稳妥构造函数模式

### javascript怎么实现继承

- 原型链继承
- 借用构造函数继承
- 组合继承(原型+借用构造)
- 原型式继承
- 寄生式继承
- 寄生组合式继承

### CommonJS 中的 require/exports 和 ES6 中的 import/export 区别？

- CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用
- CommonJS 模块是运行时加载，ES6 模块是编译时输出接口
- CommonJS 模块一旦出现某个模块被"循环加载"，就只输出已经执行的部分，还未执行的部分不会输出;ES6 模块是动态引用，如果使用import从一个模块加载变量（即import foo from 'foo'），那些变量不会被缓存，而是成为一个指向被加载模块的引用，需要开发者自己保证，真正取值的时候能够取到值。

第二个差异是因为 CommonJS 加载的是一个对象（即module.exports属性），该对象只有在脚本运行完才会生成。而 ES6 模块不是对象，它的对外接口只是一种静态定义，在代码静态解析阶段就会生成

### 什么是 "use strict"; ? 使用它的好处和坏处分别是什么？

- 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;
- 消除代码运行的一些不安全之处，保证代码运行的安全；
- 提高编译器效率，增加运行速度；
- 为未来新版本的Javascript做好铺垫。

### jquery.extend 与 jquery.fn.extend的区别？

- jquery.extend 为jquery类添加类方法，可以理解为添加静态方法
- jquery.fn.extend源码中jquery.fn = jquery.prototype，所以对jquery.fn的扩展，就是为jquery类添加成员函数

使用：jquery.extend扩展，需要通过jquery类来调用，而jquery.fn.extend扩展，所有jquery实例都可以直接调用

### 如何判断当前脚本运行在浏览器还是node环境中？（阿里）

this === window ? 'browser' : 'node';通过判断Global对象是否为window，如果不为window，当前脚本没有运行在浏览器中


