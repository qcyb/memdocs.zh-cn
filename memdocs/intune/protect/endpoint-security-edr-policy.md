---
title: 在 Microsoft Intune 中使用终结点安全性策略管理终结点检测和响应设置| Microsoft Docs
description: 在 Microsoft Endpoint Manager 中为使用终结点安全性终结点检测和响应策略管理的设备配置和部署策略。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/29/2020
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
ms.openlocfilehash: ae95fb48296f778fb98affa2270ba763d79fb766
ms.sourcegitcommit: 97f150f8ba8be8746aa32ebc9b909bb47e22121c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84879675"
---
# <a name="endpoint-detection-and-response-policy-for-endpoint-security-in-intune"></a>Intune 中关于终结点安全性的终结点检测和响应策略

将 Microsoft Defender 高级威胁防护 (Microsoft Defender ATP) 和 Intune 进行集成时，可以使用用于终结点检测和响应 (EDR) 的终结点安全性策略来管理 EDR 设置并将设备加入 Microsoft Defender ATP。

Microsoft Defender ATP 终结点检测和响应功能提供准实时且可操作的高级攻击检测。 安全分析师可以有效地对警报进行优先级排序、全面了解漏洞，并采取响应操作来消除威胁。

EDR 策略包括特定于平台的配置文件，用于管理 EDR 的设置。 配置文件自动包括用于 Microsoft Defender ATP 的加入包。 加入包用于确定如何配置设备以将其与 Microsoft Defender ATP 结合使用。 加入设备后，可以开始使用该设备的威胁数据。

EDR 策略部署到使用 Intune 管理的 Azure Active Directory (Azure AD) 中的设备组，并部署到使用 Configuration Manager 管理的本地设备集合，包括 Windows 服务器。 不同管理路径的 EDR 策略需要不同的加入包。 因此，需要为所管理的不同类型的设备创建单独的 EDR 策略。

> [!TIP]
> 公共预览版支持使用 Configuration Manager 管理的设备。

在 [Microsoft endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)的“终结点安全性”节点的“管理”下查找用于 EDR 的终结点安全性策略。

查看[终结点检测和响应配置文件设置的设置](endpoint-security-edr-profile-settings.md)。

## <a name="prerequisites-for-edr-policies"></a>EDR 策略的先决条件

常规：

- **Microsoft Defender 高级威胁防护租户** - 必须先将 Microsoft Defender ATP 租户和 Microsoft Endpoint Manager 租户（Intune 订阅）集成，才能创建 EDR 策略。 请参阅 Intune 文档中的[使用 Microsoft Defender ATP](advanced-threat-protection.md)。

**支持 Configuration Manager 设备**：

若要支持将 EDR 策略用于 Configuration Manager 设备，Configuration Manager 环境需要以下其他配置。 本文提供了[配置指南](#set-up-configuration-manager-to-support-edr-policy)：

- **2002 版或更高版本的 Configuration Manager** - 网站需要运行 Configuration Manager 2002 或更高版本。

- **安装 Configuration Manager 更新** - 若要在 Configuration Manager 2002 中启用支持，即支持使用在 Microsoft Endpoint Manager 管理中心创建的 EDR 策略，请从 Configuration Manager 控制台中安装以下更新：
  - Configuration Manager 2002 修补程序 (KB4563473)

- **配置租户附加** - 通过租户附加，可以将设备集合从 Configuration Manager 同步到 Microsoft Endpoint Manager 管理中心。 然后，可以使用管理中心将 EDR 策略部署到这些集合。

  租户附加通常配置为共同管理，但可以独立配置租户附加。

- **同步 Configuration Manager 集合** - 配置租户附加时，可选择要与 Microsoft Endpoint Manager 管理中心同步的 Configuration Manager 设备集合。 还可以稍后返回并修改要同步的设备集合。Configuration Manager 设备的 EDR 策略只能分配给已同步的集合。

  选择要同步的集合后，必须启用它们以便与 Microsoft Defender ATP 结合使用。

- **Azure AD 的权限** - 若要完成租户附加的设置，并配置将与 Microsoft Endpoint Manager 管理中心同步的 Configuration Manager 集合，需要一个对 Azure 订阅具有全局管理员权限的帐户。

## <a name="edr-profiles"></a>EDR 配置文件

[查看](endpoint-security-edr-profile-settings.md)可为以下平台和配置文件配置的设置。

**Intune** - 对于使用 Intune 管理的设备，支持以下内容：

- 平台：**Windows 10 及更高版本** - Intune 将策略部署到 Azure AD 组中的设备。
- 配置文件：终结点检测和响应 (MDM)

**Configuration Manager**（预览版） - 使用 Configuration Manager 管理的设备支持以下内容：

- 平台：Windows 10 和 windows Server - Configuration Manager 将策略部署到 Configuration Manager 集合中的设备。
- 配置文件：终结点检测和响应 (ConfigMgr)（预览）

## <a name="set-up-configuration-manager-to-support-edr-policy"></a>设置 Configuration Manager 以便支持 EDR 策略

在将 EDR 策略部署到 Configuration Manager 设备之前，请完成以下各部分中详细介绍的配置。

在 Configuration Manager 控制台中生成这些配置并用于 Configuration Manager 部署。 如果不熟悉 Configuration Manager，可计划结合使用 Configuration Manager 管理中心来完成这些任务。  

以下部分介绍了需完成的任务：

1. [为 Configuration Manager 安装更新](#task-1-install-the-update-for-configuration-manager)
2. [启用租户附加](#task-2-configure-tenant-attach-and-synchronize-collections)  
3. [选择要同步的集合](#task-3-select-collections-to-synchronize)
4. [为 Microsoft Defender ATP 启用集合](#task-4-enable-collections-for-microsoft-defender-atp)

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

如果之前已启用共同管理，则已设置好租户附加，可以跳到[任务 3](#task-3-select-collections-to-synchronize)。

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

   2. 确保在“租户加入”页面上选择“上传到 Microsoft Endpoint Manager 管理中心” 。

   3. 取消选中“为共同管理启用自动客户端注册”。

      选择此选项后，向导会显示其他页面，用于完成共同管理的设置。 有关详细信息，请参阅 Configuration Manager 内容中的[启用共同管理](../../configmgr/comanage/how-to-enable.md)。

     ![配置租户附加](media/endpoint-security-edr-policy/tenant-onboarding.png)

4. 单击“下一步”，然后单击“是”接受“创建 AAD 应用程序”通知  。 此操作可预配一个服务主体，并创建 Azure AD 应用程序注册，以促进将集合同步到 Microsoft Endpoint Manager 管理中心。

5. 在“配置上传”页面上，配置要同步的集合。可以将配置限制为一个或多个设备集合，或针对“我所有由 Microsoft Endpoint Configuration Manager 管理的设备”使用推荐的设备上传设置。

6. 单击“摘要”查看所选内容，然后单击“下一步” 。

7. 完成向导后，单击“关闭”。

   现已配置租户附加，并已选择要同步到 Endpoint Manager 管理中心的集合。

#### <a name="enable-tenant-attach-when-you-use-co-management"></a>使用共同管理时启用租户附加

1. 在 Configuration Manager 管理控制台中，转到“管理” > “概述” > “云服务” > “共同管理”   。

2. 右键单击共同管理设置，然后选择“属性”。

3. 在“配置上传”选项卡中，选择“上传到 Microsoft Endpoint Manager 管理中心” 。 单击“应用” 。
   - 设备上传的默认设置是“我所有由 Microsoft Endpoint Configuration Manager 管理的设备”。 还可以选择将配置限制到一个或多个设备集合。

     ![查看共同管理属性选项卡](media/endpoint-security-edr-policy/configure-upload.png)

4. 出现提示时，请使用全局管理员帐户登录。

5. 单击“是”接受“创建 AAD 应用程序”通知 。 此操作可预配一个服务主体，并创建 Azure AD 应用程序注册以促进同步。

6. 完成更改后，单击“确定”退出共同管理属性。

   现已配置租户附加，并已选择要同步到 Endpoint Manager 管理中心的集合。

### <a name="task-3-select-collections-to-synchronize"></a>任务 3：选择要同步的集合

配置租户附加之后，可以选择要同步的集合。如果尚未同步集合或需要重新配置要同步的集合，可以在 Configuration Manager 控制台中编辑共同管理的属性以执行此操作。

#### <a name="select-collections"></a>选择集合

1. 在 Configuration Manager 管理控制台中，转到“管理” > “概述” > “云服务” > “共同管理”   。

2. 右键单击共同管理设置，然后选择“属性”。

3. 在“配置上传”选项卡中，选择“上传到 Microsoft Endpoint Manager 管理中心” 。 单击“应用” 。

   设备上传的默认设置是“我所有由 Microsoft Endpoint Configuration Manager 管理的设备”。 还可以选择将配置限制到一个或多个设备集合。

### <a name="task-4-enable-collections-for-microsoft-defender-atp"></a>任务 4：为 Microsoft Defender ATP 启用集合

配置要同步到 Microsoft Endpoint Manager 管理中心的集合之后，仍然需要让这些集合有资格加入 Microsoft Defender ATP 和使用其策略。  为此，请在 Configuration Manager 控制台中编辑每个集合的属性。

#### <a name="enable-collections-for-use-with-advanced-threat-protection"></a>使集合能够与高级威胁防护结合使用

1. 在连接到顶层站点的 Configuration Manger 控制台中，右键单击同步到 Microsoft Endpoint Manager 管理中心的设备集合，然后选择“属性”。

2. 在“云同步”选项卡上，启用“使此集合可用于在 Intune 中分配 Microsoft Defender ATP 策略”。

   - 如果 Configuration Manager 层次结构未配置租户附加，则无法选择此选项。
  
   ![配置云同步](media/endpoint-security-edr-policy/cloud-sync.png)

3. 选择“确定”保存配置。

   此集合中的设备现在可以接收 Microsoft Defender ATP 策略了。

## <a name="create-and-deploy-edr-policies"></a>创建和部署 EDR 策略

如果 Microsoft Defender ATP 订阅与 Intune 集成，可以创建和部署 EDR 策略。 可以创建两种不同类型的 EDR 策略。 一种策略类型适用于通过 MDM 并使用 Intune 管理的设备。 第二种类型适用于使用 Configuration Manager 管理的设备。

为策略选择了该平台时，在创建新的 EDR 策略时需要选择创建的策略类型。

将策略部署到由 Configuration Manager 托管的设备之前，需要先在 Microsoft Endpoint Manager 管理中心[将 Configuration Manager 设置为支持 EDR 策略](#set-up-configuration-manager-to-support-edr-policy)。

### <a name="create-edr-policies"></a>创建 EDR 策略

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“终结点安全性” > “终结点检测和响应” > “创建策略”  。

3. 为策略选择平台和配置文件。 可通过以下信息确定选项：

   - Intune - Intune 将策略部署到 Azure AD 组中的设备。 创建策略时，请选择：
     - 平台：**Windows 10 及更高版本**
     - 配置文件：终结点检测和响应 (MDM)

   - Configuration Manager - Configuration Manager 将策略部署到 Configuration Manager 集合中的设备。 创建策略时，请选择：
     - 平台：Windows 10 和 Windows Server
     - 配置文件：终结点检测和响应 (ConfigMgr)（预览）

4. 选择“创建”。

5. 在“基本信息”页上，输入配置文件的名称和说明，然后选择“下一步” 。

6. 在“配置设置”页面上，配置要使用此配置文件管理的设置。 加入包自动包含在内，且不可进行配置。

   完成配置设置后，选择“下一步”。

7. 此步骤仅适用于“终结点检测和响应(MDM)”配置文件**：  

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

  “具有 ATP 传感器的设备”图表仅显示通过使用 Windows 10 及更高版本配置文件成功加入 Microsoft Defender ATP 的设备 。 若要确保此图表中完整显示你的设备，请将加入配置文件部署到你的所有设备中。 通过外部方法（如组策略或 PowerShell）加入 Microsoft Defender ATP 的设备被视为不具有 ATP 传感器的设备。

- 对于面向 Windows 10 和 Windows Server 平台 (Configuration Manager) 的策略，会看到策略合规性概述，但无法深入了解其他详细信息。 此视图的信息有限，因为管理中心从 Configuration Manager 接收到的状态详细信息有限，Configuration Manager 管理 Configuration Manager 设备的策略部署。


[查看](endpoint-security-edr-profile-settings.md)可同时为平台和配置文件配置的设置。

## <a name="next-steps"></a>后续步骤

- [配置终结点安全策略](endpoint-security-policy.md#create-an-endpoint-security-policy)
- 阅读 Microsoft Defender ATP 文档，详细了解[终结点检测和响应](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response)。
