---
title: 配置 Endpoint Protection
titleSuffix: Configuration Manager
description: 了解如何将 Configuration Manager 设置为更新和分发 Windows Defender 的恶意软件定义。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e48f20dd56f445a10faa485b8bb7e86dbb05f75a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704515"
---
# <a name="configure-endpoint-protection"></a>配置 Endpoint Protection

适用范围：  Configuration Manager (Current Branch)

必须先执行本文详细介绍的配置步骤，然后才能使用 Endpoint Protection 管理 Configuration Manager 客户端计算机上的安全性和恶意软件。  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>如何在 Configuration Manager 中配置 Endpoint Protection  
 Configuration Manager 中的 Endpoint Protection 具有外部依赖关系和产品内依赖关系。  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>在 Configuration Manager 中配置 Endpoint Protection 的步骤  
 使用下表来了解有关如何配置 Endpoint Protection 的步骤、详情及更多信息。  

> [!IMPORTANT]  
>  如果管理 Windows 10 计算机的 Endpoint Protection，则必须配置 Configuration Manager 以更新和分发 Windows Defender 的恶意软件定义。 虽然 Windows 10 中包含了 Windows Defender，但仍然必须安装 SCEPInstall，并且仍然需要自定义 Endpoint Protection 的客户端设置（下面的**步骤 5**） </br> </br>
> 从 Configuration Manager 1802 开始，Windows 10 设备无需安装 Endpoint Protection 代理 (SCEPInstall)。 如果已在 Windows 10 设备上安装该代理，Configuration Manager 也不会将其删除。 管理员可在运行最低 1802 客户端版本的 Windows 10 设备上删除 Endpoint Protection 代理。 SCEPInstall.exe 可能仍然存在于某些计算机上的 C:\Windows\ccmsetup 中，但不应在新客户端安装中下载它。 Endpoint Protection 的自定义客户端设置（下面的**步骤 5**）仍然是必需的。 <!--503654-->

|步骤|详细信息|  
|-----------|-------------|  
|**步骤 1：** [创建 Endpoint Protection 点站点系统角色](endpoint-protection-site-role.md)|必须先安装 Endpoint Protection 点站点系统角色，然后才能使用 Endpoint Protection。 必须将其仅安装在一个站点系统服务器上，并且必须将其安装在管理中心站点或独立主站点上层次结构的顶部。 |  
|**步骤 2：** [为 Endpoint Protection 配置警报](endpoint-configure-alerts.md)|当特定事件发生（如恶意软件感染）时，警报将通知管理员。 警报显示在“监视”  工作区的“警报”  节点中，或（可选）可通过电子邮件发送至指定用户。 |  
|**步骤 3：** [为 Endpoint Protection 客户端配置定义更新源](endpoint-definition-updates.md)|可以将 Endpoint Protection 配置为使用各种源来下载定义更新。 |  
|**步骤 4：** [配置默认反恶意软件策略并创建自定义反恶意软件策略](endpoint-antimalware-policies.md)|在安装 Endpoint Protection 客户端时，将应用默认反恶意软件策略。 在部署客户端的 60 分钟内将默认应用已部署的任何自定义策略。 请确保在部署 Endpoint Protection 客户端之前已配置了反恶意软件策略。 |  
|**步骤 5：** [为 Endpoint Protection 配置自定义客户端设置](endpoint-protection-configure-client.md)|使用自定义客户端设置为层次结构中计算机的集合配置 Endpoint Protection 设置。<br /><br /> 注意：除非确定要将这些设置应用于层次结构中的所有计算机，否则请不要配置默认 Endpoint Protection 客户端设置。 |  
