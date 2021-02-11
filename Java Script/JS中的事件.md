# JS中的事件

> 什么是事件？事件是电脑输入设备与页面进行交互的相应

* 常用的事件

|            事件            |                      描述                      |
| :------------------------: | :--------------------------------------------: |
|    onload加载完成事件：    | 页面加载完成之后，常用于做页面js代码初始化操作 |
|     onclick单击事件：      |            常用于按钮的点击相应操作            |
|    onblur失去焦点事件：    |  常用于输入框失去焦点后验证其输入内容是否合法  |
| onchange内容发生改变事件： |    常用于下拉列表和输入框内容发生改变后操作    |
|   onsubmit表达提交事件：   |    常用于表单提交前，验证所有表单项是否合法    |

## 静态注册和动态注册

> 什么是事件的注册（绑定）？
>
> 其实就是告诉浏览器，当事件响应后要执行那些操作代码，叫事件注册或事件绑定

* 静态注册事件：通过html标签的事件属性直接赋予事件响应后的代码，这种叫静态注册
* 动态注册事件：指先通过js代码得到标签的dom对象，然后通过dom对象.事件名 = function(){} 这种形式赋予事件响应后的代码，叫动态注册
  * 动态注册基本步骤：
    1. 获取标签对象
    2. 标签对象.事件名 = function(){}

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>
    <script>
        function onloadFun(){
            alert('静态注册onload，所有代码');
        }

        //onload事件动态注册，写法是固定的
        window.onload = function(){
            alert('动态注册的onload事件');
        }
    </script>
</head>
<!-- 静态注册onload事件
        onload事件是浏览器解析完页面之后就会自动触发的事件
        <body onload="onloadFun();">

 -->
<body>
    
</body>
</html>
```

## onclick单击事件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>

    <script>
        function onclickFun(){
            alert('静态注册onclick事件');
        }

        //动态注册onclick事件
        window.onload = function(){
            //1.getElementById通过id属性获取标签对象
            var btn = document.getElementById("btn2");

            //2.通过标签对象.事件名 = function(){}
            btn.onclick = function(){
                alert("动态注册onclick事件");
            }
        }
    </script>
</head>
<body>
    <!-- 静态注册onclick事件 -->
    <button onclick="onclickFun();">静态注册按钮</button>
    <button id = "btn2">动态注册按钮事件</button>
</body>
</html>
```

## onblur失去焦点事件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>

    <script>
        function onblurFun(){
            alert('静态注册失去焦点事件');
        }

        //动态注册
        window.onload = function(){
            //获取标签对象
            var onblurLose = document.getElementById("password");
            
            onblurLose.onblur = function(){
                alert('动态注册失去焦点事件');
            }
        }
    </script>
</head>
<body>
    用户名：<input type="text" onblur="onblurFun();"></br>
    密码：<input id = "password" type="text"></br>
    
</body>
</html>
```

## onchange事件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>
    <script>
        function onchangeFun(){
            alert('静态注册onchange事件');
        }

        //动态onchange事件
        window.onload = function(){
            //获取标签对象
           var food = document.getElementById("food");
           //通过标签对象.事件名 = function(){}
           food.onchange = function(){
               alert('动态注册onchang事件');
           }

        }
    </script>
</head>
<body>

    <!-- 静态注册onchange事件 -->
<select onchange="onchangeFun();">
    <option value="">苹果</option>
    <option value="">橘子</option>
    <option value="">梨</option>
    <option value="">橙子</option>
</select>

<!-- 动态注册onchange事件 -->
<select id="food">
    <option value="">苹果</option>
    <option value="">橘子</option>
    <option value="">梨</option>
    <option value="">橙子</option>
</select>
    
</body>
</html>
```

## onsubmit表单提交事件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>
    <script>
        function onsubmitFun(){
            alert('静态注册onsubmit提交事件，假设当前是不合法的提交');
            return false;
        }

        //动态注册提交事件
        window.onload = function(){
            //获取标签对象
            var onsubmitclick = document.getElementById("form01");

            //通过标签对象.事件名 = function(){}
            onsubmitclick.onsubmit = function(){
                alert('动态注册onsubmit提交事件，假设当前是不合法的提交');

                return false;
            }
        }
    </script>
</head>
<body>
    <!-- return false 可以阻止表单提交 -->
<form action="http://localhost:8080" method="get" onsubmit="return onsubmitFun();">
    <input type="submit" value="静态注册提交事件"/>
</form>

   <!-- return false 可以阻止表单提交 -->
<form action="http://localhost:8080" method="get" id="form01">
    <input type="submit" value="动态注册提交事件" />
</form>
</body>
</html>
```

