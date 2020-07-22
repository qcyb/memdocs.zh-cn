---
title: 设置 Wandera 移动威胁防御与 Intune 的集成
titleSuffix: Intune on Azure
description: 如何设置 Wandera 移动威胁防御解决方案与 Microsoft Intune 的集成，从而控制移动设备对公司资源的访问。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: b227148a6e16f7c9f8d62cb58eeb628afbd84123
ms.sourcegitcommit: 2e0bc4859f7e27dea20c6cc59d537a31f086c019
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86872012"
---
# <a name="integrate-wandera-mobile-threat-protection-with-intune"></a>将 Wandera 移动威胁防御与 Intune 集成  

完成以下步骤，以便将 Wandera 移动威胁防御解决方案与 Intune 相集成。  

## <a name="before-you-begin"></a>在开始之前  

在开始将 Wandera 与 Intune 集成的过程之前，请确保已具备以下先决条件：

- Intune 订阅
- Azure Active Directory 管理员凭据和能够授予下列权限的已分配角色：

    - 登录和读取用户配置文件
    - 使用已登录用户的身份访问目录
    - 读取目录数据
    - 向 Intune 发送设备风险信息
 
- 有效的 Wandera 订阅
    - 具有超级管理员权限的管理员帐户

## <a name="integration-overview"></a>集成概述

在 Wandera 和 Intune 之间启用移动威胁防御集成需要：

- 启用 Wandera 的 UEM Connect 服务，以便将信息与 Azure 和 Intune 同步。 这包括用户和设备生命周期管理 (LCM) 元数据以及移动威胁防御 (MTD) 设备威胁级别。
- 在 Wandera 中创建激活配置文件以定义设备注册行为。
- 将 Wandera 无线部署到托管的 iOS 和 Android 设备。
- 在非托管 iOS 和 Android 设备上使用 MAM-WE 为最终用户自助服务配置 Wandera。

## <a name="set-up-wandera-mobile-threat-defense-integration"></a>设置 Wandera 移动威胁防御集成

在 Wandera 和 Intune 之间设置集成不需要 Wandera 员工的任何支持，并且可以在几分钟内轻松完成。

### <a name="enable-support-for-wandera-in-intune"></a>在 Intune 中启用对 Wandera 的支持

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“租户管理” > “连接器和令牌” > “移动威胁防御” > “添加”。
3. 在“添加连接器”页上，使用下拉列表以选择“Wandera” 。 然后选择“创建”。  
4. 在“移动威胁防御”窗格中，从连接器列表中选择“Wandera”MTD 连接器，以打开“编辑连接器”窗格。 选择“打开 Wandera 管理控制台”以打开 Wandera 管理控制台 [RADAR](https://radar.wandera.com/login) 并登录。 
5. 在 Wandera RADAR 控制台中，转到“集成”>“UEM 集成”，然后选择“UEM Connect”选项卡 。使用“EMM 供应商”下拉列表，并选择“Microsoft Intune”。
6. 将显示一个如下所示的屏幕，指示完成集成所需的权限授予：

   ![集成和权限](./media/wandera-mtd-connector-integration/integrations-and-permissions.png) 

7. 在“Intune 用户和设备同步”旁，单击“授予”按钮启动进程，以同意 Wandera 使用 Azure 和 Intune 执行生命周期管理 (LCM) 功能。
8. 当出现提示时，选择或输入 Azure 管理员凭据。 查看请求的权限，然后选择“代表组织同意”复选框。 最后，单击“接受”以授权 LCM 集成。

   ![接受权限](./media/wandera-mtd-connector-integration/permissions.png)

9. 你将自动返回 RADAR 管理控制台。  如果授权成功，你将在“授予”按钮旁看到一个绿色的勾选标记。
10. 通过单击相应的“授予”按钮，为其余列出的集成重复同意过程，直到每个集成旁边都有绿色勾选标记。

11. 返回到 Intune 控制台，并继续编辑 Wandera MTD Connector。 将所有可用的开关设置为“开”，然后“保存”配置。

    ![启用 Wandera](./media/wandera-mtd-connector-integration/enable-wandera.png)

Intune 和 Wandera 现已连接。

## <a name="create-activation-profiles-in-wandera"></a>在 Wandera 中创建激活配置文件

使用 RADAR 中定义的 Wandera 激活配置文件有助于推动基于 Intune 的部署。  每个激活配置文件定义特定的配置选项，如身份验证要求、服务功能和初始组成员身份。

在 Wandera 中创建激活配置文件后，将其“分配”给 Intune 中的用户和设备。  虽然激活配置文件在设备平台和管理策略中是通用的，但以下步骤定义如何基于这些差异配置 Intune。

此处的步骤假定你已在 Wandera 中创建了要通过 Intune 部署到目标设备的激活配置文件。 若要了解创建和使用 Wandera 激活配置文件的更多详细信息，请参阅[激活配置文件指南](https://radar.wandera.com/?return_to=https://wandera.force.com/Customer/s/article/Enrollment-Links)。

> [!NOTE]
> 创建要通过 Intune 或 MAM-WE 进行部署的激活配置文件时，请确保将“关联用户”设置为“由标识提供程序进行身份验证”> Azure Active Directory 选项，以实现最大安全性、跨平台兼容性和简化的最终用户体验。

## <a name="deploying-wandera-over-the-air-to-mdm-managed-devices"></a>将 Wandera 无线部署到 MDM 托管设备

对于由 Intune 托管的 iOS 和 Android 设备，可以无线部署 Wandera 以实现快速的基于推送的激活。 在继续本部分之前，请确保已创建所需的激活配置文件。 将 Wandera 部署到托管设备涉及：
- 将 Wandera 配置文件添加到 Intune 并分配给目标设备。
- 将 Wandera 应用和相应的应用配置添加到 Intune 并分配给目标设备。

### <a name="configure-and-deploy-ios-configuration-profiles"></a>配置和部署 iOS 配置文件 

在本部分中，你将下载所需的 iOS 设备配置文件，然后通过 MDM 将这些文件通过 MDM 无线传递给 Intune 托管设备。

1. 在 RADAR 中，导航到要部署的激活配置文件（“设备”>“激活”），然后单击“部署策略”选项卡 >“托管设备”>“Microsoft Endpoint Manager” 。
2. 根据设备队列配置，展开“受 Apple iOS 监督”或“不受 Apple iOS 监督”部分 。
3. 下载提供的配置文件，并准备在下面的步骤中上传它们。
4. 打开“Microsoft Intune 管理门户”，并导航到“设备”>“iOS/iPadOS”>“配置文件” 。  单击“创建配置文件”。
5. 在出现的面板中，选择“平台”下的“iOS/iPadOS”，然后选择“配置文件”下的“自定义”  。 然后单击“创建”。
6. 在“名称”字段中，为配置提供描述性标题，最好与 RADAR 中激活配置文件所命名的内容相匹配。 这将有助于在将来简化交叉引用。 或者，如果需要，请提供激活配置文件代码。 我们建议通过为名称添加后缀来指示配置是用于“受监督”设备还是“不受监督”设备。
7. （可选）提供可为其他管理员提供有关配置用途和使用的详细信息的“描述”。 单击“下一步” 。
8. 单击“选择文件”，找到与步骤 3 中下载的相应激活配置文件对应的已下载的配置文件。 如果同时下载了“受监督”或“不受监督”配置文件，请谨慎选择相应的配置文件。 单击“下一步” 。
   <!-- image placeholder - ending future availability -->
9.  根据 Intune RBAC 实践的要求定义“范围标记”。  单击“下一步” 。
10. 将配置文件分配给应安装 Wandera 的用户组或设备。  我们建议从测试组开始，然后在验证激活正常工作后进行扩展。 单击“下一步” 。
11. 根据需要查看配置的正确性，然后单击“创建”以创建和部署配置文件。

> [!NOTE]
> Wandera 为受监督的 iOS 设备提供了增强的部署配置文件。 如果有包含受监督和不受监督的设备的混合队列，请根据需要对其他配置文件类型重复上述步骤。 对于通过 Intune 部署的任何未来激活配置文件，都需要遵循相同的步骤。 如果有包含受监督和不受监督的 iOS 设备的混合队列，并且需要受监督的基于模式的策略分配的帮助，请联系 Wandera 支持人员。 

## <a name="deploying-wandera-to-mam-we-devices"></a>将 Wandera 部署到 MAM-WE 设备
对于未由 Intune 托管且属于 (MAM-WE) 设备的设备，Wandera 利用基于身份验证的集成载入体验来激活和保护启用 MAM 的应用中的公司数据。 

以下部分介绍如何配置 Wandera 和 Intune，以使最终用户能够在访问公司数据之前无缝激活 Wandera。 

### <a name="configure-azure-device-provisioning-in-a-wandera-activation-profile"></a>在 Wandera 激活配置文件中配置 Azure 设备预配
要与 MAM-WE 一起使用的激活配置文件必须将“关联用户”设置为“由标识提供程序进行身份验证”> Azure Active Directory 选项。
1. 在 Wandera RADAR 门户中，选择现有激活配置文件，或创建新的激活配置文件，MAM-WE 设备将在通过“设备”>“激活”进行注册时使用该配置文件。 
2. 依次单击“部署策略”选项卡和“非托管设备”，然后滚动到“Azure 设备预配”部分 。
3. 将“Azure AD 租户 ID”输入到相应的文本字段。 如果没有现成的租户 ID，请单击“获取我的租户 ID”链接，在新选项卡中打开 Azure AD，你可以在该选项卡中轻松地将此值复制到剪贴板。
4. （可选）指定“组 ID”，以将用户激活限制到特定组。
   - 如果定义了一个或多个“组 ID”，则激活 MAM-WE 的用户必须是至少一个指定组的成员，才能使用此激活配置文件进行激活。
   - 你可以设置配置了相同 Azure 租户 ID 但具有不同组 ID 的多个激活配置文件。 这样你便可以根据 Azure 组成员身份将设备注册到 Wandera 中，从而在激活时按组启用差异化功能。
   - 可以配置一个不指定任何组 ID 的“默认”激活配置文件。  此组将作为所有激活的全部捕获，其中经过身份验证的用户不是与其他激活配置文件相关联的组的成员。
5. 单击该页右上角的“保存”。

## <a name="next-steps"></a>后续步骤
- 将 Wandera 激活配置文件加载到 RADAR 中后，在 Intune 中创建客户端应用以将 Wandera 应用部署到 Android 和 iOS/iPadOS 设备。 Wandera 应用配置提供了用于补充推送的设备配置文件的重要功能，建议对所有部署使用该配置。 有关特定于 Wandera 应用的过程和自定义详细信息，请参阅[添加 MTD 应用](mtd-apps-ios-app-configuration-policy-add-assign.md)。 
- 现已将 Wandera 与 Endpoint Manager 集成，现在可以调整配置、查看报告，以及在移动设备队列中更广泛地部署。 若要详细了解配置指南，请参阅 Wandera 文档中的[支持中心入门指南](https://radar.wandera.com/?return_to=https://wandera.force.com/Customer/s/getting-started)。
