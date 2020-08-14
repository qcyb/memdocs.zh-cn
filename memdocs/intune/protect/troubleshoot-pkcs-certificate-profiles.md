---
title: 对使用 PKCS 证书配置文件预配用于 Microsoft Intune 的证书进行故障排除 | Microsoft Docs
description: 对设备使用私钥和公钥对 (PKCS) 配置文件来请求获取用于 Intune 的证书进行故障排除。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/11/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2c6f2eb7d6174c706cdd8a3910df1d0ddc2e6ef0
ms.sourcegitcommit: 532a06163f462527254d23e7dc505b18c0c4f938
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/11/2020
ms.locfileid: "88110675"
---
# <a name="troubleshoot-pkcs-certificate-deployment-in-microsoft-intune"></a>对 Microsoft Intune 中的 PKCS 证书部署进行故障排除

本文中的信息有助于解决在 Microsoft Intune 中部署私钥和公钥对 (PKCS) 证书时遇到的几个常见问题。 在进行故障排除之前，请确保已按照[配置 PKCS 证书并用于 Intune](../protect/certficates-pfx-configure.md#export-the-root-certificate-from-the-enterprise-ca) 中所述完成以下任务：

- 查阅[使用 PKCS 证书配置文件的要求](../protect/certficates-pfx-configure.md#requirements)
- 从企业证书颁发机构 (CA) 中导出根证书
- 配置证书颁发机构上的证书模板
- 安装并配置 Intune 证书连接器
- 创建并部署受信任的证书配置文件，以部署根证书
- 创建并部署 PKCS 证书配置文件

导致出现 PKCS 证书配置文件故障的最常见原因是，PKCS 证书配置文件的配置不当。 请审阅配置文件配置，查找服务器名称或完全限定的域名 (FQDN) 中是否有拼写错误，并确认“证书颁发机构”和“证书颁发机构名称”正确无误。

- **证书颁发机构**：“证书颁发机构”计算机的内部 FQDN。 例如，server1.domain.local。
- 证书颁发机构名称：证书颁发机构 MMC 中显示的证书颁发机构名称。 请在“证书颁发机构(本地)”下查看

可以对 CA 使用 [certutil 命令行程序](https://docs.microsoft.com/windows-server/administration/windows-commands/certutil)，以确认“证书颁发机构”和“证书颁发机构名称”的名称是否正确。

## <a name="pkcs-communication-overview"></a>PKCS 通信概述

下图提供了对 Intune 中的 PKCS 证书部署过程的基本概述。

> [!div class="mx-imgBorder"]
> ![PKCS 证书配置文件流](./media/troubleshoot-pkcs-certificate-profiles/pkcs-overview-graphic.png)

1. 管理员在 Intune 中创建 PKCS 证书配置文件。
2. Intune 服务请求本地 Intune 证书连接器为用户新建证书。
3. Intune 证书连接器向 Microsoft 证书颁发机构发送 PFX Blob 和请求。
4. 证书颁发机构颁发 PFX 用户证书，并将证书发送回 Intune 证书连接器。
5. Intune 证书连接器将加密的 PFX 用户证书上传到 Intune。
6. Intune 解密 PFX 用户证书，并使用设备管理证书为设备重新加密。  然后，Intune 向设备发送 PFX 用户证书。
7. 设备向 Intune 报告证书状态。

## <a name="data-and-log-files"></a>数据和日志文件

若要确定通信和证书预配工作流的问题，请查看来自服务器基础结构和设备的日志文件。 后面关于排除 PKCS 证书配置文件故障的部分引用此部分中提到的日志文件。

- [基础结构和服务器日志](#logs-for-on-premises-infrastructure)

设备日志取决于设备平台：

- [iOS 和 iPadOS](#logs-for-ios-and-ipados-devices)
- [Android](#logs-for-android-devices)
- [Windows](#logs-for-windows-devices)

### <a name="logs-for-on-premises-infrastructure"></a>本地基础结构日志
  
支持使用 PKCS 证书配置文件来部署证书的本地基础结构包括，Microsoft Intune 证书连接器、在 Windows Server 上运行的 NDES 和证书颁发机构。

这些角色的日志文件包括 Windows 事件查看器、证书控制台和特定于 Intune 证书连接器、NDES 或及本地基础结构中的其他角色和操作的各种日志文件。

- **NDESConnector_date_time.svclog**：

  此日志显示从 Microsoft Intune 证书连接器到 Intune 云服务的通信。 可使用[服务跟踪查看器工具](https://docs.microsoft.com/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe)查看此日志文件。

  相关注册表项：*HKLM\SW\Microsoft\MicrosoftIntune\NDESConnector\ConnectionStatus*

  位置：在承载 NDES 的服务器上，位置为 %program_files%\Microsoft intune\ndesconnectorsvc\logs\logs

- **CertificateRegistrationPoint_date_time.svclog**：

  此日志显示接收和验证证书请求的 NDES 策略模块。 可使用[服务跟踪查看器工具](https://docs.microsoft.com/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe)查看此日志文件。

  位置：在承载 NDES 的服务器上，位置为 %program_files%\Microsoft intune\ndesconnectorsvc\logs\logs

- **NDESPlugin.log**：

  此日志显示向证书注册点传递证书请求的情况，以及这些请求的验证结果。

  位置：在承载 NDES 的服务器上，位置为 %program_files%\Microsoft Intune\NDESPolicyModule\logs

- **Windows 应用程序日志**：

  位置：在承载 NDES 的服务器上：运行 eventvwr.msc 以打开 Windows 事件查看器

### <a name="logs-for-android-devices"></a>适用于 Android 设备的日志

对于运行 Android 的设备，请使用“Android 公司门户”应用日志文件“OMADM.log”。 收集和查看日志之前，请确保已启用[详细日志记录](../user-help/use-verbose-logging-to-help-your-it-administrator-fix-device-issues-android.md)，然后重现该问题。

若要从设备收集 OMADM.log，请参阅[使用 USB 电缆上传日志和通过电子邮件发送日志](../user-help/send-logs-to-your-it-admin-using-cable-android.md)。

还可以参阅[上传日志和通过电子邮件发送日志](../user-help/send-logs-to-your-it-admin-by-email-android.md#upload-and-email-logs-from-microsoft-intune-app)来获取支持。

### <a name="logs-for-ios-and-ipados-devices"></a>适用于 iOS 和 iPadOS 设备的日志

对于运行 iOS/iPadOS 的设备，请使用调试日志和在 Mac 计算机上运行的 Xcode：

1. 将 iOS/iPadOS 设备连接到 Mac，然后转到“应用程序” > “实用程序”以打开控制台应用程序 。

2. 在“操作”下，选择“包含信息消息”和“包含调试消息”。

   ![选择日志选项](../protect/media/troubleshoot-pkcs-certificate-profiles/message-options.png)

3. 重现该问题，然后将日志保存到文本文件中：
   1. 选择“编辑” > “选择全部”以选择当前屏幕上的所有消息，然后选择“编辑” > “复制”将消息复制到剪贴板。
   2. 打开 TextEdit 应用程序，将复制的日志粘贴到新文本文件中，然后保存该文件。

适用于 iOS 和 iPadOS 设备的公司门户日志不包含 PKCS 证书配置文件的相关信息。

### <a name="logs-for-windows-devices"></a>Windows 设备日志

对于运行 Windows 的设备，请使用 Windows 事件日志诊断使用 Intune 管理的设备的注册或设备管理问题。

在设备上，打开“事件查看器” > “应用程序和服务日志” > “Microsoft” > “Windows” > “DeviceManagement-Enterprise-Diagnostics-Provider”

![Windows 事件日志](../protect/media/troubleshoot-pkcs-certificate-profiles/windows-event-log.png)

## <a name="antivirus-exclusions"></a>防病毒排除项

出现以下情况时，请考虑在托管 NDES 或证书连接器的服务器上添加防病毒排除项：

- 证书请求到达服务器或 Intune 证书连接器，但未得到成功处理 
- 颁发证书的速度缓慢

下面是你可能排除的位置的示例：

- %program_files%\Microsoft Intune\PfxRequest
- %program_files%\Microsoft Intune\CertificateRequestStatus
- %program_files%\Microsoft Intune\CertificateRevocationStatus

## <a name="common-errors"></a>常见错误

下面这一部分逐个介绍了以下常见错误：

- [RPC 服务器不可用 0x800706ba](#the-rpc-server-is-unavailable-0x800706ba)
- [找不到注册策略服务器 0x80094015](#an-enrollment-policy-server-cannot-be-located-0x80094015)
- [提交被挂起](#the-submission-is-pending)
- [参数不正确 0x80070057](#the-parameter-is-incorrect-0x80070057)
- [被策略模块拒绝](#denied-by-policy-module)
- [证书配置文件停留在“挂起”状态](#certificate-profile-stuck-as-pending)
- [错误 -2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED](#error--2146875374-certsrv_e_subject_email_required)

### <a name="the-rpc-server-is-unavailable-0x800706ba"></a>RPC 服务器不可用 0x800706ba

在 PFX 部署过程中，受信任的根证书显示在设备上，但 PFX 证书未显示在设备上。 NDESConnector 日志文件包含字符串“The RPC server is unavailable.0x800706ba”，如以下示例中的第一行所示：

```
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x800706BA): CCertRequest::Submit: The RPC server is unavailable. 0x800706ba (WIN32: 1722 RPC_S_SERVER_UNAVAILABLE)
IssuePfx -Generic Exception: System.ArgumentException: CCertRequest::Submit: The parameter is incorrect. 0x80070057 (WIN32: 87 ERROR_INVALID_PARAMETER)
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x80094800): The requested certificate template is not supported by this CA. (Exception from HRESULT: 0x80094800)
```

#### <a name="cause-1---incorrect-configuration-of-the-ca-in-intune"></a>原因 1 - Intune 中的 CA 配置不正确

如果 PKCS 证书配置文件指定了不正确的服务器，或者包含 CA 的名称或 FQDN 的拼写错误，可能会出现此问题。 CA 是在配置文件的以下属性中指定：

- Certification auth或ity
- 证书颁发机构名

**解决方法**：

审阅以下设置，并修复发现的不正确设置：

- “证书颁发机构”属性显示 CA 服务器的内部 FQDN。
- “证书颁发机构名称”属性显示 CA 的名称。

#### <a name="cause-2---ca-doesnt-support-certificate-renewal-for-requests-signed-by-previous-ca-certificates"></a>原因 2 - CA 不支持对由旧 CA 证书进行签名的请求进行证书续订

如果 PKCS 证书配置文件中的 CA FQDN 和名称是正确的，请审阅证书颁发机构服务器上的 Windows 应用程序日志。 查找以下示例中所示的“事件 ID 128”：

```
Log Name: Application:
Source: Microsoft-Windows-CertificationAuthority
Event ID: 128
Level: Warning
Details:
An Authority Key Identifier was passed as part of the certificate request 2268. This feature has not been enabled. To enable specifying a CA key for certificate signing, run: "certutil -setreg ca\UseDefinedCACertInRequest 1" and then restart the service.
```

当 CA 证书续订时，它必须签名联机证书状态协议 (OCSP) 响应签名证书。 签名后，OCSP 响应签名证书可以通过检查吊销状态来验证其他证书。 此签名在默认情况下是不启用的。

**解决方法**：

手动强制签名证书：

1. 在 CA 服务器上，打开提升的命令提示符，并运行以下命令：certutil -setreg ca\UseDefinedCACertInRequest 1
2. 重启“证书服务”服务。

在“证书服务”服务重启后，设备就可以收到证书了。

### <a name="an-enrollment-policy-server-cannot-be-located-0x80094015"></a>找不到注册策略服务器 0x80094015

“An enrollment policy server cannot be located”和“0x80094015”，如下面的示例所示：

```
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x80094015): An enrollment policy server cannot be located. (Exception from HRESULT: 0x80094015)
```

#### <a name="cause---certificate-enrollment-policy-server-name"></a>原因 - 证书注册策略服务器名称

如果托管 Intune NDES 连接器的计算机找不到证书注册策略服务器，就会出现此问题。

**解决方法**：

在托管 NDES 连接器的计算机上，手动配置证书注册策略服务器的名称。 若要配置此名称，请使用 [Add-CertificateEnrollmentPolicyServer](https://docs.microsoft.com/powershell/module/pkiclient/add-certificateenrollmentpolicyserver?view=win10-ps) PowerShell cmdlet。

### <a name="the-submission-is-pending"></a>提交被挂起

在你将 PKCS 证书配置文件部署到移动设备后，无法获得证书，并且 NDESConnector 日志包含字符串“The submission is pending”，如下面的示例所示：

```
IssuePfx - The submission is pending: Taken Under Submission
IssuePfx -Generic Exception: System.InvalidOperationException: IssuePfx - The submission is pending
```

此外，在证书颁发机构服务器上，可以在“挂起的请求”文件夹中看到 PFX 请求：

> [!div class="mx-imgBorder"]
> ![证书颁发机构服务器上的“挂起的请求”文件夹的屏幕截图](./media/troubleshoot-pkcs-certificate-profiles/pending-requests.png)

#### <a name="cause---incorrect-configuration-for-request-handling"></a>原因 - 请求处理配置不正确

如果在证书颁发机构“属性” > “策略模块” > “属性”对话框中选中“将请求状态设置为‘挂起’。管理员必须显式颁发证书”选项，就会出现此问题。

> [!div class="mx-imgBorder"]
> ![策略模块属性的屏幕截图](./media/troubleshoot-pkcs-certificate-profiles/policy-module-properties.png)

**解决方法**：

编辑策略模块属性，以设置以下选项：“遵循证书模板中的设置(如果适用)。否则，自动颁发证书。”

### <a name="the-parameter-is-incorrect-0x80070057"></a>参数不正确 0x80070057

在 Intune 证书连接器成功安装并配置后，设备没有收到 PKCS 证书，且 NDESConnector 日志包含字符串“The parameter is incorrect.0x80070057”，如下面的示例所示：

```
CCertRequest::Submit: The parameter is incorrect. 0x80070057 (WIN32: 87 ERROR_INVALID_PARAMETER)
```

#### <a name="cause---configuration-of-the-pkcs-profile"></a>原因 - PKCS 配置文件的配置

如果 Intune 中的 PKCS 配置文件配置错误，就会出现此问题。 以下是常见的错误配置：

- 配置文件包含不正确的 CA 名称。
- 为使用者可选名称 (SAN) 配置了电子邮件地址，但目标用户尚无有效的电子邮件地址。 这种组合导致 SAN 的值是无效的 null。

**解决方法**：

验证 PKCS 配置文件的以下配置，然后等待策略在设备上进行刷新：

- 是否配置有 CA 名称
- 是否分配到正确的用户组
- 组中的用户是否有有效的电子邮件地址

有关详细信息，请参阅[配置 PKCS 证书并用于 Intune](../protect/certficates-pfx-configure.md)。

### <a name="denied-by-policy-module"></a>被策略模块拒绝

如果设备收到受信任的根证书，但没有收到 PFX 证书，NDESConnector 日志包含字符串“The submission failed:Denied by Policy Module”，如下面的示例所示：

```
IssuePfx - The submission failed: Denied by Policy Module
IssuePfx -Generic Exception: System.InvalidOperationException: IssuePfx - The submission failed
   at Microsoft.Management.Services.NdesConnector.MicrosoftCA.GetCertificate(PfxRequestDataStorage pfxRequestData, String containerName, String& certificate, String& password)
Issuing Pfx certificate for Device ID <Device ID> failed  
```

#### <a name="cause--computer-account-permissions-to-the-certificate-template"></a>原因 - 计算机帐户对证书模板的权限

如果托管 Intune 证书连接器的服务器的计算机帐户没有对证书模板的相应权限，就会出现此问题。

**解决方法**：

1. 使用具有管理权限的帐户登录到企业 CA。
2. 打开“证书颁发机构”控制台，右键单击“证书模板”，然后选择“管理”。
3. 找到证书模板，然后打开模板的“属性”对话框。
4. 选择“安全性”选项卡，然后为其中安装了 Microsoft Intune 证书连接器的服务器添加计算机帐户。 向此帐户授予“读取”和“注册”权限。
5. 依次选择“应用” > “确定”，以保存证书模板，然后关闭“证书模板”控制台。
6. 在“证书颁发机构”控制台中，右键单击“证书模板” > “新建” > “要颁发的证书模板”。
7. 选择所修改的模板，然后单击“确定”。

有关详细信息，请参阅[配置 CA 上的证书模板](../protect/certficates-pfx-configure.md#configure-certificate-templates-on-the-ca)。

### <a name="certificate-profile-stuck-as-pending"></a>证书配置文件停留在“挂起”状态

在 Microsoft Endpoint Manager 管理中心内，PKCS 证书配置文件无法部署，状态为“挂起”。 NDESConnector 日子文件中没有明显的错误。
由于日志中没有明确标识此问题的原因，因此请逐步排查以下原因。

#### <a name="cause-1---unprocessed-request-files"></a>原因 1 - 未处理的请求文件

审阅请求文件中是否有指明为什么无法处理这些文件的错误。

1. 在托管 NDES 连接器的计算机上，使用文件资源管理器转到“%programfiles%\Microsoft Intune\PfxRequest”。
2. 使用常用的文本编辑器审阅“失败”和“正在处理”文件夹中的文件。

   > [!div class="mx-imgBorder"]
   > ![审阅 PfxRequest 文件夹](./media/troubleshoot-pkcs-certificate-profiles/pfxrequest-folder.png)

3. 在这些文件中，查找指明错误或问题的条目。 通过基于 Web 的搜索来查找错误消息，以获取关于为什么无法处理请求的提示，以及这些问题的解决方案。

#### <a name="cause-2---misconfiguration-for-the-pkcs-certificate-profile"></a>原因 2 - PKCS 证书配置文件配置错误

如果在“失败”、“正在处理”或“成功”文件夹中找不到请求文件，则原因可能是与 PKCS 证书配置文件关联的证书不正确。 例如，与配置文件关联的是从属 CA，或使用了不正确的根证书。

**解决方法**：

1. 审阅受信任的证书配置文件，以确保已将来自企业 CA 的根证书部署到设备。
2. 审阅 PKCS 证书配置文件，以确保它引用正确的 CA、证书类型，以及将根证书部署到设备的受信任的证书配置文件。

有关详细信息，请参阅在 Microsoft Intune 中[使用证书进行身份验证](../protect/certificates-configure.md)。

### <a name="error--2146875374-certsrv_e_subject_email_required"></a>错误 -2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED

PKCS 证书无法部署，且发证 CA 上的证书控制台显示包含字符串“-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED”的消息，如下面的示例所示：

```
Active Directory Certificate Services denied request abc123 because The Email name is unavailable and cannot be added to the Subject or Subject Alternate name. 0x80094812 (-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED). The request was for CN=” Common Name”.  Additional information: Denied by Policy Module”.
```

#### <a name="cause---supply-in-the-request-is-miscongifured"></a>原因 - 未正确配置“在请求中提供”

如果没有启用证书模板“属性”对话框的“使用者名称”选项卡中的“在请求中提供”选项，就会出现此问题。

> [!div class="mx-imgBorder"]
> ![配置 NDES 属性](./media/troubleshoot-pkcs-certificate-profiles/supply-in-the-request.png)

**解决方法**：

通过编辑模板来解决配置问题：

1. 使用具有管理权限的帐户登录到企业 CA。
2. 打开“证书颁发机构”控制台，右键单击“证书模板”，然后选择“管理”。
3. 打开证书模板的“属性”对话框。
4. 在“使用者名称”选项卡上，选择“在请求中提供”。
5. 选择“确定”来保存证书模板，然后关闭“证书模板”控制台。
6. 在“证书颁发机构”控制台中，右键单击“模板” > ，然后依次选择“新建” > “要颁发的证书模板”。
7. 依次选择所修改的模板和“确定”。

## <a name="next-steps"></a>后续步骤

如果仍需要解决方案，或要详细了解 Intune，请在 [Microsoft Intune 论坛](https://social.technet.microsoft.com/Forums/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)中发布问题。 许多支持工程师、MVP 和我们开发团队的成员都经常访问此论坛，所以很有可能有人可以提供帮助。

若要向 Microsoft Intune 产品支持团队开立支持请求，请参阅[如何获取 Microsoft Intune 支持](../fundamentals/get-support.md)。
若要详细了解 PKCS 证书部署，请参阅以下文章：

- [配置 PKCS 证书并用于 Intune](../protect/certficates-pfx-configure.md)
- [在 Microsoft Intune 中为设备配置证书配置文件](../protect/certificates-configure.md)
- [在 Microsoft Intune 中删除 SCEP 和 PKCS 证书](../protect/remove-certificates.md)
