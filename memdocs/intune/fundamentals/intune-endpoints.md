---
title: Microsoft Intune 网络终结点
titleSuffix: ''
description: 查看 Intune 终结点。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/08/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: b8d9aef2-8757-4e22-9b24-a0833d27304c
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3276b7d483bf0fc3f94ce12245304ad9ad2ebad3
ms.sourcegitcommit: 15450a1e92d9f67f74ae619ffe192c15948107c5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89516267"
---
# <a name="network-endpoints-for-microsoft-intune"></a>Microsoft Intune 网络终结点  

此页列出了 Intune 部署中代理设置所需的 IP 地址和端口设置。

作为仅限云的服务，Intune 不需要诸如服务器或网关的本地基础结构。

## <a name="access-for-managed-devices"></a>受管理设备的访问权限  

若要管理防火墙和代理服务器后面的设备，必须启用 Intune 的通信。

> [!NOTE]
> 本节中的信息也适用于 Microsoft Intune 证书连接器。 连接器的网络要求与受管理设备相同

- 由于 Intune 客户端使用 **HTTP (80)** 和 **HTTPS (443)** ，因此代理服务器必须支持这两种协议。 Windows 信息保护使用端口 444。
- 对于某些任务（例如下载经典电脑代理的软件更新），Intune 需要对 manage.microsoft.com 的未经身份验证的代理服务器访问权限

可以修改单个客户端计算机上的代理服务器设置。 还可以使用“组策略”设置来更改位于指定代理服务器后面的所有客户端计算机的设置。


<!--
> [!NOTE] If Windows 8.1 devices haven't cached proxy server credentials, enrollment might fail because the request doesn't prompt for credentials. Enrollment fails without warning as the request wait for a connection. If users might experience this issue, instruct them to open their browser settings and save proxy server settings to enable a connection.   -->

托管的设备需要允许“所有用户”通过防火墙访问服务的配置。


下表列出了 Intune 客户端访问的端口和服务：

|域    |IP 地址      |
|-----------|----------------|
| login.microsoftonline.com <br> *.officeconfig.msocdn.com <br> config.office.com <br> graph.windows.net <br> enterpriseregistration。windows。net | 详细信息 [Office 365 URL 和 IP 地址范围](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) |
|portal.manage.microsoft.com<br> m.manage.microsoft.com |52.175.12.209<br>20.188.107.228<br>52.138.193.149<br>51.144.161.187<br>52.160.70.20<br>52.168.54.64 <br>13.72.226.202<br>52.189.220.232|
| sts.manage.microsoft.com | 13.93.223.241 <br>52.170.32.182 <br>52.164.224.159 <br>52.174.178.4 <br>13.75.122.143 <br>52.163.120.84<br>13.73.112.122<br>52.237.192.112|
|Manage.microsoft.com <br>i.manage.microsoft.com <br>r.manage.microsoft.com <br>a.manage.microsoft.com <br>p.manage.microsoft.com <br>EnterpriseEnrollment.manage.microsoft.com <br>EnterpriseEnrollment-s.manage.microsoft.com |40.83.123.72<br>13.76.177.110<br>52.169.9.87<br>52.174.26.23<br>104.40.82.191<br>13.82.96.212<br>52.147.8.239<br>40.115.69.185|
|portal.fei.msua01.manage.microsoft.com<br>m.fei.msua01.manage.microsoft.com<br>portal.fei.msua02.manage.microsoft.com<br>m.fei.msua02.manage.microsoft.com<br>portal.fei.msua04.manage.microsoft.com<br>m.fei.msua04.manage.microsoft.com<br>portal.fei.msua05.manage.microsoft.com<br>m.fei.msua05.manage.microsoft.com<br>portal.fei.amsua0502.manage.microsoft.com<br>m.fei.amsua0502.manage.microsoft.com<br>portal.fei.msua06.manage.microsoft.com<br>m.fei.msua06.manage.microsoft.com<br>portal.fei.amsua0602.manage.microsoft.com<br>m.fei.amsua0602.manage.microsoft.com<br>fei.amsua0202.manage.microsoft.com<br>portal.fei.amsua0202.manage.microsoft.com<br>m.fei.amsua0202.manage.microsoft.com<br>portal.fei.amsua0402.manage.microsoft.com<br>m.fei.amsua0402.manage.microsoft.com<br>portal.fei.amsua0801.manage.microsoft.com<br>portal.fei.msua08.manage.microsoft.com<br>m.fei.msua08.manage.microsoft.com<br>m.fei.amsua0801.manage.microsoft.com|52.160.70.20<br>52.168.54.64 |
|portal.fei.msub01.manage.microsoft.com<br>m.fei.msub01.manage.microsoft.com<br>portal.fei.amsub0102.manage.microsoft.com<br>m.fei.amsub0102.manage.microsoft.com<br>fei.msub02.manage.microsoft.com<br>portal.fei.msub02.manage.microsoft.com<br>m.fei.msub02.manage.microsoft.com<br>portal.fei.msub03.manage.microsoft.com<br>m.fei.msub03.manage.microsoft.com<br>portal.fei.msub05.manage.microsoft.com<br>m.fei.msub05.manage.microsoft.com<br>portal.fei.amsub0202.manage.microsoft.com<br>m.fei.amsub0202.manage.microsoft.com<br>portal.fei.amsub0302.manage.microsoft.com<br>m.fei.amsub0302.manage.microsoft.com<br>portal.fei.amsub0502.manage.microsoft.com<br>m.fei.amsub0502.manage.microsoft.com<br>portal.fei.amsub0601.manage.microsoft.com<br>m.fei.amsub0601.manage.microsoft.com|52.138.193.149<br>51.144.161.187|
|portal.fei.msuc01.manage.microsoft.com <br>m.fei.msuc01.manage.microsoft.com<br>portal.fei.msuc02.manage.microsoft.com <br>m.fei.msuc02.manage.microsoft.com<br>portal.fei.msuc03.manage.microsoft.com <br>m.fei.msuc03.manage.microsoft.com<br>portal.fei.msuc05.manage.microsoft.com <br>m.fei.msuc05.manage.microsoft.com|52.175.12.209<br>20.188.107.228|
|portal.fei.amsud0101.manage.microsoft.com<br>m.fei.amsud0101.manage.microsoft.com|13.72.226.202|
|fef.msua01.manage.microsoft.com|138.91.243.97|
|fef.msua02.manage.microsoft.com|52.177.194.236|
|fef.msua04.manage.microsoft.com|23.96.112.28|
|fef.msua06.manage.microsoft.com|13.78.185.97|
|fef.msub05.manage.microsoft.com|23.97.166.52|
|fef.msuc03.manage.microsoft.com|23.101.0.100|
|fef.amsua0502.manage.microsoft.com|13.85.68.142|
|fef.amsua0602.manage.microsoft.com|52.161.28.64|
|Admin.manage.microsoft.com|52.224.221.227<br>52.161.162.117<br>52.178.44.195<br>52.138.206.56<br>52.230.21.208<br>13.75.125.10|
|wip.mam.manage.microsoft.com|52.187.76.84<br>13.76.5.121<br>52.165.160.237<br>40.86.82.163<br>52.233.168.142<br>168.63.101.57<br>52.187.196.98<br>52.237.196.51|
|mam.manage.microsoft.com|104.40.69.125<br>13.90.192.78<br>40.85.174.177<br>40.85.77.31<br>137.116.229.43<br>52.163.215.232<br>52.174.102.180<br>52.187.196.173<br>52.156.162.48|
|*.manage.microsoft.com|40.82.248.224/28<br>20.189.105.0/24<br>20.37.153.0/24<br>20.37.192.128/25<br>20.38.81.0/24<br>20.41.1.0/24<br>20.42.1.0/24<br>20.42.130.0/24<br>20.42.224.128/25<br>20.43.129.0/24<br>40.119.8.128/25<br>40.74.25.0/24<br>40.82.249.128/25<br>40.80.184.128/25<br>52.150.137.0/25|


## <a name="network-requirements-for-powershell-scripts-and-win32-apps"></a>PowerShell 脚本和 Win32 应用的网络要求  

如果使用 Intune 部署 PowerShell 脚本或 Win32 应用，还需要授予对租户当前所在的终结点的访问权限。

|ASU | 存储名称 | CDN |
| --- | --- |--- |
|AMSUA0601<br>AMSUA0602<br>AMSUA0101<br>AMSUA0102<br>AMSUA0201<br>AMSUA0202<br>AMSUA0401<br>AMSUA0402<br>AMSUA0501<br>AMSUA0502<br>AMSUA0701<br>AMSUA0702 | naprodimedatapri<br>naprodimedatasec<br>naprodimedatahotfix | naprodimedatapri.azureedge.net<br>naprodimedatasec.azureedge.net<br>naprodimedatahotfix.azureedge.net |
| AMSUB0101<br>AMSUB0102<br>AMSUB0201<br>AMSUB0202<br>AMSUB0301<br>AMSUB0302<br>AMSUB0501<br>AMSUB0502 | euprodimedatapri<br>euprodimedatasec<br>euprodimedatahotfix | euprodimedatapri.azureedge.net<br>euprodimedatasec.azureedge.net<br>euprodimedatahotfix.azureedge.net |
| AMSUC0101<br>AMSUC0201<br>AMSUC0301<br>AMSUC0501<br>AMSUD0101| approdimedatapri<br>approdimedatasec<br>approdimedatahotifx | approdimedatapri.azureedge.net<br>approdimedatasec.azureedge.net<br>approdimedatahotfix.azureedge.net |

## <a name="windows-push-notification-services-wns"></a>Windows 推送通知服务 (WNS)  

对于使用移动设备管理 (MDM) 管理的由 Intune 管理的 Windows 设备，设备操作和其他即时活动需要使用 Windows 推送通知服务 (WNS)。 有关详细信息，请参阅[允许 Windows 通知流量通过企业防火墙](/windows/uwp/design/shell/tiles-and-notifications/firewall-allowlist-config)。  

## <a name="delivery-optimization-port-requirements"></a>传递优化端口要求  

### <a name="port-requirements"></a>端口要求  

对于对等流量，传递优化将 7680 用于 TCP/IP，或将 3544 用于 NAT 遍历（也可以是 Teredo）。 对于客户端-服务通信，它通过端口 80/443 使用 HTTP 或 HTTPS。

### <a name="proxy-requirements"></a>代理要求  

若要使用传递优化，必须允许“字节范围”请求。 有关详细信息，请参阅 [Windows 更新的代理要求](/windows/deployment/update/windows-update-troubleshooting)。

### <a name="firewall-requirements"></a>防火墙要求  

允许下列主机名通过防火墙，以支持传递优化。
对于客户端与传递优化云服务之间的通信：
- \*.do.dsp.mp.microsoft.com

对于传递优化元数据：
- \*.dl.delivery.mp.microsoft.com
- \*.emdl.ws.microsoft.com

## <a name="apple-device-network-information"></a>Apple 设备网络信息  

|用途|主机名（IP 地址/子网）|协议|Port|
|-----|--------|------|-------|
|检索并显示 Apple 服务器的内容|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br> \*.phobos.itunes-apple.com.akadns.net |    HTTP    |      80      |
|与 APNS 服务器之间的通信|#-courier.push.apple.com<br>“#”是 0 到 50 范围内的一个随机数字。|    TCP     |  5223 和 443  |
|各种功能，包括访问万维网、iTunes 商店、macOS 应用商店、iCloud、消息等。 |phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net| HTTP/HTTPS |  80 或 443   |

有关详细信息，请参阅 Apple 的 [Apple 软件产品使用的 TCP 和 UDP 端口](https://support.apple.com/HT202944)、[关于 macOS、iOS/iPadOS 和 iTunes 服务器主机连接和 iTunes 后台进程](https://support.apple.com/HT201999)，以及[如果你的 macOS 和 iOS/iPadOS 客户端不获取 Apple 推送通知](https://support.apple.com/HT203609)。  

## <a name="android-port-information"></a>Android 端口信息

根据选择管理 Android 设备的方式，你可能需要打开 Google Android Enterprise 端口和/或 Android 推送通知。 有关支持的 Android 管理方法的更多信息，请参阅 [Android 注册文档](../enrollment/android-enroll.md)。 

> [!NOTE]
> 由于 Google 移动服务在中国不可用，因此在中国由 Intune 管理的设备无法使用需要 Google 移动服务的功能。 这些功能包括：Google Play 保护机制功能，如 SafetyNet 设备证明、管理 Google Play 商店的应用、Android Enterprise 功能（请参阅 [Google 文档](https://support.google.com/work/android/answer/6270910)）。 此外，Android 版 Intune 公司门户应用使用 Google 移动服务与 Microsoft Intune 服务进行通信。 由于 Google Play 服务在中国不可用，因此某些任务最长可能需要 8 小时才能完成。 有关详细信息，请参阅此[文章](../apps/manage-without-gms.md#limitations-of-intune-device-administrator-management-when-gms-is-unavailable)。

### <a name="google-android-enterprise"></a>Google Android Enterprise 

Google 针对其 [Android Enterprise 蓝皮书](https://static.googleusercontent.com/media/www.android.com/en//static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)的“防火墙”部分中所述的所需网络端口和目标主机名提供了相关文档。 

### <a name="android-push-notification"></a>Android 推送通知

Intune 利用 Google Firebase 云消息传递 (FCM)，让推送通知来触发设备操作和签入。Android 设备管理员和 Android Enterprise 都要求采用这种机制。 有关 FCM 网络要求的信息，请参阅 Google 的 [FCM 端口和防火墙](https://firebase.google.com/docs/cloud-messaging/concept-options#messaging-ports-and-your-firewall)。

## <a name="endpoint-analytics"></a>终结点分析

有关终结点分析所需终结点的详细信息，请参阅[终结点分析代理配置](../../analytics/troubleshoot.md#bkmk_endpoints)。