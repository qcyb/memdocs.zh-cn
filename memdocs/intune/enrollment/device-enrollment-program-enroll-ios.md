---
title: 注册 iOS/iPadOS 设备 - 自动设备注册
titleSuffix: Microsoft Intune
description: 了解如何使用“自动设备注册”注册公司拥有的 iOS/iPadOS 设备。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/04/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7ddbf360-0c61-11e8-ba89-0ed5f89f718b
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8fe0b1748a40858bca55cc66b250c96725bfd9f1
ms.sourcegitcommit: 411e9d93cbafc7585f5a0f9a05097fe589de804f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/24/2020
ms.locfileid: "85332870"
---
# <a name="automatically-enroll-iosipados-devices-with-apples-automated-device-enrollment"></a>通过 Apple 自动设备注册自动注册 iOS/iPadOS 设备

> [!IMPORTANT]
> 最近，Apple 从使用 Apple 设备注册计划 (DEP) 改为了使用 Apple 自动设备注册 (ADE)。 Intune 正在更新 Intune 用户界面以反映此情况。 在此类更改完成之前，Intune 门户中将继续显示设备注册计划。 无论在何处显示，它现在使用的都是自动设备注册。

可以设置 Intune 以注册通过 Apple [自动设备注册 (ADE)](https://deploy.apple.com) 购买的 iOS/iPadOS 设备。 借助自动设备注册，可以在不接触设备的情况下注册大量设备。 iPhone、iPad 和 MacBook 等设备可以直接寄送给用户。 用户打开设备时，包含 Apple 产品典型现成体验的“设置助理”将运行预先配置的设置，设备将注册以便进行管理。

若要启用 ADE，请使用 Intune 和 [Apple Business Manager (ABM)](https://business.apple.com/) 或 [Apple School Manager (ASM)](https://school.apple.com/) 门户。 需要序列号列表或购买订单编号，这样才能将设备分配到 Intune 以便在任一 Apple 门户中进行管理。 在 Intune 中创建 ADE 注册配置文件，这些配置文件包含注册过程中应用于设备的设置。 ADE 无法用于[设备注册管理员](device-enrollment-manager-enroll.md)帐户。

> [!NOTE]
> ADE 设置最终用户不一定能删除的设备配置。 因此，在[迁移到 ADE](../fundamentals/migration-guide-considerations.md) 之前，必须擦除设备，使其返回到全新状态。

## <a name="automated-device-enrollment-and-the-company-portal"></a>自动设备注册和公司门户

ADE 注册与 App Store 版公司门户应用不兼容。 可以授权用户访问 ADE 设备上的公司门户应用。 你可能希望提供此访问权限，让用户选择他们想要在其设备上使用的公司应用，或使用新式验证完成注册过程。 

若要允许在注册期间使用新式验证，请使用 ADE 配置文件中的“使用 VPP 安装公司门户”（VPP 即批量购买计划）将应用推送到设备。 有关详细信息，请参阅[通过 Apple ADE 自动注册 iOS/iPadOS 设备](device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile)。

若要允许公司门户自动更新，并在已注册到 ADE 的设备上提供公司门户应用，请通过 Intune 将公司门户应用部署为已应用[应用程序配置策略](../apps/app-configuration-policies-use-ios.md)的必需批量购买计划 (VPP) 应用。

## <a name="what-is-supervised-mode"></a>受监督模式简介

Apple 在 iOS/iPadOS 5 中引入了受监督模式。 可对处于监督模式的 iOS/iPadOS 设备进行更多管理和控制，例如阻止屏幕捕获和阻止从 App Store 安装应用。 因此，这种模式对企业拥有的设备特别有用。 在 ADE 中，Intune 支持将设备配置为受监督模式。

在 iOS/iPadOS 11 中，已弃用对未受监督的 ADE 设备的支持。 在 iOS/iPadOS 11 和更高版本中，应始终对 ADE 配置的设备进行监督。 在 iOS/iPadOS 13.0 及更高版本中，将忽略 ADE“is_supervised”标志。 在通过自动设备注册进行注册后，具有 13.0 及更高版本的所有 iOS/iPadOS 设备都将自动受到监视。 

<!--
**Steps to enable enrollment programs from Apple**
1. [Get an Apple DEP token and assign devices](#get-the-apple-dep-token)
2. [Create an enrollment profile](#create-an-apple-enrollment-profile)
3. [Synchronize DEP-managed devices](#sync-managed-device)
4. [Assign DEP profile to devices](#assign-an-enrollment-profile-to-devices)
5. [Distribute devices to users](#end-user-experience-with-managed-devices)
-->
## <a name="prerequisites"></a>必备条件
- 在 [Apple 的 ADE](https://deploy.apple.com) 中购买的设备
- [移动设备管理 (MDM) 机构](../fundamentals/mdm-authority-set.md)
- [Apple MDM Push Certificate](apple-mdm-push-certificate-get.md)

## <a name="supported-volume"></a>支持的卷

- 每令牌的最大注册配置文件数：1,000  
- 每配置文件的最大自动设备注册设备数：无限制（只要在每令牌的最大设备数范围内）
- 每 Intune 帐户的最大自动设备注册令牌数：2,000
- 每令牌的最大自动设备注册设备数：第一次同步的限制为 75,000-80,000 台设备。 Intune 将继续与 ABM 或 ASM 同步，每 12 小时签入一次，以便每次再添加 80,000 台设备。 手动同步也会再添加 80,000 台设备。 同步将继续进行，并且设备将继续以 75,000-80,000 台设备为单位从 ABM/ASM 批量同步到 Intune。 

## <a name="get-an-apple-ade-token"></a>获取 Apple ADE 令牌

必须先从 Apple 获得 ADE 令牌 (.p7m) 文件，然后才能通过 ADE 注册 iOS/iPadOS 设备。 此令牌允许 Intune 同步有关公司所拥有的 ADE 设备的信息。 还允许 Intune 将注册配置文件上传至 Apple，并向设备分配这些配置文件。

可以使用 [Apple Business Manager (ABM)](https://business.apple.com/) 或 [Apple School Manager (ASM)](https://school.apple.com/) 门户来创建令牌。 还可以使用 ABM/ASM 门户将设备分配到 Intune 进行管理。

> [!NOTE]
> 如果在迁移到 Azure 前从 Intune 经典门户删除了令牌，Intune 可能会还原已删除的 Apple ADE 令牌。 可以从 Azure 门户再次删除 ADE 令牌。

### <a name="step-1-download-the-intune-public-key-certificate-required-to-create-the-token"></a>步骤 1。 下载创建令牌所需的 Intune 公钥证书。

1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“设备” > “iOS/iPadOS” > “iOS/iPadOS 注册”  。

    ![获取注册计划令牌。](./media/device-enrollment-program-enroll-ios/ios-enroll.png)

2. 选择“注册计划令牌” > “添加” 。

3. 选择“我同意”，为 Microsoft 授予向 Apple 发送用户和设备信息的权限。

   > [!NOTE]
   > 完成步骤 2 以下载 Intune 公钥证书后，请不要关闭向导或离开此页面。 这样做会令已下载的证书失效，导致你需要再次重复此过程。 如果遇到这种情况，你通常会注意到“审阅 + 创建”选项卡上的“创建”按钮灰显，你无法完成此过程。

   ![Apple 证书工作区中用于下载公钥的“注册计划令牌”窗格的屏幕截图。](./media/device-enrollment-program-enroll-ios/add-enrollment-program-token-pane.png)

4. 选择“下载公钥”，将加密密钥 (.pem) 文件下载到本地并保存。 .pem 文件用于从 Apple 门户请求信任关系证书。


### <a name="step-2-use-your-key-to-download-a-token-from-apple"></a>步骤 2。 使用密钥从 Apple 下载令牌。

1. 选择“通过 Apple Business Manager 创建令牌”，打开 Apple 商业门户，并使用公司 Apple ID 登录。 可使用此 Apple ID 续订 ADE 令牌。
2. 在 Apple [商业门户](https://business.apple.com)中，对“设备注册计划”选择“开始” 。

3. 在“管理服务器”页上，选择“添加 MDM 服务器”。
4. 输入“MDM 服务器名称”，然后选择“下一步”。 服务器名称供参考，用于识别移动设备管理 (MDM) 服务器。 它不是 Microsoft Intune 服务器的名称或 URL。

5. “添加&lt;服务器名称&gt;”对话框随即打开，提示“上传公钥”。 选择“选择文件…” 以上传 .pem 文件，然后选择“下一步”。

6. 转到“部署计划”>“设备注册计划”>“管理设备”。&gt;&gt;
7. 在“选择设备方式”下，指定如何标识设备：
    - **序列号**
    - **订单号**
    - **上传 CSV 文件**。

   ![指定按序列号选择设备、将“选择操作”设置为“分配到服务器”并选择服务器名称的屏幕截图。](./media/device-enrollment-program-enroll-ios/enrollment-program-token-specify-serial.png)

8. 对于“选择操作”，选择“分配到服务器”，选择为 Microsoft Intune 指定的 &lt;服务器名称&gt;，然后选择“确定”  。 Apple 门户将指定的设备分配到 Intune 服务器以进行管理，然后显示“分配完成”。

   在 Apple 门户中，转到“部署计划”&gt;“设备注册计划”&gt;“查看分配历史记录”，以查看设备及其 MDM 服务器分配的列表。

### <a name="step-3-save-the-apple-id-used-to-create-this-token"></a>步骤 3. 保存用于创建此令牌的 Apple ID。

在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，提供 Apple ID 供将来参考。

![指定用来创建注册计划令牌的 Apple ID 并浏览到注册计划令牌的屏幕截图。](./media/device-enrollment-program-enroll-ios/image03.png)

### <a name="step-4-upload-your-token-and-choose-scope-tags"></a>步骤 4. 上传令牌并选择作用域标记。

1. 在“Apple 令牌”框中，浏览到证书 (.p7m) 文件，然后选择“打开”。
2. 如果要将[作用域标记](../fundamentals/scope-tags.md)应用于此 DEP 令牌，则选择“作用域 (标记)”，并选择所需的作用域标记。 应用于令牌的作用域标记将由添加到此令牌的配置文件和设备继承。
3. 选择“创建”。

使用 Push Certificate，Intune 可通过将策略推送到已注册的移动设备来注册和管理 iOS/iPadOS 设备。 Intune 会自动与 Apple 同步以查看你的注册计划帐户。

## <a name="create-an-apple-enrollment-profile"></a>创建 Apple 注册配置文件

安装令牌之后，接下来可为 ADE 设备创建注册配置文件。 设备注册配置文件定义注册时应用于设备组的设置。 每个 ADE 令牌限制为 100 个注册配置文件。

> [!NOTE]
> 如果 VPP 令牌没有足够的公司门户许可证，或令牌已到期，设备便会遭阻止。 当令牌即将过期或许可证不足时，Intune 将显示警报。
 

1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“设备” > “iOS/iPadOS” > “iOS/iPadOS 注册” > “注册计划令牌”   。
2. 选择令牌，再依次选择“配置文件” > “创建配置文件” > “iOS/iPadOS”  。

    ![“创建配置文件”的屏幕截图。](./media/device-enrollment-program-enroll-ios/image04.png)

3. 在“基本信息”页上，输入配置文件的“名称”和“说明”，以便于管理。 用户看不到这些详细信息。 

    ![配置文件名称和描述。](./media/device-enrollment-program-enroll-ios/image05.png)

4. 选择“下一步:设备管理设置”。

5. 对于“用户关联”，选择具有此配置文件的设备是否必须通过已分配的用户进行注册。
    - 通过用户关联进行注册 - 为属于用户且想要使用公司门户获取服务（如安装应用）的设备选择此选项。 如果使用的是 ADFS，且使用设置助理进行身份验证，则需要 [WS-Trust 1.3 用户名/混合终结点](https://technet.microsoft.com/library/adfs2-help-endpoints)[（了解更多）](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint)。

    - 不通过用户关联进行注册 - 为不属于单个用户的设备选择此选项。 为无需访问本地用户数据的设备和 Apple 共用的 iPad（商业版）设备选择此选项。 公司门户等应用将无法运行。

6. 如果选择“注册用户关联”，可以让用户通过公司门户（而不是 Apple 设置助理）进行身份验证。

    ![使用公司门户进行身份验证。](./media/device-enrollment-program-enroll-ios/authenticatewithcompanyportal.png)

    > [!NOTE]
    > 若要执行以下任何一项操作，请将“选择用户必须进行身份验证的位置”设置为“公司门户”。
    >    - 使用多重身份验证
    >    - 提示用户在首次登录时需要更改密码
    >    - 提示用户在注册期间重置过期的密码
    >
    > 使用 Apple 设置助理进行身份验证时，不支持执行这些操作。

7. 如果对“选择用户必须进行身份验证的位置”选择了“公司门户”，可以使用 VPP 令牌在设备上自动安装公司门户。 在这种情况下，用户无需提供 Apple ID。 要使用 VPP 令牌安装公司门户，请在“使用 VPP 安装公司门户”下选择一个令牌。 要求已将公司门户添加到 VPP 令牌中。 若要确保在注册后继续更新公司门户应用，请确保已在 Intune 中配置了应用部署（“Intune”>“客户端应用”）。 因此，用户交互不是必需的，你最有可能希望将公司门户作为 iOS/iPadOS VPP 应用，使之成为必需应用，并对分配使用设备授权。 请确保令牌没有过期，并且具有足够公司门户应用使用的设备许可证。 如果令牌到期或许可证用完，Intune 会改为安装 App Store 版公司门户，并提示输入 Apple ID。 

    > [!NOTE]
    > 如果将“选择用户必须进行身份验证的位置”设置为“公司门户”，请务必在将公司门户下载到 ADE 设备的最初 24 小时内执行设备注册流程。 否则，注册可能会失败，需要恢复出厂设置才能注册设备。
    
    ![使用 VPP 安装公司门户的屏幕截图。](./media/device-enrollment-program-enroll-ios/install-cp-with-vpp.png)

8. 如果对“选择用户必须进行身份验证的位置”选择了“设置助理”，但也想在设备上使用条件访问或部署公司应用，必须在设备上安装公司门户。 为此，请对“安装公司门户”选择“是”。  如果希望用户接收公司门户，而不需要在 App Store 中进行身份验证，请依次选择“使用 VPP 安装公司门户”和 VPP 令牌。 请确保令牌没有到期，并且有足够的设备许可证，可供正确部署公司门户应用。

9. 如果对“使用 VPP 安装公司门户”选择了令牌，可以在设置助理完成后，立即将设备锁定在单应用模式下（具体而言，即公司门户应用）。 针对“在身份验证前以单应用模式运行公司门户”，选择为“是”以设置此选项 。 要使用该设备，用户必须先使用公司门户登录以进行身份验证。

    锁定在单应用模式下的单台设备不支持多重身份验证。 这种限制的存在是因为，设备无法切换到其他应用来完成双重身份验证。 因此，若要在单应用模式设备上进行多重身份验证，必须在其他设备上进行双重身份验证。

    仅 iOS/iPadOS 11.3.1 及更高版本支持此功能。

   ![单应用模式的屏幕截图。](./media/device-enrollment-program-enroll-ios/single-app-mode.png)

10. 若要让使用此配置文件的设备受到监督，请对“已监督”选择“是”。

    ![“设备管理设置”屏幕截图。](./media/device-enrollment-program-enroll-ios/supervisedmode.png)

    “受监督”的设备会提供更多的管理选项，并且会默认禁用“激活锁”。 Microsoft 建议使用 ADE 作为监督模式启用机制，尤其是在部署大量 iOS/iPadOS 设备时。 Apple 共用的 iPad（商业版）设备必须受到监督。

    将通过两种方式通知用户他们的设备受到监督：

   - 锁定屏幕显示：“此 iPhone 由 Contoso 托管”。
   - “设置” > “常规” > “关于”屏幕显示：“此 iPhone 受到监督”。 Contoso 可以监视你的 Internet 流量并找到此设备。”

     > [!NOTE]
     > 不受监督的注册设备只能使用 Apple Configurator 重置为受监督。 以此方式重置设备需要使用 USB 线将 iOS/iPadOS 设备连接到 Mac。 有关详细信息，请参阅 [Apple Configurator 文档](http://help.apple.com/configurator/mac/2.3)。

11. 选择是否要对使用此配置文件的设备进行锁定注册。 “锁定注册”将禁用允许从“设置”菜单删除管理配置文件的 iOS/iPadOS 设置。 在设备注册之后，如果不擦除设备，就无法更改此设置。 此类设备必须将“受监督”管理模式设置为“是”。 

    > [!NOTE]
    > 在设备通过“锁定的注册”注册后，用户将无法在公司门户应用中使用“删除设备”或“恢复出厂设置”。 用户将无法使用这些选项。 用户也将无法在公司门户网站 (https://portal.manage.microsoft.com) 中删除设备。
    > 此外，如果 BYOD 设备转换为 Apple 自动设备注册设备，并通过已启用“锁定的注册”的配置文件进行注册，那将允许用户使用“删除设备”和“恢复出厂设置”30 天，30 天后这些选项将被禁用或不可用。 参考： https://help.apple.com/configurator/mac/2.8/#/cad99bc2a859 。

12. 如果选择了上面的“不通过用户关联进行注册”和“受监督”，则必须决定是否将这些设备配置为 [Apple 共用的 iPad（商业版）设备](https://support.apple.com/guide/mdm/shared-ipad-overview-cad7e2e0cf56/web) 。 对于“共用的 iPad”选择“是”，多个用户将能够登录到同一设备 。 这些用户将使用其管理式 Apple ID 和联合身份验证帐户或通过临时会话（即来宾帐户）进行身份验证。 此选项需要 iOS/iPadOS 13.4 或更高版本。

    如果选择将设备配置为 Apple 共用的 iPad（商业版）设备，则必须设置“缓存用户数上限”。 请将此值设置为希望使用“共用的 iPad”的用户数。 在 32 GB 或 64 GB 设备上最多可以缓存 24 个用户。 如果选择的数字非常小，则用户的数据在用户登录后可能需要一段时间才能缓存到设备。 如果选择的数字非常大，则用户可能没有足够的磁盘空间。  

    > [!NOTE]
    > 如果要设置 Apple 共用的 iPad（商业版），请设置以下内容： 
    > - “用户关联” = “不通过用户关联进行注册” 。 
    > - “受监督” = “是” 。 
    > - “共用的 iPad”=“是”。
    > 默认情况下，临时会话处于启用状态，允许用户登录到共用的 iPad，而无需管理式 Apple ID 帐户。 可通过配置 iOS/iPadOS 共用的 iPad [设备限制设置](../configuration/device-restrictions-ios.md)，来禁用“共用的 iPad”上的临时会话。  

13. 选择是否要让使用此配置文件的设备能够“与计算机同步”。 如果选择“通过证书允许 Apple Configurator”，则必须在“Apple Configurator 证书”下选择证书。

     > [!NOTE]
     > 如果将“与计算机同步”设置为“全部拒绝” ，则 iOS 和 iPadOS 设备上的端口将受到限制。 该端口只能用于充电，不能用于其他操作。 端口将被阻止使用 iTunes 或 Apple Configurator 2。
     如果“与计算机同步”设置为“通过证书允许 Apple Configurator”，请务必保存证书的本地副本，以供日后使用 。 你将无法更改已上传的副本，请务必保留此证书，以供日后使用。 若要从 macOS 设备或电脑连接到 iOS/iPadOS 设备，必须在连接到 iOS/iPadOS 设备的设备上安装相同的证书，该设备已使用此配置和证书注册到自动设备注册配置文件。

14. 如果在上一步中选择了“通过证书允许 Apple Configurator”，则选择要导入的“Apple Configurator 证书”。

15. 可以为设备指定命名格式，此格式在设备注册时和每次连续签入时自动应用。 若要创建命名模板，请在“应用设备名称模板”下选择“是”。 然后，在“设备名称模板”框中，输入要用于使用此配置文件的设备的名称模板。 可以指定包含设备类型和序列号的模板格式。 

16. 选择“下一步:设置助理的自定义项。

17. 在“设置助理的自定义项”页上，配置以下配置文件设置：![设置助理的自定义项](./media/device-enrollment-program-enroll-ios/setupassistantcustom.png)。


    | 部门设置 | 说明 |
    |---|---|
    | <strong>部门名称</strong> | 用户在激活过程中轻点“关于配置”时显示。 |
    |    <strong>部门电话</strong>     | 用户在激活过程中单击“需要帮助”按钮时显示。 |

    可以选择在用户设置期间隐藏设备上的“设置助理”屏幕。
    - 如果选择“隐藏”，设置期间将不会显示该屏幕。 设置设备之后，用户仍可以进入“设置”菜单来设置此功能。
    - 如果选择“显示”，设置期间将显示该屏幕。 用户有时可以跳过该屏幕，无需采取任何操作。 但是，他们可以稍后进入设备的“设置”菜单来设置此功能。 


    | 设置助理屏幕设置 | 如果选择“显示”，设置期间设备将... |
    |------------------------------------------|------------------------------------------|
    | <strong>密码</strong> | 提示用户输入密码。 对于不安全的设备，始终要求提供密码，除非以其他方式（如限制设备只能使用一个应用的展台模式）控制访问。 适用于 iOS/iPadOS 7.0 及更高版本。 |
    | <strong>位置服务</strong> | 提示用户输入位置。 适用于 macOS 10.11 及更高版本和 iOS/iPadOS 7.0 及更高版本。 |
    | <strong>还原</strong> | 显示“应用和数据”屏幕。 设置设备时，此屏幕为用户提供从 iCloud 备份还原或传输数据的选项。 适用于 macOS 10.9 及更高版本和 iOS/iPadOS 7.0 及更高版本。 |
    | <strong>iCloud 和 Apple ID</strong> | 让用户能够选择使用 Apple ID 登录并使用 iCloud。 适用于 macOS 10.9 及更高版本和 iOS/iPadOS 7.0 及更高版本。   |
    | <strong>条款和条件</strong> | 要求用户接受 Apple 的条款和条件。 适用于 macOS 10.9 及更高版本和 iOS/iPadOS 7.0 及更高版本。 |
    | <strong>Touch ID</strong> | 为用户提供设置设备的指纹识别的选项。 适用于 macOS 10.12.4 及更高版本和 iOS/iPadOS 8.1 及更高版本。 |
    | <strong>Apple Pay</strong> | 为用户提供在设备上设置 Apple Pay 的选项。 适用于 macOS 10.12.4 及更高版本和 iOS/iPadOS 7.0 及更高版本。 |
    | <strong>缩放</strong> | 设置设备时，为用户提供缩放显示内容的选项。 适用于 iOS/iPadOS 8.3 及更高版本。 |
    | <strong>Siri</strong> | 为用户提供设置 Siri 的选项。 适用于 macOS 10.12 及更高版本和 iOS/iPadOS 7.0 及更高版本。 |
    | <strong>诊断数据</strong> | 向用户显示“诊断”屏幕。 此屏幕为用户提供将诊断数据发送到 Apple 的选项。 适用于 macOS 10.9 及更高版本和 iOS/iPadOS 7.0 及更高版本。 |
    | <strong>显示色调</strong> | 为用户提供打开“显示色调”的选项。 适用于 macOS 10.13.6 及更高版本和 iOS/iPadOS 9.3.2 及更高版本。 |
    | <strong>隐私</strong> | 向用户展示“隐私”屏幕。 适用于 macOS 10.13.4 及更高版本和 iOS/iPadOS 11.3 及更高版本。 |
    | <strong>Android 迁移</strong> | 为用户提供从 Android 设备迁移数据的选项。 适用于 iOS/iPadOS 9.0 及更高版本。|
    | <strong>iMessage 和 FaceTime</strong> | 让用户能够选择设置 iMessage 和 FaceTime。 适用于 iOS/iPadOS 9.0 及更高版本。 |
    | <strong>载入</strong> | 显示用户教育的载入信息屏幕，如“封面页”以及“多任务和控制中心”。 适用于 iOS/iPadOS 11.0 及更高版本。 |
    | <strong>监视迁移</strong> | 为用户提供从监视设备迁移数据的选项。 适用于 iOS/iPadOS 11.0 及更高版本。|
    | <strong>屏幕使用时间</strong> | 显示“屏幕使用时间”屏幕。 适用于 macOS 10.15 及更高版本和 iOS/iPadOS 12.0 及更高版本。 |
    | <strong>软件更新</strong> | 显示强制“软件更新”屏幕。 适用于 iOS/iPadOS 12.0 及更高版本。 |
    | <strong>SIM 设置</strong> | 为用户提供添加移动电话计划的选项。 适用于 iOS/iPadOS 12.0 及更高版本。 |
    | <strong>外观</strong> | 向用户显示“外观”屏幕。 适用于 macOS 10.14 及更高版本和 iOS/iPadOS 13.0 及更高版本。 |
    | <strong>Express 语言</strong>| 向用户显示“Express 语言”屏幕。 |
    | <strong>首选语言</strong> | 让用户能够选择“首选语言”。 |
    | <strong>设备间迁移</strong> | 让用户能够将数据从旧设备迁移到此设备。 适用于 iOS/iPadOS 13.0 及更高版本。 |
    | <strong>注册</strong> | 向用户显示注册屏幕。 适用于 macOS 10.9 及更高版本。 |
    | <strong>FileVault</strong> | 向用户显示 FileVault 2 加密屏幕。 适用于 macOS 10.10 及更高版本。 |
    | <strong>iCloud 诊断</strong> | 向用户显示“iCloud 分析”屏幕。 适用于 macOS 10.12.4 及更高版本。 |
    | <strong>iCloud 存储</strong> | 向用户显示“iCloud 文档和桌面”屏幕。 适用于 macOS 10.13.4 及更高版本。 |
    

18. 选择“下一步”，以转到“查看 + 创建”页。

19. 若要保存配置文件，则选择“创建”。

### <a name="dynamic-groups-in-azure-active-directory"></a>Azure Active Directory 中的动态组

可使用注册“名称”字段在 Azure Active Directory 中创建动态组。 有关详细信息，请参阅 [Azure Active Directory 动态组](/azure/active-directory/users-groups-roles/groups-dynamic-membership)。

可以使用配置文件名称来定义 [enrollmentProfileName 参数](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices)，以向设备分配此注册配置文件。

为了在具有用户关联的 ADE 设备上实现最快的策略传递，请确保注册用户在设备创建前是 AAD 用户组的成员。 

向注册配置文件分配动态组可能会导致在注册后向设备传递应用程序和策略时出现一些延迟。


## <a name="sync-managed-devices"></a>同步托管设备
Intune 已拥有管理设备的权限，现在可以将 Intune 与 Apple 同步，以在 Azure 门户的 Intune 中查看托管设备。

1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“设备” > “iOS/iPadOS” > “iOS/iPadOS 注册” > “注册计划令牌”   。

2. 从列表中选择一个令牌，再选择“设备”>“同步” 。![“注册计划设备”节点和“同步”链接的屏幕截图。](./media/device-enrollment-program-enroll-ios/image06.png)

   为了遵守 Apple 有关可接受注册计划流量的条款，Intune 规定了以下限制：
   - 每七天只能运行一次完全同步。 完全同步时，Intune 会提取分配给连接到 Intune 的 Apple MDM 服务器的完整更新序列号列表。 如果 ADE 设备已从 Intune 门户中删除，应在 ADE 门户中从 Apple MDM 服务器取消对它的分配。 如果未取消分配它，那么它不会重新导入 Intune，除非完全同步运行。   
   - 每 12 小时自动运行一次同步。 用户也可以单击“同步”按钮（不能超过 15 分钟一次）运行同步。 所有同步请求都在 15 分钟内完成。 在同步完成前，“同步”按钮处于禁用状态。 此同步将刷新现有设备状态并导入分配到 Apple MDM 服务器的新设备。   


## <a name="assign-an-enrollment-profile-to-devices"></a>将注册配置文件分配到设备
必须先向设备分配注册计划配置文件才能注册他们。

>[!NOTE]
>还可以从“Apple 序列号”边栏选项卡将序列号分配给配置文件。

1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“设备” > “iOS/iPadOS” > “iOS/iPadOS 注册” > “注册计划令牌”> 从列表中选择令牌   。
2. 选择“设备”> 在列表中选择设备 >“分配配置文件”。 
3. 在“分配配置文件”下，为设备选择配置文件，然后选择“分配” 。

### <a name="assign-a-default-profile"></a>分配默认配置文件

可以选择一个默认配置文件，以将其应用于所有使用特定令牌注册的设备。

1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“设备” > “iOS/iPadOS” > “iOS/iPadOS 注册” > “注册计划令牌”> 从列表中选择令牌   。
2. 选择“设置默认配置文件”，在下拉列表中选择配置文件，然后选择“保存”。  此配置文件将应用于所有使用此令牌注册的设备。

## <a name="distribute-devices"></a>分发设备
你已启用 Apple 和 Intune 之间的管理和同步，并分配了配置文件以允许 ADE 设备注册。 现在可以将设备分配给用户。 具有用户关联的设备需要每个用户都分配有 Intune 许可证。 没有用户关联的设备需要设备许可证。 已激活设备只有在擦除后，才能应用注册配置文件。

请参阅[通过设备注册计划在 Intune 中注册 iOS/iPadOS 设备](../user-help/enroll-your-device-dep-ios.md)。

## <a name="renew-an-ade-token"></a>续订 ADE 令牌  

> [!NOTE]
> 除了每年续订一次 ADE 令牌之外，还需要在以下情况下在 Intune 和 Apple Business Manager 中续订注册计划令牌：托管的 Apple ID 密码对在 Apple Business Manager 中设置令牌的用户或离开 Apple Business Manager 组织的用户发生更改。

1. 转到 business.apple.com。  
2. 在“管理服务器”下，选择与想要续订的令牌文件相关的 MDM 服务器。
3. 选择“生成新令牌”。

    ![生成新令牌的屏幕截图。](./media/device-enrollment-program-enroll-ios/generatenewtoken.png)

4. 选择“服务器令牌”。  
5. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“设备” > “iOS/iPadOS” > “iOS/iPadOS 注册” > “注册计划令牌”> 选择令牌   。
    ![注册程序令牌屏幕截图](./media/device-enrollment-program-enroll-ios/enrollmentprogramtokens.png)

6. 选择“续订令牌”，然后输入用于创建原始令牌的 Apple ID。  
    ![生成新令牌的屏幕截图。](./media/device-enrollment-program-enroll-ios/renewtoken.png)

7. 选择“下一步”，转到“作用域标记”页，并根据需要分配作用域标记 。

8. 选择“下一步”并上传新下载的令牌。  
9. 选择“续订令牌”。 你将看到令牌已续订的确认消息。   
    ![确认消息屏幕截图。](./media/device-enrollment-program-enroll-ios/confirmation.png)

## <a name="delete-an-ade-token-from-intune"></a>从 Intune 中删除 ADE 令牌

只要满足以下条件，即可从 Intune 中删除注册配置文件令牌：
- 未向令牌分配任何设备
- 未向默认配置文件分配任何设备

1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)内，依次选择“设备” > “iOS/macOS” > “iOS/macOS 注册” > “注册计划令牌”> 选择令牌 >“设备”。
2. 删除向令牌分配的所有设备。
3. 依次转到“设备” > “iOS/macOS” > “iOS/macOS 注册” > “注册计划令牌”> 选择令牌 >“配置文件”。
4. 删除默认配置文件（若有）。
5. 依次转到“设备” > “iOS/macOS” > “iOS/macOS 注册” > “注册计划令牌”> 选择令牌 >“删除”。
