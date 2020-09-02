---
title: 排查 Intune Exchange Connector 的常见错误
titleSuffix: Microsoft Intune
description: 排查和解决本地 Microsoft Intune Exchange Connector 的常见错误
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cea8981b9fdd16e0d8da9dd36445b8fbdfe3d53f
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193940"
---
# <a name="resolve-common-errors-for-the-intune-exchange-connector"></a>解决 Intune Exchange Connector 的常见错误

本文可以帮助 Intune 管理员解决有关 Intune Exchange Connector 操作的特定错误和消息。  

## <a name="configuration-failed-and-returned-error-code-0x0000001"></a>配置失败，返回的错误代码 0x0000001

**问题**：  
尝试配置 Microsoft Intune Exchange Connector 时，会收到以下错误消息：

```
   The Microsoft Intune Exchange Connector cannot connect to the Microsoft Exchange server.  
   The following Microsoft Exchange Server address could not be reached <Exchange server Name FQDN>  
   Verify that the FQDN of the exchange server address and credentials that you entered is correct and the server is running. The Microsoft Intune Exchange Connector does not support Exchange server arrays.  
   Error code: 0x0000001  
```

如果未正确配置 Internet 代理设置，可能会出现此问题。

**解决方法**：  
配置代理设置：
1. 请与本地网络管理员联系，确保已正确配置代理设置。 
2. 使用 Netsh winhttp 命令配置代理服务器并添加所需的排除列表  。 例如：  

   ```
   Netsh winhttp set proxy proxy-server="http=proxy.corp.domain.com" bypass-list"34*.*;134.132.*.*;10.*.*;localhost;*.corp.domain.com;*.staging.domain.com"
   ```

## <a name="configuration-failed-and-returned-error-code-0x000000b"></a>配置失败，返回的错误代码 0x000000b   

**问题**：  
尝试配置 Microsoft Intune Exchange Connector 时，会收到以下错误消息：  

```
   The Microsoft Intune Exchange Connector experienced an error:  
   CertEnroll::CX509PrivateKey::Create: The system cannot find the file specified. 0x80070002 (WIN32: 2  
   ERROR_FILE_NOT_FOUND  
   Error code: 0x000000b  
```
如果用于登录 Intune 的帐户不是 Intune 全局管理员帐户，则会出现此问题。

**解决方法**：  
使用全局管理员帐户登录 Intune，或将你的帐户添加到全局管理员组。 有关详细信息，请参阅 [Microsoft Intune 的基于角色的管理控制 (RBAC)](../fundamentals/role-based-access-control.md)。

## <a name="configuration-failed-and-returned-error-code-0x0000006"></a>配置失败，返回的错误代码 0x0000006

**问题**：  
尝试配置 Microsoft Intune Exchange Connector 时，会收到以下错误消息：  

```  
   The Microsoft Intune Exchange Connector cannot connect to Microsoft Intune  
   Verify that you are connected to the Internet, check the Microsoft Intune Service Status, and try to connect again.  
   Error code: 0x00000006  
```  
如果使用代理服务器连接到 Internet 并阻止到 Intune 服务的流量，则会出现此错误。 要确定是否正在使用代理，请转到“控制面板” > “Internet 选项”，选择“连接”选项卡，然后单击“局域网设置”     。

**解决方法**：  

- **选项 1** - 删除代理设置，以便计算机无需通过代理即可连接到 Internet。  

- **选项 2** - 如 [Intune Exchange Connector 要求](exchange-connector-install.md#intune-exchange-connector-requirements)中所述，将代理服务器配置为允许与 Intune 服务通信。



## <a name="event-7000-or-7041-microsoft-intune-exchange-connector-service-wont-start"></a>事件 7000 或 7041：Microsoft Intune Exchange Connector 服务无法启动

**问题**：  
IOS 设备无法在 Intune 中注册，并生成以下某种错误消息：  

```  
   Log Name:      System
   Source:            Service Control Manager
   Date:               <time>
   Task Category: None
   Level:               Error
   Keywords:        Classic
   User:                N/A
   Computer:      <computer>
   Description:
   The Microsoft Intune Exchange Connector Service service failed to start because of the following error:  
   The service did not start because of a logon failure.
```  

```  
   Log Name:      System
   Source:            Service Control Manager
   Date:               <time>
   Event ID:          7041
   Task Category: None
   Level:               Error   
   Keywords:        Classic
   User:                N/A
   Computer:       <computer>
   Description:
   The WIEC service was unable to log on as .\WIEC_USER with the currently configured password because of the following error:
   Logon failure: the user has not been granted the requested logon type at this computer.
   Service: WIEC
   Domain and account: .\WIEC_USER
   This service account does not have the required user right "Log on as a service."  
```
如果 WIEC_User 帐户在本地策略中没有“作为服务登录”用户权限，则会出现此问题   。

**解决方法**：  
在运行 Intune Exchange Connector 的计算机上，将“作为服务登录”用户权限分配给 WIEC_User 服务帐户   。 如果计算机是群集中的节点，请确保将“作为服务登录”用户权限分配给群集中所有节点上的群集服务帐户  。  

要将“作为服务登录”用户权限分配到计算机上的 WIEC_User 服务帐户，请遵循以下步骤   ：

1. 以管理员或管理员组成员的身份登录到计算机。
2. 运行 secpol.msc 以打开“本地安全策略”  。
3. 转到“安全设置” > “本地策略”，然后选择“用户权限分配”    。
4. 在右侧窗格中，双击“作为服务登录”  。
5. 选择“添加用户或组”，将 WIEC_USER 添加到策略，然后选择两次“确定”    。

如果“作为服务登录”用户权限曾分配给 WIEC_User，但后来被删除，请与域管理员联系以确定组策略设置是否覆盖了它   。  

## <a name="next-steps"></a>后续步骤  

以下文章可帮助解决特定错误：
- [解决 Intune Exchange Connector 的常见问题](troubleshoot-exchange-connector-common-problems.md).git 

寻求支持或 Intune 社区的帮助。
- 请参阅[获取支持](../fundamentals/get-support.md)以使用 Intune 控制台帮助排查问题或打开 Microsoft 的支持案例。 
- 请在 [Microsoft Intune 论坛](/answers/products/mem)发布问题。