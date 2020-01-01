---
title: HTML、CSS、JavaScript
date: 2019-8-11 9:21:22
categories: HTML、CSS、Javascript
---
### Web
#### JavaWeb
使用Java开发基于互联网的项目。
#### 软件架构
##### C/S（客户端/服务器端）
- 优点：用户体验好；
- 缺点：开发、安装、部署、维护麻烦。
##### B/S（浏览器/服务器端）
- 优点：开发、安装、部署、维护简单；
- 缺点：对硬件要求高；应用过大时用户体验受到影响。


### B/S资源分类
#### 静态资源
  使用静态网页开发技术发布的资源
- HTMl：用于搭建基础网页，展示页面内容；
- CSS：用于美化页面，布局页面；
- JavaScript：控制页面的元素，添加动态效果。

##### 特点
- 所有用户访问，得到同样的结果；
- eg.HTML、CSS、JavaScript
- 如果用户请求的是静态资源，那么服务器会直接将静态资源发送给浏览器。浏览器内置了静态资源的解析引擎，可以展示静态资源。

#### 动态资源
使用动态网页及时发布的资源
##### 特点
- 用户访问得到的结果可能不一样；
- eg.jsp/servlet,php,asp...
- 如果用户请求动态资源，服务器会将动态资源转换为静态资源，再发送给浏览器。

### HTML
Hyper Text MarkUp Language,超文本标记语言
#### 超文本
用超链接的方法，将各种不同空间的文字信息组织在一起的网状文本
#### 标记语言
由标签构成的语言。<标签名称>，eg.HTML,XML

- 围堵标签：有开始标签和结束标签。eg.<html></html>
- 自闭和标签：开始标签和结束标签在一起。eg. <br/>

#### 标签分类
详细标签链接：[https://www.w3school.com.cn/tags/index.asp](https://www.w3school.com.cn/tags/index.asp)
##### 1.文件标签：构成HTML最基本的标签
| <html> | html文档的根标签 |
| :-: | :-: |
| head | 头标签(指定html属性和引入外部资源) |
| title | 标题标签 |
| body | 体标签 |
| <!DOCTYPE html> | 定义文档格式为html |

##### 2.文本标签：和文本有关的标签

| !-- xx-- | 注释 |
| :-: | :-: |
| p(paragraph) | 段落标签 |
| br(break) | 换行标签 |
| hr | 展示一条水平线（已弃用） |
| b(bold) | 字体加粗 |
| i(italic) | 字体斜体 |
| h1~h6(header) | 标题标签 |
| font | 字体标签 |

##### 3.图片标签
    `<img src="URL">`
- URL用相对路径；
- "./"：
    代表当前目录；
    eg."./image/1.jpg"
- "../":
    代表上一级目录；
    eg."../image/1.jpg"
    
##### 4.列表标签
- 有序列表
   ```
   <!--ol(ordered list)--> 
   <ol>
        <li></li>
    
    </ol>
   ```
    
- 无序列表    
    ```
    <!--ul(Unordered list)-->
    <ul>
        <li></li>
    </ul>
    ```
##### 5.链接标签
    href(hypertext reference)
    <a href="http://baidu.com" target="_blank"></a>    
##### 6.div 和 span
- div：每个div占满一整行。块级标签。
- span：文本信息在一行展示。行内标签/内联标签。

##### 7.语义化标签（HTML5中提供的提高可读性的标签）
```markdown
    <header> 页眉
    <footer> 页脚
```

##### 8.表格标签
| table | 定义表格 |
| :-: | :-: |
| tr(table row) | 定义行 |
| td(table data cell) | 定义单元格 |
| th(table header cell) | 定义表头单元格 |
| caption | 表格标题 |
| thead | 表示表格的头部分 |
| tbody | 表示表格的体部分 |
| tfoot | 表示表格的脚部分 |

#### 表单标签
用于采集用户输入的数据；用于和服务器进行交互。
- form：定义表单，定义的范围代表采集用户数据的范围。
- 表单中的数据想被提交，必须指定其**name属性**。

##### action：指定提交数据的URL

##### method: 指定提交方式

提交方式有7种，2种比较常用。
- get：
    1.请求参数封装在请求行中，会在地址栏中显示；
    2.请求参数大小是有限制的；
    3.不安全。
    
- post：
    1.请求参数封装在请求体中；
    2.请求参数大小无限制；
    3.较为安全。

#### 表单项标签

##### input
可以通过改变type属性值，改变元素展示样式。

###### type属性
- text（默认值）：文本输入框；
- placeholder：输入框的提示信息，输入时提示会被清空；
- password：密码输入框；
- radio：单选框；
    1.想要多个单选框实现单选的效果，例如性别选择，各个单选框的name属性值必须一样；
    2.单选框的value属性值会被提交；
    3.checked属性，可以指定默认选择。
    
- checkbox：复选框；
    1.提交框里的value属性值；
    2.checked属性指定默认值。
- file：文件选择框； 
- hidden：隐藏域，用于提交信息；
- 按钮：
    submit：提交按钮，可以提交表单；
    button：普通按钮；
    image：图片提交按钮。（src属性指定图片的路径）

- label：指定输入的文字描述信息；label的for属性和input的id属性值相同，点击label区域，会让input输入框获取焦点。
    
- select：下拉列表
    子元素：option，指定列表项。
    
- textarea：文本域
    cols：指定列数，即每行字符数，行宽；
    rows：指定行数。
    
```markdown
    <form></form>
    
    eg.
    <form action='#' method="get">
        用户名：<input type="text" name="username" placeholder="请输入用户名"><br>
        密码：<input type="password" name="password"><br>
        性别：<input type="radio" name="gender" value="male" checked> 男
            <input type="radio" name="gender" value="female"> 女
        <br>
        <input type="submit" value="登录">
    
    </form>
    
    
```

### CSS
Cascading Style Sheets,层叠样式表;
多个样式可以作用在同一个html元素上，同时生效。

- 优点
    1.解耦；
    2.更易分工协作；
    3.提高开发效率。
    
#### CSS和HTML结合

##### 1.内联样式
在标签内使用style属性指定CSS代码：
        `<div style="color:red;">hello</div>`

##### 2.内部样式
在head标签内，定义style标签，style标签的标签体内容就是CSS代码：
    ```
        <style>
            div{
                color:red;
            }
        </style>
        <div>hello</div>
    ```

##### 3.外部样式
1.定义CSS资源文件
2.在head标签内，定义link标签，引入外部的资源文件；
```markdown
    a.css文件：
        div{
            color:red;
        }

    <link rel="stylesheet" href="css/a.css">
    <div>hello</div>
```

#### CSS语法
    选择器{
        属性名1：属性值1；
        属性名2：属性值2；
    }
##### 选择器
筛选具有相似特征的元素
###### 基础选择器
- 1.id选择器
选择具体的相等id属性值的元素；
        语法：
            #id属性值{}
- 2.元素选择器
选择具有相同标签名称的元素；
        语法：
            标签名称{}
- 3.类选择器
选择具有相同的class属性值的元素；
        语法：
            .class属性值{}

- 优先级：
    id>类>元素                

###### 扩展选择器
- 1.选择所有元素:
        语法：
            *{}
- 2.并集选择器:
        语法：
            选择器1，选择器2{}
- 3.子选择器:筛选选择器1元素下的选择器2元素
        语法：
            选择器1 选择器2{}
- 4.父选择器:筛选选择器2的父元素选择器1
        语法：
            选择器1>选择器2{}
- 5.属性选择器:选择元素名称，属性名=属性值的元素
        语法：
            元素名称[属性名=“属性值”]
- 6.伪选择器:选择一些元素具有的状态
        语法：
            元素：状态{}
        eg.
            link：初始化的状态；
            visited：访问过的状态；
            active：正在访问的状态；
            hover：鼠标悬浮状态。                

#### 属性

##### 文本
            
- font-size：字体大小；
- color：字体颜色；
- text-align：对齐方式；
- line-height：行高。

##### 背景
- background

##### 边框
- border

##### 尺寸
- width
- height

##### 盒子模型：控制布局
- margin：外边距
- padding：内边框，默认情况下内边距会影响整个盒子大小；
            box-sizing：border-box；设置盒子属性，让width和height就是最终盒子的大小。
    
- float：浮动
        left    
        right    
    

### JavaScript
- 客户端脚本语言，不需要编译，直接解析执行；
- 运行在客户端浏览器中，每个浏览器都有JavaScript的解析引擎；
- 增强交互功能，添加页面动态效果。
JavaScript = ECMAScript + JavaScript(BOM + DOM)

#### ECMAScript

##### 与HTML结合方式

    <script>可以定义在html页面任何地方，但是定义的位置决定执行顺序。
###### 内部JS
    定义<script>，标签内容就是JS代码； 
###### 外部JS
    定义<script>，通过src属性引入外部的JS文件。
    
    
##### 数据类型    
###### 原始（基本）数据类型
- 1.number：
    数字。整数/小数/NAN(not a number)
- 2.string:
    字符串
- 3.boolean：
    true/false
- 4.null:                
    一个对象为空的占位符
- 5.undefined：
    未定义。如果一个变量没有给初始化值，则会被默认赋值为undefined。    

###### 引用数据类型
- 对象

##### 变量
- 一小块存储数据的内存空间；
- Java是强类型语言，而JavaScript是弱类型语言：
    强类型：开辟变量存储空间时，定义和规定了空间存储的数据类型；
    弱类型：开辟存储空间时，不定义存储数据类型，可以存放任意类型的数据。
        语法：
            var 变量名 = 初始化值;
            var定义的变量为局部变量；不用var定义的为全局变量。
            
            typeof运算符：获取变量的类型；
            null的类型为object；
            
            
##### 对象
- **Function：方法对象**
    1.创建：
        1.function 方法名称(形参列表){
            方法体
           }
        
        2.var 方法名 = function(){
            方法体
        }     
    
    2.特点：
        1.形参类型和返回值类型不用指定；
        2.方法是一个对象，名称相同的方法会被覆盖；
        3.在JS中，方法的调用只考虑方法名，参数列表不影响；
        4.方法内置对象数组，arguments，封装了所有实际参数；
        
    3.调用：
        方法名称（实际参数列表）
        
- **Array：数组对象**
    1.创建：
        1.var arr = new Array(元素列表)；
        2.var arr = new Array(默认长度)；
        3.var arr = [ 元素列表 ]；
        
    2.方法
        join(参数)：将数组中的元素按照指定的分隔符拼接为字符串；
        push()：向数组的末尾添加元素，并返回新的长度。
        
    3.特点：
        JS中，数组元素的类型可变；长度可变。
                                
- **RegExp：正则表达式对象**
    1.正则表达式：定义字符串的组成规则。
        1.单个字符：[]
            \d: 单个数字字符[0-9]
            \w: 单个单词字符[a-z A-Z 0-9]
        
        2.量词符号：
            ?: 表示出现0次或1次
            *：表示出现0次或多次
            +：出现1次或多次
            
            {m,n}：表示 m<= 数量 <=n            
        
        3.开始结束符号
            ^: 开始
            $: 结束
        
    2.正则对象：
        1.创建
            1.var reg = new RegExp("正则表达式");
            
            2.var reg = /正则表达式/;
        2.方法：
            test(参数)：验证参数字符串是否符号正则表达式；    
                                            
- **Global：全局对象**

1.特点：封装的方法不需要对象可以直接调用。  方法名()

2.方法：
            encodeURI：URL编码
            decodeURI：URL解码
            
            encodeURIComponent：URI编码，编码的字符更多
            decodeURIComponent：URI解码


3.URL编码

URI > URL 

编码：1个字节为单位，将4位二进制转为16进制。单位之间用%分隔。
                
            
#### BOM
Browser Object Model 浏览器对象模型
##### 组成
###### Window：窗口对象
**方法：**
- 1.与弹出框有关的方法：
        alert() 显示带有消息和一个确认按钮的警告框；
        confirm() 显示带有消息、确认和取消按钮的对话框，点击确认按钮返回true，点击取消按钮返回false。
        prompt() 显示可提示用户输入的对话框；返回输入的值

- 2.与打开关闭有关的方法：
        close() 关闭浏览器窗口
        open() 打开一个新的浏览器窗口
        
- 3.与定时器有关的方式
        setTimeout() 在指定的毫秒数后调用函数或计算表达式
        clearTimeout() 取消setTimeout()方法；
        
        setInterval() 按照指定的周期来调用函数或者计算表达式；
        clearInterval() 取消有setInterval设置的timeout。

**属性：**

- 1.获取其他BOM对象
    History、Location、Navigator、Screen
- 2.获取DOM对象        
    document                                         
    
###### Navigator：浏览器对象
###### Screen：显示器屏幕对象
###### History：历史记录对象

###### Location：地址栏对象
Location对象包含当前URL的信息，是Window对象的一部分，可以通过window.location访问。

#### DOM
Document Object Model 文档对象模型
- 功能 
    1.控制HTML文档的内容。
    2.代码：
        document.getElementById(id)
        
            


将标记语言文档的各个组成部分封装为对象，使用这些对象，对标记语言文档进行CRUD操作。



W3C DOM 标准：
- 1.核心DOM：针对任何结构化文档的标准模型
        Document：文档对象
        Element：元素对象
        Attribute：属性对象
        Text：文本对象
        Comment：注释对象
                    
        Node：节点对象，其他5个的父对象。                    
- 2.XML DOM：针对XML文档的标准模型            
- 3.HTML DOM：针对HTML文档的标准模型    

##### 核心DOM模型
###### Document对象
- 1.创建（获取）：在HTML Dom模型中可以使用window对象来获取
    1.window.document
    2.document
- 2.方法：
    1.获取Element对象：
        1.getElementById(): 根据id属性值获取元素对象。id唯一。            
        2.getElementByTagName(): 根据元素名称获取元素对象们。返回一个数组。            
        3.getElementByClassName(): 根据Class属性值获取元素对象们。返回一个数组。            
        4.getElementByName(): 根据name属性值获取元素对象们。返回一个数组。
        
###### Element对象
- 1.创建：通过Document来获取和创建
- 2.方法：
        1.removeAttribute(): 删除属性        
        2.setAttribute(): 设置属性        
                    
###### Node 对象

节点对象代表文档树中的一个节点。元素节点、属性节点、文本节点等。

- 所有DOM对象都可以认为是一个节点；
- 方法：
    CRUD dom树：
        appendChild(): 向节点的子节点列表的结尾添加新的子节点；
        removeChild(): 删除当前节点的指定子节点；
        replaceChild()：用新节点替换一个子节点。
        
        parentNode()： 返回节点的父节点。

##### HTML DOM模型
- 1.标签体的设置和获取：
        innerHTML
        
- 2.使用html元素对象的属性；

- 3.控制样式

##### 事件监听机制
某些组件被执行了某些操作后，触发某些代码的执行。

- 事件：某些操作。eg. 单击
- 事件源：组件。eg. 按钮，文本输入框
- 监听器：代码。
- 注册监听：将事件，事件源，监听器结合在一起。

###### 事件
- **1.点击事件**
        1.onclick：单击
        2.ondblclick：双击
        
- **2.焦点事件**
        1.onblur：失去焦点
        2.onfocus：获取焦点
        
- **3.加载事件**
        1.onload：一张页面或图像完成加载
        
- **4.鼠标事件**
        1.onmousedown 鼠标按钮被按下
        2.onmouseup 鼠标按钮被松开
        2.onmouseover 鼠标移到元素上
        2.onmouseout 鼠标移出元素
                            
- **5.键盘事件**
        1.onkeydown 某个键盘按键被按下
        2.onkeyup 某个键盘按键被松开
        3.onkeypress 某个键盘按键被按下并松开

- **6.选择和改变**
        1.onchange 域的内容被改变
        2.onselect 文本被选中

- **7.表单事件**
        1.onsubmit：确认按钮被点击
        2.onreset：重置按钮被点击
