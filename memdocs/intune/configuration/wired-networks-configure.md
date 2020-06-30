---
title: 在 Microsoft Intune 中为 macOS 设备配置 802.1x 有线网络设置 - Azure | Microsoft Docs
titleSuffix: ''
description: 为 macOS 台式计算机设备创建或添加有线网络设备配置文件。 查看不同的设置，添加证书，选择 EAP 类型以及在 Microsoft Intune 中选择身份验证方法。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f237daa5e95cb5428e707828f0104c697e338718
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2020
ms.locfileid: "85095741"
---
# <a name="add-and-use-wired-networks-settings-on-your-macos-devices-in-microsoft-intune"></a>在 Microsoft Intune 中添加和使用 macOS 设备上的有线网络设置

众多组织使用有线网络向台式计算机授予网络访问权限。 Microsoft Intune 包括内置设置，可部署到组织中的 macOS 用户和设备。 这组设置称为“配置文件”。 在配置文件中，可以包括常见设置，例如网络接口、接受的 EAP 类型和服务器信任设置。

配置文件准备就绪后，可以将其分配给不同的用户和组。 分配后，用户有权访问组织的有线网络，而无需自行配置。

作为移动设备管理 (MDM) 解决方案的一部分，请使用此功能创建 802.1x 配置文件来管理有线网络。 然后，将这些有线网络部署到 macOS 设备。

此功能适用于：

- macOS

例如，你有一个名为“Contoso 有线网络”的有线网络。 想要将所有 macOS 台式机连接到此网络。 过程如下：

1. 创建有线网络配置文件，其中包含用于连接到“Contoso 有线网络”的设置。
2. 将配置文件分配到包含所有用户 macOS 台式计算机的组。 有关使用组类型的建议，请参阅[用户组与设备组](device-profile-assign.md#user-groups-vs-device-groups)。
3. 在其台式机上，用户在网络列表中查找“Contoso 有线网络”。 然后，他们可以使用所选的身份验证方法连接到该网络。

本文列出了创建有线网络配置文件的步骤。 它还包括描述不同设置的链接。

## <a name="create-the-profile"></a>创建配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备” > “配置文件” > “创建配置文件”。
3. 输入以下属性：

    - **平台**：选择“macOS”。
    - **配置文件**：选择“有线网络”。

4. 选择“创建”。
5. 在“基本信息”中，输入以下属性：

    - **名称**：输入配置文件的描述性名称。 为配置文件命名，以便稍后可以轻松地识别它们。 例如，配置文件名称最好是“macOS 设备上整个公司的有线网络配置文件”。
    - **描述**：输入配置文件的说明。 此设置是可选的，但建议进行。

6. 选择“下一步”。
7. 在“配置设置”中，选择网络的网络接口，然后选择“可扩展身份验证协议(EAP)”类型。 有关所有设置及其用途的列表，请参阅：

    - [macOS](wired-network-settings-macos.md)

8. 选择“下一步”。
9. 在“分配”中，选择将接收配置文件的用户组或设备组。 有关分配配置文件的详细信息，请参阅[分配用户和设备配置文件](device-profile-assign.md)。

    选择“下一步”。

10. 在“查看并创建”中查看设置。 选择“创建”时，将保存所做的更改并分配配置文件。 该策略也会显示在配置文件列表中。

> [!TIP]
> 如果对有线网络配置文件使用基于证书的身份验证，请将有线网络配置文件、证书配置文件和受信任的根配置文件部署到同一组。 此部署可确保每台设备都能识别证书颁发机构的合法性。 有关详细信息，请参阅[使用 Microsoft Intune 配置证书](../protect/certificates-configure.md)。

## <a name="next-steps"></a>后续步骤

此时，配置文件创建完成，但它可能未执行任何操作。 请务必[分配此配置文件](device-profile-assign.md)，并[监视配置文件状态](device-profile-monitor.md)。
