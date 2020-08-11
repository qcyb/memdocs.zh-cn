---
title: 使用组策略管理 Endpoint Protection
titleSuffix: Configuration Manager
description: 了解如何使用组策略管理 Endpoint Protection。
ms.date: 08/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6c43ca9e1007c62835015a8c26a478af7da34ebb
ms.sourcegitcommit: c1afc8abd0d7da48815bd2b0e45147774c72c2df
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2020
ms.locfileid: "87819987"
---
# <a name="use-group-policy-settings-to-manage-endpoint-protection-in-previous-versions-of-windows"></a>使用组策略设置管理以前版本的 Windows 中的 Endpoint Protection

**适用对象：**

- [Microsoft Defender 高级威胁防护 (Microsoft Defender ATP)](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE2O8jv)
- 以下下级设备上的 System Center Endpoint Protection：
    - Windows Server 2012 R2
    - Windows 8.1
    - Windows Server 2012
    - Windows 8
    - Windows Server 2008 R2 SP1
    - Windows 7 SP1
    - Windows Server 2008 SP2
    - Windows Vista

你可能具有大量通过 Endpoint Protection 启用但超出 Configuration Manager 层次结构的下级或旧版 Windows 设备。 例如，位于外围安全区域中的设备或通过合并和收购集成的设备。 

你可以使用组策略设置在此类设备中管理 Endpoint Protection，如下所述：

- [复制 Endpoint Protection 策略定义](#copy-endpoint-protection-policy-definitions)
- 将 Endpoint Protection 策略定义加载到以下任何位置：
    - [域控制器上的中央存储（推荐）](#load-endpoint-protection-group-policy-settings-into-a-central-store-on-a-domain-controller)
    - [本地设备](#load-endpoint-protection-group-policy-settings-into-your-local-device)

> [!NOTE]
> 有关如何使用组策略设置管理 Windows 10、Windows Server 2019 和 Windows Server 2016 中的 Microsoft Defender 防病毒的信息，请参阅[使用组策略设置配置和管理 Microsoft Defender 防病毒](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-antivirus/use-group-policy-microsoft-defender-antivirus)。

## <a name="copy-endpoint-protection-policy-definitions"></a>复制 Endpoint Protection 策略定义

在由 Endpoint Protection 管理的下级 Windows 设备上，复制 Endpoint Protection 策略定义文件。

1. 转到 C:\Program Files\Microsoft Security Client\Admx。 

2. 将以下文件压缩为 zip 文件，例如 SCEP_admx.zip：
    - EndPointProtection.adml
    - EndPointProtection.admx
3. 将 zip 文件复制到临时文件夹中。 例如，C:\temp_SCEP_GPO_admx。
4. 将该文件解压缩。 

> [!NOTE]
> 用于配置 Endpoint Protection 策略设置的注册表项位于 Hkey_Local_Machine\Software\Policies\Microsoft\Microsoft Antimalware。

## <a name="load-endpoint-protection-group-policy-settings-into-a-central-store-on-a-domain-controller"></a>将 Endpoint Protection 组策略设置加载到域控制器上的中央存储中

如果你使用的是[组策略管理模板的中央存储](https://support.microsoft.com/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra)，请执行以下步骤以加载和配置 Endpoint Protection 组策略设置。 这是建议的方法。

1. 转到提取 Endpoint Protection 策略定义文件的文件夹。
2. 将 .admx 和 .adml 文件复制到域控制器上的 PolicyDefinitions 文件夹中：
    1. 将 EndPointProtection.admx 复制到 \\\\\<forest.root\>\\SYSVOL\\\<domain\>\\Policies\\PolicyDefinitions 中。 
    2. 将 EndPointProtection.adml 复制到 \\\\\<forest.root\>\\SYSVOL\\\<domain\>\\Policies\\PolicyDefinitions\\en-US 中。  

    例如：
    
    - 将 EndPointProtection.admx 复制到 \\DC\SYSVOL\contoso.com\Policies\PolicyDefinitions 中。
    - 将 EndPointProtection.adml 复制到 \\DC\SYSVOL\contoso.com\Policies\PolicyDefinitions\en-US 中。
    
    其中 DC 是域控制器的名称，contoso.com 是你的域。

3. 打开[组策略管理控制台](https://docs.microsoft.com/internet-explorer/ie11-deploy-guide/group-policy-and-group-policy-mgmt-console-ie11)并在域中创建新的组策略对象 (GPO)，例如 Endpoint Protection。
4. 右键单击 Endpoint Protection 的 GPO，然后单击“编辑”。
5. 在“组策略管理编辑器”中，转到“计算机配置” > “策略” > “管理模板: 策略定义” > “Windows 组件” > “Endpoint Protection”。

   将显示 Endpoint Protection 组策略的列表。

6. 展开包含要配置的设置的部分，双击设置将其打开，并进行配置更改。

## <a name="load-endpoint-protection-group-policy-settings-into-your-local-device"></a>将 Endpoint Protection 组策略设置加载到本地设备中

你可以将 Endpoint Protection 策略定义本地存储到设备中，而不是使用中央存储来加载这些定义。

1. 转到提取 Endpoint Protection 策略定义文件的文件夹。
2. 将 .admx 和 .adml 文件复制到本地 PolicyDefinitions 文件夹。
    1. 将 EndPointProtection.admx 复制到 %SystemRoot%/PolicyDefinitions 中。 
    2. 将 EndPointProtection.adml 复制到 %SystemRoot%/PolicyDefinitions/en-US 中。
    
    例如：

    - 将 EndPointProtection.admx 复制到 C:\Windows\PolicyDefinitions 中。
    - 将 EndPointProtection.adml 复制到 C:\Windows\PolicyDefinitions\en-US 中。
    
3. 打开“本地组策略编辑器”。
4. 转到“计算机配置” > “管理模板” > “Windows 组件” > “Endpoint Protection”。

    将显示 Endpoint Protection 组策略的列表。

5. 展开包含要配置的设置的部分，双击设置将其打开，并进行配置更改。

## <a name="next-steps"></a>后续步骤
- 有关 Endpoint Protection 的概述，请参阅 [Endpoint Protection](endpoint-protection.md)。
- 有关在独立客户端上手动配置 Endpoint Protection 的信息，请参阅[在独立客户端上配置 Endpoint Protection](endpoint-protection-configure-standalone-client.md)。
