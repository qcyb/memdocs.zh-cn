---
title: 在 Microsoft Intune 中为 Android Enterprise 设备配置 VPN 或每应用 VPN | Microsoft Docs
titleSuffix: Microsoft Intune
description: 在 Microsoft Intune 中，使用应用配置策略为 Android Enterprise 设备添加或创建 VPN 或每应用 VPN 配置文件。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7e869ad933e86d9330dbb8d6a26b1886a71cee07
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262891"
---
# <a name="use-a-vpn-and-per-app-vpn-policy-on-android-enterprise-devices-in-microsoft-intune"></a>在 Microsoft Intune 中将 VPN 和每应用 VPN 策略用于 Android Enterprise 设备

借助虚拟专用网络 (VPN)，用户可以从家中、宾馆、咖啡馆等地远程访问组织资源。 在 Microsoft Intune 中，可以使用应用配置策略在 Android Enterprise 设备上配置 VPN 客户端应用。 然后，将此策略及其 VPN 配置部署到组织的设备中。

此外，还可以创建供特定应用使用的 VPN 策略。 此功能称为“每应用 VPN”。 应用处于活动状态时，它可以连接到此 VPN，并通过此 VPN 访问资源。 当应用未处于活动状态时，则不使用此 VPN。

此功能适用于：

- Android Enterprise

可通过两种方式为 VPN 客户端应用生成应用配置策略：

- 配置设计器
- JSON 数据

本文介绍如何使用这两种选项创建每应用 VPN 和 VPN 应用配置策略。

> [!NOTE]
> 许多 VPN 客户端配置参数都类似。 但每个应用都有其唯一的项和选项。 如有问题，请咨询你的 VPN 供应商。

## <a name="before-you-begin"></a>在开始之前

- 当应用打开时，Android 不会自动触发 VPN 客户端连接。 必须手动启动 VPN 连接。 也可以使用 [always-on VPN](../configuration/vpn-settings-android-enterprise.md) 来启动连接。

- 以下 VPN 客户端支持 Intune 应用配置策略：

  - Cisco AnyConnect
  - Citrix SSO
  - F5 Access
  - 帕洛阿尔托网络全局保护
  - 脉冲安全
  - SonicWall Mobile Connect

- 在 Intune 中创建 VPN 策略时，将选择不同的项以进行配置。 这些项名称随 VPN 客户端应用的不同而异。 因此，你的环境中的项名称可能不同于本文中的示例。

- 配置设计器和 JSON 数据可以成功使用基于证书的身份验证。 如果 VPN 身份验证需要客户端证书，则先创建证书配置文件，再创建 VPN 策略。 VPN 应用配置策略使用证书配置文件中的值。

  Android Enterprise 工作配置文件设备支持 SCEP 和 PKCS 证书。 Android Enterprise 公司拥有的完全托管式专用工作配置文件设备仅支持 SCEP 证书。 有关详细信息，请参阅[在 Microsoft Intune 中使用证书进行身份验证](../protect/certificates-configure.md)。

## <a name="per-app-vpn-overview"></a>每应用 VPN 概述

创建和测试每应用 VPN 时，基本流程包括以下步骤：

1. 选择 VPN 客户端应用程序。 [在开始之前](#before-you-begin)（在本文中）列出了支持的应用。
2. 获取将使用 VPN 连接的应用的应用程序包 ID。 [获取应用包 ID](#get-the-app-package-id)（在本文中）演示了操作方法。
3. 如果使用证书对 VPN 连接进行身份验证，则先创建和部署证书配置文件，再部署 VPN 策略。 请确保证书配置文件部署成功。 有关详细信息，请参阅[在 Microsoft Intune 中使用证书进行身份验证](../protect/certificates-configure.md)。
4. 将 [VPN 客户端应用程序](apps-add-android-for-work.md)添加到 Intune，并将此应用部署给用户和设备。
5. 创建 VPN 应用配置策略。 在策略中使用应用包 ID 和证书信息。
6. 部署新的 VPN 策略。
7. 确认 VPN 客户端应用成功连接到 VPN 服务器。
8. 此应用处于活动状态时，确认此应用的流量成功通过 VPN。

## <a name="get-the-app-package-id"></a>获取应用包 ID

获取将使用 VPN 的每个应用程序的包 ID。 对于公开发布的应用程序，可以在 Google Play 商店中获取应用包 ID。 每个应用程序显示的 URL 均包含包 ID。

在下面的示例中，Microsoft Edge 浏览器应用的包 ID 是 `com.microsoft.emmx`。 包 ID 是以下 URL 的一部分：

:::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-01.png" alt-text="在 Google Play 商店的 URL 中获取应用包 ID。":::

对于业务线 (LOB) 应用，请从供应商或应用程序开发人员处获取包 ID。

## <a name="certificates"></a>证书

本文假设 VPN 连接使用基于证书的身份验证。 此外，本文还假设你已成功部署了客户端成功进行身份验证所需的证书链中的所有证书。 通常，此证书链包括客户端证书、任何中间证书以及根证书。

有关证书的详细信息，请参阅[在 Microsoft Intune 中使用证书进行身份验证](../protect/certificates-configure.md)。

部署客户端身份验证证书配置文件时，它会在证书配置文件中创建一个证书令牌。 此令牌用于创建 VPN 应用配置策略。

如果你不熟悉如何创建应用配置策略，请参阅[为托管的 Android Enterprise 设备添加应用配置策略](app-configuration-policies-use-android.md)。

## <a name="use-the-configuration-designer"></a>使用配置设计器

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“应用” > “应用配置策略” > “添加” > “托管设备”。
3. 在“基本信息”中，输入以下属性：

    - **名称**：输入策略的描述性名称。 为策略命名，以便稍后可以轻松地识别它们。 例如，策略名称可以是“应用配置策略：**Android Enterprise 工作配置文件的 Cisco AnyConnect VPN 策略”** 。
    - **描述**：输入策略的说明。 此设置是可选的，但建议进行。
    - **平台**：选择“Android Enterprise”。
    - **配置文件类型**：选项包括：
      - 所有配置文件类型：此选项支持用户名和密码身份验证。 如果使用基于证书的身份验证，请不要使用此选项。
      - 仅限公司拥有的完全托管式专用工作配置文件：此选项支持基于证书的身份验证，以及用户名和密码身份验证。
      - 仅限工作配置文件：此选项支持基于证书的身份验证，以及用户名和密码身份验证。
    - **目标应用**：选择之前添加的 VPN 客户端应用。 以下示例中使用了 Cisco AnyConnect VPN 客户端应用：

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-02.png" alt-text="在 Microsoft Intune 中创建用于配置 VPN 或每应用 VPN 的应用配置策略":::

4. 选择“下一步”。
5. 在“设置”中，输入以下属性：

    - 配置设置格式：选择“使用配置设计器”：

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-03.png" alt-text="在 Microsoft Intune 中使用配置设计器创建应用配置 VPN 策略 - 示例。":::

    - **添加**：显示配置项的列表。 选择配置所需的所有配置项，然后选择“确定”。

      在以下示例中，我们为 AnyConnect VPN 选择了一个最小列表，包括基于证书的身份验证和每应用 VPN：
  
      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-04.png" alt-text="在 Microsoft Intune 中使用配置设计器将配置项添加到 VPN 应用配置策略 - 示例。":::

    - **配置值**：输入所选配置项的值。 请牢记，项名称随所使用的 VPN 客户端应用而不同。 在示例中所选择的项中执行相应操作：

      - 每应用 VPN 允许的应用：输入先前收集的应用包 ID。 例如：

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-06.png" alt-text="在 Microsoft Intune 中使用配置设计器将允许的应用包 ID 输入到 VPN 应用配置策略中 - 示例。":::

      - 密钥链证书别名（可选）：  将值类型从“字符串”更改为“证书”。 选择要用于 VPN 身份验证的客户端证书配置文件。 例如：

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-07.png" alt-text="在 Microsoft Intune 中使用配置设计器更改 VPN 应用配置策略中的密钥链客户端证书别名 - 示例。":::

      - **协议**：选择 VPN 的 SSL 或 IPsec 隧道协议。 
      - 连接名称：输入 VPN 连接的用户友好名称。 用户会在其设备上看到此连接名称。 例如，输入 `ContosoVPN`。
      - **主机**：输入头端路由器的主机名 URL。 例如，输入 `vpn.contoso.com`。

        :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-05.png" alt-text="在 Microsoft Intune 中使用配置设计器输入 VPN 应用配置策略的协议、连接名称和主机名 - 示例":::

6. 选择“下一步”。
7. 在“分配”中，选择 VPN 应用配置策略要分配到的组。

    选择“下一步”  。

8. 在“查看并创建”中查看设置。 选择“创建”时，将保存所做的更改，并将策略部署到组。 此策略还会显示在“应用配置策略”列表中。

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-08.png" alt-text="在 Microsoft Intune 中使用配置设计器流查看应用配置策略 - 示例。":::

## <a name="use-json"></a>使用 JSON

如果你没有或不了解配置设计器中使用的所有 VPN 必需设置，请使用此选项。 如果需要帮助，请咨询你的 VPN 供应商。

### <a name="get-the-certificate-token"></a>获取证书令牌

通过这些步骤创建一个临时策略。 不会保存此策略。 其目的是复制证书令牌。 使用 JSON 创建 VPN 策略时将使用此令牌（见下一节）。

1. 在 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“应用” > “应用配置策略” > “添加” > “托管设备”。
2. 在“基本信息”中，输入以下属性：

    - **名称**：输入任意名称。 此策略是临时的，不会保存它。
    - **平台**：选择“Android Enterprise”。
    - **配置文件类型**：选择“仅限工作配置文件”。
    - **目标应用**：选择之前添加的 VPN 客户端应用。

3. 选择“下一步”。
4. 在“设置”中，输入以下属性：

    - 配置设置格式：选择“使用配置设计器”：。
    - **添加**：显示配置项的列表。 选择“值类型”为“字符串”的任意项。  选择“确定”。

      :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-11.png" alt-text="在配置设计器中为 Microsoft Intune VPN 应用配置策略选择字符串值类型的任意项":::

5. 将值类型从“字符串”更改为“证书”  。 通过此步骤，可以选择正确的客户端证书配置文件，来对 VPN 进行身份验证：

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-12.png" alt-text="在 Microsoft Intune 中更改 VPN 应用配置策略中的连接名称 - 示例":::

6. 立即将值类型更改回“字符串” 。 配置值将更改为令牌 `{{cert:GUID}}`：

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-13.png" alt-text="在 Microsoft Intune 的 VPN 应用配置策略中配置值显示证书令牌":::

7. 将此证书令牌复制并粘贴到另一个文件中（如文本编辑器）。

8. 弃用此策略。 请不要保存它。 其唯一的用途是复制并粘贴证书令牌。

### <a name="create-the-vpn-policy-using-json"></a>使用 JSON 创建 VPN 策略

1. 在 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“应用” > “应用配置策略” > “添加” > “托管设备”。

2. 在“基本信息”中，输入以下属性：

    - **名称**：输入策略的描述性名称。 为策略命名，以便稍后可以轻松地识别它们。 例如，策略名称可以是“应用配置策略：**整个公司的 Android Enterprise 工作配置文件的 JSON Cisco AnyConnect VPN 策略”** 。
    - **描述**：输入策略的说明。 此设置是可选的，但建议进行。
    - **平台**：选择“Android Enterprise”。
    - **配置文件类型**：选项包括：
      - 所有配置文件类型：此选项支持用户名和密码身份验证。 如果使用基于证书的身份验证，请不要使用此选项。
      - 仅限公司拥有的完全托管式专用工作配置文件：此选项支持基于证书的身份验证，以及用户名和密码身份验证。
      - 仅限工作配置文件：此选项支持基于证书的身份验证，以及用户名和密码身份验证。
    - **目标应用**：选择之前添加的 VPN 客户端应用。 

3. 选择“下一步”。
4. 在“设置”中，输入以下属性：

    - 配置设置格式：选择“输入 JSON 数据”。 可以直接编辑 JSON。
    - 下载 JSON 模板：可使用此选项在任何外部编辑器中下载和更新模板。 请注意使用中文引号的文本编辑器，因为它们可能会创建无效的 JSON。

    输入配置所需的值后，删除具有 `"STRING_VALUE"` 或 `STRING_VALUE` 的所有设置。

    :::image type="content" source="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-14.png" alt-text="使用 JSON 流的示例 - 编辑 JSON。":::

5. 选择“下一步”。
6. 在“分配”中，选择 VPN 应用配置策略要分配到的组。

    选择“下一步”  。

7. 在“查看并创建”中查看设置。 选择“创建”时，将保存所做的更改，并将策略部署到组。 此策略还会显示在“应用配置策略”列表中。

#### <a name="json-example-for-f5-access-vpn"></a>F5 Access VPN 的 JSON 示例

``` JSON
{
    "kind": "androidenterprise#managedConfiguration",
    "productId": "app:com.f5.edge.client_ics",
    "managedProperty": [
        {
            "key": "disallowUserConfig",
            "valueBool": false
        },
        {
            "key": "vpnConfigurations",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "name",
                            "valueString": "MyCorpVPN"
                        },
                        {
                            "key": "server",
                            "valueString": "vpn.contoso.com"
                        },
                        {
                            "key": "weblogonMode",
                            "valueBool": false
                        },
                        {
                            "key": "fipsMode",
                            "valueBool": false
                        },
                        {
                            "key": "clientCertKeychainAlias",
                            "valueString": "{{cert:77333880-14e9-0aa0-9b2c-a1bc6b913829}}"
                        },
                        {
                            "key": "allowedApps",
                            "valueString": "com.microsoft.emmx"
                        },
                        {
                            "key": "mdmAssignedId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmInstanceId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceUniqueId",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceWifiMacAddress",
                            "valueString": ""
                        },
                        {
                            "key": "mdmDeviceSerialNumber",
                            "valueString": ""
                        },
                        {
                            "key": "allowBypass",
                            "valueBool": false
                        }
                    ]
                }
            ]
        }
    ]
}
```

## <a name="additional-information"></a>其他信息

- [为托管的 Android Enterprise 设备添加应用配置策略](app-configuration-policies-use-android.md)
- [用于在 Intune 中配置 VPN 的 Android Enterprise 设备设置](../configuration/vpn-settings-android-enterprise.md)

## <a name="next-steps"></a>后续步骤

- [在 Intune 中创建 VPN 配置文件以连接到 VPN 服务器](../configuration/vpn-settings-configure.md)
