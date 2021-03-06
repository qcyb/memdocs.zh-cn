---
title: 远程协助由 Intune 托管的移动设备
description: 可以使用四个不同的选项来远程协助用户使用其移动设备。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b501ab979d87461067018f789d6d096020d3819e
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057413"
---
# <a name="remotely-assist-mobile-devices-managed-by-microsoft-endpoint-manager"></a>远程协助由 Microsoft 终结点管理器管理的移动设备

提供四个选项来远程管理由 Microsoft 终结点管理器管理的设备：

- [Microsoft Teams](https://products.office.com/microsoft-teams/) 是团队合作的中心，无论你身在何处，都可以通过它来聊天、开会和协作。
- [快速助手](https://support.microsoft.com/help/4027243/windows-10-solve-pc-problems-with-quick-assist)是一款 Windows 10 应用程序，允许两个人通过远程连接共享设备。
- [TeamViewer](https://www.teamviewer.com/) 是需另行购买的第三方程序。 它提供了一组全面的远程访问和支持功能。 Intune 和 [TeamViewer 集成](teamviewer-support.md)支持使用 TeamViewer 进行远程支持，并且可以直接在 Intune 中管理连接器。
- [远程控制](/configmgr/core/clients/manage/remote-control/introduction-to-remote-control)包含在 Microsoft Endpoint Configuration Manager 中。 它用于远程管理、提供协助或查看任何工作组计算机和加入域的计算机。

| 功能、平台和许可 | **Teams** | 快速助手 | TeamViewer (Intune) | 远程控制 (ConfigMgr) |
|:---:|:---:|:---:|:---:|:---:|
| 远程视图和控制 |![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|
| 聊天 |![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)||![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)||
| 文件传输 |![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|
| 提升的管理员访问权限 |||![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|
| 无人参与访问 |||![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|
| 同时远程控制 |![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| 多用户支持 |||![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|
| 远程操作 ||![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|
| 通过 Internet 提供支持 |![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)||
| 审核报告 |![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)||![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|
| 支持所有平台（Windows、iOS、Android、macOS） |![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)||![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)||
| 与 Windows 10 集成 – 无需其他应用 ||![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| 要求设备由 Configuration Manager 和 Intune 共同管理 ||||![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|
| 需要额外的许可\* |![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)||![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|![选中标记](../enrollment/media/enrollment-method-capab/checkmark.png)|

\* Teams 需要 Microsoft 365 许可。 若要使用 TeamViewer 和 Intune，需要获得 TeamViewer 和 Intune 的许可。 远程控制是 Configuration Manager 的一项功能，需要获得 Configuration Manager 许可。
