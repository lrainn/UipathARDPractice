> 前言：【【非原创】】UiPath Advanced RPA Developer Certification Training的课程资料机翻版。
课程链接：[Link](https://academy.uipath.com/learningpath/error-and-exception-handling-in-studio)

@[toc]
# 1 关于本课程
欢迎！

在本课程中，您将了解如何让自动化生产做好准备的最重要方面之一：如何==预测==、==检测==和==处理==流程中的异常。

我们将从介绍 UiPath 中遇到的常见异常开始。然后我们将介绍具体的异常处理活动（TryCatch、Throw、Rethrow、Retry Scope 和 Global Exception Handler）。我们还将了解 UI 自动化活动共享的一个非常有价值的属性 (ContinueOnError)。

**您将在本课程中学到什么**
在本课程结束时，您将能够：
- 描述常见的异常处理技术并解释何时应该使用它们。
- 在自动化项目中使用 TryCatch、Throw、Rethrow 和 Retry Scope 活动。
- 在有人参与和无人参与的场景中使用全局异常处理程序。
# 2 系统和业务异常 System and Business Exceptions
## 2.1 区分Errors和Exceptions：
==Errors==
Errors是特定程序通常无法处理的事件。根据导致错误的原因，有不同类型的错误 - 例如：

- 语法错误 **Syntax errors**，编译器/解释器无法将编写的代码解析为有意义的计算机指令。
- 用户错误 **User errors**，软件因某种原因确定用户的输入是不可接受的。
- 编程错误 **Programming errors**，即程序不包含语法错误但未产生预期结果。这些类型的错误通常称为错误。

==Exceptions==
异常是由程序识别（捕获）、分类和处理的事件。更具体地说，有一个由开发人员配置的例程，当捕获到异常时会激活该例程。有时，处理机制可以简单地停止执行。
一些异常与所使用的系统相关，而另一些则与业务流程的逻辑相关。

## 2.2 了解不同类型的异常
- ==系统异常 System exceptions==
您可以在下方找到在使用 UiPath 开发的项目中可能遇到的最常见异常。一般而言，几乎所有异常都是从 **System.Exception** 派生的类型，因此，例如，在 TryCatch 中使用此泛型类型将捕获所有类型的错误。
	- **NullReferenceException** - 在使用没有设置值（未初始化）的变量时发生。
	- **IndexOutOfRangeException** - 当对象的索引超出集合的限制时发生。
	- **ArgumentException** - 在调用方法并且至少有一个传递的参数不符合被调用方法的参数规范时抛出。
	- **SelectorNotFoundException** - 当机器人无法在 TimeOut 时间内为目标应用程序中的活动找到指定的选择器时抛出。
	- **OperationException** - 在超时时间内未找到图像时发生。
	- **TextNotFoundException** - 在超时时间内未找到指示的文本时发生。
	- **ApplicationException** - 描述源于技术问题的错误，例如应用程序没有响应。

- ==Business exceptions==
Business rule exceptions与上面列出的所有System exceptions是分开的。这些错误的根源在于自动化项目所依赖的某些**数据**不完整、缺失、超出设定范围（例如试图从 ATM 中提取的数据超过其每日限制），或者未通过其他数据验证标准.

在 TryCatch 活动中使用通用 System.Exception 不会自动识别业务规则异常。它们需要由开发人员使用 Throw 活动定义并在 TryCatch 内处理。

现在我们已经了解了常见的异常类型，让我们了解 Studio 中的各种异常处理技术。
# 3 TryCatch, Throw 和 Rethrow
TryCatch 活动在序列或活动中捕获指定的异常类型，并显示错误通知或关闭它并继续执行。

作为一种机制，TryCatch 运行 Try 块中的活动，如果发生错误，则执行 Catches 块中的活动。只有在**没有抛出异常或在 Catches 块中捕获并处理异常（不会重新抛出）时，才执行 finally 块**。

- ==Try==
执行的活动有可能引发错误。
- ==Catches==
发生异常时要执行的活动或活动集。请注意，可以在此块中添加多个异常和相应的活动。
- ==Finally==
执行 Try 和 Catches 块后要执行的活动或活动集。仅在没有抛出异常或发生错误并在 Catches 块中捕获（不重新抛出）时，才会执行此部分。

**视频演示 - TryCatch**
我们将使用异常处理活动（TryCatch、Throw 和 Rethrow）来捕获我们定义的系统和业务异常。

添加 TryCatch 的最简单方法是右键单击活动或序列并选择“用 TryCatch 操作围绕它”。我们还有一个热键可以做到这一点：“control + T”。另一种选择是从“活动”面板添加它。
**快速回顾一下：**
- TryCatch 活动可用于捕获运行时异常并执行恢复步骤。
- Try 块包含我们怀疑可能引发异常的活动。
- Catches 块让我们可以为多种异常类型配置案例。最通用的是系统异常。如果捕获的异常对应于 Catches 块中的父类型和子类型，则将执行最具体的情况。
- finally 块包含一个活动，只有在==没有发生错误==或==错误已被捕获==时才应执行该活动。
当我们想要抛出异常时使用 Throw 活动，即使它不是由活动生成的。它通常用于定义业务规则例外。
- Rethrow 活动只能在 catch 块内使用，并且会再次抛出最初捕获的异常。

# 4 重试范围 Retry Scope
只要不满足条件或抛出错误，Retry Scope 活动就会重试包含的活动。

![在这里插入图片描述](https://img-blog.csdnimg.cn/699ab3fb6a704c16bfabfd513cbf7b9b.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_16,color_FFFFFF,t_70,g_se,x_16)
**Retry Scope** 活动用于捕获和处理错误，这就是它类似于 TryCatch 的原因。不同之处在于此活动只是**重试执行**，而不是提供更复杂的处理机制。

活动有2个主要部分：

- **Action** ： 保存我们想要重试的活动。
- **Condition**：保持终止条件。只要==不满足==此终止条件，Retry Scope 活动就会重试 Action 部分中的活动。
它可以在没有终止条件的情况下使用，在这种情况下，它将重试活动，==直到没有异常发生或超过提供的尝试次数==。

**附加属性**
- **NumberOfRetries** ：重试序列的次数。
- **RetryInterval** ：指定每次重试之间的时间量（以秒为单位）。
- 
**视频演示 - 重试范围**

填写详细信息并下载 ACME 报告。
**快速回顾一下：**

Retry Scope 活动可以通过两种不同的方式使用：
- 在条件块中添加一个条件，以便在不满足条件的情况下，操作块中的活动将按照重试次数字段中所述的次数进行重试。
- 如果条件不存在，它将重试操作块中的活动，直到达到重试次数或活动不会抛出任何错误。

**Want to find out more?**

[Retry Scope - UiPath Activities Guide](https://docs.uipath.com/activities/docs/retry-scope)
#  5 ContinueOnError 属性 
ContinueOnError 是一个属性，用于==指定即使在活动引发错误时是否应继续执行活动==。

![在这里插入图片描述](https://img-blog.csdnimg.cn/352210bc384040cb87927ce04df83d01.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_14,color_FFFFFF,t_70,g_se,x_16)
此字段仅支持布尔值（True、False）。默认值为 False，因此，如果该字段为空并引发错误，则项目的执行将停止。如果该值设置为 True，则无论出现任何错误，项目都会继续执行。

**请记住，如果在具有作用域的活动（例如附加窗口或附加浏览器）上将 ContinueOnError 设置为 True，则在该作用域内的其他活动中发生的所有错误也将被忽略。**

不建议在所有情况下将此属性设置为 True。但有一些是有意义的，例如：
- 使用数据抓取时 - 当找不到“下一步”按钮的选择器时，活动不会在最后一页上引发错误。
- 当我们对捕获错误不感兴趣，而只是对活动的执行感兴趣时。

**Want to find out more?**
[UI Activities Properties - UiPath Studio Guide](https://docs.uipath.com/studio/v2020.10/docs/ui-activities-properties)

#  6 全局异常处理程序 The Global Exception Handler
## 6.1 简介
全局异常处理程序是一种**工作流**，旨在在遇到意外异常时确定进程的行为。这就是为什么每个自动化项目只能设置==一个==全局异常处理程序的原因。

在其默认配置中，全局处理程序在运行时捕获流程中任何活动抛出的异常并执行标准响应 - 忽略、重试、中止或继续，如设计时预定义的那样。**对于有人值守的场景，它可以配置为让用户选择操作。**
可以通过添加具有此类型的新工作流文件或通过从“项目”面板将现有工作流设置为全局异常处理程序来创建全局异常处理程序。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20bdd4196f4e41b799dfdf3d977649af.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_17,color_FFFFFF,t_70,g_se,x_16)

## 6.2 工作方式
全局异常处理程序有 2 个预定义的参数，不应删除：
- 带有 In 方向的 **errorInfo**
包含有关引发的错误和失败的工作流程的信息。存储有关触发处理程序的异常的信息，以及用于确定进程遇到错误时的行为的结果。
-  Out 方向的**result** 
用于确定进程遇到错误时的下一个行为。
![在这里插入图片描述](https://img-blog.csdnimg.cn/529725fcfcfa47a7b454133f2babe051.png)

全局异常处理程序包含以下预定义的活动。如果需要，我们还可以在我们的 Handler 中添加其他活动。
- ==Log Error==
这部分只是记录错误。开发人员可以选择日志级别 - Fatal, Error, Warn, Info, Trace等。
![在这里插入图片描述](https://img-blog.csdnimg.cn/61ab963292824e088dd71cda1213c83f.png)
- ==选择下一个行为 Choose Next Behavior==
在这里开发者可以选择在执行过程中遇到错误时要采取的行动：
	- Continue - 重新抛出异常。
	- Ignore  - 忽略异常，并从下一个活动继续执行。
	- Retry  - 重试引发异常的活动。
	- Abort - 运行当前处理程序后停止执行。、
![在这里插入图片描述](https://img-blog.csdnimg.cn/e9f1cdcc6f6d467fa7c87fa6584c7486.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
请注意，==全局异常处理程序不可用于库项目，只能用于进程==。

==只有未捕获的异常才会到达异常处理程序==。如果异常发生在 TryCatch 活动中，并且在 Catches 块中成功捕获和处理（而不是重新抛出），则它不会到达全局异常处理程序。
## 6.3 视频演示
 **视频演示 - 全局异常处理程序**

设置全局异常处理程序以解决错误工作流程中的错误。
**对于一些关键要点：**
全局异常处理程序是一种工作流，旨在在遇到执行错误时确定项目的行为。每个自动化项目只能设置一个全局异常处理程序。
Global Exception Handler 有两个参数，不应删除：带有方向 In 的 errorInfo 和带有方向 Out 的结果。
可以将以下值分配给结果参数：
继续 - 重新抛出异常。
忽略 - 忽略异常，并从下一个活动继续执行。
重试 - 重试引发异常的活动。
中止 - 在运行当前全局异常处理程序后停止执行。


**视频演示 - 在有人值守的场景中使用全局异常处理程序**

配置全局异常处理程序，让用户决定在有人照管的场景中遇到异常时要采取的操作。
**对于一些关键要点：**

在有人值守的场景中，我们可以使用 Global Exception Handler 让用户决定机器人在遇到错误时应该采取什么行动。
我们可以通过在 Handler 工作流中使用**多选输入对话框**来让用户在继续、忽略、重试和中止之间进行选择来做到这一点。然后我们将相应的动作分配给 Switch 活动中的结果参数。

**Want to find out more?**

[Global Exception Handler - UiPath Studio Guide](https://docs.uipath.com/studio/v2020.10/docs/global-exception-handler)

# 7 实践
## 练习 1 - 电子表格计算的自动化
**处理客户现金流中的异常**

您的任务是自动计算 Excel 文件中两个字段（Cash In 和 Cash Out）之间的差异并将其输入到第三列中。不幸的是，随着时间的推移，该文件积累了很多错误。一个简单的工作流将抛出 System.Exception，因为机器人将尝试使用包含字母的 Int32 变量执行数学计算。

创建一个工作流，将下面附加的 excel 文件作为输入，并为差异列上的每一行添加现金收入值和现金支出值之间的差异。如果计算两者的差值成功，则设置Status为Success，否则设置为Cash In错误或Cash Out错误。

尝试转换 Cash In 和 Cash Out 值时，使用 Try Catch 块来捕获异常。

**实践1解决方案**

按顺序启动项目，给它一个合适的名称并添加注释。
使用“Excel 应用程序范围”容器。创建一个字符串变量（“WorkbookPath”）并为其指定默认值“Practice1.xls”。在容器中，添加“读取范围”活动并：
创建一个名为 SheetName 的新字符串变量，为其指定默认值 Cashflow。确保选中 AddHeaders 复选框。
创建一个新的 DataTable 变量来存储 Excel 文件的内容。
使用“For Each Row”活动循环遍历 DataTable 并：

创建 3 个名为 CashIn、CashOut 和 Result 的 Int32 变量。
通过使用 cint(row("Cash In")) 方法，添加一个“Try Catch”活动并在“Try”块中放置一个“分配”活动以将 cashIn 值转换为 Int32。在“Catch”块中，包含具有警告级别的日志消息（“exception.Message +” at “ + exception.Source”）和状态变量的 Assign 活动（值为“Cash In wrong”）。
添加另一个“Try Catch”活动并在“Try”块中放置一个“Assign”活动，以使用 cint(row("Cash Out")) 方法将 cashOut 值转换为 Int32。在“Catch”块中，包含一个带有警告级别的日志消息（“exception.Message + ” at “ + exception.Source”）和状态变量的 Assign 活动（值为“Cash Out wrong”）
添加条件为“status is nothing”的“If statement”活动：
在“Then”下，分配结果值并将结果设置为等于 cashIn - cashOut 之间的差值，并使用“Assign”将差值写入数据表的“Difference”列中。将值“成功”分配给数据表的行（“状态”）。
在“Else”下，在“Difference”列中分配“N/A”值并将“status”变量的值分配给行（“Status”）。
创建一个“Excel 应用程序范围”并添加 WorkbookPath 的路径。
添加“写入范围”活动并将 SheetName 起始单元格设置为 A1，在值表中，选择 AddHeaders。

**序列图**
![在这里插入图片描述](https://img-blog.csdnimg.cn/93e5e011759c4a28b17319b2bcad2f78.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
**Demo:**
![在这里插入图片描述](https://img-blog.csdnimg.cn/7916b38a237642a3acd2297b7a1fe6c3.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

## 练习 2 - 使用全局异常处理程序
**从为实践 1 开发的项目开始：**

更改工作簿路径以读取 Practice2.xlsx 文件。
添加一个全局异常处理程序，用于解决 Try Catch 活动未捕获的异常。
配置异常处理程序以在消息框中显示异常消息并中止进程。
运行该过程并一一修复 Excel 文件中发现的所有问题。

**实践2解决方案**

在项目中创建一个 Global Handler 类型的新工作流。
添加“日志消息”并将其级别设置为错误并将消息设置为 errorInfo.Exception.ToString。
添加“消息框”以显示“已识别以下错误：”+ errorInfo.Exception.ToString。
在选择下一个行为下，将 ErrorAction.Abort 分配给参数“result”。

**Demo:**
![在这里插入图片描述](https://img-blog.csdnimg.cn/fd0ac2feb21c4699a921dd775e963eb1.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

