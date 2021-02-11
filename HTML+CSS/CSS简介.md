# CSS简介

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>

    <!-- 
        第二种方式：
            - 将样式编写到head中的style标签里
                然后通过CSS的选择器来选中元素并为其设置各种样式
                可以同时为多个标签设置样式，并且修改时只需要修改一处即可全部应用
            - 内部样式表更加方便对样式进行复用
                问题：
                    我们的内部样式表只能对一个网页起作用
                        它里面的样式不能跨页面进行服用
     -->


     <!-- <style>
         p{color: #00bf00; font-size: 70px;}
     </style> -->


     <!-- 
         第三种方式（外部样式表）  【开发中最佳】
            - 可以将CSS样式编写到一个外部的CSS文件中
                然后通过link标签来引入外部的CSS文件
                - 可以跨页面引用
                - 不同页面之间复用
            - 将样式编写到外部CSS文件中，可以使用浏览器的缓存机制
                从而加快网页的加载速度，提高用户的体验
      -->
      <link rel="stylesheet" href="./style.css">
</head>
<body>
    <!-- 
        网页分成三个部分
            结构（html）
            表现（CSS）
            行为（JavaScript）
        CSS
            - 层叠样式表
            - 网页实际上是一个多层的结构，通过CSS可以分别为网页的每一层来设置样式
                而最终我们能看到只是网页的最上边一层
            - 总之一句话：CSS用来设置网页中元素的样式
     -->

     <!-- 
         使用CSS来修改元素的样式

         第一种方式（内联样式，行内样式）
            - 在标签内部通过style属性来设置元素的样式
            - 问题：
                使用内联样式，样式只能对一个标签生效，如果希望影响到多个元素必须在每一个元素中都复制一遍
            
            注意：
                开发时绝对不要使用内联样式
      -->

      <!-- <p style="color: #00bf00; font-size: 60px;">这是一个使用Style设置的字体</p> -->
      <p>这是使用外部样式表设置的字体</p>
</body>
</html>
```

```css
p{
    color: #00bf00;
    font-size: 10px;
}
```

# CSS语法

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>
    <style>
        /*
            CSS 中的注释，注释中的内容会被浏览器所忽略
            
            CSS的基本语法：
                选择器  声明块

                    选择器：通过选择器可以选中页面中的指定元素
                        比如：p的作用就是选中页面中所有的p元素
                    
                    声明块：通过声明块来指定要为元素设置的样式
                        声明块由一个一个的声明组成
                        声明是一个名值对结构
                            一个样式名对应一个样式值，名和值之间以:连接，以;结尾

         */

         p{
             color: #00bf00;
             font-size: 30px;
         }
    </style>
</head>
<body>
    <p>这是一句话</p>
</body>
</html>
```

# CSS常用选择器

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>
    <style>
        /*
            将所有段落设置为红色（字体）
            
            元素选择器
                作用：根据标签名来选中指定的元素
                语法：标签名（）
                例子：p{},h1{},div{}
                    p{
                        color:red;
                    }
         */

         /*
                将其中一句话设置为红色？

                id选择器
                    作用：根据元素的id属性值选中一个元素
                    语法：#id属性值()
                    例子：#box{}，#red{}
          */
          #red{
              color: red;
          }

        
          /*
            将其中两句话设置为蓝色？
            
            类选择器
                作用：根据元素的class属性选中一组元素
                语法：.class属性值

           */
           .blue{
               color: blue;
           }
           .abc{
               font-size: 30px;
           }


           /*
            通配选择器：
                作用：选中页面中的所有元素
                语法：*{} 
            */
         
    </style>
</head>
<body>
<h1>这是一个标题</h1>
<p>这是第一句话</p>
<p>这是第二句话</p>
<p id="red">这是第三句话</p>
<p>这是第四句话</p>
<p>这是第五句话</p>

<!-- 
    class是一个标签的属性，它和id类似，不同的是class可以重复使用
        可以通过class属性来为元素分组
        可以同时为一个元素指定多个class属性
 -->
<p class="blue">这是第六句话</p>
<p class="blue abc">这是第七句话</p>
</body>
</html>
```

# 复合选择器

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>
    <style>
        /*
            将class为red 的元素设置为红色（字体） 
         */
         .red{
             color: red;
         }

         /* 将class为red的div字体大小设置为30px */
         /*
            交集选择器
                作用：选中同时符合多个条件的元素
                语法：选择器1选择器2选择器3选择器n{}
                注意：
                    交集选择器中如果有元素选择器，必须使用元素选择器开头 
          */
        div.red{
            font-size: 30px;
        }

        .a.b.c{
            color: blue;
        }

        /*
            选择器分组（并集选择器） 
                作用：同时选择多个选择器对应的元素
                语法：选择器1,选择器2,选择器3,选择器n{}
                    #p1,.p2,h1,span{}
         */
         h1,span{
             color: green;
         }
    </style>
</head>
<body>
    <div class="red">一个div标签</div>
    <p class="red">一个p标签</p>
    <div class="red2 a b c">第二个div标签</div>

    <h1>标题</h1>
    <span>66666</span>

</body>
</html>
```

# 关系选择器

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>

    <style>
        /*
            为div 的子元素span设置一个字体颜色红色
                （为div直接包含的span设置一个字体颜色）

            子元素选择器
                作用：选中指定父元素的指定子元素
                语法：父元素 > 子元素 ...
                div > p > span > n{}
         */
         div > span{
             color: orange;
         }

         /*
            后代元素选择器
                作用：选中指定元素内的指定后代元素
                语法：祖宗 后代 
          */

          div span{
              color: skyblue;
          }


          /*
            兄弟选择器
                选择紧挨着的下一个兄弟
                    语法：前一个 + 下一个
                
                选择下边所有兄弟
                    语法：兄 ~ 弟
           */

           p + span{
               color: red;
           }

           p ~ span{
               color: red;
           }



    </style>
</head>
<body>
    <!-- 
        父元素
            - 直接包含子元素的元素叫父元素
        子元素
            - 直接被父元素包含的元素是子元素
        祖先元素
            - 直接或间接包含后代元素的元素叫做祖先元素
            - 一个元素的父元素也是它的祖先元素
        后代元素
            - 直接或间接被祖先元素包含的元素叫做后代元素
            - 子元素也是后代元素
        兄弟元素
            - 拥有相同父元素的元素是兄弟元素

     -->

     <div>
         一个div标签

         <p>
             我是div中的p元素
             <span>我是p元素中的span元素</span>
         </p>

         <span>我是div中的span元素</span>
         <span>我是div中的span元素</span>
         <span>我是div中的span元素</span>
         <span>我是div中的span元素</span>
     </div>

     <span>我是div外部的span</span>
</body>
</html>
```

# 属性选择器

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>
    <style>
        /*
            [属性名] 选择含有指定属性的元素
            [属性名=属性值] 选择含有指定属性和属性值的元素
            [属性名^=属性值] 选择属性值以指定值开头的元素
            [属性名$=属性值] 选择属性值以指定值结尾的元素
            [属性名*=属性值] 选择属性值中含有某值的元素的元素 
         */
         /* p[title]{ */
         /* p[title=abc]{ */
         /* p[title^=abc]{ */
         /* p[title$=c]{ */
         p[title*=e]{
             color: orange;
         }

    </style>
</head>
<body>
    <p title="abc">这是第一句话</p>
    <p title="abcdef">这是第二句话</p>
    <p title="helloabc">这是第三句话</p>
    <p>这是第四句话</p>
    <p>这是第五句话</p>
    <p>这是第六句话</p>
</body>
</html>
```

# 伪类选择器

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>

    <style>
        /*
            将ul里的第一个li设置为红色

            伪类（不存在的类，特殊的类） 
                - 伪类用来描述一个元素的特殊状态
                    比如：第一个子元素，被点击的元素，鼠标移入的元素
                - 伪类一般情况下都是以:开头
                    :first-child第一个子元素
                    :last-child最后一个子元素
                    :nth-child()选中第n个子元素
                        特殊值：
                            n 第n个n的范围0到正无穷
                            2n或even表示选中偶数位的元素
                            2n+1或odd表示选中奇数位的元素

                    - 以上这些伪类都是根据所有的子元素进行排序

                :first-of-type
                :last-of-type
                :nth-of-type()
                    -这几个伪类的功能和上述的类似，不通点是他们在同类型元素中进行排序
            
            - :not()否定伪类
                - 将符合条件的元素从选择器中去除
         */

         /* ul > li:first-child{
             color: orange;
         } */

         /* ul > li:nth-child(2n+1){
             color: orange;
         } */

         /* ul > li:first-of-type{
             color: orange;
         } */

         ul > li:not(:nth-of-type(3)){
             color: orange;
         }
    </style>
</head>
<body>
    <ul>
        <span>这是一个span标签</span>
        <li>第零个</li>
        <li>第一个</li>
        <li>第二个</li>
        <li>第三个</li>
        <li>第四个</li>
        <li>第五个</li>
        <li>第六个</li>
</ul>
</body>
</html>
```

## 超链接的伪类

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>
    <style>
        /*
            :link 用来表示没访问过的链接（正常的链接） 
         */
         a:link{
             color: blue;
         }

         /*
            :visited 用来表示访问过的连接
                由于隐私关系，只能修改连接的颜色 
          */
          a:visited{
              color:red;
          }

          /*
            :hover 用来表示鼠标移入的状态 
           */
           a:hover{
               color: aqua;
               font-size: 30px;
           }

           /*
                :active 用来表示鼠标点击 
            */
            a:active{
                color: chartreuse;
            }
    </style>
</head>
<body>
    <a href="https://www.baidu.com">点击过的连接</a>
    <a href="https://www.baidu123.com">没有点击过的连接</a>
</body>
</html>
```

## 伪元素选择器

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>
    <style>
        p{
            font-size: 20px;
        }

        /*
            为元素：表示页面中一些特殊元素的并不真实存在的元素（特殊的位置）
                为元素使用::开头

                ::first-letter 表示第一个字母
                ::first-line    表示第一行
                ::selection     表示选中的内容

                ::before    元素的开始
                ::after     元素的结束
                    - before 和 after必须结合content属性来使用
         */
         p::first-letter{
             font-size: 30px;
         }
         p::first-line{
             background-color: orange;
         }
         p::selection{
             background-color: #00bf00;
         }

         div::before{
             content: '👉';
         }
         div::after{
             content: '👈';
         }
    </style>
</head>
<body>
    <p>Three passions, simple but overwhelmingly strong, have governed my life: the longing for love, the search for knowledge, and unbearable pity for the suffering of mankind. 
    </p>

    <div>This is a html page</div>
</body>
</html>
```

# 样式的继承

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>
    <style>
        /*
            样式的继承：我们为一个元素设置的样式同时也会应用到它的后代元素上 
         */

         p{
             color: orange;
         }
    </style>
</head>
<body>
    <p>
        一个p元素
        <span>p元素中的span元素</span>
        <!-- p中所有元素全变色，体现继承 -->
    </p>
</body>
</html>
```

# 盒模型

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>
    <style>
        
        .box1{
            /*
            内容区（content），元素中的所有的子元素和文本内容都在内容区中排列
                内容区的大小由width和height两个属性来设置
                    width 设置内容区的宽度
                    height 设置内容区的高度 
         */
            width: 200px;
            height: 200px;
            background-color: orange;

            /*
            边框（border），边框属于盒子边缘，边框里边属于盒子内部，出了边框都是盒子的外部
                边框的大小会影响到整个盒子的大小
            要设置边框，需要至少设置三个样式
                边框的宽度 border-width     默认3个像素
                    可以分别指定四个方向的边框宽度
                        四个值：上  右  下  左
                        三个值：上  左右    下
                        两个值：上下    左右
                    
                    除了border-width还有一组 border-xxx-width
                        xxx可以是 top right bottom left
                        用来单独指定某一个边的宽度

                边框的颜色 border-color
                边框的样式 border-style
         */

         border-width: 10px 20px 30px 40px;

         
         /*
            border-color 用来指定边框的颜色，同样可以分别指定四个边的边框
                规则和border-width一样
            
            border-color也可以省略不写，如果省略则自动使用color的颜色值
          */

         border-color: black;

         /*
                border-style 指定边框的样式
                    solid 表示实现
                    dotted 点状虚线
                    dashed 虚线
                    double 双线

                    border-style的默认值是none 表示没有边框
          */
         border-style:solid;


         /* 
                border简写属性，通过该属性可以同时设置边框所有的相关样式，并且没有顺序要求

                    除了border以外还有四个 border-xxx
                        border-top
                        border-right
                        border-bottom
                        border-left
          */
         /* border:solid 10px orange; */
        }

        
    </style>
</head>
<body>
    <!-- 
        盒模型、盒子模型、框模型（box model）
            - CSS将页面中的所有元素都设置为了一个矩形的盒子
            - 将元素设置为矩形的盒子后，对页面的布局就变成将不同盒子摆放到不同的位置
            - 每一个盒子都由以下几个部分组成
                内容区（content）
                内边框（padding）
                边框（border）
                外边距（margin）
     -->

     <div class="box1"></div>
</body>
</html>
```

## 盒子模型_内边距

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>
    <style>
        .box1{
            width: 200px;
            height: 200px;
            background-color: red;
            border: 10px orange solid;

            /* 
                内边距（padding）
                    - 内容区和边框之间的距离是内边框
                    - 一共有四个方向的内边距
                        padding-top
                        padding-right
                        padding-bottom
                        padding-left

                    - 内边距的设置会影响到盒子的大小
                    - 背景颜色会延申到内边距上

                一共盒子的可见框的大小，由内容区 内边距 和 边框共同决定，
                    所以在计算盒子大小时，需要将这三个区域加到一起计算


             */

             /*
                padding 内边距的简写属性，可以同时指定四个方向的内边距
                    规则和border-width 一样

              */

              padding: 20px 10px 30px 40px;

        }
    </style>
</head>
<body>
    <div class="box1">
        <div class="inner"></div>
    </div>
</body>
</html>
```

## 盒子模型_外边距

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>Document</title>
    <style>
        .box1{
            width: 200px;
            height: 200px;
            background-color: orange;
            border: royalblue 10px solid;

            /*
                外边距（margin） 
                    - 外边距不会影响盒子可见框的大小
                    - 但是外边距会影响盒子的位置
                    - 一共有四个方向的外边距
                        margin-top
                            - 上外边距，设置一个正值，元素会向下移动
                        margin-right
                            - 默认情况下设置margin-right不会产生任何效果
                        margin-bottom
                            - 下外边距，设置一个正值，其下边的元素会向下移动
                        margin-left
                            - 左外边距，设置一个政治，元素会向右移动


                    margin也可以设置负值，如果是负值则元素会向相反的方向移动
                    
                    - 元素在页面中是按照自左向右顺序排列的
                        所以默认情况下，我们设置的左和上外边距则会移动
                        而设置下和右外边距会移动其他元素

                    - margin的简写属性
                        margin 可以同时设置四个方向的外边距，用法和padding一样

                    margin会影响到盒子的实际占用空间
             */
             /* margin-top: 100px;
             margin-left: 100px; */

             /* margin-bottom: 100px; */

             margin-bottom: -100px;


        }

        .box2{
            width: 220px;
            height: 220px;
            background-color: royalblue;
        }
    </style>
</head>
<body>
    <div class="box1"></div>
    <div class="box2"></div>
</body>
</html>
```

# 常用样式

```css
/* 9.5、常用样式： 、常用样式：
1、字体颜色
color：red；
颜色可以写颜色名如：black, blue, red, green 等
颜色也可以写 rgb 值和十六进制表示值：如 rgb(255,0,0)，#00F6DE，如果写十六进制值必
须加#
2、宽度
width:19px;
宽度可以写像素值：19px；
也可以写百分比值：20%；
3、高度
height:20px;
高度可以写像素值：19px；
也可以写百分比值：20%；
4、背景颜色
background-color:#0F2D4C
4、字体样式：
color：#FF0000；字体颜色红色
font-size：20px; 字体大小
5、红色 1 像素实线边框
border：1px solid red;
7、DIV 居中
margin-left: auto;
margin-right: auto;
8、文本居中：
text-align: center;
9、超连接去下划线
text-decoration: none;
10、表格细线
table {
border: 1px solid black; /*设置边框*/
border-collapse: collapse; /*将边框合并*/
}
td,th {
border: 1px solid black; /*设置边框*/
}
11、列表去除修饰
ul {
list-style: none;
}
*/
示例代码：
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>06-css 常用样式.html</title>
<style type="text/css">
div{
color: red;
border: 1px yellow solid;
width: 300px;
height: 300px;
background-color: green;
font-size: 30px;
margin-left: auto;
margin-right: auto;
text-align: center;
}
table{
border: 1px red solid;
border-collapse: collapse;
}
td{
border: 1px red solid;
}
a{
text-decoration: none;
}
ul{
list-style: none;
}
</style>
</head>
<body>
<ul>
<li>11111111111</li>
<li>11111111111</li>
<li>11111111111</li>
<li>11111111111</li>
<li>11111111111</li>
</ul>
<table>
<tr>
<td>1.1</td>
<td>1.2</td>
</tr>
</table>
<a href="http://www.baidu.com">百度</a>
<div>我是 div 标签</div>
</body>
</html>
```



