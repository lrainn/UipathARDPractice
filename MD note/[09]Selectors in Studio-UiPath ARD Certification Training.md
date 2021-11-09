> 前言：【【非原创】】UiPath Advanced RPA Developer Certification Training的课程资料机翻版。
课程链接：[Link](https://academy.uipath.com/learningpath/selectors-in-studio)

@[toc]
# 1 关于课程
欢迎！
在本课程中，我们将了解 UI 自动化活动的主要定位方法：**选择器**。我们将首先熟悉这个概念，然后我们将进入更深入的主题，例如选择器的类型、UI 资源管理器、属性资源管理器以及配置选择器以处理不同情况。

您将在本课程中学到什么

在本课程结束时，您应该能够：
- 解释什么是选择器以及它们是如何工作的。
- 自动化时选择正确的选择器类型和设置。
- 描述如何探索用户界面元素的属性。
- 微调选择器以提高元素识别精度。
# 2 介绍Selectors
## 2.1 什么是Selectors选择器？
UiPath Studio 中的选择器是一项功能，可通过其**地址**和**属性**识别特定的用户界面元素。这些存储为 **XML 片段**。
完成元素识别以执行自动化项目中的特定活动。每次我们使用与图形用户界面元素交互的活动时，都会自动生成选择器。

我们可以将通过选择器实现的元素识别过程看作是将信件发送到某个地址的邮递员。为了让邮递员递送信件，需要特定路径并且必须包含结构化和分层的详细信息，例如国家 > 城市 > 邮政编码 > 街道名称 > 街道编号 > 公寓号。同样，UiPath Studio 需要用户界面中特定元素的详细路径。

**选择器在哪些业务场景中很有用？**
大多数情况下，当自动化流程涉及使用 **UI 元素**时，会使用选择器。典型的活动包括：
- 单击按钮。
- 在网站上的字段中输入或抓取文本。
- 从下拉列表中选择一个选项。

**视频演示 - 选择器简介**

在本视频中，我们将介绍选择器、它们的生成方式以及使它们更可靠的选项。
**视频抄本**
——
选择器是 UI 自动化活动的属性。它们包含作为 XML 片段的每个图形用户界面元素及其父元素的属性。每次我们使用与图形用户界面元素交互的活动时，都会**自动生成选择器**。
现在，让我们检查一下选择器的**属性**。
在 UI Explorer 窗口中，我们可以通过单击每个节点前面的箭头来展开或隐藏相应的部分来导航 UI 层次结构树。这就是 XAML 片段中的每一行在应用程序界面中的映射方式。组成选择器的 XAML 片段包含标记和属性。属性使我们能够在所选应用程序的特定级别与 UI 元素进行交互。
**首先，一些网页为其组成的元素生成动态 ID**。
每次我们刷新页面时，ID 属性的值都会发生变化，这意味着每次执行自动化项目时都不能可靠地使用它来识别字段。
**其次，生成的选择器可能过于具体。**
想象一个我们需要与多个相似元素一个一个交互的案例。我们将考虑两个 PDF 发票的示例。
让我们打开 UI Explorer 并指出第一个文件。我们可以注意到 PDF 文件的名称存储在 title 属性中。
当我们选择第二个文件时，选择器也会改变，因为文件名不同。因此，需要更改选择器以启用对两张发票的处理。
**继续前进，在自动化易于系统更改的应用程序时也必须调整选择器。**
例如，如果应用程序的版本或名称发生变化，则必须以识别不同版本的方式调整选择器属性。此外，一些选择器包含一个名为 **IDX** 的属性。该属性是当前元素在其包含多个相似元素的容器中的索引。建议将 IDX 属性替换为更可靠的属性，即使网页更新和索引变得不同，也要检测到项目。

**让我们快速回顾一下这个演示的关键要点。**

选择器是 UI 自动化活动的属性，可帮助机器人识别 UI 元素。它们包含作为 XML 片段的每个图形用户界面元素及其父元素的属性。可以从选择器编辑器或 UI 资源管理器中查看和编辑选择器。

选择器需要微调的一些示例是，**当目标元素包含动态 ID、选择器过于具体或包含 IDX 时**。

感谢您的观看和快乐的自动化！


## 2.2 选择器的结构

==用户界面 (UI) 是使用一系列嵌套在另一个中的容器构建的。==
让我们以 MyCRM 应用程序中名字输入字段的选择器为例，并尝试理解结构的含义。
![在这里插入图片描述](https://img-blog.csdnimg.cn/4898af3ae6fc4113b6b6f1ceb5bd6271.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_17,color_FFFFFF,t_70,g_se,x_16)
- **根节点** 
这对应于最高级别的容器，例如应用程序。 
	```xml
	<wnd app='mycrm.exe' ctrlname='Form1' />
	```
- **节点 2 蓝框** 
这标识了可以编辑数据的整个区域。 
	```xml
	<wnd ctrlname='tabControl1' />
	```
- **节点 3 橙框** 
如您所见，控制区域有 3 个选项卡。此节点标识人员选项卡。
	```xml
	 <wnd ctrlname='tabPagePeople' />
	```
- **节点 4 紫框** 
这标识了 People 选项卡的 Name 类别。如您所见，还有其他类别，地址是可见的。
	```xml
	 <wnd ctrlname='groupBox5' />
	```
- **节点 5 红框** 
这实际上是我们感兴趣的 GUI 元素。它对应于 First 字段的可编辑字段。 
	```xml
	<wnd ctrlname='textBoxPeopleFirstName' /> <ctrl name='First:' role='editable text' />
	```

### 选择器的标签和属性 Tags & Attributes of Selectors
如您所见，选择器由节点nodes组成。每个节点由标签tags 和属性attributes组成。让我们举个例子来解释这两者。下面是一个选择器节点。
```xml
<webctrl parentid='slide-list-container' tag='A' aaname='Details' class='btn-dwnl' />
```
**Tags 标签  **
- 选择器 XML 片段中的节点
- 对应屏幕上的一个视觉元素
- 第一个节点是应用程序窗口
- 最后一个节点是元素本身
例如：
- wnd（窗口）
- html（网页）
- ctrl（控制）
- webctrl（网页控件）
- java（Java应用程序控制）

**Attributes 属性**
每个属性都有一个名称和一个值。您应该只使用具有常量或已知值的属性。
例如：
- parentid=‘slide-list-container’
- tag=‘A’
- aaname=‘Details’
- class=‘btn-dwnl’

**想了解更多？**
[关于选择器 - UiPath Studio 指南](https://docs.uipath.com/studio/v2020.10/docs/about-selectors)

# 3 The UI Explorer
## 3.1 The UI Explorer是什么？
(中文：用户界面探测器)UI Explorer 是 UiPath Studio 中的功能，可让您分析和编辑选择器。它包含一个**状态按钮**，向用户显示选择器的状态，一个**可视化树面板**，显示当时正在运行的每个应用程序的可导航 UI，以及选定的 UI 元素。 UI Explorer 显示所有可用的标签和属性，并为您提供检入或检出它们的选项。
**我将在哪些业务场景中使用 UI Explorer？**
当自动生成的选择器不够稳定或不够可靠时，可以使用 UI Explorer。例如，当：

- 选择器从一个执行更改为另一个执行。
- 选择器可能会随着产品更新而更改。
- 选择器使用不可靠的信息，例如索引。
## 3.2 The UI Explorer Interface
![在这里插入图片描述](https://img-blog.csdnimg.cn/d885c7f6c0594689a3aa55f5d2c3b0a5.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
### 用户界面框架
为了返回感兴趣元素的最佳选择器，我们可以在 UiExplorer 中可用的不同 UI 框架之间切换。

- **Default**
这是一种专有方法，通常适用于所有类型的用户界面。
- **Active Accessibility**
这代表了 Microsoft 的早期解决方案，使应用程序可访问。如果默认框架无法按预期工作，建议在使用**旧版**软件时使用。
- **UI Automation**
这是 Microsoft 改进的辅助功能模型，建议在使用**较新**的应用程序时使用，以防默认框架无法按预期工作。


**Video demo - Editing a selector using the UI Explorer** 
这就是今天的全部内容。快速回顾一下：
UI Explorer 允许我们为特定的 UI 元素创建自定义选择器。
Visual Tree 面板显示 UI 层次结构的树，使我们能够通过单击每个节点前面的箭头来浏览它。选择器编辑器面板显示指定 UI 对象的选择器并允许您对其进行自定义。
面板的底部显示了我们必须在项目中使用的实际 XML 片段。 Selector Editor 面板的顶部使我们能够查看选择器中的所有节点，并通过清除它们前面的复选框来消除不需要的节点。
选择器编辑器工具与 UI Explorer 非常相似，但仅包含两个面板。

### The Property Explorer 属性资源管理器
**它是什么？**
属性资源管理器是 UI 资源管理器的一项功能，它显示**某个 UI 元素的所有属性**，包括那些未在选择器中显示的属性，如位置、可见性、内部文本等。

**我将在哪些业务场景中使用 Property Explorer？**
- 当您想在某个属性更改其值后开始活动时（使用等待属性活动）。
- 当您想要更改网页上某个属性的值时，例如其可见性（使用“设置属性”活动）。
- 当您想通过检查属性来检查某个 UI 元素的状态时（使用 Get Attribute 活动）。

**视频抄本**
![在这里插入图片描述](https://img-blog.csdnimg.cn/f1c66a6a17ff48e1a6cb359afbe5fd61.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
**想了解更多？**
[UI 资源管理器 - UiPath Studio 指南](https://docs.uipath.com/studio/v2020.10/docs/uipath-explorer)
# 4 Types of Selectors 选择器的类型
如前所述，当在活动中指示 UI 元素或使用记录器时，会**自动生成选择器**。当容器内部生成的活动移到外部或相反时，了解**完整选择器**和**部分选择器**之间的区别非常重要。
UI 自动化经典体验容器(The UI automation classic experience containers)是附加窗口、附加浏览器和打开浏览器。

1. **Full selectors 完整选择器**
	- 包含标识 UI 元素所需的所有标签和属性，包括顶级窗口；
	- 由基本记录器生成；
	- 最适合执行的操作需要在**多个窗口之间切换**时。
![在这里插入图片描述](https://img-blog.csdnimg.cn/8fcb25421c444f35886463e079ad9a27.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_17,color_FFFFFF,t_70,g_se,x_16)

2. **Partial selectors 部分选择器**
	- 不包含顶层窗口的标签和属性，因此带有部分选择器的活动必须**包含在容器**中；
	- 由桌面记录器生成；
	- 最适合在**同一窗口**中执行多个操作。
![在这里插入图片描述](https://img-blog.csdnimg.cn/4519a0473b604c87935951385991e589.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_17,color_FFFFFF,t_70,g_se,x_16)

**何时使用部分选择器和完整选择器？**
==Full selectors==:
使用**部分选择器**的最佳示例是简单的自动化，其中部署的工作流仅在**同一应用程序**中执行操作，而无需在多个窗口之间切换，就像简单的 CRM。

==Partial selectors==:
另一方面，如果工作流实际上需要与**多个窗口交互**，例如上面示例中的 CRM 和文档。这会使 UI 元素分散在多个窗口中，因此需要完整的选择器。
**想了解更多？**
[完整选择器与部分选择器 - UiPath Studio 指南](https://docs.uipath.com/studio/v2020.10/docs/full-versus-partial-selectors)
# 5 Fine-tuning 微调
## 5.1 什么是微调Fine-tuning？
微调是==优化选择器==的过程，以便在生成的选择器不可靠、过于具体或对系统更改过于敏感的情况下正确执行工作流程。
它主要由对整个过程有较大影响的小的简单更改组成，例如**添加通配符**、**使用修复功能**或**使用选择器中的变量**。

**有哪些业务场景需要微调？**

- 工作流使用名称中带有**时间戳**的文件。
- 构建工作流的环境与生产环境（例如，应用程序版本）具有**不同的参数**。
- 动态选择器的使用将提高自动化的可靠性和稳健性。

**什么时候需要对选择器进行微调？**

- **动态生成的选择器**
正如某些网站所发生的那样，每次访问时属性的值都会发生变化。
- **选择器过于具体**
一些选择器是使用文件名或更改的值自动生成的。在这里，占位符非常有用。
- **系统更改**
某些选择器包含应用程序版本或更新应用程序时更改的其他元素。
- **使用 IDX 的选择器**
IDX 是具有多个相似元素的容器中当前元素的索引。当一个新元素出现在同一个容器中时，这可能会改变。

## 5.2 我们如何微调选择器？
**使用通配符**
通配符是使您能够替换字符串中的零个或多个字符的符号。这些在处理选择器中动态变化的属性时很有用。
- 星号 (*) – 替换零个或多个字符
- 问号 (?) – 替换单个字符

**使用变量**
变量用作目标标签属性的属性。这允许选择器根据变量或参数的值轻松识别目标元素，而不是可能会更改的确切字符串。
可以更改变量以与不同的元素交互，而无需更改选择器本身。

**使用索引变量**
索引变量用于根据它们在列表中的**数字位置**访问 UI 元素，或访问数组或结构中的特定 UI 元素。它们通过识别 UI 元素的属性来工作，这些属性是**连续的数值**。
当数据存储在列表结构中并且您想根据它们的**位置或数值**引用它们时，我们使用索引变量。它们存储在具有特定数值的定义变量中。例如：
> webctrl tableCol='6' tag='TD'tableRow='{{int_Index}}'/>

**视频演示 - 在选择器中使用通配符**
我们将使用通配符替换选择器中的值以提高其可靠性。

让我们快速浏览一下关键要点。在处理一系列文件或页面时，可能需要微调选择器以应用于系列中的每个单独项目。使用**通配符**是实现这一目标的好方法。您可以通过**单击修复自动添加通配符或通过编辑选择器手动添加通配符**。可用的通配符是星号和问号。星号替换零个或多个字符，而问号恰好替换一个。

**视频演示 - 使用变量微调选择器**
我们将构建一个工作流并使用选择器中==变量的动态值==来正确识别 UI 元素。

**视频演示 - 在选择器中使用索引变量**
我们将构建一个工作流，在该工作流中我们将在 Selector 中使用**递增索引变量**。

**想了解更多？**
[带通配符的选择器 - UiPath Studio 指南](https://docs.uipath.com/studio/v2020.10/docs/selectors-with-wildcards)
[动态选择器 - UiPath Studio 指南](https://docs.uipath.com/studio/v2020.10/docs/dynamic-selectors)
# 6 Managing Difficult Situations 处理困难情况
在大多数自动生成的选择器不够可靠的情况下，微调将解决问题。但是，还有一些其他情况，我们称之为困难。考虑**在每次运行工作流时更改状态、位置或 ID 的 UI 元素的示例**。
对于这些，还有其他方法：

- **Anchor base 锚点**
这在属性值不可靠（例如，在每次执行时生成）但存在**稳定且链接到目标 UI 元素**的 UI 元素的情况下非常有用。
Anchor Base Activity 有两部分，一是定位锚 UI 元素（比如‘Find Element’），二是执行想要的 Activity

- **Relative selector 相对选择器**
此活动基本上将有关锚点选择器的信息合并到目标 UI 元素的选择器中。然而，新的选择器可能需要额外的编辑，因为第一个选择器的一些节点仍然在新的选择器中。解决方案是删除该部分（如动态 ID），然后选择器将使用锚点的选择器稳定下来。

- **Visual tree hierarchy 可视化树层次结构**
可视化树中的层次结构可以通过包含层次结构中上方元素的标签和属性来提高选择器的可靠性。
**当目标 UI 元素的选择器不可靠，但层次结构中正上方 UI 元素的选择器可靠时**，这非常有用。但是，再次选择器需要进一步编辑和验证，因为需要删除动态部分，同时您需要确保可以使用唯一属性标识目标元素。

- **Find children 寻找子元素**
当目标元素不稳定时，通过识别它的稳定父元素，并获取此父元素的所有子元素且遍历，根据子元素的某个特有且稳定的属性来定位子子元素并输出。
此活动可以识别更稳定的元素的所有子元素。由于它的输出是子元素的集合，因此您需要想出一种机制来仅识别目标 UI 元素（使用其属性之一，这使得子元素之间是唯一的，但不足以普遍识别它）。

**视频演示 - 管理困难情况**
我们将使用 Anchor Base、Relative Selector、Visual Tree Hierarchy 和 Find Children 来提高选择器的可靠性。

快速回顾一下，在某些情况下，可靠地识别 UI 元素可能需要更高级的技术。在本视频中，我们演示了==锚点==、==相对选择器==、==可视化树==和==查找子项方法==。
**Anchor Base** 使用一个稳定的元素来对一个不太稳定的相关元素执行操作。
**相对选择器**的工作方式类似，通过在 UI Explorer 中单击“指示锚点”生成。
**可视化树方法**需要分析 UI 资源管理器中的目标元素和父节点，以识别使选择器更可靠的属性组合。
**Find Children** 允许我们指示一个稳定的容器并将其子 UI 元素作为集合检索。我们可以遍历结果并过滤我们想要的元素。
为了标识目标，UI 自动化活动可以在 Selector 属性中使用类型为 string 的选择器，也可以在 Element 属性中使用类型为 UI Element 的对象，但**不能同时使用两者**。


**想了解更多？**

[Anchor Base - UiPath 活动指南](https://docs.uipath.com/studio/docs/about-selectors)
[寻找孩子 - UiPath 活动指南](https://docs.uipath.com/activities/docs/find-children)
# 7 练习
## 7.1 Practice 1 - Get and Sort Data
**练习 1 - 获取和排序数据**

创建一个工作流，生成 10 个假姓名及其详细信息，然后将它们排序在一个 excel 文件中，该文件将组织成 5 列，即：姓名、电话、出生日期、电子邮件地址和城市、州、邮编。在对所有详细信息进行排序后，工作流应继续将 excel 文件保存在指定文件夹中。

**Notes:** 
使用 *www.fakepersongenerator.com* 站点生成 10 个假名及其详细信息。
所有选择器不得包含 idx 属性。
从第一个记录生成开始到将 Excel 文件保存在特定文件夹中的最后一个活动的所有活动都应在一个工作流执行中进行处理。

**实践1解决方案**
添加“选择文件夹”活动以询问用户将放置 Excel 文件的文件夹。将结果保存到变量 ("theOutputFolder)
添加输入对话框以要求用户提供 Excel 文件名。将结果保存到变量 (fileName)
添加构建数据表活动。单击 DataTable 并添加五列。所有列都必须是字符串类型。
创建一个 Int32 类型变量（“Number Generator”）并使用 Assign 活动将其值设置为 10。这将用作我们将很快添加的 While 活动的计数器。
添加一个打开浏览器活动，在 URL 字段中创建一个新变量（“FakePersonGenerator”）并添加 https://www.fakepersongenerator.com/ 作为其默认值。
添加一个 While 活动并将条件设置为 NumberGenerator > 0。在 While 活动的 Do 容器内：
添加点击活动并使用“在屏幕上显示”来选择“生成”按钮。检查选择器。这里没有idxs。
获取姓名：添加“获取文本”活动并使用“在屏幕上指示”来选择此人的姓名。检查选择器。我们有了第一个 idx。要解决这个问题：
单击在 UI 资源管理器中打开并检查 parentclass 属性。这应该使它足够具体并解决我们的问题。
要获取城市、州、邮编：添加获取文本活动并使用屏幕上的指示来选择网站上的城市、州、邮编值。将结果存储在新变量 citiyStateZip 中。
检查选择器。我们有一个 idx。要解决这个问题：
单击在 UI 资源管理器中打开或直接打开 UI 资源管理器并确保“可视化树”面板已打开。
使用突出显示并检查最低级别的父级，您可以在其中使用不同的属性，例如 aaname 而不是 idx。
在我们的例子中，它是自下而上的第三个。
选择父级的复选框和 aaname 属性的复选框。
将 aaname 属性更改为 aaname='Gender:* 种族：* 生日：*（* 岁） 街道：* 城市、州、邮编：* 电话：* 手机：*'。您会注意到此级别的 idx 消失了。
选择属性lower并检查aaname属性。
将 aaname 属性更改为 aaname='City, State, Zip: *'
所有的 idx 都应该在这里消失。
对以下值（姓名、电话、出生日期和电子邮件地址）重复此过程。您可能会发现有些比较棘手。为每个案例创建一个单独的变量。
广告添加数据行活动。
在 Array Row 输入字段中输入 {TheName, ThePhone ,TheBirthdate ,TheEmail, cityStateZip }。
将 OutputDtataTable 变量输入到数据表属性中
添加值为 Number Generator = Number Generator - 1 的 Assign 活动
在 while 循环之后，添加一个写入范围活动。2
在 Workbookpath 字段中添加以下表达式：TheOutputFolder+"\"+FileName+".xlsx"
将 OutputDataTable 添加到 DataTable 字段。
保存并运行工作流。

**序列图**
![在这里插入图片描述](https://img-blog.csdnimg.cn/cf7237b4d5104638938ac4113d0f7e72.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
## 7.2 Practice 2 - Set Data
创建一个工作流，使用将从此处提供的 Excel 文件中获取的有组织的数据填充网站的字段。它包含以下数据：CompanyName、RoleInCompany、Address、Email、FullName、PhoneNumber。

Notes: 
- 必须从 excel 文件的全名列中获取名字和姓氏。
- 在本练习中仅使用**基于锚点**的选择器。

**实践2解决方案**

1. 以序列形式启动项目，为其命名并添加注释。
2. 使用“读取范围”活动在新创建的 DataTable 变量（“namesDataTable”）中输出 Excel 文件中的数据
3. 使用“打开浏览器”容器打开 www.rpahallenge.com。在容器中，使用“For Each Row”循环遍历 DataTable 变量的每一行。在身体里：
	- 使用 5 个“键入”活动在相应字段中输入每个单元格的数据。使用“指示锚点”编辑每个“键入”活动的选择器。使用 row(n).ToString 定位右单元格，其中 n 是右列的从零开始的索引
	- 创建 2 个字符串变量以使用它们来分配名字和姓氏的值
	- 使用 2 个“分配”活动来隔离和分配两者的值。使用以下字符串方法：
	Row(4).ToString.Substring(0, Row(4).ToString.IndexOf(" ")) 用于“FirstName”变量
	Row(4).ToString.Substring(Row(4).ToString.LastIndexOf(" ")) 用于“LastName”变量
	- 使用 2 个“输入”活动在相应字段中输入来自“名字”和“姓氏”变量的数据。使用“指示锚点”功能编辑选择器
	- 对“提交”按钮使用“点击”活动。以与之前活动相同的方式编辑选择器。

**序列图**
![在这里插入图片描述](https://img-blog.csdnimg.cn/7c48ee0b26204d13880d7073050a5fe0.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
## 7.3 Practice 3 - Highlight WFT Type Items
**练习 3 - 在 ACME 上突出显示 WFT 类型的项目**

创建一个流程，导航到 ACME (*www.acme-test.com*) 中的 Work Items 页面并突出显示表格第一页上的 Type 单元格。

询问用户要突出显示什么工作流类型（WI1、WI2、WI3、WI4 或 WI5）。
导航到 *https://acme-test.uipath.com/work-items*。
逐个突出显示第一页“类型”列中与用户选择匹配的所有单元格。
**Notes:**
您将需要一个 ACME 帐户来进行此练习。如果没有，请确保创建它
在开始练习之前，请确保转到“用户选项”和“重置测试数据”。
确保已在 Internet Explorer 页面中打开 ACME 网站。此外，在运行自动化之前，请确保您已登录。

**实践3解决方案**

- 以序列的形式启动项目，为其命名并添加注释。
- 使用输入对话框活动为用户提供在 5 种类型之间进行选择的选项。在属性面板的指定字段中写入 5 个选项，并将选项存储在新创建的变量（“SelectedValue”）中。
- 使用附加浏览器容器。在容器中：
- 添加导航活动以转到 **https://acme-test.uipath.com/work-items**。
- 使用范围为 Find Descendants 的 Find Children 活动来检索主容器的所有子项。将过滤器设置为 "<webctrl aaname='"+ SelectedValue + "'/>"。使用新创建的变量来存储结果。
- 使用 For Each 活动循环遍历子项。确保选择正确的参数类型 (UiElement)。
在 Body 中，使用 Highlight 活动并为 Element 属性提供项目迭代器。
```xml
MY:"<webctrl isleaf='1' tableCol='4' tag='TD' aaname= '"+ChoosenTypeStr+"' />"
Demo:"<webctrl aaname='"+ SelectedValue + "'/>"
```
PS:实测用aaname属性就可唯一标识该元素。因该页面aaname为唯一值。
**序列图**
![在这里插入图片描述](https://img-blog.csdnimg.cn/9e32fc099acd45179f080d928f447b21.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

**Demo:**
![在这里插入图片描述](https://img-blog.csdnimg.cn/e20f3cc5f3c64d09bfc6562d066e740a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
# 8 Learning Resources
**UiPath Documentation**

- [About Selectors - UiPath Studio Guide](https://docs.uipath.com/studio/v2020.10/docs/about-selectors)
- [Selectors with Wildcards - UiPath Studio Guide](https://docs.uipath.com/studio/v2020.10/docs/selectors-with-wildcards)

- [Full versus Partial Selectors - UiPath Studio Guide](https://docs.uipath.com/studio/v2020.10/docs/full-versus-partial-selectors)

- [UI Explorer - UiPath Studio Guide](https://docs.uipath.com/studio/v2020.10/docs/uipath-explorer)

- [Anchor Base - UiPath Activities Guide](https://docs.uipath.com/studio/docs/about-selectors)

- [Find Children - UiPath Activities Guide](https://docs.uipath.com/activities/docs/find-children)
