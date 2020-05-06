---
title: 部署资源访问配置文件
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中部署 Wi-Fi、VPN 和证书配置文件。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0272c50429973cc3e15c295303b91593075ebe01
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709455"
---
# <a name="deploy-resource-access-profiles-in-configuration-manager"></a>在 Configuration Manager 中部署资源访问配置文件

适用范围：  Configuration Manager (Current Branch)

创建以下资源访问配置文件之一后，将其部署到一个或多个集合：

- [Wi-Fi](create-wifi-profiles.md)
- [VPN](create-vpn-profiles.md)
- [Certificate](create-certificate-profiles.md)

部署这些配置文件时，需指定目标集合，并指定客户端评估配置文件符合性的频率。  

## <a name="deploy-a-profile"></a>部署配置文件

1. 在 Configuration Manager 控制台中，转到“资产和符合性”  工作区。 依次展开“符合性设置”和“公司资源访问”，然后选择相应的配置文件节点   。 例如“Wi-Fi 配置文件”  。

1. 在配置文件列表中，选择想要部署的配置文件。 然后在功能区的“主页”选项卡上，在“部署”组中，选择“部署”    。  

1. 在“部署配置文件”窗口中，指定下列信息：  

    - **集合**：选择要在其中部署配置文件的集合。

    - **生成警报**：启用此选项可配置警报。 如果在指定日期和时间前配置文件符合性低于指定百分比，则站点将生成此警报。 你也可以选择是否希望将警报发送到 System Center Operations Manager。

    - **随机延迟(小时)** ：仅用于包含简单证书注册协议 (SCEP) 设置的证书配置文件，指定一个延迟时段以避免对网络设备注册服务 (NDES) 进行过度处理。 默认值为 `64` 小时。  

    - 指定此配置文件的符合性评估计划  ：指定客户端多久评估一次此配置文件的符合性。 选择“简单计划”或配置“自定义计划”   。 默认情况下，简单计划是每 `12` 小时。

1. 选择“确定”，关闭窗口并创建部署  。

## <a name="delete-a-deployment"></a>删除部署

若要删除部署，请在列表中进行选择。 在详细信息窗格中，切换到“部署”选项卡  。选择部署，然后在功能区的“部署”  选项卡中选择“删除”  。

> [!IMPORTANT]
> 删除 VPN 配置文件部署时，Configuration Manager 不会从 Windows 中删除 VPN 配置文件。 如果要从设备中删除配置文件，则将其手动删除。

## <a name="next-steps"></a>后续步骤

[监视 Wi-Fi 和 VPN 配置文件](monitor-wifi-email-vpn-profiles.md)

[监视证书配置文件](monitor-certificate-profiles.md)
