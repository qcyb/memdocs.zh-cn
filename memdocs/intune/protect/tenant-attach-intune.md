---
title: 将 Intune 策略用于附加了租户的 Configuration Manager 设备| Microsoft Docs
description: 将 Configuration Manager 设备的租户附加配置为 Microsoft Endpoint Manager 管理中心，以便可以将所支持的策略从 Microsoft Intune 部署到这些设备。
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
ms.openlocfilehash: 5c3d5bd14efddc74e1898f374bbaac2aa962ebf7
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193659"
---
# <a name="configure-tenant-attach-to-support-endpoint-security-policies-from-intune"></a>配置租户附加以支持 Intune 中的终结点安全策略

使用 Configuration Manager 租户附加方案时，可以将终结点安全策略从 Intune 部署到使用 Configuration Manager 管理的设备。 若要使用此方案，必须首先为 Configuration Manager 配置租户附加，并从 Configuration Manager 启用设备集合，以便用于 Intune。 启用集合以供使用后，可以使用 Microsoft Endpoint Manager 管理中心创建和部署策略。

附加了租户的 Configuration Manager 设备支持下列策略类型：

- 终结点安全防病毒策略
- 终结点安全终结点检测广告响应策略

## <a name="requirements-to-use-intune-policy-for-tenant-attach"></a>使用 Intune 租户附加策略的要求

若要支持将 Intune 终结点安全策略用于 Configuration Manager 设备，Configuration Manager 环境需要以下配置。 本文提供了[配置指南](#set-up-configuration-manager-to-support-intune-policies)：

### <a name="general-requirements-for-tenant-attach"></a>租户附加的一般要求

- **配置租户附加** - 通过*租户附加*方案，可以将设备集合从 Configuration Manager 同步到 Microsoft Endpoint Manager 管理中心。 然后，可以使用管理中心将所支持的策略部署到这些集合。

  租户附加通常配置为共同管理，但可以独立配置租户附加。

- **同步 Configuration Manager 集合** - 配置租户附加时，可选择要与 Microsoft Endpoint Manager 管理中心同步的 Configuration Manager 设备集合。 还可以稍后返回并修改要同步的设备集合。Configuration Manager 设备的所支持策略只能分配给已同步的集合。

  选择要同步的集合后，必须启用它们以便用于 Intune 中的终结点安全策略。

- **Azure AD 的权限** - 若要完成租户附加的设置，需要具有 Azure 订阅的全局管理员权限的帐户。

### <a name="specific-requirements-for-intune-endpoint-security-policies"></a>Intune 终结点安全策略的特定要求

- **防病毒策略**（*预览*）：

  - **Configuration Manager** - 支持以下环境：

    - **Configuration Manager Current Branch 2006 或更高版本** - 此当前分支版本添加了对 Intune 防病毒策略的支持。
    <!--
    - **Configuration Manager technical preview 2007 or later** - Support for Intune antivirus policies was added with this technical preview version. -->

  - **Microsoft Defender 高级威胁防护租户** - 必须先将 Microsoft Defender ATP 租户和 Microsoft Endpoint Manager 租户（Intune 订阅）集成。  请参阅 Intune 文档中的[使用 Microsoft Defender ATP](advanced-threat-protection.md)。

- **终结点检测和响应策略**：

  - **Configuration Manager** - 支持以下环境：

    - **Configuration Manager 技术预览 2003 或更高版本** - 技术预览版本 2003 添加了对 Intune 终结点检测和响应策略的支持。

    - **Configuration Manager Current Branch 2002 或更高版本** - 如果使用 Configuration Manager 版本 2002，则必须安装控制台内更新 **Configuration Manager 2002 修补程序 (KB4563473)** 。 此更新实现了在 Configuration Manager 2002 中对使用终结点安全策略的支持。

  - **Microsoft Defender 高级威胁防护租户** - 必须先将 Microsoft Defender ATP 租户和 Microsoft Endpoint Manager 租户（Intune 订阅）集成。  请参阅 Intune 文档中的[使用 Microsoft Defender ATP](advanced-threat-protection.md)。

## <a name="set-up-configuration-manager-to-support-intune-policies"></a>设置 Configuration Manager 以便支持 Intune 策略

在将 Intune 策略部署到 Configuration Manager 设备之前，请完成以下各部分中详细介绍的配置。 这些配置将 Configuration Manager 设备加入 Microsoft Defender ATP，并使其可以使用 Intune 策略。

以下任务在 Configuration Manager 控制台中完成。 如果不熟悉 Configuration Manager，可结合使用 Configuration Manager 管理中心来完成这些任务。

1. [为 Configuration Manager 安装更新](#task-1-install-the-update-for-configuration-manager)
2. [启用租户附加](#task-2-configure-tenant-attach-and-synchronize-collections)  
3. [选择要同步的集合](#task-3-select-collections-to-synchronize)
4. [启用集合以支持 Intune 策略](#task-4-enable-collections-for-endpoint-security-policies)

> [!TIP]
> 若要详细了解如何将 Microsoft Defender ATP 与 Configuration Manager 结合使用，请参阅 Configuration Manager 内容中的以下文章：
>
> - [通过 Microsoft Endpoint Manager 管理中心将 Configuration Manager 客户端加入 Microsoft Defender ATP](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Microsoft Endpoint Manager 租户附加：设备同步和设备操作](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach)

### <a name="task-1-install-the-update-for-configuration-manager"></a>任务 1：为 Configuration Manager 安装更新

如果使用 Configuration Manager Current Branch 版本2002，请安装以下控制台内更新，以添加对从 Microsoft Endpoint Manager 管理中心部署的终结点安全策略的支持。

**更新详细信息**：

- Configuration Manager 2002 修补程序 (KB4563473)

若要安装此更新，请按照 Configuration Manager 文档中[安装控制台内部更新](../../configmgr/core/servers/manage/install-in-console-updates.md)中的指南进行操作。

安装更新后，返回此处以继续配置环境，使其能够支持 Microsoft Endpoint Manager 管理中心的终结点安全策略。

### <a name="task-2-configure-tenant-attach-and-synchronize-collections"></a>任务 2：配置租户附加及同步集合

通过租户附加，可从 Configuration Manager 部署中指定要与 Microsoft Endpoint Manager 管理中心同步的设备集合。 同步集合后，使用管理中心查看关于这些设备的信息并将终结点安全策略从 Intune 部署到集合。

有关租户附加方案的详细信息，请参阅 Configuration Manager 内容中的[启用租户附加](../../configmgr/tenant-attach/device-sync-actions.md)。

#### <a name="enable-tenant-attach-when-co-management-hasnt-been-enabled"></a>在尚未启用共同管理时启用租户附加

> [!TIP]
> 使用 Configuration Manager 控制台中的“共同管理配置向导”启用租户附加，但无需启用共同管理。
>
> 如果计划启用共同管理，请先熟悉共同管理、其先决条件以及如何管理工作负载，然后再继续。 请参阅 Configuration Manager 文档中的[什么是共同管理？](../../configmgr/comanage/overview.md)。

1. 在 Configuration Manager 管理控制台中，转到“管理” > “概述” > “云服务” > “共同管理”   。
2. 在功能区中，单击“配置共同管理”打开向导。
3. 在“租户加入”页面上，为环境选择“AzurePublicCloud” 。 不支持 Azure 政府云。
   1. 单击“登录”。 使用全局管理员帐户登录。

   2. 确保在“租户加入”页面上选择“上传到 Microsoft Endpoint Manager 管理中心” 。

   3. 取消选中“为共同管理启用自动客户端注册”。

      选择此选项后，向导会显示其他页面，用于完成共同管理的设置。 有关详细信息，请参阅 Configuration Manager 内容中的[启用共同管理](../../configmgr/comanage/how-to-enable.md)。

     ![配置租户附加](./media/tenant-attach-intune/tenant-onboarding.png)

4. 单击“下一步”，然后单击“是”接受“创建 AAD 应用程序”通知  。 此操作可预配一个服务主体，并创建 Azure AD 应用程序注册，以促进将集合同步到 Microsoft Endpoint Manager 管理中心。

5. 在“配置上传”页面上，配置要同步的集合。可以将配置限制为一个或多个设备集合，或针对“我所有由 Microsoft Endpoint Configuration Manager 管理的设备”使用推荐的设备上传设置。

   > [!TIP]
   > 现在可以跳过选择集合，稍后可以使用以下任务（任务 3）中的信息来配置哪些集合与 Microsoft Endpoint Manager 管理中心同步。

6. 单击“摘要”查看所选内容，然后单击“下一步” 。

7. 完成向导后，单击“关闭”。

   现已配置租户附加，并已选择要同步到 Endpoint Manager 管理中心的集合。

#### <a name="enable-tenant-attach-when-you-already-use-co-management"></a>已使用共同管理时启用租户附加

1. 在 Configuration Manager 管理控制台中，转到“管理” > “概述” > “云服务” > “共同管理”   。

2. 右键单击共同管理设置，然后选择“属性”。

3. 在“配置上传”选项卡中，选择“上传到 Microsoft Endpoint Manager 管理中心” 。 单击“应用” 。

   设备上传的默认设置是“我所有由 Microsoft Endpoint Configuration Manager 管理的设备”。 还可以选择将配置限制到一个或多个设备集合。

   ![查看共同管理属性选项卡](./media/tenant-attach-intune/configure-upload.png)

   > [!TIP]
   > 现在可以跳过选择集合，稍后可以使用以下任务（任务 3）中的信息来配置哪些集合与 Microsoft Endpoint Manager 管理中心同步。

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

### <a name="task-4-enable-collections-for-endpoint-security-policies"></a>任务 4：启用终结点安全策略的集合

将集合配置为同步到 Microsoft Endpoint Manager 管理中心后，使这些集合可以使用终结点安全策略。 当启用设备集合以使用 Intune 中的终结点安全策略时，你要将这些集合中的设备配置为加入 Microsoft Defender ATP。

#### <a name="enable-collections-for-use-with-endpoint-security-policies"></a>启用用于终结点安全策略的集合

[!INCLUDE [Enable endpoint security policies for a Configuration Manager collection](includes/make-configmgr-collection-available-edr.md)]

## <a name="next-steps"></a>后续步骤

- [为*防病毒*和*终结点检测和响应*配置终结点安全策略](endpoint-security-policy.md#create-an-endpoint-security-policy)。

- 阅读 Microsoft Defender ATP 文档，详细了解[终结点检测和响应](/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response)。