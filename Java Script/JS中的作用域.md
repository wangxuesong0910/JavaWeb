# JS中的作用域

## JavaScript作用域

```html
<script>
        //1.JavaScript作用域：就是代码名字（变量）在某个范围内起作用和效果，目的是为了提高程序的可靠性，减少命名冲突
        //2.JS的作用域（es6）之前：全局作用域   局部作用域
        //3.全局作用域：整个script标签 或者一个单独的js文件
        var num = 10;
        console.log(num);

        //4.局部作用域（函数作用域） 在函数内部就是局部作用域 这个代码名字只能在函数内部其效果和作用
        function fn(){
            // 局部作用域
            var num = 20;
            console.log(num);
        }
        fn();
    </script>
```

## 变量的作用域

```html
<script>
        //变量作用域：根据作用域不同，我们变量分为局部变量和全局变量
        // 1.全局变量：在全局作用域下的变量 在全局下都可以使用
        // 注意：如果在函数内部 没有声明直接赋值的变量也属于全局变量
        var num = 10;//num是全局变量
        
        //2.局部变量：在局部作用域下的变量  后者在函数内部的变量就是局部变量
        //注意：函数的形参也是局部变量
        function fun(aru){
            var num1 = 10;//num1就是局部变量 只能在函数内部使用
            num2 = 20;//这就是一个全局变量
        }

        //3.从执行效率来看全局变量和局部变量
        //（1） 全局变量只有浏览器关闭的时候才会销毁，比较占内存资源
        //（2）局部变量 当我们程序执行完毕就会销毁，比较节约内存资源
    </script>
```

## 预解析

```html
<script>
        //问题：
        console.log(num);//undefiend 
        var num = 10;
        //JS的预解析执行了如下操作
        // var num;
        // console.log(num);
        // num = 10;

        //问题：
        fn();

        function fn(){
            console.log(11);
        }


        //问题：
        fun();
        var fun = function(){
            console.log(22);
        }
        //JS的预解析执行了如下操作
        // var fun;
        // fun();
        // fun = function(){
        //     console.log(22);
        // }



        //1.Js引擎运行js，分为两步：预解析  代码执行
        //(1).预解析js引擎会把js里面所有的var   还有function提升到当前作用域的最前面
        //(2).代码执行  按照代码书写的顺序从上往下执行
        //2.预解析分为 变量预解析（变量提升） 和 函数预解析（函数提升）
        //（1）/变量提升 就是把所有的变量声明提升到当前的作用域最前面，不提升赋值操作
        //(2) 函数提升 就是把所有函数声明提升到当前作用域的最前面   不调用函数
    </script>
```

### 预解析案例

```html
<script>
        var num = 10;
        fun();//undefiend
        function fun(){
            console.log(num);
            var num = 20;
        }

        //相当于执行如下操作
        var num;
        function fun(){
            var num;
            console.log(num);//链式查找num
            num = 20;
        }
        num = 10;
        fun();
    </script>
```

