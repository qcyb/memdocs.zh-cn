---
title: 分配 Microsoft Intune 许可证
description: 向用户分配许可证，以便他们能够在 Intune 中进行注册
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/12/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: bb4314ea-88b5-44d3-92ce-4c6aff0587a4
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: b8552bd6bb570c91e84acd40cd2b654696eca972
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210343"
---
# <a name="assign-licenses-to-users-so-they-can-enroll-devices-in-intune"></a>向用户分配许可证，以便他们能够在 Intune 中注册设备

不管是手动添加用户还是从本地 Active Directory 同步，都必须首先为每个用户分配一个 Intune 许可证，然后用户才能在 Intune 中注册其设备。 如需查看许可证的列表，请参阅[包括 Intune 的许可证](licenses.md)。

> [!NOTE]
> 如果已向用户分配 Intune 应用保护策略但他们未将其设备注册到 Microsoft Intune，他们也需要获得 Intune 许可证以接收策略。

## <a name="assign-an-intune-license-microsoft-endpoint-manager-admin-center"></a>在 Microsoft Endpoint Manager 管理中心中分配 Intune 许可证

可以使用 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)手动添加基于云的用户并将许可证分配给基于云的用户帐户和从本地 Active Directory 同步到 Azure AD 的帐户。

1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“用户” > “所有用户”> 选择用户 >“许可证” > “分配”     。

2. 依次选择“Intune”框   > “保存”。  若要使用企业移动性 + 安全性 E5 或其他许可证，请改为选中此框。

   ![Microsoft 365 管理中心产品许可证部分的屏幕截图。](./media/licenses-assign/mem-assign-license.png)

3. 现在，该用户帐户拥有所需的权限，可以使用该服务并在管理组件中注册设备。

> [!NOTE]
> 只有在使用 Intune PC 客户端注册了设备后，用户才会出现在经典 Intune 门户中。 此外，你还可以选择要立即编辑的一组用户，为所选的用户选择添加或替换许可证。

## <a name="assign-an-intune-license-by-using-azure-active-directory"></a>使用 Azure Active Directory 分配 Intune 许可证

也可以使用 Azure Active Directory 向用户分配 Intune 许可证。 有关详细信息，请参阅 [Azure Active Directory 中的许可证用户一文](https://docs.microsoft.com/azure/active-directory/active-directory-licensing-group-assignment-azure-portal)。 

## <a name="use-school-data-sync-to-assign-licenses-to-users-in-intune-for-education"></a>使用“学校数据同步”向 Intune for Education 中的用户分配许可证

如果你是教育组织，可以使用“学校数据同步 (SDS)”向同步用户分配 Intune for Education 许可证。 只需在设置 SDS 配置文件时，选中“Intune for Education”复选框。  

![SDS 配置文件设置的屏幕截图](./media/licenses-assign/i4e-sds-profile-setup-setting.png)

分配 Intune for Education 许可证时，请确保同时分配 Intune A Direct 许可证。

![产品许可证设置的屏幕截图](./media/licenses-assign/i4e-set-licenses.png)

请参阅此[学校数据同步概述](https://support.office.com/article/Overview-of-School-Data-Sync-and-Classroom-f3d1147b-4ade-4905-8518-508e729f2e91)，了解有关 SDS 的详细信息。

## <a name="how-user-and-device-licenses-affect-access-to-services"></a>用户和设备许可证如何影响对服务的访问

* 每个你向其分配用户软件许可证的用户  ，均可访问和使用联机服务和相关软件（包括 System Center 软件）来管理应用程序和多达 15 台的 MDM 设备。 Intune PC 代理允许每个用户许可证对应 5 台物理计算机和 1 台虚拟机。
* 可以从用户许可证中单独为任何设备购买许可证。 不需要将设备许可证分配给设备。 访问和使用在线服务及相关软件（包括 System Center 软件）的每台设备都必须拥有设备许可证。
* 如果设备由多个用户使用，则每位用户均需要设备软件许可证，或所有用户都需要用户软件许可证。

## <a name="understanding-the-type-of-licenses-you-have-purchased"></a>了解已购买许可证的类型

已购买的 Intune 如何决定订阅信息：

- 如果通过企业协议购买 Intune，则可在批量许可证门户的“订阅”下找到订阅信息  。
- 如果通过云解决方案提供商购买 Intune，请与分销商联系。
- 如果通过 CC# 或转账的方式购买 Intune，则许可证将是基于用户的。

## <a name="use-powershell-to-selectively-manage-ems-user-licenses"></a>使用 PowerShell 来选择性地管理 EMS 用户许可证
使用 Microsoft 企业移动性 + 安全性（以前称为“企业移动性套件”）的组织中可能会有只需要 Azure Active Directory Premium 或 EMS 包中的 Intune 服务的用户。 你可以使用 [Azure Active Directory PowerShell cmdlet](https://msdn.microsoft.com/library/jj151815.aspx) 分配一个或一部分服务。

若要有选择性地为 EMS 服务分配用户许可证，请使用已安装的[用于 Windows PowerShell 的 Azure Active Directory 模块](https://msdn.microsoft.com/library/jj151815.aspx#bkmk_installmodule)在计算机上以管理员身份打开 PowerShell。 你可以在本地计算机或 ADFS 服务器上安装 PowerShell。

必须创建仅应用于所需服务计划的新许可证 SKU 定义。 若要执行此操作，请禁用不想应用的计划。 例如，你可以创建一个不分配 Intune 许可证的许可证 SKU 定义。 若要查看从可用服务的列表，请键入：

    (Get-MsolAccountSku | Where {$_.SkuPartNumber -eq "EMS"}).ServiceStatus

你可以运行下面的命令来排除 Intune 服务计划。 你可以使用相同的方法来扩展整个安全组，或者使用更精细的筛选器。

**示例 1**<br>
在命令行上创建一个新用户，并在不启用许可证的 Intune 部分的情况下分配一个 EMS 许可证：

    Connect-MsolService

    New-MsolUser -DisplayName "Test User" -FirstName FName -LastName LName -UserPrincipalName user@<TenantName>.onmicrosoft.com –Department DName -UsageLocation US

    $CustomEMS = New-MsolLicenseOptions -AccountSkuId "<TenantName>:EMS" -DisabledPlans INTUNE_A
    Set-MsolUserLicense -UserPrincipalName user@<TenantName>.onmicrosoft.com -AddLicenses <TenantName>:EMS -LicenseOptions $CustomEMS

验证方式：

    (Get-MsolUser -UserPrincipalName "user@<TenantName>.onmicrosoft.com").Licenses.ServiceStatus

**示例 2**<br>
为已获得许可证的用户禁用 EMS 许可证的 Intune 部分：

    Connect-MsolService

    $CustomEMS = New-MsolLicenseOptions -AccountSkuId "<TenantName>:EMS" -DisabledPlans INTUNE_A
    Set-MsolUserLicense -UserPrincipalName user@<TenantName>.onmicrosoft.com -LicenseOptions $CustomEMS

验证方式：

    (Get-MsolUser -UserPrincipalName "user@<TenantName>.onmicrosoft.com").Licenses.ServiceStatus

![PoSH-AddLic-Verify](./media/licenses-assign/posh-addlic-verify.png)
