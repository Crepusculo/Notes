
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

- [**Value**, **Reference**, **Out**, Three type of Parameters](#value-reference-out-three-type-of-parameters)

<!-- tocstop -->

# **Value**, **Reference**, **Out**, Three type of Parameters
C瞎普中有三种类型的参数: 值, 引用, 和 输出
 ```cs
 namespace ConsoleApplication1
{
    class Program
    {
        static void RefTest(ref int a, ref int b)
        {   // a:0,b:0
            a = 1;
            b = 2;
            // a:1,b:2
        }

        static void OutTest(out int a, out int b)
        {
            // a,b not define here
            a = 3;
            b = 4;
            // a:3,b:4
        }

        static void Main(string[] args)
        {
            int a = 0;
            int b = 0;
            // a:0,b:0
            RefTest(ref a,ref b);
            // a:1,b:2
            OutTest(out a,out b);
            // a:3,b:4
        }
    }
}
 ```
 上面的例子简单体现了 `ref` 和 `out` 的不同, `out`更像是声明多个返回值的意思。
 `out`像是说"这两个值将会被此函数的out参数替代"
