<!-- MDTOC maxdepth:6 firsth1:1 numbering:0 flatten:0 bullets:1 updateOnSave:1 -->

- [什么是 XML?](#什么是-xml)
- [XML 与 HTML 的主要差异](#xml-与-html-的主要差异)
- [XML 的用途](#xml-的用途)
- [XML 语法规则](#xml-语法规则)
   - [所有XML元素都须有关闭标签](#所有xml元素都须有关闭标签)
   - [XML 标签对大小写敏感](#xml-标签对大小写敏感)
   - [XML 必须正确地嵌套](#xml-必须正确地嵌套)
   - [XML 文档必须有根元素](#xml-文档必须有根元素)
   - [XML 的属性值须加引号](#xml-的属性值须加引号)
   - [实体引用](#实体引用)
   - [XML 中的注释](#xml-中的注释)
   - [在 XML 中，空格会被保留](#在-xml-中，空格会被保留)
   - [XML 以 LF 存储换行](#xml-以-lf-存储换行)
- [XML 元素](#xml-元素)
- [XML 命名规则](#xml-命名规则)
- [XML 属性](#xml-属性)
- [XML 验证](#xml-验证)
- [XML 验证 (DTD)](#xml-验证-dtd)
   - [从外部文档声明](#从外部文档声明)
   - [XML 文档构建模块](#xml-文档构建模块)
      - [声明一个元素](#声明一个元素)
      - [声明属性](#声明属性)
      - [声明一个实体](#声明一个实体)
      - [两个实例](#两个实例)
- [XML 验证 (XML Schema)](#xml-验证-xml-schema)
   - [Better than DTD:](#better-than-dtd)
   - [`<schema>` 元素](#schema-元素)
      - [简易元素](#简易元素)
      - [属性](#属性)
      - [限定 / Facets](#限定-facets)

<!-- /MDTOC -->
# 什么是 XML?
- XML 指__可扩展标记语言（EXtensible Markup Language）__
- XML 是一种__标记语言__，很类似 HTML
- XML 的设计宗旨是__传输数据__，而非显示数据
- XML 标签没有被预定义。您需要自行定义标签。
- XML 被设计为具有__自我描述性。__
- XML 是 W3C 的推荐标准

Extensible Markup Language标记语言类似HTML 标签未自定义 传输数据 __自我描述性__

# XML 与 HTML 的主要差异
XML 不是 HTML 的替代。
XML 和 HTML 为不同的目的而设计：
XML 被设计为传输和存储数据，其焦点是数据的内容。
HTML 被设计用来显示数据，其焦点是数据的外观。
HTML 旨在显示信息，而 XML 旨在传输信息。

__XML 是不作为的。__
__XML 仅仅是纯文本__

# XML 的用途
+ __XML 把数据从 HTML 分离__
数据能够存储在独立的 XML 文件中。读取一个外部 XML 文件，然后更新 HTML 中的数据内容。
+ __XML 简化数据共享__
XML 提供了一种独立于软件和硬件的数据存储方法。
+ __XML 简化数据传输__
通过 XML，可以在不兼容的系统之间轻松地交换数据。
+ __XML 简化平台的变更__
XML 数据以文本格式存储。
+ __XML 使您的数据更有用__
由于 XML 独立于硬件、软件以及应用程序，XML 使您的数据更可用，也更有用。
+ __XML 用于创建新的 Internet 语言__
很多新的 Internet 语言是通过 XML 创建的：
XHTML - 最新的 HTML 版本
    WSDL - 用于描述可用的 web service
    WAP 和 WML - 用于手持设备的标记语言
    RSS - 用于 RSS feed 的语言
    RDF 和 OWL - 用于描述资源和本体
    SMIL - 用于描述针针对 web 的多媒体

# XML 语法规则
## 所有XML元素都须有关闭标签
在 HTML，经常会看到没有关闭标签的元素：
```html
<p>This is a paragraph
<p>This is another paragraph
```
在 XML 中，省略关闭标签是非法的。所有元素都必须有关闭标签：
```xml
<p>This is a paragraph</p>
<p>This is another paragraph</p>
```
注释：您也许已经注意到 XML 声明没有关闭标签。这不是错误。声明不属于 XML 本身的组成部分。它不是 XML 元素，也不需要关闭标签。
## XML 标签对大小写敏感
## XML 必须正确地嵌套
## XML 文档必须有根元素
## XML 的属性值须加引号
与 HTML 类似，XML 也可拥有属性（名称 / 值的对）。
在 XML 中，XML 的属性值须加引号。请研究下面的两个 XML 文档。第一个是错误的，第二个是正确的：
```xml
<note date=08/08/2008>
<to>George</to>
<from>John</from>
</note>
```
```xml
<note date="08/08/2008">
<to>George</to>
<from>John</from>
</note>
```
在第一个文档中的错误是，note 元素中的 date 属性没有加引号。
## 实体引用
在 XML 中，一些字符拥有特殊的意义。
如果你把字符 "<" 放在 XML 元素中，会发生错误，这是因为解析器会把它当作新元素的开始。
这样会产生 XML 错误：
```xml
<message>if salary < 1000 then</message>
```
为了避免这个错误，请用实体引用来代替 "<" 字符：
```xml
<message>if salary &lt; 1000 then</message>
```
在 XML 中，有 5 个预定义的实体引用：
| 预定义  | 引用  | 释义
|---|---|---|
| `&lt;`  |	< |	小于
| `&gt;`  |	> |	大于
| `&amp;` |	& | 和号
| `&apos;`|	' |	单引号
| `&quot;`|	" |	引号

注释：在 XML 中，只有字符 "<" 和 "&" 确实是非法的。大于号是合法的，但是用实体引用来代替它是一个好习惯。
## XML 中的注释
在 XML 中编写注释的语法与 HTML 的语法很相似：
```xml
<!-- This is a comment -->
```
## 在 XML 中，空格会被保留
HTML 会把多个连续的空格字符裁减（合并）为一个：
```html
HTML:	Hello           my name is David.
输出:	Hello my name is David.
```
在 XML 中，文档中的空格不会被删节。

## XML 以 LF 存储换行
在 Windows 应用程序中，换行通常以一对字符来存储：回车符 (CR) 和换行符 (LF)。这对字符与打字机设置新行的动作有相似之处。在 Unix 应用程序中，新行以 LF 字符存储。而 Macintosh 应用程序使用 CR 来存储新行。

# XML 元素
XML 元素指的是从（且包括）开始标签直到（且包括）结束标签的部分。
元素可包含其他元素、文本或者两者的混合物。元素也可以拥有属性。
# XML 命名规则
XML 元素必须遵循以下命名规则：
名称可以含字母、数字以及其他的字符
__名称不能以数字或者标点符号开始__
__名称不能以字符 “xml”（或者 XML、Xml）开始__
__名称不能包含空格__
可使用任何名称，没有保留的字词。
# XML 属性
XML 属性必须加引号
属性值必须被引号包围，不过单引号和双引号均可使用。比如一个人的性别，person 标签可以这样写：
```xml
<person sex="female">
```
或者这样也可以：
```xml
<person sex='female'>
```
注释：如果属性值本身包含双引号，那么有必要使用单引号包围它，就像这个例子：
```xml
<gangster name='George "Shotgun" Ziegler'>
```
或者可以使用实体引用：
```xml
<gangster name="George &quot;Shotgun&quot; Ziegler">
```
# XML 验证
此文件包含对 DTD 的引用：
```xml
<?xml version="1.0"?>
<!DOCTYPE note SYSTEM "http://www.w3school.com.cn/dtd/note.dtd">
<note>
<to>George</to>
<from>John</from>
<heading>Reminder</heading>
<body>Don't forget the meeting!</body>
</note>
```
此文件包含对 XML Schema 的引用：
```xml
<?xml version="1.0"?>
<note
xmlns="http://www.w3school.com.cn"
xmlns:xsd="http://www.w3.org/2001/XMLSchema-instance"
xsd:schemaLocation="http://www.w3school.com.cn note.xsd">

<to>George</to>
<from>John</from>
<heading>Reminder</heading>
<body>Don't forget the meeting!</body>
</note>
```
# XML 验证 (DTD)
拥有正确语法的 XML 被称为 “形式良好” 的 XML。
通过 DTD 验证的 XML 是 “合法” 的 XML。

内部的 DOCTYPE 声明
假如 DTD 被包含在您的 XML 源文件中，它应当通过下面的语法包装在一个 DOCTYPE 声明中：
<!DOCTYPE 根元素 [元素声明]>

带有 DTD 的 XML 文档实例：

```xml
<?xml version="1.0"?>
<!DOCTYPE note [
  <!ELEMENT note (to,from,heading,body)>
  <!ELEMENT to      (#PCDATA)>
  <!ELEMENT from    (#PCDATA)>
  <!ELEMENT heading (#PCDATA)>
  <!ELEMENT body    (#PCDATA)>
]>
<note>
  <to>George</to>
  <from>John</from>
  <heading>Reminder</heading>
  <body>Don't forget the meeting!</body>
</note>
```
## 从外部文档声明
假如 DTD 位于 XML 源文件的外部，那么它应通过下面的语法被封装在一个 DOCTYPE 定义中：
```xml
<!DOCTYPE 根元素 SYSTEM "文件名">
```
这个 XML 文档和上面的 XML 文档相同，但是拥有一个外部的 DTD:
```xml
<?xml version="1.0"?>
<!DOCTYPE note SYSTEM "note.dtd">
<note>
<to>George</to>
<from>John</from>
<heading>Reminder</heading>
<body>Don't forget the meeting!</body>
</note>
```
这是包含 DTD 的 "note.dtd" 文件：
```xml
<!ELEMENT note (to,from,heading,body)>
<!ELEMENT to (#PCDATA)>
<!ELEMENT from (#PCDATA)>
<!ELEMENT heading (#PCDATA)>
<!ELEMENT body (#PCDATA)>
```
## XML 文档构建模块
所有的 XML 文档（以及 HTML 文档）均由以下简单的构建模块构成：
- __元素__
- __属性__
- __实体__
- __PCDATA__
- __CDATA__

下面是每个构建模块的简要描述。
__元素__
>像`<message></message>`这样的
```xml
<body>body text in between</body>
<message>some message in between</message>
```
__属性__
> 属性总是被置于某元素的开始标签中。属性总是以名称 / 值的形式成对出现的。下面的 "img" 元素拥有关于源文件的额外信息：
```xml
<img src="computer.gif" />
```
__实体__
>实体是用来定义普通文本的变量。实体引用是对实体的引用。

__PCDATA__
>PCDATA 的意思是被解析的字符数据（parsed character data）。
可把字符数据想象为 XML 元素的开始标签与结束标签之间的文本。
PCDATA 是__会被解析器解析的文本__。这些文本将被解析器检查实体以及标记。
文本中的标签会被当作标记来处理，而实体会被展开。
不过，被解析的字符数据不应当包含任何 &、<或者> 字符；需要使用 &amp;、&lt; 以及 &gt; 实体来分别替换它们。

__CDATA__
>CDATA 的意思是字符数据（character data）。
CDATA 是__不会被解析器解析的文本__。在这些文本中的标签不会被当作标记来对待，其中的实体也不会被展开。
### 声明一个元素
```xml
<!ELEMENT 元素名称 类别>
```
```xml
<!ELEMENT 元素名称 (元素内容)>
```
__声明一个空元素__
```xml
<!ELEMENT 元素名称 EMPTY>
```
例子：
```xml
<!ELEMENT br EMPTY>
```
XML 例子：
```xml
<br />
```
__声明一个只有 PCDATA 的元素__
```xml
<!ELEMENT 元素名称 (#PCDATA)>
```
例子：
```xml
<!ELEMENT from (#PCDATA)>
```
__声明一个带有任何内容的元素__
```xml
<!ELEMENT 元素名称 ANY>
```
例子：
```xml
<!ELEMENT note ANY>
```
__声明有子元素（序列）的元素__
```xml
<!ELEMENT 元素名称 (子元素名称 1)>
```
```xml
<!ELEMENT 元素名称 (子元素名称 1,子元素名称 2,.....)>
```
例子：
```xml
<!ELEMENT note (to,from,heading,body)>
```
当子元素按照由逗号分隔开的序列进行声明时，这些子元素必须按照相同的顺序出现在文档中。在一个完整的声明中，子元素也必须被声明，同时子元素也可拥有子元素。"note" 元素的完整声明是：
```xml
<!ELEMENT note (to,from,heading,body)>
<!ELEMENT to      (#PCDATA)>
<!ELEMENT from    (#PCDATA)>
<!ELEMENT heading (#PCDATA)>
<!ELEMENT body    (#PCDATA)>
```

__声明只出现一次的元素__
```
<!ELEMENT 元素名称 (子元素名称)>
```
例子：
```
<!ELEMENT note (message)>
```
上面的例子声明了：message 子元素必须出现一次，并且必须只在 "note" 元素中出现一次。
__声明最少出现一次的元素__
```
<!ELEMENT 元素名称 (子元素名称+)>
```
例子：
```
<!ELEMENT note (message+)>
```
上面的例子中的加号声明了：message 子元素必须在 "note" 元素内出现至少一次。
__声明出现零次或多次的元素__
```
<!ELEMENT 元素名称 (子元素名称*)>
```
例子：
```
<!ELEMENT note (message*)>
```
上面的例子中的星号声明了：子元素 message 可在 "note" 元素内出现零次或多次。
__声明出现零次或一次的元素__
```
<!ELEMENT 元素名称 (子元素名称?)>
```

例子：
```
<!ELEMENT note (message?)>
```

上面的例子中的问号声明了：子元素 message 可在 "note" 元素内出现零次或一次。

__声明 “非.../ 既...” 类型的内容__
例子：
```
<!ELEMENT note (to,from,header,(message|body))>
```

上面的例子声明了："note" 元素必须包含 "to" 元素、"from" 元素、"header" 元素，以及非 "message" 元素既 "body" 元素。
__声明混合型的内容__
例子：
```
<!ELEMENT note (#PCDATA|to|from|header|message)*>
```

上面的例子声明了："note" 元素可包含出现零次或多次的 PCDATA、"to"、"from"、"header" 或者 "message"。
### 声明属性
声明属性
属性声明使用下列语法：
```xml
<!ATTLIST 元素名称 属性名称 属性类型 默认值>
```
```
<!ATTLIST 元素名称 属性名称 属性类型 #IMPLIED|#REQUIRED|#FIXED>
```
|  值 | 解释  |
|---|---|
| 值	|属性的默认值
| #REQUIRED|	属性值是必需的
| #IMPLIED|	属性不是必需的
| #FIXED value|	属性值是固定的

以下是 __属性类型__ 的选项：
| 类型 |描述|
|---|---|
| CDATA |	值为字符数据 (character data)
| <p>```(en1 竖线 en2 竖线 ..)```</p>	| 此值是枚举列表中的一个值
| ID	| 值为唯一的 id
| IDREF	| 值为另外一个元素的 id
| IDREFS	| 值为其他 id 的列表
| NMTOKEN	| 值为合法的 XML 名称
| NMTOKENS	| 值为合法的 XML 名称的列表
| ENTITY	| 值是一个实体
| ENTITIES	| 值是一个实体列表
| NOTATION	| 此值是符号的名称
| xml:	| 值是一个预定义的 XML 值

DTD 实例:
```xml
<!ATTLIST payment type CDATA "check">
<!ATTLIST payment company CDATA #FIXED "microsoft">
<!ATTLIST payment salary CDATA (melon|coda)>
```
XML 实例:
```xml
<payment type="check" />
```
### 声明一个实体
实体是用于定义引用普通文本或特殊字符的快捷方式的变量。
实体引用是对实体的引用。
实体可在内部或外部进行声明。
__一个内部实体声明__
语法：
```
<!ENTITY 实体名称 "实体的值">
```
例子：
DTD 例子:
```xml
<!ENTITY writer "Bill Gates">
<!ENTITY copyright "Copyright W3School.com.cn">
```
XML 例子:
```xml
<author>&writer;&copyright;</author>
```
注释: 一个实体由三部分构成: 一个和号 (&), 一个实体名称, 以及一个分号 (;)。

一个外部实体声明
语法：
```
<!ENTITY 实体名称 SYSTEM "URI/URL">
```
例子：
DTD 例子:
```
<!ENTITY writer SYSTEM "http://www.w3school.com.cn/dtd/entities.dtd">
<!ENTITY copyright SYSTEM "http://www.w3school.com.cn/dtd/entities.dtd">
```
XML 例子:
```xml
<author>&writer;&copyright;</author>
```
### 两个实例
http://www.w3school.com.cn/dtd/dtd_examples.asp
更多实例, 尽在W3school

```xml
<!DOCTYPE TVSCHEDULE [

<!ELEMENT TVSCHEDULE (CHANNEL+)>
<!ELEMENT CHANNEL (BANNER,DAY+)>
<!ELEMENT BANNER (#PCDATA)>
<!ELEMENT DAY (DATE,(HOLIDAY|PROGRAMSLOT+)+)>
<!ELEMENT HOLIDAY (#PCDATA)>
<!ELEMENT DATE (#PCDATA)>
<!ELEMENT PROGRAMSLOT (TIME,TITLE,DESCRIPTION?)>
<!ELEMENT TIME (#PCDATA)>
<!ELEMENT TITLE (#PCDATA)>
<!ELEMENT DESCRIPTION (#PCDATA)>

<!ATTLIST TVSCHEDULE NAME CDATA #REQUIRED>
<!ATTLIST CHANNEL CHAN CDATA #REQUIRED>
<!ATTLIST PROGRAMSLOT VTR CDATA #IMPLIED>
<!ATTLIST TITLE RATING CDATA #IMPLIED>
<!ATTLIST TITLE LANGUAGE CDATA #IMPLIED>

]>
```
# XML 验证 (XML Schema)

XML Schema 是基于 XML 的 DTD 替代者。
XML Schema 描述 XML 文档的结构。
XML Schema 语言也称作 XML Schema 定义（XML Schema Definition，XSD）。

## Better than DTD:
XML Schema 最重要的能力之一就是对数据类型的支持。
XML Schema 使用 XML 语法
XML Schema 可扩展
XML Schema 可保护数据通信

## `<schema>` 元素
`<schema>` 元素是每一个 XML Schema 的根元素。
```xml
<?xml version="1.0"?>

<xs:schema>

...
...

</xs:schema>
```
<schema> 元素可包含属性。一个 schema 声明往往看上去类似这样：
```xml
<?xml version="1.0"?>

<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
targetNamespace="http://www.w3school.com.cn"
xmlns="http://www.w3school.com.cn"
elementFormDefault="qualified">

...
...
</xs:schema>
```
代码解释：
下面的片断：
`xmlns:xs="http://www.w3.org/2001/XMLSchema"`
显示 schema 中用到的元素和数据类型来自命名空间 "http://www.w3.org/2001/XMLSchema"。同时它还规定了来自命名空间 "http://www.w3.org/2001/XMLSchema" 的元素和数据类型应该使用前缀 `xs`：

这个片断：
`targetNamespace="http://www.w3school.com.cn"`
显示被此 schema 定义的元素 (note, to, from, heading, body) 来自命名空间： "http://www.w3school.com.cn"。

这个片断：
`xmlns="http://www.w3school.com.cn" `
指出默认的命名空间是 "http://www.w3school.com.cn"。

这个片断：
`elementFormDefault="qualified"`
指出任何 XML 实例文档所使用的且在此 schema 中声明过的元素必须被命名空间限定。

在XML中使用:
在 XML 文档中引用 Schema
此 XML 文档含有对 XML Schema 的引用：
```xml
<?xml version="1.0"?>

<note xmlns="http://www.w3school.com.cn"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://www.w3school.com.cn note.xsd">

<to>George</to>
<from>John</from>
<heading>Reminder</heading>
<body>Don't forget the meeting!</body>
</note>
```
代码解释：
下面的片断：
`xmlns="http://www.w3school.com.cn" `
规定了默认命名空间的声明。此声明会告知 schema 验证器，在此 XML 文档中使用的所有元素都被声明于 "http://www.w3school.com.cn" 这个命名空间。

一旦您拥有了可用的 XML Schema 实例命名空间：
`xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" `
您就可以使用 schemaLocation 属性了。此属性有两个值。第一个值是需要使用的命名空间。第二个值是供命名空间使用的 XML schema 的位置：
`xsi:schemaLocation="http://www.w3school.com.cn note.xsd"`

### 简易元素
XML Schema 可定义 XML 文件的元素。
简易元素指那些只包含文本的元素。它不会包含任何其他的元素或属性。
不过，“仅包含文本” 这个限定却很容易造成误解。文本有很多类型。它可以是 XML Schema 定义中包括的类型中的一种（布尔、字符串、数据等等），或者它也可以是您自行定义的定制类型。

定义简易元素
定义简易元素的语法：
```xml
<xs:element name="xxx" type="yyy"/>
```
此处 xxx 指元素的名称，yyy 指元素的数据类型。XML Schema 拥有很多内建的数据类型。
最常用的类型是：
xs:string
xs:decimal
xs:integer
xs:boolean
xs:date
xs:time
例子：
这是一些 XML 元素：
```xml
<lastname>Smith</lastname>
<age>28</age>
<dateborn>1980-03-27</dateborn>
```
这是相应的简易元素定义：
```xml
<xs:element name="lastname" type="xs:string"/>
<xs:element name="age" type="xs:integer"/>
<xs:element name="dateborn" type="xs:date"/>
```

__简易元素的默认值和固定值__
简易元素可拥有指定的默认值或固定值。
当没有其他的值被规定时，默认值就会自动分配给元素。
在下面的例子中，缺省值是 "red"：
```xml
<xs:element name="color" type="xs:string" default="red"/>
```
固定值同样会自动分配给元素，并且您无法规定另外一个值。
在下面的例子中，固定值是 "red"：
```xml
<xs:element name="color" type="xs:string" fixed="red"/>
```
### 属性
__所有的属性均作为简易类型来声明。__
简易元素无法拥有属性。假如某个元素拥有属性，它就会被当作某种复合类型。但是属性本身总是作为简易类型被声明的。
```xml
<xs:attribute name="xxx" type="yyy"/>
```
__属性的默认值和固定值__
属性可拥有指定的默认值或固定值。
当没有其他的值被规定时，默认值就会自动分配给元素。
在下面的例子中，缺省值是 "EN"：
```xml
<xs:attribute name="lang" type="xs:string" default="EN"/>
```
固定值同样会自动分配给元素，并且您无法规定另外的值。
在下面的例子中，固定值是 "EN"：
```xml
<xs:attribute name="lang" type="xs:string" fixed="EN"/>
```
__可选的和必需的属性__
在缺省的情况下，属性是可选的。如需规定属性为必选，请使用 "use" 属性：
```xml
<xs:attribute name="lang" type="xs:string" use="required"/>
```

### 限定 / Facets
__对值的限定__
下面的例子定义了带有一个限定且名为 "age" 的元素。age 的值不能低于 0 或者高于 120：
```xml
<xs:element name="age">

<xs:simpleType>
  <xs:restriction base="xs:integer">
    <xs:minInclusive value="0"/>
    <xs:maxInclusive value="120"/>
  </xs:restriction>
</xs:simpleType>

</xs:element>
```
__枚举 对一组值的限定__
如需把 XML 元素的内容限制为一组可接受的值，我们要使用枚举约束（enumeration constraint）。
下面的例子定义了带有一个限定的名为 "car" 的元素。可接受的值只有：Audi, Golf, BMW：
```xml
<xs:element name="car">

<xs:simpleType>
  <xs:restriction base="xs:string">
    <xs:enumeration value="Audi"/>
    <xs:enumeration value="Golf"/>
    <xs:enumeration value="BMW"/>
  </xs:restriction>
</xs:simpleType>

</xs:element>
```
上面的例子也可以被写为：
```xml
<xs:element name="car" type="carType">
...
</xs:element>

<xs:simpleType name="carType">
  <xs:restriction base="xs:string">
    <xs:enumeration value="Audi"/>
    <xs:enumeration value="Golf"/>
    <xs:enumeration value="BMW"/>
  </xs:restriction>
</xs:simpleType>
```
__模式约束__
```xml
<xs:element name="initials">

<xs:simpleType>
  <xs:restriction base="xs:string">
    <xs:pattern value="[A-Z][A-Z][A-Z]"/>
  </xs:restriction>
</xs:simpleType>

</xs:element>
```
__对空白字符的限定__
```xml
<xs:element name="address">

<xs:simpleType>
  <xs:restriction base="xs:string">
    <xs:whiteSpace value="preserve"/>
  </xs:restriction>
</xs:simpleType>

</xs:element>
```
如果 whiteSpace 被设置为 "replace"，意味着 XML 处理器将移除所有空白字符（换行、回车、空格以及制表符）

如果 whiteSpace 被设置为 "collapse"，意味着 XML 处理器将移除所有空白字符（换行、回车、空格以及制表符会被替换为空格，开头和结尾的空格会被移除，而多个连续的空格会被缩减为一个单一的空格）

如果 whiteSpace 限定被设置为 "preserve"，这意味着 XML 处理器不会移除任何空白字符

## 复合元素
