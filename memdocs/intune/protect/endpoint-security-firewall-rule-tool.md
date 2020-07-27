---
title: 用于 Microsoft Intune 的终结点安全防火墙规则迁移工具 - Azure | Microsoft Docs
description: 了解如何使用用于 Microsoft Intune 的终结点安全防火墙规则迁移工具。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/14/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: mattsha
ms.openlocfilehash: 7dd6d3a01d18e4d8b334bdeee3f72eeaeed67c0a
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2020
ms.locfileid: "86464970"
---
# <a name="endpoint-security-firewall-rule-migration-tool-overview"></a>终结点安全防火墙规则迁移工具概述

许多组织都希望将其安全配置移动到 Microsoft Endpoint Manager，以充分利用基于云的现代管理。

Endpoint Manager 中的终结点安全提供了丰富的 Windows 防火墙配置和精细防火墙规则管理的管理体验。

在许多组织中，他们已经制定了组策略来管理其 Windows 防火墙规则。 转向现代管理可能比较棘手，因为手动创建数百个防火墙规则会令人厌烦。

为了帮助客户将防火墙规则配置移动到 Endpoint Manager 中的终结点安全策略，我们已开发“终结点安全防火墙规则迁移工具”。

客户可以在参考/预配置的 Windows 10 客户端上运行“终结点安全防火墙规则迁移工具”，并在 Endpoint Manager 中自动创建终结点安全防火墙规则策略。 创建后，管理员可以将这些规则定位到 Azure AD 组，以配置 MDM 和共同管理的客户端。

下载[终结点安全防火墙规则迁移工具](https://aka.ms/EndpointSecurityFWRuleMigrationTool)：<br>
<a href="https://aka.ms/EndpointSecurityFWRuleMigrationTool"><img alt="Download the tool" src="./media/endpoint-security-firewall-rule-tool/downloadtool.png" width="170"></a>

## <a name="tool-usage"></a>工具用法

该工具在参考计算机上运行，并迁移当前的 Windows 防火墙规则配置。 运行该工具将导出设备上存在的所有启用的防火墙规则，并自动使用收集的规则创建新的 Intune 策略。

1. 使用本地管理员权限登录到参考计算机。
2. 下载并解压文件 `Export-FirewallRules.zip`。 <br>
   该压缩文件包含脚本文件 `Export-FirewallRules.ps1`。 
3. 在计算机上运行 `Export-FirewallRules.ps1` 脚本。 <br>
   该脚本将下载运行所需的所有必备组件。 出现提示时，请提供适当的 Intune 管理员凭据。 有关所需权限的详细信息，请参阅[所需权限](#required-permissions)。
4. 出现提示时，请提供策略名称。 <br>
   该策略将显示在“终结点安全” > “防火墙”窗格中的 [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) 中 。 

    > [!IMPORTANT]
    > 对于租户，策略的名称必须是唯一的。

    如果找到超过 150 个防火墙规则，则将创建多个策略。

    > [!NOTE]
    > 默认情况下，将仅迁移启用的防火墙规则，并仅迁移由 GPO 创建的防火墙规则。 提供交换机来修改这些默认值。 有关详细信息，请参阅[交换机](#switches)。
    >
    > 根据找到的防火墙规则的计数，该工具可能需要一些时间才能运行。

5. 完成后，该工具将输出无法自动迁移的防火墙规则计数。 有关详细信息，请参阅[不支持的配置](#unsupported-configuration)。

## <a name="switches"></a>交换机

你可以使用以下交换机（参数）修改工具的默认功能。

- `IncludeLocalRules` -使用此交换机将在导出中包括所有本地创建/默认的 Windows 防火墙规则。 请注意，启用此交换机会导致许多包含的规则。 
- `IncludedDisabledRules` - 使用此交换机将在导出中包括所有已启用和禁用的 Windows 防火墙规则。 请注意，启用此交换机会导致许多包含的规则。

## <a name="unsupported-configuration"></a>不支持的配置

由于 Windows 中缺少 MDM 支持，所以不支持以下基于注册表的设置。 这些设置并不常见，但如果你需要这些设置，请通过标准支持渠道记录此需求。

|     GPO 字段    |     原因    |
|-|-|
|      TYPE-VALUE =/ "Security=" IFSECURE-VAL    |     Windows MDM 不支持与 IPSec 相关的设置    |
|      TYPE-VALUE =/ "Security2_9=" IFSECURE2-9-VAL    |     Windows MDM 不支持与 IPSec 相关的设置    |
|      TYPE-VALUE =/ "Security2=" IFSECURE2-10-VAL     |     Windows MDM 不支持与 IPSec 相关的设置    |
|      TYPE-VALUE =/ "IF=" IF-VAL    |     接口标识符 (LUID) 不可管理    |
|      TYPE-VALUE =/ "Defer=" DEFER-VAL    |     未通过组策略或 Windows MDM 公开相关入站 NAT 遍历    |
|      TYPE-VALUE =/ "LSM=" BOOL-VAL    |     未通过组策略或 Windows MDM 公开松散源映射    |
|      TYPE-VALUE =/ "Platform=" PLATFORM-VAL    |     未通过组策略或 Windows MDM 公开 OS 版本控制    |
|      TYPE-VALUE =/ "RMauth=" STR-VAL    |     Windows MDM 不支持与 IPSec 相关的设置    |
|      TYPE-VALUE =/ "RUAuth=" STR-VAL    |     Windows MDM 不支持与 IPSec 相关的设置    |
|      TYPE-VALUE =/ "AuthByPassOut=" BOOL-VAL    |     Windows MDM 不支持与 IPSec 相关的设置    |
|      TYPE-VALUE =/ "LOM=" BOOL-VAL    |     未通过组策略或 Windows MDM 公开“仅限本地映射”    |
|      TYPE-VALUE =/ "Platform2=" PLATFORM-OP-VAL    |     未通过组策略或 Windows MDM 公开冗余设置    |
|      TYPE-VALUE =/ "PCross=" BOOL-VAL    |     未通过组策略或 Windows MDM 公开“允许配置文件交叉”    |
|      TYPE-VALUE =/ "LUOwn=" STR-VAL    |     本地用户所有者 SID 在 MDM 中不适用    |
|      TYPE-VALUE =/ "TTK=" TRUST-TUPLE-KEYWORD-VAL    |     未通过组策略或 Windows MDM 公开“将流量与信任元组关键字匹配”    |
|      TYPE-VALUE =/ “TTK2_22=” TRUST-TUPLE-KEYWORD-VAL2-22    |     未通过组策略或 Windows MDM 公开“将流量与信任元组关键字匹配”    |
|      TYPE-VALUE =/ “TTK2_27=” TRUST-TUPLE-KEYWORD-VAL2-27    |     未通过组策略或 Windows MDM 公开“将流量与信任元组关键字匹配”    |
|      TYPE-VALUE =/ “TTK2_28=” TRUST-TUPLE-KEYWORD-VAL2-28    |     未通过组策略或 Windows MDM 公开“将流量与信任元组关键字匹配”    |
|      TYPE-VALUE =/ "NNm=" STR-ENC-VAL    |     Windows MDM 不支持与 IPSec 相关的设置    |
|      TYPE-VALUE =/ "SecurityRealmId=" STR-VAL    |     Windows MDM 不支持与 IPSec 相关的设置    |

## <a name="unsupported-setting-values"></a>不支持的设置值
迁移不支持以下设置值：

**端口**
- `PlayToDiscovery` 不支持作为本地或远程端口范围。

**地址范围**
- `LocalSubnet6` 不支持作为本地或远程地址范围。 
- `LocalSubnet4` 不支持作为本地或远程地址范围。
- `PlatToDevice` 不支持作为本地或远程地址范围。

运行该工具后，将生成一个报告，其中包含未成功迁移的规则。 可以通过在 `C:\<folder needed>` 中找到的 `RulesError.csv` 来查看这些规则。 

## <a name="required-permissions"></a>所需权限
终结点安全管理器、Intune 服务管理员或全局管理员用户可以将 Windows 防火墙规则迁移到终结点安全策略。 另外，还可以使用自定义角色，其中使用“删除”、“读取”、“分配”、“创建”设置了安全基准权限，并应用了“更新”授权    。 有关详细信息，请参阅[向 Intune 授予管理员权限](../fundamentals/users-add.md#grant-admin-permissions)。

## <a name="next-steps"></a>后续步骤

- 将规则分配给 Azure AD 组以配置 MDM 和共同管理的客户端。 有关详细信息，请参阅[添加用于组织用户和设备的组](../fundamentals/groups-add.md)。
