# DOM模型

> DOM 全称是 Document Object Model 文档对象模型

## getElementById

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>
    <script>
        /**
         * 需求：当用户点击了校验按钮，要获取输入框中的内容，然后验证其是否合法
         * 验证的规则是：必须由字母，数字，下划线组成，并且长度是5到12位 
         * 
         */

         function onclickFun(){
             //1.当我们要操作一个标签的时候，一定要获取这个标签对象
             var usernameObj = document.getElementById("username");
             
             //2.获取value标签中的内容，大概就是获取当前input标签对象中的value值
             var usernameText = usernameObj.value;

             //正则表达式验证字符串，符合上面需求
             var patt = /^\w{5,12}$/;

             /**
              * test()方法用于测试某个字符串，是不是匹配我的规则
              * 匹配返回true
              * 不匹配就返回false
             */

             if(patt.test(usernameText)){
                 alert("合法用户名");
             }else{
                 alert("不合法用户名");
             }
         }
    </script>
</head>
<body>
    用户名：<input type="text" id="username" value=""/>
    <button onclick="onclickFun()">校验</button>
</body>
</html>
```

## 正则表达式

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>
    <script type="text/javascript">
        // 表示要求字符串中，是否包含字母e
        // var patt = new RegExp("e");
        // var patt = /e/; // 也是正则表达式对象
        // 表示要求字符串中，是否包含字母a或b或c
        // var patt = /[abc]/;
        // 表示要求字符串，是否包含小写字母
        // var patt = /[a-z]/;
        // 表示要求字符串，是否包含任意大写字母
        // var patt = /[A-Z]/;
        // 表示要求字符串，是否包含任意数字
        // var patt = /[0-9]/;
        // 表示要求字符串，是否包含字母，数字，下划线
        // var patt = /\w/;
        // 表示要求 字符串中是否包含至少一个a
        // var patt = /a+/;
        // 表示要求 字符串中是否 *包含* 零个 或 多个a
        // var patt = /a*/;
        // 表示要求 字符串是否包含一个或零个a
        // var patt = /a?/;
        // 表示要求 字符串是否包含连续三个a
        // var patt = /a{3}/;
        // 表示要求 字符串是否包 至少3个连续的a，最多5个连续的a
        // var patt = /a{3,5}/;
        // 表示要求 字符串是否包 至少3个连续的a，
        // var patt = /a{3,}/;
        // 表示要求 字符串必须以a结尾
        // var patt = /a$/;
        // 表示要求 字符串必须以a打头
        // var patt = /^a/;

        // 要求字符串中是否*包含* 至少3个连续的a
        // var patt = /a{3,5}/;
        // 要求字符串，从头到尾都必须完全匹配
        // var patt = /^a{3,5}$/;

        var patt = /^\w{5,12}$/;

        var str = "wzg168[[[";

        alert( patt.test(str) );


    </script>
</head>
<body>
    
</body>
</html>
```

### 两种常见的验证提示效果

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>
    <script>
        /**
         * 需求：当用户点击了校验按钮，要获取输入框中的内容，然后验证其是否合法
         * 验证的规则是：必须由字母，数字，下划线组成，并且长度是5到12位 
         * 
         */

         function onclickFun(){
             //1.当我们要操作一个标签的时候，一定要获取这个标签对象
             var usernameObj = document.getElementById("username");
             
             //2.获取value标签中的内容，大概就是获取当前input标签对象中的value值
             var usernameText = usernameObj.value;

             //正则表达式验证字符串，符合上面需求
             var patt = /^\w{5,12}$/;

             /**
              * test()方法用于测试某个字符串，是不是匹配我的规则
              * 匹配返回true
              * 不匹配就返回false
             */

             //通用提示校验结果
             var usernameSpan = document.getElementById("usernameSpan");
             //innerHTML 表示其实标签和结束标签中的内容
             //innerHTML 这个属性可读可写
             if(patt.test(usernameText)){
                //通用提示校验结果方法一：
                // usernameSpan.innerHTML = "合法用户名";

                //通用提示校验结果方法二：
                usernameSpan.innerHTML = "<img src=\"./img/right.png\"  width=\"12\" height=\"12\">";
                //  alert("合法用户名");
             }else{
                // usernameSpan.innerHTML = "不合法用户名";
                usernameSpan.innerHTML = "<img src=\"./img/wrong.png\" width=\"12\" height=\"12\">";
                //  alert("不合法用户名");
             }
         }
    </script>
</head>
<body>
    用户名：<input type="text" id="username" value=""/>

    <!-- 通用提示校验结果方法： -->
    <span id= "usernameSpan" style="color: red;"></span>

    <button onclick="onclickFun()">校验</button>
</body>
</html>
```

## getElementByName

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>
    <script>
        function checkAll(){
            //所有复选框全选
            //document.getElementsByName("hobby");根据指定name属性查询返回多个标签对象集合
            //这个集合的操作跟数组一样
            //集合中每个元素都是dom对象
            
            var hobby = document.getElementsByName("hobby");

            //checked表示复选框的中选中状态，如果选中位true，不选为false
            for(var i =0; i < hobby.length; i++){
                hobby[i].checked = true;
            }

        }

        function checkNo(){
            //所有复选框全选
            //document.getElementsByName("hobby");根据指定name属性查询返回多个标签对象集合
            //这个集合的操作跟数组一样
            //集合中每个元素都是dom对象
            
            var hobby = document.getElementsByName("hobby");

            //checked表示复选框的中选中状态，如果选中位true，不选为false
            for(var i =0; i < hobby.length; i++){
                hobby[i].checked = false;
            }

        }

        function checkRevers(){
            //所有复选框全选
            //document.getElementsByName("hobby");根据指定name属性查询返回多个标签对象集合
            //这个集合的操作跟数组一样
            //集合中每个元素都是dom对象
            
            var hobby = document.getElementsByName("hobby");

            //checked表示复选框的中选中状态，如果选中位true，不选为false
            for(var i =0; i < hobby.length; i++){
                hobby[i].checked = !hobby[i].checked;
                // if(hobby[i].checked){
                
                //     hobby[i].checked = false;
                // }else{
                //     hobby[i].checked = true;
                // }
                
            }
        }

    </script>
</head>
<body>
    兴趣爱好：
    <input type="checkbox" name="hobby" value="cpp">C++
    <input type="checkbox" name="hobby" value="java">java
    <input type="checkbox" name="hobby" value="js">js
    <br/>
    <button onclick="checkAll()">全选</button>
    <button onclick="checkNo()">全不选</button>
    <button onclick="checkRevers()">反选</button>
    
</body>
</html>
```

## getElementByTagName

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script>
        function checkAll(){
           //document.getElementsByTagName("input");按照指定签名来进行查询并返回集合
           //这个集合的操作跟数组一样
           //集合中都是dom对象，在html中从上到下顺序
           var inputs = document.getElementsByTagName("input");
           for (var i = 0; i < inputs.length; i++) {
               inputs[i].checked = true;
           }

        }
    </script>
</head>
<body>
    兴趣爱好：
    <input type="checkbox" name="hobby" value="cpp">C++
    <input type="checkbox" name="hobby" value="java">java
    <input type="checkbox" name="hobby" value="js">js
    <br/>
    <button onclick="checkAll()">全选</button>
</body>
</html>
```

## dom对象查询练习

