---
title: 特性和功能
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 的主要管理功能。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5cdd0a9497f07d80813aca5dc169c4d61944e85d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706395"
---
# <a name="features-and-capabilities-of-configuration-manager"></a>Configuration Manager 的特性和功能

适用范围：  Configuration Manager (Current Branch)

本文总结了 Configuration Manager 的主要管理功能。 每项功能都有自己的先决条件，并且每个功能的使用方式可能会影响 Configuration Manager 层次结构的设计和实现。 例如，你希望将软件更新部署到层次结构中的设备，则需要软件更新站点系统角色。  

有关如何规划和安装 Configuration Manager 以在环境中支持这些管理功能的详细信息，请参阅[为 Configuration Manager 做准备](../get-ready.md)。  

## <a name="co-management"></a>共同管理

共同管理是将现有 Configuration Manager 部署附加到 Microsoft 365 云的主要方式之一。 它使你能够使用 Configuration Manager 和 Microsoft Intune 同时管理 Windows 10 设备。 借助共同管理，可以通过添加新功能（如条件访问）在 Configuration Manager 中云附加现有投资。 有关详细信息，请参阅[什么是共同管理](../../../comanage/overview.md)？

## <a name="desktop-analytics"></a>桌面分析

桌面分析是一项基于云的服务，可与 Configuration Manager 集成。 该服务为你提供见解和情报，让你在了解更多信息的情况下决定 Windows 客户端的更新是否就绪。 它将组织中的数据与从数百万台连接到 Microsoft 云服务的设备中聚合得到的数据进行组合。 有关详细信息，请参阅[什么是桌面分析](../../../desktop-analytics/overview.md)？

## <a name="cloud-attached-management"></a>云附加管理

使用云管理网关、基于云的分发点和 Azure Active Directory 等功能来管理基于 Internet 的客户端。

有关详细信息，请参阅下列文章：

- [在 Internet 上管理客户端](../../clients/manage/manage-clients-internet.md)
- [规划 Azure AD](../security/plan-for-security.md#bkmk_planazuread)
- [Azure 服务](../../servers/deploy/configure/azure-services-wizard.md)

## <a name="real-time-management"></a>实时管理

使用 CMPivot 立即查询联机设备，然后筛选和分组数据以获取深入见解。 还可以使用 Configuration Manager 控制台管理 Windows PowerShell 脚本，并将其部署到客户端。 有关详细信息，请参阅 [CMPivot](../../servers/manage/cmpivot.md)和[创建和运行 PowerShell 脚本](../../../apps/deploy-use/create-deploy-scripts.md)。

## <a name="application-management"></a>应用程序管理

帮助你创建、管理、部署和监视一系列你管理的不同设备的应用程序。 从 Configuration Manager 控制台部署、更新和管理 Office 365。 此外，Configuration Manager 还与适用于企业和教育的 Microsoft Store 集成，以提供基于云的应用。 有关详细信息，请参阅[应用程序管理简介](../../../apps/understand/introduction-to-application-management.md)。

## <a name="os-deployment"></a>OS 部署

部署 Windows 10 的就地升级，或捕获和部署操作系统映像。 映像部署可以使用 PXE、多播或可启动的媒体。 它还可帮助使用 Windows Autopilot 重新部署现有设备。 有关详细信息，请参阅 [OS 部署简介](../../../osd/understand/introduction-to-operating-system-deployment.md)。  

## <a name="software-updates"></a>软件更新

管理、部署和监视组织中的软件更新。 与 Windows 传递优化和其他对等缓存技术集成，以帮助控制网络使用情况。 有关详细信息，请参阅[软件更新简介](../../../sum/understand/software-updates-introduction.md)。  

## <a name="company-resource-access"></a>公司资源访问

允许组织中的用户对远程位置中的数据和应用程序进行访问。 此功能包括 Wi-fi、VPN、电子邮件和证书配置文件。 有关详细信息，请参阅[保护数据和站点基础结构](../../../protect/understand/protect-data-and-site-infrastructure.md)。

## <a name="compliance-settings"></a>符合性设置

帮助你评估、跟踪和修正组织中客户端设备的配置合规性。 此外，你还可以使用符合性设置来配置你管理的设备上的一系列功能和安全设置。 有关详细信息，请参阅[确保设备合规性](../../../compliance/understand/ensure-device-compliance.md)。  

## <a name="endpoint-protection"></a>Endpoint Protection

提供针对组织中的计算机的安全性、反恶意软件和 Windows 防火墙管理。 此区域包括与以下 Windows Defender 套件功能的管理和集成：

- Windows Defender 防病毒
- Microsoft Defender 高级威胁防护
- Windows Defender 攻击防护
- Windows Defender 应用程序防护
- Windows Defender 应用程序控制
- Windows Defender 防火墙

有关详细信息，请参阅 [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)。  

## <a name="inventory"></a>库存

有助于识别和监视资产。

### <a name="hardware-inventory"></a>硬件清单

收集有关组织中的设备硬件的详细信息。 有关详细信息，请参阅[硬件清单简介](../../clients/manage/inventory/introduction-to-hardware-inventory.md)。  

### <a name="software-inventory"></a>软件清单

收集和报告有关存储在组织中客户端计算机上的文件的信息。 有关详细信息，请参阅[软件清单简介](../../clients/manage/inventory/introduction-to-software-inventory.md)。  

### <a name="asset-intelligence"></a>资产智能

提供工具以收集清单数据，并监视组织中的软件许可证使用情况。 有关详细信息，请参阅[资产智能简介](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md)。  

## <a name="on-premises-mobile-device-management"></a>本地移动设备管理

通过使用内置在设备平台中的管理功能的本地 Configuration Manager 基础结构来注册和管理设备。 （典型管理使用单独安装的 Configuration Manager 客户端。）此功能当前支持管理 Windows 10 企业版和 Windows 10 移动版设备。 有关详细信息，请参阅[使用本地基础结构管理移动设备](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。  

## <a name="power-management"></a>电源管理

管理和监视组织中客户端计算机的功耗。 配置电源计划，并使用 LAN 唤醒在工作时间以外进行维护。 有关详细信息，请参阅[电源管理简介](../../clients/manage/power/introduction-to-power-management.md)。  

## <a name="remote-control"></a>远程控制

提供工具以通过远程方式从 Configuration Manager 控制台中管理客户端计算机。 有关详细信息，请参阅[远程控制简介](../../clients/manage/remote-control/introduction-to-remote-control.md)。  

## <a name="reporting"></a>报表

从 Configuration Manager 控制台中使用 SQL Server Reporting Services 的高级报表功能。 此功能提供了数百个默认报表。 有关详细信息，请参阅[报表简介](../../servers/manage/introduction-to-reporting.md)。  

## <a name="software-metering"></a>软件计数

监视和收集 Configuration Manager 客户端中的软件使用情况数据。 你可以使用这些数据来确定软件安装后是否使用。 有关详细信息，请参阅[使用软件计数监视应用使用情况](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)。  
