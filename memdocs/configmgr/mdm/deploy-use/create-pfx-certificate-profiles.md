---
title: 创建 PFX 证书配置文件
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager 中的 PFX 文件生成支持加密数据交换的用户特定的证书。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d240a836-c49b-49ab-a920-784c062d6748
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b45474484629b437f2548fb375075cfe55275ee2
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724571"
---
# <a name="create-pfx-certificate-profiles-using-a-certificate-authority"></a>使用证书颁发机构创建 PFX 证书配置文件

适用范围：  Configuration Manager (Current Branch)

了解如何创建使用证书颁发机构凭据的证书配置文件。 本文重点介绍个人信息交换（PFX）证书配置文件的具体信息。 有关如何创建和配置这些配置文件的详细信息，请参阅[证书配置文件](../../protect/deploy-use/introduction-to-certificate-profiles.md)。

Configuration Manager 允许你使用证书颁发机构颁发的凭据创建 PFX 证书配置文件。 你可以选择 "Microsoft" 或 "Entrust" 作为证书颁发机构。 当部署到用户设备时，PFX 文件生成特定于用户的证书以支持加密的数据交换。

若要从现有证书文件导入证书凭据，请参阅[导入 PFX 证书配置文件](import-pfx-certificate-profiles.md)。

## <a name="prerequisites"></a>先决条件

在开始创建证书配置文件之前，请确保必要的先决条件已准备就绪。 有关详细信息，请参阅[证书配置文件的先决条件](../../protect/plan-design/prerequisites-for-certificate-profiles.md)。 例如，对于 PFX 证书配置文件，你需要一个[证书注册点](../../protect/deploy-use/certificate-infrastructure.md#step-2---install-and-configure-the-certificate-registration-point)站点系统角色。

## <a name="create-a-profile"></a>创建档案  

1. 在 Configuration Manager 控制台中，请参阅 "**资产和符合性**" 工作区，展开 "**符合性设置**"，展开 "**公司资源访问**"，然后选择 "**证书配置文件**"。

1. 在功能区的“主页”选项卡上，选择“创建”组中的“创建证书配置文件”************。

1. 在 "**创建证书配置文件向导**" 的 "**常规**" 页上，指定下列信息：  

    - **名称**：输入证书配置文件的唯一名称。 最多可以使用 256 个字符。  

    - **说明**：提供对证书配置文件进行概述的描述，此配置文件可帮助在 Configuration Manager 控制台中识别该配置文件。 最多可以使用 256 个字符。  

1. 选择 "**个人信息交换-PKCS #12 （PFX）设置-创建**"。 此选项将代表用户从连接的本地证书颁发机构（CA）申请证书。 选择证书颁发机构： **Microsoft**或**Entrust Datacard**。

    > [!NOTE]
    > **导入**选项从现有证书获取信息来创建证书配置文件。 有关详细信息，请参阅[导入 PFX 证书配置文件](import-pfx-certificate-profiles.md)。

1. 在 "**受支持的平台**" 页上，选择此证书配置文件支持的 OS 版本。 有关 Configuration Manager 的版本支持的操作系统版本的详细信息，请参阅[客户端和设备支持的操作系统版本](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)。

1. 在 "**证书颁发机构**" 页上，选择用于处理 PFX 证书的证书注册点（CRP）：

    1. **主站点**：选择包含 CA 的 CRP 角色的服务器。
    1. **证书颁发机构**：选择相关的 CA。

    有关详细信息，请参阅[证书基础结构](../../protect/deploy-use/certificate-infrastructure.md)。

" **PFX 证书**" 页上的 "设置" 不同于 "**常规**" 页上的所选 CA：

- [Microsoft CA](#bkmk_microsoft)
- [Entrust Datacard CA](#bkmk_entrust)

### <a name="configure-pfx-certificate-settings-for-microsoft-ca"></a><a name="bkmk_microsoft"></a>为 Microsoft CA 配置**PFX 证书**设置

1. 对于 "**证书模板名称**"，请选择证书模板。

1. 若要将证书配置文件用于 S/MIME 签名或加密，请启用**证书使用**。

    启用此选项时，它会将与目标用户关联的所有 PFX 证书传递给其所有设备。 如果未启用此选项，则每个设备都会收到一个唯一的证书。  

1. 将“使用者名称格式”**** 设置为“公用名”**** 或“完全可分辨名称”****。 如果你不确定要使用哪一个，请联系你的 CA 管理员。

1. 对于 "**使用者可选名称**"，请根据 CA 启用**电子邮件地址**和**用户主体名称（UPN）** 。

1. **续订阈值**：根据过期之前的剩余时间百分比，确定自动续订证书的时间。

1. 将“证书有效期”**** 设置为证书的生存期。

1. 当证书注册点指定 Active Directory 凭据时，启用**Active Directory 发布**。

1. 如果选择了一个或多个 Windows 10 支持的平台：

    1. 将 " **Windows 证书存储**" 设置为 "**用户**"。 （"**本地计算机**" 选项不部署证书，请不要选择它。）

    1. 选择以下**密钥存储提供程序（KSP）** 之一：

        - **如果存在受信任的平台模块 (TPM) 则安装到该处**  
        - **安装到受信任的平台模块（TPM），否则失败**
        - **安装到 Windows Hello 企业版，否则失败**
        - **安装到软件密钥存储提供程序**

1. 完成向导。

### <a name="configure-pfx-certificate-settings-for-entrust-datacard-ca"></a><a name="bkmk_entrust"></a>为 Entrust Datacard CA 配置**PFX 证书**设置

1. 对于 "**数字标识" 配置**，请选择配置文件。 Entrust 管理员创建数字标识配置选项。

1. 若要将证书配置文件用于 S/MIME 签名或加密，请启用**证书使用**。

    启用此选项时，它会将与目标用户关联的所有 PFX 证书传递给其所有设备。 如果未启用此选项，则每个设备都会收到一个唯一的证书。  

1. 若要将 Entrust**使用者名称格式**标记映射到 Configuration Manager 字段，请选择 "**格式**"。

    “证书名称格式”**** 对话框列出了 Entrust 数字标识配置变量。 对于每个 Entrust 变量，请选择适当的 Configuration Manager 字段。

1. 若要将 Entrust**使用者备用名称**令牌映射到受支持的 LDAP 变量，请选择 "**格式**"。

    “证书名称格式”**** 对话框列出了 Entrust 数字标识配置变量。 对于每个 Entrust 变量，请选择相应的 LDAP 变量。

1. **续订阈值**：根据过期之前的剩余时间百分比，确定自动续订证书的时间。

1. 将“证书有效期”**** 设置为证书的生存期。

1. 当证书注册点指定 Active Directory 凭据时，启用**Active Directory 发布**。

1. 如果选择了一个或多个 Windows 10 支持的平台：

    1. 将 " **Windows 证书存储**" 设置为 "**用户**"。 （"**本地计算机**" 选项不部署证书，请不要选择它。）

    1. 选择以下**密钥存储提供程序（KSP）** 之一：

        - **如果存在受信任的平台模块 (TPM) 则安装到该处**  
        - **安装到受信任的平台模块（TPM），否则失败**
        - **安装到 Windows Hello 企业版，否则失败**
        - **安装到软件密钥存储提供程序**

1. 完成向导。

## <a name="deploy-the-profile"></a>部署配置文件

创建证书配置文件后，它现在可在 "**证书配置文件**" 节点中使用。 有关如何部署它的详细信息，请参阅[部署资源访问配置文件](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)。

## <a name="see-also"></a>另请参阅

[创建新的证书配置文件](../../protect/deploy-use/create-certificate-profiles.md)

[导入 PFX 证书配置文件](import-pfx-certificate-profiles.md)

[部署 Wi-fi、VPN、电子邮件和证书配置文件](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)
