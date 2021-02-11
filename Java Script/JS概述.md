# JS

## JS简介

> 浏览器分为两个部分：渲染引擎和JS引擎

* 渲染引擎：用来解析HTML与CSS，俗称内核，比如chrome浏览器的blink，老版本的webkit
* JS引擎：也称为JS解释器，用来读取网页中的JavaScript代码，对其处理后运行，比如chrome浏览器的V8

>浏览器本身不会执行JS代码，而是通过内置的JavaScript引擎（解释器）来执行JS代码，JS引擎执行代码时逐行解释每一句源码（转换为机器语言），然后由计算机去执行，所以JavaScript语言归为脚本语言，会逐行解释执行

## JS的组成

### DOM-文档对象模型

* **文档对象模型**（Document Object Model，简称DOM），是W3C组织推荐的处理可扩展标记语言的标准编程接口。通过DOM提供的接口可以对页面上的各种元素进行操作（大小、位置、颜色等）。

* BOM（Browser Object Model，简称BOM）是指 浏览器对象模型，它提供了独立于内容的、可以与浏览器窗口进行互动的对象结构。通过BOM可以操作浏览器窗口，比如弹出框、控制浏览器跳转、获取分辨率等。     

## JS规范

> JS有3种书写位置，分别为行内、内嵌和外部

### 1.行内式JS

```html
    <input type="button" value="点击我" onclick="alert('Hello World')"/>
```

* 可以将单行或少量JS代码写在HTML标签的事件属性中（以on开头的属性），如：onclick
* 注意单双引号的使用：在HTML中我们推荐使用双引号，JS中我们推荐使用单引号
* 可读性差，在html中编写JS大量代码时，不方便阅读；
* 引号易错，引号多层嵌套匹配时，非常容易弄混；
* 特殊情况下使用

### 2. 内嵌式JS

```html
<script>
        alert("Hello Word");
    </script>

```

* 可以将多行JS代码写到<script>标签中
* 内嵌JS是学习时常用的方式

### 3. 外部JS文件

```html
<script src="Demo01.js"></script>
```

```js
alert("hello word");
```

* 利于HTML页面代码结构化，把大段JS代码独立到HTML页面之外，既美观，也方便文件级别的复用
* 引用外部JS文件的script标签中间不可以写代码
* 适合于JS代码量比较大的情况

## JS中的注释

```html
    <script>
        // 1.单行注释   ctrl+/
        /*
            2.多行注释  默认快捷键  shift + alt + a 
         */
    </script>
```

## JS中的输入输出语句

> 为了方便信息的输入输出，JS提供了一些输入输出语句，其常用的语句如下：

|       方法       |              说明              |  归属  |
| :--------------: | :----------------------------: | :----: |
|   alert（msg）   |        浏览器弹出警示框        | 浏览器 |
| console.log(msg) |    浏览器控制台打印输出信息    | 浏览器 |
|   prompt(info)   | 浏览器弹出输入框，用户可以输入 | 浏览器 |

```html
  <script>
        //  弹出输入框
        prompt('ssss');

        // alert 弹出警示框，用户可看
        alert('6666');

        // console 控制台输出，给程序员测试用
        console.log('测试内容：F12可看');
    </script>
```



