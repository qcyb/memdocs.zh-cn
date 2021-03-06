---
title: Microsoft 10 共享设备设置 - Microsoft Intune - Azure | Microsoft Docs
description: 添加并使用 Windows 10 来配置在 Microsoft Intune 中多个用户共享或使用的设备。 查看所有设置列表以及对设备（包括 Microsoft Surface）的效果。 控制来宾帐户、管理帐户和删除非活动帐户、允许或阻止保存到本地存储、设置电源和睡眠选项、选择安装更新的时间，并在设备配置文件的教育环境中使用设备。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d3a1a66988f922a293187f3ed30e3659dee567b1
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915698"
---
# <a name="windows-10-and-later-settings-to-manage-shared-devices-using-intune"></a>Windows 10 及更高版本设置，用于保护使用 Intune 的设备

Windows 10 及更高版本的设备（如 Microsoft Surface），可用于多个用户。 具有多个用户的设备称为共享设备，是移动设备管理 (MDM) 解决方案的一部分。

通过 Microsoft Intune，终端用户可使用来宾帐户登录这些共享设备。 用户使用设备时，只能访问你允许访问的功能。 作为 Intune 管理员，你可以为共享 Windows 10 设备配置访问权限、选择删除帐户的时间和控制电源管理设置等。

本文列出并介绍用于 Windows 10（及更高版本）设备配置文件的设置。 在 Intune 中创建配置文件时，可以将配置文件部署或分配到贵组织中的设备组。 还可以将此配置文件分配到具有混合设备类型和操作系统版本的设备组。

有关 Intune 中此功能的详细信息，请参阅[控制共享电脑或多用户设备上的访问权限、帐户和电源功能](shared-user-device-settings.md)。 有关 Windows CSP 的详细信息，请参阅 [SharedPC CSP](/windows/client-management/mdm/sharedpc-csp)。

## <a name="before-your-begin"></a>准备工作

[创建配置文件](shared-user-device-settings.md)。

## <a name="shared-multi-user-device-settings"></a>共享的多用户设备设置

这些设置使用 [SharedPC CSP](/windows/client-management/mdm/sharedpc-csp)。

- **共享电脑模式**：“启用”会打开共享电脑模式。 在此模式下，一次只能有一位用户登录设备。 第一位用户注销前，其他用户无法登录。设置为“未配置”（默认）时，Intune 不会更改或更新此设置。
- **来宾帐户**：选择此模式，在登录屏幕上创建来宾选项。 来宾帐户不需要任何用户凭证或身份验证。 此设置在每次使用时会创建新的本地帐户。 选项包括：
  - **来宾**：在本地设备上创建来宾帐户。
  - **域**：在 Azure Active Directory (AD) 中创建来宾帐户。
  - **来宾和域**：在本地设备上和 Azure Active Directory (AD) 中创建来宾帐户。
- **帐户管理**：选择是否自动删除帐户。 选项包括：
  - **未配置**（默认）：Intune 不会更改或更新此设置。
  - **启用**：自动删除来宾创建的帐户以及 AD 和 Azure AD 中的帐户。 用户注销设备或运行系统维护时，也会删除这些帐户。

    此外请输入：

    - **帐户删除**：选择删除帐户的时间：
      - **达到存储空间阈值**
      - **达到存储空间阈值和非活动时间阈值**
      - **注销后立即**

    此外请输入：

    - **开始删除阈值(%)** ：输入磁盘空间的百分比 (0-100)。 总磁盘/存储空间低于输入的值时，删除缓存的帐户。 不断删除帐户以回收磁盘空间。 首先删除处于非活动状态时间最长的帐户。
    - **停止删除阈值(%)** ：输入磁盘空间的百分比 (0-100)。 总磁盘/存储空间达到输入的值时，停止删除缓存的帐户。
    - **非活动帐户阈值**：请输入应在帐户连续多少天未登录后将其删除，范围是 0-60 天。

  - **已禁用**：来宾创建的本地、AD 和 Azure AD 帐户保留在设备上，不会被删除。

- **本地存储**：使用本地存储，用户可以保存并查看该设备的硬盘上的文件。 选项包括：
  - **未配置**（默认）：Intune 不会更改或更新此设置。
  - **启用**：阻止用户保存和查看设备硬盘上的文件。
  - **已禁用**：允许用户使用文件资源管理器查看和保存本地文件。

- **电源策略**：允许或阻止用户更改电源设置。 选项包括：
  - **未配置**（默认）：Intune 不会更改或更新此设置。
  - **启用**：用户不能关闭“休眠”、不能替代所有睡眠操作（比如合上设备盖），也不能更改电源设置。
  - **已禁用**：用户可以让设备进入休眠状态、可以合上设备盖让设备进入睡眠模式，也可以更改电源设置。

- **睡眠超时(秒)** ：输入设备进入休眠模式前的非活动状态秒数 (0-18000)。 `0` 表示设备永不休眠。 如果未设定秒数，设备会在 3600 秒（60 分钟）后进入睡眠状态。

- **电脑唤醒时登录**：选择在设备退出休眠模式后用户是否必须登录。 选项包括：
  - **未配置**（默认）：Intune 不会更改或更新此设置。
  - **启用**：在设备退出休眠模式时要求用户使用密码登录。
  - **已禁用**：用户无需输入其用户名和密码。

- **维护开始时间(从午夜开始计算的分钟数)** ：自动维护任务（如 Windows 更新）运行时，输入分钟数 (0-1440)。 默认开始时间为午夜，或零 (`0`) 分钟。 通过输入从午夜开始计算的开始时间（分钟数），更改开始时间。 例如，如果希望从凌晨 2 点开始维护，请输入 `120`。 如果希望从晚上 8 点开始维护，请输入 `1200`。

  设置为“未配置”（默认）时，Intune 不会更改或更新此设置。

- **教育策略**：选择是否启用教育环境策略。 选项包括：
  - **未配置**（默认）：Intune 不会更改或更新此设置。
  - **启用**：将更严格的推荐设置用于在学校使用的设备。
  - **已禁用**：不使用默认和推荐教育策略。

  有关教育策略作用的详细信息，请参阅[面向教育行业客户的 Windows 10 配置建议](/education/windows/configure-windows-for-education)。

> [!TIP]
> [设置共享或来宾电脑](/windows/configuration/set-up-shared-or-guest-pc)（打开另一个文档网站）是此 Windows 10 功能的出色资源，包括可在共享模式下设置的概念和组策略。

## <a name="next-steps"></a>后续步骤

- [分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。
- 请参阅 [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md) 的设置。