---
title: 用于中国部署的网络终结点 - Microsoft Intune
titleSuffix: ''
description: 查看 Intune 的中国终结点。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: b5551e537716ed12a0a5b5de19b747ffc7c4dcac
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347332"
---
# <a name="china-endpoints-for-microsoft-intune"></a>Microsoft Intune 的中国终结点

此页列出了 Intune 部署中代理设置所需的中国终结点。

若要管理防火墙和代理服务器后面的设备，必须启用 Intune 的通信。

- 由于 Intune 客户端使用 **HTTP (80)** 和 **HTTPS (443)** ，因此代理服务器必须支持这两种协议
- 对于某些任务（例如下载软件更新），Intune 需要对 manage.microsoft.com 的未经身份验证的代理服务器访问权限

可以修改单个客户端计算机上的代理服务器设置。 还可以使用“组策略”设置来更改位于指定代理服务器后面的所有客户端计算机的设置。

托管的设备需要允许“所有用户”通过防火墙访问服务的配置。

有关适用于中国客户的 Windows 10 自动注册和设备注册的详细信息，请参阅[设置 Windows 设备的注册](../enrollment/windows-enroll.md#windows-10-auto-enrollment-and-device-registration)。

下表列出了 Intune 客户端访问的端口和服务：

|终结点|**IP 地址**|
|---------------------|-----------|
|*.manage.microsoft.cn | 40.73.38.143<br>139.217.97.81<br>52.130.80.24<br>40.73.41.162<br>40.73.58.153<br>139.217.95.85 |


## <a name="intune-customer-designated-endpoints-in-china"></a>中国 Intune 客户指定的终结点
- Azure 门户：https:\//portal.azure.cn/
- Office 365：https:\//portal.partner.microsoftonline.cn/
- Intune 公司门户：https:\//portal.manage.microsoftonline.cn/
- Microsoft Endpoint Manager 管理中心：https:\//endpoint.microsoftonline.cn/


## <a name="partner-service-endpoints"></a>合作伙伴服务终结点

由世纪互联运营的 Intune 依赖于以下合作伙伴服务终结点：
- Azure AD Sync 服务：https:\//syncservice.partner.microsoftonline.cn/DirectoryService.svc
- Evo STS：https:\//login.chinacloudapi.cn/
- Azure AD Graph：https:\//graph.chinacloudapi.us
- MS Graph：https:\//microsoftgraph.chinacloudapi.cn
- ADRS：https:\//enterpriseregistration.partner.microsoftonline.cn

[!INCLUDE [Intune notices](../includes/windows-push-notification-services.md)]

[!INCLUDE [Intune notices](../includes/apple-device-network-information.md)]

## <a name="next-steps"></a>后续步骤
[了解有关 Intune 由世纪互联在中国运营的详细信息](china.md)

