---
title: 在 Microsoft Intune 中使用私钥证书和公钥证书 - Azure | Microsoft Docs
description: 在 Microsoft Intune 中使用公钥加密标准 (PKCS) 证书、使用根证书和证书模板、安装 Microsoft Intune 连接器 (NDES) 和使用 PKCS 证书的设备配置文件。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28ca32bc65ee0c4647c22b10b6b5d47a25efa202
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643615"
---
# <a name="configure-and-use-pkcs-certificates-with-intune"></a>在 Intune 中配置和使用 PKCS 证书

Intune 支持使用私钥和公钥对 (PKCS) 证书。 本文有助于帮助配置所需的本地证书连接器等基础结构，导出 PKCS 证书，然后将证书添加到 Intune 设备配置配置文件。

Microsoft Intune 包括内置的设置来使用 PKCS 证书对组织资源进行访问和身份验证。 证书用于进行身份验证并保证用户安全访问公司资源（例如 VPN 或 WiFi 网络）。 使用 Intune 中的设备配置配置文件，将这些设置部署到设备。

有关使用导入的 PKCS 证书的信息，请参阅[导入的 PFX 证书](certificates-imported-pfx-configure.md)。


## <a name="requirements"></a>要求

要在 Intune 中使用 PKCS 证书，必须具有以下基础结构：

- **Active Directory 域**：  
  此部分中列出的所有服务器都必须加入 Active Directory 域。

  有关安装和配置 Active Directory 域服务 (AD DS) 的详细信息，请参阅 [AD DS 设计和规划](/windows-server/identity/ad-ds/plan/ad-ds-design-and-planning)。

- **证书颁发机构**：  
   企业证书颁发机构 (CA)。

  有关安装和配置 Active Directory 证书服务 (AD CS) 的信息，请参阅 [Active Directory 证书服务分步指南](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772393(v=ws.10))。

  > [!WARNING]  
  > Intune 要求在企业证书颁发机构 (CA) 而非独立 CA 中运行 AD CS。

- **客户端**：  
  连接到企业 CA。

- **根证书**：  
  从企业 CA 导出的根证书的副本。

- **Microsoft Intune 的 PFX 证书连接器**：

  有关先决条件和发行版等 PFX 证书连接器的信息，请参阅[证书连接器](certificate-connectors.md)。

  > [!IMPORTANT]
  > 从 PFX 证书连接器 6.2008.60.607 版本开始，PKCS 证书配置文件不再需要 Microsoft Intune 连接器。 
  
## <a name="export-the-root-certificate-from-the-enterprise-ca"></a>从企业 CA 中导出根证书

要使用 VPN、WiFi 或其他资源对设备进行身份验证，设备需要根证书或中间 CA 证书。 以下步骤介绍如何从企业 CA 中获取所需的证书。

**使用命令行**：  

1. 使用管理员帐户登录根证书颁发机构服务器。

2. 转到“开始” > “运行”，然后输入“Cmd”以打开命令提示符  。

3. 指定“certutil -ca.cert ca_name.cer”，以将根证书导出为“ca_name.cer”文件。

## <a name="configure-certificate-templates-on-the-ca"></a>在 CA 上配置证书模板

1. 使用具有管理权限的帐户登录到企业 CA。
2. 打开“证书颁发机构”控制台，右键单击“证书模板”，然后选择“管理”。
3. 找到“用户”证书模板，右键单击该模板，然后选择“复制模板”以打开“新建模板的属性面板”  。

    > [!NOTE]
    > 对于 S/MIME 电子邮件签名和加密方案，许多管理员使用单独的证书进行签名和加密。 如果使用 Microsoft Active Directory 证书服务，则针对 S/MIME 电子邮件签名证书可使用“仅 Exchange 签名”模板，针对 S/MIME 加密证书可使用“Exchange 用户”模板 。  如果使用第三方证书颁发机构，建议查看其指南，设置签名和加密模板。

4. 在“兼容性”选项卡上：

    - 将“证书颁发机构”设置为“Windows Server 2008 R2”
    - 将“证书接收人”设置为“Windows 7 / Server 2008 R2”

5. 在“通用”选项卡上，将“模板显示名称”设置为对你有意义的名称 。

    > [!WARNING]
    > 默认情况下，“模板名称”与“模板显示名称”相同，不包含空格。 请记下模板名称，供以后使用。

6. 在“请求处理”中，选择“允许导出私钥” 。

    > [!NOTE]
    > 与 SCEP 相反，使用 PKCS 时，系统在安装了连接器的服务器上而不是在设备上生成证书私钥。 证书模板必须允许导出私钥，以便证书连接器能够导出 PFX 证书并将其发送到设备。 
    >
    > 但请注意，证书安装在设备本身之上，其私钥标记为不可导出。

7. 在“加密”处，确认将“最小密钥大小”设置为 2048。
8. 在“使用者名称”处，选择“在请求中提供” 。
9. 在“扩展”处，确认在“应用程序策略”下显示有加密文件系统、安全电子邮件和客户端身份验证。

    > [!IMPORTANT]
    > 对于 iOS/iPadOS 证书模板，转到“扩展”选项卡，更新“密钥用法”，并确保未选择“数字签名为原件的证明”  。

10. 在“安全”选项中，为安装 Microsoft Intune 连接器的服务器添加计算机帐户。 允许该帐户具有读取和注册权限。
11. 选择“应用” > “确认”以保存证书模板。 关闭“证书模板控制台”。
12. 在“证书颁发机构”控制台中，右键单击“证书模板” > “新建” > “要颁发的证书模板”。 选择在先前步骤中创建的模板。 选择“确定”。
13. 为了让服务器管理已注册设备和用户的证书，请使用以下步骤：

    1. 右键单击“证书颁发机构”，选择“属性”。
    2. 在“安全”选项卡上，添加运行连接器（Microsoft Intune 连接器和 Microsoft Intune 的 PFX 证书连接器）的服务器的计算机帐户 。 
    3. 向计算机帐户授予“发布和管理证书”以及“请求证书”允许权限。

14. 注销企业 CA。

## <a name="download-install-and-configure-the-pfx-certificate-connector"></a>下载、安装和配置 PFX 证书连接器

开始操作前，先[查看连接器的要求](certificate-connectors.md)，并确保环境和 Windows 服务器可以支持连接器。

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“租户管理” > “连接器和令牌” > “证书连接器” > “+ 添加”。

3. 针对 PKCS #12 的连接器单击“下载证书连接器软件”并将文件保存到可从服务器上进行访问的位置，将在该服务器上安装连接器。

   ![Microsoft Intune 连接器下载](./media/certficates-pfx-configure/download-connector.png)

4. 下载完成后，登录服务器并运行安装程序 (PfxCertificateConnectorBootstrapper.exe)。  
   - 如果你接受默认安装位置，连接器将安装到 `Program Files\Microsoft Intune\PFXCertificateConnector`。
   - 连接器服务在本地系统帐户下运行。 如果需要通过代理进行 Internet 访问，请确认本地服务帐户可以访问服务器上的代理设置。

5. 安装后，Microsoft Intune 的 PFX 证书连接器将打开“注册”选项卡。 要启用到 Intune 的连接，请“登录”并输入具有 Azure 全局管理员或 Intune 管理员权限的帐户。

   > [!WARNING]
   > 默认情况下，在 Windows Server 中，“IE 增强的安全配置”设置为“启用”导致登录 Office 365 出现问题。

6. 选择“CA 帐户”选项卡，然后输入在证书颁发机构上拥有“颁发和管理证书”权限的帐户的凭据。 这些凭据将用于对证书颁发机构执行证书吊销。 

    单击“应用”以应用更改。

7. 关闭窗口。

8. 在 Microsoft Endpoint Manager 管理中心，返回到“租户管理” > “连接器和令牌” > “证书连接器”  。 片刻之后，将显示绿色勾号且连接状态更新。 连接器服务器现可与 Intune 通信。

## <a name="create-a-trusted-certificate-profile"></a>创建受信任的证书配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择并转到“设备” > “配置文件” > “创建配置文件”。

3. 输入以下属性：
   - **平台**：选择将接收此配置文件的设备的平台。
   - **配置文件**：选择“受信任的证书”
  
4. 选择“创建”。

5. 在“基本信息”中，输入以下属性：
   - **名称**：输入配置文件的描述性名称。 为配置文件命名，以便稍后可以轻松地识别它们。 例如，配置文件名称最好是“整个公司的受信任证书配置文件”。
   - **描述**：输入配置文件的说明。 此设置是可选的，但建议进行。

6. 选择“下一步”  。

7. 在“配置设置”中，指定之前导出的 .cer 文件根 CA 证书。

   > [!NOTE]
   > 能否为证书选择“目标存储区”取决于步骤三中所选的平台。

   ![创建配置文件并上传受信任的证书](./media/certficates-pfx-configure/certificates-pfx-configure-profile-fill.png)

8. 选择“下一步”  。

9. 在“作用域标记”（可选）中，分配一个标记以将配置文件筛选到特定 IT 组（如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`）。 有关范围标记的详细信息，请参阅[将 RBAC 和范围标记用于分布式 IT](../fundamentals/scope-tags.md)。

   选择“下一步”  。

10. 在“分配”中，选择将接收配置文件的用户或组。 计划将此证书配置文件部署到接收 PKCS 证书配置文件的相同组。 有关分配配置文件的详细信息，请参阅[分配用户和设备配置文件](../configuration/device-profile-assign.md)。

    选择“下一步”  。

11. （仅适用于 Windows 10）在“适用性规则”中，指定适用性规则以优化此配置文件的分配。 可以根据操作系统版本或设备版本来选择是否分配配置文件。

  有关详细信息，请参阅“在 Microsoft Intune 中创建设备配置文件”中的[适用性规则](../configuration/device-profile-create.md#applicability-rules)。

12. 在“查看并创建”中查看设置。 选择“创建”时，将保存所做的更改并分配配置文件。 该策略也会显示在配置文件列表中。

## <a name="create-a-pkcs-certificate-profile"></a>创建 PKCS 证书配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择并转到“设备” > “配置文件” > “创建配置文件”。

3. 输入以下属性：
   - **平台**：选择设备平台。 选项包括：
     - Android 设备管理员
     - Android Enterprise > 公司拥有的完全托管式专用工作配置文件
     - Android Enterprise > 仅工作配置文件
     - iOS/iPadOS
     - macOS
     - Windows 10 及更高版本
   - **配置文件**：选择“PKCS 证书”

   > [!NOTE]
   > 在应用了 Android Enterprise 配置文件的设备上，使用 PKCS 证书配置文件安装的证书在设备上不可见。 若要确认证书部署是否成功，请检查 Intune 控制台中配置文件的状态。
4. 选择“创建”。

5. 在“基本信息”中，输入以下属性：
   - **名称**：输入配置文件的描述性名称。 为配置文件命名，以便稍后可以轻松地识别它们。 例如，配置文件名称最好是“整个公司的 PKCS 配置文件”。
   - **描述**：输入配置文件的说明。 此设置是可选的，但建议进行。

6. 选择“下一步”  。
7. 在“配置设置”中，根据所选择的平台，可配置的设置有所不同。 选择平台进行详细设置：-Android 设备管理员 -Android Enterprise -iOS/iPadOS -Windows 10
   
   |设置     | 平台     | 详细信息   |
   |------------|------------|------------|
   |续订阈值 (%)        |<ul><li>All         |建议设为 20%  | 
   |证书有效期  |<ul><li>All         |如果没有更改证书模板，则此选项可能设置为一年。 |
   |密钥存储提供程序 (KSP)   |<ul><li>Windows 10  |对于 Windows，请选择在设备上存储密钥的位置。 |
   |证书颁发机构      |<ul><li>All         |显示企业 CA 的内部完全限定的域名 (FQDN)。  |
   |证书颁发机构名称 |<ul><li>All         |列出企业 CA 的名称，例如“Contoso 证书颁发机构”。 |
   |**证书模板名称**    |<ul><li>All         |列出证书模板的名称。 |
   |证书类型             |<ul><li>Android Enterprise（工作配置文件）</li><li>iOS</li><li>macOS</li><li>Windows 10 及更高版本|选择一个类型： <ul><li> “用户”证书类型可包含证书使用者和 SAN 中的用户和设备属性。 </il><li>“设备”证书只能在证书主题和 SAN 中包含设备属性。 设备适用于无用户设备（例如网亭或其他共享设备）的情况。  <br><br> 此选择影响使用者名称格式。 |
   |**使用者名称格式**          |<ul><li>All         |有关如何配置使用者名称格式的详细信息，请参阅本文后面的[使用者名称格式](#subject-name-format)。  <br><br> 对于大多数平台，除非另有要求，否则请使用“公用名”选择。 <br><br>对于以下平台，使用者名称格式由证书类型决定： <ul><li>Android Enterprise（工作配置文件）</li><li>iOS</li><li>macOS</li><li>Windows 10 及更高版本</li></ul>  <p>  |
   |**使用者可选名称**     |<ul><li>All         |对于“属性”，除非需要，请选择“用户主体名称(UPN)”，否则请配置相应的“值”，然后单击“添加”。 <br><br>有关详细信息，请参阅本文后面的[使用者名称格式](#subject-name-format)。|
   |**扩展密钥用法**           |<ul><li> Android 设备管理员 </li><li>Android Enterprise（设备所有者、工作配置文件） </li><li>Windows 10 |证书通常需要“客户端身份验证”，以便用户或设备能够对服务器进行身份验证。 |
   |**允许所有应用访问私钥** |<ul><li>macOS  |请将其设置为“启用”，以使为关联的 Mac 设备配置的应用可以访问 PKCS 证书私钥。 <br><br> 有关此设置的详细信息，请参阅 Apple 开发人员文档中[配置文件参考](https://developer.apple.com/business/documentation/Configuration-Profile-Reference.pdf)中的 AllowAllAppsAccess 证书有效负载部分。 |
   |**根证书**             |<ul><li>Android 设备管理员 </li><li>Android Enterprise（设备所有者、工作配置文件） |选择以前分配的根 CA 证书配置文件。 |

8. 选择“下一步”  。

9. 在“作用域标记”（可选）中，分配一个标记以将配置文件筛选到特定 IT 组（如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`）。 有关范围标记的详细信息，请参阅[将 RBAC 和范围标记用于分布式 IT](../fundamentals/scope-tags.md)。

   选择“下一步”  。

10. 在“分配”中，选择将接收配置文件的用户或组。 计划将此证书配置文件部署到接收受信任的证书配置文件的相同组。 有关分配配置文件的详细信息，请参阅[分配用户和设备配置文件](../configuration/device-profile-assign.md)。

    选择“下一步”  。

11. 在“查看并创建”中查看设置。 选择“创建”时，将保存所做的更改并分配配置文件。 该策略也会显示在配置文件列表中。


### <a name="subject-name-format"></a>使用者名称格式

为以下平台创建 PKCS 证书配置文件时，使用者名称格式的选项取决于所选的证书类型，即“用户”或“设备”。  

平台：

- Android Enterprise（工作配置文件）
- iOS
- macOS
- Windows 10 及更高版本

> [!NOTE]
> 当生成的证书签名请求 (CSR) 中的使用者名称包含以下字符之一作为转义字符（后跟反斜杠 \\）时，使用 PKCS 获取证书存在[与 SCEP 相同的](certificates-profile-scep.md#avoid-certificate-signing-requests-with-escaped-special-characters)已知问题：
> - \+
> - ;
> - ,
> - =

- **“用户”证书类型**  
  使用者名称格式的格式选项包括两个变量：公用名 (CN) 和电子邮件 (E)。 可将“公用名(CN)”设置为以下任何变量：

  - **CN={{UserName}}** ：用户的用户主体名称，例如 janedoe@contoso.com。
  - **CN={{AAD_Device_ID}}** ：在 Azure Active Directory (AD) 中注册设备时分配的 ID。 此 ID 通常用于向 Azure AD 进行身份验证。
  - **CN={{SERIALNUMBER}}** ：制造商通常用于标识设备的唯一序列号 (SN)。
  - **CN={{IMEINumber}}** ：用于标识移动电话的国际移动设备标识 (IMEI)。
  - **CN={{OnPrem_Distinguished_Name}}** ：用逗号分隔的一系列相对可分辨名称，如 CN=Jane Doe、OU=UserAccounts、DC=corp、DC=contoso、DC=com。

    要使用 {{OnPrem_Distinguished_Name}} 变量，请确保使用 [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect) 将onpremisesdistinguishedname 用户属性与 Azure AD 同步 。

  - **CN={{onPremisesSamAccountName}}** ：管理员可以使用 Azure AD 连接到名为 onPremisesSamAccountName 的属性，将 Active Directory 中的 samAccountName 属性同步到 Azure AD。 Intune 可以将该变量替换为证书使用者中的证书颁发请求的一部分。 samAccountName 属性是指用户登录名，该名称用于支持早期版本的 Windows（Windows 2000 之前）中的客户端和服务器。 用户登录名的格式为：DomainName\testUser，或仅 testUser 。

    要使用 {{onPremisesSamAccountName}} 变量，请确保使用 [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect) 将 onPremisesSamAccountName 用户属性与 Azure AD 同步 。

  通过使用这些变量的一个或多个与静态字符串的组合，可以创建一个自定义使用者名称格式，例如：  
  - CN={{UserName}},E={{EmailAddress}},OU=Mobile,O=Finance Group,L=Redmond,ST=Washington,C=US
  
  该示例包含使用者名称格式，其中除了不仅使用了 CN 和 E 变量，还使用了组织单元、组织、位置、省/直辖市/自治区和国家/地区值的字符串。 [CertStrToName 函数](/windows/win32/api/wincrypt/nf-wincrypt-certstrtonamea)介绍此函数及其支持的字符串。

- **“设备”证书类型**  
  “使用者名称格式”的格式选项包括以下变量： 
  - **{{AAD_Device_ID}}**
  - **{{Device_Serial}}**
  - **{{Device_IMEI}}**
  - **{{SerialNumber}}**
  - **{{IMEINumber}}**
  - **{{AzureADDeviceId}}**
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

## <a name="next-steps"></a>后续步骤

[使用 SCEP 证书](certificates-scep-configure.md)，或[从 Symantec PKI 管理器 Web 服务颁发 PKCS 证书](certificates-digicert-configure.md)。

[对 PKCS 证书配置文件进行故障排除](../protect/troubleshoot-pkcs-certificate-profiles.md)
