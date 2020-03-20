---
title: 对 Jamf Pro 与 Microsoft Intune 的集成进行故障排除
titleSuffix: Microsoft Intune
description: 关于将 Jamf Pro for Mac 设备与 Microsoft Intune 集成时排查一些最常见问题的建议。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 335841a8642429e36c277673fd8a238d486366c9
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79350611"
---
# <a name="troubleshoot-integration-of-jamf-pro-with-microsoft-intune"></a>对 Jamf Pro 与 Microsoft Intune 的集成进行故障排除

本文可帮助 Intune 管理员了解 Jamf Pro for macOS 与 Intune 集成的问题并对其进行故障排除。

> [!TIP]  
> 本文中的大部分信息最初出现在 support.microsoft.com 上的[排查 Jamf 与 Microsoft Intune 集成时的问题](https://support.microsoft.com/help/4519171/troubleshoot-problems-when-integrating-jamf-with-microsoft-intune)。

## <a name="prerequisites"></a>必备条件

在开始故障排除之前，请收集一些基本信息以阐明问题并缩短查找解决方案的时间。 例如，当遇到与 Jamf-Intune 集成相关的问题时，请始终验证是否满足了先决条件。 在开始故障排除之前，请查看以下注意事项：

- 查看[将Jamf Pro 与 Intune 集成](conditional-access-integrate-jamf.md#prerequisites)的先决条件。
- 所有用户都必须具有 Microsoft Intune 和 Microsoft AAD Premium P1 许可证 
- 必须具有在 Jamf Pro 控制台中拥有 Microsoft Intune 集成权限的用户帐户。
- 必须拥有在 Azure 中具有全局管理员权限的用户帐户。


调查 Jamf Pro 与 Intune 的集成时，请考虑以下信息： 
- 确切错误消息是什么？
- 错误消息位于何处？
- 何时开始出现问题？  Jamf Pro 与 Intune 的集成是否有效？
- 有多少用户受到影响？ 是所有用户都受影响还是仅仅一部分用户受影响？
- 有多少设备受到影响？ 是所有设备都受影响还是仅仅一部分设备受影响？
 

## <a name="common-problems"></a>常见问题 

以下信息可帮助你在设置 Intune 和 Jamf Pro 集成后识别并解决设备的常见问题。  

| 问题   | 更多信息                  |
|-----------------|--------------------------|
| **设备在 Jamf Pro 中被标记为无响应**  | [设备无法通过 Jamf Pro 或 Azure AD 签入](#devices-are-marked-as-unresponsive-in-jamf-pro) |
| **打开应用时，设备无法注册，Mac 设备提示进行密钥链登录**  | [系统会提示用户输入密码，以允许应用注册到 Azure AD](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app)。 |
| **设备无法注册**  | 可能的原因如下： <br> **-** [***原因 1*** - Azure 中的 Jamf Pro 应用具有不正确的权限](#cause-1) <br> **-** [***原因 2*** - Azure AD 中的 Jamf 本机 macOS 连接器存在问题](#cause-2)  <br> **-** [***原因 3*** - 用户没有有效的 Intune 或 Jamf 许可证](#cause-3) <br> **-** [***原因 4*** - 用户未使用 Jamf 自助服务来启动公司门户应用](#cause-4) <br> **-** [***原因 5*** - Intune 集成关闭](#cause-5) <br> **-** [***原因 6*** - 设备之前已在 Intune 中注册，或用户多次尝试注册设备](#cause-6) <br> **-** [***原因 7*** - JamfAAD 请求从用户的密钥链访问“Microsoft Workplace Join 密钥”](#cause-7) |
|  **Mac 设备在 Intune 中显示为兼容，但在 Azure 中显示为不兼容** | [设备注册问题](#mac-device-shows-compliant-in-intune-but-noncompliant-in-azure) |
| **使用 Jamf 注册的 Mac 设备的 Intune 控制台中出现重复条目** | [同一设备的多个注册](#duplicate-entries-appear-in-the-intune-console-for-mac-devices-enrolled-by-using-jamf) |
| **合规性策略无法评估设备** | [策略面向设备组](#compliance-policy-fails-to-evaluate-the-device) |
| **无法检索 Microsoft Graph API 的访问令牌** | 可能的原因如下： <br> -[Azure 中 Jamf Pro 应用的权限](#theres-a-permission-issue-with-the-jamf-pro-application-in-azure) <br> - [Jamf 或 Intune 许可证已过期](#a-license-required-for-jamf-intune-integration-has-expired) <br> **-** [端口未打开](#the-required-ports-arent-open-on-your-network)|
 

### <a name="devices-are-marked-as-unresponsive-in-jamf-pro"></a>设备在 Jamf Pro 中标记为无响应  

**原因**：以下是 Jamf Pro 将设备标记为“无响应”的常见原因  ：

- 设备无法使用 Jamf Pro 签入。  
  Jamf Pro 希望设备每 15 分钟签入一次。 如果设备在 24 小时内无法签入，Jamf 会将其标记为无响应。  

- 设备无法使用 Azure AD 签入。  
  成功注册到 Azure AD 后，macOS 设备将获得 Azure 令牌：
  - 此令牌每 12 小时刷新一次。   
  - 当令牌刷新失败 24 小时或更长时间时，Jamf Pro 会将设备标记为无响应。  
  - 如果 Azure 令牌过期，则会提示用户登录到 Azure 以获取新令牌。 Azure 访问的刷新令牌每七天生成一次。

**解决方法**  
Jamf Pro 将设备标记为“无响应”后，设备的已注册用户必须登录才能更正无响应状态  。 该用户必须是已加入该帐户的工作用户，因为他们在其登录密钥链中具有 Intune 中的标识。



### <a name="mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app"></a>打开应用时，Mac 设备提示进行密钥链登录  

配置 Intune 和 Jamf Pro 集成并部署条件访问策略后，使用 Jamf Pro 管理设备的用户在打开 Microsoft Office 365 应用程序（如 Teams、Outlook 和其他需要 Azure AD 身份验证的应用）时，会收到密码提示。 

例如，在打开 Microsoft Teams 时，会出现一个提示，其中包含类似于以下示例的文本：

``` 
  Microsoft Teams wants to sign using key “Microsoft Workplace Join Key” in your keychain.  
  To allow this, enter the “login” keychain password 
```

**原因**：这些提示由 Jamf Pro 为需要 Azure AD 注册的每个适用应用生成。 

**解决方法**   
在提示下，用户必须提供其设备密码才能登录 Azure AD。 选项包括：
- **拒绝** - 不登录并且不使用应用。
- **允许** - 一次性登录。 下次应用打开时，系统会提示再次登录。
- **始终允许** - 为应用程序缓存登录凭据。 下次应用打开时，系统不会提示登录。  

仅为一个应用选择“始终允许”可批准该应用以供将来登录  。 其他应用会提示进行身份验证，直到它们也设置为“始终允许”  。 一个应用的缓存凭据不能由另一个应用使用。  

### <a name="devices-fail-to-register"></a>设备无法注册  

对于无法注册的 Mac 设备，有几个常见的原因。  

#### <a name="cause-1"></a>原因 1  

**Azure 中的 Jamf Pro 企业应用程序具有错误的权限或具有多个权限**  

  在 Azure 中创建应用时，必须删除所有默认 API 权限，然后为 Intune 分配一个 update_device_attributes 权限  。 

  **解决方法**  
  查看并在必要时更正在 Azure AD 中创建的 Jamf 应用的权限。 请参阅[在 Azure AD 中为 Jamf 创建应用程序](conditional-access-integrate-jamf.md#create-an-application-in-azure-active-directory)的过程。 

#### <a name="cause-2"></a>原因 2  

未在 Azure AD 租户中创建 Jamf 本机 macOS 连接器应用，或者该连接器的同意是由没有全局管理员权限的帐户签署的   

  **解决方法**  
  请参阅 docs.jamf.com 上的[与 Microsoft Intune 集成](https://docs.jamf.com/10.13.0/jamf-pro/administrator-guide/Integrating_with_Microsoft_Intune.html)中的“配置 macOS Intune 集成”部分  。 

#### <a name="cause-3"></a>原因 3

**用户没有有效的 Intune 或 Jamf 许可证**  

  缺少有效的许可证可导致以下错误，这表明 Jamf 许可证已过期：  
  ```
    Unable to connect to Microsoft Intune.  
    
    Check your Microsoft Intune Integration configuration.
  ```  

  **解决方法**
  - Jamf 许可证：请联系 Jamf 获得帮助，以获取 Jamf 的新许可证。  
  - Intune 许可证：为用户分配有效的许可证，或与 Microsoft 或合作伙伴联系，获取有关如何获取当前许可证的信息。

#### <a name="cause-4"></a>原因 4  

用户未使用 Jamf 自助服务来启动公司门户应用 

若要让设备通过 Jamf 成功注册到 Intune，用户必须使用 Jamf 自助服务打开 Intune 公司门户。 如果用户手动打开公司门户，设备将无需连接到 Jamf 即可进行注册。  

若要确定设备用于注册的服务，请查看设备上的公司门户应用。 通过 Jamf 注册后，你应该会收到通知，提示你打开自助服务应用以进行更改。

在公司门户应用中，用户可能会看到 `Not registered`，并且公司门户日志中可能会出现类似于以下示例的条目  ：  

```
   Line 7783: <DATE> <IP ADDRESS> INFO com.microsoft.ssp.application TID=1  
 
   WelcomeViewController.swift: 253 (startLogin()) Portal launched without WPJ only arg while account is under partner management
```

**解决方法**  
若要将注册源从 Intune 更改为 Jamf：
1. [从 Intune 取消注册 macOS 设备](https://docs.microsoft.com/user-help/unenroll-your-device-from-intune-macos)。 若要避免未从 Intune 中完全删除的设备造成更多麻烦，请参阅此原因列表中的[原因 6](#cause-6)  。  

2. 在设备上，使用 Jamf 自助服务打开公司门户应用，然后使用 Intune 注册设备。 此任务要求你[使用 Jamf 来部署适用于 macOS 的公司门户应用](conditional-access-assign-jamf.md#deploy-the-company-portal-app-for-macos-in-jamf-pro)，并[在 Jamf Pro 中创建了一个使用 Azure AD 注册用户设备的策略](conditional-access-assign-jamf.md#create-a-policy-in-jamf-pro-to-have-users-register-their-devices-with-azure-active-directory)。  

3. 门户打开时，你看到的第一个屏幕会提示登录。 使用你的工作或学校帐户  

4. 公司门户确认帐户信息后会显示“设备注册”和“设备符合性”状态。 黄色三角形突出显示保护学校或工作 macOS 设备需采取的操作。 单击“开始”可开始注册。  

5. 如果系统出现提示，请键入计算机的登录信息。  
     
在管理中注册设备可能需要几分钟时间。 在此期间，可在设备上执行其他操作。 完成公司访问设置后，将收到一条消息，通知操作已完成。

#### <a name="cause-5"></a>原因 5  

**Intune 集成关闭**

如果 Intune 集成关闭，则在用户尝试注册设备时，会在公司门户收到一个显示以下消息的弹出窗口：  

```
   Invalid command line input
   
   Registration-only command line flag (-r) can only be used when partner management is enabled in Intune. Please contact your IT admin.
```  

关闭集成后，Jamf Pro 服务器会向 Intune 服务器发送一个脉冲，告知 Intune 已禁用集成。 

**解决方法**  
在 Jamf Pro 中重新启用 Intune 集成。 请参阅[在 Jamf Pro 中配置 Microsoft Intune 集成](conditional-access-integrate-jamf.md#enable-intune-to-integrate-with-jamf-pro)。


#### <a name="cause-6"></a><a name="cause-6"></a>原因 6  

**设备之前已在 Intune 中注册，或用户多次尝试注册设备**

如果设备未在 Jamf 中注册，但未从 Intune 中正确删除，或进行了多次注册尝试，则可能会在门户中看到同一设备的多个实例。 这会导致 Jamf 注册失败。

**解决方法**  
1. 在 Mac 上，启动“终端”  。
2. 运行“sudo JAMF removemdmprofile”  。
3. 运行“sudo JAMF removeFramework”  。
4. 在 JAMF Pro 服务器上，删除计算机的清单记录。
5. 从 AzureAD 中删除设备。
6. 删除设备上的以下文件（如果存在）：
   - /Library/Application Support/com.microsoft.CompanyPortal.usercontext.info
   - /Library/Application Support/com.microsoft.CompanyPortal
   - /Library/Application Support/com.jamfsoftware.selfservice.mac
   - /Library/Saved Application
   - State/com.jamfsoftware.selfservice.mac.savedState
   - /Library/Saved Application State/com.microsoft.CompanyPortal.savedState
   - /Library/Preferences/com.microsoft.CompanyPortal.plist
   - /Library/Preferences/com.jamfsoftware.selfservice.mac.plist
   - /Library/Preferences/com.jamfsoftware.management.jamfAAD.plist
   - /Users/<username>/Library/Cookies/com.microsoft.CompanyPortal.binarycookies
   - /Users/<username>/Library/Cookies/com.jamf.management.jamfAAD.binarycookies
   - com.microsoft.CompanyPortal
   - com.microsoft.CompanyPortal.HockeySDK
   - enterpriseregistration。windows。net
   - https://device.login.microsoftonline.com
   - https://device.login.microsoftonline.com/
   - Microsoft 会话传输密钥（公钥和私钥）
   - Microsoft Workplace Join 密钥（公钥和私钥）
7. 从设备上的密钥链中删除引用 Microsoft、Intune 或公司门户的所有内容，包括 DeviceLogin.microsoft.com 证书    。 删除除 JAMF 公钥和私钥外的 JAMF 引用  。 
   > [!IMPORTANT]  
   > 删除公钥和私钥将中断设备注册。

8. 删除你找到的以下任何条目：  
   - 种类：应用程序密码；帐户：com.microsoft.workplacejoin.thumbprint
   - 种类：应用程序密码；帐户：com.microsoft.workplacejoin.registeredUserPrincipalName
   - 种类：证书；颁发者：MS-Organization-Access
   - 种类：标识首选项；名称（如果存在，则为 ADFS STS URL）： https://adfs\<DNSName>.com/adfs/ls
   - 种类：标识首选项；名称： https://enterpriseregistration.windows.net
   - 种类：标识首选项；名称： https://enterpriseregistration.windows.net/  
9. 重启 Mac 设备。
10. 从设备中卸载公司门户。
11. 请转到 portal.manage.microsoft.com 并删除 Mac 设备的所有实例。 等待至少 30 分钟，然后再执行下一步。
12. 在 JAMF Pro 中重新注册设备。
13. 重新打开自助服务并启动注册策略。


#### <a name="cause-7"></a>原因 7  

**JamfAAD 请求从用户的密钥链访问“Microsoft Workplace Join 密钥”**

注册期间，macOS 设备的用户将收到以下提示，以允许 JamfAAD 从其密钥链访问密钥： 

```
   JamfAAD wants to access key “Microsoft Workplace Join Key" in your keychain. 
    
   To allow this, enter the “login” keychain password
```

**解决方法**  
若要成功使用 Azure AD 注册设备，Jamf 要求用户提供其帐户密码，并选择“允许”  。

此请求类似于本文前面的[在打开应用时，Mac 设备提示输入密钥链登录](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app)的请求。  

 
### <a name="mac-device-shows-compliant-in-intune-but-noncompliant-in-azure"></a>Mac 设备在 Intune 中显示为兼容，但在 Azure 中显示为不兼容  

**原因**：以下情况可能导致设备在 Intune 中显示为兼容，但在 Azure 中显示为不兼容：  
- 设备未正确注册。  
- 该设备已多次注册而未进行必要的清理。

**解决方法**  
若要解决此问题，请按照本文前面的针对设备注册失败的[*原因 6*](#cause-6) 的解决方案进行操作  。 


### <a name="duplicate-entries-appear-in-the-intune-console-for-mac-devices-enrolled-by-using-jamf"></a>使用 Jamf 注册的 Mac 设备的 Intune 控制台中出现重复条目  
 
**原因**：多次使用 Intune 注册设备，通常会在从 Intune 中删除设备后重新注册。  

从 Intune 和 Jamf Pro 集成中删除设备后，可能会遗留某些数据，这可能会导致连续注册创建重复条目。  

**解决方法**  
若要解决此问题，请按照本文前面的针对设备注册失败的[*原因 6*](#cause-6) 的解决方案进行操作  。 

### <a name="compliance-policy-fails-to-evaluate-the-device"></a>合规性策略无法评估设备  

**原因**：Jamf 与 Intune 的集成不支持针对设备组的符合性策略。 

**解决方法**  
修改要分配给用户组的 macOS 设备的合规性策略。 


### <a name="could-not-retrieve-the-access-token-for-microsoft-graph-api"></a>无法检索 Microsoft Graph API 的访问令牌

收到以下错误：

```
   Could not retrieve the access token for Microsoft Graph API. Check the configuration for Microsoft Intune Integration.
```   

此错误的源可能是以下某种原因： 

#### <a name="theres-a-permission-issue-with-the-jamf-pro-application-in-azure"></a>Azure 中的 Jamf Pro 应用存在权限问题

在 Azure 中注册 Jamf Pro 应用时，会出现以下某种情况：  
- 应用获得了多个权限。
- 未选择“授予 \<你的公司> 管理许可”选项  。  

**解决方法**  
请参阅本文前面的[设备注册失败](#devices-fail-to-register)的原因 1 的解决方案。

#### <a name="a-license-required-for-jamf-intune-integration-has-expired"></a>Jamf-Intune 集成所需的许可证已过期

**解决方法**：请参阅[设备注册失败](#devices-fail-to-register)的原因 3 的解决方案。 

#### <a name="the-required-ports-arent-open-on-your-network"></a>网络上未打开所需的端口

**解决方法**：查看将 Jamf Pro 与 Intune 集成的[先决条件](conditional-access-integrate-jamf.md#prerequisites)中的网络端口的信息。


## <a name="next-steps"></a>后续步骤
了解有关[将 Jamf Pro 与 Intune 集成](conditional-access-integrate-jamf.md)的详细信息