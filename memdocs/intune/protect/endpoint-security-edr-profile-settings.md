---
title: Intune 终结点安全终结点检测和响应设置 | Microsoft Docs
description: Microsoft Intune 中的终结点安全终结点检测和响应策略设置
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/22/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: dd53ec47435ba9dc416d2b152719b393d1647f90
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2020
ms.locfileid: "83823990"
---
# <a name="endpoint-detection-and-response-policy-settings-for-endpoint-security-in-intune"></a>Intune 中的终结点安全终结点检测和响应策略设置

查看可以在 Intune 终结点安全节点[终结点检测和响应策略](../protect/endpoint-security-edr-policy.md)配置文件中配置的设置。

受支持的平台和配置文件：

- **Windows 10 及更高版本**：使用此平台可将策略部署到由 Intune 管理的设备。
  - 配置文件：终结点检测和响应 (MDM)

- **Windows 10 和 Windows Server**：使用此平台可将策略部署到由 Configuration Manager 管理的设备。
  - 配置文件：终结点检测和响应 (ConfigMgr)（预览）
  
  此平台和配置文件以提供公共预览版。

## <a name="endpoint-detection-and-response-mdm"></a>终结点检测和响应 (MDM)

**终结点检测和响应**：

- Microsoft Defender ATP 客户端配置包类型

  上传将用于加入 Microsoft Defender ATP 客户端的已签名配置包。

  - **未配置**（默认）
  - **加入 blob**  
  - **登出 blob**  

  设置为“加入 blob”时，可以配置以下设置：

  - 高级威胁防护加入 blob  
    单击“选择加入文件”打开“选择加入文件”窗格，在其中指定 `.onboarding` 文件。

  设置为“登出 blob”时，可以配置以下设置：
  
  - 高级威胁防护登出 blob  
     单击“选择登出文件”打开“选择登出文件”窗格，在其中指定 `.offboarding` 文件。

- **所有文件的示例共享**  

  返回或设置 Microsoft Defender 高级威胁防护示例共享配置参数。  
  - **未配置**（默认）
  - **是**

- **加快遥测报告频率**

  - **未配置**（默认）
  - **是** - 提高 Microsoft Defender 高级威胁防护遥测报告频率。

## <a name="endpoint-detection-and-response-configmgr-preview"></a>终结点检测和响应 (ConfigMgr)（预览）

**终结点检测和响应**：

- **所有文件的示例共享**  

  返回或设置 Microsoft Defender 高级威胁防护示例共享配置参数。  
  - **未配置**（默认）
  - **是**

- **加快遥测报告频率**

  - **未配置**（默认）
  - **是** - 提高 Microsoft Defender 高级威胁防护遥测报告频率。

## <a name="next-steps"></a>后续步骤

[EDR 的终结点安全策略设置](../protect/endpoint-security-edr-policy.md)
