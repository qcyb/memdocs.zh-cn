---
title: 监视电子邮件、Wi-Fi 和 VPN 配置文件
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中监视电子邮件、Wi-Fi 和 VPN 配置文件的符合性状态。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e2315b8b-98bc-40e1-8ef9-bfb5e69ab109
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 59e372641c303e77f0d88e655bb917660c9e677c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709425"
---
# <a name="monitor-email-wi-fi-and-vpn-profiles-in-configuration-manager"></a>在 Configuration Manager 中监视电子邮件、Wi-Fi 和 VPN 配置文件

适用范围：  Configuration Manager (Current Branch)

将 Configuration Manager 电子邮件、Wi-Fi 或 VPN 配置文件部署到层次结构中的用户后，可以使用下列过程来监视配置文件的符合性状态：  

-   [如何在 Configuration Manager 控制台中查看符合性结果](#BKMK_console)  

-   [如何使用报表来查看符合性结果](#BKMK_Reports)  

##  <a name="how-to-view-compliance-results-in-the-configuration-manager-console"></a><a name="BKMK_console"></a> 如何在 Configuration Manager 控制台中查看符合性结果  
 使用此过程在 Configuration Manager 控制台中查看有关所部署配置文件的符合性的详细信息。  

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>在 Configuration Manager 控制台查看符合性结果  

1.  在 Configuration Manager 控制台中，单击“监视”  。  

2.  在“监视”  工作区中，单击“部署”  。  

3.  在“部署”  列表中，选择要查看其符合性信息的配置文件部署。  

4.  可以在主页上查看有关配置文件部署符合性的摘要信息。 若要查看详细信息，请选择配置文件部署，然后在“主页”  选项卡上的“部署”  组中，单击“查看状态”  以打开“部署状态”  页。  

     “部署状态”  页包含下列选项卡：  

    -   **符合：** 显示基于受影响资产数量的配置文件的符合性。 你可以双击规则以在“资产和符合性”  工作区中的“用户”  节点下创建一个临时节点，其中包含符合此配置文件的所有用户。 “资产详细信息”  窗格显示符合配置文件的用户。 双击列表中的用户以显示其他信息。  

        > [!IMPORTANT]  
        >  如果某个配置文件在客户端设备上不适用，则不会评估该配置文件；但是，它返回的状态为符合。  

    -   **错误：** 显示基于受影响资产数量的所选配置文件部署的所有错误的列表。 你可以双击规则以在“资产和符合性”  工作区的“用户”  节点下创建一个临时节点，其中包含对于此配置文件生成了错误的所有用户。 当你选择某个用户时，“资产详细信息”  窗格将显示受所选问题影响的用户。 双击列表中的用户以显示有关问题的其他信息。  

    -   **不符合：** 显示基于受影响资产数量的配置文件内所有不符合规则的列表。 你可以双击规则以在“资产和符合性”  工作区的“用户”  节点下创建一个临时节点，其中包含不符合此配置文件的所有用户。 当你选择某个用户时，“资产详细信息”  窗格将显示受所选问题影响的用户。 双击列表中的用户以显示有关问题的进一步信息。  

    -   **未知：** 显示所有未报告所选配置文件部署符合性的用户的列表，以及设备的当前客户端状态。  

5.  在“部署状态”  页上，可以查看有关所部署的配置文件的符合性的详细信息。 将在“部署”  节点下创建一个临时节点，该节点可帮助你快速再次找到此信息。  

##  <a name="how-to-view-compliance-results-by-using-reports"></a><a name="BKMK_Reports"></a> 如何使用报表来查看符合性结果  
 符合性设置（包括 Configuration Manager 中的配置文件）还包括一些内置报表，使你能监视有关配置文件的信息。 这些报表的报表类别为“符合性和设置管理”  。  

> [!IMPORTANT]  
>  在符合性设置报表中使用参数“设备筛选器”  和“用户筛选器”  时，你必须使用通配符 (%) 字符。  

 有关如何在 Configuration Manager 中配置报表的详细信息，请参阅[报表简介](../../core/servers/manage/introduction-to-reporting.md)。  
