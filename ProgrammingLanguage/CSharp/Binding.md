# TypeConverter
将 XAML 标签的 Attribute 与对象的 Property 进行映射

## 操作实例:

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
```cs
public class StringToHumanTypeConverter : TypeConverter
{
    public override object ConvertFrom(ITypeDescriptorContext context, System.Globalization.CultureInfo culture, object value)
    {
        public override object
    }
}
```
