前言：【【非原创】】UiPath Advanced RPA Developer Certification Training的课程资料机翻版。
课程链接：[Link](https://academy.uipath.com/learningpath/project-organization-in-studio)

@[toc]

# 1 关于本课程 
欢迎！
在本课程中，我们将重点介绍组织项目的最佳实践。我们将学习选择项目布局、分解复杂流程、重用项目的各个部分、管理组件版本以及防止异常。

**每个 UiPath 实施都需要遵循明确的原则**
**我们的目的是建立自动化流程，这些流程是：**
- ==Reliable== 
可靠（机器人应按预期工作，意外错误率最低）
- ==Efficient== 
高效（应尽可能缩短执行时间）
- ==Maintainable== 
可维护（工作流应该易于理解和调试）
- ==Extensible== 
可扩展（添加新功能应该很容易

**在本课程结束时，您将能够：**
- 为每个工作流程选择合适的**项目布局**。
- 将复杂的自动化项目**拆分**为可单独开发的功能工作流。
- 创建和共享项目**模板**以加快开发速度。
- 识别跨项目的可**重用**组件并将它们存储为库以备将来重用。
- 解释使用**异常**处理技术的好处。
- 解释使用 UiPath 的**版本控制**功能来保持开发工作的可跟踪性和可靠性的好处。

# 2 选择工作流布局
对于自动化的小型流程或大型自动化项目的一部分，有 3 种布局选项 - 序列、流程图和状态机（Sequence, Flowchart and State Machine.）。

## 2.1 Sequence
**什么时候使用？**
	- 当有明确的连续步骤，没有太多条件时（例如，UI 自动化）。
	- 通常，序列用于嵌套工作流，高级逻辑通过流程图或状态机处理。
	
**有哪些优势？**
	- 易于理解和遵循，采用自上而下的s方法。
	- 非常适合简单的逻辑，比如在互联网上搜索项目。

**有什么缺点？**
	- 在同一序列中嵌套太多条件会使过程难以阅读。
	- 不适合连续流动。

## 2.2 Flowchart
**什么时候使用？**

- 当您有一个包含==多个条件==的复杂流程时，流程图至少在视觉上更容易理解和遵循。
- 当您需要一个仅在几种条件之一中终止的流时。

**有哪些优势？**
- 易于理解，因为它类似于软件计算中的逻辑图。
- 流程图最重要的方面是，与序列不同，它们呈现多个分支逻辑运算符，使您能够创建复杂的业务流程并以多种方式连接活动。

**有什么缺点？**
- 流程图应仅用作一般工作流程（其中嵌套有序列），而不应用于项目的各个部分（嵌套在其他工作流程中）。
## 2.3 State Machine
**什么时候使用？**

首先，让我们了解什么是状态机。它是一个抽象机器，由有限数量的预定义状态和这些状态之间的转换组成。==在任何时候，根据验证的外部输入和条件，它只能处于其中一种状态==。
状态机可以使用有限数量的清晰和稳定的状态来通过。日常生活中的一些例子包括自动售货机、电梯或交通灯。

**有哪些优势？**
- 可用于更复杂的连续工作流。
- 可以轻松定义状态之间的转换并提供灵活性。
- 可以容纳更复杂且无法通过简单循环和 If 语句捕获的进程。
- 使用状态机更容易覆盖所有可能的情况/转换。

**有什么缺点？**
- 由于其复杂性而导致更长的开发时间：将过程拆分为逻辑“状态”、找出转换等。

**注意：**状态机不能被过度使用——它们应该只定义项目的==骨架==。
事实上，有一些基于状态机的模板专门用于构建大型企业自动化。最常用的是==机器人企业框架==——我们有单独的课程在 RPA 开发人员高级学习计划中涵盖它。

## 2.4 Want to find out more?

[Sequences - UiPath Studio Guide](https://docs.uipath.com/studio/v2020.10/docs/sequences)

[Flowcharts - UiPath Studio Guide](https://docs.uipath.com/studio/v2020.10/docs/flowcharts)

[State Machines - UiPath Studio Guide](https://docs.uipath.com/studio/v2020.10/docs/state-machines)

# 3 在工作流库中组织项目
通过允许对组件进行独立测试，同时鼓励团队协作，将自动化流程分解为更小的工作流程可确保开发速度和可靠性。两者对于此类举措的成功都至关重要。此外，在复杂的自动化中（就像大多数企业项目一样），问题不是是否应该分解，而是如何分解。

**有多种方法可以拆分工作流，至少应考虑 3 个因素作为分解标准：**
- 正在自动化的应用程序
- 某项操作的目的（登录、处理、使用OCR读取文档、填写模板等）
- 每个工作流的长度
- 其他项目中的工作流可重用性

例如，一个复杂的流程可以拆分为每个应用程序的工作流，并且对于这些应用程序中的每一个，可以拆分输入、处理或输出。如果这些工作流中的任何一个太长，它们可以进一步拆分，同时记住这样做的目的。

## 3.1 视频演示 - 在工作流程中分解项目

在本视频中，您将探索如何将复杂的流程分解为更小的工作流程。如果您正在构建，请下载下面的起始项目。
BEFORE:
![在这里插入图片描述](https://img-blog.csdnimg.cn/fd436694f4df4a95802e147fd5a08d04.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
AFTER:
![在这里插入图片描述](https://img-blog.csdnimg.cn/28544b6b9cf64f069fac963f581a9807.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
![在这里插入图片描述](https://img-blog.csdnimg.cn/4cd7d219c3d8439286b29fa67bf0d675.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
![在这里插入图片描述](https://img-blog.csdnimg.cn/b3bec98b5b7e4298a11013f15a103914.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
## 3.2 使用多个工作流处理项目中的数据

将项目拆分为更小的工作流会影响数据的处理方式。由于变量仅在同一个工作流中起作用，因此拥有多个工作流需要参数。

您可能从 Studio 中的变量、数据类型和控制流课程中了解到，参数与变量非常相似——它们动态存储数据，具有相同的数据类型，并且支持相同的方法。
**主要区别**在于“==Direction==”属性，表示数据传递的方向。方向可以是 In、Out 和 In/Out：
- ==In==
如果我们想传递一个仅在**调用的工作流**中使用的值。外->内。
- ==Out==
如果我们想传递要在**调用的工作流之外**使用的值，在父工作流中使用。内->外。
- ==In/Out==
如果我们要将值从**父工作流传递到调用的工作流**，请在调用的工作流中修改它，然后将新值传递回父工作流。内< - >外。

考虑从总工资中减去所有税款的调用工作流。您至少需要 2 个参数：
- 映射到包含总工资的变量的“in”参数
- 将净工资值传递给父工作流中的变量的“out”参数

**使用参数的最佳实践**
- ==命名==：
在命名参数时使用方向作为前缀 - 例如in_ArgumentName1、out_ArgumentName2、io_ArgumentName3。
- ==方向==：
具体说明论证方向。除非需要，否则避免使用 In/Out。

**Want to find out more?**
[Arguments - UiPath Studio Guide](https://docs.uipath.com/studio/v2020.10/docs/using-arguments)
[Invoke Workflow File - UiPath Activities Guide](https://docs.uipath.com/activities/docs/invoke-workflow-file)
# 4 Libraries 库
提取工作流并在整个自动化项目中==重用==它们是保持项目有组织、可读和可持续的好习惯。同时，存在工作流可以在不同项目中重复使用的情况。考虑登录 SAP 的顺序。每次自动化项目与 SAP 打交道时，都需要相同的步骤序列。

**在单独的项目中存储和重用组件**是通过==流程库==完成的。流程库是一个包含多个可重用组件的包，这些组件由一个或多个充当单独活动的工作流组成。库保存为 **.nupkg** 文件，然后使用包管理器安装在不同的项目中。

我们如何确定项目的一部分是否可重用？考虑可以在多个流程中使用哪些活动序列。例如：登录、注销、启动多个进程通用的多个应用程序、数据输入序列。
**视频演示 - Libraries 库**

在本视频中，您将了解如何在工作流中创建库和使用库中的活动。
在开始之前，让我们先了解一下什么是流程库的基础知识。库是包含可重用组件的包。它们由一个或多个工作流组成，每个工作流都作为一项单独的活动。库保存为 NuGet 包，可以像使用包管理器的常规活动包一样安装。安装后，开发人员可以在他们的项目中使用它们，它们将作为依赖项列出。
通过编辑工作文件夹中的 json 文件，可以随时更改这些详细信息。

在此视频中，我们已将库存储在本地。将它存储在 Orchestrator 中可能是一个更好的主意。要了解其工作原理，请导航到 Orchestrator for RPA 开发人员课程并查看那里的库课程。

**最佳实践 -  Libraries**
在库中，每个工作流都可以设置为公共或私有。公共项目可以在添加了库的项目中用作活动，而私有项目只能在库内部使用（私有库被其他公有库调用，不能直接被用户调用）。
**Want to find out more?**
[About Libraries - UiPath Studio Guide](https://docs.uipath.com/studio/v2020.10/docs/about-libraries)
# 5 项目模板
通过在 Studio 中创建项目模板并与团队共享，可以提高开发自动化项目的速度。 Studio 允许您创建和发布自定义模板或使用可用内置模板中的模板。

**视频演示 - 创建和共享项目模板**

在本视频中，您将探索项目模板的创建以及如何在另一个自动化项目中使用它。

**快速回顾一下：**
- 我们可以通过在“开始”选项卡的“新建项目”部分中选择“模板”来创建新模板。
- 构建后，新模板需要发布到 Orchestrator、本地提要或自定义提要。
- 我们可以通过从“开始”选项卡的“从模板新建”部分或从“模板”部分中选择模板来基于模板创建新项目。

**Want to find out more?**
[Project Templates - UiPath Studio Guide](https://docs.uipath.com/studio/v2020.10/docs/project-templates)

# 6 异常处理
自动化项目经常遇到中断或干扰计划执行的事件。其中一些是在开发和测试阶段确定的，并实施了处理机制。

考虑一个自动化，其中输入数据来自 Web 表单，应用程序尝试将数据与使用姓氏的现有客户端列表进行匹配。但是如果用户在拼写名称时出错怎么办？当然，这个名字不会被识别。

**一个好的项目设计将包括识别和识别异常的方法，以及仅在捕获异常时执行的操作模式。**这些可以简单地停止执行，或在工作流中自动执行显式操作，甚至将问题上报给人工操作员。

**可以通过两种方式预测和处理异常：**
- 在活动级别，使用 **Try/Catch** 块或 **Retry Scope**。
- 在全局级别，使用全局异常处理程序(the **Global Exception Handler**)。

Studio 课程中的错误和异常处理( **Error and Exception Handling in Studio course**)将深入介绍两者。在这一点上，能够选择正确的异常类型很重要，因为这些信息将在开发后期的更高级别用于做出其他决策。例外(==exceptions==)的类别是：
- **Application exception**
应用程序异常描述了源于技术问题的错误，例如应用程序没有响应。
考虑一个从员工数据库中提取电话号码并将其插入财务应用程序的项目。如果尝试进行交易时，金融应用程序冻结，则机器人无法找到应插入电话号码的字段，并最终抛出错误。这类问题有可能通过重试事务来解决，因为应用程序可以解冻。
在管理应用程序异常时，为活动和工作流制定良好的命名约定极为重要。这将有助于跟踪导致异常的活动。
- **Business rule exception**
业务异常描述了一种错误，其根源在于自动化项目所依赖的某些数据不完整、缺失、超出设定范围（例如试图从 ATM 中提取的数据超过每日限额）或未通过其他数据验证标准（如包含字母的发票金额）。**业务规则异常不会“自然”发生，它们需要使用 Throw 活动来定义。**
考虑一个处理发票的机器人，其业务规则由流程所有者设置，只有金额低于 1000 美元的发票才能进入自动化流程。对于其他流程，适用不同的流程，涉及人类用户来处理它们。
在这种情况下，重试事务不会产生任何解决问题的机会，而是应通知业务用户有关待处理发票的信息，并且应将案例视为业务异常 - 因为这是通常流程中的异常，并且验证是由开发人员在工作流中明确进行的。
作为推荐的做法，异常中的文本应包含足够的信息，以便人类用户（业务用户或开发人员）了解发生的情况以及需要采取的措施。

**Want to find out more?**

[Try Catch - UiPath Activities Guide](https://activities.uipath.com/docs/try-catch)
[Global Exception Handler - UiPath Studio Guide](https://docs.uipath.com/studio/v2020.10/docs/global-exception-handler)

# 7 版本控制系统集成
源代码控制系统在大型项目中特别有用，其中每个阶段都有多个团队和个人做出贡献。源代码控制系统允许不同团队和位置的用户访问相同的资源并处理相同的项目。它们还用于对代码进行版本控制并维护开发过程中所做的所有更改的历史记录。

通过后台视图中的 Teams 页面，Studio 支持以下源代码控制系统：
- ==Git==
通过 Git 集成，您可以：
	- 克隆远程存储库。
	- 添加项目。
	- Commit and push。
	- 将项目复制到 Git。
	- 创建和管理分支。
	- 解决与 File Diff 选项的冲突。

- ==TFS==
	- 支持以下版本:
		- 2012
		- 2013
		- 2015
	- Express 2012
	- Express 2013
	- Express 2015
	- 首先，您需要在 Studio 中设置 TFS。
	- 然后您可以打开一个项目或将一个新项目添加到 TFS。

- ==SVN==
通过 SVN 集成，您可以：
	- 从 SVN 打开一个项目。
	- 将项目添加到 SVN。
# 8 Best Practices
让我们回顾一下在建立良好的项目组织时要遵循的要点：

- **开发前设计**
在开始实际开发之前，彻底分析流程，确定需求并计划解决方案。

- **将流程分解为组件**
将流程分解为更小的工作流程，以便更好地理解代码、独立测试和可重用性。这也会影响效率，因为不同的团队成员可以处理不同的（较小的）工作流。

- **重用组件**
使用库为您的项目创建和存储可重用组件。

- **使用项目中的文件夹**
根据目标应用程序将项目的工作流分组到不同的文件夹中

- **遵循命名约定**
在整个项目中保持一致的命名约定。

- **正确配置参数**
根据信息方向调用工作流时，请使用正确类型的参数 (In/Out/InOut)。对于命名，我们的建议是 PascalCase，将参数的方向作为前缀 (in_/out_/io_)。

- **小心处理敏感数据**
负责任地处理敏感数据：不应将凭据直接存储在工作流程中，而应从更安全的位置（如 Windows 凭据存储或 Orchestrator 资产）加载，并与获取安全凭据、获取凭据和键入安全文本活动一起使用。

- **处理特定异常**
使用 Try/Catch 块来预测和处理异常。同时请记住，简单地使用 Try/Catch 只会识别错误，而不是解决错误。因此，请确保您开发错误处理机制并集成它们。

- **处理全局异常**
将全局异常处理程序用于全局和/或不太可能发生的情况（例如，Windows 更新弹出窗口）。

- **使您的项目易于阅读**
向您的工作流程添加注释以阐明每个工作流程的目的。

- **使用日志记录**
在生产中使用日志来获取有关关键时刻或任何需要特定数据的相关信息。[您可以在此处阅读有关日志类型的更多信息](https://docs.uipath.com/studio/docs/types-of-logs)。

**使用工作流分析器**
在将您的项目发送给同行评审之前，运行工作流分析器以查看它与 UiPath 和您的组织定义的开发规则的合规性。

# 9 Practice
## 9.2 Practice 2 - Fix My Workflow
**从录音重新组织工作流程**
附件中的工作流程包括录制会话的结果。对其进行重组，以便：

- 将项目的各个部分放在单独的工作流中并调用它们。
- 在循环中生成 5 个名称。
- 将结果写入一个名为 people.xlsx 的文件中。

**实践2解决方案**

1. 将变量名称更改为有意义的名称：
	例如，H 可以更改为名称。
	Dd 应该是电话号码。
	Dd1 最好称为电子邮件。
	如果 Add Data Row 活动中 ArrayRow 属性的值尚未自动更新，请手动更新。
2. 将录音部分放在单独的工作流程中：

	最简单的方法是右键单击“附加窗口”容器并选择“提取为工作流”选项。
	请注意，名称、电话号码和电子邮件变量已自动创建为新生成的工作流的 Out 类型的参数，因为此新文件不接收任何输入，但应该返回到主工作流，从网络中提取的数据字段.更改参数的名称以包含方向作为前缀；
	在主工作流中，该序列已替换为针对新工作流的“调用工作流”活动。
	单击“导入参数”，然后在每个参数的“值”字段中输入相应的变量。
3. 在主工作流中创建一个循环并在其中调用新创建的工作流。
由于我们要执行 5 次，因此合适的选择是 While 或 Do While 循环。
	
	将“While”活动拖到工作流中后，使用变量面板创建一个默认值为0的“Int32”变量，这样我们就可以将其用作计数器；
	使用先前创建的变量为“While”活动设置“条件”，例如 counter < 5。
	将之前生成的“Invoke Workflow”活动和“Add Data Row”拖到循环内；
	使用“分配”活动来增加计数器变量的值。
	
**BEFORE:**
![在这里插入图片描述](https://img-blog.csdnimg.cn/a8a3afe327694111b952ed9de803a969.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

**AFTER:**
![在这里插入图片描述](https://img-blog.csdnimg.cn/e6a27e62411f4afc96abcbeb28cb4c5b.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
## 9.3 Practice 3 - Libraries
**更新库并使用更新的库**

从库视频演示中创建的库开始：

1. 在库中创建两个新组件，它们将：

	- 导航到 ACME 系统 1 上的发票，选择显示所有发票，提取所有发票数据并将其保存到名为“All Invoices.xlsx”的 .xlsx 文件中
	- 导航到 ACME 系统 1 上的发票，提供供应商税号，并将结果保存到名为“All invoices for”+<VendorTaxID>“.xlsx”的 .xlsx 文件中。供应商税号必须通过用户输入提供。
2. 创建一个项目，让用户选择下载所有工作项、下载所有发票或仅下载属于用户输入的某个税号的发票。为每个选项使用库组件。


**实践3解决方案**

1. 更新库

序列 1 – 导航到发票（私人工作流程）：
调用“导航到主页”工作流程；
使用“悬停”活动将鼠标悬停在“发票”按钮上以访问二级菜单；
使用“点击”活动点击“搜索发票”按钮；
使用“点击”活动点击“显示所有发票”按钮。
您可以使用记录器记录活动 2-4。

序列 2 – 下载所有发票（公共工作流程）
调用“导航到发票”工作流程；
使用“数据抓取”选项（“提取结构化数据”活动）以输出方向提取 DataTable 参数中的所有发票和详细信息。

序列 3 – 导航到按供应商税号搜索发票（私有工作流程）
调用“导航到主页”工作流程
使用“悬停”活动将鼠标悬停在“发票”按钮上以访问二级菜单
使用“点击”活动点击“搜索发票”按钮。
您可以使用记录器来捕捉活动 2-3。

序列 4 – 下载供应商税号的所有发票（公共工作流程）
调用“Navigate to search invoice by VendorTaxID”工作流程；
使用“键入”活动在搜索字段中写入输入值。使用带有 In 方向的 String 参数；
使用“点击”活动点击“搜索”按钮；
使用“数据抓取”选项（“提取结构化数据”活动）以输出方向提取 DataTable 参数中的所有发票和详细信息。


2. 创建工作流

使用“输入对话框”让用户在 3 个选项之间进行选择；
使用可从管理包安装的 UiPath.Credential.Activities 中的“获取安全凭据”活动。通过这种方式，您可以将凭据存储在 2 个字符串变量（“用户名”和“密码”）中；
使用图书馆中的“登录”活动；
使用“开关”执行与用户选项对应的工作流：
**案例 1**：下载所有工作项
以序列的形式启动工作流；
使用库中的“下载所有工作项”活动并将 DataTable 参数的值分配给 DataTable 变量；
使用“写入范围”活动将数据表中的数据写入 Excel 文件。

**案例二**：下载所有发票
使用库中的“下载所有活动”活动并将 DataTable 参数的值分配给 DataTable 变量；
使用“写入范围”活动将数据表中的数据写入 Excel 文件。

**案例 3**：按供应商税号下载发票
使用“输入对话框”活动从用户那里获取税号并将其存储在字符串变量（“VendorTaxID”）中；
使用库中的“下载供应商税号的所有发票”活动，“VendorTaxID”参数等于“VendorTaxID”变量；
使用“If”活动，使用“.Rows.Count”方法检查是否有与输入的税号对应的发票。如果是这样，请使用“写入范围”活动将数据表中的数据写入 Excel 文件；
使用库中的“注销”活动。

**序列图**
![在这里插入图片描述](https://img-blog.csdnimg.cn/04d14c38417b459c9f367b79dafebfba.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
库结构：
![在这里插入图片描述](https://img-blog.csdnimg.cn/273239a414634863bece87e16b946827.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_11,color_FFFFFF,t_70,g_se,x_16)
**Demo:**
![在这里插入图片描述](https://img-blog.csdnimg.cn/d4874476c3484aba904522802a065183.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

