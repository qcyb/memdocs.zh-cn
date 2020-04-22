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
ms.openlocfilehash: 39f881b05c9698a8560fe009331fac3389b35bde
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "79364287"
---
# <a name="configure-the-take-a-test-app-on-windows-10-devices-using-intune"></a>使用 Intune 在 Windows 10 设备上配置“参加测验”应用

使用“参加测验”应用，你可以在课堂的 Windows 10 设备上安全地管理在线测试。 若要设置“参加测验”应用，你需要在 Intune 中创建设备配置文件，并配置安全评估设置。 本文介绍了“参加测试”应用的设置。 

配置了配置文件后，请将其分配给学生并进行部署。 

[Intune 中的“参加测验”应用](education-settings-configure.md)提供了此功能的详细信息。

## <a name="before-you-begin"></a>在开始之前

[创建设备配置文件](education-settings-configure.md#create-a-device-profile)。

## <a name="take-a-test-settings"></a>“参加测验”设置
创建设备配置文件后，转到“配置文件类型”，并选择“安全评估(教育)”   。 你将看到以下“参加测试”应用设置。 


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
- **评估 URL**：输入希望用户参加的测验的 URL。 若要详细了解如何获取 URL，请参阅[“参加测验”文档](https://docs.microsoft.com/education/windows/take-tests-in-windows-10)。
- **打印机连接**：选择“需要”以仅允许从连接到打印机的设备访问“参加测试”应用  。 此设置还使应试者可以使用应用的打印按钮。 如果选择“未配置”，则允许学生从未连接到打印机的设备访问应用  。  
- **屏幕监视**：选择“允许”  可在用户参加测验时监视屏幕活动。 如果选择“未配置”  ，便无法在测验期间监视屏幕。
- **文本建议**：选择“允许”  可向测验者显示文本建议。 如果选择“未配置”  ，便无法向正在参加测验的用户显示文本建议。

## <a name="next-steps"></a>后续步骤

请务必[分配配置文件](device-profile-assign.md)，并[监视配置文件状态](device-profile-monitor.md)。
