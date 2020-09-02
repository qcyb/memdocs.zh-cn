---
title: Windows Holographic for Business 共享设备设置 - Microsoft Intune - Azure | Microsoft Docs
description: 添加并使用 Windows Holographic for Business 来配置由 Microsoft Intune 中多个用户共享或使用的设备。 查看帐户管理设置列表及其对设备（包括 Microsoft HoloLens）的效果。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
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
ms.openlocfilehash: 88b7f41b873697a7ec34bd1fc2f1098384ab1c18
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915715"
---
# <a name="windows-holographic-for-business-settings-to-manage-shared-devices-using-intune"></a>Windows Holographic for Business 设置，用于管理使用 Intune 的共享设备

Windows Holographic for Business 设备（如 Microsoft HoloLens）可以由多个用户使用。 具有多个用户的设备称为共享设备，是移动设备管理 (MDM) 解决方案的一部分。

通过 Microsoft Intune，用户可以使用来宾帐户登录到这些共享设备。 用户使用设备时，只能访问你允许访问的功能。

本文列出并介绍用于 Windows Holographic for Business 设备配置文件的设置。 在 Intune 中创建配置文件时，可以将配置文件部署或分配到贵组织中的设备组。 还可以将此配置文件分配到具有混合设备类型和操作系统版本的设备组。

有关 Intune 中此功能的详细信息，请参阅[控制共享电脑或多用户设备上的访问权限、帐户和电源功能](shared-user-device-settings.md)。 有关 Windows CSP 的详细信息，请参阅 [AccountManagement CSP](/windows/client-management/mdm/accountmanagement-csp)。

## <a name="before-your-begin"></a>准备工作

[创建 Windows 10 共享多用户设备配置文件](shared-user-device-settings.md)。

创建 Windows 10 共享用户设备配置文件时，设置数超过了本文所列的设置数。 Windows Holographic for Business 设备支持本文中的设置。

## <a name="shared-multi-user-device-settings"></a>共享的多用户设备设置

> [!NOTE]
> 运行 Windows Holographic for Business 的设备（包括 Microsoft HoloLens）仅支持“帐户管理”设置。 如果配置 Intune 中显示的任何其他设置（包括“共享电脑模式”），不会对这些设备造成任何影响。

- **帐户管理**：选择是否自动删除帐户。 选项包括：
  - **未配置**（默认）：自动删除来宾创建的帐户以及 AD 和 Azure AD 中的帐户。 用户注销设备或运行系统维护时，也会删除这些帐户。

    此外请输入：

    - **帐户删除**：选择删除帐户的时间：
      - **达到存储空间阈值**
      - **达到存储空间阈值和非活动时间阈值**
      - **注销后立即**

    此外请输入：

    - **开始删除阈值(%)** ：输入磁盘空间的百分比 (0-100)。 总磁盘/存储空间低于输入的值时，删除缓存的帐户。 不断删除帐户以回收磁盘空间。 首先删除处于非活动状态时间最长的帐户。
    - **停止删除阈值(%)** ：输入磁盘空间的百分比 (0-100)。 总磁盘/存储空间达到输入的值时，停止删除缓存的帐户。

  - **禁用**：来宾创建的本地、AD 和 Azure AD 帐户保留在设备上，不会被删除。

## <a name="next-steps"></a>后续步骤

- [分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。
- 请参阅 [Windows 10 及更高版本](shared-user-device-settings-windows.md)的共享用户设备设置。