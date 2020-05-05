---
title: 为本地 MDM 设置注册
titleSuffix: Configuration Manager
description: 向用户授予在 Configuration Manager 中为本地移动设备管理（MDM）注册设备的权限。
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 9ffaea91-1379-4b86-9953-b25e152f56a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c8213fac603d69e0f2afd31631e61ad301090f6
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724681"
---
# <a name="set-up-device-enrollment-for-on-premises-mdm-in-configuration-manager"></a>在 Configuration Manager 中为本地 MDM 设置设备注册

适用范围：  Configuration Manager (Current Branch)

设置本地移动设备管理（MDM）的最后一步是使用户能够注册其设备。 使用 Configuration Manager 客户端设置向用户授予在本地 MDM 中注册设备的权限。

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createProf"></a> 创建注册配置文件

若要推送允许用户注册移动设备所需的设置，请将新的注册配置文件添加到默认的客户端设置。 此配置文件将应用到 Configuration Manager 站点中的所有用户。

> [!NOTE]
> 此过程使用**默认的客户端设置**，这些设置将自动应用于所有设备和用户。 或者，您可以创建自定义客户端设置，然后将其部署到所选的集合。 此替代方法需要至少两个自定义客户端设置，一个用于 "*设备*设置"，一个用于 "*用户*设置"。 有关详细信息，请参阅[如何配置客户端设置](../../core/clients/deploy/configure-client-settings.md)。

1. 在 Configuration Manager 控制台中，打开 "**管理**" 工作区，然后选择 "**客户端设置**" 节点。 打开 "**默认客户端设置**" 并选择 "**注册**" 组。

1. 在 "设备设置" 下，指定**新式设备的轮询间隔（分钟）**。 默认情况下，此间隔为60分钟。

1. 在 "用户设置" 下，启用 "**允许用户注册新式设备**" 选项。

1. 对于**新式设备注册配置文件**，请选择 "**设置配置文件**"。 在 "注册配置文件" 窗口中，选择 "**创建**"。

1. 在 "创建注册配置文件" 窗口中，指定以下信息：

    - 注册配置文件的唯一的描述性**名称**。

    - 提供有关配置文件的附加信息的可选**说明**。

    - 选择包含设备管理点的**管理站点代码**。 选择 **"确定"** 以保存并关闭。

## <a name="configure-additional-client-settings"></a><a name="bkmk_addClient"></a>配置其他客户端设置

注册设备后，还可以通过其他客户端设置来配置设备。 有关更多常规信息，请参阅[如何配置客户端设置](../../core/clients/deploy/configure-client-settings.md)。

Configuration Manager 支持用于本地 MDM 的以下客户端设置：

- **客户端策略**：这些设置指定将客户端策略下载到设备的频率。 你还可以对用户策略启用设置。 有关详细信息，请参阅[关于客户端设置-客户端策略](../../core/clients/deploy/about-client-settings.md#client-policy)。

- **软件部署**：设置评估软件部署的时间间隔。 有关详细信息，请参阅[关于客户端设置-软件部署](../../core/clients/deploy/about-client-settings.md#software-deployment)。

    > [!NOTE]
    > 对于本地 MDM，软件部署设置只能用作默认客户端设置。

## <a name="discover-users"></a><a name="bkmk_enableUsers"></a>发现用户

为了使用户能够接收包含本地 MDM 注册配置文件的客户端设置，站点将发现其用户帐户 Active Directory。 为了确保需要注册配置文件的每个人能够获得它，请运行对 Active Directory 用户运行发现。 有关详细信息，请参阅[Active Directory 用户发现](../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)。

## <a name="install-the-trusted-root-certificate"></a><a name="bkmk_storeCert"></a>安装受信任的根证书

已加入域的设备会获得与宿主站点系统角色的服务器进行信任的通信的信任根证书。 Active Directory 证书服务自动分发受信任的根证书。 未加入域的计算机和移动设备需要通过其他方式安装此证书以允许注册。

> [!NOTE]
> 如果 web 服务器证书由公共证书颁发机构颁发，则大多数设备已信任这些 Ca。 如果你的设计包括使用其中一个公共 Ca，则无需执行此步骤。

[导出受信任的根证书](set-up-certificates-on-premises-mdm.md#bkmk_exportCert)后，需要将其安装在要注册的设备上。 例如，未加入域并且无法从 Active Directory 中自动获取的设备。 你使用的进程将取决于以下因素：

- 特定设备类型和技术功能
- OS 版本
- 你的业务、安全和用户体验要求

下面的列表包含在设备上传递和安装受信任的根证书的一些示例方法：

- 文件共享

- 电子邮件附件

- 内存卡

- 受限设备

- 云存储（例如 OneDrive）

- 近场通信 (NFC) 连接

- 条形码扫描程序

- 现成体验 (OOBE) 预配包

### <a name="manually-install-the-trusted-root-certificate-in-windows"></a>在 Windows 中手动安装受信任的根证书

1. 在要注册的设备上，在 "文件资源管理器" 中浏览到受信任的根证书文件（.cer），然后将其**打开**。

1. 在 "证书" 窗口中，选择 "**安装证书**"。

1. 在证书导入向导中，选择 "**本地计算机**"，然后选择 "**下一步**" 以管理员身份继续。

1. 在 "证书存储" 页上，选择 **"将所有证书放入下列存储**"，然后选择 "**浏览**"。

1. 在 "选择证书存储" 窗口中，选择 "**受信任的根证书颁发机构**"，然后选择 **"确定"**。

1. 完成和向导。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [注册设备](../deploy-use/enroll-devices-on-premises-mdm.md)
