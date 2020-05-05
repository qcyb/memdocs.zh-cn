---
title: 规划本地 MDM
titleSuffix: Configuration Manager
description: 规划本地移动设备管理以在 Configuration Manager 中管理移动设备
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5690e4fe003939d00dee1185e6f6551813c346e5
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724691"
---
# <a name="plan-for-on-premises-mdm-in-configuration-manager"></a>在 Configuration Manager 中规划本地 MDM

适用范围：  Configuration Manager (Current Branch)

计划在 Configuration Manager 中实现本地移动设备管理（MDM）时，有几个关键领域要查看：

- 支持的设备和操作系统版本
- 所需站点系统角色
- 安全通信
- 设备注册

> [!IMPORTANT]
> 当站点或任何移动设备未连接到 Microsoft Intune 时，你的组织仍需要 Intune 许可证才能使用此功能。 有关详细信息，请参阅[Microsoft Intune 许可](https://docs.microsoft.com/intune/fundamentals/licenses)。

准备 Configuration Manager 基础结构来处理本地 MDM 之前，请考虑以下要求。

## <a name="supported-devices"></a><a name="bkmk_devices"></a> 支持的设备  

Configuration Manager 的 current branch 支持在本地移动设备管理中为运行 Windows 10 的设备进行注册。 这些设备类型主要包括便携式计算机、IoT 和 Surface Hub。 有关特定版本的详细信息和列表，请参阅[客户端和设备支持的操作系统版本](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS)。

## <a name="site-system-roles"></a><a name="bkmk_roles"></a> 站点系统角色

本地 MDM 至少需要以下站点系统角色之一：

- **注册代理点** ，用于支持注册请求。

- **注册点** ，用于支持设备注册。

- **设备管理点** ，用于策略传递。 此角色是管理点的变体，但允许移动设备管理。

- **分发点** ，用于内容传递。

根据组织的需要，你可以将这些角色安装在单个服务器上，也可以在不同的服务器上单独安装。

> [!NOTE]
> 需要将用于本地 MDM 的每个角色配置为 HTTPS 终结点，以便与受信任的设备通信。 有关详细信息，请参阅 [所需受信任的通信](#bkmk_trustedComs)。

有关更多常规信息，请参阅[规划站点系统服务器和角色](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)。

## <a name="trusted-communications"></a><a name="bkmk_trustedComs"></a>可信通信

本地 MDM 要求你启用站点系统角色以进行 HTTPS 通信。 根据你的需要，你可以使用组织的证书颁发机构（CA）在服务器和设备之间建立可信连接。 你还可以使用公开发布的 CA 作为受信任的颁发机构。 无论采用哪种方式，都需要配置以下证书：

- 承载所需站点系统角色的服务器上的 IIS 中的**web 服务器证书**。 如果一台服务器托管多个站点系统角色，则只需要该服务器的一个证书。 如果每个角色都在单独的服务器上，则每个服务器都需要一个单独的证书。

- 颁发 web 服务器证书的 CA 的**受信任的根证书**。 在需要连接到站点系统角色的所有设备上安装此根证书。

有关详细信息，请参阅[在本地 MDM 中为受信任通信设置证书](../get-started/set-up-certificates-on-premises-mdm.md)。

## <a name="device-enrollment"></a><a name="bkmk_enrollment"></a>设备注册

为本地 MDM 启用设备注册：

- 授予用户通过客户端设置进行注册的权限

- 为托管所需角色的站点系统服务器配置受信任的通信设备

作为用户启动的注册的替代方法，你可以设置批量注册包。 此包允许设备在无需用户干预的情况下进行注册。 将包交付给设备，然后将其设置为使用或在完成 OOBE 过程后使用。

有关详细信息，请参阅[为本地 MDM 设置设备注册](../get-started/set-up-device-enrollment-on-premises-mdm.md)。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [安装站点系统角色](../get-started/install-site-system-roles-for-on-premises-mdm.md)
