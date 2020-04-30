---
title: 在 Microsoft Intune 中使用 Windows 更新的更新符合性报告
titleSuffix: Microsoft Intune
description: 使用 OMS 更新符合性查看向 Intune 部署的 Windows 更新的报告数据。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 157c61e9f145295f5ef728d12385fa44697a88e2
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81725643"
---
# <a name="intune-compliance-reports-for-updates"></a>Intune 的更新符合性报告

使用 Intune 将 Windows 更新部署到 Windows 10 设备时，请使用 Intune 或名为“更新符合性”的免费解决方案查看有关更新符合性的详细信息  。 更新符合性是 Microsoft Operations Management Suite (OMS) 的一部分。

## <a name="use-intune"></a>使用 Intune

查看已配置的 Windows 10 更新通道的部署状态策略报告：

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“设备”   > “概述”   > “软件更新状态”  。 可查看有关已分配的任意更新通道状态的一般信息。

3. 若要查看更多详细信息，请选择“监视器”  。 然后，在“软件更新”  下，选择“每个更新通道部署状态”  并选择要查看的部署通道。

   在“监视”部分，从下列报表中进行选择以查看有关更新通道的更详细信息： 

   - **设备状态** - 这将显示设备配置状态，有关详细信息，请参阅[更新 deviceConfigurationDeviceStatus]( https://docs.microsoft.com/graph/api/intune-deviceconfig-deviceconfigurationdevicestatus-update?view=graph-rest-1.0)。

   - **用户状态** - 这将显示用户名、状态和上次报告日期，有关详细信息，请参阅[列出 deviceConfigurationUserStatuses](https://docs.microsoft.com/graph/api/intune-deviceconfig-deviceconfigurationuserstatus-list?view=graph-rest-1.0)。

   - **最终用户更新状态** - 这将显示 Windows 设备更新状态，有关详细信息，请参阅 [windowsUpdateState](https://docs.microsoft.com/graph/api/resources/intune-shared-windowsupdatestate?view=graph-rest-beta)。

## <a name="use-update-compliance"></a>使用更新符合性

可使用[更新符合性](https://technet.microsoft.com/itpro/windows/manage/update-compliance-monitor)监视 Windows 10 更新的推出情况。 更新符合性通过 Azure 门户提供，满足其[先决条件](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started#update-compliance-prerequisites)的设备可免费使用。  

使用此解决方案时，可将商业 ID 部署到要报告其更新符合性且由 Intune 托管的任意 Windows 10 设备上。  

在 Intune 中，使用自定义策略的 OMA-URI 设置来配置商业 ID。 请参阅[在 Intune 中使用适用于 Windows 10 设备的自定义设置](../configuration/custom-settings-windows-10.md)。

用于配置商业 ID 的 OMA-URI（区分大小写）路径为：./Vendor/MSFT/DMClient/Provider/MS DM Server/CommercialID 

例如，你可以在“**添加或编辑 OMA-URI 设置**”中使用以下值：

- **设置名称**：Windows Analytics 商业 ID
- **设置说明**：为 Windows Analytics 解决方案配置商业 ID
- OMA-URI（区分大小写）：./Vendor/MSFT/DMClient/Provider/MS DM Server/CommercialID  
- **数据类型**：字符串
- **值**：\<使用 OMS 工作区中 Windows 遥测选项卡上显示的 GUID>

> [!NOTE]
> 有关 MS DM 服务器的详细信息，请参阅 [DMClient 配置服务提供程序 (CSP)]( https://docs.microsoft.com/windows/client-management/mdm/dmclient-csp)。

## <a name="next-steps"></a>后续步骤

[管理 Intune 中的软件更新](windows-update-for-business-configure.md)
