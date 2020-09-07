---
title: 设置移动设备管理机构
titleSuffix: Microsoft Intune
description: 在 Intune 中设置移动设备管理机构。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/16/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 8deff871-5dff-4767-9484-647428998d82
ms.reviewer: damionw
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 676e7a4db54558eaea87ad2fa8efbe8af546f035
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996565"
---
# <a name="set-the-mobile-device-management-authority"></a>设置移动设备管理机构

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

移动设备管理 (MDM) 机构设置决定了管理设备的方式。 作为 IT 管理员，必须先设置 MDM 机构，然后用户才能注册设备来进行管理。

可能的设置包括：

- **Intune 独立版** - 仅限云的管理，可使用 Azure 门户进行配置。 包括 Intune 提供的所有功能。 [在 Intune 控制台中设置 MDM 机构](#set-mdm-authority-to-intune)。

- **Intune 共同管理** - 集成了 Intune 云解决方案和适用于 Windows 10 设备的 Configuration Manager。 可使用 Configuration Manager 控制台配置 Intune。 [配置设备自动注册到 Intune](/configmgr/comanage/tutorial-co-manage-clients#configure-auto-enrollment-of-devices-to-intune)。 

- **Microsoft 365 的基本移动性和安全性** - 如果已激活此配置，则会看到 MDM 机构设置为“Office 365”。 如果要开始使用 Intune，则需要购买 Intune 许可证。

- **Microsoft 365 的基本移动性和安全性[共存](#coexistence)** - 如果你已在使用 Microsoft 365 的基本移动性和安全性，则可将 Intune 添加到租户上，然后将管理机构设置为 Intune 或 Microsoft 365 的基本移动性和安全性，以便各个用户可决定使用哪项服务管理其注册了 MDM 的设备。 将基于分配给每个用户的许可证定义用户的管理机构：如果用户只有 Microsoft 365 基本或标准许可证，则其设备将由 Microsoft 365 的基本移动性和安全性进行管理。 如果用户有授权使用 Intune 的许可证，则其设备将由 Intune 管理。 如果向之前由 Microsoft 365 的基本移动性和安全性管理的用户添加授权使用 Intune 的许可证，则其设备将切换到 Intune 管理。 在将用户切换到 Intune 之前，请务必分配 Intune 配置给用户，以替换 Microsoft 365 的基本移动性和安全性，否则其设备将丢失 Microsoft 365 的基本移动性和安全性配置，并且不会从 Intune 接收任何替换信息。

## <a name="set-mdm-authority-to-intune"></a>将 MDM 机构设置为 Intune

对于使用 1911 服务版本及更高版本的租户，MDM 机构会自动设置为 Intune。

对于 1911 版本之前的服务版本租户，如果尚未设置 MDM 权限，请执行以下步骤。

1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，选择橙色横幅，打开“移动设备管理机构”设置。 如果尚未设置 MDM 机构，则仅显示橙色横幅。
2. 在“移动设备管理机构”下，从以下选项中选择你的 MDM 机构：
  - Intune MDM 机构
  - **无**

  ![Intune 移动设备管理机构设置屏幕的屏幕截图](./media/mdm-authority-set/set-mdm-auth.png)

  将出现一条消息，表明已成功将 MDM 机构设置为 Intune。

### <a name="workflow-of-intune-administration-ui"></a>Intune 管理 UI 的工作流
启用 Android 或 Apple 设备管理后，Intune 将发送设备和用户信息来与这些第三方服务集成，以便管理其各自的设备。

可以同意共享数据的场景包括：
- 启用 Android 工作配置文件。
- 启用并上传 Apple MDM Push Certificate 时。
- 启用任何诸如设备注册计划、School Manager 或批量采购计划等 Apple 服务时。

不论在哪种情况下，该许可都与运行移动设备管理服务密切相关。 例如，确认 IT 管理员已授权 Google 或 Apple 设备注册。 以下位置提供当新的工作流上线时用于查阅共享了哪些信息的文档：
- [Intune 向 Google 发送的数据](https://aka.ms/Data-intune-sends-to-google)
- [Intune 向 Apple 发送的数据](https://aka.ms/data-intune-sends-to-apple)

## <a name="key-considerations"></a>重要注意事项
切换到新的 MDM 机构后，在设备签入并与服务同步之前，可能会有一定的过渡时间（最长八小时）。 需要在新的 MDM 机构中配置设置，以确保注册的设备在更改后将继续受到管理和保护。 
- 设备必须在更改后与服务连接，以便来自新 MDM 机构（Intune 独立版）的设置可替换设备上的现有设置。
- 更改 MDM 机构后，来自先前 MDM 机构的一些基本设置（如配置文件）将在设备上最长保留 7 天，或直到设备首次连接到该服务为止。 建议尽快配置新 MDM 机构中的应用和设置（如策略、配置文件和应用），并将设置部署到包含具有现有已注册设备的用户的用户组。 更改 MDM 机构后，一旦设备连接到服务，它将从新 MDM 机构接收新设置，并防止在管理和保护方面出现空白。
- 不会将没有关联用户的设备（通常在具有 iOS/iPadOS 设备注册计划或批处理注册方案时）迁移到新的 MDM 机构。 对于这些设备，需要调用支持以获取将它们移动到新 MDM 机构的帮助。

## <a name="coexistence"></a>Coexistence

通过启用共存，可以将 Intune 用于一组新用户，同时继续将基本移动性和安全性用于现有用户。 可以通过用户控制哪些设备由 Intune 管理。 如果用户分配有 Intune 许可证或正在使用 Configuration Manager 进行 Intune 共同管理，则所有已注册的设备都将由 Intune 管理。 否则，用户将由基本移动性和安全性管理。

启用共存有三个主要步骤：
1. 准备工作
2. 添加 Intune MDM 机构
3. 用户和设备迁移（可选）。

### <a name="preparation"></a>准备工作

在启用与基本移动性和安全性的共存之前，请考虑以下几点：
- 确保你想要通过 Intune 管理的用户拥有足够的 [Intune 许可证](licenses.md)。
- 查看哪些用户分配有 Intune 许可证。 启用共存后，任何已分配有 Intune 许可证的用户都可以将其设备切换到 Intune。 若要避免意外的设备切换，我们建议你在启用共存之前不分配任何 Intune 许可证。
- 创建并部署 Intune 策略来替换最初通过 Office 365 安全与合规门户部署的设备安全策略。 应为希望从基本移动性和安全性转换到 Intune 的任何用户执行此替换。 如果没有为这些用户分配 Intune 策略，则启用共存可能会导致其丢失基本移动性和安全性设置。 这些设置将丢失而不进行替换，如托管电子邮件配置文件。 即使将设备安全策略替换为 Intune 策略，在设备移到 Intune 管理后，也可能会提示用户重新对其电子邮件配置文件进行身份验证。

### <a name="add-intune-mdm-authority"></a>添加 Intune MDM 机构

若要启用共存，必须为你的环境添加 Intune 作为 MDM 机构：

1. 使用 Azure AD 全局或 Intune 服务管理员权限登录到 endpoint.microsoft.com。
2. 导航到“设备”。
3. 将显示“添加 MDM 机构”边栏选项卡。
4. 若要将 MDM 机构从“Office 365”切换到“Intune”并启用共存，请选择“Intune MDM 机构” > “添加”。
  “添加 MDM 机构”屏幕的屏幕截图![](./media/mdm-authority-set/add-mdm-authority.png)

### <a name="migrate-users-and-devices-optional"></a>迁移用户和设备（可选）

启用 Intune MDM 机构后，将激活共存，然后可以通过 Intune 开始管理用户。 （可选）如果要将设备由基本移动性和安全性管理转换到由 Intune 管理，请为这些用户分配 Intune 许可证。 用户的设备将在下次 MDM 签入时切换到 Intune。 将不再应用通过基本移动性和安全性应用到这些设备的设置，并且会将其从设备中删除。

## <a name="mobile-device-cleanup-after-mdm-certificate-expiration"></a>MDM 证书过期后的移动设备清理

当移动设备与 Intune 服务通信时，将自动续订 MDM 证书。 如果移动设备被擦除，或者它们在一段时间内无法与 Intune 服务通信，则 MDM 证书将不会续订。 MDM 证书过期 180 天后，设备将从 Azure 门户中删除。

## <a name="remove-mdm-authority"></a>删除 MDM 机构

可将 MDM 机构更改回“未知”。 服务使用 MDM 机构确定已注册设备的目标报告门户（Microsoft Intune 或 Microsoft 365 的基本移动性和安全性）。

## <a name="what-to-expect-after-changing-the-mdm-authority"></a>更改 MDM 机构的预期结果

- 当 Intune 服务检测到租户的 MDM 机构已发生更改时，它将向所有已注册的设备发送通知消息，以便签入并与服务同步（此通知并非计划的定期签入）。 因此，租户的 MDM 机构从 Intune 独立版更改后，开机且联机的所有设备将与服务连接，接收新的 MDM 机构，并且由新的 MDM 机构托管。 对这些设备的管理和保护不会中断。
- 更改 MDM 机构过程中（或在不久之后），即使设备开机且联机，但设备在新的 MDM 机构中注册到该服务之前，将会有最长八小时的延迟（取决于计划的下次定期签入的执行时间）。  

 > [!IMPORTANT]  
 > 在更改 MDM 机构以及将续订的 APN 证书上传到新机构时，iOS/iPadOS 设备的新设备注册和设备签入将失败。 因此，更改 MDM 机构后，请务必尽快查看并将 APN 证书上传到新机构。

- 用户可以通过手动启动从设备到服务的签入来快速更改为新的 MDM 机构。 用户可以通过使用公司门户应用轻松进行此更改，并启动设备符合性检查。
- 更改 MDM 机构后，要验证设备签入并与服务同步后一切工作是否正常运行，可在新 MDM 机构中查找设备。
- 在更改 MDM 机构期间设备处于脱机状态时，以及设备签入服务时，会存在一个过渡期。 为帮助确保设备在此过渡期间仍然受到保护并可正常运行，以下配置文件将在设备上保留长达七天（或直到设备与新的 MDM 机构连接并接收将覆盖现有设置的新设置为止）：
   - 电子邮件配置文件
   - VPN 配置文件
   - 证书配置文件
   - Wi-Fi 配置文件
   - 配置文件
- 更改为新的 MDM 机构后，Microsoft Intune 管理控制台中的符合性数据可能需要长达一周的时间才能准确报告。 但是，Azure Active Directory 和设备上的符合性状态是准确的，因此，设备仍将受到保护。
- 确保用于覆盖现有设置的新设置与以前的设置具有相同的名称，以确保覆盖旧设置。 否则，设备可能会出现冗余配置文件和策略。  

 > [!TIP]  
 > 作为最佳做法，你应该在 MDM 机构更改完成后立即创建所有管理设置和配置以及部署。 这有助于确保在过渡期间对设备进行保护和主动管理。

- 更改 MDM 机构后，请执行以下步骤来验证新设备是否成功注册到新的机构：  
 - 注册新设备
 - 确保新注册的设备显示在新 MDM 机构中。
 - 执行一个从管理控制台到设备的操作，如远程锁定。 如果成功，则表示该设备将由新的 MDM 机构管理。
- 如果你对特定设备有疑问，则可以取消注册然后重新注册设备，以使其连接到新的机构并尽快接受管理。

## <a name="next-steps"></a>后续步骤

设置 MDM 机构后即可开始[注册设备](../enrollment/device-enrollment.md)。