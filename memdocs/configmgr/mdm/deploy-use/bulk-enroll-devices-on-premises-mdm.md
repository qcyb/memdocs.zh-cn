---
title: 如何批量注册设备
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 中的本地移动设备管理（MDM）以自动方式批量注册设备。
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b36f5e4a-2b57-4d18-83f6-197081ac2a0a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bfe2d395187f8af86e2d09156a45f7398a5bc670
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724611"
---
# <a name="how-to-bulk-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>如何在 Configuration Manager 中向本地 MDM 批量注册设备

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 本地移动设备管理（MDM）中的批量注册是一种自动注册设备的方法。 另一种方法是用户注册，要求用户输入其凭据来注册设备。 批量注册使用注册程序包在注册过程中对设备进行身份验证。 此包是一个 ppkg 文件，它还可以包含用于支持注册的证书和 Wi-fi 配置文件。

## <a name="create-a-certificate-profile"></a><a name="bkmk_createCert"></a> 创建证书配置文件

包含一个证书配置文件，用于在设备上自动安装受信任的根证书。 在设备和本地 MDM 所需的站点系统角色之间进行受信任的通信需要此根证书。

为本地 MDM 准备站点时，将导出受信任的根证书。 在注册程序包的证书配置文件中使用此证书。 有关如何获取受信任的根证书的详细信息，请参阅[导出受信任的根证书](../get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert)。

使用导出的证书创建证书配置文件。 有关详细信息，请参阅[如何创建证书配置文件](../../protect/deploy-use/create-certificate-profiles.md)。

## <a name="create-a-wi-fi-profile"></a><a name="CreateWifi"></a> 创建 Wi-Fi 配置文件

大容量注册包的另一个组件是 Wi-fi 配置文件。 此配置文件可确保设备具有连接到的网络连接以支持注册。

有关如何在 Configuration Manager 中创建 Wi-fi 配置文件的详细信息，请参阅[如何创建 wi-fi 配置文件](../../protect/deploy-use/create-wifi-profiles.md)。

### <a name="wi-fi-profile-limitations"></a>Wi-fi 配置文件限制

为本地 MDM 批量注册创建 Wi-fi 配置文件时，请查看以下限制。

#### <a name="wi-fi-security-configurations-for-on-premises-mdm"></a>用于本地 MDM 的 wi-fi 安全配置

Configuration Manager 的 current branch 仅支持以下本地 MDM Wi-fi 安全配置：

- 安全类型：“WPA2 企业” **** 或“WPA2 个人” ****

- 加密类型：“AES” **** 或“TKIP” ****

- EAP 类型：“智能卡或其他证书” **** 或“PEAP” ****

#### <a name="proxy-server"></a>代理服务器

尽管 Configuration Manager 在 Wi-fi 配置文件中具有代理服务器信息的设置，但它不会在设备注册时配置代理。 如果需要在大容量注册的设备上设置代理服务器：

- 设备注册后，使用配置项目部署设置。

- 使用 Windows 映像和配置设计器（ICD）创建第二个包，并将其与大容量注册包一起部署。

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createEnroll"></a> 创建注册配置文件

注册配置文件允许你指定设备注册所需的设置。 这些设置包括[证书配置文件](#bkmk_createCert)和[wi-fi 配置文件](#CreateWifi)。

1. 在 Configuration Manager 控制台中，请参阅 "**资产和符合性**" 工作区，展开 "**所有公司拥有的设备**"，展开 " **Windows**"，然后选择 "**注册配置文件**" 节点。

1. 在功能区中，选择 "**创建注册配置文件**"。

1. 在 "创建注册配置文件向导" 的 "**常规**" 页上，指定下列信息：

    - **Name**：标识配置文件的唯一名称

    - **说明**：用于进一步描述配置文件的可选字段

    - **管理机构**：仅选择**本地**

1. 在 "**站点分配**" 页上，选择具有设备管理点的**管理站点代码**。

1. 在 "**选择注册代理点**" 页上，选择 "**仅 Intranet**"，然后选择一个或多个注册代理点。 设备将使用这些服务器来启动注册过程。

1. 在 "**选择受信任的根证书**" 页上，选择包含受信任的根证书的证书配置文件。

1. 在 " **wi-fi 配置文件**" 页上，选择包含要连接的设备必需的网络设置的 wi-fi 配置文件。

    > [!TIP]
    > 如果没有为注册包使用 Wi-fi 配置文件，请跳过此步骤。

1. 完成向导。

## <a name="create-an-enrollment-package"></a><a name="bkmk_createPpkg"></a>创建注册包

注册包（ppkg）是用于为本地 MDM 批量注册设备的文件。 Configuration Manager 创建此文件。 虽然你可以使用 Windows ICD 创建类似类型的程序包，但只有你在 Configuration Manager 中创建的包才能用于为本地 MDM 注册设备。 使用 Windows ICD 创建的包只能提供注册所需的用户主体名称（UPN），而不能启动实际的注册过程。

创建注册程序包的过程需要适用于 Windows 10 的 Windows 评估和部署工具包 (ADK)。 在运行 Configuration Manager 控制台的计算机上，安装最新版本的 Windows ADK。 选择**映像和配置设计器（ICD）** 功能和任何依赖项。 （此版本不需要与 Configuration Manager 站点用于操作系统部署的版本相匹配。）有关详细信息，请参阅[下载适用于 windows 10 的 WINDOWS ADK](https://docs.microsoft.com/windows-hardware/get-started/adk-install)。

1. 在 Configuration Manager 控制台中，请参阅 "**资产和符合性**" 工作区，展开 "**所有公司拥有的设备**"，展开 " **Windows**"，然后选择 "**注册配置文件**" 节点。

1. 选择现有的注册配置文件。 在功能区中，选择 "**导出**"。

1. 在 "导出注册包" 窗口中，指定以下信息：

    - **有效期（天）**：默认情况下，Configuration Manager 将注册包设置为两周后过期（14天）。 有效期到期后，不能使用包进行设备注册。 输入一个介于1和30之间的整数。

    - **包文件**：指定 ppkg 文件的本地或网络文件路径和名称。

    - **加密包**：启用此选项以对包进行密码保护。 导出包后 Configuration Manager 会显示生成的密码。 将密码复制并保存在安全的位置。 不能使用没有密码的已导出注册包。

        > [!IMPORTANT]
        > Configuration Manager 不保存密码，并且不能对其进行自定义或更改。 一旦您关闭了显示该密码的窗口，就无法检索该密码。

1. 选择“导出”  。 Configuration Manager 使用 Windows ADK 创建注册包。

Configuration Manager 跟踪有效的注册包。 在控制台中，展开 "**注册配置文件**" 节点，然后选择 "**导出的包**"。

> [!TIP]
> 如果从 Configuration Manager 控制台删除注册包，则不能使用它来注册设备。 使用此方法管理不希望其他人用于大容量注册的注册包。

## <a name="bulk-enroll-a-device"></a><a name="bkmk_getPpkg"></a>批量注册设备

你可以使用包在设备的现成体验（OOBE）过程前后注册设备。 注册包还可以作为原始设备制造商（OEM）设置包的一部分包含在内。

要使用包进行大容量注册，需要以物理方式将其传送到设备。 有多种方法取决于你的需求，例如：

- 从文件系统复制

- 附加到电子邮件

- 跨近现场通信（NFC）连接进行复制

- 从内存卡复制

- 扫描条码

- 从受限设备复制

- 包含在 OEM 设置包中

### <a name="enroll-a-device-with-bulk-enrollment-package"></a>使用批量注册包注册设备

1. 在设备上，打开 ppkg 文件。 如有必要，请以管理员身份运行。

1. Windows 询问包是否来自受信任的源，请选择 **"是"**。

注册过程将开始。

## <a name="verify-enrollment"></a><a name="bkmk_verifyEnroll"></a>验证注册

### <a name="verify-bulk-enrollment-on-the-device"></a>验证设备上的批量注册

1. 在设备上，打开 "**设置**"。

1. 选择 "**帐户**"，然后选择 "**访问工作单位或学校**"。 注册成功后，将在 " **" "**" 下看到一个帐户。

1. 选择该帐户，然后选择 "**同步**"。此操作通过 Configuration Manager 启动管理。

### <a name="verify-enrollment-in-the-console"></a>在控制台中验证注册

使用 Configuration Manager 控制台验证是否已成功注册设备。 在 Configuration Manager 控制台中，转到“资产和符合性”工作区，并选择“设备”********。 在设备列表中浏览或搜索已注册的设备。
