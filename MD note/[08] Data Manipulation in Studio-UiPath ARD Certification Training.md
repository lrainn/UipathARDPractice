> 前言：【【非原创】】UiPath Advanced RPA Developer Certification Training的课程资料机翻版。
课程链接：[Link](https://academy.uipath.com/learningpath/data-manipulation-in-studio)

@[toc]
# 1 关于课程
欢迎！
在本课程中，我们将介绍最重要的数据操作操作和示例。这些将使用您在工作中遇到的一些最常见的数据类型进行演示，即：
- 字符串
- 列表
- 字典

**您将在本课程中学到什么**
在本课程结束时，您将能够在 UiPath Studio 中执行以下操作：
- 使用最常见的 .NET 方法来操作 ==String== 变量。
- 使用特定的方法来初始化和操作==List== 变量。
- 使用特定的方法来初始化和操作==Dictionary== 变量。
- 使用 UiPath Studio 中的 RegEx 构建器执行复杂的==字符串==操作。
 
# 2 什么是数据操作 Data Manipulation
## 2.1 什么是数据操作
数据操作是修改、结构化、格式化或排序数据的过程，以促进其使用并提高其管理能力。

**我将在哪些业务场景中使用数据操作？**
网站所有者经常使用数据操作方法从他们的网络服务器日志中提取和查看特定信息。这允许观看他们最受欢迎的页面以及他们的流量来源。
考虑查询公共财务或法律数据库的过程。数据操作为信用分析师提供了仅提取相关数据并将其用于其他文档或将其与来自其他来源的信息相关联的手段。
## 2.2 Strings 字符串
### 2.2.1 字符串是什么？
字符串是与==文本==对应的数据类型。很难想象一个不涉及使用字符串的自动化场景。
任何时候需要捕获、处理、在应用程序之间发送或显示文本时，字符串都会派上用场（除非数据是结构化的 - 就像表格一样）。
**在哪些业务场景中您最有可能遇到字符串？**
- 获取操作的状态。
- 从较大的文本部分中提取相关片段。
- 向人类用户显示信息。

**视频演示 - 字符串操作**
**使用字符串方法提取特定的文本片段并以不同的格式显示它们**。
你好，欢迎来到这个关于字符串操作的演示！
在本视频中，我们将通过一个在各种业务场景中经常遇到的示例来了解字符串操作。我们将看到**如何使用字符串方法和属性从输入字符串中提取信息并组成输出字符串。**
```vbnet
InitialMessage.Split("."c).First.ToString.Substring(InitialMessage.LastIndexOf("author")+"author".Length).Trim
InitialMessage.Split("."c)(1).ToString.Split(":"c).Last.ToString.Split(","c).ToList
String.Format("{0} 的可用性：{1}",author.String.Join(";" +vbcr,Bookstores))
```
我们介绍过的方法是 Split、SubString、LastIndexOf、Trim、ToList、String.Format 和 String.Join。
感谢您的收看，我们下期再见！
![在这里插入图片描述](https://img-blog.csdnimg.cn/49f2caa7dd4f445fa7304440b34896ec.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
### 2.2.2 String methods 字符串方法
字符串操作是通过使用从 VB.Net 借来的字符串方法来完成的。以下是 RPA 中最常用的一些方法。
> - ==String.Concat==
**连接**两个指定对象的字符串表示形式。
表达式：*String.Concat (VarName1, VarName2)*
输出数据类型：String

> - ==Contains==
**检查**指定的子字符串是否出现在字符串中。返回真或假。
表达式：*VarName.Contains (“text”)*
输出数据类型：Boolean 

> - ==String.Format==
将对象的值转换为字符串（并将它们插入到另一个文本中）。
表达式: *String.Format(“{0} is {1}”, VarName1, VarName2)*
输出数据类型: String

> - ==IndexOf==
返回此实例中指定 Unicode 字符或字符串**第一次出现**的**从零开始**的索引。
表达式：*VarName1.IndexOf(“a”)*
输出数据类型：Int32

> - ==LastIndexOf==
报告指定 Unicode 字符或字符串在此实例中**最后一次**出现的**从零开始**的索引位置。
表达式：*VarName1.LastIndexOf("author")*
输出数据类型：Int32

> - ==String.Join==
**连接**集合中的元素并将它们显示为字符串。
表达式：*String.Join(“|”, CollVarName1)*
输出数据类型：String

> - ==Replace==
替换字符串中所有出现的子字符串。
表达式：*VarName.Replace (“original”, “replaced”)*
输出数据类型：String

> - ==Split==
使用给定的分隔符将字符串拆分为子字符串。
表达式：*VarName.Split(“|”c)(index)*
输出数据类型：Array of String

> - ==Substring==
使用起始索引和长度从字符串中提取子字符串。
表达式：*VarName1.Substring(startIndex,[ length])*
输出数据类型：String

**想了解更多？**
所有字符串方法
有关[字符串方法](https://docs.microsoft.com/en-us/dotnet/api/system.string?view=netframework-4.8#methods)的完整列表，您可以访问 microsoft.com 上的 .Net 门户上的专用空间。
## 2.2  Lists 列表
### 2.2.1 Lists是什么？
列表（或 List<T>，正如您将遇到的那样）是由**相同数据类型**（例如字符串或整数）的对象组成的数据结构。每个对象在列表中都有一个固定的位置；因此，它可以**通过索引访问**。
==数组是用于存储多个对象的固定大小结构，而列表允许我们添加、插入和删除项目==。
列表可以存储大量元素——名称、数字、时间坐标等等。列表提供了特定的操作方法，例如：
- 添加和删​​除项目。
- 搜索元素。
- 循环遍历项目（并对每个项目执行某些操作）。
- 对对象进行排序。
- 提取项目并将它们转换为其他数据类型。

**在哪些业务场景中您最有可能遇到列表？**
- 存储项目团队成员的计算机名称，用于需要进行的特定配置。
- 收集和存储符合特定条件的发票数量。
- 跟踪在特定时间段内针对特定问题创建的票号。

**视频演示 - 使用列表**

列表如何合并和排序，以及列表中的字符串对象如何格式化以使其看起来相同。
```bnet
Enumerable.Concat(SpainCities.AsEnumerable,UKCities.AsEnumerable).ToList
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/af6f0ff6655c4343af3c5067524bec49.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
### 2.2.2 引用类型初始化
初始化变量就是指定要分配给它的初始值。所有变量在声明时都会被赋予一个初始值。但是，根据新变量是**值类型**还是**引用类型**，此过程略有不同。

- **值类型** 
	==不需显式实例化==
	对于数字、布尔值、日期时间和其他值类型，如果我们不明确这样做，编译器将给它们一个有效值。例如，Ints 默认初始化为零，DateTimes 默认初始化为 DateTime.MinValue。在 Studio 中，即使字符串属于引用类型，也会为它们分配一个空白的默认值。

- **引用类型** 
==需要显式实例化==
引用类型变量，如列表和字典，初始化为我们提供的对象。如果我们不这样做，编译器将不会赋值。这意味着我们需要实例化一个对象并将其分配给我们刚刚声明的变量。

要开始使用列表和字典等引用类型，我们需要经过 3 个步骤：**声明、实例化和分配对象**。
- 我们**声明**了一个引用变量，比如说一个 String 类型的 List。我们提供名称，选择 *System.Collections.Generic.List<T>* 类型并指示 String。
- 我们**实例化**一个对象作为变量的初始值。在我们的例子中，我们想从一个不包含值的 String 对象列表开始，所以我们使用表达式 new List(of String)。
- 我们通过使用变量面板中的默认值或使用**分配**活动将对象分配给新变量（或初始化变量）。

### 2.2.3 适用于集合的 UiPath 方法
可以使用 .NET 方法或使用 UiPath Studio 提供的集合方法来操作列表。
> - ==Add to Collection==
将项目**添加**到指定的集合。它等效于 List.Add()。例如，它可用于将新名称添加到公司名称列表中。
![在这里插入图片描述](https://img-blog.csdnimg.cn/a005b100679842ae8979d7398e95b75b.png)

> - ==Remove from Collection==
从指定的集合中**移除**一个项目，并且可以输出一个布尔变量来确认移除操作的成功。例如，此活动可用于从要处理的发票列表中删除发票编号。![在这里插入图片描述](https://img-blog.csdnimg.cn/d28825c1f744454e8f013ae45c1892eb.png)


> - ==Exists in Collection==
通过输出布尔值作为结果指示给定项目是否存在于给定集合中。我们可以使用此活动来检查客户列表是否包含特定名称。
![在这里插入图片描述](https://img-blog.csdnimg.cn/c32b422def5d4d0abf2a8fe5158e56bd.png)

> - ==Clear Collection==
清除所有项目的指定集合。一种可能的用途是在开始一个过程的新阶段之前清空一个集合，该阶段将再次填充它。![在这里插入图片描述](https://img-blog.csdnimg.cn/b34c2b80465947c9b8556d32b063f44e.png)
## 2.3 Dictionaries 字典
### 2.3.1 Dictionaries是什么？
字典（或 Dictionary<TKey, TValue>，你会遇到它们）是 (key, value) 对的集合，其中的键是唯一的。想想您手机中的地址簿，其中每个姓名都有相应的数据（电话号码、电子邮件）。

==声明变量时必须选择键和值的数据类型==。 Dictionaries 中的数据类型可以是任何受支持的变量（例如，包括 Dictionaries）。
最常与字典相关的操作是：
- 添加和删​​除（键，值）对。
- 检索与键关联的值。
- 将新值重新分配给现有键。

**在哪些业务场景中您最有可能遇到词典？**
- 存储需要在整个过程中访问的配置详细信息或其他信息。
- 存储员工的职务或其他相关信息。
- 存储供应商的银行账户。

**视频演示 - 字典**
在这个演示中，我们将创建一个字典并存储人们的名字和他们的生日。然后，对于每个人，我们将打印以下信息：

- 这个人的名字。
- 今年的生日是否已经过去。
- 生日是今年的星期几。

**视频演示 - 字典和列表**
在这个演示中，我们将创建一个包含字符串和字符串列表数据类型的字典，并了解如何对其进行操作。

### 2.3.2 使用字典的方法
> - ==Initialization 初始化==
就像在 Lists 的例子中一样，Dictionary 变量需要使用实例化对象进行初始化。在前面的示例中，实例化和初始化是在“分配”活动中完成的。但是，正如您在列表一章中记得的那样，它们也可以在变量面板中完成。

> - ==Adding Key-Value Pairs 添加键值对==
*VarName.Add(Key, Value)* 
向现有字典添加一个项目。因为 Add 不返回值，所以我们使用 Invoke Method 活动。

> - ==Removing Keys 删除键==
*VarName.Remove(Key)*
从字典中删除一个项目。它可以用于“分配”活动。

> - ==Retrieving 检索==
> - *VarName.Item(Key)*
通过键返回字典项
>- *VarName.Count* 
返回字典项数的 Int32 值
>- *VarName.ContainsKey(Key)* 
检查具有给定键的项目是否存在于字典中并返回布尔结果
>- *VarName.TryGetValue(Key, Value)* 
检查字典中是否存在具有给定键的项目，如果找到则返回布尔结果和值

## 2.4 The RegEx Builder 正则表达式生成器
### 2.4.1 The RegEx Builder是什么？
正则表达式（REGEX，或regexp）是一种特定的搜索模式，可用于轻松匹配、定位和管理文本。但是，创建 RegEx 表达式可能具有挑战性。
UiPath Studio 包含一个 RegEx 构建器，可简化正则表达式的创建。
RegEx 的典型用途包括：
- 输入验证。
- 字符串解析。
- 数据抓取。
- 字符串操作。

**我将在哪些业务场景中使用 RegEx？**
检索遵循==特定模式==的文本片段，例如：

- 提取以某个数字开头的电话号码。
- 从批量文本中收集所有街道名称，即使它们不遵循特定模式 - 其中一些包含“Street”，其他包含“Rd.”等等。
- 使用常规 String 方法构建相同的表达式需要更长的时间——例如，RegEx 有一个预定义的表达式来定位字符串中的所有 URL。


**视频演示 - 使用 RegEx 构建器**
在这个演示中，我们将使用 RegEx 在包含多个地址的字符串中查找所有街道名称和号码。

### 2.4.2 UiPath 中使用 RegEx 构建器的方法
> - ==Matches==
搜索所有出现的输入字符串并返回所有成功的匹配项。
输出数据类型：System.Collections.Generic.IEnumerable<System.Text.RegularExpressions.Match>

> - ==IsMatch==
指示指定的正则表达式是否在指定的输入字符串中找到匹配项。
输出数据类型：String

> - ==Replace==
用指定的替换字符串替换与正则表达式模式匹配的字符串。
输出数据类型：String

**Want to find out more?**
[RegEx Builder Wizard - UiPath Activities Guide](https://docs.uipath.com/activities/docs/regex-builder-wizard)
[Matches - UiPath Activities Guide](https://docs.uipath.com/activities/docs/matches)
[Is Match - UiPath Activities Guide](https://docs.uipath.com/activities/docs/is-match)
[Replace - UiPath Activities Guide](https://docs.uipath.com/activities/docs/replace)

## 2.5 DateTime 日期时间
### 2.5.1 DateTime是什么？
顾名思义，DateTime 类型 (System.DateTime) 使您能够在变量中存储有关**日期和时间**的信息。
可以在系统命名空间 **System.DateTime** 下的“浏览并选择 .Net 类型”窗口中找到此类变量。

DateTime 变量的典型用途包括**附加文档**或**执行时间跨度计算**。

**我将在哪些业务场景中使用 DateTime？**
在以下情况下处理对时间敏感的文档，​​例如发票：
- 时间格式在整个过程中变化。
- 处理文件时需要增加或减少特定的时间。

**视频演示 - 使用 DateTime 类型**
在此演示中，我们将使用 DateTime 变量执行各种数据操作操作。

### 2.5.2 可与 UiPath 中的 DateTime 变量一起使用的方法
> - ==ToString==
将变量转换为字符串格式。数据也可以进一步处理为特定类型的字符串。
> - ==DateTime.Parse==
将变量从字符串转换为 DateTime 变量。此方法仅适用于不变文化时间格式变化。
> - ==Subtract==
对 DateTime 变量单位值执行**减法运算**。单位可以从几天到几毫秒不等。
> - ==Math.Abs==
用于显示**绝对值**。
例如，我们的结果是“-5”，但我们希望结果显示为“5”。

**Want to find out more?**
[DateTime Variables - UiPath Studio Guide](https://docs.uipath.com/studio/docs/date-and-time-variables)
[StackOverflow](https://stackoverflow.com/questions/46778141/datetime-formats-used-in-invariantculture)
# 3 练习
## 3.1 Practice 1 - Lists
**对列表进行排序并打印 3 个值**
给定输入的国家列表，请对列表进行排序并按降序打印前 3 个值。

注意：请将此值用于列表初始化：来自 {"Germany", "Spain", "Japan", "Brazil", "India", "China"} 的 new List(of String)。

**实践 1 解决方案**

- 将项目作为一个序列启动，并使用以下默认值定义一个字符串列表变量*（“InputData”）： new List(of String) from {"Germany", "Spain", "Japan", "Brazil", "India “， “中国”}*。
- 添加“调用方法”活动。在 MethodName 下写入“Sort”，在 TargetObject 下写入“InputData”。保持 TargetType 不变（空）。
- 再添加一项“调用方法”活动。在 MethodName 下写下“Reverse”，并像之前的“Invoke Method”一样填写其他 2 个字段
- 创建一个新的字符串变量列表。
- 将“分配”活动添加到设计器面板。
- 在 To 字段中，输入在步骤 4 中创建的变量。
- 在值字段中，输入原始变量的名称，后跟 .GetRange(0,3)。此变量存储排序列表中的前三个- 值。
- 添加“写行”活动。这将打印值。
- 在“写入行”活动的文本中使用“String.Join”方法：*String.Join (", ", econdvariablename.ToArray)*。

**流程图**![在这里插入图片描述](https://img-blog.csdnimg.cn/18e903a40a1c4c6d9bb8ad30e1ca7826.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
## 3.2 Practice 2 - Lists and DateTimes
**验证列表中的日期是否在当年过去**

给定格式为 dd.MM.yyyy 的字符串输入列表，请检查是否有任何日期与当前月份相同，并打印该日期以输出。

对于具有不同月份的日期，打印以输出从当前日期到列表中的日期（当前年份）经过/到期的天数。

注意：使用以下值初始化一个列表：
```vbnet
 new List(of String) from {"01.02.1980", "04.05.1985","06.08.1988","24.09.1999","18.11.1986","11.10 .1983"}
```
**实践2解决方案**

```vbnet
DateTime.ParseExact(InputDate, "dd.MM.yyyy", nothing) '按格式构建DateTime类变量

String.Format("The month of {0} is the same as curent month", InputDate) '格式化字符串

Datetime.Now.Subtract(new DateTime(Datetime.Now.Year, TmpDate.Month, TmpDate.Day))  '日期减法

String.Format( "{0} days passed from current day to {1}", TimeDifference.Days.ToString, TmpDate.Day.ToString+"." +TmpDate.Month.ToString+"."+DateTime.Now.Year.ToString)

String.Format( "{0} days until the date {1}", Math.Abs(TimeDifference.Days).ToString, TmpDate.Day.ToString+ "." + TmpDate.Month.ToString+"."+DateTime.Now.Year.ToString)
```
在序列中使用“ForEach”活动来遍历列表中的所有项目（“变量名中的“ForEach”），并在正文中使用以下活动和方法：

- 创建一个 DateTime 变量（“TmpDate”）并在“Assign”活动中使用“DateTime.ParseExact”方法转换为 DateTime：*TmpDate = DateTime.ParseExact(InputDate, "dd.MM.yyyy", nothing)*
- 使用“If”活动来验证项目的月份是否与当前月份相同：*TmpDate.Month = DateTime.Now.Month*：
- 如果满足条件，请使用“Write Line”活动和“String.Format”方法打印一条消息。
- 如果不满足条件，则添加具有以下活动和方法的序列：一种。创建一个 TimeSpan 类型（“TimeDifference”）的新变量，使用“分配”活动中的“减去”方法计算- 当前月份和项目月份之间的差异： *TimeDifference = Datetime.Now.Subtract(new DateTime(Datetime.Now.Year, TmpDate.Month, TmpDate.Day))*
- 使用“If”活动来验证日期是在未来还是过去，方法是将条件声明为 TimeDifference.Days > 0 并使用“String 'Write Line' 活动中的 .Format' 方法： *String.Format( "{0} days before the date {1}", Math.Abs​​(TimeDifference.Days).ToString, TmpDate.Day.ToString+ "." + TmpDate .Month.ToString+"."+DateTime.Now.Year.ToString*

**流程图**
![在这里插入图片描述](https://img-blog.csdnimg.cn/cd5a509bc8684cd7ad0c92be4e80bb28.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

## 3.3 Practice 3 - Dictionaries and Integers
**计算并打印每个环法自行车赛冠军的胜利次数**

给定一个包含年份和姓名的输入字典，请计算每个获胜者的胜利次数，并打印所有获胜者的名字以及相应的胜利次数。

注意：使用以下值初始化类型为 (Int32, String) 的字典 :
```vbnet
 New Dictionary(Of Int32,String) From {{2006,"Oscar Pereiro"},{2007,"Alberto Contador"}, {2008, "Carlos Sastre"}, {2009,"Alberto Contador"}, {2010, "Andy Schleck"}, {2011, "Cadel Evans"}, {2012,"Bradley Wiggins"}, {2013,"Chris Froome"}, { 2014,"Vincenzo Nibali"},{2015,"Chris Froome"},{2016,"Chris Froome"},{2017,"Chris Froome"},{2018,"Geraint Thomas"}}
```
**实践3解决方案**

- 以序列的形式启动项目并创建一个类型为 (String, Int32) 的新字典

- 使用“For Each”*（“ForEach WinnerNames in FirstDictionaryName.Values”）*循环遍历第一个字典中的值，并使用“If”中的“.ContainsKey”方法检查该值是否已作为新字典中的键存在活动*（“SecondDictionaryName.ContainsKey（WinnerName）”）*：

- 如果满足条件，则使用“分配”活动来增加相应键的值：
	>*WinnerCounts(WinnerName) = WinnerCounts(WinnerName) + 1*![在这里插入图片描述](https://img-blog.csdnimg.cn/41a3283eb6e545f88d83f1b9c530e56f.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_8,color_FFFFFF,t_70,g_se,x_16)
- 如果不满足条件，则使用“调用方法”活动将键添加到值为“1”的第二个字典中，TargetObject 为第二个字典名称，“添加”为 MethodName
- 使用“For Each”（“ForEach 获胜者 in SecondDictionaryName”）循环遍历第二个字典，并使用“If”为那些使用“Write Line”赢得 1 次胜利的人和赢得更多胜利的人编写差异化文本。

**流程图**
![在这里插入图片描述](https://img-blog.csdnimg.cn/5db4712057564edb89ee763973e50202.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

## 3.4 Practice 4 - Dictionaries and Doubles
**计算发往一个城市的包裹的总重量**

考虑一个运输公司的数据库，其中包含人员和他们发送到世界各地某些城市的包裹，以及他们的重量。数据库是一个Dictionary，键是String类型（人名），值是Dictionary（String/Cities，Double/Weight）类型。

请计算一个城市目的地的总重量。完成此操作后，应向用户显示一个输入对话框，其中包含输入数据字典中存在的不同城市列表。如果用户未从输入对话框中选择任何值，则打印“用户未选择任何值”；否则，您可以打印“发送到 <ChosenCity> 的包裹的总重量为 x.xx”（使用两位数）。

**注意**：对于输入数据，请下载下面的工作流程，其中已经定义了字典。

新字典（字符串，字典（字符串，双））从{
{"John C", New Dictionary(Of String, Double) From {{"Madrid",2.1},{"Paris",1.1}} },
{"Sarah C", 新字典(Of String, Double) From {{"New York",2.1},{"Paris",3.3},{"Berlin", 0.8}} },
{"Kyle R", New Dictionary(Of String, Double) From {{"San Francisco",2.8},{"New York",1.1}} },
{"Johnny B", New Dictionary(Of String, Double) From {{"New York",2.1},{"Paris",3.3}, {"Cairo",1.3}, {"Chicago",1.9}} }
**实践4解决方案**

- 按顺序启动项目。
- 使用“For Each”循环遍历初始字典的值，并（在正文中）使用“For Each”循环遍历第二个字典（城市）的键，并检查该城市是否已经在字典中（使用“If”和“包含”方法）：
- 如果满足条件，则使用“分配”活动将存储在相应值中的权重添加到现有值中；
- 如果不满足条件，则使用“调用方法”活动和“添加”作为 MethodName 在字典中添加具有相应值的城市
- 使用“输入对话框”活动通过使用活动属性中“选项”下的 SecondVariableName.Keys.ToArray 来显示所有城市。如果用户选择一个城市，则使用“Write Line”和“String.Format”方法打印组合权重。
- 如果用户没有选择城市，请使用“写行”来显示通用消息。

**序列图**
![在这里插入图片描述](https://img-blog.csdnimg.cn/ac653cef5247466a8306e6baeb41f445.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
**Demo:**
![在这里插入图片描述](https://img-blog.csdnimg.cn/df040445eb9648a1b7216263dd105e6b.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)



## 3.5 Practice 5 - Input Validation
**验证用户的字符串输入**

开发工作流以根据一组规则请求用户文本输入，并将输入验证规则合并到工作流中。
更具体地说，用户输入的字符串必须通过以下验证规则：
- 最小长度：8 个字符
- 以大写字母开头
- 最多 20 个字符
- 允许用户 3 次尝试写入正确的字符串（不考虑用户未键入任何内容的情况）。

注意：请在此练习中使用流程图。

**实践5解决方案**

- 以流程图的形式启动项目（考虑到预期的大量决策点），并通过“消息框”告知用户规则。
- 向用户展示“输入对话框”。
- 检查用户是否在输入字段中输入了任何内容。如果未提供文本，则返回“输入对话框”阶段。
- 使用 RegEx（'Is Match' 活动）验证输入文本 - 'Advanced' 类型，^([A-Z][\w]{7,20})*$
- 使用 Int32 变量来计算用户尝试输入失败的次数（不考虑空输入）。
- 使用决策节点检查用户是否达到 3 次失败尝试。
- 如果用户达到最多 3 次失败尝试，则使用“写入行”活动写入以输出以下消息：“已超出最大重试次数”并结束执行。
- 如果 RegEx 验证通过，则打印以下消息以输出：“您的文本遵循规则！”并结束执行。您可以使用变量来存储呈现给用户的文本。
```
正则表达式：^[A-Z]\S{7,19}$
Demo: ^([A-Z][\w]{7,20})*$
```

**序列图**
![在这里插入图片描述](https://img-blog.csdnimg.cn/ccf53fa66235425297cc5231644f800e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
**Demo:**
![在这里插入图片描述](https://img-blog.csdnimg.cn/eced78dc0a8345f3aae6cf8eda0699da.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

## 3.6 Practice 6 - Replacing Placeholders
**获取输入信息并用它来填充字符串中的占位符**

您有以下模板：“您好 <first_name> <last_name> 先生，我们想邀请您参加下周 <day_of_week> 的开幕活动。请在本周结束前确认。

创建一个工作流以从用户那里获取输入并替换上面短语中提供的输入数据。

注意：请使用上面的文本创建一个字符串变量。

**实践6解决方案**

- 按顺序启动项目并创建 3 个字符串变量来分别存储名字、姓氏和星期几。
- 添加一个包含 3 个输入对话框活动的 While 活动（一个用于名字，一个用于姓氏，一个用于星期几）。
- 对带有输入数据的 3 个字符串中的每一个使用“分配”活动中的“替换”方法：VariableName = VariableName.Replace("<parameter>",StringVariable.Trim)。为了保留格式，请在每个字符串变量后使- 用“Trim”方法来删除任何不需要的空格。
- 使用“写入行”活动打印输出。
**序列图**
![在这里插入图片描述](https://img-blog.csdnimg.cn/18b1cba8c53442a6b106e4b2973e3966.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
**Demo:**
![在这里插入图片描述](https://img-blog.csdnimg.cn/53e97876afa44f28accca65eec4115e1.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

## 3.7 Practice 7 - Extract Email Address

**从字符串中提取电子邮件地址（不使用 RegEx）**

给定一个包含一个电子邮件地址的字符串，创建一个工作流程以在不使用正则表达式的情况下提取电子邮件地址。

注意：对于输入，请使用具有以下值的字符串变量“请使用以下地址与我联系 john.doe@localcompany.com，这是公司电子邮件”

**练习7解决方案**

- 按顺序启动项目并创建 2 个变量（一个 String 和一个 Int32）。使用 2 个“分配”活动 - 第一个用于定位“@”字符，第二个用于存储其索引（通过使用“IndexOf”方法：IndexTextToFind = VariableName.IndexOf("@")）。
- 提取“@”前后的所有文本，并使用“分配”活动将每个文本存储在变量中，例如 EmailAddress_Part1 和 EmailAddress_Part2。
- 仅保留从 EmailAddress_Part1 的最后一个空格字符到末尾的文本部分，并使用“Assign”活动中的“LastIndexOf”方法将其保存到“EmailAddress_Part1”变量中：EmailAddress_Part1.Substring(EmailAddress_Part1.LastIndexOf(" "))。
- 将 EmailAddress_Part2 中的所有文本提取到第一个空格字符（使用“If”检查空格是否存在；如果不存在，则将所有文本视为电子邮件的一部分）。
- 使用“写行”活动打印以输出电子邮件地址：即“电子邮件地址是 john.doe@localcompany.com”。
**序列图**
![在这里插入图片描述](https://img-blog.csdnimg.cn/bbd6ae961c2a40a6bd2d132ba7151bbb.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
**Demo:**
![在这里插入图片描述](https://img-blog.csdnimg.cn/336bd09d6345494db282f72130664f6c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

## 3.8 Practice 8 - Extract Email Address with RegEx
**从字符串中提取电子邮件地址（使用 RegEx）**

给定一个包含一个电子邮件地址的字符串，创建一个工作流以使用正则表达式提取电子邮件地址。

注意：对于输入，请使用具有以下值的字符串变量“请使用以下地址与我联系 john.doe@localcompany.com，这是公司电子邮件”
**练习8解**

- 按顺序启动项目。
- 将“匹配”活动与为电子邮件地址量身定制的 RegEx 一起使用，并使用 IEnumerable 变量来存储它们。
使用“For Each”活动遍历创建的变量中的值，并使用“Write Line”活动和“Value”方法来显示值。
```
正则表达式：\s\w+.?\w+@\w+.\w+,
Demo:((?>[a-zA-Z\d!#$%&'*+\-\/=?^_`{|}~]+\x20*|"((?=[\x01-\x7f])[^"\\]|\\[\x01-\x7f])*"\x20*)*(?<angle><))?((?!\.)(?>\.?[a-zA-Z\d!#$%&'*+\-\/=?^_`{|}~]+)+|"((?=[\x01-\x7f])[^"\\]|\\[\x01-\x7f])*")@(((?!-)[a-zA-Z\d\-]+(?<!-)\.)+[a-zA-Z]{2,}|\[(((?(?<!\[)\.)(25[0-5]|2[0-4]\d|[01]?\d?\d)){4}|[a-zA-Z\d\-]*[a-zA-Z\d]:((?=[\x01-\x7f])[^\\\[\]]|\\[\x01-\x7f])+)\])(?(angle)>)
```
**序列图**
![在这里插入图片描述](https://img-blog.csdnimg.cn/46553c0ed94546fd8560ec94ceccca62.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

**Demo:**
![在这里插入图片描述](https://img-blog.csdnimg.cn/a4a0de22311f43ee8c5fad214fd0732a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

## 3.9 Practice 9 - Calculate a DateTime Difference
**计算两个事件之间的DateTime差异**

给定两个“String”变量，“Server1StartDate”的“Default”值为“19/05/2021 20:15:07”，“Server2StartDate”的“Default”值为“08/03/2021 13:12”： 10”。

计算两台服务器之间的总正常运行时间差异。

**练习9解**

- 开始新的自动化流程。
- 拖放一个新的“序列”活动并将其重命名为“计算总正常运行时间和差异的序列”。添加一个注释来描述它，比如“获取服务器的初始开始日期，从字符串转换为日期时间，计算差异和总正常运行时间。”
- 选择“变量”面板并创建一个字符串类型的新变量，将其命名为“Server1StartDate”并指定“19/05/2021 20:15:07”作为其默认值。
- 选择“变量”面板并创建一个字符串类型的新变量，将其命名为“Server2StartDate”并指定“08/03/2021 13:12:10”作为其默认值。
- 接下来，拖放一个新的“分配”活动并将其命名为“分配当前日期和时间”。选择“收件人”字段，然后按住“CTRL+K”创建一个类型为“System.DateTime”的新变量并将其命名为“DateTimeNow”。在表达式字段中，输入“现在”。
- 接下来，拖放“Multiple Assign”活动并将其命名为“Multiple Assign to Convert from String to DateTime”。
- 选择 To 字段，然后（按住并按“CTRL+K”以）创建一个类型为“System.DateTime”的新变量并将其命名为“Server1ToDateTime”。在表达式字段中，键入“DateTime.ParseExact(Server1StartDate, "dd/MM/yyyy HH:mm:ss",CultureInfo.InvariantCulture)”。
- 选择“添加”以添加另一个变量。选择 To 字段，然后按住并（按“CTRL+K”）创建一个类型为“System.DateTime”的新变量并将其命名为“Server2ToDateTime”。在表达式字段中，键入“DateTime.ParseExact(Server2StartDate, "dd/MM/yyyy HH:mm:ss",CultureInfo.InvariantCulture)”。
- 接下来，拖放另一个“多重分配”活动并将其命名为“多重分配以计算总服务器正常运行时间和差异”。
- 选择 To 字段，然后按住并（按“CTRL+K”）创建一个类型为“System.TimeSpan”的新变量并将其命名为“Server1Uptime”。在表达式字段中，键入“*DateTimeNow.Subtract(Server1ToDateTime).Duration*”。
- 选择“添加”以添加另一个变量。选择 To 字段，然后按住并（按“CTRL+K”）创建另一个类型为“System.TimeSpan”的变量并将其命名为“Server2Uptime”。在表达式字段中，键入“DateTimeNow.Subtract(Server2ToDateTime).Duration”。
- 选择“添加”以添加第三个变量。选择 To 字段，然后按住并（按“CTRL+K”）创建另一个“String”类型的变量并将其命名为“UptimeDifference”。在表达式字段中，输入 '(Server1Uptime.Subtract(Server2Uptime)).ToString("%d\d\ " + "%h\h\ " + "%m\m\ " + "%s\s\ ") '。
- 拖放一个新的“日志消息”活动并将其命名为“显示总正常运行时间”。选择“信息”作为日志级别并输入以下表达式“Server1 已运行“+ Server1Uptime.ToString +” days.hours:minutes:seconds.milliseconds”+vbLf +“Server2 已运行“+ Server2Uptime。 ToString + " days.hours:minutes:seconds.milliseconds"'。
- 接下来，拖放“If”活动并将其重命名为“记录两台服务器之间的正常运行时间差异”。
- 在“条件”字段中键入“Server1Uptime > Server2Uptime”。
- 在“Then”字段中，拖放一条日志消息并将其重命名为“Server1 has been running long”。选择“信息”作- - 为日志级别并输入“服务器 1 具有” + 正常运行时间差异 + “比服务器 2 的额外运行时间”。
- 在“Else”字段中，拖放一条日志消息并将其重命名为“Server2 has been running long”。选择“信息”作为日志级别，然后输入““服务器 2 具有” + UptimeDifference + “比服务器 1 的额外运行时间”。
**Demo:**
![在这里插入图片描述](https://img-blog.csdnimg.cn/e5b5da8dad004b66b4c72c7f3304896b.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)


