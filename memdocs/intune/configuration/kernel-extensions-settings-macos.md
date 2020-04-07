---
title: Microsoft Intune 中的 macOS 内核扩展设置 - Azure | Microsoft Docs
titleSuffix: ''
description: 在 macOS 设备上添加、配置或创建设置可使用内核扩展。 此外，允许用户覆盖已批准的扩展、允许来自团队标识符的所有扩展或是允许 Microsoft Intune 中的特定扩展或应用。
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
ms.openlocfilehash: 2e18fad8f1112681a62bcdacd63c652cfd4ad3ac
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359282"
---
# <a name="macos-device-settings-to-configure-and-use-kernel-extensions-in-intune"></a>用于在 Intune 中配置和使用内核扩展的 macOS 设备设置

本文列出并介绍了可以在 macOS 设备上控制的各种内核扩展设置。 作为移动设备管理 (MDM) 解决方案的一部分，使用这些设置可在设备上添加和管理内核扩展。

若要详细了解 Intune 中的内核扩展以及任何先决条件，请参阅[添加 macOS 内核扩展](kernel-extensions-overview-macos.md)。

我们将这些设置添加到 Intune 中的设备配置配置文件中，然后分配或部署到 macOS 设备。

## <a name="before-you-begin"></a>在开始之前

[创建设备内核扩展配置文件](kernel-extensions-overview-macos.md)。

> [!NOTE]
> 这些设置适用于不同的注册类型。 有关不同注册类型的详细信息，请参阅 [macOS 注册](../enrollment/macos-enroll.md)。

## <a name="kernel-extensions"></a>内核扩展

### <a name="settings-apply-to-user-approved-automated-device-enrollment"></a>设置适用范围：用户批准、自动化的设备注册

- 允许用户覆盖  ：“允许”  使用户可以批准配置文件中未包含的内核扩展。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能会阻止用户允许未包含在配置文件中的扩展。 即，只允许使用配置文件中包含的扩展。

  有关此功能的详细信息，请参阅[用户批准的内核扩展加载](https://developer.apple.com/library/archive/technotes/tn2459/_index.html)（打开 Apple 网站）。

- 允许的团队标识符  ：使用此设置可允许使用一个或多个团队 ID。 允许使用并信任使用输入的团队 ID 签名的任何内核扩展。 换句话说，使用此选项可允许使用采用相同团队 ID（可能是特定开发人员或合作伙伴）的所有内核扩展。

  “添加”  要加载的有效且已签名内核扩展的团队标识符。 可以添加多个团队标识符。 团队标识符必须是字母数字（字母和数字）并且包含 10 个字符。 例如，输入 `ABCDE12345`。

  添加团队标识符之后，还可以删除它。

  [找到你的团队 ID](https://help.apple.com/developer-account/#/dev55c3c710c)（打开 Apple 网站）提供了详细信息。

- 允许的内核扩展  ：使用此设置可允许使用特定内核扩展。 仅允许使用或信任输入的内核扩展。

  “添加”  要加载的内核扩展的捆绑标识符和团队标识符。 对于未签名的旧内核扩展，使用空团队标识符。 可以添加多个内核扩展。 团队标识符必须是字母数字（字母和数字）并且包含 10 个字符。 例如，对于“捆绑 ID”  输入 `com.contoso.appname.macos`，对于“团队标识符”  输入 `ABCDE12345`。

  > [!TIP]
  > 若要在 macOS 设备上获取内核扩展 (Kext) 的捆绑 ID，可以执行以下操作：
  >
  > 1. 在终端中，运行 `kextstat | grep -v com.apple`，并记下输出。 安装所需的软件或 Kext。 再次运行 `kextstat | grep -v com.apple`，并查找更改。
  >
  >    在终端中，`kextstat` 会列出操作系统上的所有内核扩展。 
  >
  > 2. 在设备上，打开 Kext 的信息属性列表文件 (Info.plist)。 将显示捆绑 ID。 每个 Kext 都在内部存储一个 Info.plist 文件。

> [!NOTE]
> 无需添加团队标识符和内核扩展。 可以配置一个或另一个。

## <a name="next-steps"></a>后续步骤

[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。
