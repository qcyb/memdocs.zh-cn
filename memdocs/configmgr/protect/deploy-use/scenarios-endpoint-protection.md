---
title: 保护计算机免遭恶意软件攻击
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中实现 Endpoint Protection，使计算机免受恶意软件侵害。
ms.date: 05/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 539c7a89-3c03-4571-9cb4-02d455064eeb
author: mestew
ms.author: mstewart
manager: doubeby
ms.openlocfilehash: 6e0e350fe490de50a053e93f2922feba5e0ea8c5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706415"
---
# <a name="example-scenario-use-endpoint-protection-to-protect-computers-from-malware"></a>示例方案：使用 Endpoint Protection 来保护计算机免受恶意软件侵害

适用范围：  Configuration Manager (Current Branch)

本文提供了示例方案，展示如何在 Configuration Manager 中实施 Endpoint Protection 以保护组织中的计算机免遭恶意软件攻击。  



## <a name="scenario-overview"></a>方案概述

 Configuration Manager 在 Woodgrove Bank 上安装和使用。 该银行目前使用 System Center Endpoint Protection 来保护计算机免受恶意软件攻击。 此外，该银行使用 Windows 组策略来确保公司中的所有计算机上都启用了 Windows 防火墙，并确保在 Windows 防火墙阻止新程序时通知用户。  

Configuration Manager 管理员已受命将 Woodgrove Bank 的反恶意软件升级到 System Center Endpoint Protection，以便银行可以利用最新的反恶意软件功能并能够从 Configuration Manager 控制台集中管理反恶意软件解决方案。 


## <a name="business-requirements"></a>业务要求

此实现具有下列要求：  

- 使用 Configuration Manager 来管理组策略当前管理的 Windows 防火墙设置。  

- 使用 Configuration Manager 软件更新，将恶意软件定义下载到计算机。 如果软件更新不可用，例如，如果计算机未连接到公司网络，则计算机必须从 Microsoft 更新中下载定义更新。  

- 用户的计算机必须每天执行一次恶意软件快速扫描。 但是，服务器必须在每个星期六的凌晨 1 点（工作时间外）运行完全扫描。  

- 每次发生下列事件之一时，请发送电子邮件警报：  

  -   在任意计算机上检测到恶意软件  

  -   在 5% 以上的计算机上检测到相同的恶意软件威胁  

  -   在任意 24 小时内检测到相同恶意软件威胁的次数超过 5 次  

  -   在任意 24 小时内检测到 3 种以上的不同类型的恶意软件  

  管理员随后执行以下步骤来实现 Endpoint Protection：  



##  <a name="steps-to-implement-endpoint-protection"></a>若要实现 Endpoint Protection 的步骤  

|过程|参考|  
|-------------|---------------|  
|管理员查看 Configuration Manager 中 Endpoint Protection 的基本概念的可用信息。|有关 Endpoint Protection 的概述信息，请参阅 [Endpoint Protection](endpoint-protection.md)。|  
|管理员查看并实现使用 Endpoint Protection 所需的先决条件。|有关 Endpoint Protection 的先决条件的信息，请参阅[规划 Endpoint Protection](../plan-design/planning-for-endpoint-protection.md)。|  
|管理员仅在一个站点系统服务器上安装 Endpoint Protection 站点系统角色，该服务器位于 Woodgrove Bank 层次结构的顶部。|有关如何安装 Endpoint Protection 站点系统角色的详细信息，请参阅[配置 Endpoint Protection](endpoint-protection-configure.md) 中的“先决条件”。|  
|管理员配置 Configuration Manager 以使用 SMTP 服务器发送电子邮件警报。<br /><br /> **注意:** 仅当希望在生成 Endpoint Protection 警报时收到电子邮件通知，才必须配置 SMTP 服务器。|有关详细信息，请参阅[在 Endpoint Protection 中配置警报](endpoint-configure-alerts.md)。|  
|管理员创建包含所有计算机和服务器的设备集合以安装 Endpoint Protection 客户端。 他们将此集合命名为“受 Endpoint Protection 保护的所有计算机”  。<br /><br /> **提示：** 无法为用户集合配置警报。|有关如何创建集合的详细信息，请参阅[如何创建集合](../../core/clients/manage/collections/create-collections.md)|  
|管理员配置集合的以下警报： <br /><br />1) **检测到恶意软件**：管理员将警报严重性配置为“严重”  。 <br /><br />2) **在多台计算机上检测到相同类型的恶意软件**：管理员将警报的严重性配置为“严重”  并指定当 5% 以上的计算机检测到恶意软件时将生成警报。 <br /><br />3) **在指定时间间隔内，在计算机上重复检测到相同类型的恶意软件**：管理员将警报的严重性配置为“严重”并指定当在 24 小时内检测到恶意软件的次数超过 5 次时将生成警报。 <br /><br />4) **在指定的时间间隔内，同一台计算机上检测到多种恶意软件**：管理员将警报的严重性配置为“严重”并指定当 24 小时内检测到 3 种以上的恶意软件时将生成警报。<br /><br /> “警报严重性”的值指示将在 Configuration Manager 控制台和电子邮件中接收的警报中显示的警报级别  。<br /><br /> 此外，他们选择“在 Endpoint Protection 仪表板中查看此集合”选项，以便可在 Configuration Manager 控制台中监视警报  。|请参阅[配置 Endpoint Protection](endpoint-configure-alerts.md) 中的“为 Endpoint Protection 配置警报”。|  
|管理员通过使用自动部署规则将 Configuration Manager 软件更新配置为每天下载和部署定义更新三次。|有关详细信息，请参阅[使用 Configuration Manager 软件更新来提供定义更新](endpoint-definitions-configmgr.md)中的“使用 Configuration Manager 软件更新来提供定义更新”部分。|  
|管理员检查默认反恶意软件政策中的设置，其中包含来自 Microsoft 推荐的安全设置。 对于每天执行一次快速扫描的计算机，他们将更改以下设置：<br /><br /> 1) **在客户端计算机上运行每日快速扫描**：**是**。<br /><br /> 2) **每日快速扫描计划时间**：**早上 9:00**。<br /><br /> 管理员注意到“从 Microsoft 更新分发的更新”默认选为了定义更新源  。 这满足了计算机在无法接收 Configuration Manager 软件更新时从 Microsoft 更新下载定义的业务需求。|请参阅[如何为 Endpoint Protection 创建和部署反恶意软件策略](endpoint-antimalware-policies.md)。|  
|管理员创建一个集合，其中只含有名为“Woodgrove Bank 服务器”的 Woodgrove Bank 服务器  。|请参阅[如何创建集合](../../core/clients/manage/collections/create-collections.md)|  
|管理员创建一个名为“Woodgrove Bank 服务器策略”的自定义反恶意软件政策  。 他们只添加“计划扫描”设置，并进行以下更改  ：<br /><br /> **扫描类型**：**全部**<br /><br /> **扫描日期**：**星期六**<br /><br /> **扫描时间**：**凌晨 1:00**<br /><br /> **在客户端计算机上运行每日快速扫描**：**否**。|请参阅[如何为 Endpoint Protection 创建和部署反恶意软件策略](endpoint-antimalware-policies.md)。|  
|管理员将“Woodgrove Bank 服务器策略”自定义反恶意软件政策部署到“Woodgrove Bank 服务器”集合   。|请参阅[如何为 Endpoint Protection 创建和部署反恶意软件策略](endpoint-antimalware-policies.md)一文中的“将反恶意软件策略部署到客户端计算机”。|  
|管理员为 Endpoint Protection 创建一组新的自定义客户端设备设置，并将其命名为“Woodgrove Bank Endpoint Protection 设置”  。<br /><br /> **注意:** 如果不希望在层次结构中的所有客户端上安装并启用 Endpoint Protection，请确保在默认客户端设置中将选项“管理客户端计算机上的 Endpoint Protection 客户端”  和“在客户端计算机上安装 Endpoint Protection 客户端”  均配置为“否”  。|有关详细信息，请参阅[为 Endpoint Protection 配置自定义客户端设置](endpoint-protection-configure-client.md)。|  
|他们为 Endpoint Protection 配置以下设置：<br /><br /> **在客户端计算机上管理 Endpoint Protection 客户端**：**是**<br /><br /> 此设置和值确保已安装的所有现有 Endpoint Protection 客户端将由 Configuration Manager 托管。<br /><br /> **在客户端计算机上安装 Endpoint Protection 客户端**：**是**。</br></br>请注意，从 Configuration Manager 1802 开始，Windows 10 设备不需要安装 Endpoint Protection 代理  。 如果已在 Windows 10 设备上安装该代理，Configuration Manager 也不会将其删除。 管理员可在运行最低 1802 客户端版本的 Windows 10 设备上删除 Endpoint Protection 代理。|有关详细信息，请参阅[为 Endpoint Protection 配置自定义客户端设置](endpoint-protection-configure-client.md)。|  
|管理员将“Woodgrove Bank Endpoint Protection 设置”客户端设置部署到“受 Endpoint Protection 保护的所有计算机”集合   。|请参阅[在 Configuration Manager 中配置 Endpoint Protection](endpoint-antimalware-policies.md) 中的“为 Endpoint Protection 配置自定义客户端设置”。|  
|管理员使用创建的 Windows 防火墙策略向导，通过配置域配置文件的以下设置创建策略：<br /><br /> 1) **启用 Windows 防火墙**：**是**<br /><br /> 2)<br />                    **Windows 防火墙阻止新程序时通知用户**：**是**|请参阅[如何为 Endpoint Protection 创建和部署 Windows 防火墙策略](../../protect/deploy-use/create-windows-firewall-policies.md)|  
|管理员将新的防火墙策略部署到先前创建的“受 Endpoint Protection 保护的所有计算机”集合  。|请参阅[如何为 Endpoint Protection 创建和部署 Windows 防火墙策略](create-windows-firewall-policies.md)中的“部署 Windows 防火墙策略”|  
|管理员使用 Endpoint Protection 的可用管理任务来管理反恶意软件和 Windows 防火墙策略、在必要时执行计算机按需扫描、强制计算机下载最新的定义并指定当检测到恶意软件时采取的任何进一步操作。|请参阅[如何为 Endpoint Protection 管理反恶意软件策略和防火墙设置](endpoint-antimalware-firewall.md)|  
|管理员使用以下方法来监视 Endpoint Protection 的状态和 Endpoint Protection 采取的操作：<br /><br /> 1) 通过使用“监视”  工作区中“安全性”  下的“Endpoint Protection 状态”  节点。<br /><br /> 2)通过使用“资产和符合性”  工作区中的“Endpoint Protection”  节点。<br /><br /> 3) 通过使用 Configuration Manager 内置报表。|请参阅[如何监视 Endpoint Protection](monitor-endpoint-protection.md)|  

 管理员告知经理已成功实施 Endpoint Protection，并且根据指定的业务要求，确认 Woodgrove Bank 的计算机当前受到保护，免受反恶意软件攻击。 

## <a name="next-steps"></a>后续步骤

有关详细信息，请参阅[如何配置 Endpoint Protection](endpoint-protection-configure.md)