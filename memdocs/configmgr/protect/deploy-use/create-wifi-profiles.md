---
title: 如何创建 Wi-Fi 配置文件
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中使用 Wi-Fi 配置文件将无线网络设置部署到组织中的用户。
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 21dffd1201b04846a9fffcdc7cc917465daa5905
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690225"
---
# <a name="create-wi-fi-profiles"></a>创建 Wi-Fi 配置文件

适用范围：  Configuration Manager (Current Branch)

在 Configuration Manager 中使用 Wi-Fi 配置文件将无线网络设置部署到组织中的用户。 通过部署这些设置，可以让用户很方便地连接到 Wi-Fi。  

例如，你有一个 Wi-Fi 网络并想让所有 Windows 笔记本电脑都能够连接到该网络。 创建 Wi-Fi 配置文件，其中包含连接到无线网络所必需的设置。 然后，将该配置文件部署到在层次结构中拥有 Windows 笔记本电脑的所有用户。 这些设备的用户可以在无线网络列表中看到网络，并且可以容易地连接到此网络。  

可以为以下 OS 版本配置 Wi-Fi 配置文件：

- Windows 8.1，32 位或 64 位

- Windows RT 8.1

- Windows 10 或 Windows 10 移动版

还可以使用 Configuration Manager 通过本地移动设备管理 (MDM) 将无线网络设置部署到移动设备。 如需详细了解基本信息，请参阅[什么是本地 MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。

在创建 Wi-Fi 配置文件时，你可以纳入各种各样的安全设置。 其中包括已通过使用 Configuration Manager 证书配置文件推送的服务器验证和客户端身份验证证书。 有关证书配置文件的详细信息，请参阅[证书配置文件](introduction-to-certificate-profiles.md)。

## <a name="create-a-wi-fi-profile"></a>创建 Wi-fi 配置文件

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区中，依次展开“符合性设置”和“公司资源访问”，然后选择“Wi-Fi 配置文件”节点     。

1. 在“主页”  选项卡上的“创建”  组中，选择“创建 Wi-Fi 配置文件”  。

1. 在“创建 Wi-Fi 配置文件向导”的“常规”  页上，指定下列信息：

    - **名称**：输入用于在控制台中标识配置文件的唯一名称。

    - **描述**：（可选）添加说明，以提供有关 Wi-Fi 配置文件的更多信息。

    - **从文件中导入现有的 Wi-Fi 配置文件项**：选择此选项以使用另一个 Wi-Fi 配置文件中的设置。 如果你选择此选项，向导的其余页面会简化为两页：“导入 Wi-Fi 配置文件”  和“支持的平台”  。

        > [!IMPORTANT]
        > 确保导入的 Wi-Fi 配置文件包含 Wi-Fi 配置文件的有效 XML。 导入文件时，Configuration Manager 不会验证该配置文件。

    - **报表的不符合性严重程度**：从下面的严重性级别中选择一个，作为设备在将 Wi-Fi 配置文件评估为不符合时报告的严重性级别。 例如，如果配置文件安装失败，则不符合。

        - **无**：对于 Configuration Manager 报表，不符合此符合性规则的设备不报告故障严重性。

        - **信息**

        - **警告**

        - **严重**

        - **严重事件**：违反此符合性规则的计算机在 Configuration Manager 报表中将故障严重性级别报告为“严重”  。 设备还会在应用程序事件日志中以 Windows 事件的形式记录不符合状态。

1. 在向导的“Wi-Fi 配置文件”页上，指定下列信息  ：

    - **网络名称**：提供设备将显示为网络名称的名称。

        > [!IMPORTANT]
        > Configuration Manager 不支持在网络名称中使用单引号 (`'`) 或逗号 (`,`) 字符。

    - **SSID**：指定无线网络 ID（区分大小写）。

    - **当此网络处于范围内则自动连接**
    - **连接到此网络时查找其他无线网络**
    - **在网络未广播其名称(SSID)时连接**

1. 在“安全配置”页上，指定以下信息  ：

    > [!IMPORTANT]
    > 如果你正在为[本地 MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) 创建 Wi-Fi 配置文件，Configuration Manager 的 Current Branch 仅支持以下 Wi-Fi 安全性配置：  
    >
    > - 安全类型：“WPA2 企业”  或“WPA2 个人”   
    > - 加密类型：“AES”  或“TKIP”   
    > - EAP 类型：“智能卡或其他证书”  或 PEAP   

    - **安全类型**：选择无线网络使用的安全协议，或者，如果网络无安全保护，请选择“无身份验证(开放式)”  。

    - **加密**：设置无线网络的加密方法（如果安全类型支持的话）。

    - **EAP 类型**：选择所选加密方法的身份验证协议。

        > [!NOTE]
        > 仅限 Windows Phone 设备：不支持 EAP 类型“LEAP”和“EAP-FAST”   。

        选择“配置”，为所选的 EAP 类型指定属性  。 对于某些所选的 EAP 类型，此选项不可用。

        > [!IMPORTANT]
        > EAP 类型配置窗口来自 Windows。 确保在支持所选 EAP 类型的计算机上运行 Configuration Manager 控制台。

    - **每次登录时记住用户凭据**：选择此选项可以存储用户凭据，这样用户就不必每次登录 Windows 都输入无线网络凭据了。

1. 在向导的“高级设置”页上，指定 Wi-Fi 配置文件的其他设置  。 高级设置可能不可用或可能会有所不同，具体情况视你在向导的“安全性配置”页上所选的选项而定  。 例如，身份验证模式或单一登录选项。

1. 在“代理设置”页上，如果无线网络使用代理服务器，请选择“配置此 Wi-Fi 配置文件的代理设置”选项   。 然后提供代理的配置信息。

1. 在“支持的平台”页上，选择此 Wi-Fi 配置文件适用的 OS 版本  。

1. 完成向导。

## <a name="next-step"></a>下一步

> [!div class="nextstepaction"]
> [如何部署 Wi-Fi 配置文件](deploy-wifi-vpn-email-cert-profiles.md)
