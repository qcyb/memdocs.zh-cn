---
title: 在 Microsoft Intune 中使用 SCEP 证书配置文件 - Azure | Microsoft Docs
description: 在 Microsoft Intune 中创建和分配简单证书注册协议 (SCEP) 证书配置文件。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 35cf4b3afb766d8729d3438d2d8c61e1d79f4791
ms.sourcegitcommit: 48ec5cdc5898625319aed2893a5aafa402d297fc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84531734"
---
# <a name="create-and-assign-scep-certificate-profiles-in-intune"></a>在 Intune 中创建和分配 SCEP 证书配置文件

[配置基础结构](certificates-scep-configure.md)以支持简单证书注册协议 (SCEP) 证书之后，即可创建 SCEP 证书配置文件，然后将其分配给 Intune 中的用户和设备。

> [!IMPORTANT]
> 使用 SCEP 证书配置文件的设备必须信任受信任的根证书颁发机构 (CA)。 最好是通过将[受信任的证书配置文件](../protect/certificates-configure.md#create-trusted-certificate-profiles)部署到接收 SCEP 证书配置文件的组中来建立根 CA 的信任。 受信任的证书配置文件会预配受信任的根 CA 证书。

## <a name="create-a-scep-certificate-profile"></a>创建 SCEP 证书配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择并转到“设备” > “配置文件” > “创建配置文件”。

3. 输入以下属性：
   - **平台**：选择设备平台。
   - **配置文件**：选择“SCEP 证书”

     对于 Android Enterprise 平台，配置文件类型分为以下两类：“仅限设备所有者”和“仅限工作配置文件”。 确保为所管理的设备选择正确的 SCEP 证书配置文件。  

     “仅限设备所有者”配置文件的 SCEP 证书配置文件具有以下限制：

      1. 在“监视”下，证书报表不可用于设备所有者 SCEP 证书配置文件。

      2. 不能使用 Intune 撤销由 SCEP 证书配置文件为设备所有者预配的证书。 可以通过外部进程或直接通过证书颁发机构来实现撤销。

      3. 对于 Android 企业专用设备，SCEP 证书配置文件仅支持 Wi-Fi 网络配置和身份验证。  Android 企业专用设备上的 SCEP 证书配置文件不支持 VPN 或应用身份验证。

4. 选择“创建”。

5. 在“基本信息”中，输入以下属性：
   - **名称**：输入配置文件的描述性名称。 为配置文件命名，以便稍后可以轻松地识别它们。 例如，配置文件名称最好是“整个公司的 SCEP 配置文件”。
   - **描述**：输入配置文件的说明。 此设置是可选的，但建议进行。

6. 选择“下一步”。

7. 在“配置设置”中，然后完成以下配置：

   - **证书类型**：

     （适用对象：Android、Android Enterprise、iOS/iPadOS、macOS、Windows 8.1 和更高版本以及 Windows 10 和更高版本。）

     根据证书配置文件的使用方式选择类型：

     - **用户**：“用户”证书类型可包含证书使用者和 SAN 中的用户和设备属性。  
     - **设备**：“设备”证书只能在证书主题和 SAN 中包含设备属性。

       “设备”适用于无用户设备的情况（如展台）或 Windows 设备。 在 Windows 设备上，证书位于本地计算机证书存储中。

   - **使用者名称格式**：

     选择 Intune 如何自动创建证书请求中的使用者名称。 使用者名称格式的选项取决于所选的证书类型，即“用户”或“设备” 。

     > [!NOTE]
     > 当生成的证书签名请求 (CSR) 中的使用者名称包含以下字符之一作为转义字符（后跟反斜杠 \\）时，使用 SCEP 获取证书存在[已知问题](#avoid-certificate-signing-requests-with-escaped-special-characters)：
     > - \+
     > - ;
     > - ,
     > - =

     - **“用户”证书类型**

       “使用者名称格式”的格式选项包括：

       - 未配置
       - 公用名称
       - 包含电子邮件地址的公用名称
       - 作为电子邮件地址的公用名称
       - IMEI（国际移动设备标识）
       - **序列号**
       - **自定义**：选中此选项时，也会显示“自定义”文本框。 使用此字段输入一个自定义使用者名称格式，包括变量。 自定义格式支持两种变量：公用名 (CN) 和电子邮件 (E)。 可将“公用名(CN)”设置为以下任何变量：

         - **CN={{UserName}}** ：用户的用户名（如 janedoe）。
         - CN={{UserPrincipalName}}：用户的用户主体名称（如 janedoe@contoso.com）。\*
         - **CN={{AAD_Device_ID}}** ：在 Azure Active Directory (AD) 中注册设备时分配的 ID。 此 ID 通常用于向 Azure AD 进行身份验证。
         - **CN={{SERIALNUMBER}}** ：制造商通常用于标识设备的唯一序列号 (SN)。
         - **CN={{IMEINumber}}** ：用于标识移动电话的国际移动设备标识 (IMEI)。
         - **CN={{OnPrem_Distinguished_Name}}** ：用逗号分隔的一系列相对可分辨名称，如 CN=Jane Doe、OU=UserAccounts、DC=corp、DC=contoso、DC=com。

           要使用 {{OnPrem_Distinguished_Name}} 变量，请确保使用 [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) 将onpremisesdistinguishedname 用户属性与 Azure AD 同步 。

         - **CN={{onPremisesSamAccountName}}** ：管理员可以使用 Azure AD 连接到名为 onPremisesSamAccountName 的属性，将 Active Directory 中的 samAccountName 属性同步到 Azure AD。 Intune 可以将该变量替换为证书使用者中的证书颁发请求的一部分。 samAccountName 属性是指用户登录名，该名称用于支持早期版本的 Windows（Windows 2000 之前）中的客户端和服务器。 用户登录名的格式为：DomainName\testUser，或仅 testUser 。

            要使用 {{onPremisesSamAccountName}} 变量，请确保使用 [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) 将 onPremisesSamAccountName 用户属性与 Azure AD 同步 。

         通过使用这些变量的一个或多个与静态字符串的组合，可以创建一个自定义使用者名称格式，例如：  
         - CN={{UserName}},E={{EmailAddress}},OU=Mobile,O=Finance Group,L=Redmond,ST=Washington,C=US

         该示例包含使用者名称格式，其中除了不仅使用了 CN 和 E 变量，还使用了组织单元、组织、位置、省/直辖市/自治区和国家/地区值的字符串。 [CertStrToName 函数](https://msdn.microsoft.com/library/windows/desktop/aa377160.aspx)介绍此函数及其支持的字符串。
         
         \* 对于 Android 仅设备所有者配置文件，CN={{UserPrincipalName}} 设置将不起作用。 Android 仅设备所有者配置文件可用于没有用户的设备，所以此配置文件将无法获取用户的用户主体名称。 如果确实需要对包含用户的设备使用此选项，可以使用如下解决方法：CN={{UserName}}\@contoso.com - 它提供你手动添加的用户名和域，例如 janedoe@contoso.com

      - **“设备”证书类型**

        “使用者名称格式”的格式选项包括以下变量：

        - **{{AAD_Device_ID}}** 或 **{{AzureADDeviceId}}** - 可以使用任何一个变量通过 Azure AD ID 来标识设备。
        - **{{Device_Serial}}**
        - **{{Device_IMEI}}**
        - **{{SerialNumber}}**
        - **{{IMEINumber}}**
        - **{{WiFiMacAddress}}**
        - **{{IMEI}}**
        - **{{DeviceName}}**
        - {{FullyQualifiedDomainName}}（仅适用于 Windows 和加入域的设备）
        - **{{MEID}}**

        可在文本框中指定这些变量，后跟变量的文本。 例如，可以将名为 Device1 的设备的公用名添加为 CN={{DeviceName}}Device1。

        > [!IMPORTANT]
        > - 指定变量时，请将变量名称括在大括号 {} 中（如示例中所示），以避免出现错误。  
        > - 在设备证书的使用者或 SAN 中使用的设备属性（例如 IMEI、SerialNumber 和 FullyQualifiedDomainName）可能被有权访问设备的人员仿造   。
        > - 设备必须支持在证书配置文件中为该配置文件指定的所有变量，才能在该设备上安装。  例如，如果在 SCEP 配置文件的使用者名称中使用 {{IMEI}} 并将其分配给没有 IMEI 号码的设备，则配置文件安装将失败。

   - **使用者可选名称**：选择 Intune 在证书请求中自动创建使用者可选名称 (SAN) 的方式。 SAN 的选项取决于所选的证书类型，即“用户”或“设备” 。

      - **“用户”证书类型**

        从可用属性中进行选择：

        - **电子邮件地址**
        - **用户主体名称 (UPN)**

        例如，用户证书类型可以在使用者可选名称中包含用户主体名称 (UPN)。 如果使用客户端证书向“网络策略服务器”进行身份验证，则要将使用者可选名称设置为 UPN。

      - **“设备”证书类型**

        使用“属性”下拉列表并选择一个属性，分配一个值并将该值添加到证书配置文件中  。 可以通过选择其他属性来添加多个值。

        可用的属性包括：

        - **电子邮件地址**
        - **用户主体名称 (UPN)**
        - **DNS**

        凭借“设备”证书类型，可以对值使用以下设备证书变量：

        - **{{AAD_Device_ID}}** 或 **{{AzureADDeviceId}}** - 可以使用任何一个变量通过 Azure AD ID 来标识设备。
        - **{{Device_Serial}}**
        - **{{Device_IMEI}}**
        - **{{SerialNumber}}**
        - **{{IMEINumber}}**
        - **{{WiFiMacAddress}}**
        - **{{IMEI}}**
        - **{{DeviceName}}**
        - **{{FullyQualifiedDomainName}}**
        - **{{MEID}}**

        要为属性指定一个值，请用大括号将变量名称括起来，后跟该变量的文本。 例如，可以为 DNS 属性添加一个值 {{AzureADDeviceId}}.domain.com，其中 .domain.com 是文本。 对于名为 User1 的用户，电子邮件地址可能显示为 {{FullyQualifiedDomainNameUser1@Contoso.com}}。

        > [!IMPORTANT]
        > - 使用设备证书变量时，请将变量名称括在大括号 { } 内。
        > - 请勿在变量后面的文本中使用大括号“{ }”、竖线符号“|”以及分号“;”  。
        > - 在设备证书的使用者或 SAN 中使用的设备属性（例如 IMEI、SerialNumber 和 FullyQualifiedDomainName）可能被有权访问设备的人员仿造   。
        > - 设备必须支持在证书配置文件中为该配置文件指定的所有变量，才能在该设备上安装。  例如，如果在 SCEP 配置文件的 SAN 中使用 {{IMEI}} 并将其分配给没有 IMEI 号码的设备，则配置文件安装将失败。

   - **证书有效期**：

     可以在证书模板中输入低于（但不能高于）有效期的值。 如果将证书模板配置为[支持可从 Intune 控制台设置的自定义值](certificates-scep-configure.md#modify-the-validity-period-of-the-certificate-template)，请使用此设置来指定证书过期之前的剩余时间量。

     例如，如果证书模板中的证书有效期为 2 年，则输入值可以为 1 年，但不能为 5 年。 该值还必须小于发证 CA 证书的剩余有效期。

   - **密钥存储提供程序 (KSP)** ：

     （适用对象：Windows 8.1 和更高版本以及 Windows 10 和更高版本）

     指定存储证书密钥的位置。 从下面的值中进行选择：

     - 注册到受信任的平台模块(TPM) KSP (若有); 否则，注册到软件 KSP
     - 注册到受信任的平台模块(TPM) KSP，否则失败
     - 注册到 Passport，否则失败(Windows 10 及更高版本)
     - **注册到软件 KSP**

   - **密钥用法**：

     选择证书的密钥用法选项：

     - **数字签名**：仅当数字签名有助于保护密钥时才允许密钥交换。
     - **密钥加密**：仅在密钥已加密时才允许密钥交换。

   - **密钥大小(位)** ：

     选择密钥中包含的位数。

   - **哈希算法**：

     （适用对象：Android、Android Enterprise、Windows Phone 8.1、Windows 8.1 和更高版本以及 Windows 10 和更高版本。）

     选择要与此证书一起使用的可用哈希算法类型之一。 选择连接设备支持的最高级别安全性。

   - **根证书**：

     选择受信任的证书配置文件，该配置文件是之前被配置并分配给此 SCEP 证书配置文件的适用用户和设备。 受信任的证书配置文件用于预配具有受信任的根 CA 证书的用户和设备。 有关受信任证书配置文件的信息，请参阅“在 Intune 中使用证书进行身份验证”中的[导出受信任的 CA 证书](certificates-configure.md#export-the-trusted-root-ca-certificate)和[创建受信任的证书配置文件](certificates-configure.md#create-trusted-certificate-profiles)。 如果具有根证书颁发机构和证书发证机构，请选择验证证书发证机构的受信任的根证书配置文件。

   - **扩展密钥用法**：

     为证书的预期目的添加值。 大多数情况下，证书需要“客户端身份验证”以便用户或设备能够向服务器进行验证。 可根据需要添加其他密钥用法。

   - **续订阈值(%)** ：

     输入设备请求证书续订之前剩余的证书有效期限的百分比。 例如，如果输入“20”，将在证书的有效期限已使用 80% 时尝试续订证书。 将持续尝试续订，直到续订成功。 续订会生成新的证书，从而生成新的公钥/私钥对。

   - **SCEP 服务器 URL**：

     为通过 SCEP 颁发证书的 NDES 服务器输入 1 个或多个 URL。 例如，输入类似于 `https://ndes.contoso.com/certsrv/mscep/mscep.dll` 的内容。

     你可以根据需要添加其他 SCEP URL 进行负载均衡。 设备分别对 NDES 服务器进行三次调用；目的在于获取服务器功能、获取公钥，然后提交签名请求。 如果使用多个 URL，负载均衡可能会导致对 NDES 服务器的后续调用使用不同的 URL。 如果在同一请求期间联系其他服务器进行后续调用，则该请求将失败。

     管理 NDES 服务器 URL 的行为特定于每个设备平台：

     - **Android**：设备会随机排列在 SCEP 策略中接收到的 URL 列表，然后遍历该列表，直到找到可访问的 NDES 服务器。 然后设备在整个过程中继续使用相同的 URL 和服务器。 如果设备无法访问任何 NDES 服务器，则此过程将失败。
     - **iOS/iPadOS**：Intune 会随机排列 URL 并向设备提供单个 URL。 如果设备无法访问 NDES 服务器，则 SCEP 请求失败。
     - **Windows**：NDES URL 列表随机排列后会传递给 Windows 设备，然后 Windows 设备按接收的顺序尝试这些 URL，直到找到可用的 URL 为止。 如果设备无法访问任何 NDES 服务器，则此过程将失败。

     如果在对 NDES 服务器的三次调用中，任何一次都无法成功连接到相同的 NDES 服务器，则 SCEP 请求将失败。 例如，当负载均衡解决方案为对 NDES 服务器的第二次或第三次调用提供不同的 URL，或者基于 NDES 的虚拟化 URL 提供不同的实际 NDES 服务器时，就可能发生这种情况。 请求失败后，设备将在其下一个策略周期中再次尝试该过程，从 NDES URL 的随机列表（或用于 iOS/iPadOS 的单个 URL）开始。  

8. 选择“下一步”。

9. 在“作用域标记”（可选）中，分配一个标记以将配置文件筛选到特定 IT 组（如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`）。 有关范围标记的详细信息，请参阅[将 RBAC 和范围标记用于分布式 IT](../fundamentals/scope-tags.md)。

   选择“下一步”。

10. 在“分配”中，选择将接收配置文件的用户或组。 有关分配配置文件的详细信息，请参阅[分配用户和设备配置文件](../configuration/device-profile-assign.md)。

    选择“下一步”。

11. （仅适用于 Windows 10）在“适用性规则”中，指定适用性规则以优化此配置文件的分配。 可以根据操作系统版本或设备版本来选择是否分配配置文件。

   有关详细信息，请参阅“在 Microsoft Intune 中创建设备配置文件”中的[适用性规则](../configuration/device-profile-create.md#applicability-rules)。

12. 在“查看并创建”中查看设置。 选择“创建”时，将保存所做的更改并分配配置文件。 该策略也会显示在配置文件列表中。

### <a name="avoid-certificate-signing-requests-with-escaped-special-characters"></a>避免证书签名请求中包含转义的特殊字符

包含用以下一个或多个特殊字符作为转义字符的使用者名称 (CN) 的 SCEP 和 PKCS 证书请求存在一个已知问题。 将其中一个特殊字符作为转义字符的使用者名称将导致 CSR 中使用者名称不正确。 错误的使用者名称会导致 Intune SCEP 质询验证失败，并且不会颁发证书。

特殊字符为：
- \+
- ,
- ;
- =

当使用者名称包含一个特殊字符时，请使用以下选项之一来解决此限制：

- 用引号封装包含特殊字符的 CN 值。  
- 删除 CN 值中的特殊字符。

例如，使用者名称显示为 Test user (TestCompany, LLC)。  如果 CSR 包含一个 CN，该 CN 在 TestCompany 和 LLC 之间有逗号，则会出现问题 。  可以通过在整个 CN 周围加上引号，或者删除 TestCompany 和 LLC  之间的逗号来避免这一问题：

- **添加引号**：CN="Test User (TestCompany, LLC)",OU=UserAccounts,DC=corp,DC=contoso,DC=com
- **删除逗号**：*CN=Test User (TestCompany LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com*

 但是，使用反斜杠字符转义逗号的尝试将失败，CRP 日志中出现错误：
 
- **转义的逗号**：*CN=Test User (TestCompany\\, LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com*

此错误类似于以下错误：

```
Subject Name in CSR CN="Test User (TESTCOMPANY\, LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com" and challenge CN=Test User (TESTCOMPANY\, LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com do not match  

  Exception: System.ArgumentException: Subject Name in CSR and challenge do not match

   at Microsoft.ConfigurationManager.CertRegPoint.ChallengeValidation.ValidationPhase3(PKCSDecodedObject pkcsObj, CertEnrollChallenge challenge, String templateName, Int32 skipSANCheck)

Exception:    at Microsoft.ConfigurationManager.CertRegPoint.ChallengeValidation.ValidationPhase3(PKCSDecodedObject pkcsObj, CertEnrollChallenge challenge, String templateName, Int32 skipSANCheck)

   at Microsoft.ConfigurationManager.CertRegPoint.Controllers.CertificateController.VerifyRequest(VerifyChallengeParams value
```

## <a name="assign-the-certificate-profile"></a>分配证书配置文件

分配 SCEP 证书配置文件的方法与[部署设备配置文件](../configuration/device-profile-assign.md)以实现其他目的相同。

若要使用 SCEP 证书配置文件，设备还必须已接收受信任的证书配置文件，且该配置文件预配了受信任的根 CA 证书。 建议将受信任的根证书配置文件和 SCEP 证书配置文件都部署到相同的组中。

在继续之前，请考虑以下事项：

- 将 SCEP 证书配置文件分配给组时，将在设备上安装受信任的根 CA 证书文件（如“受信任的证书配置文件”中所述）。 设备使用 SCEP 证书配置文件来为该受信任的根 CA 证书创建证书请求。

- SCEP 证书配置文件仅安装在特定设备上，该设备可运行你在创建证书配置文件时指定的平台。

- 可以向用户集合或设备集合分配证书配置文件。

- 若要在注册设备后向设备快速发布证书，请将证书配置文件分配给用户组（而不是设备组）。 如果分配到设备组，则需要在设备接收策略前进行完整的设备注册。

- 如果使用 Intune 和 Configuration Manager 的共同管理，请在 Configuration Manager 中将资源访问策略的[工作负载滑块](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads)设置为“Intune”或“试点 Intune”。 此设置允许 Windows 10 客户端启动请求证书的过程。

> [!NOTE]
> - 在 iOS/iPadOS 设备上，当 SCEP 证书配置文件或 PKCS 证书配置文件与其他配置文件（如 Wi-Fi 或 VPN 配置文件）相关联，设备将收到其他每个配置文件的证书。 这会使 iOS/iPadOS 设备拥有 SCEP 或 PKCS 证书请求提供的多个证书。 
> - 在 iOS 13 和 macOS 10.15 中，还需要考虑一些[额外的安全要求（已被 Apple 记录在案）](https://support.apple.com/HT210176)。  


## <a name="next-steps"></a>后续步骤

[分配配置文件](../configuration/device-profile-assign.md)

[SCEP 证书配置文件部署故障排除](../protect/troubleshoot-scep-certificate-profiles.md)
