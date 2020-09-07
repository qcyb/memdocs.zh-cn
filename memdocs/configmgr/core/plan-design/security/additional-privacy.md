---
title: 其他隐私信息
titleSuffix: Configuration Manager
description: 了解 Microsoft 如何收集和使用来自 Configuration Manager 的数据。
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b419f313b9d4d300d286cf32605ebfe7e0e1573c
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068049"
---
# <a name="additional-information-about-privacy-for-configuration-manager"></a>关于 Configuration Manager 隐私的其他信息

适用范围：  Configuration Manager (Current Branch)


## <a name="updates-and-servicing"></a>更新和服务

Configuration Manager 使用更新模型，有助于环境保持最新更新和最新功能。 此功能使用称作“服务连接点”的站点系统角色。 选择在其中安装此角色的服务器。 

有关收集的信息及其使用方式的详细信息，请参阅[使用情况数据](#usage-data)。



## <a name="usage-data"></a>使用情况数据

Configuration Manager 收集有关自身的诊断和使用情况数据，Microsoft 使用这些数据改进将来版本的安装体验、质量和安全性。
诊断和使用情况数据可用于每个 Configuration Manager 层次结构。 它包含在每个主站点和管理中心站点每周运行一次的 SQL Server 查询。 层次结构使用管理中心站点时，主站点中的数据随后会复制到该站点。 在层次机构的顶层站点上，服务连接点在检查更新时提交此信息。 如果服务连接点处于脱机模式下，则将使用服务连接工具传输信息。

Configuration Manager 仅从站点 SQL Server 数据库收集数据，而不会直接从客户端或站点服务器收集数据。

管理员可以通过转到 Configuration Manager 控制台的“使用情况数据”  部分更改收集数据的级别。

有关使用情况数据级别和设置的详细信息，请参阅[诊断和使用情况数据](../diagnostics/diagnostics-and-usage-data.md)。



## <a name="log-analytics-connector"></a>Log Analytics 连接器

Log Analytics 连接器同步数据，例如从 Configuration Manager 到 Azure 云服务的集合。 管理员配置此功能后，Azure 订阅 ID 和密钥会存储在 Configuration Manager 数据库中。 Azure Active Directory 客户端密钥和 Azure 工作区共享的密钥均存储在本地 Configuration Manager 数据库中。 Configuration Manager 和 Azure 之间的所有通信均使用 HTTPS。 除随机化诊断和使用情况数据之外，不会向 Microsoft 提供有关集合的任何其他信息。 

有关 Log Analytics 收集的信息的详细信息，请参阅 [Log analytics 数据安全](/azure/log-analytics/log-analytics-data-security)。



## <a name="asset-intelligence"></a>资产智能

资产智能使管理员能够定义、跟踪和主动管理与配置标准的符合性。 对部署以及物理和虚拟应用程序的使用进行计量和报告可帮助组织做出更明智的软件许可业务决策，并保持与许可协议的相容性。 从 Configuration Manager 客户端收集使用数据之后，你可以使用不同的功能来查看数据，包括集合、查询和报告。

在每次同步过程中，将从 Microsoft 下载已知软件的目录。 可以选择向 Microsoft 发送以下相关信息：在组织中发现的要进行研究以及添加到目录中的未分类软件标题。 在上传此信息之前，对话框会显示要上传的数据。 无法取消上传的数据。 资产智能不会向 Microsoft 发送关于用户和计算机或许可证使用的信息。

上载软件标题后，Microsoft 研究员会对此资料进行标识和分类，然后向使用此功能的所有其他客户以及目录的其他消费者提供该资料。 任何已上传的软件标题都将公开。 应用程序及其分类会成为目录的一部分，然后可供目录的其他用户下载。 在配置资产智能数据收集以及确定是否将信息提交给 Microsoft 之前，请考虑组织的隐私要求。

默认情况下，Configuration Manager 中不启用资产智能。 上传未分类的标题决不会自动发生，系统并不打算自动进行此任务。 你必须手动选择并批准上载每个软件标题。



## <a name="endpoint-protection"></a>Endpoint Protection

Microsoft Cloud Protection Service，以前称作 Microsoft Active Protection Service 或 MAPS。

适用的产品：Configuration Manager 的 System Center Endpoint Protection 和 Endpoint Protection 功能（用于管理 System Center Endpoint Protection 和 Windows Defender for Windows 10）。 用于 Linux 的 System Center Endpoint Protection 和用于 Mac 的 System Center Endpoint Protection 还未实现此功能。

Microsoft Cloud Protection Service 反恶意软件社区是一个包括 System Center Endpoint Protection 用户的自愿性全球在线社区。 加入 Microsoft Cloud Protection Service 时，System Center Endpoint Protection 会自动向 Microsoft 发送信息。 Microsoft 使用信息来确定调查潜在威胁的软件，并帮助提高 System Center Endpoint Protection 的效率。 此社区帮助阻止新的恶意软件感染的传播。 如果 Microsoft Cloud Protection Service 报告中包括有关恶意软件或 Endpoint Protection 客户端可删除的有害软件的详细信息，Microsoft Cloud Protection Service 将下载最新的签名来解决此问题。 Microsoft 云保护服务还能够发现“误报”，并解决这些误报问题。 （误报，即最初被确定为恶意软件，但结果并非如此。） 

Microsoft Cloud Protection Service 报告中包含有关可疑恶意软件的信息，例如文件名、加密哈希、供应商、大小和日期戳。 此外，Microsoft Cloud Protection Service 可能会收集完整的 URL 以指明文件的来源。 这些 URL 有时可能包含个人信息，例如窗体中输入的搜索词或数据。 报告中可能还包括 Endpoint Protection 通知存在有害软件时你采取的操作。 Microsoft Cloud Protection Service 报告中包含此信息有助于 Microsoft 评估 Endpoint Protection 检测并删除恶意软件和有害软件的有效性，以及识别新的恶意软件。

如果有基本或高级的成员资格，则可以加入 Microsoft Cloud Protection Service。 基本成员报告中包含上述信息。 高级成员报告更加全面，可能包括有关 Endpoint Protection 检测到的软件的其他详细信息，例如此类软件的位置、文件名、软件操作方式以及软件影响计算机的方式。 这些报告以及来自其他加入 Microsoft Cloud Protection Service 的 Endpoint Protection 用户的报告有助于 Microsoft 研究人员更快地发现新威胁。 之后，将为符合分析条件的程序创建恶意软件定义，而更新后的定义将通过 Microsoft 更新提供给所有用户。

为了帮助检测和修复某些种类的恶意软件感染，产品会定期向 Microsoft Cloud Protection Service 发送有关用户的电脑安全状态的信息。 此信息包括有关用户的电脑的安全设置信息以及日志文件，描述在电脑启动时所加载的驱动程序和其他软件。

还会发送一个专门识别用户电脑的数字。 Microsoft Cloud Protection Service 可能还会收集潜在恶意软件文件连接到的 IP 地址。

Microsoft Cloud Protection Service 报告可用于改进 Microsoft 软件和服务。 这些报告还可用于进行统计或其他测试或分析目的，以及用于生成定义。 只有根据业务需要必须使用报告的 Microsoft 员工、承包商、合作伙伴和供应商才有权访问这些报告。

Microsoft Cloud Protection Service 不会有意收集个人信息。 就算 Microsoft Cloud Protection Service 收集到任何个人信息，Microsoft 也不会使用该信息来识别用户的身份或与用户联系。

有关详细信息，请参阅 [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)。



## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>站点层次结构 - 包含 Bing 地图的地理视图

> [!IMPORTANT]
> 自 2020 年 8 月起，已弃用此功能。 请使用“层次结构图表”选项。<!--8116777-->

在 Configuration Manager 控制台中，转到“监视”**** 工作区，选择“站点层次结构”**** 节点，然后切换到“地理视图”****。 此视图允许用户使用 Microsoft 必应地图提供的地图查看 Configuration Manager 物理服务器拓扑。 为了启用此功能，会将你提供的位置信息从服务器发送到 Bing 地图 Web 服务。

Microsoft 使用该信息来运行和改进 Microsoft Bing 地图以及其他 Microsoft 站点和服务。 有关详细信息，请参阅 [Microsoft 隐私声明](https://privacy.microsoft.com/privacystatement)。

你可以选择不为站点层次结构使用地理视图。 此默认“层次结构图表”视图允许你查看层次结构，且不使用必应地图服务。
