---
title: 在 Microsoft Intune 中使用终结点安全性策略管理终结点检测和响应设置| Microsoft Docs
description: 在 Microsoft Endpoint Manager 中为使用终结点安全性终结点检测和响应策略管理的设备配置和部署策略。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: cba7b357dfae0c9dae06e8a21ddd0583fd96bcae
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820521"
---
# <a name="endpoint-detection-and-response-policy-for-endpoint-security-in-intune"></a>Intune 中关于终结点安全性的终结点检测和响应策略

将 Microsoft Defender 高级威胁防护 (Microsoft Defender ATP) 和 Intune 进行集成时，可以使用用于终结点检测和响应 (EDR) 的终结点安全性策略来管理 EDR 设置并将设备加入 Microsoft Defender ATP。

Microsoft Defender ATP 终结点检测和响应功能提供准实时且可操作的高级攻击检测。 安全分析师可以有效地对警报进行优先级排序、全面了解漏洞，并采取响应操作来消除威胁。

EDR 策略包括特定于平台的配置文件，用于管理 EDR 的设置。 配置文件自动包括用于 Microsoft Defender ATP 的加入包。 加入包用于确定如何配置设备以将其与 Microsoft Defender ATP 结合使用。 加入设备后，可以开始使用该设备的威胁数据。

EDR 策略部署到使用 Intune 管理的 Azure Active Directory (Azure AD) 中的设备组，并部署到使用 Configuration Manager 管理的本地设备集合，包括 Windows 服务器。 不同管理路径的 EDR 策略需要不同的加入包。 因此，需要为所管理的不同类型的设备创建单独的 EDR 策略。

在 [Microsoft endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)的“终结点安全性”节点的“管理”下查找用于 EDR 的终结点安全性策略。

查看[终结点检测和响应配置文件设置的设置](endpoint-security-edr-profile-settings.md)。

## <a name="prerequisites-for-edr-policies"></a>EDR 策略的先决条件

常规：

- **Microsoft Defender 高级威胁防护租户** - 必须先将 Microsoft Defender ATP 租户和 Microsoft Endpoint Manager 租户（Intune 订阅）集成，才能创建 EDR 策略。 请参阅 Intune 文档中的[使用 Microsoft Defender ATP](advanced-threat-protection.md)。

**对 Configuration Manager 客户端的支持**：

- **为 Configuration Manager 设备设置租户附加** - 若要支持将 EDR 策略部署到 Configuration Manager 托管的设备，请配置 *“租户附加”* 。 这包含配置 Configuration Manager 设备集合，以支持 Intune 终结点安全策略。

  若要设置租户附加，包括将 Configuration Manager 集合同步到 Microsoft Endpoint Manager 管理中心，并使其可以使用终结点安全策略，请参阅[配置租户附加以支持 Endpoint Protection 策略](../protect/tenant-attach-intune.md)。

## <a name="edr-profiles"></a>EDR 配置文件

[查看](endpoint-security-edr-profile-settings.md)可为以下平台和配置文件配置的设置。

**Intune** - 对于使用 Intune 管理的设备，支持以下内容：

- 平台：**Windows 10 及更高版本** - Intune 将策略部署到 Azure AD 组中的设备。
- 配置文件：终结点检测和响应 (MDM)

**Configuration Manager** - 使用 Configuration Manager 管理的设备支持以下功能：

- 平台：**Windows 10 和 Windows Server - Configuration Manager (ConfigMgr)** 将策略部署到 Configuration Manager 集合中的设备。
- 配置文件：**终结点检测和响应 (ConfigMgr)**

## <a name="set-up-configuration-manager-to-support-edr-policy"></a>设置 Configuration Manager 以便支持 EDR 策略

在将 EDR 策略部署到 Configuration Manager 设备之前，请完成以下各部分中详细介绍的配置。

在 Configuration Manager 控制台中生成这些配置并用于 Configuration Manager 部署。 如果不熟悉 Configuration Manager，可计划结合使用 Configuration Manager 管理中心来完成这些任务。  

以下部分介绍了需完成的任务：

1. [为 Configuration Manager 安装更新](#task-1-install-the-update-for-configuration-manager)
2. [启用租户附加](#task-2-configure-tenant-attach-and-synchronize-collections)  

> [!TIP]
> 若要详细了解如何将 Microsoft Defender ATP 与 Configuration Manager 结合使用，请参阅 Configuration Manager 内容中的以下文章：
>
> - [通过 Microsoft Endpoint Manager 管理中心将 Configuration Manager 客户端加入 Microsoft Defender ATP](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Microsoft Endpoint Manager 租户附加：设备同步和设备操作](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach)

### <a name="task-1-install-the-update-for-configuration-manager"></a>任务 1：为 Configuration Manager 安装更新

Configuration Manager 版本 2002 需要更新，以便支持结合使用从 Microsoft Endpoint Manager 管理中心部署的终结点检测和响应策略。

**更新详细信息**：

- Configuration Manager 2002 修补程序 (KB4563473)

你会发现此更新是一项 Configuration Manager 2002 的控制台内部更新。

若要安装此更新，请按照 Configuration Manager 文档中[安装控制台内部更新](../../configmgr/core/servers/manage/install-in-console-updates.md)中的指南进行操作。

安装更新后，返回此处以继续配置环境，使其能够支持 Microsoft Endpoint Manager 管理中心的 EDR 策略。

### <a name="task-2-configure-tenant-attach-and-synchronize-collections"></a>任务 2：配置租户附加及同步集合

通过租户附加，可从 Configuration Manager 部署中指定要与 Microsoft Endpoint Manager 管理中心同步的设备集合。 同步集合后，使用管理中心查看关于这些设备的信息并将 EDR 策略从 Intune 部署到集合。  

有关租户附加方案的详细信息，请参阅 Configuration Manager 内容中的[启用租户附加](../../configmgr/tenant-attach/device-sync-actions.md)。

#### <a name="enable-tenant-attach-when-co-management-hasnt-been-enabled"></a>在尚未启用共同管理时启用租户附加

> [!TIP]
> 使用 Configuration Manager 控制台中的“共同管理配置向导”启用租户附加，但无需启用共同管理。

如果计划启用共同管理，请先熟悉共同管理、其先决条件以及如何管理工作负载，然后再继续。 请参阅 Configuration Manager 文档中的[什么是共同管理？](../../configmgr/comanage/overview.md)。

1. 在 Configuration Manager 管理控制台中，转到“管理” > “概述” > “云服务” > “共同管理”   。
2. 在功能区中，单击“配置共同管理”打开向导。
3. 在“租户加入”页面上，为环境选择“AzurePublicCloud” 。 不支持 Azure 政府云。
   1. 单击“登录”。 使用全局管理员帐户登录。

对于使用 Intune 管理的设备，支持以下内容：

- 平台：**Windows 10 及更高版本** - Intune 将策略部署到 Azure AD 组中的设备。
  - 配置文件：终结点检测和响应 (MDM)

### <a name="devices-managed-by-configuration-manager-in-preview"></a>Configuration Manager 托管的设备 *（处于预览状态）*

使用 Configuration Manager 通过*租户附加*方案管理的设备支持以下功能：

- 平台：**Windows 10 和 Windows Server - Configuration Manager (ConfigMgr)** 将策略部署到 Configuration Manager 集合中的设备。
  - 配置文件：终结点检测和响应 (ConfigMgr)（预览）

## <a name="create-and-deploy-edr-policies"></a>创建和部署 EDR 策略

将 Microsoft Defender ATP 订阅与 Intune 集成时，可以创建和部署 EDR 策略。 可以创建两种不同类型的 EDR 策略。 一种策略类型适用于通过 MDM 并使用 Intune 管理的设备。 第二种类型适用于使用 Configuration Manager 管理的设备。

通过为策略选择平台，可在配置新的 EDR 策略时选择要创建的策略类型。

将策略部署到由 Configuration Manager 托管的设备之前，需要先在 Microsoft Endpoint Manager 管理中心将 Configuration Manager 设置为支持 EDR 策略。 请参阅[配置租户附加以支持 Endpoint Protection 策略](../protect/tenant-attach-intune.md)。


### <a name="create-edr-policies"></a>创建 EDR 策略

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“终结点安全性” > “终结点检测和响应” > “创建策略”  。

3. 为策略选择平台和配置文件。 可通过以下信息确定选项：

   - Intune - Intune 将策略部署到 Azure AD 组中的设备。 创建策略时，请选择：
     - 平台：**Windows 10 及更高版本**
     - 配置文件：终结点检测和响应 (MDM)

   - Configuration Manager - Configuration Manager 将策略部署到 Configuration Manager 集合中的设备。 创建策略时，请选择：
     - 平台：**Windows 10 和 Windows Server (ConfigMgr)**
     - 配置文件：**终结点检测和响应 (ConfigMgr)**

4. 选择“创建”。

5. 在“基本信息”页上，输入配置文件的名称和说明，然后选择“下一步” 。

6. 在“配置设置”页面上，配置要使用此配置文件管理的设置。 加入包自动包含在内，且不可进行配置。

   完成配置设置后，选择“下一步”。

7. 此步骤仅适用于“终结点检测和响应(MDM)”配置文件：  

   在“作用域标记”页上，选择“选择作用域标记”以打开“选择标记”窗格，将作用域标记分配给配置文件 。
  
   选择“下一步”继续操作。

8. 在“分配”页上，选择将接收此策略的组或集合。 选择取决于所选的平台和配置文件：

   - 对于 Intune，需要从 Azure AD 中选择组。
   - 对于 Configuration Manager，需要从 Configuration Manager 中选择已同步到 Microsoft Endpoint Manager 管理中心并已能够使用 Microsoft Defender ATP 策略的集合。

   可以选择不在此时分配组或集合，而是在以后编辑策略来添加分配。

   完成后，选择“下一步”。

9. 完成后，在“查看 + 创建”页上，选择“创建” 。

   为创建的配置文件选择策略类型时，新配置文件将显示在列表中。

## <a name="edr-policy-reports"></a>EDR 策略报告

可以在 Microsoft Endpoint Manager 管理中心查看有关所部署的 EDR 策略的详细信息。 若要查看详细信息，请转到“终结点安全性” > “终结点部署和响应”，然后选择要查看合规性详细信息的策略 ：

- 对于面向 Windows 10 及更高版本 (Intune) 的策略，会显示策略合规性概述。 还可以选择图表以查看接收了策略的设备的列表，并深入了解各个设备的详细信息。

  **“具有 ATP 传感器的设备”** 的图表仅显示通过使用 **Windows 10 及更高版本**配置文件成功加入 Microsoft Defender ATP 的设备。 若要确保此图表中完整显示你的设备，请将加入配置文件部署到你的所有设备中。 通过外部方法（如组策略或 PowerShell）加入 Microsoft Defender ATP 的设备被视为不具有 ATP 传感器的设备。

- 对于面向**Windows 10 和 Windows Server 平台 (Configuration Manager)** 的策略，会看到策略合规性概述，但无法深入了解其他详细信息。 此视图的信息有限，因为管理中心从 Configuration Manager 接收到的状态详细信息有限，Configuration Manager 管理 Configuration Manager 设备的策略部署。

[查看](endpoint-security-edr-profile-settings.md)可同时为平台和配置文件配置的设置。

## <a name="next-steps"></a>后续步骤

- [配置终结点安全策略](endpoint-security-policy.md#create-an-endpoint-security-policy)
- 阅读 Microsoft Defender ATP 文档，详细了解[终结点检测和响应](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response)。
