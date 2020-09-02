---
title: 在 Microsoft Intune 中的 HoloLens 2 设备上使用 Windows Defender 应用程序控制 - Azure | Microsoft Docs
description: 配置 Windows Defender 应用程序控制 (WDAC) CSP，以允许或阻止应用在 Microsoft Intune 中的 HoloLens 2 设备上打开。 使用 PowerShell 和自定义配置文件。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f4a1929749c5921714078ec54ac687f4cefe1474
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915868"
---
# <a name="use-wdac-and-windows-powershell-to-allow-or-blocks-apps-on-hololens-2-devices-with-microsoft-intune"></a>使用 WDAC 和 Windows PowerShell 允许或阻止 Microsoft Intune 的 HoloLens 2 设备上的应用

Microsoft HoloLens 2 设备支持 [Windows Defender 应用程序控制 (WDAC) CSP](/windows/client-management/mdm/applicationcontrol-csp)，它将替换 [AppLocker CSP](/windows/client-management/mdm/applocker-csp)。

通过 Windows PowerShell 和 Microsoft Intune，可以使用 WDAC CSP 来允许或阻止特定应用在 Microsoft HoloLens 2 设备上打开。 例如，你可能想要允许或阻止 Cortana 应用在组织中的 HoloLens 2 设备上打开。

此功能适用于：

- 运行了 Windows Holographic for Business 的 HoloLens 2 设备

WDAC CSP 基于 [Windows Defender 应用程序控制 (WDAC) 功能](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control)。 还可以[使用多个 WDAC 策略](/windows/security/threat-protection/windows-defender-application-control/deploy-multiple-windows-defender-application-control-policies)。

本文介绍如何：

1. 使用 Windows PowerShell 创建 WDAC 策略。
2. 使用 Windows PowerShell 将 WDAC 策略规则转换为 XML，更新 XML，然后将 XML 转换为二进制文件。
3. 在 Microsoft Intune 中，创建[自定义设备配置文件](custom-settings-windows-holographic.md)，添加此 WDAC 策略二进制文件，然后将该策略应用于 HoloLens 2 设备。

在 Intune 中，必须创建自定义配置文件才能使用 Windows Defender 应用程序控制 (WDAC) CSP。 

使用本文中的步骤作为模板，以允许或拒绝特定应用在 HoloLens 2 设备上打开。

## <a name="prerequisites"></a>必备条件

- 熟悉 Windows PowerShell。
- 使用以下身份登录到 Intune：

  - 策略和配置文件管理员或 Intune 角色管理员(Intune 角色) 

    或者

  - 全局管理员或 Intune 服务管理员(Azure AD 角色) 

  [Intune 的基于角色的访问控制 (RBAC)](../fundamentals/role-based-access-control.md)提供了详细信息。

- 使用 HoloLens 2 设备创建用户组或设备组。 有关详细信息，请参阅[用户组与设备组](device-profile-assign.md#user-groups-vs-device-groups)。

## <a name="example"></a>示例

此示例使用 Windows PowerShell 创建 Windows Defender 应用程序控制 (WDAC) 策略。 该策略可阻止特定应用打开。 然后，使用 Intune 将策略部署到 HoloLens 2 设备。

1. 在台式计算机上，打开 Windows PowerShell 应用。
2. 在台式计算机上获取有关已安装应用程序包的信息：

    ```powershell
    $package1 = Get-AppxPackage -name *<applicationname>*
    ```

    例如，输入：

    ```powershell
    $package1 = Get-AppxPackage -name *cortana*
    ```

    接下来，确认包具有应用程序属性：

    ```powershell
    $package1
    ```

    你将看到类似以下应用详细信息的属性：

    ```powershell
    Name              : Microsoft.Windows.Cortana
    Publisher         : CN=Microsoft Windows, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
    Architecture      : Neutral
    ResourceId        : neutral
    Version           : 1.13.0.18362
    PackageFullName   : Microsoft.Windows.Cortana_1.13.0.18362_neutral_neutral_cw5n1h2txyewy
    InstallLocation   : C:\Windows\SystemApps\Microsoft.Windows.Cortana_cw5n1h2txyewy
    IsFramework       : False
    PackageFamilyName : Microsoft.Windows.Cortana_cw5n1h2txyewy
    PublisherId       : cw5n1h2txyewy
    IsResourcePackage : False
    IsBundle          : False
    IsDevelopmentMode : False
    NonRemovable      : True
    IsPartiallyStaged : False
    SignatureKind     : System
    Status            : Ok
    ```

3. 创建一个 WDAC 策略，并将应用包添加到 DENY 规则：

    ```powershell
    $rule = New-CIPolicyRule -Package $package1 -Deny
    ```

4. 对于任何其他想要 DENY 的应用程序，请重复步骤 2 和 3：

    ```powershell
    $rule += New-CIPolicyRule -Package $package<2..n> -Deny
    ```

    例如，输入：

    ```powershell
    $package2 = Get-AppxPackage -name *windowsstore*
    $rule += New-CIPolicyRule -Package $package<2..n>  -Deny
    ```

5. 将 WDAC 策略转换为 newPolicy.xml：

    ```powershell
    New-CIPolicy -rules $rule -f .\newPolicy.xml -UserPEs
    ```

    若要面向应用的所有版本，请在 newPolicy.xml 中确保 `PackageVersion="65535.65535.65535.65535"` 位于 Deny 节点中：

    ```xml
    <Deny ID="ID_DENY_D_1" FriendlyName="Microsoft.WindowsStore_8wekyb3d8bbwe FileRule" PackageFamilyName="Microsoft.WindowsStore_8wekyb3d8bbwe" PackageVersion="65535.65535.65535.65535" />
    ```

    对于 `PackageFamilyNameRules`，可以使用以下版本：

    - **允许**：输入 `PackageVersion, 0.0.0.0`，这意味着“允许此版本及更高版本”。
    - **拒绝**：输入 `PackageVersion, 65535.65535.65535.65535`，这意味着“拒绝此版本及更低版本”。

6. 将 newPolicy.xml 与台式计算机上的默认策略合并。 此步骤会创建 mergedPolicy.xml。 例如，允许运行 Windows、WHQL 签名的驱动程序和存储签名的应用：

    ```powershell
    Merge-CIPolicy -PolicyPaths .\newPolicy.xml,C:\Windows\Schemas\codeintegrity\examplepolicies\DefaultWindows_Audit.xml -o mergedPolicy.xml
    ```

7. 在 mergedPolicy.xml 中禁用“审核模式”规则 。 合并时，自动启用审核模式：

    ```powershell
    Set-RuleOption -o 3 -Delete .\mergedPolicy.xml
    ```

8. 在 mergedPolicy.xml 中启用“重新启动时使 EA 无效”规则 ：

    ```powershell
    Set-RuleOption -o 15 .\mergedPolicy.xml
    ```

    有关这些规则的详细信息，请参阅[了解 WDAC 策略规则和文件规则](/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create)。

9. 将 mergedPolicy.xml 转换为二进制格式。 此步骤会创建 compiledPolicy.bin。 将此 compiledPolicy.bin 二进制文件添加到 Intune。

    ```powershell
    ConvertFrom-CIPolicy .\mergedPolicy.xml .\compiledPolicy.bin
    ```

10. 在 Intune 中，创建自定义设备配置文件：

    1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中创建 Windows 10 自定义设备配置文件。

        有关具体步骤，请参阅[使用 Intune 中的 OMA-URI 创建自定义配置文件](custom-settings-configure.md)。

    2. 创建配置文件时，请输入以下设置：

      - **OMA-URI**：输入 `./Vendor/MSFT/ApplicationControl/Policies/<PolicyGUID>`。 将 `<PolicyGUID>` 替换为在步骤 6 中创建的 mergedPolicy.xml 文件中的 PolicyTypeID 节点。

        使用我们的示例，输入 `./Vendor/MSFT/ApplicationControl/Policies/A244370E-44C9-4C06-B551-F6016E563076`。

        策略 GUID 必须与 mergedPolicy.xml 文件中的 PolicyTypeID 节点匹配（在步骤 6 中创建） 。

      - **数据类型**：设置为 Base64 文件。 它自动将文件从 bin 转换为 base64。
      - **证书文件**：上传 compiledPolicy.bin 二进制文件（在步骤 9 中创建）。

      设置如下所示：

      :::image type="content" source="./media/custom-profile-hololens/custom-applicationcontrol-omauri.png" alt-text="添加自定义 OMA-URI 以便在 Microsoft Intune 中配置 ApplicationControl CSP。":::

11. [分配](device-profile-assign.md)配置文件给 HoloLens 2 组时，请检查配置文件状态。 成功应用配置文件后，请重新启动 HoloLens 2 设备。

## <a name="next-steps"></a>后续步骤

[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。

[详细了解 Intune 中的自定义配置文件](custom-settings-configure.md)。