
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

* [第四章 阶段计划](#第四章-阶段计划)
* [产品计划](#产品计划)
    * [! 术语定义](#术语定义)
* [第九章 个体软件开发过程](#第九章-个体软件开发过程)
* [第十章 缺陷](#第十章-缺陷)
    * [! What](#what)
    * [! why](#why)
* [第十一章 缺陷查找技术](#第十一章-缺陷查找技术)
    * [! 发现缺陷的步骤](#发现缺陷的步骤)
    * [! 发现和修复缺陷的方案:](#发现和修复缺陷的方案)
    * [! 利用代码复查发现缺陷](#利用代码复查发现缺陷)
    * [! 在编译前进行代码复查的原因](#在编译前进行代码复查的原因)
* [第十三章 缺陷预测](#第十三章-缺陷预测)
    * [why](#why-1)
    * [! 缺陷密度](#缺陷密度)
* [第十四章 缺陷排除效益 缺陷引入和排除率](#第十四章-缺陷排除效益-缺陷引入和排除率)
* [第十五章 质量成本](#第十五章-质量成本)

<!-- tocstop -->
# 第四章 阶段计划

阶段计划: 基于时间段的计划。
时间段即日历上的一段时间，如一天、一周、一个
月或一年，阶段计划是这段时间内对时间
的安排。

产品计划: 基于活动的计划。产品计划是
产品活动期间的时间安排。

# 产品计划
## ! 术语定义
__一个产品__ 是你为合作者、老板或客户生产的物品；
产品可以是有形的，如程序或报告；
也可以是无形的，如提供的服务等。

__一个项目__ 通常是生产一种产品。

__一个任务__ 已定义的一部分工作。

__一个过程__ 定义了完成项目的方法。

__计划__ 描述了完成一个特定项目的方法。

__一个作业__ 是你所做的事情, 一个项目或一项任务。

产品计划可以帮助软件工程师判断某项工作将
要花费多少时间以及什么时候能够完成

产品计划还可以帮助软件工程师跟踪工作的进
展情况，了解项目的状态

一份基本的产品计划包括以下三个方面：
+ 待开发产品的规模及其重要的特性：规模估计
+ 完成工作所需时间的估计：项目时间
+ 项目进度计划。

# 第九章 个体软件开发过程

__一个过程__ 定义完成开发项目的方法。
__过程__ 有多个阶段或步骤, 计划, 设计, 开发, 复查, 编译, 测试, 后置
__一个过程阶段__ 由许多 __任务__ 或 __活动__ 组成,

__一个过程__ 可以包括一个或多个阶段,
__一个阶段__ 可以包括一个或多个任务或活动

__一个过程__ 必须有明确的入口和出口
__过程的步骤__ 定义了要完成的任务,以及如何完成这些任务

一个有完整描述的过程称为 __已定义的过程__;
__已定义的过程__ 一般由一些脚本、表格、模板和标准组
成。
__一个过程脚本__ 是一组过程的用户在使用过程中应该遵守的 __书面的__ 步骤。

对于一个已定义的过程，每个阶段产生一个特定的结果，阶段完成时刻即为一个可测量的检查点。

# 第十章 缺陷
## ! What
缺陷是指程序中存在的错误,如语法错误,一个不正确的语句..
缺陷时任何影响到程序完整而有效地满足用户要求的东西,
缺陷是客观存在的, 是可以标志描述和统计的

## ! why
+ 软件质量体现在许多方面，但首先要面对的而且必须解决的方面是软件缺陷
+ 提高程序设计水平；
+ 减少程序中缺陷的个数；
+ 节省时间；
+ 节约开支；
+ 负责任的完成工作。

# 第十一章 缺陷查找技术
## ! 发现缺陷的步骤
+ 标识缺陷征兆
+ 从征兆推断出缺陷的位置
+ 确定程序中的错误
+ 决定如何修复缺陷
+ 修复缺陷
+ 验证这个修复是否已经解决了问题

标识征兆 -> 征兆推断缺陷 -> 确定缺陷 ->
决定方案 -> 修复缺陷 -> 验证修复


## ! 发现和修复缺陷的方案:
__编译器:__
> 编译器能标识出大部分语法错误
> 但编译器不能检查出所有的拼写、标点符号或其它不符合语法的缺陷
> 原因是编译器经常可以在源程序有缺陷的情况下生成代码

__测试:__
> 测试的质量是由测试用例所覆盖的程序功能的程度决定的，
> 事实上，除了最简单的程序，任何程序的完全测试都是不可能的

__发行:__
> 发行仍然含有缺陷的产品，然后等待用户发现和反馈缺陷信息：
> 这是花费最大的策略；

__个人复查源程序清单(代码复查):__
> 这是最快最有效的发现和修复缺陷的方法。

## ! 利用代码复查发现缺陷
目标: 尽可能 __早__ 和 __多__ 的发现缺陷, 开发过程每前进一部, 发现和修复缺陷的平均代价要增长10倍。

代码复查注意事项:

+ 第一次编译前进行代码复查
+ 在打印出的源程序清单上复查
+ 在缺陷记录日志上记录发现的每一个缺陷
+ 根据以前在编译和测试阶段发现的缺陷类型复查

=> 时机 打印清单 记录日志 经验

## ! 在编译前进行代码复查的原因
+ 无论编译前还是编译后, 进行完整的代码复查的时间基本相同
+ 节省编译时间
+ 编译后, 不想复查
+ 编译前后, 对检查语法的有效性的效果是一样的
+ 经验证明 在编译阶段中程序有大量缺陷时 一般在测试阶段也会有很多缺陷

# 第十三章 缺陷预测
## why
1. 准确估计程序中缺陷的个数
2. 决定是否进行下一轮测试或者代码复查

## ! 缺陷密度
单位: Defects/KLOC
步骤:
+ 累计每个过程发现的缺陷总个数(__$D$__)
+ 统计新开发和修改的代码__行数__(__$N$__)
+ 缺陷密度 __$Dd$ = $1000 * D/N$__


    例：一个96行的源程序总共发现14个缺陷，
    则缺陷密度是：
    Dd＝1000×14/96＝145.83Defects/KLOC

缺陷估计就是拿以往统计的缺陷密度乘上新写的行数

# 第十四章 缺陷排除效益 缺陷引入和排除率
若一个程序在开始测试时有100个缺陷，在测试阶段发现了45个缺陷，则测试阶段的缺陷排除效益为45％。

$$ Defects/Hour =  60 * \frac{defects(import)}{mins}$$
$$ Defects/Hour =  60 * \frac{defects(handle)}{mins}$$

100 * 排除/引入 = 效益

$$ 100 * \frac{handle}{produce} $$

# 第十五章 质量成本
过失成本、质检成本和预防成本。

A/FR = 复查时间 / 编译和测试时间
