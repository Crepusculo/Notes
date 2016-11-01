

# 文件结构
界面 <= `xxx.xaml` <===> `xxx.xaml.cs` => 界面对应的后台代码文件

特别的:
`app.xaml` 设置应用程序的起始文件与资源
`app.xaml.cs`: `app.xaml`的后台文件,继承自`System.Window.Application`,用于处理整个WPF应用程序的相关。

# App.xaml

```XAML
<Application x:Class="WpfApp1.App"
             <!-- WPF应用程序的默认命名空间映射 -->
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             <!-- 映射可扩展应用程序标记语言(XAML)的扩展命名空间, 通常将其映射为 x 前缀 -->
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             <!-- 系统资源定义区 -->
             StartupUri="MainWindow.xaml">
    <Application.Resource>
        <!-- 系统资源定义区 -->
    </Application.Resource>
</Application>

```

`StartupUri` 属性可以指定项目运行时的启动窗体。
## App.xaml
## App.xaml.cs
