---
title: 部署 BitLocker 管理
titleSuffix: Configuration Manager
description: 将 BitLocker 管理代理部署到 Configuration Manager 客户端，并将恢复服务部署到管理点
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 39aa0558-742c-4171-81bc-9b1e6707f4ea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 96594731ef64577d30267376d3bcb93268e59a9e
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075007"
---
# <a name="deploy-bitlocker-management"></a>部署 BitLocker 管理

适用范围：  Configuration Manager (Current Branch)

<!--3601034-->

Configuration Manager 中的 BitLocker 管理包含以下组件：

- **BitLocker 管理代理**：当[创建策略](#create-a-policy)并[将其部署到集合](#deploy-a-policy)时，Configuration Manager 会在设备上启用此代理。

- **恢复服务**：这是接收来自客户端的 BitLocker 恢复数据的服务器组件。 有关详细信息，请参阅[恢复服务](#recovery-service)。

创建和部署 BitLocker 管理策略之前的准备工作：

- 查看[先决条件](../../plan-design/bitlocker-management.md#prerequisites)

- 如有必要，请在站点数据库中[加密恢复密钥](encrypt-recovery-data.md)

## <a name="create-a-policy"></a>创建策略

在创建和部署此策略时，Configuration Manager 客户端将在设备上启用 BitLocker 管理代理。

> [!NOTE]
> 若要创建 BitLocker 管理策略，需要 Configuration Manager 中的“完全权限管理员”角色  。

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区，展开“Endpoint Protection”，然后选择“BitLocker 管理”节点    。

1. 在功能区中选择“创建 BitLocker 管理控制策略”  。

1. 在“常规”页中，指定名称和可选说明  。 选择要在具有此策略的客户端上启用的组件：  

    - **操作系统驱动器**：管理是否加密 OS 驱动器

    - **固定驱动器**：管理设备中其他数据驱动器的加密

    - **可移动驱动器**：管理可从设备中移除的驱动器的加密，如 USB 密钥

    - **客户端管理**：管理 BitLocker 驱动器加密恢复信息的密钥恢复服务备份  

1. 在“设置”页面上，针对 BitLocker 驱动器加密配置以下全局设置  ：

    > [!NOTE]
    > 启用 BitLocker 时，Configuration Manager 会应用这些设置。 如果驱动器已加密或正在处理中，则对这些策略设置的任何更改都不会更改设备上的驱动器加密状况。
    >
    > 如果禁用或未配置这些设置，BitLocker 将采用默认加密方法（AES 128 位）。

    - 对于 Windows 8.1 设备，请启用“驱动器加密方法和密码强度”选项  。 然后选择加密方法。

    - 对于 Windows 10 设备，请启用“驱动器加密方法和密码强度(Windows 10)”选项  。 然后分别为 OS 驱动器、固定数据驱动器和可移动数据驱动器选择加密方法。

    若要详细了解此页面上的这些设置和其他设置，请参阅[设置参考 - 设置](../../tech-ref/bitlocker/settings.md#setup)。

1. 在“操作系统驱动器”页上，指定以下设置  ：  

    - **操作系统驱动器加密设置**：如果启用此设置，用户必须保护 OS 驱动器，并且 BitLocker 会加密驱动器。 如果禁用该设置，用户无法保护驱动器。  

    在具有兼容的 TPM 的设备上，可以在启动时使用两种类型的身份验证方法，以便为加密的数据提供额外的保护。 在计算机启动时，它只能使用 TPM 进行身份验证，或者它还可能要求输入个人标识号 (PIN)。 配置下列设置：

    - **选择操作系统驱动器的保护程序**：将其配置为使用 TPM 和 PIN 或只使用 TPM。

    - **配置启动时的最小 PIN 长度**：如果要求使用 PIN，则此值是用户可以指定的最短长度。 在计算机启动以解锁驱动器时，用户输入此 PIN。 默认情况下，最小 PIN 长度为 `4`。

    若要详细了解此页面上的这些设置和其他设置，请参阅[设置参考 - OS 驱动器](../../tech-ref/bitlocker/settings.md#os-drive)。

1. 在“固定驱动器”页面上，指定以下设置  ：

    - **固定数据驱动器加密**：如果启用此设置，BitLocker 会要求用户将所有固定数据驱动器置于被保护状态。 然后对数据驱动器进行加密。 启用此策略时，请启用自动解锁或“固定数据驱动器密码策略”设置  。

    - **为固定数据驱动器配置自动解锁**：允许或要求 BitLocker 自动解锁任何加密的数据驱动器。 若要使用自动解锁，还需要使用 BitLocker 加密 OS 驱动器。

    若要详细了解此页面上的这些设置和其他设置，请参阅[设置参考 - 固定驱动器](../../tech-ref/bitlocker/settings.md#fixed-drive)。

1. 在“可移动驱动器”页面上，指定以下设置  ：

    - **可移动数据驱动器加密**：如果启用此设置并允许用户应用 BitLocker 保护，Configuration Manager 客户端会将有关可移动驱动器的恢复信息保存到管理点上的恢复服务。 此行为允许用户在忘记或丢失保护手段（密码）的情况下恢复驱动器。

    - **允许用户对可移动数据驱动器应用 BitLocker 保护**：用户可以为可移动驱动器启用 BitLocker 保护。

    - **可移动数据驱动器密码策略**：使用这些设置设置密码约束，以解锁受 BitLocker 保护的可移动驱动器。

    若要详细了解此页面上的这些设置和其他设置，请参阅[设置参考 - 可移动驱动器](../../tech-ref/bitlocker/settings.md#removable-drive)。

1. 在“客户端管理”页上，指定以下设置  ：

    > [!IMPORTANT]
    > 如果管理点中没有已启用 HTTPS 的网站，请勿配置此设置。 有关详细信息，请参阅[恢复服务](#recovery-service)。

    - **配置 BitLocker 管理服务**：启用此设置时，Configuration Manager 会自动且无提示地备份站点数据库中的密钥恢复信息。 如果禁用或未配置此设置，则 Configuration Manager 不会保存密钥恢复信息。

        - **选择要存储的 BitLocker 恢复信息**：将其配置为使用恢复密码和密钥包，或仅使用恢复密码。

        - **允许以纯文本格式存储恢复信息**：如果没有 BitLocker 管理加密证书，Configuration Manager 会以纯文本形式存储密钥恢复信息。 有关详细信息，请参阅[加密恢复数据](encrypt-recovery-data.md)。

    若要详细了解此页面上的这些设置和其他设置，请参阅[设置参考 - 客户端管理](../../tech-ref/bitlocker/settings.md#client-management)。

1. 完成向导。

若要更改现有策略的设置，请在列表中选择它，然后选择“属性”  。

在创建多个策略时，可以配置它们的相对优先级。 如果将多个策略部署到一个客户端，系统会根据优先级值来确定其设置。

## <a name="deploy-a-policy"></a>部署策略

1. 选择“BitLocker 管理”节点中的现有策略  。 在功能区中，选择“部署”  。

1. 选择作为部署目标的设备集合。

1. 如果希望设备在任何时候都可能加密或解密其驱动器，请选择“允许维护时段外的修正”选项  。 即使集合存在维护时段，仍会修正此 BitLocker 策略。

1. 配置简单计划或自定义计划   。 默认情况下，客户端每 12 小时评估一次针对此策略的符合性。

1. 选择“确定”部署策略  。

可以为同一策略创建多个部署。 若要查看有关每个部署的其他信息，请在“BitLocker 管理”节点中选择策略，然后在详细信息窗格中切换到“部署”选项卡   。

## <a name="monitor"></a>监视

在“BitLocker 管理”节点的详细信息窗格中，查看有关策略部署的基本符合性统计信息  ：

- 符合性计数
- 失败计数
- 不符合项计数

切换到“部署”选项卡，查看符合性百分比和推荐的操作  。 选择部署，然后在功能区中选择“查看状态”  。 此操作会将视图切换到“监视”工作区的“部署”节点   。 与其他配置策略部署的部署类似，可以在此视图中查看更详细的符合性状态。

若要了解客户端报告不符合 BitLocker 管理策略的原因，请参阅[不符合性代码](../../tech-ref/bitlocker/non-compliance-codes.md)。

若要详细了解如何排除故障，请参阅[排除 BitLocker 故障](../../tech-ref/bitlocker/troubleshoot.md)。

使用以下日志进行监视和故障排除：

### <a name="client-logs"></a>客户端日志

- MBAM 事件日志：在 Windows 事件查看器中，浏览到“应用程序和服务”>“Microsoft”>“Windows”>“MBAM”。  有关详细信息，请参阅[关于 BitLocker 事件日志](../../tech-ref/bitlocker/about-event-logs.md)和[客户端事件日志](../../tech-ref/bitlocker/client-event-logs.md)。

- 客户端日志路径中的 BitlockerMangementHandler.log，默认情况下为 `%WINDIR%\CCM\Logs`

### <a name="management-point-logs-recovery-service"></a>管理点日志（恢复服务）

- 恢复服务事件日志：在 Windows 事件查看器中，浏览到“应用程序和服务”>“Microsoft”>“Windows”>“MBAM-Web”。 有关详细信息，请参阅[关于 BitLocker 事件日志](../../tech-ref/bitlocker/about-event-logs.md)和[服务器事件日志](../../tech-ref/bitlocker/server-event-logs.md)。

- 恢复服务跟踪日志：`<Default IIS Web Root>\Microsoft BitLocker Management Solution\Logs\Recovery And Hardware Service\trace*.etl`

## <a name="recovery-service"></a>恢复服务

BitLocker 恢复服务是一种服务器组件，用于接收来自 Configuration Manager 客户端的 BitLocker 恢复数据。 创建 BitLocker 管理策略时，站点将部署恢复服务。 Configuration Manager 在带有已启用 HTTPS 网站的每个管理点上自动安装恢复服务。

Configuration Manager 将恢复信息存储在站点数据库中。 如果没有 BitLocker 管理加密证书，Configuration Manager 会以纯文本形式存储密钥恢复信息。

有关详细信息，请参阅[加密恢复数据](encrypt-recovery-data.md)。

## <a name="migration-considerations"></a>迁移注意事项

如果当前使用 Microsoft BitLocker Administration and Monitoring (MBAM)，则可以将管理无缝迁移到 Configuration Manager。 在 Configuration Manager 中部署 BitLocker 管理策略时，客户端会自动将恢复密钥和包上传到 Configuration Manager 恢复服务。

> [!IMPORTANT]
> 在从独立 MBAM 迁移到 Configuration Manager BitLocker 管理时，如果需要独立 MBAM 的现有功能，请勿通过 Configuration Manager BitLocker 管理重复使用独立 MBAM 服务或组件。 如果重复使用这些服务器，当 Configuration Manager BitLocker 管理在这些服务器上安装其组件时，独立 MBAM 将停止工作。 请勿运行 MBAMWebSiteInstaller.ps1 脚本在独立的 MBAM 服务器上设置 BitLocker 门户。 设置 Configuration Manager BitLocker 管理时，请使用单独的服务器。

### <a name="group-policy"></a>组策略

- BitLocker 管理设置与 MBAM 组策略设置是完全兼容的。 如果设备接收组策略设置和 Configuration Manager 策略，请配置它们以进行匹配。

- Configuration Manager 不实现所有 MBAM 组策略设置。 如果在组策略中配置其他设置，则 Configuration Manager 客户端上的 BitLocker 管理代理将遵循这些设置。

### <a name="tpm-password-hash"></a>TPM 密码哈希

- 以前的 MBAM 客户端不会将 TPM 密码哈希上传到 Configuration Manager。 客户端仅上传一次 TPM 密码哈希。

- 如果需要将此信息迁移到 Configuration Manager 恢复服务，请在设备上清除 TPM。 重新启动后，它会将新的 TPM 密码哈希上传到恢复服务。

### <a name="re-encryption"></a>重新加密

Configuration Manager 不会重新加密已使用 BitLocker 驱动器加密保护的驱动器。 如果部署的 BitLocker 管理策略与驱动器的当前保护状况不匹配，则会将其报告为不符合。 驱动器仍会受到保护。

例如，使用 MBAM 在没有 PIN 保护的情况下加密驱动器，但 Configuration Manager 策略需要 PIN。 即使驱动器已加密，它也不符合该策略。

为了解决此问题，请先在设备上禁用 BitLocker。 然后使用新设置部署新策略。

## <a name="co-management-and-intune"></a>共同管理和 Intune

<!-- SCCMDocs#2321 -->

BitLocker 的 Configuration Manager 客户端处理程序可感知共同管理。 如果设备已进行共同管理，并且你将 [Endpoint Protection 工作负载](../../../comanage/workloads.md#endpoint-protection)切换到了 Intune，则 Configuration Manager 客户端会忽略它的 BitLocker 策略。 该设备会从 Intune 获取 Windows 加密策略。

在切换加密管理机构时，请计划[重新加密](#re-encryption)。

要详细了解如何使用 Intune 管理 BitLocker，请参阅以下文章：

- [使用 Intune 设备加密](../../../../intune/protect/encrypt-devices.md#bitlocker-encryption-for-windows-10)
- [Microsoft Intune 中 BitLocker 策略问题疑难解答](../../../../intune/protect/troubleshoot-bitlocker-policies.md)

## <a name="next-steps"></a>后续步骤

[设置 BitLocker 报表和门户](setup-websites.md)
