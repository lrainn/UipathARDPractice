前言：【【非原创】】UiPath Advanced RPA Developer Certification Training的课程资料机翻版。
课程链接：[Link](https://academy.uipath.com/learningpath/orchestrator-for-rpa-developers)

@[toc]
# 1 关于本课程
欢迎！

**Orchestrator 是 UiPath 平台的核心，为自动化和机器人提供管理功能。**这可以应用于小型部署以及企业规模，其中组织建模也是必要的。

我们在这里从 RPA 开发人员的角度介绍 Orchestrator。我们将更多地坚持在开发中使用 Orchestrator 功能以及它们在运行时的工作方式，而不是在管理方面。除此之外，我们还将研究使用 Orchestrator 作为库、资产( **assets**)等存储库的可能性。

**您将在本课程中学到什么**

在本课程结束时，您应该能够：

- 定义 Orchestrator 的用途和主要功能。

- 描述 Orchestrator 实体及其用途，并区分 tenant context和 folder context。

- 从 Orchestrator 创建、配置和供应无人值守机器人。

- 使用无人值守机器人以不同方式执行作业 ：作为单独作业、队列或大规模部署。

- 描述如何在 Orchestrator 中分​​配和使用许可证。

- 建立大规模无人值守的机器人劳动力。

- 直接在 Studio 中使用 Orchestrators 资源。

- 在 Orchestrator 中发布、安装和更新库和模板。

- 将文件存储在storage buckets中并在自动化项目中使用它们。

- 使用触发器和 SLAs 自动执行作业。
# 2 先决条件 Prerequisites
我需要什么技术设置？
1. **UiPath Orchestrator 的演示实例**
	
	如果您工作的公司有用于开发或测试的 Orchestrator 实例，请请求访问。您将需要一个 Studio 许可证和一个无人值守许可证。
	
	如果您无法确保这一点，UiPath 自动化云的社区计划始终是一个选项。它为您提供所需的一切，包括 Orchestrator、有人值守许可证和无人值守许可证。立即访问以下链接创建您的帐户。
2. **UiPath Studio 安装在您的机器上并连接到 Orchestrator**
	
	您将需要它来跟进项目的开发，以及利用 Studio 和 Orchestrator 之间的协同作用。
	如果您不知道该怎么做，请返回学院并查找 RPA 开发入门课程。

3. **一个单独的工作站来安装您的无人值守机器人**

	只要连接到互联网，一台简单的 Windows 机器就可以做到。更好的是，Windows 服务器计算机或虚拟机将允许您在更大范围内尝试无人值守自动化。
# 3 Orchestrator概述
## 3.1 介绍 UiPath Orchestrator
### 3.1.1 什么是Orchestrator？

Orchestrator 是 UiPath 平台的组件，用于管理自动化、机器人和相关实体。尽管有不同的云和本地部署选项以及由节点、服务器和高可用性功能组成的相当复杂的基础设施，但用户可以通过简单的 Web 界面访问它。

Orchestrator 提供**基于角色的访问控制**以及**租户和文件夹结构**来复制组织结构。用户可以使用无人值守的机器人劳动力运行在 Studio 中开发并发布到 Orchestrator 的自动化工作流。**此外，Orchestrator 用于管理和分发许可证，以及存储自动化资源。**

### 3.1.2 Orchestrator 的主要功能是什么？

- **Provisioning**：创建并维护与机器人和参与用户的连接。

- **控制和许可证分发**：启用许可证、角色、权限、组和文件夹层次结构的创建、分配和维护。

- **以无人参与模式运行自动化作业**：支持以各种方式创建和分发自动化作业，包括通过队列和触发器。

- **自动化存储和分发**：允许对自动化项目、资产和凭证以及自动化中使用的大型文件进行受控存储和分发。

- **Monitoring**：允许监控作业和机器人并存储日志以进行审计和分析。

- **Inter-connectivity**：充当第三方解决方案或应用程序的集中通信点。

## 3.2 Orchestrator 实体、租户和文件夹
### 3.2.1 Orchestrator entities
我们先来看看 UiPath 平台的核心 RPA 组件是如何协同工作的。让我们熟悉所涉及的实体。
![在这里插入图片描述](https://img-blog.csdnimg.cn/0beb1e3d0f9f4b73a99d2730e6e6936f.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
**现在让我们快速回顾一下这些实体：**

- **Robot (Orchestrator entity)**
现在您已经熟悉了 UiPath 平台的组件 UiPath Robot。这是一个执行主机，它运行在 Orchestrator 中作为作业发布的自动化进程。
在 Orchestrator 中，机器人实体代表图像或机器人组件，控制其连接和功能。机**器人实体仅在与 Orchestrator 中的用户相关定义时才存在。**
- **Folder**
文件夹支持自动化实体（流程、队列、资产）的分离和分层组织以及角色和权限的细粒度配置。
分层结构允许每个一级文件夹下最多 **6 个**子文件夹。
文件夹有助于复制组织层次结构，将团队之间的自动化流程分离、流程数据隔离和用户访问控制。同时，在有意义的情况下，它们允许共享资源和资产。
- **Package**
在 UiPath Studio 中开发的项目，作为 NuGet 包发布到 Orchestrator。可以存储和使用同一项目的多个版本。
包也可以手动上传到 Orchestrator。
- **Process**
它是已分配到某个文件夹的包的版本。
- **Job**
作业表示在 UiPath 机器人上执行流程。您可以在有人值守或无人值守模式下启动作业的执行。您**不能在有人值守的机器人上从 Orchestrator 启动作业**，除非使用个人工作区进行调试，并且它们不能在锁定屏幕下运行。
- **Heartbeat**
有人值守和无人值守的机器人每 30 秒向 Orchestrator 发送一次心跳。这会向 Orchestrator 发出信号，表明连接正在工作。
### 3.2.2 Tenants and folders 租户和文件夹
就像文件夹一样，tenants旨在在 Orchestrator 的同一实例中复制组织层次结构。

从层次结构的角度来看，文件夹是tenants的细分。虽然在文件夹的情况下更多的是关于层次结构和分离，但tenants之间显然是相互隔离的。

考虑一家典型的大公司，其中数据和业务流程通常在销售和财务等部门之间分开。但是，这些细分部门会将一些数据或一些流程分开，同时共享其他数据。

在 Orchestrator 中，一些实体存在于tenants context中，而其他实体存在于 folder context中：

#### Tenant entities
从上面定义的实体来看，==Robot==是租户实体。这意味着**它们可以分配到该租户中的多个文件夹**。使用角色和权限，可以自定义机器人处理每个文件夹的方式。我们稍后会看到。

使用提要( feeds)将包发布到 Orchestrator。订阅源可以配置为租户级别或文件夹级别。然后可以在任何文件夹中的流程中使用发布到租户源的包。如果它是使用文件夹源发布的，则不能用于其他文件夹中的进程。

还有一些其他 Orchestrator 实体存在于租户级别：
- **User**
在 Orchestrator 中，人类用户和机器人都被唯一标识为用户。
- **Machine (Orchestrator entity)**
这些是与人类用户和机器人工作的工作站相对应的 Orchestrator 实体。使用 API 密钥，它们可以启用物理机和 Orchestrator 之间的连接。
- **License**
使用 Studio 和/或机器人（有人值守和无人值守）的权利是通过许可证获得的。**许可证存在于租户级别**，从那里分发给用户，并在计算机连接到 Orchestrator 时使用。
- **Webhook**
Webhooks 在 API 级别促进 Orchestrator 和其他应用程序之间的通信。这些是在租户级别映射的，这意味着它们无法在文件夹之间进行区分，并且将为整个租户提供信息。

#### Folder entities
From the entities defined at the beginning of the lesson,  ==processes== and ==jobs== are folder entities.Packages depend on the feed configuration.

除此之外，文件夹级别还存在其他几个实体：
- ==Asset==
	An asset 是存储在 Orchestrator 中供机器人使用的一段数据。有四种类型的资产：
	- **Text** - 仅存储字符串（不需要添加引号）。
	- **Bool** - 支持 true 或 false 值。
	- **Integer** - 仅存储整数。
	- **Credential** - 包含机器人执行特定过程所需的用户名和密码，例如登录详细信息。
	
	资产可以具有全局价值或每个用户的价值。这意味着只有**指定用户**才能访问存储在该资产中的特定值。
- ==Storage bucket==
Storage buckets是用于存储可用于自动化项目的文件的实体。
- ==Queue==
队列是可以容纳**无限数量**项目、存储**不同类型数据**的容器。
将物品送入队列的过程通常与处理队列物品的过程不同，由不同的机器人处理。
- ==Trigger==
触发器能够以结构化的方式执行作业。有两种类型的触发器：
	- **Time triggers 时间触发器**：通过这些，您可以安排流程的重复执行。
	- **Queue triggers 队列触发器**：这些触发器基于添加到队列中的新项目来执行流程。

#### Roles
角色是一组权限，用于控制人类用户和机器人对租户和文件夹实体的访问。

每个权限都由至少一个**操作类型**（查看、编辑、创建和删除）和一个**实体**（无论是租户级别还是文件夹级别）的组合定义。例如，您可以设置权限只查看某个文件夹中的队列，而不能查看其他队列，并且不做任何其他操作。

**以下是可以设置个人权限的实体：**
| Tenant entities |Folder entities  |
|---|---|
| Alerts| Assets |
| Audit | Storage Files |
| Background tasks| Storage Buckets |
| Libraries| Environments |
| License| Execution Media |
| Robots| Folder Packages |
| Machines|  Jobs|
| ML Logs|Logs  |
| Packages|Monitoring  |
| Roles|  Processes|
| Settings| Queues |
| Folders|Triggers  |
| Users| Triggers |
|  Webhooks| Subfolders |
||Action Assignment |
||Action Catalogs |
||Actions |
||Tasks Assignment |
||Test Case Execution Artifacts |
||Test Data Queue Items |
||Test Data Queues |
||Test Set Executions |
||Test Sets |
||Test Set Schedules |
||Transactions |
##### Standard roles
默认情况下，可以在**Tenant 级别**创建某些角色。这些涵盖了使用文件夹的人类用户和机器人的基本需求。
|  Role| Level | Use|
|:--|--|:--|
|Tenant Administrator  | Tenant | 具有此角色的用户可以管理租户中的所有实体，包括文件夹。 |
| Allow to be Folder Administrator | Tenant |  此角色在租户级别具有最低权限，但允许拥有它的用户在文件夹级别获得管理权限。这是通过下面的**Folder Administrator**角色完成的。|
| Folder Administrator | Folder |具有此角色的用户可以管理文件夹中的所有实体。此角色需要与**Allow to be Folder Administrator**角色一起使用。  |
| Allow to be Automation User | Tenant | 此角色在租户级别具有最低权限，并允许用户获得执行存储在文件夹中的进程的权限。这是通过下面的**Automation User**角色完成的。参与用户和机器人都需要这个角色。 |
| Automation User | Folder | 具有此角色的用户可以在文件夹中执行进程。此角色需要与租户级别的**Allow to be Automation User**角色结合使用。参与用户和机器人都需要这个角色。 |
### 小结
![在这里插入图片描述](https://img-blog.csdnimg.cn/58694e9a8dfd4fedae9df2629678ce64.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
## 3.3 Robot Provisioning and License Distribution 机器人供应和许可证分发
让我们回顾一下！

### 3.3.1 使用无人值守机器人成功运行作业：

- 在无人值守机器人面板中，在用户级别启用自动机器人创建。
- The automatic robot creation is enabled at user level, in the Unattended Robot panel.
- 运行无人值守机器人的工作站使用机器模板连接到 Orchestrator。
- The workstation on which the unattended robot runs is connected to Orchestrator using a machine template.
- 用户和机器模板与我们要运行的进程在同一个文件夹中。
- The user and the machine template are in the same folder with the process we want to run.
- 租户上提供无人参与的运行时（许可证）。
- Unattended runtimes (licenses) are available on the tenant.
### 3.3.2 User creation
在 Orchestrator 中，具有有人值守许可证（Robot 或 Studio）的人类用户和无人值守机器人都需要有相应的 Orchestrator 用户。
根据部署类型和组织设置，以不同方式添加和管理用户：
- 可以在本地 Orchestrator 中本地添加用户。
- 用户必须先添加到自动化云中，然后再添加到云 Orchestrator 中以授予他们许可证。
- 如果预先配置了集成，则可以从 Active Directory 为本地和云 Orchestrator 添加用户。
### 3.3.3 Automatic robot creation
为了简化有人值守和无人值守机器人的创建以及许可证配置，可以在用户级别、有人值守和无人值守机器人以及有人值守机器人的组级别启用自动化机器人创建。

### 3.3.4 Machine templates
机器人在物理或虚拟工作站上运行。这些在 Orchestrator 中由称为机器（machines）的实体进行镜像。 Orchestrator 中的机器用作 API 密钥生成器，授权机器人和 Orchestrator 之间的连接。

**Orchestrator 中有两种类型的机器：**
	- **Machine templates**：这允许使用单个 API 密钥连接到多个工作站。
	- **Standard machines**：这允许 Orchestrator 和单个机器之间的连接。这适用于机器人需要在特定机器上运行的场景。

### 3.3.5 License distribution
在 Orchestrator 中，许可证也称为**runtimes**。它们在机器模板级别分配，位于租户菜单中的机器下。

在那里分配的运行时数应与可以在使用该机器模板连接的单台机器上运行的最大用户数相匹配。在普通的 Windows 机器上，只有一个用户可以运行。但是在 Windows 服务器机器上，多个用户可以同时运行。

无论机器上运行的用户数量有多少，只要机器连接到 Orchestrator，就会消耗许可证。
# 4 与Orchestrator工作
## 4.1 Unattended Automation with Folders
在功能上**，有人值守自动化的目的**是让机器人准备好在人类用户需要时、在他们的工作周期和工作时间内接管不需要的任务。

当谈到**无人值守自动化时，目的**就大不相同：机器人需要尽可能地忙碌，尽可能少地人工输入。在下面的视频中，我们将首先再次看到无人值守机器人的配置是多么容易。然后我们将创建和运行作业，充分利用许可证消耗模型，基于 UI 交互的进程分离和作业优先级。
![在这里插入图片描述](https://img-blog.csdnimg.cn/76ed8fda240847a48ed770569c37b75c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

**Video transcript**
您好，欢迎观看有关 Orchestrator 文件夹无人值守自动化的演示。

在今天的视频中，我们将首先了解**如何在 Orchestrator 文件夹中设置无人值守机器人**。然后我们将使用我们正在设置的无人值守机器人运行**后台和前台作业**。在做这一切的同时，我们还将介绍**工作优先级**的概念。

在我们开始之前先介绍一下后台和前台进程。

**后台进程**，也称为 Headless Process，是指在不与任何类型的 UI 交互的情况下运行的作业。在 UiPath Studio 中构建时，需要设置一个进程在后台启动。
多个后台进程可以同时进行。
**前台进程**使用图形用户界面。例如，基于这种区别，前台进程可以与有人值守自动化中的一个或多个后台进程并行运行。我们现在将看到它在涉及 Orchestrator 文件夹的无人值守自动化场景中是如何工作的。
多个前台进程会依次进行。由于作业需要 UI 交互，因此作业将以顺序模式运行。第一个结束后，第二个开始。
一旦 UI 相关作业结束并且运行时被释放，无头进程的最后一个作业就会开始。发生这种情况是因为它具有比 UI 依赖进程的剩余优先级更高的优先级。

**无人值守的机器人并不作为独立的实体存在。它们是 Orchestrator 中的用户和机器之间的组合**，通过机器模板连接到 Orchestrator。

**让我们简要回顾一下我们所做的**：我们首先设置了一个机器模板和一个 Active Directory 用户，我们将它们添加到一个文件夹并运行了 10 个作业——5 个使用无头进程，另外 5 个使用前台进程。我们还为无头工作设置了高优先级。

### Let's recap
是什么让unattended automation with folders真正有效？

- **The use of folders and job priorities（作业优先级）**
通过在文件夹、角色和权限的帮助下准确反映业务层次结构，我们可以控制对自动化流程的访问，并确保将精力花在带来最大回报的地方。作业优先级可以确保业务优先级在自动化过程中得到很好的体现。

- **基于 UI 交互的进程分离**
Orchestrator 中的进程现在区分为与用户界面交互的进程（称为前台进程）和不与用户界面交互的进程，称为background or headless processes。
这对自动化作业的执行方式有重大影响。无人值守的机器人可以同时运行前台作业和与机器上可用运行时一样多的无头作业。

- **每台机器的许可证分配**
为每台机器分配许可证（运行时）可确保优化它们的使用。例如，在 Windows Server 机器上，多个机器人可以打开会话并运行无人参与的作业，最多运行时数达到最大值。
### 自定义作业分配策略
Orchestrator 中设计了无人值守自动化，以确保资源优化和有效性。但在某些情况下，业务逻辑更为重要。 Orchestrator 提供了一些功能和选项来允许**自定义作业分配过程**，以便某些作业或资源仅对某些用户可用：
- **Assets per user 每个用户的资产** 
可以创建和设置资产，以便只有给定的用户才能访问它们。

- **每个用户或机器的作业分配**
当一个无人值守的工作被创建时，它可以被动态分配，任何空闲的机器人都可以捡起它。或者它可以配置为仅由特定用户拾取或在特定机器上执行。

- **每个用户的触发器分配**
触发器可以设置为动态分配作业，或仅将作业分配给特定用户。

## 4.2 Studio 中的 Orchestrator 资源
Orchestrator 和 Studio 之间的深度集成，通过交互式登录功能，允许 RPA 开发人员直接使用文件夹实体，如队列、资产和流程。观看下面的演示，了解如何使用 Studio 中的专用面板来加快开发速度。

好的，我们到了本演示的结尾，在演示中，我们看到了如何通过简单的拖放操作在自动化工作流中使用 Orchestrator 资源（例如资产和队列），这要归功于 Studio 和 Orchestrator 之间的深度集成。
## 4.3 Orchestrator 中的库和模板
在自动化和机器人管理的许多其他功能中，Orchestrator 还可用于存储库和模板以增加可重用性。这样，公司中的所有开发人员都可以使用 Orchestrator 作为**共享开发资产**并**确保使用正确版本**的一种方式。
演示：使用 Orchestrator 发布和安装库

## 4.4 Storage Buckets
### 4.4.1 什么是Storage Buckets

存储桶是用于存储可用于自动化项目的文件的 Orchestrator 实体。 UiPath Studio 提供了一组活动来简化存储桶的使用。这些活动位于 Orchestrator 下的 UiPath.System.Activities 包中。

可以使用 Orchestrator 数据库或某些外部提供商（例如 Azure、Amazon 或 MinIO）创建存储桶。每个存储桶都是一个文件夹范围的实体，允许对存储和内容访问进行细粒度控制。

### 4.4.2 为什么需要Storage Buckets

UiPath Studio 提供了许多选项来处理自动化项目中的文件。在某些情况下，存储桶可能是最好的方式：例如，当使用存储在集中位置的大文件时，或者当您需要以受控方式授予多个机器人访问权限时。

## 4.5 queues 队列
### 4.5.1 介绍queues 
**什么是Queues？**
**Queues是可以容纳无限数量项目的容器。**项目可以存储多种类型的数据，默认情况下以**自由**形式存储。如果需要特定的数据模式，可以在创建队列时以 JSON 文件的形式上传。

Orchestrator 中的队列将存储项目并将它们单独分配给机器人进行处理，并根据流程结果监控项目的状态。一旦队列项目进入处理，它们就成为事务。**项目是不可分割的工作单元**：客户合同、发票、投诉等。

**为什么需要Queues？**
**在复杂逻辑强调的大规模自动化场景中，使用队列非常有用。**此类场景带来了许多挑战——将来自多个来源的项目组合在一起，根据独特的逻辑处理它们，有效利用资源，或在单个项目和队列级别报告功能，包括使用 SLA。
考虑零售公司通过表格进行的客户登记流程：客户可能来自不同的来源（在线、合作伙伴、自己的商店、呼叫中心），因此将他们添加到处理线的过程顺利至关重要。此外，使用队列将确保在 SLA 时间限制内处理这些队列。

**演示：配置、填充和使用队列**

在下一个视频中，我们将首先在 Orchestrator 中创建一个队列。然后我们将转到 Studio，在那里我们将创建一个调度程序来填充队列，并创建一个表演者从队列中获取数据并将其输入到网站上。
队列对于大型自动化项目极其重要。它们允许存储和处理基本上无限量的数据，前提是数据可以在事务中进行组织。队列通过容纳不同的数据类型提供了很大的灵活性。它们非常适合从不同渠道获取数据、标准化并用作其他应用程序（如 ERP 或 CRM）的输入的情况。
### 4.5.2 回顾和扩展：使用队列
**创建队列**

在 Orchestrator 中，可以通过菜单中的同名条目轻松创建队列。它们是文件夹实体，允许设置细粒度的权限。

创建队列时，您可以设置最大重试次数（您希望队列项目重试的次数）和唯一引用字段（如果您希望事务引用唯一，请选择是）。**一旦创建了队列，就无法修改这些设置。**

队列创建为空，但 UiPath Studio 中有特定活动可以让机器人填充队列。 Orchestrator 也直接支持从 .csv 文件批量上传。

**填充和消耗队列**

为了确保机器人的最佳使用，队列通常与运行自动化的 **Dispatcher-Performer** 模型一起使用。在这个模型中，涉及队列的过程的两个主要阶段是分开的：
- 在 Orchestrator 中获取数据并将其送入队列的阶段，机器人可以从中获取和处理数据。这称为调度程序**Dispatcher**。
- 处理数据的阶段。这被称为**Performer**。
- 
使用位于 Orchestrator 下 UiPath.System.Activities 包中的特定活动来处理队列和队列项目。这些是：

- **Add Queue Item**
在工作流中遇到此活动时，机器人会将项目发送到指定队列，并配置时间范围和其他参数。
- **Add Transaction Item**
机器人在队列中添加一个项目并以“进行中”状态开始交易。在机器人完成此活动并更新状态之前，无法发送队列项进行处理。
- **Get Transaction Item**
从队列中获取一个项目来处理它，将状态设置为“进行中”。
- **Postpone Transaction Item**
添加必须处理事务的时间参数。
- **Set Transaction Progress**
允许为正在进行的事务创建自定义进度状态。这对于处理持续时间较长的事务很有用，分解工作负载将提供有价值的信息。
- **Set Transaction Status**
将事务项的状态更改为失败（有应用程序或业务异常）或成功。一般情况下，会重试因应用异常而失败的事务，不会重试因业务异常而失败的事务。

**队列项目状态**

队列项可以具有以下状态之一。这些将根据人类用户和机器人操作和/或使用设置交易状态活动自动设置。可以使用 Set Transaction Progress 活动为“进行中”的队列项目设置自定义子状态。
- **New**
	- 该项目刚刚通过 Add Queue Item 添加到队列中，或者
	- 该项目被推迟，或
	- 添加了截止日期，或
	- 该项目是在启用自动重试的前一个队列项目尝试失败后添加的。
- **In Progress**
该项目是使用获取事务项目或添加事务项目活动处理的。
当项目具有此状态时，还会在“进度”列中显示自定义进度状态。
- **Failed**
该项目不满足项目中的业务或应用程序要求。
因此，它被发送到设置事务状态活动(**Set Transaction Status** )，该活动将其状态更改为失败.
- **Successful**
项目已处理并发送到设置事务状态活动，该活动将其状态更改为成功。
- **Abandoned**
项目长时间（大约 24 小时）保持在“进行中”状态而未进行处理。
- **Retried**
该项目因应用程序异常而失败并已重试（在重试过程结束时，状态将更新为最终状态 - 成功或失败。
- **Deleted**
该项目已从交易页面手动删除。

除了以上这些，已经被放弃或失败的队列项目可以进入修订阶段。在这种情况下，审阅者会设置特定的修订状态。查看下图，其中说明了两种类型的状态。

![在这里插入图片描述](https://img-blog.csdnimg.cn/b743fa4f6b8f47119bfd1ee2c2d9c036.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)
## 4.6 中场休息 - 事务处理模型 Transaction Processing Models
在队列课程中，我们已经看到了最复杂的事务处理模型。但不是唯一的。如果这不是您的第一门涵盖 UiPath Studio 功能的课程，那么您已经看过其他两个模型。

如果这是您的第一门涵盖 UiPath Studio 的课程，请不要担心！您将轻松掌握其他两种事务处理模型。

但首先，让我们确保我们知道什么是Transaction。
### 4.6.1 什么是Transaction？
通过完成业务流程的一部分，**Transaction表示最小（原子）数据量和处理数据所需的必要步骤。**一个典型的例子是从邮箱中读取一封电子邮件并从中提取数据的过程。

我们将数据称为原子数据，因为一旦它被处理，我们就假设随着业务流程的推进，我们不再需要它。

----
**在考虑业务流程的步骤及其重复方式时，我们可以将业务流程分为三类：**

1. **线性 Linear**
该过程的步骤仅执行一次，如果需要处理不同的数据，则需要再次执行自动化。例如，如果我们回到本章介绍中的电子邮件示例，并且新电子邮件到达，则需要再次执行自动化以对其进行处理。
**线性过程通常简单且易于实现，但不太适合需要使用不同数据重复步骤的情况。**

![在这里插入图片描述](https://img-blog.csdnimg.cn/45215003df584e239932b8cfc9be7b67.png)

---
2. **迭代 Iterative**
**该过程的步骤执行多次，但每次使用不同的数据项。**例如，自动化可以检索多封电子邮件并重复执行相同的步骤，而不是在每次执行时阅读一封电子邮件。

这种过程可以用一个简单的循环来实现，但它的缺点是，如果在处理一个项目时出现问题，整个过程就会中断，其他项目仍然没有处理。

![在这里插入图片描述](https://img-blog.csdnimg.cn/5f5bfdb18b0c4ec8a1a068392266a0f7.png)

---
3.**事务性 Transactional**

与迭代过程类似，事务过程的步骤在不同的数据项上重复多次。然而，自动化的设计使得每个可重复的部分都是独立处理的。

这些可重复的部分被称为事务。**事务彼此独立，因为它们不共享任何数据或有任何要处理的特定顺序。**

![在这里插入图片描述](https://img-blog.csdnimg.cn/0b0500097a924dcd92699f6b56f1564e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
这三类流程可以看作是自动化项目的成熟阶段，从简单的线性任务开始，然后重复多次，最后演变为事务方法。

但是，这并不是对所有情况的绝对规则，应根据过程的特点（例如，正在处理的数据和重复频率）和其他相关要求（例如，易用性和稳健性）来选择类别。

---

**我将在哪些业务场景中使用事务处理？**
- 您需要从文件夹中的多张发票中读取数据，并将该数据输入到另一个系统中。每张发票都可以看作是一笔交易，因为每张发票都有一个重复的过程（即提取数据并将其输入到其他地方）。
- 电子表格中有一个人员及其电子邮件地址的列表，需要向每个人发送一封电子邮件以及一条个性化的消息。此过程中的步骤（即从电子表格中获取数据、创建个性化消息和发送电子邮件）对每个人都是相同的，因此电子表格中的每一行都可以视为一次transaction。
- 在寻找新公寓时，可以使用机器人根据某些标准进行搜索。对于每个搜索结果，机器人都会提取有关房产的信息并将数据插入电子表格中。在这种情况下，每个属性的详细信息页面构成一个transaction。
## 4.7 触发器和 SLAs
### 4.7.1 队列触发器和时间触发器
**什么是触发器？**
触发器能够以结构化的方式执行作业。有两种类型的触发器：
- 时间触发器：通过这些，您可以安排流程的重复执行。
- 队列触发器：这些触发器基于添加到队列中的新项目来执行流程。
触发器是文件夹实体，因此可以定义细粒度的访问权限。

**为什么需要触发器？**
**时间触发器**是自动执行需要特定节奏的流程的好方法。例如，运行一个处理员工提交的费用的流程。

**队列触发器**可能是处理以变化且无法预测的速度填充新项目的队列的最佳选择。它们还可以证明对于具有严格 SLA 和违反它们的重大后果的流程很有价值。示例可能包括涉及客户的所有业务流程：入职、购买、投诉。

### 4.7.2 Service Level Agreements  服务水平协议 (SLAs)
**Orchestrator 中的 SLA 是什么？**
Orchestrator 中的 SLA 只是 SLA 通用概念的应用。换句话说，**它是提供者和客户之间的承诺，具有关于所提供服务的可衡量指标。**
在 Orchestrator 中，这采用必须处理队列项目的时间间隔（以天和/或小时表示）的形式。风险 SLA 是 Orchestrator 中的后续概念，旨在确定需要采取纠正措施以避免违反 SLA 的点。

**为什么在 Orchestrator 中需要 SLA？**
自动化流程是基于有关队列项目量的某些假设运行的。这决定了分配给特定进程和队列的机器人容量。
在某些情况下，现实与这些假设不同。在没有 SLA 的情况下，违规行为可能会被发现为时已晚，并且会带来代价高昂的后果。

### 4.7.3 演示：设置队列触发器和 SLA

在下一个视频中，我们将使用我们在上一课中创建的队列，我们​​正在创建一个队列触发器并为其启用 SLA。
右侧的字段非常重要。第一个是关于触发第一个作业所需的项目数量。当您不希望在队列中有特定数量的项目之前启动进程时，这很有用。


允许的挂起和运行作业的最大数量将决定触发器的速度，它必须与分配的运行时间和机器人数量相匹配。假设我们有 2 个机器人和 2 台具有无人值守许可证的机器，让我们将此示例设置为 2。


第三个字段用于指定添加到队列中以启动新作业的新项目的数量。当以非计划方式填充队列时，这非常有用。让我们将此设置为两个。请记住，此数字是在之前设置的待处理和正在运行的作业的最大数量之上计算的。
示例其工作原理如下：每 30 分钟自动检查一次未处理的项目。如果数字满足我们在触发器创建时设置的条件，则该过程将开始。
## 4.8 Monitoring and Alerts 监控和警报
Orchestrator 提供了用于监控作业执行、机器人和机器以及队列和 SLA 的扩展功能。最重要的是，机器人可以在开发时使用 Studio 中的特定活动在运行时发出警报。

在下面的演示中查看监控功能。
Alerts是确保机器人按照参数工作的强大工具。根据角色，用户可以启用或禁用给定组件的警报。只需导航到我的个人资料并使用专用切换。


# 5 实践
## 5.1 练习 1 - 将无人值守机器人连接到 Orchestrator
您可能已经适应了您参加的环境。 Studio 已安装并获得许可，您有一个有人值守的机器人，通过交互式登录连接到 Orchestrator，并通过 UiPath 助手进行控制。

是时候通过配置无人值守的机器人并连接到同一个 Orchestrator 来进一步完善您的环境了。您需要一台单独的机器来部署它，并需要一个具有无人值守许可证的 Orchestrator（可以是社区自动化云）。

**练习 1 - 解决方案**

- 在**自动化云**和 **Orchestrator** 中：

1. 在自动化云中的自动化用户组中添加用户。
2. 打开 Orchestrator 并转到租户级别的用户。
3. 在 Orchestrator 中添加用户并授予他们“**允许成为自动化用户**”角色。
4. 从无人值守机器人选项卡中切换“自动为此用户创建无人值守机器人”。添加域（如果您使用的是 Windows 机器，则为机器名称）和 Windows 登录用户名（以及 Windows 密码，如果有的话）。
5. 在租户级别的机器下创建机器模板，并至少分配一个无人值守的执行槽。
6. 创建一个文件夹。如果可能，请向其发布流程。
7. 将用户和机器模板都分配给文件夹。

- 在将部署无人值守机器人的机器上：

1. 确保已安装 UiPath 代理。如果您有权访问企业安装程序，请使用它。否则，社区安装程序应该可以工作，但您还将拥有 UiPath 助手（这不是问题）。
2. 如果未打开，请从安装 UiPath 的文件夹中打开 UiPath Agent。
3. 右键单击 UiPath 代理并打开 Orchestrator 设置。
4. 输入与机器模板对应的机器密钥和 Orchestrator URL（从打开自动化云的浏览器到租户名称）。
单击连接。
如果安装了 UiPath 助手，可以实现上述 2-4 步。

## 5.2 练习 2 - Orchestrator 资源
是时候进一步推进我们之前开发的项目了。作为一般原则，我们应该致力于将静态值排除在我们的项目之外。原因很简单，更新存储在工作流之外的值比要求开发人员更新项目更容易。

请求很简单：更新下面的项目（我们在 Studio 课程中使用 Orchestrator 资源开发的项目）以从 Orchestrator 检索 ACME URL。

**练习 2 - 解决方案**
1. 在 Orchestrator 中，转到在 Studio 课程中为使用 Orchestrator 资源创建凭据和队列的同一文件夹，然后打开资产药丸。
如果您没有按照该课程中的演示进行操作，也没关系。创建资产，选择类型 Credential 并存储 ACME 的用户名和密码。然后通过导航到同一文件夹中的队列药丸来创建一个简单的队列。确保此处的名称和 Studio 项目中的名称与凭证和队列均匹配。
2. 创建一个文本类型的新资产并粘贴 ACME 地址：https://acme-test.uipath.com/login。
3. 在 Studio 中打开工作流程。打开资源面板并刷新。如果您看到刚刚创建的资产，只需将其拖到 Open Browser 活动之前即可。选择获取资产活动。在获取资产活动的输出字段中创建一个新变量。确保其范围是全球性的。
如果在“资源”面板中没有看到您的资产，则表示您未登录 Orchestrator。登录，然后继续该步骤。
4. 将 Open Browser 活动中的字符串替换为新创建的变量的名称。就是这样 - 运行并享受！

**序列图**
![在这里插入图片描述](https://img-blog.csdnimg.cn/e2dfa4eb2bc04630af6fe3ccdf91479d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

## 5.3 练习 3 - 队列
您的任务是自动化在柜员应用程序“UiDemo”中插入交易的过程。与交易相关的输入数据存储在 Excel 文件中。由于交易量非常大，需要多台机器人同时工作。根据解决方案架构师 (SA) 和业务分析师 (BA) 的说法，该流程需要分配给多达 5 个机器人。

广管局已确定一项经常性业务例外：
- 无效的输入数据 - 有些值不是数字。

**你的任务：**
- 下载 UiDemo 和下面的输入 Excel 文件。
- 构建一个 Dispatcher (Producer) 进程，将输入文件中的每一行作为队列项添加到 Orchestrator 队列中。
- 构建一个Performer（消费者）进程，获取每个队列项并在UiDemo 中输入数据。
- 包括一个异常处理机制来捕获非整数值。
- 确保在 Orchestrator 中为事务设置了正确的状态。
- 包括安全终止进程的机制。

**UiDemo 登录凭据：**

Username: admin
Password: password
**解决方案**

1. 在 Orchestrator 中创建队列

在 Orchestrator 文件夹中的队列部分下，点击添加按钮。
单击名称字段并输入名称，例如“队列 1”。
确保选中“自动重试”选项，并在“最大重试次数”部分中键入 2。

2. 创建调度器

创建一个新序列并为其命名 - 即 AddItems。
使用读取范围将 Excel 文件作为数据表读取。
添加 For Each Row 活动。
拖放 Add Queue Item 活动并将其放置在 For Each Row 活动中。
在“属性”面板中选择 QueueName 字段，然后键入在前面步骤中创建的队列的名称。确保将文本放在引号之间。
ItemInformation 字段是可以添加交易项目值的地方。此过程的工作方式类似于将参数传递给调用的工作流。按下按钮。显示一个 ItemInformation 窗口，使您能够创建一个参数。
单击创建参数。
将第一个参数命名为“CashIn”。
将 ArgumentType 设置为 String 并将方向设置为 In。
通过在数据表的第一列上输入信息来填写值字段 - row("CashIn").ToString。
对第二个字段和第三个字段执行相同的步骤 (7-10)（命名它们：OnUsCheck 和 NotOnUsCheck）。
运行工作流。
检查 Orchestrator 中的值
找到您之前创建的队列。
按更多操作按钮并选择查看交易。显示之前创建的交易项目。
按查看详细信息按钮查看您在 Studio 中输入的值。

3. 创建表演者

- 在 Studio 中创建一个新序列。将其命名为“ProcessTransactions”。
- 将 Get Transaction Item 活动拖放到 Designer 面板。
- 双击 Get Transaction Item 活动以查看相应的属性面板。
- 通过输入先前创建的队列来填写 QueueName 字段。
- 单击 TransactionItem 字段并按 Ctrl + K 创建一个类型为 Transaction Item 的新变量。
- 键入名称，例如“TransactionItem”，然后按 Enter。
- 运行项目。返回 Orchestrator 并注意发生了什么。第一个交易项目的状态从“新建”更改为“进行中”。发生这种情况是因为 Orchestrator 尚未收到有关该项目状态的指示。
- 返回到您在 Studio 中打开的项目。添加 If 活动并使用以下表达式作为条件：TransactionItem IsNot Nothing。在 Else 块中放置一个 Terminate Workflow 活动。这将确保工作流在没有项目剩余时结束。
在 If 活动的 Then 块中添加 Try Catch 活动。在尝试部分中，添加 3 个分配活动。
创建 3 个变量，对应于将在 UIDemo 应用程序中填写的字段（CashIn、OnUsCheck、NotOnUsCheck）。将每个变量放在 3 个分配活动中的每一个的左侧。
在 Assign 活动的右侧，添加从事务项中提取相应数据并将其转换为 Integer 的表达式。例如，对于 CashIn 字段，它将如下所示：cint(TransactionItem.SpecificContent(“CashIn”))。
现在使用这些值将它们输入到 UiDemo.exe 中。打开应用程序并登录。 （证书在练习开始时提供）。保持应用程序打开以进行练习。
对 Try 部分中的每个变量使用 Type into 活动。在这三个 Type Into 之后，对 UiDemo 中的 Accept 按钮使用 Click 活动。
为确保我们将此队列项通知 Orchestrator，请将设置事务状态活动拖到设计器面板。
双击 Set Transaction Status 以查看其对应的 Properties 面板。
点击 TransactionItem 字段以输入在前面的步骤中创建的 TransactionItem 变量。
确保状态字段设置为“成功”。
在捕获部分中，将无效的强制转换异常添加为“System.InvalidCastException”。然后添加设置交易状态，填写交易项目变量并将状态设置为“失败”并带有说明性消息 - 例如“从 String 到类型 'Integer' 的转换无效。”

4. 终止和停止进程

Orchestrator 中的每个正在运行的进程都有一个与之关联的运行状态。用户可以选择停止或终止进程。 Kill 将立即停止进程，这可能会导致不必要的错误。

Stop 将通过关闭应用程序和注销以安全的方式执行此操作。但这需要在我们的工作流程中使用“应该停止”活动。它通知在控制流到达应停止活动时是否已按下 Orchestrator 中的停止按钮。这类似于电脑游戏中的保存游戏功能。让我们这样做。

转到 Performer 的 Project 面板并打开 Main 工作流程。将流程图活动拖放到此处。
创建一个名为“counter”的 Int32 类型的新变量，默认值设置为“1”。
添加带有消息“Processing Transaction number”+counter.ToString 的日志消息
从“项目”面板将 ProcessTransactions.xaml 工作流拖放到流程图内，并将其与流程图的起点连接起来。
使用 Assign 活动在每次进程运行时将计数器的值增加 1。将此活动与上一项活动联系起来。
拖放“应该停止”活动并将其与之前使用的“分配”活动连接起来。在“属性”面板和“结果”中，按 Ctrl+K 创建一个新变量以存储此活动的输出。称之为“应该停止”。检查变量面板，您会看到“shouldStop”是使用布尔类型创建的。
此外，添加一个 Flow Decision 活动并连接它。在“条件”属性的“属性”面板中，设置变量“shouldStop”，因为我们需要检查进程是否应该停止。
对 True 案例使用日志消息活动。在其中写入一条代表性消息，例如“进程已停止。 “
对于 False 情况，将 Flow Decision 与顶部的第一个 Log 消息活动连接起来。您的工作流程应如下所示：
![在这里插入图片描述](https://img-blog.csdnimg.cn/3842279fd3574fdfb3219c45b0d0b25e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)
5. 出版表演者

从 Studio 的顶部菜单中按发布。将出现一个弹出窗口，您应该会看到有关您的包裹的信息。单击发布。
转到 Orchestrator -> 租户 -> 包。在此处搜索您的项目，您应该会看到它。
转到至少连接了一个无人值守机器人的文件夹中的进程并创建一个新进程。在包名称中选择您刚刚发布的包。
导航到作业并为您的流程创建一个新作业。选择进程，然后选择机器上的机器人，然后单击开始。

**序列图**
![在这里插入图片描述](https://img-blog.csdnimg.cn/e277e6fc76544aa48c2f548286a9def1.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAcXFfMzgzMTYxNDg=,size_20,color_FFFFFF,t_70,g_se,x_16)

## 5.4 练习 4 - 触发器
为之前创建的流程添加 2 个计划以：

- 在添加进程的文件夹中的所有机器人上每小时运行一次。
- 每周一下午 05:30（UTC-06 时区）在给定机器人上运行 3 次。

**解决方案**
1. 每小时：
	- 转到文件夹并添加新的时间触发器。
	- 检查“每小时”选项，每 1 小时在 0 分钟。
	- 在“执行目标”选项卡下保留“任何用户”和“任何机器”，然后点击“创建”。
2. 每周一3次：
	- 添加新的时间触发器。
	- 选中“每周”选项，选择“星期一”并插入开始时间。
	- 从“执行目标”选项卡中的可用用户中选择特定用户。
