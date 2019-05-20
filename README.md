[TOC]

# css知识点

## 1.空格和换行

### ①white-space

**指定元素内的空白怎样处理**

值：

>  normal | pre | nowrap | pre-wrap | pre-line

+ **normal**：默认处理方式，**合并文本间的空白距离（多个相邻空格合并成一个空格，），tab解析为空格，换行解析为空格，文字超出边界换行**
+ **nowrap**：合并文字间的空白距离，tab和换行解析为空格，文字超出边界不换行

+ **pre**：不合并文字间的空白距离，保留tab，换行解析为tab并换行，文字超出边界时不换行

+ **pre-wrap**：不合并文字间的空白距离，保留tab，换行解析为tab并换行，当文字超出边界时换行

+ **pre-line**：保持文本的**换行**，不保留文字间的空白距离，换行仅解析为换行，文字碰到边界时发生换行

| white-space属性 | 源码空格 | 源码换行 | <br>换行 | 容器边界换行 |
| --------------- | -------- | -------- | -------- | ------------ |
| normal          | 合并     | 忽略     | 换行     | 换行         |
| nowrap          | 合并     | 忽略     | 换行     | 不换行       |
| pre             | 保留     | 换行     | 换行     | 不换行       |
| pre-wrap        | 保留     | 换行     | 换行     | 换行         |
| pre-line        | 合并     | 换行     | 换行     | 换行         |

### ②word-break

**控制单词如何被拆分换行的**

值：

> normal | break-all | keep-all

`word-break:keep-all`：

![image-20190520142516720](../../../Users/lsb/Library/Application Support/typora-user-images/image-20190520142516720.png)

**所有“单词”一律不拆分换行**，注意，我这里的“单词”包括连续的中文字符（还有日文、韩文等），或者可以理解为**只有空格可以触发自动换行**

`word-break:break-all`：

![image-20190520142555154](../../../Users/lsb/Library/Application Support/typora-user-images/image-20190520142555154.png)

**所有单词碰到边界一律拆分换行**，不管你是`incomprehensibilities`这样一行都显示不下的单词，还是`long`这样很短的单词，只要碰到边界，都会被强制拆分换行。所以用`word-break:break-all`时要慎重呀。


这样的效果好像并不太好呀，能不能就把incomprehensibilities拆一下，其它的单词不拆呢？那就需要下面这个属性了

### ③word-wrap（overflow-wrap）

`word-wrap`又叫做`overflow-wrap`：

> word-wrap 属性原本属于微软的一个私有属性，在 CSS3 现在的文本规范草案中已经被重名为 overflow-wrap 。 word-wrap 现在被当作 overflow-wrap 的 “别名”。 稳定的谷歌 Chrome 和 Opera 浏览器版本支持这种新语法。

**这个属性也是控制单词如何被拆分换行的**，实际上是作为`word-break`的互补，它只有两个值：`normal | break-word`，那我们看下`break-word`：

![image-20190520142953044](../../../Users/lsb/Library/Application Support/typora-user-images/image-20190520142953044.png)

终于达到了上文我们希望的效果，**只有当一个单词一整行都显示不下时，才会拆分换行该单词**。
所以我觉得`overflow-wrap`更好理解好记一些，overflow，只有长到溢出的单词才会被强制拆分换行！

（前面的`word-break`属性除了列出的那三个值外，也有个`break-word`值，效果跟这里的`word-wrap:break-word`一样，然而只有Chrome、Safari等部分浏览器支持）

### 总结

最后总结一下三个属性

- white-space，**控制空白字符的显示**，同时还能控制是否自动换行。它有五个值：`normal | nowrap | pre | pre-wrap | pre-line`
- word-break，**控制单词如何被拆分换行**。它有三个值：`normal | break-all | keep-all`
- word-wrap（overflow-wrap）**控制长度超过一行的单词是否被拆分换行**，是`word-break`的补充，它有两个值：`normal | break-word`

下面是本文里所有例子的代码的地址，每个属性做成了选项，方便操作学习~

https://codepen.io/YGYOOO/pen/jvyrWK

注：本文来自<https://juejin.im/post/5b8905456fb9a01a105966b4#heading-2>

2.