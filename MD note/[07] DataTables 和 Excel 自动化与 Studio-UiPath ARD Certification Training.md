>前言：【【非原创】】UiPath Advanced RPA Developer Certification Training的课程资料机翻版。
课程链接：[Link](https://academy.uipath.com/channeldetail/uipath-advanced-rpa-developer-certification-training)
@[toc]
# 学习目标
在本课程结束时，学习者应该能够：
- 创建、自定义和填充 DataTable 变量。
- 使用最常用的 DataTable 操作方法。
- 区分处理 Excel 文件时使用的活动类别：工作簿活动和 Excel 应用程序集成活动。
- 使用特定活动来处理 Excel 文件（读取数据、写入数据、保存文件等）。
- 使用 Select 方法筛选数据表。

**议程：**
- 什么是数据表？
- 使用数据表
- 工作簿和共同活动
- Excel应用范围及具体活动
- 选择方法
- 实践

# 1 关于本课
欢迎！
本课程涵盖使用最广泛的商业工具之一——==Excel==。
我们将使用 UiPath Studio 提供的特定方法和工具，了解处理 Excel 和相关文件（.xlsx、.xls、.csv）的不同方法。我们还将介绍一种用于处理 Excel 文件和数据库的变量——==DataTable==(System.Data.DataTable)。
**您将在本课程中学到什么**
在本课程结束时，您将能够：
1. 创建、自定义和填充 DataTable 变量。
2. 使用最常用的数据表操作方法。
3.  区分使用 Excel 文件时使用的活动类别：工作簿活动和 Excel 应用程序集成活动。
4. 使用特定活动来处理 Excel 文件（读取数据、写入数据、保存文件等）。
5. 使用 **Select 方法**过滤数据表。
# 2 数据表 DataTables
## 2.1 什么是数据表
 在我们开始之前......
 让我们回顾一下 Excel 中的主要概念。
考虑一组公司员工的典型数据库。在 Excel 文件中组织它的自然方式是什么？

![将左侧的概念与右侧的数据片段相匹配。](https://img-blog.csdnimg.cn/986308fc331f47aa8a7d42280999b2f1.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
**什么是DataTables？**
DataTable 是一种变量，可以将数据存储为具有行和列的简单电子表格。您可以根据其唯一的列和行坐标来识别每条数据。将其视为 Excel 工作表的内存表示。
在 DataTables 中，应用了标识列和行的常规约定——**列通过大写字母标识，行通过数字标识**。

**工作表和数据表有什么区别？**
- **DataTable**
DataTable 是单个数据库表的内存表示形式，该表具有行和列的集合。
- **Worksheet**
Excel Worksheet是具有不同可视化选项和广泛的图形用户界面使用的数据的可视化表示。

**数据表是如何创建的？**
创建数据表最常见的活动和方法是：
- **构建数据表活动 The Build Data Table Activity**
通过使用此活动，您可以选择列数和每列的数据类型。此外，您可以使用特定选项配置每一列，例如允许空值、唯一值、自动递增（对于数字）、默认值和长度（对于字符串）。
- **阅读范围活动 The Read Range Activities**
此活动获取工作表（或该工作表中的选择）的内容并将其存储在 DataTable 变量中，该变量可以使用 Ctrl + K 从“属性”面板创建。
- **读取 CSV 活动 The Read CSV Activity**
此活动捕获 CSV 文件的内容并将其存储在 DataTable 变量中。尽管不再常用，但仍有处理此类文档的遗留应用程序或内部构建的应用程序。
- **数据抓取操作 The Data Scraping Action**
UiPath Studio 的此功能使您能够将结构化数据从浏览器、应用程序或文档提取到 DataTable。
- **从文本活动生成数据表 The Generate Data Table From Text Activity**
通过让用户指示**行和列分隔符**，可用于从结构化文本创建数据表。

## 2.2 使用数据表 Working with DataTables
### 2.2.1 视频演示 - 使用数据表：
创建两个数据表，将它们连接到第三个，从后者中删除不必要的列并对条目进行排序。
![在这里插入图片描述](https://img-blog.csdnimg.cn/1019a1b71f284fea8051fefb66c294c8.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

UiPath 提供了广泛的活动，可用于处理 DataTable 变量：
- **添加数据列 Add Data Column**
将一列添加到现有的 DataTable 变量。通过指定数据类型和配置选项（允许空值、请求唯一值、自动递增、默认值和最大长度），输入数据可以是 DataColumn 类型，也可以将列添加为空。
- **添加数据行 Add Data Row**
向现有 DataTable 变量添加新行。通过将每个对象与每列的数据类型进行匹配，输入数据可以是 DataRow 类型，也可以作为 Array Row 输入。
- **构建数据表 Build Data Table**
用于使用专用窗口创建 DataTable。此活动允许自定义每列的列数和数据类型。
- **Clear Data Table 清除数据表**
清除现有 DataTable 变量中的所有数据。
- **Filter Data Table 过滤数据表**
允许使用各种条件通过过滤器向导过滤数据表。此活动可以配置为为活动的输出创建一个新的 DataTable，或者保留现有的 DataTable 并过滤（删除）与过滤条件不匹配的条目。
- **For Each Row in Data Table 对于数据表中的每一行**
用于为 DataTable 的每一行执行特定活动（类似于 For Each 循环）。
- **Generate Data Table From Text 从文本生成数据表**
通过让用户指示行和列分隔符，可用于从结构化文本创建数据表。
- **Join Data Tables 连接数据表**
根据回答问题“如何处理不匹配的数据？”的连接规则，使用连接向导使用彼此通用的值组合来自两个表的行。它是业务场景中最有用的活动之一，在这种情况下，使用多个数据表是很常见的。这就是我们将在接下来的课程中更深入地介绍该主题的原因。
- **Lookup Data Table 查找数据表**
它类似于 Excel 中的 vLookup。您可以在指定的 DataTable 中搜索提供的值，RowIndex 返回其值。或者它可以配置为从具有给定坐标（行索引和目标列）的单元格返回值。
- **Merge Data Table 合并数据表**
用于将指定的 DataTable 附加到当前的 DataTable。该操作比 Join Data Type 活动更简单，因为它有 4 个预定义操作可以对缺失的架构执行。
- **Output Data Table 输出数据表**
使用 CSV 格式将数据表写入字符串。
- **Remove Data Column 删除数据列**
从指定的 DataTable 中删除某个列。输入可能由列索引、列名或数据列变量组成。
- **Remove Data Row 删除数据行**
从指定的 DataTable 中删除一行。输入可能由行索引或数据行变量组成。
- **Remove Duplicate Rows 删除重复行**
从指定的 DataTable 变量中删除重复的行，只保留第一次出现的行。
- **Sort Data Table 排序数据表**
可以根据特定列中的值对数据表进行升序或降序排序。
- **Get Row Item 获取行项目**
根据指定的列从 DataTable 的行中检索值。
- **Update Row Item 更新行项目**
将指定的值分配给 DataTable 行的指示列。

## 2.2.2 重点：加入数据表  Joining DataTables
它是如何工作的？
![在这里插入图片描述](https://img-blog.csdnimg.cn/a68b1ea4880640b18dcd0e4a5aa691a9.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_15,color_FFFFFF,t_70,g_se,x_16)
1. 必须指定三个数据表变量 - 两个输入数据表和一个输出数据表。请注意，前两个的顺序非常重要，因为有一个选项可以保留数据表 1 中的值并且无法更改。
2. 必须选择联接类型 - 有三个选项：

	- Inner：保留两个表中符合联接规则的所有行。任何不符合规则的行都将从结果表中删除。
	- Left：保留 DataTable1 中的所有行，仅保留 DataTable2 中符合 Join 规则的值。空值被插入到 DataTable1 中的行的列中，而这些行在 DataTable2 行中没有匹配项。
	- Full：保留DataTable1 和DataTable2 中的所有行，无论是否满足连接条件。空值被添加到两个表中没有匹配项的行中。
3. 必须配置加入规则（可以有一个或多个规则）：
	- 每个 DataTable 中的一列必须由它们的名称 (String)、它们的索引 (Int32) 或 ExcelColumn 变量指定
	- 必须选择运算符：=（等于）、!=（不等于）、>（大于）、<（小于）、>=（大于或等于）、<=（小于或等于）到）

**我将在哪些业务场景中使用加入数据表？**
联接数据表提供了一种最简单的方法，可以将来自两个来源的数据集中在一处：
- 汇集从 2 个应用程序中提取的 2 个员工数据库
- 检查在营销活动（数据库 2）中联系了哪些客户（数据库 1）
- 检查公司的哪些供应商（内部数据库）申请了公共援助（公共数据库）

# 3 工作簿 Excel
## 3.1  Workbooks and Common Activities
在许多业务场景中，数据库存储在Workbooks （通常称为 Excel 文件或电子表格）中。可以使用我们在前一章中学到的方法以及其他替代方法和工具将这些数据库处理为数据表。是时候看看 RPA 如何处理工作簿了。

UiPath 提供了两种不同的方式来访问和操作工作簿：
- **Workbook** 或文件访问级别
- **Excel** 或 Excel 应用程序集成

它们中的每一个都有优点和局限性。

### 3.1.1 Workbook  - 文件访问级别
所有工作簿活动都将在==后台执行==。
(+) 不需要安装 Microsoft Excel，只需在不使用Excel 应用程序打开文件，就可以更快、更可靠地执行某些操作；
(!) 仅适用于 .xls 和 .xlsx 文件。
(!) 不适用于 .xlsm 文件。
(!) 该文件不应在运行时在 Excel 中打开。
![在这里插入图片描述](https://img-blog.csdnimg.cn/1a9b13dd5c564a868d0858754fd72695.png)
### 3.1.2 Excel - Excel 应用程序集成
UiPath 会像人类一样打开 Excel。
(+) 与 .xls、.xlsx 和 .xlsm 一起工作，并且它有一些与 .csv 一起工作的特定活动。所有活动都可以设置为==对用户可见==或==在后台运行==。**该文件可以在运行时在 Excel 中打开**。
(!) 即使未选中“可见”框，也**必须安装 Microsoft Excel**。如果文件未打开，则将为每个活动打开、保存和关闭该文件。
![在这里插入图片描述](https://img-blog.csdnimg.cn/71fc713f66854e709cb1f0c698ca4ae6.png)
两个访问级别共享一些活动，Excel 应用集成还有更多活动。

### 3.1.3 让我们从常见的活动开始：
- **Append Range 添加范围**
将 DataTable 中的信息添加到指定 Excel 电子表格的末尾。如果工作表不存在，则会创建它。
- **Get Table Range 获取表格范围**
使用 table name作为输入，从指定的spreadsheet 中定位并提取 Excel 表格的范围。
- **Read Cell 读取单元格**
读取给定单元格的内容并存储为==字符串==。
- **Read Cell Formula 读取单元格公式**
从给定单元格读取公式并将其存储为==字符串==。
- **Read Column 读取列**
读取以用户输入的单元格开头的列，并将其存储为IEnumerable <object> 变量。
- **Read Range 读取范围**
读取指定范围并将其存储在 DataTable 中。如果在“Excel 应用程序范围”下的“读取范围”活动中选中“使用过滤器”，它将仅读取过滤后的数据。 “Workbook”下的读取范围活动不存在此选项。
- **Read Row 读取行**
从用户输入的单元格开始读取一行，并将其存储为 IEnumerable <object> 变量。
- **Write Cell 写单元格**
将值写入指定的单元格。如果单元格包含数据，活动将覆盖它。如果指定的sheet 不存在，则会创建它。
- **Write Range 写入范围**
从“StartingCell”字段中指示的单元格开始写入电子表格中 DataTable 变量中的数据。

**想了解更多？**
- [Workbook Activities - UiPath 活动指南](https://docs.uipath.com/activities/docs/system-excel)
- [Excel 集成活动 - UiPath 活动指南](https://docs.uipath.com/activities/docs/app-integration-excel)
## 3.2  Excel应用范围及具体活动
### 3.2.1 Excel应用范围
与 Excel 的集成是通过使用 *Excel Application Scope* 活动实现的。它是一个容器，用于处理指定 Excel 文件的所有其他 Excel 活动都必须放在容器内。执行结束时，指定的工作簿和 Excel 应用程序将==自动关闭==。
*Excel Application Scope* 可以配置为将容器中活动的输出写入不同的文件中。
>重要说明：如果同一工作流处理来自两个或多个 Excel 文件的信息，则必须为**每个文件**使用 Excel 应用程序范围。

**视频演示 - 使用 Excel 文件第 1 部分**
从两个不同扩展名的文件中读取数据，过滤数据表，保留2005年以前的公司数据，并将数据放在一起，并将数据写入不同的文件。
**PS：** 过滤数据表时：
通过读取范围操作从 Excel 读取的所有数字数据都被 UiPath 解释为 ==Double==，因此在筛选向导中用于这些列的比较的值应始终相应地设置格式，
doblue类型 ex: ==Year < 2005.00==
结果表：
![在这里插入图片描述](https://img-blog.csdnimg.cn/dedafd277c744f68ab7cea5845fee6ee.png)

![在这里插入图片描述](https://img-blog.csdnimg.cn/782394d0a2e946a9a9966a42995d523c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

**视频演示 - 使用 Excel 文件第 2 部分**
从数据库中过滤数据并将结果导出到新文件中，提取年龄在 30 岁以下且收入在 10 万以上的员工的姓名。
![在这里插入图片描述](https://img-blog.csdnimg.cn/26c54e89d74e4803a4ecd48a493a640e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

让我们快速回顾一下我们在这个演示中学到的东西：
使用 Excel 文件的标准方法是将数据存储在数据表变量中并执行不同的数据操作活动以获得所需的结果。
要使用 UiPath 工作簿活动读取范围活动获取 Excel 文件中的所有数据，请确保将范围字段设置为空。
使用过滤数据表活动时可以访问过滤向导。
**每次我们在过滤器向导中添加数值时，我们都会在数值后输入“.00”。否则，过滤将失败。**
如果我们想通过多个不一定都为真的条件来过滤数据，我们可以将过滤向导中的条件标准按钮切换为“或”。默认情况下，按钮设置为“And”，当我们想要多个条件都为真时使用。
为了指示我们要处理的列，我们使用了列的名称，因为它往往更可靠，但索引也始终是一个选项。
这就是这个演示！
感谢您的观看和快乐的自动化！
### 3.2.2 Excel App 集成特定活动
- **CSV Activities CSV活动**
这些活动可以使用 DataTable 变量读取和写入 CSV 文件。尽管在 Excel 应用程序集成下可以找到，但**即使它们没有放置在 Excel Application Scope 容器中，它们也能工作**。
> **Append to CSV 附加到 CSV**：将数据表中的信息添加到 CSV 文件，如果它不存在则创建它。活动==不会覆盖==现有数据。
**Read CSV 读取 CSV**：从 CSV 文件中读取所有条目并将它们存储在==数据表==中。
**Write CSV 写入 CSV**：使用 DataTable 中的信息==覆盖== CSV。

- **Range Activities 范围活动**
这些活动可以读取数据、插入和删除行和列，甚至复制/粘贴整个范围。它们类似于 DataTable 下的相应活动，但它们直接在 Excel 文件中工作。

	>**Delete Column 删除列** ：根据名称从 Excel 文件中删除列。
 **Insert Column 插入列**：在 Excel 文件中的某个位置插入一个空白列。
**Insert/Delete Columns 插入/删除列**：根据指定的更改类型添加空白列或删除现有列。 
**Read Column 读取列**：从以开始单元属性字段中指定的单元格开头的列中读取值，并将它们存储在IEnumerable<Object> 变量中。
**Insert/Delete Rows 插入/删除行**：根据指定的更改类型添加空白行或删除现有行
 **Select Range 选择范围**：选择 Excel 文件中的特定范围。通常，它与对所选数据执行某种操作的另一个活动配对。 
 **Get Selected Range 获取选定范围**：将给定范围输出为字符串。 
 **Delete Range 删除范围**：从 Excel 文件中删除指定范围。
 **Auto Fill Range 自动填充范围**：在 Excel 文件中的给定范围内应用给定公式。
 **Copy Paste Range 复制粘贴范围**：将整个范围（值、公式和格式）从源工作表复制并粘贴到目标工作表。 
 **Lookup Range 查找范围**：在给定范围内的所有单元格中搜索一个值。
 **Remove Duplicate Range 删除重复范围**：删除给定范围内的所有重复行。
 **Read Range 读取范围**：读取 Excel 范围的值并将其存储在 DataTable 变量中。如果未指定范围，则读取整个电子表格。如果范围指定为单元格，则读取从该单元格开始的整个电子表格。
**Append Range 追加范围**：将存储在 DataTable 变量中的信息添加到指定 Excel 电子表格的末尾。如果该工作表不存在，则会使用 SheetName 字段中指示的名称创建一个新工作表。 
**Write Range 写入范围**：从“起始单元格”字段中指示的单元格开始，从电子表格中的 DataTable 变量写入数据。如果未指定起始单元格，则从 A1 单元格开始写入数据。如果工作表不存在，则使用 SheetName属性中指定的值创建一个新工作表。
 - **Table Activities 表格活动**
这些活动直接在 Excel 文件中**创建、筛选和排序**表格。
	> **Filter Table 筛选表**：对 Excel 文件内表中列中的所有值应用筛选器。保存文件后，将仅显示符合过滤条件的行。请注意，此活动不会删除不符合条件的行，而只会隐藏它们。此方法的一个很好的用途是在此之后使用读取范围活动，并选中“使用过滤器”框。输出将是一个仅包含满足给定条件的条目的数据表。
**Sort Table 排序表**：根据给定列中的值对 Excel 文件中的表进行排序。
**Create Table 创建表**：它在“属性”面板中指定的范围内创建一个表（带有名称）。
- **File Activities 文件活动**
这些活动通过保存或关闭 Excel 文件直接使用。
	> **Close Workbook 关闭工作簿**
**Save Workbook 保存工作簿**
 
 - **Cell Color Activities 单元格颜色活动**
这些活动能够捕获和修改 Excel 文件中单元格的背景颜色。
	>**Get Cell Color 获取单元格颜色**：读取 Excel 文件中的背景颜色或给定单元格并将其存储为颜色变量输出。
**Set Range Color 设置范围颜色**：更改给定范围内所有单元格的背景颜色。输入是一个颜色变量。
 - **Sheet Activities 工作表活动**
这些活动可以对 Excel 文件中的工作表执行各种操作。
	>**Get Workbook Sheet 获取工作簿表**：通过索引读取工作表的名称。
**Get Workbook Sheets 获取工作簿工作表**：提取工作表名称并按索引顺序存储它们。
**Copy Sheet 复制工作表**：复制 Excel 文件中的工作表并粘贴到同一 Excel 文件或指定的不同 Excel 文件中。
 - **Pivot Table Activities 数据透视表活动**
这些活动有助于处理 Excel 文件中的数据透视表。
	>**Refresh Pivot Table 刷新数据透视表**：刷新 Excel 文件中的数据透视表。这在数据透视表源数据更改时很有用，因为刷新不是自动的。
 **Create Pivot Table 创建数据透视表**：使用指定的工作表和给定的参数创建数据透视表。
 
 - **Macro Activities 宏活动**
这些活动可以执行已在 Excel 文件中定义的宏，也可以从其他文件调用宏。请注意，这些活动适用于 ==.xslm==文件。
	> **Execute Macro 执行宏**
	**Invoke VBA 调用 VBA**：来自另一个文件的宏

**想了解更多？**
[Excel 应用程序集成 - UiPath 活动指南](https://docs.uipath.com/activities/docs/app-integration-excel)
# 4 选择方法 THE SELECT METHOD
## 4.1 视频演示 - Select 方法
使用 select 方法使用多个条件过滤数据表，然后将结果输出到不同的数据表。
ps: Select方法筛选结果为0时会报错。
> ApartmentsDT.Select("[Pet friendly] = 'Yes'").CopyToDataTable
![在这里插入图片描述](https://img-blog.csdnimg.cn/e149399df3244c429ab3b44fd0fb5ac6.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/5d36377e7bcb42b38e0fc85552966ed3.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
## 4.2 Select 方法的语法
让我们来看看我们在演示视频中使用的语法来标识每个组件。
![在这里插入图片描述](https://img-blog.csdnimg.cn/0b259c1f9d274ff689f83b0c52a588d6.png)
- **Apartments**
数据表变量的名字
- **Select**
调用的方法。
- **[Pet friendly]**
要过滤的列之一的名称。此表达式中使用的其他列是 [Price] 和 [Number of rooms]。
- **= 'Yes'**
用来过滤数据表的运算符和值。表达式 [Pet Friendly] = 'Yes' 意味着我们将在 Pet Friendly 列中保留包含值 Yes 的所有行。
- **AND**
可用于使用多个条件搜索数据表的逻辑运算符。需要放置在标准之间。在逻辑运算符之后使用 NOT 时，可用于创建排除标准。

# 5 练习 PRACTICE
## 5.1 Practice 1 - 计算总和
**计算 2 个 Excel 文件中的总和**

以 3 种方式计算 Excel 文件中两列值的总和。创建一个工作流，将 A 列上的值与 B 列上的值相加，并以不同方式将它们写入 C 列：
- 保持 Excel 打开并实时逐行写入结果，以便您可以看到更改。
- 保持 Excel 关闭，在内存 DataTable 中设置列​​值并将所有表一次添加到新的 Excel 文件中，最后。
- 使用原始文件中的 Excel 公式计算总和。
注意：使用下面的 Sample Columns.xlsx 文件作为本练习的输入文件。
1. ![在这里插入图片描述](https://img-blog.csdnimg.cn/c88352bdbca14de586f3c0260cf542bf.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
Demo:
>  dt_InputTable.Rows.IndexOf(Row) + 1 //获取数据表行索引（行对象）
![在这里插入图片描述](https://img-blog.csdnimg.cn/04978c78018945d69e80f7b1a426d188.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

2. ![在这里插入图片描述](https://img-blog.csdnimg.cn/84c462b2055046cc981715c77fffc5ad.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
==Demo:==
> Integer.Parse(ValueA)//将字符串转换为数字
![在这里插入图片描述](https://img-blog.csdnimg.cn/b1f24e6af3714d44936c538804081c8e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)3. ![在这里插入图片描述](https://img-blog.csdnimg.cn/177e472fbc29473ba82bb745167a398e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
==Demo:==
>  dt_InputTable.Rows.Count //返回数据表总行数
![在这里插入图片描述](https://img-blog.csdnimg.cn/356d4b8ca8644ecd919b9a0f788a6df8.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)


## 5.2 Practice 2 -  计算损失发票
**检查发给破产客户的发票**
检查 Excel 文件中的哪些发票是发给破产客户的，并计算要记录为损失的发票总和。
输入文件：
- Invoices (.xlsx)
- Clients (.csv)
![在这里插入图片描述](https://img-blog.csdnimg.cn/252e632b4f364ba8a1d907531639811d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
==Demo：==
![在这里插入图片描述](https://img-blog.csdnimg.cn/b4a1d7fcdabb4ecd8ac4fbdba027b45d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

## 5.3  Practice 3 - 计算费用百分比
**汇总现金和信用卡费用并计算类别的百分比**

我们有一张信用卡支付的费用清单（租金、食物、水电费、休闲、储蓄）。我们发现有些交易丢失了，因为它们是用现金完成的。准备一个工作流，将所有费用放在一个文件中，并计算每项费用的百分比。

输入文件：
- CardPayments (.xlsx)
- CashPayments (.xlsx)
![在这里插入图片描述](https://img-blog.csdnimg.cn/45c5403ce75f448682e1e14f9877b9c3.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
==Demo:==
![在这里插入图片描述](https://img-blog.csdnimg.cn/66a8f4cee6c54cf8af03296b6ed71532.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

# 6 额外资源 ADDITIONAL RESOURCES
==DataTables==
- **DataTable Variables - UiPath Studio Guide**
[Learn more about working with DataTable variables](https://studio.uipath.com/docs/data-table-variables)
- **Programming - UiPath Activities Guide**
[Learn more about DataTable activities](https://docs.uipath.com/activities/docs/programming-system)

==Workbook Activities==
- **Workbook Activities - UiPath Activities Guide**
[Learn more about File-Access Level activities](https://activities.uipath.com/docs/append-range)
- **Excel App Integration - UiPath Activities Guide**
[Learn more about the Excel App Integration](https://activities.uipath.com/docs/append-csv-file)



