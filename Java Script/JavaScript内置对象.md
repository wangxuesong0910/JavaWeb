# JavaScript内置对象

## 内置对象

* JavaScript中的对象分为3种：自定义对象、内置对象、浏览器对象
* 前面两种对象是JS基础，属于ECMAScript；第三个浏览器对象属于我们JS独有的，我们JS API讲解
* 内置对象就是指JS语言自带的一些对象，这些对象供开发者使用，并提供了一些常用的或者是最基本而必要的功能（属性和方法）

## 查文档

### MDN

* 学习一个内置对象 的使用，只要学会其常用成员即可，我们可以通过查文档学习，可以通过MDN/W3C来查询
* Mozilla开发者网络（MDN）提供了有关开放网络技术（Open Web）的信息，包括HTML、CSS和万维网及HTML5应用的API

## Math对象

```html
<script>
        //Math数学对象，不是一个构造函数，所以不需要new来调用，而是直接使用里面的属性和方法即可
        console.log(Math.PI);
        console.log(Math.max(19,1,11));
        console.log(Math.max(-1,-10));
        console.log(Math.max(1,22,'aaa'));//NaN
        console.log(Math.max());//-Infinity
    
        console.log(Math.abs(-1));//绝对值
        console.log(Math.abs('-1'));//隐式转换 会把字符串型 -1 转换为数字型
    </script>
```

### Random随机数

```html
<script>
        //猜数字游戏
        function getNum(min,max){
            return Math.floor(Math.random() * (max - min + 1)) + min;
        }

        var random = getNum(1,10);
        while(true){
            var num = prompt("随机输入1到10之间的任意一个数字");
            if(num > 10 || num <1){
                alert('输入数据超出范围');
            }else if(num < random){
                alert('小了');
            }else if(num > random){                
                alert('大了');
            }else{
                alert('恭喜你');
                break;
            }
        }
        
    </script>
```

## 日期对象

* Date对象和Math对象不一样，他是一个构造函数，所以我们需要实例化后才能使用
* Date实例用来处理日期和时间

```html
<script>
        //Date() 日期对象 是一个构造函数  必须使用new 来调用创建我们的日期对象
        var arr = new Array();//创建一个数组对象
        var obj = new Object();//创建了一个实例对象
        //1.使用Date   如果没有参数，返回当前系统的当前时间
        var date = new Date();
        console.log(date);
        //2.参数常用的写法  数字型  2019, 10, 01  或者是  字符串型 '2019-10-1  8:8:8'
        var date1 = new Date(2020,10,01);
        console.log(date1);//返回的是11月，不是10月

        var date2 = new Date('2020-10-1  8:8:8');
        console.log(date2);
    </script>
```

### 日期格式化

* 如果想要2019-8-8 8:8:8格式的日期，要怎么办？
* 需要获取日期指定的部分，所以我们要手动得到这种 格式

|    方法名     |             说明             |        代码        |
| :-----------: | :--------------------------: | :----------------: |
| getFullYear() |           获取当年           | dObj.getFullYear() |
|  getMonth()   |       获取当月(0-11）        |  dObj.getMonth()   |
|   getDate()   |         获取当天日期         |   dObj.getDate()   |
|   getDay()    | 获取星期几（周日0 到周六 6） |   dObj.getDay()    |
|  getHours()   |         获取当前小时         |  dObj.getHours()   |
| getMinutes()  |         获取当前分钟         | dObj.getMinutes()  |
| getSeconds()  |         获取当前秒钟         | dObj.getSeconds()  |

```html
//获取指定日期对象的时分秒
<script>
        //格式化日期  时分秒
        var date = new Date();

        //要求封装一个函数 返回当前的时分秒  格式：08:08:08
        function getTime(){
           var h =  date.getHours();
           h = h < 10 ? '0'+h:h;
           var m = date.getMinutes();
           m = m < 10 ? '0'+m:m;
           var s = date.getSeconds();
           s = s < 10 ? '0'+s:s;

           return h+':'+m+':'+s;
        }

        console.log(getTime());
    </script>
```

```html
<script>
        //获得Date总的毫秒数（时间戳）  不是当前时间的毫秒数 而是距离1970年1月1号过了多少毫秒
        //1.通过 valueOf()  getTime()
        var date = new Date();
        console.log(date.valueOf());
        console.log(date.getTime());
        //2.简单写法（最常用的写法）
        var date1 = +new Date();// +new Date()  返回的就是总的毫秒数
        console.log(date1);
        //3. H5 新增的  获得总的毫秒数
        console.log(Date.now());
    </script>
```

