---
title: 通过 Intune 使用 FileVault 磁盘加密对 macOS 设备进行加密
titleSuffix: Microsoft Intune
description: 使用内置加密方法 FileVault 对 macOS 设备进行加密，并在 Intune 门户中管理这些加密设备的恢复密钥。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
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
ms.openlocfilehash: 99facc87d068239962ab0d40874aa081f5e19189
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989690"
---
# <a name="use-filevault-disk-encryption-for--macos-with-intune"></a>通过 Intune 对 macOS 使用 FileVault 磁盘加密

Intune 支持 macOS FileVault 磁盘加密。 FileVault 是 macOS 附带的整盘加密程序。 可以使用 Intune 在运行 macOS 10.13 或更高版本的设备上配置 FileVault。

使用以下策略类型之一配置托管设备上的 FileVault：

- [macOS FileVault 的终结点安全策略](#create-an-endpoint-security-policy-for-filevault)。 终结点安全中的 FileVault 配置文件是专用于配置 FileVault 的一组集中设置。

  查看[用于磁盘加密策略的配置文件中可用的 FileVault 设置](../protect/endpoint-security-disk-encryption-profile-settings.md)。

- [用于 macOS FileVault 终结点保护的设备配置文件](#create-an-endpoint-security-policy-for-filevault)。 FileVault 设置是 macOS Endpoint Protection 的可用设置类别之一。 有关使用设备配置文件的详细信息，请参阅[在 Inunte 中创建设备配置文件](../configuration/device-profile-create.md)。

  查看[用于设备配置策略的终结点保护配置文件中可用的 FileVault 设置](../protect/endpoint-protection-macos.md#filevault)。

若要管理 Windows 10 的 BitLocker，请参阅[管理 BitLocker 策略](../protect/encrypt-devices.md)。

> [!TIP]
> [加密报表](encryption-monitor.md)中提供了有关所有受管理设备中设备加密状态的详细信息。

创建使用 FileVault 加密设备的策略后，策略将分两个阶段应用于设备。 首先，准备好设备，以启用 Intune 检索和备份恢复密钥。 此操作称为“托管”。 托管密钥后，磁盘加密便可启动。

若要使 FileVault 在设备上运行，需要进行用户批准的设备注册。 用户必须手动批准系统首选项中的管理配置文件，才能将注册视为用户批准。

## <a name="permissions-to-manage-filevault"></a>用于管理 FileVault 的权限

若要在 Intune 中管理 FileVault，你的帐户必须具有适用的 Intune [基于角色的访问控制](../fundamentals/role-based-access-control.md) (RBAC) 权限。

下面是 FileVault 权限（“远程任务”类别的一部分）和授予权限的内置 RBAC 角色：

- **获取 FileVault 密钥**：
  - 支持人员操作员
  - 终结点安全管理器

- **轮换 FileVault 密钥**
  - 支持人员操作员

## <a name="create-and-deploy-policy"></a>创建和部署策略

### <a name="create-an-endpoint-security-policy-for-filevault"></a>为 FileVault 创建终结点安全策略

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“终结点安全” > “磁盘加密” > “创建策略”  。

3. 在“基本信息”页上，输入以下属性，然后选择“下一步” 。
   1. **平台**：macOS
   2. **配置文件**：FileVault

   ![选择 FileVault 配置文件](./media/encrypt-devices-filevault/select-macos-filevault-es.png)

4. 在“配置设置”页上：
   1. 将“启用 FileVault”设置为“是”。
   2. 对于“恢复密钥类型”，仅支持“个人恢复密钥”。
   3. 配置其他设置以满足你的要求。

   请考虑添加一条消息，以帮助指导用户检索其设备的恢复密钥。 使用个人恢复密钥轮换设置时，此信息对用户非常有用。通过该设置，可以定期自动为设备生成新的恢复密钥。

   例如：若要检索丢失或最近轮换的恢复密钥，请从任意设备登录 Intune 公司门户网站。 在门户中，转到“设备”并选择已启用 FileVault 的设备，然后选择“获取恢复密钥”。 系统会显示当前恢复密钥。

5. 完成配置设置后，选择“下一步”。

6. 在“作用域标记”页上，选择“选择作用域标记”打开“选择标记”窗格，将作用域标记分配给配置文件 。

   选择“下一步”继续操作。

7. 在“分配”页上，选择将接收此配置文件的组。 有关分配配置文件的详细信息，请参阅“分配用户和设备配置文件”。
选择“下一步”。

8. 完成后，在“查看 + 创建”页上，选择“创建” 。 为创建的配置文件选择策略类型时，新配置文件将显示在列表中。

### <a name="create-a-device-configuration-policy-for-filevault"></a>为 FileVault 创建设备配置策略

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“设备” > “配置文件” > “创建配置文件”。

3. 设置下列选项:
   1. **平台**：macOS
   2. **配置文件**：Endpoint Protection

   ![选择 FileVault 配置文件](./media/encrypt-devices-filevault/select-macos-filevault-dc.png)

4. 选择“设置” > “FileVault” 。

   ![FileVault 设置](./media/encrypt-devices-filevault/filevault-settings.png)

5. 对于 FileVault，请选择“启用”。

6. 对于“恢复密钥类型”，仅支持“个人密钥”。

   请考虑添加一条消息，以帮助指导用户检索其设备的恢复密钥。 使用个人恢复密钥轮换设置时，此信息对用户非常有用。通过该设置，可以定期自动为设备生成新的恢复密钥。

   例如：若要检索丢失或最近轮换的恢复密钥，请从任意设备登录 Intune 公司门户网站。 在门户中，转到“设备”并选择已启用 FileVault 的设备，然后选择“获取恢复密钥” 。 系统会显示当前恢复密钥。

7. 配置其余 [FileVault 设置](endpoint-protection-macos.md#filevault)以满足业务需求，然后选择“确定”。

8. 完成其他设置配置，然后保存配置文件。

## <a name="manage-filevault"></a>管理 FileVault

若要查看有关接收 FileVault 策略的设备的信息，请参阅[监视磁盘加密](../protect/encryption-monitor.md)。

Intune 首次使用 FileVault 加密 macOS 设备时，会创建个人恢复密钥。 加密时，设备一次性向设备用户显示个人密钥。

对于受管理设备，Intune 可以托管个人恢复密钥的副本。 通过对密钥进行托管，Intune 管理员可以轮换密钥以帮助保护设备，并且用户可以恢复丢失或轮换的个人恢复密钥。

在 Intune 使用 FileVault 对 macOS 设备进行加密后：

- 管理员可以使用 Intune 加密报告查看和管理 FileVault 恢复密钥。
- 用户可以从设备上的 Web 公司门户查看设备的个人恢复密钥。 在 Web 公司门户中，先选择已加密的 macOS 设备，再选择“获取恢复密钥”作为远程设备操作。

> [!IMPORTANT]
> Intune 无法管理由用户加密而非由 Intune 加密的设备。 即 Intune 无法托管这些设备的个人恢复密钥，也无法管理轮换的恢复密钥。 用户必须解密其设备，然后让 Intune 对设备进行加密，Intune 才可以管理设备的 FileVault 和恢复密钥。

### <a name="retrieve-personal-recovery-key"></a>检索个人恢复密钥

对于 Intune 加密的 macOS 设备，最终用户可以使用 iOS 公司门户应用、Android 公司门户应用或通过 Android Intune 应用检索其个人恢复密钥（FileVault 密钥）。

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
