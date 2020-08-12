---
title: 在 Microsoft Intune 中设置注册限制
titleSuffix: ''
description: 按平台限制注册，并在 Intune 中设置设备注册限制。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/17/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 9691982c-1a03-4ac1-b7c5-73087be8c5f2
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e5ed799d01ea4fdae1f9ecb013b4cf73deb0e6f0
ms.sourcegitcommit: 47ed9af2652495adb539638afe4e0bb0be267b9e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/10/2020
ms.locfileid: "88051649"
---
# <a name="set-enrollment-restrictions"></a>设置注册限制

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

作为 Intune 管理员，可创建和管理注册限制，这些限制可以定义注册接受 Intune 的管理的设备，其中包括：
- 设备数。
- 操作系统和版本。

可创建多个限制并将其应用于不同用户组。 可为不同限制设置[优先级顺序](#change-enrollment-restriction-priority)。

>[!NOTE]
>注册限制不是安全功能。 遭到入侵的设备可能会误报字符。 这些限制是针对非恶意用户的最合适的障碍。

可创建的特定注册限制包括：

- 最大设备注册数。
- 可注册的设备平台：
  - Android 设备管理员
  - Android Enterprise 工作配置文件
  - iOS/iPadOS
  - macOS
  - Windows
  - Windows Mobile
- 适用于 iOS/iPadOS、Android 设备管理员、Android Enterprise 工作配置文件、Windows 和 Windows Mobile 的平台操作系统版本。 （仅可使用 Windows 10 版本。 如果允许 Windows 8.1，请将此处留空。）
  - 最低版本。
  - 最高版本。
- 限制[个人拥有的设备](device-enrollment.md#bring-your-own-device)（仅限 iOS、Android 设备管理员、Android Enterprise 工作配置文件、macOS、Windows 和 Windows Mobile）。

## <a name="default-restrictions"></a>默认限制

为设备类型和设备限制注册限制自动提供默认限制。 更改默认选项。 默认限制适用于所有用户和无用户注册。 可通过创建优先级更高的新限制来替代这些默认值。

## <a name="create-a-device-type-restriction"></a>创建设备类型限制

1. 登录 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > “设备” > “注册限制” > “创建限制” > “设备类型限制”   。
2. 在“基本信息”页上，为限制提供名称和可选说明  。
3. 选择“下一步”，转到“平台设置”页。
4. 在“平台”中，对想要此限制允许的平台选择“允许”。
    ![选择平台设置的屏幕截图](./media/enrollment-restrictions-set/choose-platform-settings.png)
5. 在“版本”中，选择想要允许的平台支持的最低版本和最高版本。 对于 iOS 和 Android，版本限制仅适用于向公司门户注册的设备。
     支持的版本格式包括：
    - Android 设备管理员和 Android Enterprise 工作配置文件支持 major.minor.rev.build。
    - iOS/iPadOS 支持 major.minor.rev。操作系统版本不会应用于使用设备注册计划、Apple School Manager 或 Apple Configurator 应用注册的 Apple 设备。
    - Windows 仅对 Windows 10 支持 major.minor.build.rev。
    
    > [!IMPORTANT]
    > Android Enterprise（工作配置文件）和 Android 设备管理员平台具有以下行为：
    > - 如果两个平台都允许用于同一组，则如果用户的设备支持工作配置文件，则用户将使用该工作配置文件注册，否则他们将注册为 DA。 
    > - 如果两个平台都允许用于一个组，且针对特定非重叠版本进行了改进，那么用户将收到为其 OS 版本定义的注册流。 
    > - 如果两个平台都是允许的，但阻止同时用于相同的版本，那么在具有受阻止版本的设备上，将按 Android 设备管理员注册流程注册用户，然后阻止其注册并提示其注销。 
    >
    > 值得注意的是，除非在 Android 中完成了适当的先决条件，否则工作配置文件或设备管理员注册都无法成功。 
    
   > [!Note]
   > Windows 10 注册过程中不提供修订号，因此对于实例，如果输入 10.0.17134.100 而设备是 10.0.17134.174，则在注册过程中将阻止该实例。

6. 在“个人拥有”中，对想要允许作为个人拥有的设备的平台选择“允许”。
7. 在“设备制造商”下，输入要阻止的以逗号分隔的制造商列表。
8. 选择“下一步”，转到“作用域标记”页。
9. 在“作用域标记”页上，可选择添加要应用到此限制的作用域标记。 若要详细了解作用域标记，请参阅[将基于角色的访问控制和作用域标记用于分布式 IT](../fundamentals/scope-tags.md)。 使用具有注册限制的作用域标记时，用户只能对具有作用域的策略重新排序。 而且，他们只能对具有作用域的策略位置重新排序。 用户可以看到每个策略的真实优先级编号。 作用域的用户可以判断其策略的相对优先级，即使他们看不到所有其他策略。
10. 选择“下一步”，转到“分配”页。
11. 选择“选择要包含的组”，然后使用搜索框找到想要此限制包含的组。 限制仅适用于它分配到的组。 如果连一个组都没有分配限制，则不会产生任何影响。 然后选取“选择”。 
    ![选择平台设置的屏幕截图](./media/enrollment-restrictions-set/select-groups.png)
12. 选择“下一步”，以转到“查看 + 创建”页。
13. 选择“创建”以创建限制。
14. 使用高于默认值的优先级创建新限制。 可[更改优先级](#change-enrollment-restriction-priority)。


## <a name="create-a-device-limit-restriction"></a>创建设备限制

1. 登录 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > “设备” > “注册限制” > “创建限制” > “设备限制”   。
2. 在“基本信息”页上，为限制提供名称和可选说明  。
3. 选择“下一步”，转到“设备限制”页。
4. 对于“设备限制”，选择用户可以注册的最大设备数量。
    ![选择设备限制的屏幕截图](./media/enrollment-restrictions-set/choose-device-limit.png)
5. 选择“下一步”，转到“作用域标记”页。
6. 在“作用域标记”页上，可选择添加要应用到此限制的作用域标记。 若要详细了解作用域标记，请参阅[将基于角色的访问控制和作用域标记用于分布式 IT](../fundamentals/scope-tags.md)。 使用具有注册限制的作用域标记时，用户只能对具有作用域的策略重新排序。 而且，他们只能对具有作用域的策略位置重新排序。 用户可以看到每个策略的真实优先级编号。 作用域的用户可以判断其策略的相对优先级，即使他们看不到所有其他策略。
7. 选择“下一步”，转到“分配”页。
8. 选择“选择要包含的组”，然后使用搜索框找到想要此限制包含的组。 限制仅适用于它分配到的组。 如果连一个组都没有分配限制，则不会产生任何影响。 然后选取“选择”。 
    ![选择组的屏幕截图](./media/enrollment-restrictions-set/select-groups-device-limit.png)
9. 选择“下一步”，以转到“查看 + 创建”页。
10. 选择“创建”以创建限制。
11. 使用高于默认值的优先级创建新限制。 可[更改优先级](#change-enrollment-restriction-priority)。

在 BYOD 注册期间，用户会看到一条通知，告知他们何时达到了已注册的设备限制。 例如，在 iOS 上：

![iOS 设备限制通知](./media/enrollment-restrictions-set/enrollment-restrictions-ios-set-limit-notification.png)

> [!IMPORTANT]
> 设备限制不适用于以下 Windows 注册类型：
> - 共同托管的注册
> - GPO 注册
> - 加入 Azure Active Directory 的注册
> - 加入 Bulk Active Directory 的注册
> - Autopilot 注册
> - 设备注册管理员注册
>
> 不对这些注册类型强制执行设备限制，因为它们被视为共享设备方案。
> 可以在 [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal#configure-device-settings) 中为这些注册类型设置硬性限制。


## <a name="change-enrollment-restrictions"></a>更改注册限制

通过执行以下步骤可更改注册限制的设置。 这些限制不会影响已注册的设备。 无法使用此功能阻止注册了 [Intune PC 代理](../fundamentals/manage-windows-pcs-with-microsoft-intune.md)的设备。

1. 登录 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > “设备” > “注册限制” > 选择要更改的限制 >“属性”  。
2. 选择要更改的设置旁边的“编辑”。
3. 在“编辑”页上，根据需要进行更改，继续转到“查看 + 保存”页，然后选择“保存”。


## <a name="blocking-personal-android-devices"></a>阻止个人 Android 设备
- 如果阻止个人拥有的 Android 设备管理员设备进行注册，个人拥有的 Android Enterprise 工作配置文件设备仍可注册。
- 默认情况下，Android Enterprise 工作配置文件设备的设置与 Android 设备管理员设备的设置相同。 更改 Android Enterprise 工作配置文件或 Android 设备管理员设置后，将不再如此。
- 如果阻止个人 Android Enterprise 工作配置文件注册，那么仅公司拥有的 Android 设备可使用 Android Enterprise 工作配置文件注册。

## <a name="blocking-personal-windows-devices"></a>阻止个人 Windows 设备
如果阻止个人 Windows 设备注册，Intune 将进行检查以确保每个新 Windows 注册请求都已授权为企业注册。 将阻止未经授权的注册。

如果符合以下条件，则视为已授权为 Windows 企业注册：
- 注册用户使用的是[设备注册管理员帐户]( device-enrollment-manager-enroll.md)。
- 设备通过 [Windows Autopilot](enrollment-autopilot.md) 进行注册。
- 该设备已在 Windows Autopilot 中注册，但不是 Windows 设置中的仅 MDM 注册选项。
- 设备的 IMEI 号在“设备注册” > “[公司设备标识符](corporate-identifiers-add.md)”中列出 。
- 设备通过[批量预配包](windows-bulk-enroll.md)进行注册。
- 设备通过 GPO 或[从 Configuration Manager 自动注册以执行共同管理](https://docs.microsoft.com/configmgr/comanage/quickstart-paths#bkmk_path1)进行注册。
 
以下注册被 Intune 标记为企业。 但由于它们不提供 Intune 管理员每设备控制，因此将被阻止：
- 通过 [Windows 设置过程中的 Azure Active Directory 加入](https://docs.microsoft.com/azure/active-directory/device-management-azuread-joined-devices-frx)实现的[自动 MDM 注册](windows-enroll.md#enable-windows-10-automatic-enrollment)\*。
- 通过 [Windows 设置中的 Azure Active Directory 加入](https://docs.microsoft.com/azure/active-directory/user-help/user-help-register-device-on-network)实现的[自动 MDM 注册](windows-enroll.md#enable-windows-10-automatic-enrollment)*。
 
以下个人注册方法也将被阻止：
- 通过[从 Windows 设置中添加工作帐户](https://docs.microsoft.com/azure/active-directory/user-help/user-help-join-device-on-network)实现的[自动 MDM 注册](windows-enroll.md#enable-windows-10-automatic-enrollment)\*。
- 通过 Windows 设置中的[仅 MDM 注册]( https://docs.microsoft.com/windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device)选项。

\* 如果通过 Autopilot 注册，则不会受到阻止。


## <a name="blocking-personal-iosipados-devices"></a>阻止个人 iOS/iPadOS 设备
默认情况下，Intune 将 iOS/iPadOS 设备分类为个人拥有的设备。 若要分类为公司拥有的设备，iOS/iPadOS 设备必须满足以下条件之一：
- [已使用序列号注册](corporate-identifiers-add.md)。
- 已使用自动设备注册（以前称为设备注册计划）注册


## <a name="change-enrollment-restriction-priority"></a>更改注册限制优先级

当用户在分配有限制的多个组中时，则使用优先级。 用户仅遵循其所在组分配到的最高优先级的限制。 例如，Joe 位于优先级为 5 的限制的 A 组，也位于优先级为 2 的限制的 B 组。 Joe 仅受优先级为 2 的限制约束。

创建限制时，将其添加到默认值正上方的列表中。

设备注册同时包括设备类型和设备限制的默认限制。 这两个限制应用于所有用户，除非由更高优先级的限制替代。

>[!NOTE]
>用户受注册限制约束。 在非用户驱动的注册场景（例如 Windows Autopilot 自部署模式或白手套预配）中，仅实施默认优先级限制（针对“所有用户”）。


可更改任何非默认限制的优先级。

1. 登录到 Azure 门户。
2. 选择“更多服务”，搜索“Intune”，然后选择“Intune”  。
3. 选择“设备注册” > “注册限制” 。
4. 将鼠标悬停在优先级列表中的限制上。
5. 使用三个垂直点，将优先级拖到列表中的所需位置。
