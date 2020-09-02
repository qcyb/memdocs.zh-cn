---
title: Microsoft Intune 中的 Windows 10 教育设置 - Azure | Microsoft Docs
description: 查看所有适用于 Windows 10 设备的教育设置的列表。 在设备配置文件中结合使用这些设置和“参加测验”应用，在 Intune 中选择用户或学生登录方式、在测验期间监视屏幕等。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/03/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: kakyker
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2c6648f66c585dac5b8913fdb13adfcb98cbf927
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88912689"
---
# <a name="configure-the-take-a-test-app-on-windows-10-devices-using-intune"></a>使用 Intune 在 Windows 10 设备上配置“参加测验”应用

使用“参加测验”应用，你可以在课堂的 Windows 10 设备上安全地管理在线测试。 若要设置“参加测验”应用，你需要在 Intune 中创建设备配置文件，并配置安全评估设置。 本文介绍了“参加测试”应用的设置。 

配置了配置文件后，请将其分配给学生并进行部署。 

[Intune 中的“参加测验”应用](education-settings-configure.md)提供了此功能的详细信息。

## <a name="before-you-begin"></a>在开始之前

[创建设备配置文件](education-settings-configure.md#create-a-device-profile)。

## <a name="take-a-test-settings"></a>“参加测验”设置

- **帐户类型**：选择用户登录测验的方式。 选项包括：
  - Azure AD 帐户
  - 域帐户
  - 本地帐户
  - 本地来宾帐户：仅在运行 Windows 10 版本 1903 及更高版本的设备上可用。
- **帐户用户名**：输入用于“参加测验”应用的帐户的用户名。 可以按如下格式输入帐户：
  - `user@contoso.com`
  - `domain\username`
  - `user@contoso.com`
  - `computerName\username`
- **帐户名**：要设置本地来宾帐户类型，请输入“参加测试”应用使用的帐户名称。 帐户名称将在登录屏幕上以磁贴形式显示。 学生单击磁贴即可启动测试。  
- **评估 URL**：输入希望用户参加的测验的 URL。 若要详细了解如何获取 URL，请参阅[“参加测验”文档](/education/windows/take-tests-in-windows-10)。
- **打印机连接**：“需要”仅允许从连接到打印机的设备访问“参加测验”应用。 此设置还使应试者可以使用应用的“打印”按钮。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 默认情况下，OS 可允许学生从未连接到打印机的设备访问应用。  
- **屏幕监视**：“允许”可在用户参加测验时监视屏幕活动。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 默认情况下，OS 可能会阻止你在测验期间监视屏幕。
- **文本建议**：选择“允许”可向测验者显示文本建议。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置。 默认情况下，OS 可能会在用户执行测验时阻止文本建议。

## <a name="next-steps"></a>后续步骤

[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。

详细了解[“参加测验”应用](education-settings-configure.md)。