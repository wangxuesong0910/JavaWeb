# XML dom4j使用

* 由于dom4j  不是sun公司的技术，而属于第三方公司的技术，我们需要使用dom4j 就需要到dom4j官网下载 dom4j的jar包

## dom4j编程步骤

1. 先加载xml文件创建Document对象
2. 通过Document对象拿到根元素对象
3. 通过根元素.elements(标签名); 可以返回一个集合，这个集合里放着。所有你指定的标签名的元素对象
4. 找到你想要修改、修改的子元素，进行相应在的操作
5. 保存在硬盘上

## 详细步骤

1. 添加dom4j的jar包 并添加到类路径
2. 需要解析的.xml文件内容
3. 代码实现

```java
/*
* dom4j 获取 Documet 对象
*/
@Test
public void getDocument() throws DocumentException {
// 要创建一个 Document 对象，需要我们先创建一个 SAXReader 对象
SAXReader reader = new SAXReader();
// 这个对象用于读取 xml 文件，然后返回一个 Document。
Document document = reader.read("src/books.xml");
// 打印到控制台，看看是否创建成功
System.out.println(document);
}
```

```java
 @Test
    public void Test3() throws DocumentException {
        //四步操作
        //1. 创建SAXReader对象，用来读取xml文件，获取Document对象
        //2. 通过Document对象，拿到xml的根元素对象
        //3. 通过根元素对象，获取所有的book标签对象
        //4. 遍历每个book标签对象，然后获取到book标签对象内的每一个元素，在通过getText()方法拿到起始标签和结束标签之间的文本

        //1. 操作：创建SAXReader对象用来读取xml文件，获取Document对象
        SAXReader saxReader = new SAXReader();
        Document read = saxReader.read("src/books.xml");

        //2.通过Document对象，拿到xml的根元素对象
        Element rootElement = read.getRootElement();

        //3.通过根元素对象，获取所有的book标签对象
        List<Element> elements = rootElement.elements();

        //4.遍历每个book标签对象，然后获取到book标签对象内的每一个元素，再通过getText（）方法拿到文本
        for (Element e : elements) {
            // 测试
            // System.out.println(book.asXML());
            // 拿到 .xml 下面的元素对象
            Element name = e.element("name");
            Element price = e.element("price");
            Element author = e.element("author");

            // 再通过 getText() 方法拿到起始标签和结束标签之间的文本内容
            System.out.println("书名" + name.getText() + " , 价格:"
                    + price.getText() + ", 作者：" + author.getText());

        }
    }
```

