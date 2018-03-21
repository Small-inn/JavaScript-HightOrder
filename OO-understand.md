## js面相对象基础知识
![这就是面向对象编程](https://github.com/Small-inn/JavaScript-HightOrder/blob/master/img/oo.JPEG)

## js的基本数据类型(五种)
> number string boolean undefined null (symbol es6中提出的)
## js的数据类型
> Number String Boolean Undefined Object(null是一种空指针，指向一个空对象) Function 

## 内置对象属性与方法
>> 属性：与对象相关的值
>> 方法：能够在对象上执行的动作
1. Array
    - 属性：
        - length：设置或者返回数组中元素的数目
    - 方法：
        - concat(): 连接两个或者更多的数组，并返回结果
        - join()：把数组的所有元素放入一个字符串，通过指定的分隔符进行分隔
        - pop()：删除并返回数组的最后一个元素
        - push()：向数组的末尾添加一个或者更多元素，返回新的长度
        - reserse()：颠倒数组中元素的顺序
        - shift()：删除并返回数组的第一个元素
        - slice()：从某个已有的数组返回选定的元素
        - sort()：对数组的元素进行排序
        - splice()：删除元素，并向数组添加新的元素
        - unshift()：向数组的开头添加一个或者更多元素，并返回新的长度
2. Date
    - 不说了，太长了
3. Number
    - 属性：
         - MAX_VALUE：可表示的最大的数
         - MIN_VALUE：可表示的最小的数
         - NAN：非数字
         - NEGATIVE_INFINITY：负无穷大，溢出时返回该值
         - POSITIVE_INFINITY：正无穷大，溢出时返回该值
    - 方法：
         - toString() 把数字转化成字符串，使用指定的基数
         - toFixed()：把数字转化成字符串，结果的小数点后又指定位数的数字
         - toExponential()：把对象的值转化为指数计数法
         - toPrecision()：把数字格式化为指定的长度
         - valueOf()：返回一个Number对象的基本数字值
4. Boolean
    - 方法：
         - toString()：把逻辑值转化为字符串，并返回结果
         - valueOf()：返回Boolean对象的原始值
5. String
    - 属性和方法：更长就不写了
6. Math
    - 属性和方法：一般不常用，常用的掌握就行了
## 值类型和引用类型
* 值类型(基本数据类型)：number boolean undefined null string 值类型直接存储在变量访问的位置
* 引用类型(复杂数据类型)：对象 数组 函数 存储变量处的值是一个指针，指向存储对象的内存处

> eg: 
```
1.
function foo(num){
    num++ 
} 
var a = 1;
foo(a);
console.log(a);// 1

2.
function fn(o){
    o.age++;
}
var p = {name:"张三",age: 19};
foo(p);
console.log(p.age);//20

```
<p>
  函数调用的过程其实就是实参给形参赋值的过程，当参数为值类型，函数内外的两个变量完全不同，仅仅是存的值一样而已，修改时互不影响，当参数为引用类型时，函数内外的两个变量不同，但是共同指向同一个对象，在函数内部修改对象数据会影响外部
</p>

```
        //面试题
        function upgrade(p){
            //p=p1 隐式操作

            p = {
                name:"白富美"
            }

            p.name = "矮穷丑";
        }

        var p1 = {
            name:"高富帅"
        }

        upgrade(p1);

        console.log(p1.name);
```

![图解](https://github.com/Small-inn/JavaScript-HightOrder/blob/master/img/%E7%B1%BB%E5%9E%8B%E8%B5%8B%E5%80%BC%E9%9D%A2%E8%AF%95%E9%A2%98.png)

## 对象的动态特性
>> 对象创建好之后，可以随时为对象新增成员(属性和方法)，这就是对象的动态特性。
>> 访问对象属性以及成员的方式：1.点语法 2.关联数组语法
```
eg:
var obj = {};
obj.name = 'hh';
//点语法
obj.name
//关联数组语法
obj['name'] //注意这里属性名一定要是字符串
``` 
## ==与===区别
> == 判断值是否相等， === 判断类型和值是否相等
```
console.log({} == {})// 对象在内存中创建的地址不一样的 所以为false
console.log({} === {})

console.log([] == ![])
console.log([].valueOf())// []
console.log([].toString())// ''
console.log(Boolean(''))// false
//1.首先调用数组的valueOf方法，获取返回值，看看能不能继续参与运算，不能参与运算
//2.调用数组的toString方法，再把返回值转换成布尔类型
//3.在进行判断


console.log({} == !{})
console.log({}.valueOf())// [object object]
console.log([object object].toString())// [object object]
console.log(Boolean([object object]))// true
//1.首先调用数组的valueOf方法，获取返回值，看看能不能继续参与运算，不能参与运算
//2.调用数组的toString方法，再把返回值转换成布尔类型
//3.在进行判断
```
## 构造函数
>> 构造函数：在JavaScript中，构造函数是给对象添加属性，初始化属性用的
>> 使用构造函数创建对象的过程：
1. 首先使用new关键字创建对象，类似于使用{}，这个时候创建出来的对象是一个没有任何成员你的对象，这里要注意一下：
    - 使用new关键字创建的对象，对象的类型是就是这个对象使用的构造函数逇函数名
    - 使用{}创建对象，对象的类型一定是Object，相当于使用了new Object()
2. 使用构造函数为其初始化成员
    - 在构造函数调用开始的时候，就有一个赋值操作，就是让this = 刚创建出来的对象
    - 在构造函数里，this就是代表刚创建出来的对象
3. 在构造函数中，利用对象的动态特性，为对象添加成员
>> 传统构造函数存在的问题：new 出来的对象里面的方法，每次创建新对象，构造函数的方法也要被创建一次，浪费资源。
## 面向对象的特点
1. 封装性：
    对象就是将数据与功能组合一起，就是封装
    1. js对象就是键值对的集合
       - 键值如果是数据(基本数据、复合数据、空数据)，称为属性
       - 键值如果是函数，称为方法
    2.对象就是将属性与方法封装起来
    3.方法就是将过程封装起来
2. 继承性
```
//本题主要考混入继承，手动实现Object.assign()方法

function extend() {
    var target,
        arg = arguments;
    if (arg.length >= 2) {
        target = arg[0];
        for (var i = 0; i < arg.length; i++) {
            for (var k in arg[i]) {
                target[k] = arg[i][k]
            }
        }
    }
    return target

}
```
>> 当前对象可以使用其他对象的属性和方法
3. 多态性（基于强类型）
    js中没有多态，父类指针指向子类对象
## 原型
* 每一个函数被创建的时候，都有一个跟它关联的对象创建出来
* 每一个构造函数创建出来的对象，都会默认的和构造函数的神秘对象关联
* 当使用一个方法进行属性或者方法访问的时候，会在当前对象内查找该属性和方法，如果未找到，就去与之关联的对象里面查找
<p style="color:red">
    在原型上操作，如果是读数据，当前对象没有就去与之关联的原型中查找，直到null
    如果是写数据，当前对象有该数据时，就修改，没有就添加 
</p>

## 原型链
```
function Person() {
    this.name = '张三';
    this.sayHello = function () {
    }
}

var p = new Person();
```
![原型图](https://github.com/Small-inn/JavaScript-HightOrder/blob/master/img/%E5%8E%9F%E5%9E%8B%E5%9B%BE%E8%A7%A3%EF%BC%88%E5%9F%BA%E6%9C%AC%E7%9A%84%E4%B8%89%E8%A7%92%E5%85%B3%E7%B3%BB%EF%BC%89.png)


## 完整版原型链
![完整版原型链](https://github.com/Small-inn/JavaScript-HightOrder/blob/master/img/%E5%AE%8C%E6%95%B4%E7%89%88%E7%9A%84%E5%8E%9F%E5%9E%8B%E9%93%BE.png)

##  原型成员
1. Object.prototype.__proto__: 指向对象被实例化的时候，用作原型的对象
2. Object.prototype.hasOwnProperty(): 返回一个布尔值，表示某个对象是否含有指定的属性，而且此属性非原型链继承的，这里注意与in关键字的区别
3. Object.prototype.isPrototypeOf():返回一个布尔值，表示指定的对象是否在本对象的原型链中
4. Object.prototype.toString(): 返回对象的字符串表示
5. Object.prototype.valueOf(): 返回指定对象的原始值
6. Object.prototype.propertyIsEnumerable(): 返回一个布尔值，判断对象本身是否拥有某个属性，并判断对象的指定属性能否被遍历


## instanceof关键字
>> 判断一个构造函数的原型对象是否在前者的原型链上


## 作用域
> 域表示一个范围，就是作用范围，作用域说明一个变量在什么地方可以使用，什么地方不可以使用。
    - 块级作用域
        - JavaScript中没有块级作用域
```
{
    var num = 10;
    {
        console.log(num)
    }
}
console.log(num)
```
<p>
    上面这段代码在js中不会报错，但是在c#,java,c等语言中就会报错
</p>

## 词法作用域
> 词法(代码)作用域，就是代码在编写过程中体现出来的作用范围，代码一旦写好，不用执行，作用范围就已经确定好了。
    - 在js中词法作用域规则
        - 函数允许访问函数外的数据
        - 整合代码结构中只有函数可以限定作用域
        - 作用域规则首先使用提升规则分析
        - 如果当前作用规则中有名字，就不考虑外面的名字

## 变量的提升(JavaScript预解析)
1 js并不是在运行时简简单单的逐字逐句的的解析执行
2 JavaScript预解析
> JavaScript引擎在对JavaScript代码进行解释之前，会对JavaScript代码进行预解析，在预解析阶段会将关键字var和function开头的语句块提前进行处理。
* 声明：告诉编译器/解析器有这个变量存在，这个行为是不分配内存空间的，在JavaScript中声明一个变量的操作，var a;
* 定义：为分配内存空间
* 初始化：在定义变量之后，系统为变量分配的空间内存储的值是不确定的，所以要对这个空间进行初始化，以确保程序的安全性和准确性。
* 赋值： 在变量分配好内存之后的某个时间内，对变量进行刷新操作。
```
console.log(fn)
var fn = 1;
function fn(){

}
//这时会打印出function(){}
<p>当函数名与变量名相同时，只会对函数进行提升，而不会对变量进行提升，会忽略变量。</p>
```

```
func()
function func(){
    console.log(1);
}
var func = function(){
    console.log(2);
}
<p>函数声明方式：function fn(){}; 函数表达方式：var fn = function(){};这两者的区别：函数声明会对函数体提升，而函数表达式是不会对函数体进行提升的</p>
```

> eg：
```
var num = 1;
function num () {
     alert( num );
}
num();
//提升之后
function num(){
   alert(num)
}
num = 1;
num();//Typeerror:num is not a function
```

3 预解析是分作用域的
4 预解析是分段的

## 作用域链
> 只有函数可以制造作用域结构， 那么只要是代码，就至少有一个作用域, 即全局作用域。凡是代码中有函数，那么这个函数就构成另一个作用域。如果函数中还有函数，那么在这个作用域中就又可以诞生一个作用域。
```
function f1() {
    function f2() {
    }
}

var num = 456;
function f3() {
    function f4() {    
    }
}
```
![作用域链图示](https://github.com/Small-inn/JavaScript-HightOrder/blob/master/img/%E4%BD%9C%E7%94%A8%E5%9F%9F%E9%93%BE%E5%9B%BE%E7%A4%BA.png)

## 变量访问规则
* 首先看变量在第几条链上, 在该链上看是否有变量的定义与赋值, 如果有直接使用
* 如果没有到上一级链上找( n - 1 级链 ), 如果有直接用, 停止继续查找.
* 如果还没有再次往上刚找... 直到全局链( 0 级 ), 还没有就是 is not defined
* 注意,同级的链不可混合查找
<p style="color:red">声明变量使用`var`, 如果不使用`var`声明的变量就是全局变量( 禁用 )</p>

## 闭包
> 闭包从字面意思理解就是闭合, 包起来.简单的来说闭包就是,一个具有封闭的对外不公开的, 包裹结构, 或空间.在JavaScript中函数可以构成闭包. 一般函数是一个代码结构的封闭结构, 即包裹的特性, 同时根据作用域规则, 只允许函数访问外部的数据, 外部无法访问函数内部的数据, 即封闭的对外不公开的特性. 因此说函数可以构成闭包.
* 函数内的数据不能直接在函数外被访问，是因为作用域的关系，上级作用域不能直接访问下级作用域中的数据。

## 函数的四种调用模式
1.函数模式 this指向window
2.方法模式 this指向调用当前方法的对象
3.构造函数模式 this指向new出来的对象
4.上下文模式 this指向动态，默认可以是window