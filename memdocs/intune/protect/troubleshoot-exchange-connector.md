---
title: Exchange Connector 疑难解答
titleSuffix: Microsoft Intune
description: 解决与 Intune On-premises Exchange Connector 相关的问题。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: a7e3c742-295b-40bb-9afa-17f243062500
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 57a7b232b7391d6b8716d4c2a56d69b44f6c07ee
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914746"
---
# <a name="troubleshoot-the-intune-exchange-connector"></a>Intune Exchange Connector 疑难解答

本文介绍如何解决与 Intune Exchange Connector 相关的问题。

> [!IMPORTANT]
>
> 从 2020 年 7 月开始，已弃用对 Exchange Connector 的支持，并已替换为 Exchange [新式混合身份验证](/office365/enterprise/hybrid-modern-auth-overview) (HMA)，此外，还删除了将 Exchange Connector 添加到 Intune 的功能。
>
> 以前配置和使用 Exchange Connector 的客户继续获得该连接器支持。


## <a name="before-you-start"></a>开始之前

在开始排查 Intune 中的 Exchange Connector 问题之前，请收集一些基本信息，为进一步操作打下坚实的基础。 此方法可帮助你更好地了解问题的性质，并更快地解决问题。

- 验证你的进程是否满足安装要求。 请参阅[设置本地 Intune Exchange 连接器](exchange-connector-install.md)。
- 验证你的帐户是否具有 Exchange 和 Intune 管理员权限。
- 请注意完整和确切的错误消息文本、详细信息和显示消息的位置。
- 确定问题的开始时间： 
  - 是否首次设置连接器？ 
  - 连接器是先运行正常，然后才失败的吗？
  - 如果连接器正常，Intune 环境、Exchange 环境或运行连接器软件的计算机上发生了哪些更改？
- 什么是 MDM 机构？
- 使用哪种版本的 Exchange？

### <a name="use-powershell-to-get-more-data-on-exchange-connector-issues"></a>使用 PowerShell 获取有关 Exchange Connector 问题的更多数据

- 若要获取某个邮箱的所有移动设备的列表，请使用 `Get-ActiveSyncDeviceStatistics -mailbox mbx`
- 若要获取某个邮箱的 SMTP 地址的列表，请使用 `Get-Mailbox -Identity user | select emailaddresses | fl`
- 若要获取有关设备的访问状态的详细信息，请使用 `Get-CASMailbox <upn> | fl`

## <a name="review-the-connector-configuration"></a>查看连接器配置

查看[本地 Exchange Connector 要求](exchange-connector-install.md#intune-exchange-connector-requirements)确保正确配置环境和连接器。 

### <a name="general-considerations-for-the-connector"></a>连接器的一般注意事项

- 确保你的防火墙和代理服务器允许在托管 Intune Exchange Connector 和 Intune 服务的服务器之间进行通信。

- 托管 Intune Exchange Connector 和 Exchange 客户端访问服务器 (CAS) 的计算机应已加入域且位于同一 LAN 上。 请确保为 Intune Exchange Connector 使用的帐户添加所需的权限。

- 用于检索自动发现设置的通知帐户  。 有关 Exchange 中自动发现的详细信息，请参阅 [Exchange Server 中的自动发现服务](/exchange/architecture/client-access/autodiscover?view=exchserver-2016)。

- Intune Exchange Connector 使用通知帐户凭据向 EWS URL 发送“发送通知电子邮件与‘入门’链接（用于在 Intune 中注册）”的请求  。 使用“入门”链接注册是 Android 非 Knox 设备的一项要求  。 否则，条件访问将阻止这些设备。

### <a name="common-issues-for-connector-configurations"></a>连接器配置的常见问题

- **帐户权限**：在“Microsoft Intune Exchange Connector”对话框中，请确保已指定具有执行[必需 Windows PowerShell Exchange cmdlet](exchange-connector-install.md#exchange-cmdlet-requirements) 的相应权限的用户帐户。
- **通知电子邮件**：启用通知并指定通知帐户。
- **客户端访问服务器同步**：配置 Exchange Connector 时，指定与托管 Exchange Connector 的服务器之间延迟尽可能低的 CAS。 CAS 和 Exchange Connector 间的通信延迟可能导致设备发现延迟，尤其是在使用 Exchange Online Dedicated 时。
- **同步计划**：使用新注册设备的用户可能会在获取访问权限时遇到延迟，直到 Exchange Connector 与 Exchange CAS 同步。 完全同步一天进行一次，而增量（快速）同步每天进行多次。 可以[手动强制执行快速同步或完全同步](exchange-connector-install.md#manually-force-a-quick-sync-or-full-sync)以尽量减少延迟。

## <a name="next-steps"></a>后续步骤
以下文章可帮助解决常见问题和特定错误：

- [解决 Intune Exchange Connector 常见问题](troubleshoot-exchange-connector-common-problems.md)。
- [解决 Intune Exchange Connector 常见错误](troubleshoot-exchange-connector-common-errors.md)。

寻求支持或 Intune 社区的帮助：

- 请参阅[获取支持](../fundamentals/get-support.md)以使用 Intune 控制台帮助排查问题或打开 Microsoft 的支持案例。 
- 请在 [Microsoft Intune 论坛](/answers/products/mem)发布问题。  
