### 将 ListView, GridView等水平排列
Scrollxxx接口根本就没有这种东西.. 核心看VirtualizingStackPanel那一行就好了
```xml
<ListView
    ScrollViewer.HorizontalScrollBarVisibility="Auto"
    ScrollViewer.HorizontalScrollMode="Enabled"
    ScrollViewer.VerticalScrollMode="Disabled">
    <ListView.ItemsPanel>
        <ItemsPanelTemplate>
            <VirtualizingStackPanel Orientation="Horizontal" />
        </ItemsPanelTemplate>
    </ListView.ItemsPanel>
</ListView>
```
