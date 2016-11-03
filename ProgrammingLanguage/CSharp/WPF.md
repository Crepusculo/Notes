

# 文件结构

界面 <= `xxx.xaml` <===> `xxx.xaml.cs` => 界面对应的后台代码文件

特别的: `app.xaml` 设置应用程序的起始文件与资源 `app.xaml.cs`: `app.xaml`的后台文件,继承自`System.Window.Application`,用于处理整个WPF应用程序的相关。

# App.xaml

```{xml}
<Application x:Class="WpfApp1.App"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             StartupUri="MainWindow.xaml">
    <Application.Resource>
        <!-- 系统资源定义区 -->
    </Application.Resource>
</Application>
```

`x:Class="WpfApp1.App"`WPF应用程序的默认命名空间映射 `xmlns="..."` WPF 应用程序的默认命名空间映射 `xmlns:x="..."` XAML映射的扩展命名空间, 通常将其映射为x前缀 `StartupUri` 属性可以指定项目运行时的启动窗体。

## App.xaml

## App.xaml.cs

# 布... 布局观?

- 控件的布局应该由容器来决定，而不是通过自身使用margin之类的东西来控制位置。
    - 因为这些属性原本应该是控制自己内部展现或与邻里之间关系的；
- 控件应避免明确的定义具体的尺寸
    - 因为显示器分辨率及windows窗体的大小都有可能随时改变，如果明确的定义尺寸,当窗体变动后就会出现大面积的空白或是缺失。但为了控件功能及效果的展示，应该限定一个可接受的最大及最小尺寸。
    - 通过`MinWidth`, `MinHeight`, `MaxWidth`, `MaxHeight`属性可以实现这一点。
- 不要将界面元素位置设置成与屏幕坐标相关.
- 容器应将有效空间共享给其子控件，这也是为了不在窗体调整后，遗留出大块的空余。
- 第五条，容器嵌套使用，因为不同的容器，表现效果不同，必要时应结合使用。
