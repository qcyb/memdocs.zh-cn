---
title: 通过 Intune 使用 FileVault 磁盘加密对 macOS 设备进行加密
titleSuffix: Microsoft Intune
description: 使用内置加密方法 FileVault 对 macOS 设备进行加密，并在 Intune 门户中管理这些加密设备的恢复密钥。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
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
ms.openlocfilehash: cdfec1d82d68e97544172c56cecc416846b4a0f6
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2020
ms.locfileid: "86460478"
---
# <a name="use-filevault-disk-encryption-for--macos-with-intune"></a>通过 Intune 对 macOS 使用 FileVault 磁盘加密

Intune 支持 macOS FileVault 磁盘加密。 FileVault 是 macOS 附带的整盘加密程序。 可以使用 Intune 在运行 macOS 10.13 或更高版本的设备上配置 FileVault。

使用以下策略类型之一配置托管设备上的 FileVault：

- [macOS FileVault 的终结点安全策略](#create-endpoint-security-policy-for-filevault)。 终结点安全中的 FileVault 配置文件是专用于配置 FileVault 的一组集中设置。

  查看[用于磁盘加密策略的配置文件中可用的 FileVault 设置](../protect/endpoint-security-disk-encryption-profile-settings.md)。

- [用于 macOS FileVault 终结点保护的设备配置文件](#create-endpoint-security-policy-for-filevault)。 FileVault 设置是 macOS Endpoint Protection 的可用设置类别之一。 有关使用设备配置文件的详细信息，请参阅[在 Inunte 中创建设备配置文件](../configuration/device-profile-create.md)。

  查看[用于设备配置策略的终结点保护配置文件中可用的 FileVault 设置](../protect/endpoint-protection-macos.md#filevault)。

若要管理 Windows 10 的 BitLocker，请参阅[管理 BitLocker 策略](../protect/encrypt-devices.md)。

> [!TIP]
> Intune 提供内置的[加密报告](encryption-monitor.md)，其中提供了有关所有受管理设备中的设备加密状态的详细信息。

创建使用 FileVault 加密设备的策略后，策略将分两个阶段应用于设备。 首先，准备好设备，以启用 Intune 检索和备份恢复密钥。 此操作称为“托管”。 托管密钥后，磁盘加密便可启动。

除了使用 Intune 策略通过 FileVault 加密设备，你还可以将策略部署到托管设备，使 Intune [在用户加密设备时能够承担 FileVault 的管理](#assume-management-of-filevault-on-previously-encrypted-devices)。 此方案要求设备从 Intune 接收 FileVault 策略，然后用户将其个人恢复密钥上传到 Intune。

若要使 FileVault 在设备上运行，需要进行用户批准的设备注册。 用户必须手动批准系统首选项中的管理配置文件，才能将注册视为用户批准。

## <a name="permissions-to-manage-filevault"></a>用于管理 FileVault 的权限

若要在 Intune 中管理 FileVault，你的帐户必须具有适用的 Intune [基于角色的访问控制](../fundamentals/role-based-access-control.md) (RBAC) 权限。

下面是 FileVault 权限（“远程任务”类别的一部分）和授予权限的内置 RBAC 角色：

- **获取 FileVault 密钥**：
  - 支持人员操作员
  - 终结点安全管理器

- **轮换 FileVault 密钥**
  - 支持人员操作员

## <a name="create-device-configuration-policy-for-filevault"></a>为 FileVault 创建设备配置策略

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“设备” > “配置文件” > “创建配置文件”。

3. 在“创建配置文件”页上，设置以下选项，然后单击“创建”：
   - **平台**：macOS
   - **配置文件**：Endpoint Protection

   ![选择 FileVault 配置文件](./media/encrypt-devices-filevault/select-macos-filevault-dc.png)

4. 在“基本信息”页上，输入以下属性：

   - **名称**：输入策略的描述性名称。 为策略命名，以便稍后可以轻松地识别它们。 例如，好的策略名称可包括配置文件类型和平台。

   - **描述**：输入策略的说明。 此设置是可选的，但建议进行。

5. 在“配置设置”页上，选择“FileVault”，以展开可用设置：

   > [!div class="mx-imgBorder"]
   > ![“FileVault”设置](./media/encrypt-devices-filevault/filevault-settings.png)

6. 配置下列设置：
  
   - 对于“启用 FileVault”，选择“是”。

   - 对于“恢复密钥类型”，选择“个人密钥”。

   - 对于“个人恢复密钥的托管位置说明”，请添加有助于指导用户[如何为设备检索恢复密钥](#retrieve-a-personal-recovery-key)的消息。 使用个人恢复密钥轮换设置时，此信息对用户非常有用。通过该设置，可以定期自动为设备生成新的恢复密钥。

     例如：若要检索丢失或最近轮换的恢复密钥，请从任意设备登录 Intune 公司门户网站。 在门户中，转到“设备”并选择已启用 FileVault 的设备，然后选择“获取恢复密钥” 。 系统会显示当前恢复密钥。

   配置其余 [FileVault 设置](endpoint-protection-macos.md#filevault)来满足业务需求，然后选择“下一步”。

7. 在“作用域标记”页上，选择“选择作用域标记”打开“选择标记”窗格，将作用域标记分配给配置文件 。

   选择“下一步”继续操作。

8. 在“分配”页上，选择将接收此配置文件的组。 有关分配配置文件的详细信息，请参阅“分配用户和设备配置文件”。
选择“下一步”。

9. 完成后，在“查看 + 创建”页上，选择“创建” 。 为创建的配置文件选择策略类型时，新配置文件将显示在列表中。

## <a name="create-endpoint-security-policy-for-filevault"></a>为 FileVault 创建终结点安全策略

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“终结点安全” > “磁盘加密” > “创建策略”  。

3. 在“基本信息”页上，输入以下属性，然后选择“下一步” 。
   - **平台**：macOS
   - **配置文件**：FileVault

   ![选择 FileVault 配置文件](./media/encrypt-devices-filevault/select-macos-filevault-es.png)

4. 在“配置设置”页上：
   1. 将“启用 FileVault”设置为“是”。
   2. 对于“恢复密钥类型”，仅支持“个人恢复密钥”。
   3. 配置其他设置以满足你的要求。

   请考虑添加一条消息，以帮助指导用户[如何检索其设备的恢复密钥](#retrieve-a-personal-recovery-key)。 使用个人恢复密钥轮换设置时，此信息对用户非常有用。通过该设置，可以定期自动为设备生成新的恢复密钥。

   例如：若要检索丢失或最近轮换的恢复密钥，请从任意设备登录 Intune 公司门户网站。 在门户中，转到“设备”并选择已启用 FileVault 的设备，然后选择“获取恢复密钥”。 系统会显示当前恢复密钥。

5. 完成配置设置后，选择“下一步”。

6. 在“作用域标记”页上，选择“选择作用域标记”打开“选择标记”窗格，将作用域标记分配给配置文件 。

   选择“下一步”继续操作。

7. 在“分配”页上，选择将接收此配置文件的组。 有关分配配置文件的详细信息，请参阅“分配用户和设备配置文件”。
选择“下一步”。

8. 完成后，在“查看 + 创建”页上，选择“创建” 。 为创建的配置文件选择策略类型时，新配置文件将显示在列表中。

## <a name="manage-filevault"></a>管理 FileVault

若要查看有关接收 FileVault 策略的设备的信息，请参阅[监视磁盘加密](../protect/encryption-monitor.md)。

Intune 首次使用 FileVault 加密 macOS 设备时，会创建个人恢复密钥。 加密时，设备一次性向设备用户显示个人密钥。

对于受管理设备，Intune 可以托管个人恢复密钥的副本。 通过对密钥进行托管，Intune 管理员可以轮换密钥以帮助保护设备，并且用户可以恢复丢失或轮换的个人恢复密钥。

当 Intune 策略加密设备时，或在用户上传手动加密的设备恢复密钥后，Intune 会托管恢复密钥。

Intune 托管个人恢复密钥后：

- 管理员可以使用 Intune 加密报告管理和轮换任何托管 macOS 设备的 FileVault 恢复密钥。
- 管理员只能查看标记为“公司”的托管的 macOS 设备的个人恢复密钥。 他们无法查看个人设备的恢复密钥。
- 用户可以查看和[从受支持的位置检索其个人恢复密钥](#retrieve-a-personal-recovery-key)。 例如，从公司门户网站，用户可以选择“获取恢复密钥”作为远程设备操作。

### <a name="assume-management-of-filevault-on-previously-encrypted-devices"></a>在以前加密的设备上承担 FileVault 的管理

Intune 可以在使用 Intune 策略加密的 macOS 设备上管理 FileVault 磁盘加密。 Intune 还可以接管由设备用户（而不是通过 Intune 策略）加密的设备上的 FileVault 管理。

#### <a name="prerequisites-to-assume-management-of-filevault"></a>承担 FileVault 管理的先决条件

若要对以前加密的设备承担管理，必须满足以下条件：

1. **将 FileVault 策略部署到设备**。 以前加密的设备必须能够从 Intune 接收启用 FileVault 磁盘加密的策略。

   在这种情况下，该策略不会解密或重新加密设备。 相反，该策略使 Intune 能够对设备上已启用的 FileVault 加密进行管理。  你可以使用终结点安全磁盘加密策略或设备配置终结点保护策略，通过 FileVault 加密设备。

   请参阅[创建和部署策略](#create-device-configuration-policy-for-filevault)。

2. **用户将其个人恢复密钥上传到 Intune**。  设备收到 FileVault 策略后，指示加密设备的设备用户将其个人恢复密钥上传到 Intune。 如果密钥输入成功，Intune 将承担 FileVault 加密的管理，并为此设备和用户创建一个新的个人恢复密钥。

   > [!IMPORTANT]
   > Intune 不会警示用户必须上传其个人恢复密钥才能完成加密。 而是使用普通 IT 通信通道向以前使用 FileVault 加密 macOS 设备的用户发出警报，他们必须将其个人恢复密钥上传到 Intune。  
   >
   > 根据你的合规性策略，在 Intune 成功管理设备上的 FileVault 加密之前，可能会阻止设备访问公司资源。

#### <a name="upload-a-personal-recovery-key"></a>上传个人恢复密钥

若要使 Intune 能够管理以前加密设备上的 FileVault，设备用户必须使用公司门户网站将设备的当前个人恢复密钥上传到 Intune。  上传后，Intune 将轮换密钥以创建新的个人恢复密钥，然后由 Intune 存储该密钥，以用于将来恢复（如果需要）。

在公司门户网站中，用户找到其加密的 macOS 设备并选择“存储恢复密钥”选项。 输入个人恢复密钥后，Intune 将尝试轮换密钥以生成新密钥。 执行轮换的目的是验证输入的密钥是否准确。 如果用户需要恢复其设备，则由 Intune 存储和管理此新密钥以供将来使用。

如果密钥轮换失败，则设备未处理 FileVault 策略，或者输入的密钥对设备来说不准确。

成功轮换后，用户可以[从受支持的位置检索其新的个人恢复密钥](#retrieve-a-personal-recovery-key)。

 查看[最终用户内容以上传个人恢复密钥](../user-help/store-recovery-key.md)。

> [!IMPORTANT]
> 对于由用户而不是由 Intune 加密的设备，Intune 无法管理设备 FileVault 加密，除非该设备收到 FileVault 策略并且设备用户成功上传其个人恢复密钥。

### <a name="retrieve-a-personal-recovery-key"></a>检索个人恢复密钥

对于由 Intune 管理其 FileVault 加密的 macOS 设备，最终用户可以使用任何设备从以下位置检索其个人恢复密钥（FileVault 密钥）：

- 公司门户网站
- iOS/iPadOS 公司门户应用
- Android 公司门户应用
- Intune 应用

管理员可以查看标记为“公司”设备的加密 macOS 设备的个人恢复密钥。 他们无法查看个人设备的恢复密钥。

拥有个人恢复密钥的设备必须已注册 Intune，并且通过 Intune 使用 FileVault 加密。 使用 iOS 公司门户应用、Android 公司门户应用、Android Intune 应用或公司门户网站，用户可以看到访问其 Mac 设备所需的 FileVault 恢复密钥。

设备用户可以选择“设备” > “加密并注册的 macOS 设备” > “获取恢复密钥”。 浏览器将显示 Web 公司门户并显示恢复密钥。

### <a name="rotate-recovery-keys"></a>轮换恢复密钥

Intune 支持多种选项来轮换和恢复个人恢复密钥。 轮换密钥的一个原因是，当前个人密钥丢失或被认为存在风险。

- **自动执行轮换**：管理员可以配置 FileVault 设置个人恢复密钥轮换以定期自动生成新的恢复密钥。 为设备生成新密钥时，不会向用户显示密钥。 相反，用户必须从管理员或使用公司门户应用获取密钥。

- **手动轮换**：管理员可以查看自己使用 Intune 管理且使用 FileVault 加密的设备的相关信息。 然后，可以选择手动轮换企业设备的恢复密钥。 不能轮换个人设备的恢复密钥。

  轮换恢复密钥：

  1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

  2. 选择“设备”> “所有设备” 。

  3. 从设备列表中，选择已加密且要为其轮换密钥的设备。 然后在“监视”下，选择“ **恢复密钥**”。
  
  4. 在“恢复密钥”窗格中，选择“轮换 FileVault 恢复密钥”。

     设备下次使用 Intune 签入时，系统将轮换个人密钥。 需要时，用户可以通过公司门户获取新密钥。

### <a name="recover-recovery-keys"></a>恢复恢复密钥

- **管理员**：管理员无法查看使用 FileVault 加密的设备的个人恢复密钥。

- **最终用户**：最终用户可以从任何设备使用公司门户网站查看其任何受管理设备的当前个人恢复密钥。 无法从公司门户应用中查看恢复密钥。

  查看恢复密钥：
  
  1. 从任意设备登录 Intune 公司门户网站。

  2. 在门户中，转到“设备”，然后选择使用 FileVault 加密的 macOS 设备。

  3. 选择“获取恢复密钥”。 系统会显示当前恢复密钥。

## <a name="next-steps"></a>后续步骤

[管理 BitLocker 策略](../protect/encrypt-devices.md)

[监视磁盘加密](../protect/encryption-monitor.md)
