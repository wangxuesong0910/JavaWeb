# JSON

> **JSON** (JavaScript Object Notation) 是一种轻量级的数据交换格式。易于人阅读和编写。同时也易于机器解析和生成。JSON 
>
> 采用完全独立于语言的文本格式，而且很多语言都提供了对 json 的支持（包括 C, C++, C#, Java, JavaScript, Perl, Python 
>
> 等）。 这样就使得 JSON 成为理想的数据交换格式。

* JSON 是一种轻量级的数据交换格式
* 轻量级指的是跟xml做比较
* 数据交换指的是客户端和服务器之间业务数据的传递格式

## JSON在JavaScript中的使用

### JSON的定义

> json 是由键值对组成，并且由花括号（大括号）包围。每个键由引号引起来，键和值之间使用冒号进行分隔， 
>
> 多组键值对之间进行逗号进行分隔。

```js
<script type="text/javascript">
			// json的定义
			var jsonObj = {
				"key1":12,
				"key2":"abc",
				"key3":true,
				"key4":[11,"arr",false],
				"key5":{
					"key5_1" : 551,
					"key5_2" : "key5_2_value"
				}
				"key6":[{
					"key6_1_1":6611,
					"key6_1_2":"key6_1_2_value"
				},{
					"key6_2_1":6621,
					"key6_2_2":"key6_2_2_value"
				}]
			}
			// json的访问
			// json对象转字符串
			// json字符串转json对象
		</script>
```

### JSON的访问

1. json本身是一个对象
2. json中的key我们可以理解为是对象中的一个属性
3. json中的key访问就跟访问对象的属性一样：json对象.key

```js
<script type="text/javascript">
			// json的定义
			var jsonObj = {
				"key1":12,
				"key2":"abc",
				"key3":true,
				"key4":[11,"arr",false],
				"key5":{
					"key5_1" : 551,
					"key5_2" : "key5_2_value"
				},
				"key6":[{
					"key6_1_1":6611,
					"key6_1_2":"key6_1_2_value"
				},{
					"key6_2_1":6621,
					"key6_2_2":"key6_2_2_value"
				}]
			};
			// json的访问
			// alert(jsonObj.key1);//12
			// alert(jsonObj.key2); // abc
			// alert(jsonObj.key3); // true
			// alert(jsonObj.key4);// 得到数组[11,"arr",false]
			// json 中 数组值的遍历
			// for (var i = 0;i<jsonObj.key4.length;i++){
			// 	alert(jsonObj.key4[i]);
			// }
			// alert(jsonObj.key5.key5_1);//551
			// alert(jsonObj.key5.key5_2);//key5_2_value
			// alert( jsonObj.key6 );// 得到json数组\
			// // 取出来每一个元素都是json对象
			// var jsonItem = jsonObj.key6[0];
			// // alert( jsonItem.key6_1_1 ); //6611
			// alert( jsonItem.key6_1_2 ); //key6_1_2_value

			// alert(jsonObj);

			


			// json对象转字符串
			// json字符串转json对象
		</script>
```

### JSON的两个常用方法

* JSON的存在有两种形式
  1. 一种是：对象的形式存在，我们叫他json对象
  2. 字符串的形式存在，我们叫它json字符串
  3. 一般我们要操作json中的数据的时候，需要json对象的格式
  4. 一般我们要在客户端和服务器之间进行数据交换的时候，使用json字符串

* JSON.stringify()   把json对象转换成json字符串
* JSON.parse()       把json字符串转成为json对象

```js
<script type="text/javascript">
			// json的定义
			var jsonObj = {
				"key1":12,
				"key2":"abc",
				"key3":true,
				"key4":[11,"arr",false],
				"key5":{
					"key5_1" : 551,
					"key5_2" : "key5_2_value"
				},
				"key6":[{
					"key6_1_1":6611,
					"key6_1_2":"key6_1_2_value"
				},{
					"key6_2_1":6621,
					"key6_2_2":"key6_2_2_value"
				}]
			};
			// json的访问
			// alert(jsonObj.key1);//12
			// alert(jsonObj.key2); // abc
			// alert(jsonObj.key3); // true
			// alert(jsonObj.key4);// 得到数组[11,"arr",false]
			// json 中 数组值的遍历
			// for (var i = 0;i<jsonObj.key4.length;i++){
			// 	alert(jsonObj.key4[i]);
			// }
			// alert(jsonObj.key5.key5_1);//551
			// alert(jsonObj.key5.key5_2);//key5_2_value
			// alert( jsonObj.key6 );// 得到json数组\
			// // 取出来每一个元素都是json对象
			// var jsonItem = jsonObj.key6[0];
			// // alert( jsonItem.key6_1_1 ); //6611
			// alert( jsonItem.key6_1_2 ); //key6_1_2_value

			// alert(jsonObj);




			// json对象转字符串
			var jsonObjString = JSON.stringify(jsonObj);//特别像java中对象的toString
			alert(jsonObjString);


			// json字符串转json对象
			var jsonObj2 = JSON.parse(jsonObjString);
			alert(jsonObj2.key1);//12
		</script>
```

### JSON 在java 中的使用

#### javaBean 和 json的互转

* toJson()：   	把 java 对象转换成为 json 字符串
* fromJson(String  json , Class<T>)：   把Json字符串转换回Java对象
  * 第一个参数是json 字符串
  * 第二个参数是转换回去的 Java 对象类型

```java
    /**
     * 1. javaBean和json的互转
     */
    @Test
    public void test1(){
        Person person = new Person(1, "wxs");

        //创建Gson对象实例
        Gson gson = new Gson();
        // toJson 方法可以把 java 对象转换成为 json 字符串
        String s = gson.toJson(person);
        System.out.println(s);

        //fromJson 把json字符串转换回Java 对象
        //第一个参数是json 字符串
        //第二个参数是转换回去的 Java 对象类型
        Person person1 = gson.fromJson(s, Person.class);
        System.out.println(person1);
    }
```

#### List 和 Json 的互转

* 需要继承json的jar包中的TypeToken

```java
public class PersonListType extends TypeToken<ArrayList<Person>> {
}
```

```java
  @Test
    public void test2(){
        ArrayList<Person> personArrayList = new ArrayList<>();

        personArrayList.add(new Person(1,"wxs"));
        personArrayList.add(new Person(2,"www"));

        Gson gson = new Gson();

        //把list 转换为 json 字符串
        String personListJsonString = gson.toJson(personArrayList);
        System.out.println(personListJsonString);

        //把json字符串 转换为list数组
        List<Person> list = gson.fromJson(personListJsonString, new PersonListType().getType());

        System.out.println(list);
        Person person = list.get(0);
        System.out.println(person);
    }
```

#### Map 和 Json 的互转

```java
 @Test
    public void test3(){
        HashMap<Integer, Person> personHashMap = new HashMap<>();

        personHashMap.put(1,new Person(1,"wxs"));
        personHashMap.put(2,new Person(2,"www"));

        Gson gson = new Gson();

        //把map集合转换为 json 字符串
        String personJson = gson.toJson(personHashMap);
        System.out.println(personJson);

        // Map<Integer,Person> personMap2 = gson.fromJson(personMapJsonString, new PersonMapType().getType());
        //使用匿名内部类改写，减少类的创建
        HashMap<Integer, Person> personMap2 =   gson.fromJson(personJson,new TypeToken<HashMap<Integer,Person>>(){}.getType());
        System.out.println(personMap2);
        Person p = personMap2.get(1);
        System.out.println(p);


    }
```

