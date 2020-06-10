---
title: 配置适用于 Android Enterprise 设备的 VPN
titleSuffix: Microsoft Intune
description: 使用应用保护策略 TOC 配置适用于 Android Enterprise 设备的 VPN。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/01/2020
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
ms.openlocfilehash: bcb7bd506d92befa3c73faf7270de28765f5b192
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347413"
---
# <a name="configure-a-vpn-for-android-enterprise-devices"></a>配置适用于 Android Enterprise 设备的 VPN

本主题介绍如何创建应用配置策略，使其可以与 Android Enterprise 设备上的 VPN 客户端一起部署。 此配置将允许所选应用程序的网络流量访问公司资源。

> [!NOTE]
> 打开所选应用程序之一时，Android 平台当前不支持自动触发 VPN 客户端连接。 必须先手动启动 VPN 连接，也可使用[始终可用 VPN](../configuration/vpn-settings-android-enterprise.md)。

若要创建配置策略以实现成功的 VPN 访问，必须满足以下先决条件：所选 VPN 客户端必须支持托管应用程序配置文件。 当前，支持 Intune 应用配置策略的 VPN 客户端包括：
- Cisco AnyConnect
- Citrix SSO
- F5 Access
- Palo Alto Global Connect
- 脉冲安全
- SonicWall Mobile Connect

如果对 VPN 终结点进行身份验证访问的方法要求使用客户端证书，则应提前创建证书配置文件，以帮助填充应用配置策略的必需值。

> [!NOTE]
> 虽然 Android Enterprise 工作配置文件方案同时支持 SCEP 和 PKCS 证书，但 Android Enterprise 设备所有者方案目前仅支持 SCEP 证书。 

创建和测试每应用 VPN 配置文件的基本流程如下：
1.  为基础结构选择相应的 VPN 客户端应用程序。
2.  标识要与 VPN 连接一起使用的生产力应用的应用程序包 ID。
3.  部署满足 VPN 连接的身份验证要求所需的任何证书配置文件。 请确保验证部署是否成功。
4.  部署 VPN 客户端应用程序。
5.  使用在先前步骤中收集的信息为基于应用配置的 VPN 配置文件做准备。
6.  部署新创建的 VPN 配置文件。
7.  验证 VPN 客户端应用是否能够成功连接到 VPN 服务器基础结构。
8.  验证来自所选生产力应用的流量在其处于活动状态时是否成功传输 VPN。

## <a name="get-the-app-package-id"></a>获取应用包 ID

标识要授予其 VPN 访问权限的每个应用程序的包 ID。 对于公开可用的应用程序，请考虑获取 Google Play 商店中每个应用程序的包 ID。 每个应用程序显示的 URL 均包含包 ID。 例如，Android 版本 Microsoft Edge 浏览器的包 ID 为 `com.microsoft.emmx`。 包 ID 作为 URL 的一部分包含其中。

![查找应用包 ID 的示例。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-01.png)

对于业务线 (LOB) 应用，请让你的供应商或应用程序开发团队提供相关的包 ID。

## <a name="certificates"></a>证书

在本主题中，我们假设你的 VPN 连接将使用基于证书的身份验证，且你已成功部署了使客户端身份验证成功所需的链中的所有证书。 通常，这将包括客户端证书、任何中间证书以及根证书。
有关 Android Enterprise 证书部署的其他信息，请先查看主题[在 Microsoft Intune 中使用证书进行身份验证](../protect/certificates-configure.md)。

部署客户端身份验证证书配置文件后，需要一些有关该配置文件的详细信息，以生成 VPN 应用配置策略。
如果你不熟悉如何创建应用配置文件，请参阅主题[为托管的 Android Enterprise 设备添加应用配置策略](../apps/app-configuration-policies-use-android.md)。
 

## <a name="build-the-vpn-profile"></a>生成 VPN 配置文件

可通过两种方式为 VPN 应用生成应用配置策略。 可使用“配置设计器”或“JSON 数据”选项 。 如果配置设计器方法中未提供所需的所有设置，则需要 JSON 数据选项 。 如果你确定需要 JSON 选项以获得支持，请咨询你的 VPN 供应商。 在本主题中，我们将演示这两种方法的示例。 在 JSON 数据和配置设计器这两种方法中，你都可以成功合并基于证书的身份验证 。 使用 JSON 数据方法时，可以首先使用配置设计器提取必要的配置文件值 。

> [!NOTE]
> 尽管许多 VPN 客户端配置参数都很相似，但每个应用都具有其独特的项和选项。 如果出现问题，请咨询你的 VPN 供应商。 

## <a name="use-the-configuration-designer-flow"></a>使用配置设计器流

1.  首先为受管理设备添加新的应用配置策略。
2.  输入相应的名称。
3.  选择“Android Enterprise”作为平台。
4.  如果需要基于证书的身份验证，请选择“仅限工作配置文件”或“仅限设备所有者”作为配置文件类型 。 工作所有者和设备所有者配置文件与基于证书的身份验证不兼容。
5.  对于目标应用，请选择已部署的 VPN 客户端；在此示例中，我们使用先前部署的 Cisco AnyConnect VPN 客户端

  ![创建应用配置策略的示例 - 基本信息。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-02.png)

6. 在下一页上，使用“配置设置”下拉菜单，然后选择“使用配置设计器”选项。

  ![使用配置设计器流的示例 - 设置。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-03.png)

7. 单击“添加”以显示配置项列表。
8.  选择所选配置所需的所有配置项。 在本示例中，我们使用一个最小列表为 AnyConnect VPN 进行设置，包括基于证书的身份验证和每应用 VPN。
  
  <img alt="Example of using the Configuration Designer Flow - Configuration keys." src="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-04.png" width="350">

9. 为“连接名称”、“主机”和“协议”项输入相应的值  。

  ![使用配置设计器流的示例 - 配置项选择。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-05.png)  

  > [!NOTE]
  > 这些项的名称可能不同，具体取决于为其生成策略的 VPN 客户端应用程序。

10. 输入先前在“每个应用 VPN 所允许的应用”项中收集的应用程序包 ID。

  ![使用配置设计器流的示例 - 应用程序包 ID。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-06.png)  

11. 在“KeyChain 证书别名”（可选）中，将值类型从“字符串”切换为“证书”，这将使你能够选择要用于 VPN 身份验证的正确客户端证书配置文件   。

  ![使用配置设计器流的示例 - 更新 KeyChain 证书别名。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-07.png)  

12. 在下一页上，选择任何相应的范围标记。
13. 在下一页上，输入要向其部署应用配置策略的相应组。
14. 选择“创建”以完成策略的创建和部署。

  ![使用配置设计器流的示例 - 查看。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-08.png)  

## <a name="use-the-json-flow"></a>使用 JSON 流

创建临时配置文件：
1.  首先为受管理设备添加新的应用配置策略。
2.  输入相应的名称（此配置文件的使用是临时的，因为它不会保存）。
3.  选择“Android Enterprise”作为平台。
4.  对于目标应用，选择已部署的 VPN 客户端。
5.  如果需要基于证书的身份验证，请选择“仅限工作配置文件”或“仅限设备所有者”作为配置文件类型 。 工作所有者和设备所有者配置文件与基于证书的身份验证不兼容。

  ![使用 JSON 流的示例 - 基本信息。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-09.png)  

6.  在下一页上，使用“配置设置”下拉菜单，然后选择“使用配置设计器”选项 。

  ![使用 JSON 流的示例 - 配置设置格式。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-10.png)  

7.  单击“添加”以显示配置项列表。
8.  选择值类型“字符串”中的任一项，然后单击“确定”  。

  <img alt="Example of using the JSON Flow - Select a key." src="./media/app-configuration-vpn-ae/app-configuration-vpn-ae-11.png" width="350">

9.  现在，将值类型从“字符串”更改为“证书”  。 这将使你能够选择要用于 VPN 身份验证的正确客户端证书配置文件。

  ![使用 JSON 流的示例 - 连接名称。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-12.png)  

10. 立即将值类型更改回“字符串” 。 请注意，配置值将更改为格式为 `{{cert:GUID}}` 的令牌。
11. 选择证书的令牌表示形式并将其复制到其他位置，例如文本编辑器。

  ![使用 JSON 流的示例 - 配置值。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-13.png)  

12. 放弃正在创建的配置文件 – 前面步骤的唯一目的是确定证书令牌。

### <a name="create-the-vpn-profile"></a>创建 VPN 配置文件

1.  首先为受管理设备添加新的应用程序配置文件。
2.  输入相应的名称。
3.  选择“Android Enterprise”作为平台。
4.  对于目标应用，选择已部署的 VPN 客户端。
5.  如果需要基于证书的身份验证，请选择“仅限工作配置文件”或“仅限设备所有者”作为配置文件类型 。 工作所有者和设备所有者配置文件与基于证书的身份验证不兼容。
6.  使用“配置设置”下拉菜单，然后选择“输入 JSON 数据”选项 。
7.  你可以直接编辑 JSON，也可以根据需要使用“下载 JSON 模板”按钮进行下载，然后在所选外部编辑器中修改模板。 请小心可选择使用智能引号的文本编辑器，因为将其包括在内会导致 JSON 无效。

  ![使用 JSON 流的示例 - 编辑 JSON。](./media/app-configuration-vpn-ae/app-configuration-vpn-ae-14.png)  

8.  无论使用哪种方法，填充所需配置所需的值后，必须删除整个 JSON 中具有“STRING_VALUE”或 STRING_VALUE 值的所有剩余设置。

#### <a name="example-json-for-f5-access-vpn"></a>F5 Access VPN 的 JSON 示例

下面是用于 F5 Access VPN 的 JSON 数据示例。

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

## <a name="summary"></a>“摘要”

使用适用于 Android Enterprise 注册设备的应用配置策略可使你利用每应用的 VPN 行为，尽管该行为在平台中没有直接支持。 

## <a name="additional-information"></a>其他信息

有关相关信息，请参阅以下主题：
- [为托管的 Android Enterprise 设备添加应用配置策略](../apps/app-configuration-policies-use-android.md)
- [用于在 Intune 中配置 VPN 的 Android Enterprise 设备设置](../configuration/vpn-settings-android-enterprise.md)

## <a name="next-steps"></a>后续步骤

- [在 Intune 中创建 VPN 配置文件以连接到 VPN 服务器](../configuration/vpn-settings-configure.md)
