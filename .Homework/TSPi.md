# C . 1th
+ 周期性开发策略:
    + <span class="delete">最小可使用版本开始进行</span>
+ 周期性开发策略 约束:
    + <span class="delete">每个周期产生都是可以测试的版本</span>
    + <span class="delete">周期足够小,在可用时间内测试和开发</span>
    + <span class="delete">集成 可以获得期望的产品</span>
# C . 2th
+ 一般的团队问题
    + <span class="delete">领导效率低下
    + <span class="delete">需求扩散
    + <span class="delete">合作失败
    + <span class="delete">缺乏参与
    + <span class="delete">拖延和缺乏自信
    + <span class="delete">低质量
    + <span class="delete">低效率的评估
+ 什么是团队
    + <span class="delete">至少有2个人
    + <span class="delete">有共同的目标
    + <span class="delete">有具体的分工
    + <span class="delete">需要组员相互依赖
+ 建立一个高效的团队
    + <span class="delete">团队凝聚力
    + <span class="delete">挑战性目标
    + <span class="delete">反馈
    + <span class="delete">共同的工作框架
+ TSPi 如何构建团队
    + <span class="delete">Goals
    + <span class="delete">Roles
    + <span class="delete">Plans
    + <span class="delete">Communication
    + <span class="delete">External Communication
# C . 3th
+ 团队角色
    + <span class="delete">Team Leader
    + <span class="delete">Develope manager
    + <span class="delete">Quality/Process manager
    + <span class="delete">Planning manager
    + <span class="delete">Support Manager

+ 为什么要有团队目标
    + <span class="delete">团队目标制定了框架和策略

+ TSPi 的目标建立
    + Team GoalA<span class="delete">生成高质量产品
        + <span class="delete">第一次编译之前找出缺陷百分比: <span class="delete">80%
        + <span class="delete">系统编译发现错误数<span class="delete">0
        + <span class="delete">工程完成时包含功能需求<span class="delete">100%
    + Team GoalB<span class="delete">Run a productive and well-managed project
        + <span class="delete">估计产品规模错误<span class="delete"><20%
        + <span class="delete">估计开发时间错误<span class="delete"><20%
        + <span class="delete">记录和进入工程记事本的数据<span class="delete">100%
    + Team GoalC<span class="delete">Finish on time
        + <span class="delete">开发周期结束时间提前或推迟<span class="delete"><4
+ 团队分工
    + TL
        + <span class="delete">组建和维护高效的团队
        + <span class="delete">增强成员工作激情
        + <span class="delete">解决队员带来的问题
        + <span class="delete">向 Instructor 汇报团队进度
        + <span class="delete">组织团队会议
    + DM
        + <span class="delete">组织人员 分配任务 生成产品
    + PM
        + <span class="delete">制定详尽、精细的计划
        + <span class="delete">每周准确汇报团队情况
    + QCM
        + <span class="delete">准确汇报队员情况,正确使用TSPi进程数据
        + <span class="delete">保证团队遵照 TSPi 开发产品
        + <span class="delete">适度检查并报告
        + <span class="delete">会议记录 写进工程记事本
    + SM
        + <span class="delete">保证合适的开发工具和方法
        + <span class="delete">没有不被授权的改变
        + <span class="delete">风险记录系统记录所有风险事件
        + <span class="delete">在团队开发周期中达到重用目标
+ 团队会议:<span class="delete">一起分析上周周数据和开发周期日期
+ 第一次团队会议
    + <span class="delete">讨论角色
    + <span class="delete">复查并更新目标
    + <span class="delete">决定每周例会时间
    + <span class="delete">讨论一个团队成员向计划经理提交数据的准确时间

# C . 4th
+ 策略: 构建一个大系统的方法
+ 策略目标: 最小化风险
+ TSPi的基本策略: 周期进程中开发产品
+ 策略如何进行:
    1. 定义主要
    2. 决定可选
    3. 定义可选的风险和利益
    4. 风险评估
    5. 做出策略性决定
    6. 文档化
+ 制定一个概要设计
    + <span class="delete">(what)概要设计应该包括在开发周期中准备实现的所有功能
    + <span class="delete">(how/when)决定在每个周期开发什么功能
+ 制定初步规模估计
    1. <span class="delete">分析假定模块, 判定新加和改变的LOC
    2. <span class="delete">将估计数据写进START表
    3. <span class="delete">使用估计的代码规模 和一个 LOC/hour 比率, 求出每个功能花费的时间
    4. Planning Manager<span class="delete">制订初步的规模和时间估计
+ 风险?
    + 薛定谔
+ SCM 从开始到结束 控制生产 的一系列 活动
    + <span class="delete">CIP</span>
    + <span class="delete">CCP</span>
    + <span class="delete">CCB</span>
+ <span class="delete">CIP</span>配置定义计划
    + <span class="delete">产品命名唯一
    + <span class="delete">产品基线完成点
    + <span class="delete">产品拥有者定义
+ <span class="delete">CCP</span>配置控制流程
    + <span class="delete">同一时间 不允许 多个工程师 对同一产品进行修订
    + <span class="delete">修订是被授权的
+ <span class="delete">配置控制委员会
    + <span class="delete">保证基线产品不被随意修改, 所有更改要提交表格给配置控制委员会

# C . 5th 开发计划
PV
EV
Task 粒度 小于 <span class="delete">10
+ <span class="delete">

+ 计划过程
    + 列出
        + START -> SUMS
    + 制定 T
        + 分出task,
        + 写PV, 排序
        + 列入TASK
    + SCHEDULE
        + 分配时间 PM制定SCHEDULE表
    + 比较T和S
        + Ttotal > Stotal表示工作量过大,
        + 可以增加时间(S)
        + 可以减少任务(T)
    + SUMP 的 size - time
        + <span class="delete">size from SUMS
        + <span class="delete">time from TASK
        + <span class="delete">defect from SUMQ
    + 制定 Q
        + Summary rates
            + LOC / Hour
            + %reuse
            + %new reuse
        + PDF (Percent defect-free)
            + <span class="delete">>90% on system test
        + D/page
        + D/KLOC
        + D/Ratios (D/R)
            + <span class="delete">代码复查 / 编译 >2
            + <span class="delete">设计复查 / 单元测试 >2
        + Dev [time] ratios
            + <span class="delete">需求检查 / 需求 >= 25%
            + <span class="delete">HLD检查 / HLD >= 50%
            + <span class="delete">DLD rev / DLD >= 50%
            + <span class="delete">DLD / coding >= 100%
        + A/FR
            + <span class="delete">
            $$\frac{(review+inspection)}{ (compile + test )}$$
            + TSP = 1
        + Review and inspection rates:
            + Req r/s < 2p/hour
            + HLD r/s < 5p/hour
            + DLD r/s < 100 LOC/hour
            + Code r/s < 200 LOC/hour
        + D-injection(D/h)
        + D-removal(D/h)
        + Phase Yields:<span class="delete">在一个阶段中移除错误的百分比
        + Process Yields:<span class="delete">在一个给定阶段之前移除错误的百分比
            + Compile PY > 75%
            + Test PY > 85%
        + SUMQ + TASK -> SUMP
        + 工程师个人计划
        + 平衡团队工作

# C . 6th 定义需求
+ SRS
    + <span class="delete">Software Requirement 说明书
    + 6条 F E D A O
    + <span class="delete">功能需求
    + <span class="delete">外部接口需求
    + <span class="delete">设计限制
    + <span class="delete">属性分析
    + <span class="delete">其他需求
+ Why SRS is important ?
    + <span class="delete">用户不知道想要什么 直到使用 需求一直在变 需要用文档的形式固定下来
    + <span class="delete">帮助管理变更
+ 需求进程::
    + 开发经理在做
    + 复查 澄清 任务分配 归档 ==[制定系统测试计划]==
    + QCM复查 -> 写入 INS

# C . 7th 团队设计
+ HLD 必须写 SRS
+ HLD 内容 <span class="delete">组件 接口 行为
+ DLD 内容 <span class="delete">逻辑结构
+ HLD <span class="delete"> 设计阶段 </span>DLD<span class="delete">实现阶段</span>
+ 设计标准 NISDLD
    + <span class="delete">Naming conventions
    + <span class="delete">Interface formats
    + <span class="delete">System and error meesage
    + <span class="delete">Defect standard
    + <span class="delete">LOC counting
    + <span class="delete">Design representation standards
+ 设计复用
    + 复用接口设计
    + 复用文档标准
    + 复用部分指令
    + 应用支持
+ SDS (分锅)(DAPD)
    + <span class="delete">产品总体架构设计
    + <span class="delete">产品功能分配到组件
    + <span class="delete">每个组件的外部说明
    + <span class="delete">确定每个周期开发的功能和部件

# C . 8th 产品实现
+ 实现标准 (SNCSDD)
    + <span class="delete">Standards reviews
    + <span class="delete">Naming, Interface and message standards
    + <span class="delete">Coding s
    + <span class="delete">Size s
    + <span class="delete">Defect s
    + <span class="delete">Defect p
+ 实现策略
    + rrt
    +
+ 进程
    + 入口准则
    + 实现计划 (DM)
    + 分配任务 (TL)
    + DLD / DLD review -> LOGD LOGT
    + 测试计划
    + DLD inspection
    + code / code review / compile
    + code inspection
    + ut -> LOGD LOGT
    + 组件质量复查
    + 组件发布
    + 出口准则

C . 9th 集成测试和系统测试
+ 准则
    + 目的<span class="delete">不是修正 而是评估产品质量
    + <span class="delete">质量在开发级阶段已经决定
+ TSPi 测试策略
    + <span class="delete">构建系统
    + <span class="delete">集成测试
    + <span class="delete">系统测试
    + <span class="delete">回归测试
+ The Build and Integration
    + <span class="delete">大爆炸
        + <span class="delete">全部一起乱搞
        + <span class="delete"> 使用测试最少
        + <span class="delete"> 很少成功
    + <span class="delete">One-at-a-time
        + <span class="delete">一次一个
        + <span class="delete">能测出新添加有无问题
        + <span class="delete">太慢
    + <span class="delete">聚类
        + <span class="delete">一次一类
    + <span class="delete">平面系统
        + <span class="delete">发现关联
        + <span class="delete">需要暗桩
+ The System
    + <span class="delete">功能第一
        + <span class="delete">功能测试
        + <span class="delete">在normal abmormal important 进行可用性评估
        + <span class="delete">性能评估
    + <span class="delete">功能区
    + <span class="delete">自底向上
    + <span class="delete">自顶向下

+ 跟踪和评估测试
    + LOGTEST FORM 包含测试运行统计和包含的结果
+ 文档(DDDARU)
    + <span class="delete">DO 文档组织
    + <span class="delete">DT 文档术语
    + <span class="delete">DC 文档内容
    + <span class="delete">A 准确性
    + <span class="delete">R 可读性
    + <span class="delete">U 可懂
    + 书写风格
        + 短句
        + 简单
        + 大量列表和专用条款
+ 测试进程
    + 入
    + 测试开发
    + 构建
    + 集成
    + 系统
    + ~~回归~~
    + 文档
    + 出
