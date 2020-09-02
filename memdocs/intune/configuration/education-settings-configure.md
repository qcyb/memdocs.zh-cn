---
title: 在 Microsoft Intune 中添加或配置教育设置 - Azure | Microsoft Docs
description: 在 Microsoft Intune 中 Windows 10 及更高版本设备上的设备配置文件中使用“参加测验”应用。 使用教育版设置创建配置文件，输入测试应用 URL，选择用户登录方式，在测试期间监视屏幕，以及在测试期间允许或阻止文本建议。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7b1a605e456edb525afec306ff594ba7cc3895aa
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88912723"
---
# <a name="use-the-take-a-test-app-on-windows-10-devices-in-microsoft-intune"></a>在 Microsoft Intune 中的 Windows 10 设备上使用“参加测验”应用

Intune 中的教育配置文件专为学生在设备上参加测验或考试而设计。 此功能包含“参加测验”应用，以及用于添加测验 URL、选择最终用户的测验登录方式等的设置。 此功能支持以下平台：

- Windows 10 及更高版本

在用户登录后，“参加测验”应用自动打开，并显示所输入的测验。 正在参加测验时，无法在设备上运行其他任何应用。 [Windows 10 中的“参加测验”](/education/windows/take-tests-in-windows-10)详细介绍了“参加测验”应用。

本文列出了在 Microsoft Intune 中创建设备配置文件的步骤。 其中还包括了解适用于 Windows 10 设备的教育设置所需的信息。

## <a name="create-a-device-profile"></a>创建设备配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备” > “配置文件” > “创建配置文件”。
3. 输入以下属性：

    - **平台**：选择“Windows 10 及更高版本”。
    - **配置文件**：选择“安全评估(教育)”。

4. 选择“创建”。
5. 在“基本信息”中，输入以下属性：

    - **名称**：输入新配置文件的描述性名称。
    - **描述**：输入配置文件的说明。 此设置是可选的，但建议进行。

6. 选择“下一步”。
7. 在“配置设置”中，输入要配置的设置：

    - [Windows 10 及更高版本](education-settings-windows.md)

8. 选择“下一步”。

9. 在“作用域标记”（可选）中，分配一个标记以将配置文件筛选到特定 IT 组（如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`）。 有关范围标记的详细信息，请参阅[将 RBAC 和范围标记用于分布式 IT](../fundamentals/scope-tags.md)。

    选择“下一步”。

10. 在“分配”中，选择要接收配置文件的用户或用户组。 有关分配配置文件的详细信息，请参阅[分配用户和设备配置文件](device-profile-assign.md)。

    选择“下一步”。

11. 在“查看并创建”中查看设置。 选择“创建”时，将保存所做的更改并分配配置文件。 该策略也会显示在配置文件列表中。

每台设备在下次签入时，将应用该策略。

## <a name="next-steps"></a>后续步骤

查看 [Windows 10 教育设置](education-settings-windows.md)及其说明的列表。

[分配配置文件](device-profile-assign.md)之后，[监视其状态](device-profile-monitor.md)。