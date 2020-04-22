---
title: 配置适用于 Windows 10 的应用保护策略
titleSuffix: Microsoft Intune
description: 本主题介绍如何配置适用于 Windows 10 设备的应用保护策略 (APP)。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 949fddec-5318-4c9a-957e-ea260e6e05be
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: e7dcad93f836ee564e973555bebe1a1f5d7ba3c3
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "80323695"
---
# <a name="get-ready-for-windows-information-protection-in-windows-10"></a>为 Windows 10 中的 Windows 信息保护做准备 

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

通过在 Azure AD 中设置 MAM 提供程序为 Windows 10 启用移动应用程序管理 (MAM)。 通过在 Azure AD 中设置 MAM 提供程序，可以在使用 Intune 创建新的 Windows 信息保护 (WIP) 策略时定义注册状态。 注册状态可以是 MAM 或移动设备管理 (MDM)。

## <a name="to-configure-the-mam-provider"></a>配置 MAM 提供程序

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“所有服务”  ，然后选择“M365 Azure Active Directory”  以切换仪表板。
3. 选择 **Azure Active Directory**。
4. 选择“管理”  组中的“移动性(MDM 和 MAM)”  。
5. 单击“Microsoft Intune”  。
6. 配置“配置”  窗格上的“还原默认 MAM URL”  组中的设置。

   **MAM 用户范围**  
   使用 MAM 自动注册来管理员工的 Windows 设备上的企业数据。 将 MAM 自动注册配置为使用用户自己的设备方案。<ul><li>**无**<br>选择是否所有用户均不可在 MAM 中注册。</li><li>**部分**<br>选择包含将要在 MAM 中进行注册的用户的 Azure AD 组。</li><li>**全部**<br>选择是否所有用户均可在 MAM 中注册。</li></ul>

   **MAM 使用条款 URL**  
   Microsoft Intune 不支持 MAM 使用条款 URL。 必须将此输入框留空，以便应用保护策略。

   **MAM 发现 URL**  
   MAM 服务的注册终结点的 URL。 注册终结点用于使用 MAM 服务注册设备以进行管理。

   **MAM 符合性 URL**  
   Microsoft Intune 不支持 MAM 符合性 URL。 必须将此输入框留空，以便应用保护策略。 

7. 单击 **“保存”** 。

## <a name="next-steps"></a>后续步骤

[创建 WIP 策略](windows-information-protection-policy-create.md)
