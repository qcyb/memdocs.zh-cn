---
title: 桌面分析故障排除
titleSuffix: Configuration Manager
description: 帮助解决桌面分析问题的技术详细信息。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 96e9f7523ae8946b7756a8a39d1757e652eb3c8c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696895"
---
# <a name="troubleshoot-desktop-analytics"></a>桌面分析故障排除

使用本文中的详细信息来帮助解决与 Configuration Manager 集成的桌面分析问题。

## <a name="confirm-prerequisites"></a>确认先决条件

许多常见问题是由于缺少先决条件引起的。 首先确认以下配置：

- [必备条件](overview.md#prerequisites)  

- [Windows 组件更新](enroll-devices.md#update-devices)  

- [如何启用数据共享](enable-data-sharing.md)，其中包括以下主题：  

  - 客户端需要连接到的 Internet 终结点  

  - 代理服务器身份验证  

  - 诊断数据级别  

## <a name="monitor-connection-health"></a>监视器连接运行状况

使用 Configuration Manager 中的“连接运行状况”  仪表板，按设备运行状况向下钻取类别。 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“桌面分析服务”节点，然后选择“连接运行状况”仪表板    。  

有关详细信息，请参阅[监视连接运行状况](monitor-connection-health.md)。

> [!NOTE]
> Configuration Manager 与桌面分析的连接依赖于服务连接点。 对此站点系统角色所做的任何更改都可能会影响与云服务的同步。 有关详细信息，请参阅[关于服务连接点](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move)。

从版本 2002 开始，如果 Configuration Manager 站点无法连接到云服务所需的终结点，则会引发严重状态消息 ID 11488。 当无法连接到服务时，SMS_SERVICE_CONNECTOR 组件状态将更改为严重。 在 Configuration Manager 控制台的[“组件状态”](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus)节点中查看详细状态。<!-- 5566763 -->

## <a name="log-files"></a>日志文件

有关详细信息，请参阅[桌面分析的日志文件](../core/plan-design/hierarchy/log-files.md#desktop-analytics)

自 Configuration Manager 版本 1906 起，使用 Configuration Manager 安装目录中的“DesktopAnalyticsLogsCollector.ps1”  工具来帮助对桌面分析进行故障排除。 它会运行一些基本故障排除步骤，并将相关日志收集到单个工作目录中。 有关详细信息，请参阅[日志收集器](log-collector.md)。

### <a name="enable-verbose-logging"></a>启用详细日志记录

1. 在服务连接点上，转到以下注册表项：`HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. 将“Logginglevel”  值设置为 `0`  

## <a name="azure-ad-applications"></a><a name="bkmk_AzureADApps"></a> Azure AD 应用程序

桌面分析会将以下应用程序添加到 Azure AD：

- **Configuration Manager 微服务**：将 Configuration Manager 与桌面分析连接。 此应用没有访问权限要求。  

- **MALogAnalyticsReader**：监视 Azure Log Analytics 工作区，确保成功复制了每日快照。 有关详细信息，请参阅 [MALogAnalyticsReader 应用程序角色](#bkmk_MALogAnalyticsReader)。  

- **Office 365 客户端管理员**：允许 Configuration Manager 从桌面分析检索部署计划信息和设备就绪状态。

如果需要在完成设置后预配这些应用，请转到“连接服务”  窗格。 选择“为用户和应用配置访问权限”  并预配应用。  

- **适用于 Configuration Manager 的 Azure AD 应用**。 如果在完成设置后需要预配或解决连接问题，请参阅[为 Configuration Manager 创建和导入应用](#create-and-import-app-for-configuration-manager)。 此应用需要在“Configuration Manager 服务”API 上“写入 CM 集合数据”  和“读取 CM 集合数据”   。  

### <a name="create-and-import-app-for-configuration-manager"></a>为 Configuration Manager 创建并导入应用

如果无法从“配置 Azure 服务”向导为 Configuration Manager 创建 Azure AD 应用，或者如果想要重用现有应用，则需要手动创建并导入它。 在桌面分析门户上完成[初始载入](set-up.md#initial-onboarding)后，使用以下步骤：

#### <a name="create-app-in-azure-ad"></a>在 Azure AD 中创建应用

1. 以具有“全局管理员”  权限的用户身份打开 [Azure 门户](https://portal.azure.com)，转到“Azure Active Directory”  ，然后选择“应用注册”  。 然后选择“新建注册”  。  

2. 在“创建”  窗格中，配置以下设置：  

    - **名称**：标识应用的唯一名称，例如 `Desktop-Analytics-Connection`  

    - **支持的帐户类型**：**仅此组织目录中的帐户 (Contoso)**

    - **重定向 URI (可选)** ：**Web**  

    <!--     - **Sign-on URL**: this value isn't used by Configuration Manager, but required by Azure AD. Enter a unique and valid URL, for example: `https://configmgrapp`   -->
  
    选择“注册”  。  

3. 选择应用，记下“应用程序(客户端) ID ”  和“目录(租户) ID”  。 这些值是用于配置 Configuration Manager 连接的 GUID。  

4. 在“管理”菜单中，选择“证书和密码”   。 选择“新建客户端密码”  。 输入“描述”  ，指定过期持续时间，然后选择“添加”  。 复制密钥的“值”，该值用于配置 Configuration Manager 连接  。

    > [!Important]  
    > 这是复制密钥值的唯一机会。 如果现在不复制，则需要创建另一个密钥。  
    >
    > 将密钥值保存在安全的位置。  

5. 在“管理”菜单中，选择“API 权限”   。  

    1. 在“API 权限”面板中，选择“添加权限”   。  

    2. 在“请求 API 权限”面板中，切换到“我的组织使用的 API”   。  

    3. 搜索并选择“Configuration Manager 微服务”  API。  

    4. 选择“应用程序权限”  组。 展开“CmCollectionData”  ，并选择以下两个权限：“写入 CM 集合数据”  和“读取 CM 集合数据”  。  

    5. 选择“添加权限”  。  

6. 在“API 权限”面板中，选择“授予管理员同意...”   。选择“是”  。  

#### <a name="import-app-in-configuration-manager"></a>在 Configuration Manager 中导入应用

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Azure 服务”节点    。 在功能区中选择“配置 Azure 服务”  。  

2. 在 Azure 服务向导的“Azure 服务”页上，配置以下设置  ：  

    - 指定 Configuration Manager 中的对象名称  。  

    - 指定可选说明以帮助标识服务  。  

    - 从可用服务列表中选择“桌面分析”  。  
  
   选择“下一步”  。  

3. 在“应用”  页上，选择相应的“Azure 环境”  。 然后选择“导入”Web 应用  。 在“导入应用”窗口中配置以下设置  ：  

    - **Azure AD 租户名称**：此名称是它在 Configuration Manager 中的命名方式  

    - **Azure AD 租户 ID**：从 Azure AD 复制的“目录 ID”   

    - **客户端 ID**：从 Azure AD 应用复制的“应用程序 ID”   

    - **密钥**：从 Azure AD 应用复制的密钥“值”   

    - **密钥到期日期**：密钥的相同过期日期  

    - **应用 ID URI**：此设置应自动填充以下值：`https://cmmicrosvc.manage.microsoft.com/`  
  
   选择“验证”，然后选择“确定”，关闭“导入应用”窗口   。 在 Azure 服务向导的“应用”页上选择“下一步”  。  

若要继续完成“诊断数据”  页上的向导其余部分，请参阅[连接到服务](connect-configmgr.md#bkmk_connect)。

#### <a name="troubleshoot-app-in-configuration-manager"></a>Configuration Manager 中的应用故障排除

如果在创建或导入应用时遇到问题，请首先检查 Smsadminui.log  中是否存在特定错误。 然后，检查以下配置：

- 你已成功将租户注册到桌面分析服务。 有关详细信息，请参阅[如何设置桌面分析](set-up.md)。

- 所有必需的终结点都是可访问的。 有关详细信息，请参阅[终结点](enable-data-sharing.md#endpoints)。

- 确保登录的用户具有正确的权限。 有关详细信息，请参阅[先决条件](overview.md#prerequisites)。

- 确保一般情况下用户可以登录 Azure。 此操作确定是否存在一般 Azure AD 身份验证问题。

- 检查有关桌面分析工作程序的 SMS_SERVICE_CONNECTOR 组件的状态消息   。

### <a name="maloganalyticsreader-application-role"></a><a name="bkmk_MALogAnalyticsReader"></a> MALogAnalyticsReader 应用程序角色

设置桌面分析即表示你代表你的组织同意。 此同意是为 MALogAnalyticsReader 应用程序分配工作区的 Log Analytics 阅读者角色。 桌面分析需要此应用程序角色。

如果在设置时此过程出现问题，请使用以下过程手动添加此权限：

1. 转到 [Azure 门户](https://portal.azure.com)，然后选择“所有资源”  。 选择“Log Analytics”类型  的工作区。  

2. 在工作区菜单中，选择“访问控制(IAM)”  ，然后选择“添加”  。  

3. 在“添加权限”面板中  ，配置以下设置：  

    - **角色**：**阅读者**  

    - **将访问权限分配到**：**Azure AD 用户、组或应用程序**  

    - **选择**：**MALogAnalyticsReader**  

4. 选择“保存”  。

门户会显示一条通知，指出它添加了角色分配。

## <a name="data-latency"></a>数据延迟

<!-- 3846531 -->
第一次设置桌面分析、注册新客户端或配置新部署计划时，Configuration Manager 和桌面分析门户中的报表可能不会立即显示完整的数据。 可能需要 2-3 天才会执行以下步骤：

- 活动设备将诊断数据发送到桌面分析服务
- 服务对数据进行处理
- 服务与 Configuration Manager 站点同步

将 Configuration Manager 层次结构中的设备集合同步到桌面分析时，这些集合可能需要一小时才能出现在桌面分析门户中。 同样，在桌面分析中创建部署计划时，与部署计划关联的新集合可能需要一小时才能出现在 Configuration Manager 层次结构中。 主站点创建集合，管理中心站点与桌面分析同步。 Configuration Manager 可能需要长达 24 小时来评估和更新集合成员身份。 若要加快此过程，请手动更新集合成员身份。<!-- 4984639 -->

> [!Note]
> 为了使手动集合更新反映更改，SMS_SERVICE_CONNECTOR_M365ADeploymentPlanWorker 组件首先需要同步。 运行此进程可能需要一小时。 有关详细信息，请参阅 **M365ADeploymentPlanWorker.log**。

在桌面分析门户中，有两种数据类型：“管理员数据”和“诊断数据”   ：

- “管理员数据”  指的是对工作区配置所做的任何更改。 例如，当更改资产的“升级决策”  或“重要性”  时，会更改管理员数据。 这些更改通常具有复合效果，因为它们会改变安装了有问题资产的设备的就绪状态。

- “诊断数据”  指的是从客户端设备上载到 Microsoft 的系统元数据。 此数据支持桌面分析。 它包括诸如设备清单之类的属性，以及安全和功能更新状态。

默认情况下，每天自动刷新桌面分析门户中的所有数据。 此刷新包括诊断数据中的更改，以及对配置（管理员数据）所做的任何更改。 它应在每天 08:00 UTC 之前显示在桌面分析门户中。

更改管理员数据时，会触发工作区中管理员数据的按需刷新。 从桌面分析门户的任意页面，打开数据流通浮出控件：

![桌面分析门户中数据流通浮出控件选项卡的屏幕截图](media/data-currency-flyout.png)

然后，选择“应用更改”  ：

![桌面分析门户中展开的数据流通浮出控件屏幕截图](media/data-currency-flyout-expand.png)

此过程通常要花费 15-60 分钟。 具体取决于工作区的大小以及需要处理的更改的范围。 请求按需刷新数据时，不会更改诊断数据。  有关详细信息，请参阅[桌面分析常见问题](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal)。

如果在上述时间范围内未看到更改发生更新，请等待 24 小时后再执行下一日刷新。 如果发现更长时间的延迟，请检查服务运行状况仪表板。 如果服务报告为正常，请联系 Microsoft 支持部门。<!-- 3896921 -->
