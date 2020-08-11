---
title: 在独立客户端上配置 Endpoint Protection
titleSuffix: Configuration Manager
description: 了解如何在独立客户端上配置 Endpoint Protection。
ms.date: 07/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f8d116879b0a85f3276d848b01c69d575b8b69fd
ms.sourcegitcommit: 41b2b50d5870dc127a8848a6657d56112f92515a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87758306"
---
# <a name="configure-endpoint-protection-on-a-standalone-client"></a>在独立客户端上配置 Endpoint Protection

适用范围：Configuration Manager (Current Branch)

你的组织可能有大量无法使用 Microsoft Endpoint Configuration Manager 进行管理或保护的独立客户端。 如果没有任何 Endpoint Protection，这些独立客户端将容易受到潜在恶意软件攻击。 若要保护此类独立客户端，你可以按照本主题中所述，使用 Endpoint Protection 手动配置它们。

若要在独立客户端上手动配置 Endpoint Protection，请执行以下操作：

- [为独立客户端创建反恶意软件策略](#create-an-antimalware-policy-for-the-standalone-client)
- [将 Endpoint Protection 客户端安装包传输到独立客户端](#transfer-endpoint-protection-client-installation-package-to-the-standalone-client)
- [在独立客户端上安装 Endpoint Protection](#install-endpoint-protection-on-the-standalone-client)

## <a name="prerequisites"></a>先决条件

下面是在独立客户端上配置 Endpoint Protection 的先决条件：

- 必须具有对 Endpoint Protection 客户端安装包 **scepinstall.exe** 的访问权限。 可以在 C:\Program Files\Microsoft Configuration Manager\Client 文件夹中找到此包。 
- 确保已安装 [Endpoint Protection 客户端的 2017 年 1 月反恶意软件平台更新](https://support.microsoft.com/help/3209361/january-2017-anti-malware-platform-update-for-endpoint-protection-clie)。 

## <a name="create-an-antimalware-policy-for-the-standalone-client"></a>为独立客户端创建反恶意软件策略

在此步骤中，将在 Configuration Manager 控制台中创建自定义反恶意软件策略，然后将其传输到独立客户端。

创建反恶意软件策略时，必须配置定义更新源，以使策略定义在独立客户端上保持最新。 如果你的独立客户端已连接到 Internet，则可以将定义更新源配置为 [Microsoft 更新](endpoint-definitions-microsoft-updates.md)和 [Microsoft 恶意软件防护中心](endpoint-definitions-protection-center.md)。 或者，选择[网络共享](endpoint-definitions-network.md)作为定义分发源，并使用最新的定义更新包进行定期更新。 

若要为独立客户端创建反恶意软件策略，请执行以下操作：

1. 在 Configuration Manager 控制台中单击“资产和符合性”。
2. 在“资产和符合性”  工作区中，展开“Endpoint Protection” ，然后单击“反恶意软件策略” 。
3. 在上 **主页** 选项卡上，在 **创建** 组中，单击 **创建反恶意软件策略**。
4. 在 **常规** 部分 **创建反恶意软件策略** 对话框框中，输入名称和策略的描述。
5. 在 **创建反恶意软件策略** 对话框框中，配置设置，您需要为此反恶意软件策略，然后单击 **确定**。 有关可配置的设置列表，请参阅[反恶意软件策略设置的列表](endpoint-antimalware-policies.md#list-of-antimalware-policy-settings)。
    > [!NOTE]
    > 对于“定义更新”设置，如果你的独立客户端已连接到 Internet，则选择“从 Microsoft 更新分发的更新”和“从 Microsoft 恶意软件防护中心分发的更新”。  
    > 或者，选择“来自 UNC 文件共享的更新”以通过网络共享分发策略定义。 然后，添加一个或多个指向网络共享上定义更新文件位置的 UNC 路径。

6. 将新创建的策略导出为 XML：
    1. 在“反恶意软件策略”列表中，右键单击你的策略。
    1. 选择“导出”  。
    1. 将策略另存为 XML，例如 standalone.xml。
7. 将新的反恶意软件策略 XML 传输到要在其上配置 Endpoint Protection 的目标独立客户端。

## <a name="transfer-endpoint-protection-client-installation-package-to-the-standalone-client"></a>将 Endpoint Protection 客户端安装包传输到独立客户端

在此步骤中，将从 Configuration Manager 服务器复制 Endpoint Protection 客户端安装包 (scepinstall.exe)，并将其传输到独立客户端。

1. 登录到 Configuration Manager 服务器。
2. 导航到 Configuration Manager 安装文件夹的客户端文件夹 (C:\Program Files\Microsoft Configuration Manager\Client)。
3. 复制 scepinstall.exe。
4. 将 scepinstall.exe 传输到要在其上安装 Endpoint Protection 客户端软件的目标独立客户端。

## <a name="install-endpoint-protection-on-the-standalone-client"></a>在独立客户端上安装 Endpoint Protection
在此步骤中，将从独立客户端上的命令提示符处运行安装程序包 (scepinstall.exe) 和反恶意软件策略（两者以前均从 Configuration Manager 服务器传输）。

若要在独立客户端上安装 Endpoint Protection，请执行以下操作：

1. 在独立客户端上，以管理员身份打开命令提示符。
2. 将目录更改为保存 scepinstall.exe 安装程序文件的文件夹。
3. 输入以下命令，使用反恶意软件策略运行 scepinstall.exe：

    ```cmd
    scepinstall.exe /policy <full path>\<policy file>
    ```

    将 `full path` 替换为保存反恶意软件策略 XML 文件的路径，并将 `policy file` 替换为反恶意软件策略文件名。
 
    将提取安装程序并启动安装向导。

4. 按照屏幕上的说明完成客户端安装。

    在安装向导的最后一个屏幕上，默认选择在获取最新更新后扫描计算机查找是否存在潜在威胁的选项。 可以清除该复选框以跳过扫描。

## <a name="change-antimalware-policy-settings-on-a-standalone-endpoint-protection-client"></a>在独立的 Endpoint Protection 客户端上更改反恶意软件策略设置

若要在独立的 Endpoint Protection 客户端上更改或更新反恶意软件策略，请执行以下操作： 

1. [为独立客户端创建反恶意软件策略](#create-an-antimalware-policy-for-the-standalone-client)。
2. 在独立客户端上运行以下命令：

```cmd
C:\Program Files\Microsoft Security Client\ConfigSecurityPolicy.exe <full path>\<policy file>
```

将 `full path` 替换为保存新反恶意软件策略 XML 文件的路径，并将 `policy file` 替换为反恶意软件策略文件名。

## <a name="next-steps"></a>后续步骤

有关如何使用 Endpoint Protection 管理 Configuration Manager 客户端计算机上的安全和恶意软件，请参阅[配置 Endpoint Protection](endpoint-protection-configure.md)。