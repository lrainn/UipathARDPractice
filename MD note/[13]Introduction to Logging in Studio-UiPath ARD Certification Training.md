前言：【【非原创】】UiPath Advanced RPA Developer Certification Training的课程资料机翻版。
课程链接：[Link](https://academy.uipath.com/learningpath/introduction-to-logging-in-studio)

@[toc]
# 1 关于本课程

欢迎！
日志记录使我们能够跟踪重要信息，这些信息可以帮助我们了解Robot, Orchestrator, Studio和我们的流程发生的情况。
机器人执行日志(Robot execution logs)是在机器人执行流程时生成的。
在生产环境中，您将无法访问调试功能，而是依靠日志来检查、诊断和修复您的流程。
我们在本课程中的重点是学习在开发项目和理解日志消息时设置有效日志记录的基础知识。
您将在本课程中学到什么

在本课程结束时，您应该能够：
- 解释什么是机器人执行日志(**Robot execution logs**)。
- 解释什么是默认日志、用户定义的日志和日志级别。
- 解释机器人执行日志(**Robot execution logs**)。
- 有效地使用日志消息活动(**Log Message activities**)。
# 2 日志概述 Logging Overview
## 2.1 UiPath 中的日志类型
一开始，我们已经提到本课的重点是在开发项目时设置有用的日志记录。对于一些上下文，让我们首先查看 UiPath 平台生成的主要日志类型：
- Studio logs 工作室日志
- Setup logs 设置日志
- Orchestrator diagnostic logs  Orchestrator 诊断日志
- Robot logs  机器人日志
![在这里插入图片描述](https://img-blog.csdnimg.cn/41ea906e698a4ebebf13c897ca076f94.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
## 2.2 Robot logs 机器人日志
机器人日志是由 UiPath 机器人生成的消息。机器人日志有两种类型：**Robot execution logs**（机器人执行日志）和**Robot diagnostic logs**（机器人诊断日志）。Robot execution logs描述流程的执行，而Robot diagnostic logs描述机器人的功能。我们将专注于Robot execution logs。

### 2.2.1 Robot execution logs 机器人执行日志

在工作室中**运行进程时生成**的日志类型是机器人日志的子集，称为机器人执行日志。
让我们看看如何创建默认日志和自定义日志。
![在这里插入图片描述](https://img-blog.csdnimg.cn/d2f16089c2774212a063bb654bd51f5b.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_18,color_FFFFFF,t_70,g_se,x_16)

- **Robot Execution Logs 机器人执行日志**

机器人执行日志可用于监督、诊断和调试生产过程，收集过程性能数据，甚至跟踪业务结果，例如处理的交易总价值。在本课中，我们将重点介绍监督、诊断和调试方面。

Robot Execution Logs可以是默认日志(**default logs **)，也可以是自定义日志( **user-defined logs**)。

发生某些事件时会自动生成默认日志。此类别记录的事件是：

- 每次**启动进程**时都会生成执行开始（Level = Information）
- 每次**流程结束**时都会生成执行结束（Level = Information）
- 每次启动流程中的**事务**时都会生成事务开始（级别 = Information）
- 每次流程中的**事务完成**时都会生成事务结束（级别 = Information）
- 每次执行遇到**错误**并停止时生成错误日志（Level = Error）
- 如果 Robot Logging Setting 设置为 Verbose 并包含活动名称、类型、变量值、参数等，则会生成调试日志（级别 = Trace）

**user-defined logs**是根据用户在 Studio 中设计的流程，在使用 ***Log Message*** 活动或 ***Write Line*** 活动时生成的。

## 2.3  日志级别

日志级别让我们可以按**严重性**或日志消息与进程执行相关的**重要性**对日志消息进行排序。 Orchestrator 中使用日志级别来过滤掉特定级别以下的日志。

| 日志级别 |意义  |
|--|:--|
| Fatal | 机器人无法或不应从此错误中恢复。出现了严重错误，需要停止该过程。例如，机器人无法处理异常，或者它与之交互的网站显示一条消息，表明它正在维护中。 |
| Error | 发生错误。机器人将尝试恢复并继续处理下一个项目。 |
| Warn | 我们需要从其余日志信息中脱颖而出的任何重要数据。 |
| Info | 有关机器人进度的信息。通常包括我们何时进入/退出工作流，何时从外部源读取数据等。 |
| Trace | 开发/调试时有用的信息，但在生产中没有用且不需要。 |
|Debugging / Verbose level  | 详细级别为每个单独活动的执行生成默认日志，通过提供有关变量和参数值的更多信息，允许进行更深入的诊断我们可以通过启用 Studio 中的“日志活动”选项来生成详细日志。 |

Verbose 级别会记录活动的消息：开始和结束，以及使用的变量和参数的值。 **Verbose 级别用于调试**。

**默认情况下，Verbose级别包括：**
- 执行启动日志条目：每次启动进程时生成。
- 执行结束日志条目：每次进程完成时生成。
- 事务启动日志条目：每次机器人从 Orchestrator 获取事务项时生成。
- 事务结束日志条目：每次机器人将事务状态设置为成功或失败时生成。
- 活动信息日志条目：每次活动在工作流中启动、出现故障或完成时生成。

默认情况下，在 Studio 中运行进程将记录Trace level logs。要在本地将日志记录设置为Verbose级别，请访问“调试”选项卡，启用功能区中的“日志活动”选项并在调试模式下运行流程。

**Want to find out more?**

[Robot Logs   - UiPath Robot Guide](https://docs.uipath.com/robot/v2020.10/docs/robot-logs)
[Types of Logs   - UiPath Studio Guide](https://docs.uipath.com/studio/v2020.10/docs/types-of-logs)
[Logging Levels   - UiPath Studio Guide](https://docs.uipath.com/studio/v2020.10/docs/logging-levels)

# 3 访问和读取机器人执行日志
您可以在多个位置访问机器人执行日志：

- 在 UiPath Studio 的**输出面板**中，用于从 Studio 执行先前的流程。

- 在 *%localappdata%\UiPath\Logs\<shortdate>_Execution.log* 文件中，所有进程从 **UiPath Studio** 在机器上运行。日志将在 Trace 级别及以上或 Verbose 级别及以上生成，具体取决于是否激活 Verbose 级别。

- 在 *%localappdata%\UiPath\Logs\<shortdate>_Execution.log* 文件中，所有进程从 **UiPath Assistant**在机器上运行。日志将在 UiPath 助手及更高版本中定义的级别生成。

- 在 **Orchestrator** 中，在连接到 Orchestrator 时运行进程时的日志部分。日志将在定义的级别及更高级别生成。
- 
在本课程中，我们将学习如何编写有效的日志消息和解释日志文件，因此我们重点关注从“**输出**”面板和 **%localappdata%\UiPath\Logs\<shortdate>_Execution.log** 访问日志。

PS:通过单击调试、选择打开日志并访问所需日期的执行文件，可以在本地访问日志。
## 3.1 日志条目的剖析
让我们花点时间了解日志条目的结构。这在检查执行日志以分析行为或找出导致异常的原因时非常有用。日志采用 **JSON** 的形式，几乎只是一个键值对（“field1:value1”、“field2:value2”）。

默认日志字段存在于所有日志中：
- **Message**: 日志消息
- **Level**: 定义日志严重性
- **Timestamp**: 执行操作的确切日期和时间
- **FileName**: 正在“执行”的 .xaml 文件的名称
- **JobId**: 运行进程的作业的键
- **ProcessName**: 触发日志记录的进程名称
- **ProcessVersion**: 进程的版本号
- **WindowsIdentity**:执行记录的操作的用户的名称
- **RobotName**: 机器人的名称（在 Orchestrator 中定义）
- 
除了默认字段之外，日志还可以包含**特定于类型**的字段和**用户定义**的字段。
- 特定于类型的字段(**Type-specific fields**)
取决于日志类型，如执行结束的 totalExecutionTimeInSeconds 和 totalExecutionTime。
- 用户定义的字段**(User-defined fields** )
在 Studio 中定义（通过使用**添加日志字段活动**）并在活动生成后出现在所有后续日志中，除非它们被活动删除日志字段（以编程方式）删除。

## 3.2 设置 UiPath Assistant的日志级别
如果已连接，从UiPath Assistant运行进程会将日志发送到 Orchestrator，但也会在 %localappdata%\UiPath\Logs\<shortdate>_Execution.log 中生成日志。

日志条目将在UiPath Assistant及更高版本中设置的级别生成。例如，如果级别设置为Error，则只会生成Error 和Fatal 级别的日志。

让我们花点时间看看如何在 UiPath Assistant中设置日志级别。
**介绍**
在此示例中，我们希望将 UiPath 助手配置为仅记录通过它执行的进程的信息级别及更高级别的事件。让我们看看如何做到这一点。
- 我们将打开 UiPath 助手并点击首选项图标 Preference icon。
- 接下来，我们将点击首选项按钮。
- 现在，我们将点击 Orchestrator 设置选项。
- 请注意，日志级别也适用于生成本地日志，而不仅仅是发送到 Orchestrator 的内容。我们将单击日志级别下拉列表。
- 我们将选择 Information选项。
- 我们已经完成了。从现在开始，UiPath 助手将仅在本地和 Orchestrator 中保存信息级别及更高级别的日志。我们可以点击关闭。

**Want to find out more?**

[Types of logs  - UiPath Studio Guide](https://docs.uipath.com/studio/v2020.10/docs/types-of-logs#log-fields)

# 4 Logging Best Practices
在诊断生产中的流程时，您会发现很多时候，默认的异常日志消息很有帮助，但不足以全面说明失败的原因。用户定义的日志是您可以用来跟踪机器人在整个过程中的进度并更好地了解执行情况的面包屑。

另一方面，过度日志记录会增加 Orchestrator 的负载，减慢您的进程，并且由于日志条目的数量庞大而难以诊断问题。

解决方案是**在项目的战略点定义正确的日志消息**。下面的最佳实践涵盖了一些用于识别可能导致问题的事件的健康用途。

理想情况下应该使用日志消息活动：
- 在每个工作流的开始和结束（Log level = Information）。
- 每次在 Catch 块中捕获异常（Log level = Error）。
- 每次引发业务规则异常( Business Rule Exception)时（Log Level = Error）。
- 例如，当从外部源读取数据时，在读取 Excel 文件时在信息级别记录一条消息（Log Level = Information）
- 在 Parallel 或 Pick 活动中，在每个分支上记录消息，以便跟踪被采用的分支（Log Level = Information）。
- 在 If/Flowchart Decision/Switch/Flow Switch 活动中（但是，由于流程可能有很多这些活动，我们可以将日志级别从 Information 降低到 Trace，因此我们在数据库中没有很多这些日志） 

# 5 练习 - 添加日志消息
让我们应用最佳实践和日志级别使用指示。在本练习中，我们将从第一个模拟中演示的项目开始。

我们的项目由几个工作流文件组成。该项目导航到 ACME System 1，登录，导航到下载客户端和支持页面，下载所有文档，然后注销。

在给定的项目中，只有一个工作流文件 (GetCredentials.xaml) 包含用户定义的日志记录。您将如何添加日志消息以使执行易于监督？

**实践解决方案**

在下面，您将找到我们建议包含在工作流程中的日志消息活动列表。您可以根据公司的最佳实践或您自己的经验和判断来定义日志。
> ACME Login.xaml
1. 位置：在“如果页面未加载”活动的“Then”分支中
级别：Fatal
消息：“无法打开”+ in_URL +“页面”
原因：**机器人无法从此错误中恢复**。
![在这里插入图片描述](https://img-blog.csdnimg.cn/6475645a87e647f8b7270ebba9db6d38.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
2. 位置：在“如果登录成功”活动的“Then”分支中
级别：Info
消息：“在 ACME 中成功验证”
为什么：在 If/Flowchart Decision/Switch/Flow Switch 活动中使用日志消息。对于较小的流程，特别是当它是机器人进程中的重要一步时，我们可以使用信息级别。![在这里插入图片描述](https://img-blog.csdnimg.cn/469a60d32a4345bba505ef27db81e0f7.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
3. 哪里：在“如果登录成功”活动的“Else”分支中
级别：Fatal
消息：“提供的凭据错误”
原因：机器人无法从此错误中恢复。
![在这里插入图片描述](https://img-blog.csdnimg.cn/79502fbcd11c4025b923ac64a12bf0f8.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
> Open browser.xaml
1. 哪里：在 If 需要最大化活动的 Then 分支中
级别：跟踪
消息：“最大化浏览器窗口”
原因：在 If/Flowchart Decision/Switch/Flow Switch 活动中使用日志消息。
![在这里插入图片描述](https://img-blog.csdnimg.cn/5dd293d930bb4119970060282d8c8541.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
> CreateSavingPath.xaml

1. 位置：在 If is 文件夹的 Then 分支的开始处，并且它存在活动
级别：==Warn==
消息：“路径不存在：” + in_FolderPathToSave + “。尝试创建路径”
原因：使用警告级别记录我们需要从其余日志信息中脱颖而出的任何重要数据。
![在这里插入图片描述](https://img-blog.csdnimg.cn/54cc646235ca4b08849294a491286c15.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

