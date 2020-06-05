---
title: Microsoft Intune 中的共享或多用户设备设置 - Azure | Microsoft Docs
description: 添加并使用由 Microsoft Intune 中多个用户共享或使用的 Windows 10 和 Windows Holographic for Business 设备。 查看所有设置的列表以及这些设置对设备（包括 Microsoft HoloLens）的效果。 控制来宾帐户、管理帐户和删除非活动帐户、允许或阻止保存到本地存储、设置电源和睡眠选项、选择安装更新的时间，并在设备配置文件的教育环境中使用设备。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4f85c30c9472849d26802c8cdccd7a95006a3e4a
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2020
ms.locfileid: "83984007"
---
# <a name="control-access-accounts-and-power-features-on-shared-pc-or-multi-user-devices-using-intune"></a>使用 Intune 控制共享电脑或多用户设备上的访问权限、帐户和电源功能

具有多个用户的设备称为共享设备，是移动设备管理 (MDM) 解决方案的常见部分。 使用 Microsoft Intune，可以自定义运行以下平台的共享设备：

- Windows 10 专业版和更高版本
- Windows 10 企业版和更高版本
- Windows Holographic for Business，例如 HoloLens

例如，学校拥有许多通常由学生使用的设备。 使用此设置，学校 Intune 管理员可启用共享电脑功能，一次允许一个用户。 学生在设备上不能在不同登录帐户之间切换。 如果学生注销，你还可以选择删除所有用户特定的设置。

最终用户可以使用来宾帐户登录到这些共享设备。 用户登录后，系统会缓存凭据。 最终用户使用设备时，只能访问你允许访问的功能。 例如，你可以进行如下设置：选择设备何时进入睡眠模式，用户是否可以在本地查看和保存文件，启用或禁用电源管理设置等。 此外，还可控制用户注销时是否删除来宾帐户，或达到阈值时是否删除非活动帐户。

本文介绍如何创建配置文件，并包括指向可用设置及其说明的链接。

在 Intune 中创建配置文件时，可以将配置文件部署或分配到贵组织中的设备组。 还可以将此配置文件分配给具有混合设备类型和操作系统 (OS) 版本的设备组。

## <a name="create-the-profile"></a>创建配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备” > “配置文件” > “创建配置文件”。
3. 输入以下属性：

   - **平台**：选择“Windows 10 及更高版本”。
   - **配置文件**：选择“共享的多用户设备”。

4. 选择“创建”。
5. 在“基本信息”中，输入以下属性：

   - **名称**：输入新配置文件的描述性名称。
   - **描述**：输入配置文件的说明。 此设置是可选的，但建议进行。

6. 选择“下一步”。
7. 在“配置设置”中，根据所选择的平台，可配置的设置有所不同。 选择平台，以了解详细设置：

    - [Windows 10 及更高版本](shared-user-device-settings-windows.md)
    - [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md)

8. 选择“下一步”。

9. 在“作用域标记”（可选）中，分配一个标记以将配置文件筛选到特定 IT 组（如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`）。 有关范围标记的详细信息，请参阅[将 RBAC 和范围标记用于分布式 IT](../fundamentals/scope-tags.md)。

    选择“下一步”。

10. 在“分配”中，选择将接收配置文件的设备组。 有关分配配置文件的详细信息，请参阅[分配用户和设备配置文件](device-profile-assign.md)。

    选择“下一步”。

    > [!NOTE]
    > 请务必向组织中的设备组分配配置文件。

11. 在“查看并创建”中查看设置。 选择“创建”时，将保存所做的更改并分配配置文件。 该策略也会显示在配置文件列表中。

每台设备在下次签入时，将应用该策略。

## <a name="next-steps"></a>后续步骤

- 请参阅 [Windows 10 及更高版本](shared-user-device-settings-windows.md)和 [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md) 的所有设置。
- [分配配置文件](device-profile-assign.md)之后，[监视其状态](device-profile-monitor.md)。
