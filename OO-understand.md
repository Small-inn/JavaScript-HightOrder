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
    属性：length：设置或者返回数组中元素的数目
    方法：concat(): 连接两个或者更多的数组，并返回结果
         join()：把数组的所有元素放入一个字符串，通过指定的分隔符进行分隔
         pop()：删除并返回数组的最后一个元素
         push()：向数组的末尾添加一个或者更多元素，返回新的长度
         reserse()：颠倒数组中元素的顺序
         shift()：删除并返回数组的第一个元素
         slice()：从某个已有的数组返回选定的元素
         sort()：对数组的元素进行排序
         splice()：删除元素，并向数组添加新的元素
         unshift()：向数组的开头添加一个或者更多元素，并返回新的长度
2. Date
    不说了，太长了
3. Number
    属性：MAX_VALUE：可表示的最大的数
         MIN_VALUE：可表示的最小的数
         NAN：非数字
         NEGATIVE_INFINITY：负无穷大，溢出时返回该值
         POSITIVE_INFINITY：正无穷大，溢出时返回该值
    方法：toString() 把数字转化成字符串，使用指定的基数
         toFixed()：把数字转化成字符串，结果的小数点后又指定位数的数字
         toExponential()：把对象的值转化为指数计数法
         toPrecision()：把数字格式化为指定的长度
         valueOf()：返回一个Number对象的基本数字值
4. Boolean
    方法：toString()：把逻辑值转化为字符串，并返回结果
         valueOf()：返回Boolean对象的原始值
5. String
    属性和方法：更长就不写了
6. Math
    属性和方法：一般不常用，常用的掌握就行了
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

![图解]()

    