---
title: 设置注册状态页
titleSuffix: Microsoft Intune
description: 为注册 Windows 10 设备的用户设置问候语页面。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/10/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 8518d8fa-a0de-449d-89b6-8a33fad7b3eb
ms.reviewer: ericor
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 75f6585144f62636033c94f701a57cb70e018c26
ms.sourcegitcommit: 47ed9af2652495adb539638afe4e0bb0be267b9e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/10/2020
ms.locfileid: "88051574"
---
# <a name="set-up-the-enrollment-status-page"></a>设置注册状态页
 
[!INCLUDE [azure_portal](../includes/azure_portal.md)]
 
注册状态页 (ESP) 显示注册新设备后以及新用户登录该设备时的预配过程。  这使 IT 管理员能够选择性地阻止对设备的访问，直到设备完全预配，同时向用户提供有关预配过程中剩余任务的信息。

ESP 可以作为任何 [Windows Autopilot](../../autopilot/index.yml) 预配方案的一部分使用，也可以作为 Azure AD 联接的默认开箱即用体验 (OOBE) 的一部分与 Windows Autopilot 分开使用，对首次登录设备的任何新用户也适用。

可以创建具有不同配置的多个注册状态页配置文件，以指定以下内容：

- 显示安装进度
- 阻止访问，直到完成预配过程
- 时间限制
- 允许的故障排除操作

这些配置文件按优先级顺序指定；将使用适用的最高优先级。  每个 ESP 配置文件都可以针对包含设备或用户的组。  确定要使用的配置文件时，请遵循以下标准：

- 将首先使用针对设备的最高优先级配置文件。
- 如果没有针对设备的配置文件，则将使用针对当前用户的最高优先级配置文件。  （这仅适用于存在用户的情况。 在白手套和自部署情景中，只能使用设备目标。）
- 如果没有针对特定组的配置文件，则将使用默认 ESP 配置文件。

## <a name="available-settings"></a>可用设置

可以配置以下设置，以自定义注册状态页的行为：

<table>
<th align="left">设置<th align="left">是<th align="left">否
<tr><td>显示应用和配置文件安装进度<td>显示注册状态页。<td>不显示注册状态页。
<tr><td>在安装所有应用和配置文件之前阻止设备使用<td>可以使用此表中的设置自定义注册状态页的行为，以便用户可以解决潜在的安装问题。
<td>显示注册状态页，其中不包含可解决安装故障的其他选项。
<tr><td>出现安装错误时允许用户重置设备<td>出现安装故障时显示“重置设备”按钮。<b></b><td>出现安装故障时不显示“重置设备”按钮。<b></b>
<tr><td>出现安装错误时允许用户使用设备<td>出现安装故障时显示“仍然继续”按钮。<b></b><td>出现安装故障时不显示“仍然继续”按钮。<b></b>
<tr><td>安装时间超出指定的分钟数时显示超时错误<td colspan="2">指定等待安装完成所需的分钟数。 将输入默认值 60 分钟。
<tr><td>出现错误时显示自定义消息<td>提供一个文本框，可以在其中指定出现安装错误时要显示的自定义消息。<td>显示默认的消息： <br><b>安装超出组织设置的时间限制。 请重试，也可联系你的 IT 支持人员以获取帮助。<b>
<tr><td>允许用户收集与安装错误有关的日志<td>若出现安装错误，将显示“收集日志”按钮。<b></b> <br>若用户单击此按钮，将要求他们选择一个位置，以用于保存日志文件“MDMDiagReport.cab”<b></b><td>出现安装错误时不显示“收集日志”按钮。<b></b>
<tr><td>如果这些所需应用已分配给用户/设备，则在安装这些应用之前阻止设备使用<td colspan="2">选择“全部”或“已选择”。<b></b><b></b> <br><br>若选择了“已选择”，将显示“所选应用”按钮，以允许你选择启用设备前必须安装的应用。<b></b><b></b>
</table>

## <a name="turn-on-default-enrollment-status-page-for-all-users"></a>为所有用户启用默认注册状态页

若要启用注册状态页，请执行以下步骤。
 
1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“设备” > “Windows” > “Windows 注册” > “注册状态页”   。
2. 在“注册状态页”边栏选项卡中，选择“默认” > “设置”  。
3. 有关“显示应用和配置文件安装进度”，请选择“是” 。
4. 选择要打开的其他设置，然后选择“保存”。

## <a name="create-enrollment-status-page-profile-and-assign-to-a-group"></a>创建注册状态页配置文件并将其分配到组

1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“设备” > “Windows” > “Windows 注册” > “注册状态页” > “创建配置文件”    。
2. 提供名称和说明 。
3. 选择“创建”。
4. 在“注册状态页”列表中选择新配置文件。
5. 选择“分配” > “选择组”> 选择要采用此配置文件的组 >“选择” > “保存”   。
6. 选择“设置”> 选择要应用于此配置文件的设置 >“保存” 。

## <a name="set-the-enrollment-status-page-priority"></a>设置注册状态页的优先级

设备或用户可以处于多个组中，并且具有多个注册状态页配置文件作为目标。 若要控制首先考虑哪些配置文件，可以为每个配置文件设置优先级；优先级较高的配置文件将首先考虑。

1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“设备” > “Windows” > “Windows 注册” > “注册状态页”   。
2. 将鼠标悬停在列表中的配置文件上。
3. 使用三个垂直点，将该配置文件拖到列表中的所需位置。

## <a name="block-access-to-a-device-until-a-specific-application-is-installed"></a>在安装特定应用程序之前阻止访问设备

你可以指定在注册状态页 (ESP) 完成之前必须安装的应用。

1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“设备” > “Windows” > “Windows 注册” > “注册状态页”   。
2. 选择配置文件 >“设置”。
3. 有关“显示应用和配置文件安装进度”，请选择“是” 。
4. 有关“在安装所有应用和配置文件之前阻止设备使用”，请选择“是” 。
5. 有关“如果这些所需应用已分配给用户/设备，则在安装这些应用之前阻止设备使用”，请选择“已选择” 。
6. 选择“选择应用”> 选择应用 >“选择” > “保存”。

Intune 使用此列表中包含的应用来筛选应被视为要阻止的列表。  它并未指定应安装的应用。  例如，如果将此列表配置为包含“应用 1”、“应用 2”和“应用 3”，并且“应用 3”和“应用 4”定向于设备或用户，则注册状态页将仅跟踪“应用 3”。  仍将安装“应用 4”，但注册状态页不会等待它完成。

最多可指定 100 个应用。

## <a name="enrollment-status-page-tracking-information"></a>注册状态页跟踪信息

注册状态页跟踪以下三个阶段的信息：设备准备、设备设置和帐户设置。

### <a name="device-preparation"></a>设备准备

对于设备准备，注册状态页跟踪以下内容：

- 受信任的平台模块 (TPM) 密钥证明（适用时）
- Azure Active Directory 联接过程
- Intune (MDM) 注册
- 安装 Intune 管理扩展（用于安装 Win32 应用）

### <a name="device-setup"></a>设备设置

注册状态页跟踪以下设备设置项目：

- 安全策略
  - 适用于所有注册的一个配置服务提供程序 (CSP)。
  - 此处不跟踪 Intune 配置的实际 CSP。
- 应用程序
  - 每台计算机业务线 (LoB) MSI 应用。
  - LoB 应用商店应用（安装上下文为设备）。
  - 离线应用商店和 LoB 应用商店应用（安装上下文为设备）。
  - Win32 应用程序（仅 Windows 10 版本 1903 及更高版本） 
- 连接性配置文件
  - 为“所有设备”或注册设备是成员的设备组分配 VPN 或 Wi-Fi 配置文件，但仅适用于 Autopilot 设备
- 为“所有设备”或注册设备是成员的设备组分配证书配置文件，但仅适用于 Autopilot 设备

### <a name="account-setup"></a>帐户设置

对于帐户设置，注册状态页将跟踪以下各项（如果已将它们分配给当前登录的用户）：

- 安全策略
  - 适用于所有注册的一个 CSP。
  - 此处不跟踪 Intune 配置的实际 CSP。
- 应用程序
  - 为所有设备、所有用户或注册设备的用户所属的用户组分配的每个用户 LoB MSI 应用。
  - 为所有用户或注册设备的用户所属的用户组分配的每台计算机 LoB MSI 应用。
  - 分配到以下任一对象的 LoB 商店应用、在线商店应用和离线商店应用：
    - 所有设备
    - 所有用户
    - 用户组，其中注册设备的用户是安装上下文设置为 User 的成员。
  - Win32 应用程序（仅 Windows 10 版本 1903 及更高版本） 
- 连接性配置文件
  - 为所有用户或注册设备的用户所属的用户组分配的 VPN 或 Wi-Fi 配置文件。
- 证书
  - 为所有用户或注册设备的用户所属的用户组分配的证书配置文件。

### <a name="troubleshooting"></a>疑难解答

以下是与“注册状态页”相关的疑难解答常见问题。

- 为什么不使用注册状态页安装和跟踪我的应用程序？
  - 为了保证使用注册状态页安装和跟踪应用程序，请确保：
      - 使用“所需”分配，将应用分配到包含设备（对于面向设备的应用）或用户（对于面向用户的应用）的 Azure AD 组。  （在 ESP 的设备阶段，跟踪面向设备的应用，而在 ESP 的用户阶段跟踪面向用户的应用。）
      - 你可以指定“在安装完所有应用和配置文件之前，应避免使用设备”，也可以将应用加入“在完整完这些所需应用之前，应避免使用设备”列表中 。
      - 这些应用安装在设备上下文中，无用户上下文适用性规则。

- 为什么注册状态页显示非 Autopilot 部署，例如当用户首次从 Configuration Manager 共同管理注册设备登录时？  
  - 注册状态页会列出所有注册方法的安装状态，包括
      - Autopilot
      - Configuration Manager 共同管理
      - 新用户首次登录到已应用注册状态页策略的设备时
      - 当“仅向通过全新安装体验(OOBE)预配的设备显示页面”设置启用并且设置了策略时，只有第一个登录设备的用户才会收到注册状态页

- 在设备上配置注册状态页时，如何禁用它？
  - 注册时，将在设备上设置注册状态页策略。 必须先禁用用户和设备注册状态页部分，才可禁用注册状态页。 可使用以下配置创建自定义 OMA-URI 设置，来禁用这些部分。

      禁用用户注册状态页：

      ```
      Name:  Disable User ESP (choose a name you desire)
      Description:  (enter a description)
      OMA-URI:  ./Vendor/MSFT/DMClient/Provider/MS DM Server/FirstSyncStatus/SkipUserStatusPage
      Data type:  Boolean
      Value:  True 
      ```
      禁用设备注册状态页：

      ```
      Name:  Disable Device ESP (choose a name you desire)
      Description:  (enter a description)
      OMA-URI:  ./Vendor/MSFT/DMClient/Provider/MS DM Server/FirstSyncStatus/SkipDeviceStatusPage
      Data type:  Boolean
      Value:  True 
      ```
- 如何收集日志文件？
  - 有两种收集注册状态页日志文件的方法：
      - 在 ESP 策略中允许用户收集日志。 注册状态页发生超时时，最终用户可以选择“收集日志”的选项。 插入 U 盘，即可将日志文件复制到 U 盘中
      - 输入 Shift-F10 按键顺序打开命令提示符，然后输入以下命令行，生成日志文件： 

      ```
      mdmdiagnosticstool.exe -area Autopilot -cab <pathToOutputCabFile>.cab 
      ```

### <a name="known-issues"></a>已知问题

以下是与“注册状态页”相关的已知问题。

- 禁用 ESP 配置文件无法从设备删除 ESP 策略，用户首次登录到设备时仍然获得 ESP。 禁用 ESP 配置文件后未删除策略。 必须部署 OMA-URI 才能禁用 ESP。 有关如何使用 OMA-URI 禁用 ESP 的说明，请参阅上文。 
- 设备设置期间重启将强制用户输入凭据才能过渡到帐户设置阶段。 重启时不会保留用户凭据。 用户输入凭据后，注册状态页可继续使用。 
- 在 1903 之前的 Windows 10 版本上，执行添加工作和学校帐户注册时，注册状态页经常超时。 注册状态页将等待 Azure AD 注册完成。 已在 Windows 10 版本 1903 及更高版本中修复此问题。  
- 使用 ESP 执行混合 Azure AD Autopilot 部署所需的时间超出 ESP 配置文件定义的超时持续时间。 在混合 Azure AD Autopilot 部署中，ESP 所需的时间比 ESP 配置文件设置的值超出 40 分钟。 此延迟为本地 AD 连接器创建 Azure AD 的新设备记录提供了时间。 
- 在 Autopilot 用户驱动模式下，Windows 登录页未预填充用户名。 如果在 ESP 的设备设置阶段出现重启：
  - 不会保留用户凭据
  - 用户必须先重新输入凭据，然后才可由设备设置阶段继续转到帐户设置阶段
- ESP 长时间停滞，或始终未完成“正在识别”阶段。 在识别阶段期间，Intune 将计算 ESP 策略。 若当前用户未分配 Intune 许可证，设备可能始终无法完成计算 ESP 策略。  
- 配置 Microsoft Defender 应用程序控制会导致在 Autopilot 期间提示重启。 配置 Microsoft Defender 应用程序 (AppLocker CSP) 需要重启。 配置此策略后，可能会导致设备在 Autopilot 期间重启。 目前无法取消或推迟此重启。
- 启用 DeviceLock 策略 (https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock) 做为 ESP 配置文件一部分时，OOBE 或用户桌面自动登录可能会出于两个原因而意外失败。
  - 若设备在退出 ESP 设备设置阶段前未重启，可能会提示用户输入 Azure AD 凭据。 此提示将出现，而不会出现自动登录成功提示（成功时用户将看到 Windows 首次登录动画）。
  - 若设备在用户输入 Azure AD 凭据后和退出 ESP 设备设置阶段前重启，自动登录将失败。 因为 ESP 设备设置阶段始终未完成，因此会出现此故障。 解决方法为重置设置。

## <a name="next-steps"></a>后续步骤

设置 Windows 注册页后，了解如何管理 Windows 设备。 有关详细信息，请参阅[什么是 Microsoft Intune 设备管理？](../remote-actions/device-management.md)
