<!-- MDTOC maxdepth:6 firsth1:1 numbering:0 flatten:0 bullets:1 updateOnSave:1 -->

- [XAML](#xaml)
   - [Advantages](#advantages)
   - [MyFirstWpfApplication](#myfirstwpfapplication)
      - [Windows1.xaml](#windows1xaml)
      - [App.xaml](#appxaml)
         - [App.xaml](#appxaml)
         - [App.xaml.cs](#appxamlcs)
   - [XAML 语法](#xaml-语法)
      - [TypeConverter](#typeconverter)
            - [操作实例:](#操作实例)
- [来介绍一些容器控件](#来介绍一些容器控件)
   - [Grid](#grid)
- [布... 布局观?](#布-布局观)

<!-- /MDTOC -->

# XAML
Extensible Application Markup Language
可拓展的应用程序标记语句

## Advantages
- 解耦
- 高效
- 其它都是吹水的

## MyFirstWpfApplication


![Resource\cs_wpf_pic_1.png][1]


- **Properties:**
    - 里面主要是程序要用到的一些资源
        - 比如图标, 图片, 静态字符串 和 配置信息
- **References:**
    - 标记了当前项目需要引用哪些其它的项目。
    - 比如 .NET Framework 中的类库
- **App.xaml**
    - 程序的主体
        - 在 Windows 系统里, 一个程序就是一个进程(Process)。
        - Windows 规定, 一个 GUI 进程需要有一个 **窗口**(Window) 作为"主窗口"
    - App.xaml 文件的作用就是声明了程序的进程会是谁, 同时指定了程序的主窗口是谁。
    - App.xaml.cs 对应 App.xaml 的后台代码
    - `App.xaml.cs`: `App.xaml`的后台文件,继承自`System.Window.Application`,用于处理整个WPF应用程序的相关。
- **Window1.xaml**:
    - 在 App.xaml 中被指定的程序主窗口就是它啦~
    - 它同样也有自己的后台代码 Window1.xaml.cs



![Resource\cs_wpf_pic_2.png][2]



### Windows1.xaml
Let us see see the simplest code in xaml
```xml
<Window x:Class="MyFirstWpfApplication.Window1"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             Title="Window1" Height="300" Width="300">
             <Grid>

             </Grid>
</Window>
```

关于`xmlns`定义名称空间:
```xml
xmlns[:可选的映射前缀]="名称空间"
```
在没有写可选映射前缀的情况下, 意味着所有来自于这个名称空间的标签前都不用加前缀,这个没有映射前缀的名称空间称为"默认名称空间"

默认名称空间只能有一个

默认引进来的两个东西拥有一堆中
`"http://schemas.microsoft.com/winfx/2006/xaml/presentation"` 中含有一堆 `System.Windows` 下的类库, 对应的是绘制UI相关的程序集
`"http://schemas.microsoft.com/winfx/2006/xaml"`中则对应一些与 XAML 语法和编译相关的 CLR 名称空间, 是语言层面的东西


形如 `x:Class="xxx"`的xaml文件本质上会在编译过程中生成一个继承自 `Window` 的类
```cs
class xxx:Windows
{
    ...
}
```

> **思考一下, 在一般情况里, 我们的 class 名字和 .xaml.cs 类的名字是相同的, 难道它们不会冲突吗?**
> 这也就是在 .xaml.cs 的类的声明中使用 `partial` 关键字的意义了。
> 使用 `partial` 关键字可以把一个类分拆在多处定义, 只要各部分代码不冲突即可。 显然由 XAML 解析生成的类在声明时也使用了 partial 关键字, 这样, 由 XAML 解析生成的类和 C# 文件里定义的部分就合二为一。



### App.xaml
#### App.xaml

```xml
<Application x:Class="WpfApp1.App"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             StartupUri="MainWindow.xaml">
    <Application.Resource>
        <!-- 系统资源定义区 -->
    </Application.Resource>
</Application>
```

`x:Class="WpfApp1.App"`WPF应用程序的默认命名空间映射
`xmlns="..."` WPF 应用程序的默认命名空间映射
`xmlns:x="..."` XAML映射的扩展命名空间, 通常将其映射为x前缀 `StartupUri` 属性可以指定项目运行时的启动窗体。

#### App.xaml.cs

## XAML 语法
- 创建的 UI 是与 XAML 结构相同的树状结构
    - 两个操作UI树的辅助类:
        - `VisualTreeHelper`
        - `LogicalTreeHelper`
- XAML 是一种声明性的语言
    - XAML 会对每个标签创建一个与之对应的对象
    - XAML 语言不能编写程序的运行逻辑
    - XAML 使用字符串进行简单赋值
    - 或者使用属性元素(Properties Element)进行复杂赋值
    - 区分两种"属性": 使用 Attribute 为 对象的 Property 进行赋值
        - 可以简单理解为 Attribute 对应标签, Properties 对应类
    - 举个例子, 来看看给 `Rectangle` 搞一个 `Fill`标签
        - ```xml
            ...
            <Grid VerticalAlignment="Center" HorizontalAlignment="Center">
                <Rectangle x:Name="rectangle" Width="200" Height="200" Fill="Blue"/>
            </Grid>
            ...
          ```
          ![Resource\cs_wpf_pic_3.png][3]
          "Blue" 这个字符串最终被翻译成一个 `SolidColorBrush` 对象并赋值给了 rectangle 对象, 换成 C# 代码是这样:
          ```cs
            // ...
            SolidColorBrush sBrush = new SolidColorBrush();
            sBrush.Color = Colors.Blue;
            this.rectangle.Fill = sBrush;
            // ...
          ```
- Attribute=Value 这种形式的语法赋值中, 由于 XAML 语法的限制, Value 只能是一个字符串值
    - > **如果一个类能使用 XAML 进行声明,并允许它的 Property 与 XAML 标签的 Attribute 互相映射, 那就需要为这些 Property 准备适当的转换机制**

        - 使用 `TypeConverter` 类的派生类, 在派生类中重写 `TpyeConverter` 的一些方法

    - > **由于 Value 是一个字符串, 所以其格式复杂度有限, 尽管可以在转换机制里包含一定的按格式解析字符串的功能以便转换成较复杂的目标对象, 但这会让最终的 XAML 使用者头疼不已。因为他们不得不在没有编码辅助的情况下手写一个格式复杂的字符串以满足赋值要求**

        - 使用属性元素 (Property Element)

### TypeConverter
将 XAML 标签的 Attribute 与对象的 Property 进行映射

##### 操作实例:

首先我们准备一个类
```cs
public class Human
{
    public string Name {get; set;}
    public Human Child {get; set;}
}
```
现在我们的期望是 如果在XAML里这样写:
```xml
    <Window.Resource>
        <local:Human x:key="Human" Child="ABC"/>
    </Window.Resource>
```
则能够为 Human 实例的 Child 属性赋予一个 Human 类型的值, 并且 Child.Name就是这个这个字符串的值。

先来试试直接写行不行。 在 UI 上添加一个按钮 button1
注册一个点击事件
```cs
private void button1_Click(object sender, RoutedEventArgs e)
{
    Human h = (Human)this.FindResource("human");
    MessageBox.Show(h.Child.Name);
}
```
编译没有问题, 但是在单击按钮之后程序抛出异常, 告诉 Child 不存在。
原因很简单: Human 的 Child 是 Human 类型, 而XAML代码中的 "ABC" 是个字符串, 编译器无法把一个字符串类型转换给一个 Human 实例。

现在我们就需要使用 `TypeConverter` 和 `TypeConverterAttribute` 这两个类了

1. 继承 `TypeConverter` 类, 重写 `ConvertFrom` 方法。 这个方法有一个参数名为 value, 这个值就是在 XAML 文档里为它设置的值, 我们要做的就是讲 value 转型到适合的类型。
```{cs}
public class StringToHumanTypeConverter : TypeConverter
{
    public override object ConvertFrom(ITypeDescriptorContext context, System.Globalization.CultureInfo culture, object value)
    {
        public override object
    }
}
```


# 来介绍一些容器控件
## Grid
- WPF 中的 Grid 的每一个单元格中可以放置多个控件，但控件可能会层叠在一起。
- WPF 中的 Grid 支持单元格的合并，类似于 HTML 中的 table td 中的 rowspan 和 col pan
- Grid 中的行和列可以自定义高度和宽度。
    - `Height ="60"` 不加 “星号” 表示固定高度。
    - `Height="60*"` 加 “星号” 表示加权的高度 ，在调整窗体大小时，此高度和宽度会按照窗体大小改变的比例进行缩放

# 布... 布局观?

1. 控件的布局应该由容器来决定，而不是通过自身使用margin之类的东西来控制位置。
    - 因为这些属性原本应该是控制自己内部展现或与邻里之间关系的；
2. 控件应避免明确的定义具体的尺寸
    - 因为显示器分辨率及windows窗体的大小都有可能随时改变，如果明确的定义尺寸,当窗体变动后就会出现大面积的空白或是缺失。但为了控件功能及效果的展示，应该限定一个可接受的最大及最小尺寸。
    - 通过`MinWidth`, `MinHeight`, `MaxWidth`, `MaxHeight`属性可以实现这一点。
3. 不要将界面元素位置设置成与屏幕坐标相关.
4. 容器应将有效空间共享给其子控件，这也是为了不在窗体调整后，遗留出大块的空余。


---------------------------------------


[1]: ../\\../\\Resource\cs_wpf_pic_1.png
[2]: ../\\../\\Resource\cs_wpf_pic_2.png
[3]: ../\\../\\Resource\cs_wpf_pic_3.png
