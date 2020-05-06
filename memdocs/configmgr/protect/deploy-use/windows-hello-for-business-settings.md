---
title: Windows Hello 企业版设置
titleSuffix: Configuration Manager
description: 了解如何将 Windows Hello 企业版与 Configuration Manager 集成。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c60f30e306c6ff52849cfcdd4696d67a7d26f395
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706215"
---
# <a name="windows-hello-for-business-settings-in-configuration-manager"></a>Configuration Manager 中的 Windows Hello 企业版设置

适用范围：  Configuration Manager (Current Branch)

<!--1245704-->
Configuration Manager 与 Windows Hello 企业版集成。 （此功能旧称为“Microsoft Passport for Work”。）Windows Hello 企业版是 Windows 10 设备的备用登录方法。 其使用 Active Directory 或 Azure Active Directory (Azure AD) 帐户来替代密码、智能卡或虚拟智能卡。 在 Hello 企业版中，可以使用“用户手势”取代密码进行登录  。 用户手势可以是 PIN、生物识别身份验证或指纹读取器等外部设备。

> [!Important]  
> 自版本 1910 起，不支持 Configuration Manager 中的“使用 Windows Hello 企业版进行基于证书的身份验证”设置。 有关详细信息，请参阅[已弃用的功能](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)。 基于密钥的身份验证仍有效。
>
> Active Directory 联合身份验证服务注册机构 (ADFS RA) 部署更加简单，提供了更好的用户体验，并且具有更具确定性的证书注册体验。 请对“使用 Windows Hello 企业版进行基于证书的身份验证”使用 ADFS RA。
>
> 对于共同管理的设备，不妨将[“资源访问策略”  工作负荷](../../comanage/workloads.md#resource-access-policies)迁移到 Intune 中。 然后，使用 Intune 策略来管理这些证书。 有关详细信息，请参阅[如何切换工作负载](../../comanage/how-to-switch-workloads.md)。

有关详细信息，请参阅 [Windows Hello 企业版](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)。

> [!Note]  
> 默认情况下，Configuration Manager 不启用此项可选功能。 必须在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](../../core/servers/manage/install-in-console-updates.md#bkmk_options)。<!--505213-->  

Configuration Manager 通过以下方式与 Windows Hello 企业版集成：  

- 控制用户可用来和不可用来登录的手势。  

- 在 Windows Hello 企业版密钥存储提供程序 (KSP) 中存储身份验证证书。 有关详细信息，请参阅[证书配置文件](introduction-to-certificate-profiles.md)。  

- 创建并部署 Windows Hello 企业版配置文件，用于控制运行 Configuration Manager 客户端的域加入 Windows 10 设备上的设置。 自版本 1910 起，无法使用基于证书的身份验证。 如果使用的是基于密钥的身份验证，无需部署证书配置文件。

## <a name="configure-a-profile"></a>配置配置文件  

1. 在 Configuration Manager 控制台中，转到“资产和符合性”  工作区。 依次展开“符合性设置”和“公司资源访问”   ，然后选择“Windows Hello 企业版配置文件”  节点。

1. 在功能区中，选择“创建 Windows Hello 企业版配置文件”  ，以启动配置文件向导。

1. 在“常规”  页上，指定此配置文件的名称和可选说明。

1. 在“支持的平台”  页上，选择此配置文件应该应用于的 OS 版本。

1. 在“设置”页面上，配置下列设置  ：

    - **配置 Windows Hello 企业版**：指定此配置文件是启用、禁用还是不配置 Hello 企业版。

    - **使用受信任的平台模块(TPM)** ：TPM 额外提供了一层数据安全。 选择下列值之一：  

      - **必需**：仅限可访问 TPM 的设备预配 Windows Hello 企业版。  

      - **首选**：首次尝试使用 TPM 的设备。 如果这不可用，他们可以使用软件加密。

    - **身份验证方法**：将此选项设置为“未配置”  或“基于密钥”  。

        > [!NOTE]
        > 自版本 1910 起，不支持 Configuration Manager 中的“使用 Windows Hello 企业版进行基于证书的身份验证”设置。

    - 配置最小 PIN 长度  ：若要规定用户 PIN 的最小长度，请启用此选项，并指定值。 如果启用，默认值为“`4`”。

    - 配置最大 PIN 长度  ：若要规定用户 PIN 的最大长度，请启用此选项，并指定值。 如果启用，默认值为“`127`”。

    - **要求 PIN 有效期限(天数)** ：指定用户必须更改设备 PIN 前的天数。

    - 禁止重用旧 PIN  ：不允许用户使用以前用过的 PIN。

    - **要求在 PIN 中使用大写字母**：指定用户是否必须在 Windows Hello 企业版 PIN 中包含大写字母。 选择：  

      - **允许**：用户可以在其 PIN 中使用大写字母，但不强制。

      - **必需**：用户必须在其 PIN 中包含至少一个大写字母。  

      - **不允许**：用户不能在其 PIN 中使用大写字母。  

    - **要求在 PIN 中使用小写字母**：指定用户是否必须在 Windows Hello 企业版 PIN 中包含小写字母。 选择：  

      - **允许**：用户可以在其 PIN 中使用小写字母，但不强制。

      - **必需**：用户必须在其 PIN 中包含至少一个小写字母。  

      - **不允许**：用户不能在其 PIN 中使用小写字母。  

    - **配置特殊字符**：指定 PIN 中特殊字符的使用。 选择：  

        > [!NOTE]
        > 特殊字符包括以下字符集：
        >
        > ``` characters
        > ! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~
        > ```

      - **允许**：用户可以在其 PIN 中使用特殊字符，但不强制。  

      - **必需**：用户必须在其 PIN 中包含至少一个特殊字符。  

      - **不允许**：用户不能在其 PIN 中使用特殊字符。 此行为与“未配置”  设置一样。  

    - 配置 PIN 中数字的使用  ：指定 PIN 中数字的使用。 选择：

      - **允许**：用户可以在 PIN 中使用数字，但不强制。  

      - **必需**：用户必须在 PIN 中添加至少一个数字。  

      - **不允许**：用户不能在 PIN 中使用数字。

    - 启用生物识别手势  ：使用生物识别身份验证，如面部识别或指纹。 这些是 Windows Hello 企业版 PIN 的替代模式。 用户仍需配置 PIN，因为生物识别身份验证可能失败。  

      如果设置为“是”，Windows Hello 企业版则允许生物识别身份验证  。 如果设置为“否”，Windows Hello 企业版将阻止生物识别身份验证（对于所有帐户类型）  。  

    - 使用增强型防欺骗：  在支持增强型防欺骗的设备上配置此技术。 如果设置为“是”，则 Windows 将在支持反电子欺骗技术时要求所有用户对面部识别功能使用此技术  。  

    - 使用电话登录  ：为移动电话配置双因素身份验证。

1. 完成向导。

以下屏幕截图是 Windows Hello 企业版配置文件设置的示例：  

![Windows Hello 企业版策略向导，显示可用设置列表](../media/hello-for-business-settings.png)

## <a name="configure-permissions"></a>配置权限

1. 以域管理员或等效凭据身份，登录安装了以下可选功能的安全管理工作站：RSAT：Active Directory 域服务和轻型目录服务工具。

1. 打开“Active Directory 用户和计算机”控制台  。

1. 选择域，转到“操作”  菜单，然后选择“属性”  。

1. 切换到“安全性”  选项卡，然后选择“高级”  。

    > [!TIP]
    > 如果看不到“安全性”  选项卡，请关闭“属性”窗口。 转到“视图”  菜单，然后选择“高级功能”  。

1. 选择“添加”  。

1. 选择“选择主体”  ，并输入“`Key Admins`”。

1. 从“适用于”  列表中，选择“后代用户对象”  。

1. 在页面底部，选择“全部清除”  。

1. 在“属性”  部分中，选择“读取 msDS-KeyCredentialLink”  。

1. 选择“确定”保存所做的更改并关闭所有窗口  。

## <a name="next-steps"></a>后续步骤

[证书配置文件](introduction-to-certificate-profiles.md)
