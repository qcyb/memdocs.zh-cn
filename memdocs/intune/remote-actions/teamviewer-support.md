---
title: 在 Microsoft Intune 中远程管理设备 - Azure | Microsoft Docs
description: 查看使用 TeamViewer 所需的角色、如何安装 TeamViewer 连接器，以及在 Azure 门户中使用 Microsoft Intune 远程管理设备的分步指南
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 72cdd888-efca-46e6-b2e7-fb9696bb2fba
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b94146cc429f2a7f7b196f15527e8687368e6d78
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988243"
---
# <a name="use-teamviewer-to-remotely-administer-intune-devices"></a>使用 TeamViewer 远程管理 Intune 设备

可使用 [TeamViewer](https://www.teamviewer.com) 远程管理 Intune 托管的设备。 TeamViewer 是需另行购买的第三方程序。 本主题介绍如何在 Intune 中配置 TeamViewer，以及如何远程管理设备。 

## <a name="prerequisites"></a>必备条件

- 使用支持的设备。 Intune 托管 Android 设备管理、Android 工作配置文件、Windows、iOS/iPadOS 和 macOS 设备支持远程管理。 TeamViewer 可能不支持 Windows Holographic (HoloLens)、Windows Team (Surface Hub) 或 Windows 10 S。有关可支持性的信息，请参阅 [TeamViewer](https://www.teamviewer.com)，了解所有更新。

> [!NOTE]
> Android 专用设备和完全托管设备不受支持。

- Azure 门户中的 Intune 管理员必须具有以下 [Intune 角色](../fundamentals/role-based-access-control.md)：  

  - **更新远程协助**：允许管理员修改 TeamViewer 连接器设置
  - **请求远程协助**:允许管理员为任何用户发起新的远程协助会话。 具有此角色的用户不受作用域内任何 Intune 角色的限制。 此外，获得了作用域内某一 Intune 角色的用户或设备组也可以请求远程协助。 

- 具有登录凭据的 [TeamViewer](https://www.teamviewer.com) 帐户。 只有一些 TeamViewer 许可证可能支持与 Intune 集成。 有关 TeamViewer 特定的需求，请参阅 [TeamViewer 集成合作伙伴：Microsoft Intune](https://www.teamviewer.com/integrations/microsoft-intune/)。

通过 TeamViewer，可以让 Intune TeamViewer 连接器创建 TeamViewer 会话，读取 Active Directory 数据并保存 TeamViewer 帐户访问令牌。

## <a name="configure-the-teamviewer-connector"></a>配置 TeamViewer 连接器

要向设备提供远程协助，请按照以下步骤配置 Intune TeamViewer 连接器：

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“租户管理” > “连接器和令牌” > “TeamViewer 连接器”    。
3. 选择“连接”  ，然后接受许可协议。
4. 选择“登录到 TeamViewer 并授权”  。
5. 随即一个 Web 页面将打开 TeamViewer 网站。 输入 TeamViewer 许可证凭据，然后单击“登录”  。

## <a name="remotely-administer-a-device"></a>远程管理设备

配置连接器后，即可远程管理设备。 请使用以下步骤： 

1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中。
2. 依次选择“设备”和“所有设备”   。
3. 从列表中，选择想要远程管理的设备>“…” > “新远程协助会话”   。
4. 将 Intune 连接到 TeamViewer 服务后，将看到设备的一些相关信息。 选择“连接”  可开始远程会话。

![使用 TeamViewer 远程管理 Android 设备 - 示例](./media/teamviewer-support/android-teamviewer.png)

启动远程会话时，用户会在设备的公司门户应用图标上看到通知标志。 打开应用时也会显示通知。 然后，用户即可接受远程协助请求。

> [!NOTE]
> 使用“无用户”方法（如设备注册管理器 (DEM) 和 Windows 配置设计器 (WCD)）注册的 Windows 设备不会在公司门户应用中显示 TeamViewer 通知。 在这些情况下，建议使用 TeamViewer 门户生成会话。

在 TeamViewer 中，可对设备完成一系列操作，包括控制该设备。 有关可执行操作的详细信息，请参阅 [TeamViewer 指南](https://www.teamviewer.com/support/documents/)。

完成后，关闭 TeamViewer 窗口。
