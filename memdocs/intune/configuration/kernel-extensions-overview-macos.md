---
title: 使用 Microsoft Intune 创建 macOS 内核扩展配置文件 - Azure | Microsoft Docs
titleSuffix: ''
description: 添加或创建 macOS 设备配置文件，然后配置内核扩展，使其允许用户替代和添加团队标识符以及 Microsoft Intune 中的捆绑包和团队标识符。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8f9212d275b17db6a40e3133b5363cd13c9d13d6
ms.sourcegitcommit: 0ad7cd842719887184510c6acd9cdfa290a3ca91
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2020
ms.locfileid: "80551423"
---
# <a name="add-macos-kernel-extensions-in-intune"></a>使用 Intune 添加 macOS 内核扩展

> [!NOTE]
> macOS 内核扩展正在替换为系统扩展。 有关详细信息，请参阅[支持提示：在 Intune 中为 macOS Catalina 10.15 使用系统扩展而不是内核扩展](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413)。

在 macOS 设备上，可添加内核级功能。 这些功能可访问正常程序无法访问的 OS 部分。 组织可能具有应用、设备功能等无法满足的特定需求或要求。 

要添加始终允许在设备上加载的内核扩展，请使用 Microsoft Intune 添加“内核扩展”(KEXT)，然后将这些扩展部署到设备。

例如，你有一个病毒扫描程序，可扫描设备中是否存在恶意内容。 你可使用 Intune 将此病毒扫描程序的内核扩展添加为允许的内核扩展。 然后，向 macOS 设备分配该扩展。

利用此功能，管理员可以允许用户替代内核扩展，添加团队标识符，以及使用 Intune 添加特定内核扩展。

此功能适用于：

- macOS 10.13.2 及更高版本

要使用此功能，设备必须符合以下情况：

- 使用 Apple 设备注册计划 (DEP) 通过 Intune 进行注册。 如需了解详细信息，请参阅[自动注册 macOS 设备](../enrollment/device-enrollment-program-enroll-macos.md)。

  要么

- 使用 Intune 通过“已批准的用户注册”（Apple 的术语）进行注册 如需了解详细信息，请参阅[为 macOS High Sierra 中内核扩展的更改做好准备](https://support.apple.com/en-us/HT208019)（打开 Apple 网站）。

Intune 使用“配置文件”创建和自定义这些设置，从而满足组织需求。 在配置文件中添加这些功能后，就可以将配置文件推送或部署到组织的 macOS 设备上。

本文介绍如何通过 Intune 使用内核扩展创建设备配置文件。

> [!TIP]
> 有关内核扩展的详细信息，请参阅[内核扩展概述](https://developer.apple.com/library/archive/documentation/Darwin/Conceptual/KernelProgramming/Extend/Extend.html)（打开 Apple 网站）。

## <a name="what-you-need-to-know"></a>须知内容

- 可以添加未签名的旧版内核扩展。
- 请确保输入正确的团队标识符和内核扩展的捆绑包 ID。 Intune 不会验证输入的值。 如果输入的信息不正确，则该扩展将无法在设备上运行。 团队标识符长度正好为 10 个字母数字字符。 

> [!NOTE]
> Apple 发布了有关所有软件的签名和公证的信息。 在 macOS 10.14.5 和更新版本中，通过 Intune 部署的内核扩展不必满足 Apple 的公证策略。
>
> 有关此公证策略以及任何更新或更改的信息，请参阅以下资源：
>
> - [分发前对应用进行公证](https://developer.apple.com/documentation/security/notarizing_your_app_before_distribution)（打开 Apple 网站） 
> - [为 macOS High Sierra 中内核扩展的更改做好准备](https://support.apple.com/en-us/HT208019)（打开 Apple 网站）

> [!NOTE]
> Intune 用户界面 (UI) 正在更新为提供全屏体验，可能需要数周时间才能完成。 在租户收到此更新之前，创建或编辑本文所述的设置时的工作流将略有不同。

## <a name="create-the-profile"></a>创建配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备”   > “配置文件”   > “创建配置文件”  。
3. 输入以下属性：

    - **平台**：选择“macOS” 
    - **配置文件**：选择“扩展”  。

4. 选择“创建”。 
5. 在“基本信息”  中，输入以下属性：

    - **名称**：输入策略的描述性名称。 为策略命名，以便稍后可以轻松地识别它们。 例如，策略名称最好是“macOS：配置登录屏幕”**将内核扩展添加到设备**。
    - **描述**：输入策略的说明。 此设置是可选的，但建议进行。

6. 选择“下一步”  。

7. 在“配置设置”中，配置以下设置  ：

    - [macOS](kernel-extensions-settings-macos.md)

8. 选择“下一步”  。
9. 在“作用域标记”（可选）中，分配一个标记以将配置文件筛选到特定 IT 组（如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`）  。 有关范围标记的详细信息，请参阅[将 RBAC 和范围标记用于分布式 IT](../fundamentals/scope-tags.md)。

    选择“下一步”  。

10. 在“分配”中，选择将接收配置文件的用户或组  。 有关分配配置文件的详细信息，请参阅[分配用户和设备配置文件](device-profile-assign.md)。

    选择“下一步”  。

11. 在“查看并创建”中查看设置  。 选择“创建”时，将保存所做的更改并分配配置文件  。 该策略也会显示在配置文件列表中。

## <a name="next-steps"></a>后续步骤

创建配置文件后，即可进行分配。 下一步，[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。
