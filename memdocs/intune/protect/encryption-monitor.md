---
title: Microsoft Intune 中加密设备的加密报表
titleSuffix: Microsoft Intune
description: 查看有关 iOS/iPadOS 或 Windows 设备加密状态的报表，并从 Microsoft Intune 门户中访问 FileVault 和 BitLocker 恢复密钥。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/18/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: c07fc8102504a9ca3ee5694e8cb9b1d5f8b568bc
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79352236"
---
# <a name="monitor-device-encryption-with-intune"></a>使用 Intune 监视设备加密

Microsoft Intune 加密报告是一个集中位置，可便于查看设备加密状态的详细信息，并查找设备恢复密钥的管理选项。 可用的恢复密钥选项取决于要查看的设备类型。

要查找报告，请登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。 选择“设备” > “监视器”，然后在“配置”下选择“加密报告”     。

## <a name="view-encryption-details"></a>查看加密详细信息

加密报表显示你管理的受支持设备的常见详细信息。 以下各部分提供有关 Intune 在报表中显示的信息的详细信息。

### <a name="prerequisites"></a>必备条件

加密报表支持在运行以下操作系统版本的设备上进行报告：

- macOS 10.13 或更高版本
- Windows 版本 1607 或更高版本

### <a name="report-details"></a>报表详细信息

“加密”报表窗格显示管理的设备列表，其中包含有关这些设备的高级详细信息。 可以从列表中选择设备以深入查看设备[“设备加密状态”](#device-encryption-status)窗格中的其他详细信息。

- **设备名称** - 设备的名称。
- **OS** - 设备平台（如 Windows 或 macOS）。
- **OS 版本** - 设备上安装的 Windows 或 macOS 版本。
- **TPM 版本**（仅适用于 Windows 10）  - Windows 10 设备上安装的受信任的平台模块 (TPM) 芯片版本。
- **加密就绪情况** - 评估设备是否准备好支持适用的加密技术（如 BitLocker 或 FileVault 加密）。 设备标识为：
  - **就绪**：可以使用 MDM 策略对设备进行加密，前提是设备满足以下要求：

    **对于 macOS 设备**：
    - MacOS 版本 10.13 或更高版本

    **对于 Windows 10 设备**：
    - *商业版*、*企业版*、*教育版* 1703 或更高版本，或者 *Pro* 版本 1809 或更高版本
    - 设备必须安装有 TPM 芯片

    有关详细信息，请参阅 Windows 文档中的 [BitLocker 配置服务提供商 (CSP)](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp)。

  - **未就绪**：设备不具完备的加密功能，但仍支持加密。 例如，用户可以手动加密 Windows 设备，也可以通过可设置为无需 TPM 即可加密的组策略加密设备。
  - **不适用**：用于对此设备进行分类的信息不足。

- **加密状态** – OS 驱动器是否加密。

- **用户主体名称** - 设备的主要用户。

### <a name="device-encryption-status"></a>设备加密状态

从加密报表选择设备时，Intune 会显示“设备加密状态”窗格  。 此窗格提供以下详细信息：

- **设备名称** – 所查看设备的名称。

- **加密就绪情况** - 通过 MDM 策略评估设备是否准备好支持加密。

  例如：如果 Windows 10 设备的就绪情况为“未就绪”，它可能仍支持加密  。 要指定“就绪”，Windows 10 设备必须安装有 TPM 芯片  。 无需 TPM 芯片，即可支持加密。 （有关详细信息，请参阅上一部分中的“加密就绪情况”  。）

- **加密状态** - OS 驱动器是否加密。 Intune 最多可能需要 24 小时才能开始报告设备加密状态或对该状态所做的更改。 此时间包括 OS 加密的时间，以及设备报告回 Intune 的时间。

  为了在设备正常签入前加快 FileVault 加密状态的报告速度，请让用户在加密完成后同步自己的设备。

- **配置文件** - 适用于此设备且配置了以下值的“设备配置”配置文件列表  ：

  - macOS：
    - 配置文件类型 = 终结点保护 
    - “设置”>“FileVault”>“FileVault”=“启用” 

  - Windows 10：
    - 配置文件类型 = 终结点保护 
    - “设置”>“Windows 加密”>“加密设备”=“需要” 

  如果配置文件状态摘要表明存在问题，则可使用配置文件列表来确定要查看的所有策略  。

- **配置文件状态摘要** – 适用于此设备的配置文件摘要。 摘要表示适用配置文件中的最不利条件。 例如，如果几个适用的配置文件中只有一个导致错误，则配置文件状态摘要将显示“错误”   。

  若要查看状态的更多详细信息，请依次转到“Intune”   > “设备配置”   > “配置文件”  ，再选择配置文件。 （可选）依次选择“设备状态”  和设备。

- **状态详细信息** – 关于设备加密状态的高级详细信息。

  > [!IMPORTANT]
  > 对于 Windows 10 设备，Intune 仅显示运行 Windows 10 2019 年 4 月更新或更高版本的设备的状态详细信息   。

  此字段显示可检测到的每个适用错误的信息。 使用此信息可了解设备加密未准备就绪的原因。

  Intune 可能报告的状态详细信息示例如下：

  **macOS**：
  - 尚未检索和存储恢复密钥。 最有可能是因为设备尚未解锁或签入。

    *请考虑以下事项：此结果不一定表示错误条件，而是表示一种临时状态，这可能是由于设备上的计时所致，因为必须先在设备上设置恢复密钥托管，再将加密请求发送到设备。此状态也可能表示设备一直处于锁定状态，或最近未使用 Intune 签入。最后，由于 FileVault 加密只有在设备接通电源（充电）之后才会启动，因此用户可以接收尚未加密的设备的恢复密钥*。

  - 用户正在延迟加密，或当前正在加密。

    *请考虑以下事项：要么用户在收到加密请求后尚未注销（这在 FileVault 可以加密设备之前是必需的），要么用户已手动解密设备。Intune 无法阻止用户解密其设备。*

  - 设备已加密。 设备用户必须解密设备才能继续操作。

    *请考虑以下事项：Intune 无法在已加密的设备上设置 FileVault。相反，用户必须手动解密其设备，然后才能通过设备配置策略和 Intune 对其进行管理*。

  - FileVault 需要用户在 MacOS Catalina 及更高版本中批准其管理配置文件。

    *请考虑以下事项：自 MacOS 版本 10.15 (Catalina) 起，用户批准的注册设置可能导致要求用户手动批准 FileVault 加密。有关详细信息，请参阅 Intune 文档中的[用户批准注册](../enrollment/macos-enroll.md)* 。

  - 未知。

    *请考虑以下事项：导致未知状态的一个可能原因是，设备已锁定，Intune 无法启动托管或加密过程。设备解锁后，进程可以继续*。

  **Windows 10**：
  - BitLocker 策略需要用户同意启动 BitLocker 驱动器加密向导以开始加密 OS 卷，但用户未同意。

  - OS 卷的加密方法与 BitLocker 策略不匹配。

  - BitLocker 策略需要 TPM 保护程序保护 OS 卷，但未使用 TPM。

  - BitLocker 策略需要只有 TPM 的保护程序保护 OS 卷，但未使用 TPM 保护。

  - BitLocker 策略需要对 OS 卷使用 TPM+PIN 保护，但未使用 TPM+PIN 保护程序。

  - BitLocker 策略需要对 OS 卷使用 TPM+启动密钥保护，但未使用 TPM+启动密钥保护程序。

  - BitLocker 策略需要对 OS 卷使用 TPM+PIN+启动密钥保护，但未使用 TPM+PIN+启动密钥保护程序。

  - OS 卷未受保护。

  - 恢复密钥备份失败。

  - 固定驱动器未受保护。

  - 固定驱动器的加密方法与 BitLocker 策略不匹配。

  - 为了加密驱动器，BitLocker 策略需要用户以管理员身份登录，或者，如果设备连接到 Azure AD，AllowStandardUserEncryption 策略必须设置为 1。

  - Windows 恢复环境 (WinRE) 未配置。

  - TPM 无法用于 BitLocker 要么是因为它不存在，要么是因为它在注册表中不可用，要么是因为 OS 位于可移动驱动器中。

  - TPM 未准备就绪，BitLocker 无法使用。

  - 恢复密钥备份所需的网络不可用。

## <a name="export-report-details"></a>导出报表详细信息

查看“加密”报表窗格时，可以选择“导出”以创建报表详细信息的 .csv 文件下载   。 此报表涵盖“加密报表”窗格中的高级详细信息以及你管理的所有设备的“设备加密状态”详细信息   。

![导出详细信息](./media/encryption-monitor/export.png)

此报表可用于识别设备组的问题。 例如，可使用报告来标识 macOS 设备列表，其中所有设备全都报告“用户已启用 FileVault”  （表示设备必须经过手动解密，然后 Intune 才能管理设备的 FileVault 设置）。

## <a name="filevault-recovery-keys"></a>FileVault 恢复密钥

Intune 首次使用 FileVault 加密 macOS 设备时，会创建个人恢复密钥。 加密时，设备一次性向最终用户显示个人密钥。

对于受管理设备，Intune 可以托管个人恢复密钥的副本。 通过对密钥进行托管，Intune 管理员可以轮换密钥以帮助保护设备，并且用户可以恢复丢失或轮换的个人恢复密钥。

Intune 支持多种选项来轮换和恢复个人恢复密钥。 轮换密钥的一个原因是，当前个人密钥丢失或被认为存在风险。

> [!IMPORTANT]
> Intune 无法管理由用户加密而非由 Intune 加密的设备。 即 Intune 无法托管这些设备的个人恢复密钥，也无法管理轮换的恢复密钥。 用户必须解密其设备，然后让 Intune 对设备进行加密，Intune 才可以管理设备的 FileVault 和恢复密钥。

### <a name="rotate-recovery-keys"></a>轮换恢复密钥

- **自动执行轮换**：管理员可以配置 FileVault 设置个人恢复密钥轮换以定期自动生成新的恢复密钥。 为设备生成新密钥时，系统不会向用户显示密钥。 相反，用户必须从管理员或使用公司门户应用获取密钥。

- **手动轮换**：作为管理员，你可以查看自己使用 Intune 管理且使用 FileVault 加密的设备的相关信息。 然后，可以选择手动轮换企业设备的恢复密钥。 无法轮换个人设备的恢复密钥。

  轮换恢复密钥：

  1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
  
  2. 选择“设备”> “所有设备”     。
  
  3. 从设备列表中，选择已加密且要为其轮换密钥的设备。 然后在“监视”下，选择“ **恢复密钥**”。
  
  4. 在“恢复密钥”窗格中，选择“轮换 FileVault 恢复密钥”  。

     设备下次使用 Intune 签入时，系统将轮换个人密钥。 需要时，最终用户可以通过公司门户获取新密钥。

### <a name="recover-recovery-keys"></a>恢复恢复密钥

- **管理员**：管理员无法查看使用 FileVault 加密的设备的个人恢复密钥。

- **最终用户**：最终用户可以从任何设备使用公司门户网站查看其任何受管理设备的当前个人恢复密钥。 无法从公司门户应用中查看恢复密钥。

  查看恢复密钥：
  
  1. 从任意设备登录 Intune 公司门户网站  。

  2. 在门户中，转到“设备”，然后选择使用 FileVault 加密的 macOS 设备  。

  3. 选择“获取恢复密钥”  。 系统会显示当前恢复密钥。

## <a name="bitlocker-recovery-keys"></a>BitLocker 恢复密钥

Intune 提供了对 BitLocker 的 Azure AD 边栏选项卡的访问权限，以便你能够在 Intune 门户中查看 Windows 10 设备的 BitLocker 密钥 ID 和恢复密钥。 为了能够访问，设备必须将其密钥托管到 Azure AD。

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“设备” > “所有设备”   。

3. 选择列表中的设备，然后在“监视”下，选择“恢复密钥”   。
  
   如果 Azure AD 中有密钥，将提供以下信息：
   - BitLocker 密钥 ID
   - BitLocker 恢复密钥
   - 驱动器类型

   如果 Azure AD 中没有密钥，Intune 将显示“未找到此设备的 BitLocker 密钥”  。

使用 [BitLocker 配置服务提供程序](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp) (CSP) 获取 BitLocker 的信息。 Windows 10 1703 版本和更高版本，以及 Windows 10 专业版 1809 版本和更高版本支持 BitLocker CSP。

## <a name="next-steps"></a>后续步骤

创建[设备符合性](compliance-policy-create-windows.md)策略。
