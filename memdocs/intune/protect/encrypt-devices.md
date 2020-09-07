---
title: 在 Intune 中通过 BitLocker 加密 Windows 10 设备
titleSuffix: Microsoft Intune
description: 使用 BitLocker 内置加密方法加密设备，并在 Intune 门户中管理这些加密设备的恢复密钥。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/28/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: 8843ab5c8bf3d0e6970398c1ad81a8a2b3b8f9cb
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193957"
---
# <a name="manage-bitlocker-policy-for-windows-10-in-intune"></a>在 Intune 中管理适用于 Windows 10 的 BitLocker 策略

使用 Intune 在运行 Windows 10 的设备上配置 BitLocker 磁盘加密。

运行 Windows 10 或更高版本的设备可以使用 BitLocker。 某些 BitLocker 设置要求设备具有受支持的 TPM。

使用以下策略类型之一在受管理设备上配置 BitLocker：

- [适用于 Windows 10 BitLocker 的终结点安全磁盘加密策略](#create-an-endpoint-security-policy-for-bitlocker)。 终结点安全中的 BitLocker 配置文件是专用于配置 BitLocker 的一组集中设置。

  查看[磁盘加密策略中的 BitLocker 配置文件](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker)中可用的 BitLocker 设置。

- [用于 Windows 10 BitLocker 终结点保护的设备配置文件](#create-an-endpoint-security-policy-for-bitlocker)。 BitLocker 设置是 Windows 10 终结点保护的可用设置类别之一。

  查看[设备配置策略的终结点保护配置文件](../protect/endpoint-protection-windows-10.md#windows-settings)中可用的 BitLocker 设置。

> [!TIP]
> Intune 提供内置的[加密报告](encryption-monitor.md)，其中提供了有关所有受管理设备中的设备加密状态的详细信息。 在 Intune 使用 BitLocker 加密 Windows 10 设备之后，你可在查看 Intune 加密报告时查看和检索 BitLocker 恢复密钥。
>
> 还可以从设备访问 BitLocker 的重要信息，如 Azure Active Directory (Azure AD) 中所示。
[加密报表](encryption-monitor.md)中提供了有关所有受管理设备中设备加密状态的详细信息。

## <a name="permissions-to-manage-bitlocker"></a>用于管理 BitLocker 的权限

若要在 Intune 中管理 BitLocker，你的帐户必须具有适用的 Intune [基于角色的访问控制](../fundamentals/role-based-access-control.md) (RBAC) 权限。

下面是 BitLocker 权限（“远程任务”类别的一部分）和授予权限的内置 RBAC 角色：

- 轮换 BitLocker 密钥
  - 支持人员操作员

## <a name="create-and-deploy-policy"></a>创建和部署策略

使用以下过程之一创建所需的策略类型。

### <a name="create-an-endpoint-security-policy-for-bitlocker"></a>为 BitLocker 创建终结点安全策略

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“终结点安全” > “磁盘加密” > “创建策略”  。

3. 设置下列选项:
   1. **平台**：Windows 10 或更高版本
   2. **配置文件**：BitLocker

   ![选择 BitLocker 配置文件](./media/encrypt-devices/select-windows-bitlocker-es.png)

4. 在“配置设置”页上，根据业务需求配置 BitLocker 设置。  

   如果要以无提示方式启用 BitLocker，请参阅本文中的[以无提示的方式在设备上启用 BitLocker](#silently-enable-bitlocker-on-devices)，了解其他先决条件以及必须使用的特定设置配置。

   选择“下一步”。

5. 在“作用域标记”页上，选择“选择作用域标记”打开“选择标记”窗格，将作用域标记分配给配置文件 。

   选择“下一步”继续操作。

6. 在“分配”页上，选择将接收此配置文件的组。 有关分配配置文件的详细信息，请参阅“分配用户和设备配置文件”。

   选择“下一步”。

7. 完成后，在“查看 + 创建”页上，选择“创建” 。 为创建的配置文件选择策略类型时，新配置文件将显示在列表中。

### <a name="create-a-device-configuration-profile-for-bitlocker"></a>为 BitLocker 创建设备配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“设备” > “配置文件” > “创建配置文件”。

3. 设置下列选项:
   1. **平台**：Windows 10 及更高版本
   2. **配置文件类型**：Endpoint Protection

   ![选择配置文件](./media/encrypt-devices/select-windows-bitlocker-dc.png)

4. 选择“设置” > “Windows Encryption” 。

   ![BitLocker 设置](./media/encrypt-devices/bitlocker-settings.png)

5. 根据业务需求配置 BitLocker 设置。

   如果要以无提示方式启用 BitLocker，请参阅本文中的[以无提示的方式在设备上启用 BitLocker](#silently-enable-bitlocker-on-devices)，了解其他先决条件以及必须使用的特定设置配置。

6. 选择“确定”。

7. 完成其他设置配置，然后保存配置文件。

## <a name="manage-bitlocker"></a>管理 BitLocker

若要查看有关接收 BitLocker 策略的设备的信息，请参阅[监视磁盘加密](../protect/encryption-monitor.md)。 查看加密报告时，还可以查看和检索 BitLocker 恢复密钥。

### <a name="silently-enable-bitlocker-on-devices"></a>以无提示的方式在设备上启用 BitLocker

你可以配置一个 BitLocker 策略，该策略自动且以无提示的方式在设备上启用 BitLocker。 这意味着，即使用户不是设备上的本地管理员，BitLocker 也能成功启用而无需向最终用户呈现任何 UI。

**设备先决条件**：

设备必须满足以下条件才能以无提示的方式启用 BitLocker：

- 如果最终用户以管理员身份登录到设备，则设备必须运行 Windows 10 版本 1803 或更高版本。
- 如果最终用户以标准用户身份登录到设备，则设备必须运行 Windows 10 版本 1809 或更高版本。
- 设备必须加入了 Azure AD  

**BitLocker 策略配置**：

*BitLocker 基本设置*的以下两个设置必须在 BitLocker 策略中进行配置：

- **其他磁盘加密的警告** = 阻止。
- **允许标准用户在 Azure AD 加入期间启用加密** = 允许

BitLocker 策略不得要求使用启动 PIN 或启动密钥。 需要 TPM 启动 PIN 或启动密钥时，BitLocker 无法以无提示的方式启用，并且需要与最终用户交互。  通过同一策略中的以下三个 *BitLocker OS 驱动器设置*可以满足此要求：

- 兼容的 TPM 启动 PIN 不得设置为需要使用 TPM 的启动 PIN
- 兼容的 TPM 启动密钥不得设置为需要使用 TPM 的启动密钥
- 兼容的 TPM 启动密钥和 PIN 不得设置为需要使用 TPM 的启动密钥和 PIN

### <a name="view-details-for-recovery-keys"></a>查看有关恢复密钥的详细信息

Intune 提供了对 BitLocker 的 Azure AD 边栏选项卡的访问权限，以便你能够在 Intune 门户中查看 Windows 10 设备的 BitLocker 密钥 ID 和恢复密钥。 为了能够访问，设备必须将其密钥托管到 Azure AD。

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“设备” > “所有设备”   。

3. 选择列表中的设备，然后在“监视”下，选择“恢复密钥”。
  
   如果 Azure AD 中有密钥，将提供以下信息：
   - BitLocker 密钥 ID
   - BitLocker 恢复密钥
   - 驱动器类型

   如果 Azure AD 中没有密钥，Intune 将显示“未找到此设备的 BitLocker 密钥”。

使用 [BitLocker 配置服务提供程序](/windows/client-management/mdm/bitlocker-csp) (CSP) 获取 BitLocker 的信息。 Windows 10 1703 版本和更高版本，以及 Windows 10 专业版 1809 版本和更高版本支持 BitLocker CSP。

### <a name="rotate-bitlocker-recovery-keys"></a>BitLocker 恢复密码轮转

可以使用 Intune 设备操作远程轮转运行 Windows 10 版本 1909 或更高版本的设备的 BitLocker 恢复密码。

#### <a name="prerequisites"></a>必备条件

设备必须满足以下先决条件才支持 BitLocker 恢复密码轮转：

- 设备必须运行 Windows 10 版本 1909 或更高版本

- 已加入 Azure AD 和混合加入的设备必须通过 BitLocker 策略配置启用对密钥轮换的支持：

  - 将“客户端驱动的恢复密码轮换”配置为“在已加入 Azure AD 的设备上启用轮换”或“在已加入 Azure AD 和混合加入的设备上启用轮换” 
  - 将“将 BitLocker 恢复信息保存到 Azure Active Directory”配置为“启用”
  - 将“启用 BitLocker 之前在 Azure Active Directory 中存储恢复信息”配置为“必需”

#### <a name="to-rotate-the-bitlocker-recovery-key"></a>BitLocker 恢复密码轮转

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“设备” > “所有设备” 。

3. 在所管理的设备列表中，选择一个设备，选择“更多”，然后选择“BitLocker 密码轮转”设备远程操作。

4. 在设备的“概述”页面上，选择“BitLocker 密钥轮换”。 如果此选项未显示，请选择省略号 (…) 以显示更多选项，然后选择“BitLocker 密钥轮换”设备远程操作。

   ![选择省略号以查看更多选项](./media/encrypt-devices/select-more.png)

## <a name="next-steps"></a>后续步骤

[管理 FileVault 策略](../protect/encrypt-devices-filevault.md)

[监视磁盘加密](../protect/encryption-monitor.md)
