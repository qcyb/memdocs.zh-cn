---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 06/29/2020
ms.openlocfilehash: 26bfbe7b7cabef8c8dee56077b924b69c4c5886a
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590520"
---
### <a name="azure-ad-authentication-doesnt-work"></a><a name="ki_auth"></a>Azure AD 身份验证不起作用
<!--7569264-->
Configuration Manager 无法正常使用 Azure Active Directory (Azure AD) 安全令牌服务。 管理点上的 **CCM_STS.log** 包含类似于以下错误的条目：`ProcessRequest - Exception: System.IO.FileLoadException: Could not load file or assembly 'System.IdentityModel.Tokens.JWT.`它还包括 HRESULT 0x80131040。

另一个症状是云管理网关 (CMG) 出现问题。 如果运行 CMG 连接分析器，它将无法测试管理点的 CMG 通道，并出现以下错误：`Failed to get ConfigMgr token with Azure AD token. Status code is '500' and status description is 'CMGConnector_InternalServerError'.`

此问题是由支持库的版本差异导致的。

要解决此问题，请将 System.IdentityModel.Tokens.JWT.dll 从站点服务器安装目录的 \bin\X64 文件夹中复制到管理点上的 SMS_CCM\CCM_STS\bin 文件夹。
