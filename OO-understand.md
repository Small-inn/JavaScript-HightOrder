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

