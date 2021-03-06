---
title: 1606 的诊断数据
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 版本 1606 收集的诊断和使用情况数据的级别。
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7350d03-f440-4744-82d4-75f8c6c25028
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: a8cc58a11c1cce86bb5964ef4ad55958619a4529
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88994865"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1606-of-configuration-manager"></a>Configuration Manager 版本 1606 收集的诊断使用情况数据收集的级别

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 版本 1606 收集三个级别的诊断和使用情况数据：“基本”、“增强”和“完全”    。 默认情况下，此功能设置为增强级别。 以下部分提供有关每个级别所收集数据的其他详细信息。

针对以前版本进行的更改使用 ***[新增]*** ***[已更新]*** ***[已删除]*** 或 ***[已移动]*** 进行了注明。


> [!IMPORTANT]
>  Configuration Manager 不会收集基本或增强级别的站点代码、站点名称、IP 地址、用户名、计算机名、物理地址或电子邮件地址。 在完全级别收集的信息没有目的性，即可能包括在日志文件或内存快照等高级诊断信息中。 Microsoft 不会使用此信息来识别你的身份、与你联系或进行广告宣传。

##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> 如何更改级别
 如果管理员具有基于角色的管理作用域，其中包括对**站点**对象类的**修改**权限，则其可以通过 Configuration Manager 控制台中的“诊断和使用数据”设置更改已收集数据的级别。

   要执行此操作，请在控制台中，转到“后台”选项卡（左上角带下拉箭头的选项卡），选择“使用情况数据”  ，然后选择要使用的数据级别。  

##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> 级别 1 - 基本
 基本级别包括层次结构相关数据、帮助改进安装或升级体验所需的数据，以及帮助确定哪些 Configuration Manager 更新适合你的层次结构的数据。

 从 Configuration Manager 版本 1606 开始，此级别包括以下内容：


-   安装程序信息：
      - 内部版本、安装类型、语言包、启用的功能  

      -   更新包部署状态和错误、下载进度和先决条件错误 

      -  升级后脚本的版本

      -  更新快速通道的使用

-   数据库性能指标（复制处理信息、按处理器和磁盘使用情况排列靠前的 SQL Server 存储过程）

-   基本数据库配置（处理器、群集配置和分布式视图配置）

-   Configuration Manager 数据库架构（所有对象定义的哈希）

-   Configuration Manager 客户端版本和操作系统版本的计数

-   托管设备操作系统和 Exchange Connector 所设置策略的计数

-   客户端语言和区域设置计数

-   Windows 10 设备（按分支和内部版本）计数

-   基本 Configuration Manager 站点层次结构数据（站点列表、类型、版本、状态、客户端计数和时区）

-   基本站点系统服务器信息（使用的站点系统角色、Internet 和 SSL 状态、操作系统、处理器，以及物理计算机或虚拟机）

-   基本用户发现统计信息（用户发现计数和最小/最大/平均组大小）

-   基本 Endpoint Protection 信息（反恶意软件客户端版本）

-   基本应用程序和部署类型计数（应用总数、包含多个部署类型的应用总数、包含依赖项的应用总数、被取代的应用总数和使用中的部署技术数）

-   基本操作系统部署 (OSD) 计数（图像）

-   分发点和管理点类型以及基本配置信息（受保护、预留、PXE、多播、SSL 状态、请求/对等分发点、启用 MDM、启用 SSL 等。）

-   遥测统计信息（运行时间、运行时和错误）

-  配置的遥测级别、模式（联机或脱机）和快速更新配置

-  网络发现的使用（启用或禁用）
-  管理控制台：

    -  有关控制台连接的统计信息（操作系统版本、语言、SKU 和体系结构、系统内存、逻辑处理器计数、连接站点 ID、已安装的 .NET 版本和控制台语言包）    


- ***[新增]*** SQL 版本、服务包级别、版本、排序规则 ID 和字符集


##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> 级别 2 - 增强
安装完成后，默认级别为增强级别。 此级别包括在基本级别收集的数据、特定于功能的数据（频率和持续使用时间）、Configuration Manager 客户端设置（组件名称、状态和轮询间隔等特定设置）和有关软件更新的基本信息。

此级别为 Microsoft 提供对将来版本的产品和服务进行有用改进所需的最小数据，因此是推荐的级别。 此级别不收集对象名称（站点、用户、计算机或对象）、有关安全相关对象的详细信息或需要软件更新的系统计数等漏洞。

从 Configuration Manager 版本 1606 开始，此级别包括以下内容：

-   **应用程序管理：**  

    -    组织内所使用部署类型的基本使用情况/目标信息（用户与目标设备、所需设备与可用设备，以及通用应用）  

    -   应用程序部署信息（安装/卸载、需要批准、已启用/禁用用户交互、依赖关系和取代）  

    -   可用应用程序请求统计信息  

    -   包（按类型）计数  

    -   应用程序适用性（按操作系统）计数  

    -   包/程序部署计数  

    -   App-V 环境和部署属性计数  

    -   Windows 10 授权应用程序许可证计数  

    -   每个用户/设备在每个时间段的应用程序部署的最大/最小/平均数目

    -   维护时段类型和持续时间  

    -  应用程序策略大小和复杂性统计信息

    - ***[新增]*** 适用于企业的 Windows 应用商店应用计数和同步统计信息（包括汇总的应用类型）  

    - ***[新增]*** 边界组统计信息（快速和慢速的数量，以及每组的计数）

    - ***[新增]*** MSI 配置选项和计数

    - ***[新增]*** 应用要求（部署技术引用的内置条件计数）

    - ***[新增]*** 应用取代、链的最大深度

    - ***[新增]*** 通用数据访问 (UDA) 使用情况及创建方式



-   **客户端：**  

    -   已启用客户端代理的列表/计数  

    -   从每个源位置类型进行的客户端安装计数  

    -   客户端安装失败计数  

    -  ***[新增]*** 客户端自动升级部署配置，包括客户端试验

    -  ***[新增]*** 客户端运行状况统计信息和首要问题摘要

    - ***[新增]*** BIOS 使用年限（年）

    - ***[新增]*** 操作系统使用寿命（月）

    - ***[新增]*** 软件中心操作计数

    - ***[新增]*** 主动管理技术 (AMT) 客户端版本

    - ***[新增]*** 客户端部署下载错误

    - ***[新增]*** 客户端通知操作的操作状态（每个操作的运行次数，目标客户端的最大数，平均成功率）

    - ***[新增]*** 用于客户端的部署方法，每个部署方法的客户端计数

    - ***[新增]*** 客户端缓存大小配置



- ***[新增]*** **云服务：**

  - ***[新增]*** 同步到 Operations Management Suite 的集合计数

  - ***[新增]*** 是否启用 Operations Management Suite 云连接器



- ***[新增] 集合：***

    -  ***[已移动]*** 收集评估统计信息（查询时间、已分配与未分配计数、按类型计数、ID 滚动更新和规则使用情况）

    - ***[新增]*** 无部署的集合

    - ***[新增]*** 集合 ID 使用情况（未用完 ID）



-   **符合性设置：**  

    -   配置项目计数（按类型）  

    -   基本配置基线信息（计数、部署数目和引用数目）  

    -   ***[已更新]*** 引用内置设置的部署的计数（现捕获修正设置）  

    -   ***[已更新]*** 针对自定义设置创建的规则和部署的计数（现捕获修正设置）  
    -   部署的简单证书注册协议 (SCEP)、VPN、Wi-Fi、证书 (.pfx) 和合规性策略模板的计数

    -  SCEP 证书、VPN、Wi-Fi、证书 (.pfx) 和合规性策略部署的计数（按平台）

    - ***[新增]*** Passport for Work 策略（已创建、已部署）



-   **内容：**  

    -   边界（按类型）计数  

    -   边界组信息（分配给每个边界组的边界和站点系统的计数）  

    -   分发点组信息（分配给每个分发点组的包和分发点的计数）  

    -   分发点配置信息（分支缓存的使用和分发点监视）  

    -   分发管理器配置信息（线程、重试延迟、重试次数和请求分发点设置）  


-   **Endpoint Protection：**  

    -   Endpoint Protection 反恶意软件和 Windows 防火墙策略的使用情况（分配给组的唯一策略数）<br /><br /> 这不包括有关策略所含设置的任何信息。  

    -   Endpoint Protection 部署错误（Endpoint Protection 策略部署错误代码计数）  

    -   选择在 Endpoint Protection 仪表板中显示的集合数  

    -   为 Endpoint Protection 功能配置的警报数  

    - ***[新增]*** 高级威胁防护 (ATP) 策略（策略计数和是否已部署策略）


-   ***[已删除]*** **移动应用程序管理 (MAM)：**  

    -   ***[已删除]*** 启用了 MAM 的 Office 应用程序、业务线应用程序和策略计数（按操作系统）  

    -   ***[已删除]*** MAM 应用程序/策略部署的计数  

    -   ***[已删除]*** 创建的规则计数（按 MAM 设置）  


- ***[新增]*** **迁移：**

  -  ***[新增]*** 已迁移的对象（使用迁移对象）的计数



-   **移动设备管理 (MDM)：**  

    -   已发出的移动设备操作计数：锁定、固定剩余部分、擦除和停用命令  

    -   由 Configuration Manager 和 Microsoft Intune 托管的移动设备计数和这些设备的注册方式（批量或基于用户）  

    -   移动设备轮询计划和移动设备签入持续时间的统计信息  

    -   移动设备策略计数  

    -   具有多个注册移动设备的用户计数  

-   **Microsoft Intune 故障排除：**

    -   从 Microsoft Intune 下载的状况、状态、清单、RDR、DDR、UDX、租户状况、POL、LOG、证书、CRP、重新同步、CFD、RDO、BEX、ISM 和符合性消息的计数和大小

    -   复制到 Microsoft Intune 的设备操作（擦除、停用、锁定）、遥测和数据消息的计数和大小

    -   Microsoft Intune 的完全和增量用户同步统计信息


-   **本地移动设备管理 (MDM)：**  

    -   本地 MDM 应用程序部署的部署成功/失败统计信息  

    -   Windows 10 批量注册包和配置文件计数  



-   **操作系统部署：**  

    -   启动映像、驱动程序、驱动程序包、启用多播的分发点、启用 PXE 的分发点以及任务序列的计数  

    -   ***[新增]*** 任务序列步骤使用情况计数



-   **站点更新：**

    - 已安装的 Configuration Manager 修补程序的版本




-   **软件更新：**  

    -   具有软件更新部署的集合总数/平均数和已部署更新的最大数/平均数  

    -   与同步绑定的自动部署规则数  

    -   创建新的更新或将更新添加到现有组的自动部署规则数  

    -   自动部署规则中使用的可用和截止时间增量  

    -   每个更新的平均和最大分配数  

    -   使用 System Center Update Publisher 创建和部署的更新数  

    -   更新组和分配的计数  

    -   更新包计数和包的目标分发点的最大/最小/平均数  

    -   更新组的数目和每个组的更新的最小/最大/平均数目  

    -   更新数和已部署、已过期、被取代、已下载和包含 EULA 的更新所占百分比  

    -   更新扫描错误代码和计算机计数  

    -   客户端更新评估和扫描计划  

    -   软件更新点同步计划  

    -   具有多个部署的自动部署规则数  

    -   用于活动 Windows 10 服务计划的配置  

    -   Windows 10 仪表板内容版本  

    -   使用面向企业的 Windows 更新的 Windows 10 客户端计数  

    -   群集修补统计信息  

    -   部署的 Microsoft 365 更新计数  

    -   软件更新点同步的分类

    -   ***[新增]*** 软件更新点负载平衡统计信息



-   **SQL/性能数据：**  

    -   最大数据库表计数  

    -   SQL 始终可用副本信息  

    -  SQL 更改跟踪保持期

    - ***[新增]*** 启用和计划（完全、增量）的发现类型

    - ***[新增]*** 发现操作统计信息（找到的对象的计数）

    - ***[新增]*** SQL 更改跟踪性能问题、保持期和自动清理状态



- ***[新增]*** **其他**

    - [新增] 使用 LAN 唤醒 (WOL) 的站点计数



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> 级别 3 - 完全
完全级别包括基本和增强级别的所有数据。 它还包括有关 Endpoint Protection、更新符合性百分比和软件更新信息的其他信息。 此级别还可包括系统文件和内存快照（可能包含捕获时存在于内存或日志文件中的个人信息）等高级诊断信息。

从 Configuration Manager 版本 1606 开始，此级别包括以下内容：

-   集合评估与刷新统计信息

-   Endpoint Protection 运行摘要（包括受保护、有风险、未知与不支持客户端的计数）

-   Endpoint Protection 策略设置

-   软件更新部署信息（客户端与 UTC 时间、必需、可选与无提示，以及重启抑制的目标部署所占百分比）

-   软件更新部署的总体符合性

-   自动部署规则评估计划信息

-   ***[已删除]*** 包含网络访问保护策略的客户端数

-   软件更新部署错误代码和计数

-   软件更新部署集合中停用客户端的最小/最大/平均数目

-   包含已过期软件更新的组计数

-   每个包的软件更新的最小/最大/平均数目

-   软件更新扫描成功百分比

-   上次软件更新扫描后的最小/最大/平均小时数

-    软件更新点同步的软件更新产品
-    符合性设置：SCEP、VPN、Wi-Fi 和符合性策略模板配置详细信息

-    Intune 托管设备的 EAS 条件访问策略的类型（阻止或隔离）

-   ***[新增]*** 环境中排名前 50 位的 CPU

-   ***[新增]*** Configuration Manager 使用情况的 DCM 配置包

-   ***[新增]*** MSI 产品代码（客户部署的常见应用）

-   ***[新增]*** ATP 运行状况摘要

-   ***[新增]*** 详细的客户端部署安装错误
