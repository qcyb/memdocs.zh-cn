---
title: 在 Microsoft Intune 中管理终结点安全性 | Microsoft Docs
description: 了解安全管理员如何使用终结点安全性节点在 Microsoft Endpoint Manager 中管理设备的安全性并修正设备问题。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: e3ab2e31aa8a35ef04c150972cd7bb7650e46040
ms.sourcegitcommit: 97f150f8ba8be8746aa32ebc9b909bb47e22121c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84879708"
---
# <a name="manage-endpoint-security-in-microsoft-intune"></a>在 Microsoft Intune 中管理终结点安全性

作为安全管理员，请使用 Intune 中的终结点安全性节点来配置设备安全性，并在这些设备面临风险时管理设备的安全任务。 终结点安全策略旨在帮助你专注于设备的安全性并降低风险。 可用任务有助于识别有风险的设备、对这些设备进行修正，并将其恢复到符合状态或更安全的状态。

终结点安全性节点对通过 Intune 提供的工具进行分组，你将使用这些工具来保证设备的安全性：

- **查看所有托管设备的状态**。 借助[所有设备](#manage-devices)视图，可概括性地了解设备符合性，然后深入到特定设备来了解未满足的符合性策略，以便解决它们。

- **部署为设备建立最佳做法安全配置的安全基线**。 Intune 包括用于 Windows 设备的[安全基线](#manage-security-baselines)，还有一个不断扩充的应用程序列表，其中有 Microsoft Defender 高级威胁防护 (Microsoft Defender ATP) 和 Microsoft Edge 等应用。 安全基线是预配置的几组 Windows 设置，可帮助应用相关安全团队建议的一组已知设置和默认值。

- **通过严格集中的策略管理设备上的安全配置**。  每个[终结点安全性策略](#use-policies-to-manage-device-security)侧重于设备安全的各个方面，例如防病毒、磁盘加密、防火墙，以及通过与 Microsoft Defender ATP 集成而实现的数个方面。

- **通过符合性策略制定设备和用户要求**。 通过[符合性策略](../protect/device-compliance-get-started.md)，可设置设备和用户为实现符合性而必须满足的规则。 规则可包括操作系统版本、密码要求和设备威胁级别等等。

  与 Azure Active Directory (Azure AD) [条件访问策略](#configure-conditional-access)集成来强制实施符合性策略时，可控制托管设备及尚未托管的设备对公司资源的访问权限。

- **将 Intune 与 Microsoft Defender ATP 团队集成**。 通过[与 Microsoft Defender ATP 集成](#set-up-integration-with-microsoft-defender-atp)，获取对[安全任务](#review-security-tasks-from-microsoft-defender-atp)的访问权限。 安全任务将 Microsoft Defender ATP 和 Intune 紧密相连，帮助安全团队确定存在风险的设备并向 Intune 管理员提供详细的修正步骤供其采取行动。

本文的下面各部分介绍了可通过管理中心的终结点安全性节点执行的不同任务，以及使用这些任务所需的基于角色的访问控制 (RBAC) 权限。

## <a name="manage-devices"></a>管理设备

终结点安全性节点包括“所有设备”视图，你可在这里查看 Microsoft Endpoint Manager 中可用的所有 Azure AD 设备的列表。

在此视图中，可选择要深入到的设备来获取详细信息，例如设备不符合哪些策略。 你还可使用此视图中的访问来修正设备的问题，包括重启设备、启动恶意软件扫描或在 Windows 10 设备上轮换 BitLocker 密钥。

有关详细信息，请参阅[在 Microsoft Intune 中使用终结点安全功能管理设备](../protect/endpoint-security-manage-devices.md)。

## <a name="manage-security-baselines"></a>管理安全基线

Intune 中的安全基线是预配置的几组设置，这些设置是 Microsoft 相关安全团队针对该产品提出的最佳做法建议。 Intune 支持对 Windows 10 设备设置、Microsoft Edge 和 Microsoft Defender 高级威胁防护等使用安全基线。

为保护用户和设备，可使用安全基线快速部署设备和应用程序设置的最佳做法配置。 支持对运行 Windows 10 版本 1809 及更高版本的设备使用安全基线。

有关详细信息，请参阅[使用安全基线在 Intune 中配置 Windows 10 设备](../protect/security-baselines.md)。

安全基线是 Intune 中配置设备设置的几种方法之一。 管理设置时，请务必了解环境中可用于配置设备的其他方法，从而避免冲突。 请参阅本文后面的[避免策略冲突](#avoid-policy-conflicts)。

## <a name="review-security-tasks-from-microsoft-defender-atp"></a>查看 Microsoft Defender ATP 中的安全任务

将 Intune 与 Microsoft Defender 高级威胁防护 (Microsoft Defender ATP) 集成后，可查看 Intune 中的安全任务，这些任务可识别存在风险的设备并提供降低风险的步骤。 然后，可使用这些任务在风险成功得到缓解后向 Microsoft Defender ATP 报告。

- Microsoft Defender ATP 团队将确定存在风险的设备，并将该信息作为安全任务传递给 Intune 团队。 他们单击几下即可为 Intune 创建安全任务，用于识别存在风险的设备以及漏洞，并提供有关如何缓解风险的指导。

- Intune 管理员会查看安全任务，然后在 Intune 中进行操作以修正这些任务。 缓解后，他们将任务设置为“完成”，然后将该状态传达回 Microsoft Defender ATP 团队。

通过安全任务，这两个团队可在哪些设备存在风险，以及如何、何时修正这些风险方面保持同步。

要详细了解如何使用安全任务，请参阅[使用 Intune 修正由 Microsoft Defender ATP 标识的漏洞](../protect/atp-manage-vulnerabilities.md)。

## <a name="use-policies-to-manage-device-security"></a>使用策略管理设备安全性

作为安全管理员，请使用终结点安全性节点中的“管理”下的安全策略。 通过这些策略，可配置设备安全性，而无需从设备配置配置文件和安全基线中浏览内容更多的正文和更大范围的设置。

![管理策略](./media/endpoint-security/endpoint-security-policies.png)

要详细了解如何使用这些安全策略，请参阅[使用终结点安全性策略管理设备安全性](../protect/endpoint-security-policy.md)。

终结点安全性策略是 Intune 中配置设备设置的几种方法之一。 管理设置时，请务必了解环境中可用于配置设备的其他方法并避免冲突。 请参阅本文后面的[避免策略冲突](#avoid-policy-conflicts)。

还可在“管理”下找到设备符合性和条件访问策略  。 这些策略类型不是用于配置终结点的集中安全策略，而是用于管理设备和访问公司资源的重要工具。

## <a name="use-device-compliance-policy"></a>使用设备符合性策略

使用设备符合性策略来确定允许设备和用户访问网络及公司资源的条件。

[可用的符合性设置](../protect/device-compliance-get-started.md#next-steps)取决于所使用的平台，但常见的策略规则包括：

- 要求设备运行最低版本或特定版本的操作系统
- 设置密码要求
- 指定由 Microsoft Defender ATP 或其他移动威胁防御合作伙伴确定的最大允许设备威胁级别

除了策略规则，符合性策略还支持：

- 在 Intune 中定义的[位置](../protect/use-network-locations.md)。 使用具有符合性策略的位置时，策略可确保设备连接到工作网络以符合相关条件。
- [针对非符合性的操作](../protect/actions-for-noncompliance.md) 这些操作按时间顺序排列，应用于不符合条件的设备。 操作包括发送电子邮件或通知来提醒设备用户存在非符合性的情况、远程锁定设备，甚至停用不符合条件的设备并删除其上可能包含的所有公司数据。

将 Intune 与 Azure AD [条件访问策略](#configure-conditional-access)集成来强制实施符合性策略后，条件访问可使用符合性数据来控制托管设备及未托管的设备对公司资源的访问权限。

要了解详细信息，请参阅[在设备上设置规则以允许使用 Intune 访问组织中的资源](../protect/device-compliance-get-started.md)。

设备符合性策略是 Intune 中配置设备设置的几种方法之一。 管理设置时，请务必了解环境中可用于配置设备的其他方法并避免冲突。 请参阅本文后面的[避免策略冲突](#avoid-policy-conflicts)。

## <a name="configure-conditional-access"></a>配置条件访问

为了保护设备和公司资源，可将 Azure Active Directory (Azure AD) 条件访问策略与 Intune 结合使用。

Intune 将设备符合性策略的结果传递给 Azure AD，然后 Azure AD 使用条件访问策略来强制实施哪些设备和应用程序可访问你的公司资源。 条件访问策略可帮助控制不由 Intune 托管的设备的访问权限。 你甚至还可使用与 Intune 集成的 [Mobile Threat Defense 合作伙伴](../protect/mobile-threat-defense.md)的符合性详细信息。

下面是将条件访问与 Intune 结合使用的两种常见方法：

- 基于设备的条件访问，它确保只有托管和符合条件的设备可访问网络资源。
- 基于应用的条件访问，它使用应用保护策略来管理用户对未使用 Intune 管理的设备上的网络资源的访问。

要详细了解如何条件访问与 Intune 结合使用，请参阅[了解条件访问和 Intune](../protect/conditional-access.md)。

## <a name="set-up-integration-with-microsoft-defender-atp"></a>设置与 Microsoft Defender ATP 集成

将 Microsoft Defender ATP 与 Intune 集成后，可提高确定和应对风险的能力。

虽然 Intune 可与多个[移动威胁防御合作伙伴](../protect/mobile-threat-defense.md)集成，但使用 Microsoft Defender ATP 时，将 Microsoft Defender ATP 与 Intune 紧密集成，你还能访问深层设备保护选项，包括：

- 安全任务 - ATP 与 Intune 管理员之间就存在风险的设备、如何修正风险以及确认何时缓解风险方面进行无缝通信。
- 简化在客户端上加入 Microsoft Defender ATP 的流程。
- 在 Intune 符合性策略中使用 ATP 设备风险信号。
- 获得“篡改防护”功能。

 要详细了解如何将 Microsoft Defender ATP 与 Intune 结合使用，请参阅[使用 Intune 中的条件访问强制执行 Microsoft Defender ATP 的符合性](../protect/advanced-threat-protection.md)。

## <a name="role-based-access-control-requirements"></a>基于角色的访问控制要求

若要在 Microsoft Endpoint Manager 管理中心的终结点安全性节点中管理任务，帐户必须：

- 分配有 Intune 许可证。
- 具有基于角色的访问控制 (RBAC) 权限，且这些权限等效于内置的 Intune“终结点安全性管理员”角色。 “终结点安全性管理员”角色会授予对 Microsoft Endpoint Manager 管理中心的访问权限。 此角色可由管理安全性和符合性功能的人员使用，这些功能包括安全基线、设备符合性、条件访问和 Microsoft Defender ATP。

有关详细信息，请参阅 [Microsoft Intune 的基于角色的访问控制 (RBAC)](../fundamentals/role-based-access-control.md)

### <a name="permissions-granted-by-the-endpoint-security-manager-role"></a>“终结点安全性管理员”角色授予的权限

可转到“租户管理” > “角色” > “所有角色”，再选择“终结点安全性管理员” > “属性”，在 Microsoft Endpoint Manager 管理中心查看以下权限列表    。

**权限：**

- **Android for Work**
  - 读取
- **审核数据**
  - 读取
- **公司设备标识符**
  - 读取
- **设备合规性策略**
  - 分配
  - 创建
  - 删除
  - 读取
  - 更新
  - 查看报表
- **设备配置**
  - 读取
- **设备注册管理器**
  - 读取
- **Endpoint Protection 报表**
  - 读取
- **注册计划**
  - 读取设备
  - 读取配置文件
  - 读取令牌
- **Intune 数据仓库**
  - 读取
- **受管理应用**
  - 读取
- **受管理设备**
  - 删除
  - 读取
  - 设置主要用户
  - 更新
- **移动应用**
  - 读取
- **组织**
  - 读取
- **PolicySets**
  - 读取
- **远程协助**
  - 读取
- **远程任务**
  - 获取 FileVault 密钥。
- **角色**
  - 读取
- **安全基线**
  - 分配
  - 创建
  - 删除
  - 读取
  - 更新
- **安全任务**
  - 读取
  - 更新
- **电信费用**
  - 读取
- **条款和条件**
  - 读取

## <a name="avoid-policy-conflicts"></a>避免策略冲突

可为设备配置的许多设置都可通过 Intune 中的不同功能进行管理。 这些功能包括（但不限于）：

- 终结点安全性策略
- 安全基线
- 设备配置策略
- Windows 10 注册策略

例如，终结点安全性策略中的设置包含在设备配置策略的“终结点保护”和“设备限制”配置文件中找到的设置内，它们同样通过各种安全基线进行管理 。

要避免冲突，一种方法是不使用不同的基线、相同基线的实例，也不使用不同策略类型和实例来管理设备上的相同设置。 这要求规划用于将配置部署到不同设备的方法。 使用多种方法或同一方法的实例来配置相同的设置时，请确保不同方法一致或未部署到同一设备。

如果发生冲突，可使用 Intune 的内置工具来确定这些冲突的来源并进行解决。 有关详情，请参阅：

- [在 Intune 中对策略和配置文件进行故障排除](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [监视安全基线](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="next-steps"></a>后续步骤

配置：

- [安全基线](../protect/security-baselines.md)
- [符合性策略](../protect/device-compliance-get-started.md)
- [条件访问策略](#configure-conditional-access)
- [与 Microsoft Defender ATP 集成](../protect/advanced-threat-protection.md)
