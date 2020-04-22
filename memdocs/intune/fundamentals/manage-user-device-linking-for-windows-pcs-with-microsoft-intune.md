---
title: 管理 Windows 电脑的用户设备链接
titleSuffix: Microsoft Intune
description: 如何将用户链接到 Intune 管理的 Windows 电脑。
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/01/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid: 53c99d63-c312-442a-8a71-de1b10fcd39b
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: 72b816938e803b28a06d3975f062f105d4c6a1cc
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "79358736"
---
# <a name="manage-user-device-linking-for-windows-pcs"></a>管理 Windows 电脑的用户设备链接

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

本主题中的信息仅适用于通过使用 Intune 软件客户端作为电脑进行管理的 Windows 桌面。 

必须将用户链接到计算机，然后才能将软件部署到用户。 可将某个用户链接到多台计算机，但每台计算机只能链接到一个用户。 用户会自动链接到他们使用公司门户在 Intune 中注册的任何计算机。

有关设备的主要用户的详细信息，请参阅[查找主要用户](../remote-actions/find-primary-user.md)。

若要将用户链接到计算机：

1. 在 [Microsoft Intune 管理控制台](https://manage.microsoft.com/)中，选择“组”&gt;“所有设备”（或包含需链接到用户的计算机的另一个组）   。

2. 选择要链接用户的计算机，然后选择“链接用户”  。

   “链接用户”  对话框显示可用用户的列表、其显示名称、用户 ID 和每个用户当前链接到的计算机的数量。 如果用户已链接到所选计算机，则该用户的名称和用户 ID 会显示在“当前用户”  下面。 如果计算机未链接到任何用户，则“当前用户”  下面将显示“无用户”  。

3. 执行以下操作之一：

   - 若要使计算机与其当前用户（如果存在当前用户）链接，请选择“取消”  。

   - 若要删除指向当前用户的链接（如果有），请选择“删除链接”&gt;“确定”  。

   - 若要将计算机链接到新用户，请在“所有用户”  列表中，选择用户。 确认用户数据正确，然后选择**确定**。

> [!TIP]
> 如果想要限制最终用户将自己链接到计算机的能力，则启用“Microsoft Intune 代理设置”  策略中的“限制用户将自己链接到计算机的能力”  选项。

## <a name="see-also"></a>另请参阅

[使用 Intune 软件客户端的常见 Windows 电脑管理任务](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)
