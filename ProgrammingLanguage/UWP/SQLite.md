# Import
1.
    -- 在Visual Studio 2015插件管理器里搜索并安装 SQLite for UWP
    --  或者在 https://www.sqlite.org/download.html 下载uap适配版本的SQLite

    > 下载完了以后需要重启项目
2. 使用 Nuget 包管理器添加两个引用:
   [SQLite.Net-PCL](https://www.nuget.org/packages/SQLite.Net-PCL/)
   `Install-Package SQLite.Net-PCL`
   [SQLite.Net.Async-PCL](https://www.nuget.org/packages/SQLite.Net.Async-PCL/)
   `Install-Package SQLite.Net.Async-PCL`
3. 之后就可以在项目中看到引用的包了
    ![uwp_sqlite_1](/assets/uwp_sqlite_1.jpg)
4. 接下来我们还需要给这玩意儿配置引用
    ![uwp_sqlite_2](/assets/uwp_sqlite_2.png)
    引用 -> Universal Windows -> 扩展
    ![uwp_sqlite_3](/assets/uwp_sqlite_3.png)

    ![uwp_sqlite_4](/assets/uwp_sqlite_4.png)
