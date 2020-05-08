---
title: 导入 PFX 证书配置文件
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager 中的 PFX 文件生成支持加密数据交换的用户特定的证书。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3304d480f0650191a784a9152ae464e81c2207a1
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906398"
---
# <a name="import-pfx-certificate-profiles"></a>导入 PFX 证书配置文件

适用范围：  Configuration Manager (Current Branch)

了解如何通过从外部证书导入凭据来创建证书配置文件。 本文重点介绍个人信息交换（PFX）证书配置文件的具体信息。 有关如何创建和配置这些配置文件的详细信息，请参阅[证书配置文件](../../protect/deploy-use/introduction-to-certificate-profiles.md)。

对于不同的设备和操作系统版本，Configuration Manager 支持不同种类的证书存储区。 例如，Windows 10 和 Windows 10 移动版。 有关详细信息，请参阅[证书配置文件先决条件](../../protect/plan-design/prerequisites-for-certificate-profiles.md)。

使用 Configuration Manager 导入证书凭据，然后将 PFX 文件设置到设备。 可以使用这些文件生成特定于用户的证书以支持加密的数据交换。

> [!TIP]  
> 有关此过程的分步演练，请参阅博客文章[如何在 Configuration Manager 中创建和部署 PFX 证书配置文件](https://docs.microsoft.com/archive/blogs/karanrustagi/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager)。  

## <a name="create-a-profile"></a>创建档案

1. 在 Configuration Manager 控制台中，请参阅 "**资产和符合性**" 工作区，展开 "**符合性设置**"，展开 "**公司资源访问**"，然后选择 "**证书配置文件**"。

1. 在功能区的“主页”选项卡上，选择“创建”组中的“创建证书配置文件”************。

1. 在 "**创建证书配置文件向导**" 的 "**常规**" 页上，指定下列信息：  

    - **名称**：输入证书配置文件的唯一名称。 最多可以使用 256 个字符。  

    - **说明**：提供对证书配置文件进行概述的描述，此配置文件可帮助在 Configuration Manager 控制台中识别该配置文件。 最多可以使用 256 个字符。  

1. 选择 "**个人信息交换-PKCS #12 （PFX）设置-导入**"。 此选项将导入现有证书中的信息以创建证书配置文件。

    > [!NOTE]
    > "**创建**" 选项代表用户从连接的本地证书颁发机构（CA）申请证书。 然后，此过程安全地将证书以 PFX 文件形式传递给客户端。 有关详细信息，请参阅[使用证书颁发机构创建 PFX 证书配置文件](create-pfx-certificate-profiles.md)。

1. 在 "**创建证书配置文件向导**" 的 " **PFX 证书**" 页上，指定设备密钥存储提供程序（KSP）：

    - **如果存在受信任的平台模块 (TPM) 则安装到该处**  
    - **安装到受信任的平台模块（TPM），否则失败**
    - **安装到 Windows Hello 企业版，否则失败**
    - **安装到软件密钥存储提供程序**

1. 在 "**受支持的平台**" 页上，选择支持的设备平台。

1. 完成向导。

## <a name="deploy-the-profile"></a>部署配置文件

创建并配置证书配置文件后，它现在可在 "**证书配置文件**" 节点中使用。 有关如何部署它的详细信息，请参阅[部署资源访问配置文件](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)。

## <a name="assign-primary-users"></a>分配主要用户

在需要安装 PFX 证书的 Windows 10 设备上，将目标用户分配为主要用户。 有关详细信息，请参阅[用户设备相关性](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。

## <a name="provision-a-create-pfx-script"></a>预配 create PFX 脚本

若要导入 PFX 证书，请使用以下 Configuration Manager PowerShell cmdlet 来预配 Create PFX 脚本：

- [CMClientCertificatePfx](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmclientcertificatepfx?view=sccm-ps)
- [导入-CMClientCertificatePfx](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmclientcertificatepfx?view=sccm-ps)
- [CMClientCertificatePfx](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmclientcertificatepfx?view=sccm-ps)

### <a name="example-script"></a>示例脚本

若要将 PFX 文件预配到用户的证书配置文件，请在包含 Configuration Manager 控制台的计算机上打开 PowerShell。 根据环境中的值更改变量。

``` PowerShell
# The display name of your PFX Import certificate profile
$PfxProfileDisplayName = "ImportPFX"

# The password you used to protect/encrypt the external PFX file that was created/exported from your certificate storage provider
# If you omit this password, PowerShell will securely prompt you for it. You can specify it as a parameter for process automation.
$password = ""

# The username of the user who will receive this PFX certificate on their device
$user = "Melissa"

# The full path to the PFX file you exported from the certificate store
$pfxfile = "c:\p1.pfx"

# If the target user isn't in the same domain as the user running this script, specify a different domain
Import-CMClientCertificatePfx -UserName "$env:USERDOMAIN\$user" -Password (ConvertTo-SecureString -String $password -AsPlainText -Force) -CertificateProfilePfx (Get-CMCertificateProfilePfx -Fast -Name $PfxProfileDisplayName) -Path $pfxfile
```

## <a name="see-also"></a>另请参阅

[创建新的证书配置文件](../../protect/deploy-use/create-certificate-profiles.md)

[使用证书颁发机构创建 PFX 证书配置文件](create-pfx-certificate-profiles.md)

[部署 Wi-fi、VPN、电子邮件和证书配置文件](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)
