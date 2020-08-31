---
title: Microsoft Intune 中的设备符合性合作伙伴 - Azure | Microsoft Docs
description: 将第三方设备符合性合作伙伴用作使用 Intune 托管的设备的符合性数据源。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/17/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fe6a46c10f55378292e57548494852c4014c062a
ms.sourcegitcommit: 21b6c0c054e5371f32d611a2411ccd166b0e03bc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88643697"
---
# <a name="support-third-party-device-compliance-partners-in-intune"></a>支持 Intune 中的第三方设备符合性合作伙伴

对于你通过一个或多个第三方设备符合性合作伙伴托管的设备，Microsoft Intune 可以向 Azure Active Directory (Azure AD) 添加符合性状态数据。 通过此配置，这些设备的符合性数据可以用于条件访问策略。

默认情况下，Intune 设置为设备的移动设备管理 (MDM) 机构。 将符合性合作伙伴添加到 Azure AD 和 Intune 后，你会将该合作伙伴配置为通过 Azure AD 用户组分配给该合作伙伴的设备的移动设备管理 (MDM) 机构的源。

若要允许使用来自设备符合性合作伙伴的数据，请完成以下任务：

1. 将 Intune 配置为使用设备合规性合作伙伴，然后配置其设备由该符合性合作伙伴管理的用户组。

2. 配置符合性合作伙伴以将数据发送到 Intune。

3. 将 iOS 或 Android 设备注册到该设备符合性合作伙伴。

完成这些任务后，设备符合性合作伙伴会向 Intune 发送设备状态详细信息。 然后，Intune 会将此信息添加到 Azure AD。 例如，具有不符合状态的设备会将该状态添加到 Azure AD 中的其设备记录中。

然后系统将通过条件访问策略评估符合性状态，与 Intune 托管设备的符合性状态数据相同。  默认情况下，Intune 是 iOS 和 Android 的已注册符合性合作伙伴。 添加其他合作伙伴时，可以设置优先级顺序，以确保正确的合作伙伴可管理设备以满足你的业务需求。

## <a name="supported-device-compliance-partners"></a>支持的设备符合性合作伙伴

公共预览版中：

- VMware Workspace ONE UEM (formerly AirWatch)

## <a name="prerequisites"></a>必备知识

- 订阅 Microsoft Intune，以及 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)的访问权限。

- 订阅设备符合性合作伙伴。

- 查看符合性合作伙伴的文档，了解受支持的设备平台和其他先决条件。

## <a name="configure-intune-to-work-with-a-device-compliance-partner"></a>将 Intune 配置为使用设备符合性合作伙伴

启用对设备合规性合作伙伴的支持，以将来自该合作伙伴的符合性状态数据用于条件访问策略。

### <a name="add-a-compliance-partner-to-intune"></a>将符合性合作伙伴添加到 Intune

1. 登录到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 转到“租户管理” > “连接器和令牌” > “合作伙伴符合性管理” > “添加符合性合作伙伴”   。

   > [!div class="mx-imgBorder"]
   > ![添加设备符合性合作伙伴](./media/device-compliance-partners/add-compliance-partner.png)

3. 在“基本信息”页上，展开“符合性合作伙伴”下拉列表，然后选择要添加的合作伙伴 。

   - 若要将 VMware Workspace ONE 作为 iOS 或 Android 平台的合规性合作伙伴，请选择 **“VMware Workspace ONE 移动版合规性”** 。

   接下来，选择“平台”的下拉列表，然后选择“平台”。 macOS 无法与此预览配合使用。

   即使已将多个符合性合作伙伴添加到 Azure AD，也只能对每个平台使用一个合作伙伴。

4. 在“分配”上，选择具有由此合作伙伴管理的设备的用户组。 使用此分配，你将更改适用设备的 MDM 机构以使用此合作伙伴。 另外，具有合作伙伴管理的设备的用户必须分配 Intune 许可证。

5. 在“查看 + 创建”页上，查看你的所选内容，然后选择“创建”以完成此配置 。

你的配置现在显示在“合作伙伴符合性管理”页上。

### <a name="modify-the-configuration-for-a-compliance-partner"></a>修改符合性合作伙伴的配置

1. 登录到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 转到“租户管理” > “连接器和令牌” > “合作伙伴符合性管理”，然后选择要修改的合作伙伴配置  。 配置按平台类型排序。

3. 在合作伙伴配置“概述”页上，选择“属性”以打开你可在其中编辑分配的“属性”页 。

4. 在“属性”页上，选择“编辑”以打开“分配”视图，你可在其中更改将使用此配置的组 。

5. 选择“查看 + 保存”，然后选择“保存”以保存你的编辑 。

6. *仅当使用 VMware Workspace ONE 时，此步骤才适用*：

   从 Workspace ONE UEM 控制台中，必须手动同步在 Microsoft Endpoint Manager 管理中心中保存的更改。 在手动同步更改之前，Workspace ONE UEM 无法识别配置更改，已分配的新组中的用户不会成功报告合规性。

   若要手动从 Azure 服务同步，请执行以下步骤：
   1. 登录到 VMware Workspace ONE UEM console。
   2. 转到 **“设置”**  >  **“系统”**  >  **“企业集成”**  >  **“目录服务”** 。
   3. 对 *“同步 Azure 服务”* ，单击 **“同步”** 。

      自初始配置或上次手动同步以来所做的所有更改都将从 Azure 服务同步到 UEM。  

## <a name="configure-your-compliance-partner-to-work-with-intune"></a>将符合性合作伙伴配置为使用 Intune

要使设备符合性合作伙伴能够使用 Intune，必须完成特定于该合作伙伴的配置。 有关此任务的信息，请参阅适用的合作伙伴的文档：

- [VMware Workspace ONE UEM](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/services/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)  

## <a name="enroll-your-ios-or-android-devices-to-that-device-compliance-partner"></a>将 iOS 或 Android 设备注册到该设备符合性合作伙伴

请参阅设备符合性合作伙伴文档，了解如何向该合作伙伴注册设备。 注册设备并向合作伙伴提交符合性数据后，该符合性数据将转发到 Intune 并添加到 Azure AD。

## <a name="monitor-devices-managed-by-third-party-device-compliance-partners"></a>监视由第三方设备符合性合作伙伴管理的设备

配置第三方设备符合性合作伙伴并向其注册设备后，合作伙伴会将符合性详细信息转发给 Intune。 在 Intune 接收到该数据后，你可以在 Azure 门户中查看设备的详细信息。

登录到 Azure 门户，然后转到 **“Azure AD”**  >  **“设备”**  > [ **“所有设备”** ](https://portal.azure.com/#blade/Microsoft_AAD_Devices/DevicesMenuBlade/Devices/menuId/)。

## <a name="next-steps"></a>后续步骤

使用第三方合作伙伴提供的文档为设备创建合规性策略。

- [VMware Workspace ONE UEM](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/services/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)
