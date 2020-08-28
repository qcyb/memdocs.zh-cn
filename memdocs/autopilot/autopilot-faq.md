---
title: Windows Autopilot 常见问题
ms.reviewer: This topic provides OEMs, partners, administrators, and end users with answers to some frequently asked questions about deploying Windows 10 with Windows Autopilot.
manager: laurawi
description: Windows Autopilot 的支持信息
keywords: mdm, 设置, windows, windows 10, oobe, 管理, 部署, autopilot, ztd, 零接触, 合作伙伴, msfb, intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: low
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: af7b7f3a871683f7b75583292df5cb3d6e5de4c4
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993211"
---
# <a name="windows-autopilot-faq"></a>Windows Autopilot 常见问题

**适用于： Windows 10**

本文为 Oem、合作伙伴、管理员和最终用户提供有关通过 Windows Autopilot 部署 Windows 10 的常见问题的解答。 

本文末尾 [提供了本文中使用的缩写](#glossary) 。


## <a name="microsoft-partner-center"></a>Microsoft 合作伙伴中心

| 问题 | Answer |
| --- | --- |
| 在合作伙伴中心，是否需要随每个设备文件上传一起提供租户 ID？ 是否需要允许企业客户访问其设备 Microsoft Store for Business (MSfB) ？     | 不行。 提供租户 ID 是合作伙伴中心中的一次性条目，可以在将来的设备上传时重复使用。 |
| 客户或租户知道他们的设备已准备好在 MSfB 中声明了吗？    |  在伙伴中心完成设备文件上传后，租户可以在 MSfB 中看到可用于 Windows Autopilot 安装程序的设备。 OEM 需要通知租户访问 MSfB。 正在开发从 MSfB 到租户的 Autonotification。  |
| 客户如何授权 OEM 或渠道合作伙伴代表客户注册 Autopilot 设备？   |  在 OEM 或通道合作伙伴可以代表客户注册 Autopilot 设备之前，客户必须先向他们授予许可。  许可过程以 OEM 或渠道合作伙伴开始，向客户发送一个链接，该链接将客户定向到 MSfB 中的许可页。  有关详细信息，请参阅 [注册](registration-auth.md)。  |
|  如果业务客户在 MSfB 中注册了设备，并且以后希望使用合作伙伴中心) 云解决方案提供商 (CSP 来管理这些设备，是否存在任何限制？ | 设备将需要在 MSfB 中由业务客户删除，然后才能在合作伙伴中心上传和管理设备。 | 
| Windows Autopilot 是否支持删除选项以启用本地管理员帐户？    |  Windows Autopilot 不支持删除本地管理员帐户。 但是，它支持限制用户执行 Azure Active Directory (在 OOBE 中 Azure AD) 域加入标准帐户 (与管理员帐户默认) 。|
| 如何在合作伙伴中心测试 Windows Autopilot CSV 文件？    |  只有 CSP 合作伙伴有权访问合作伙伴中心门户。 如果你是 CSP，则可以创建一个销售代理用户帐户，该帐户有权访问用于测试文件的设备。 可以在合作伙伴中心完成此操作。 <br><br>有关详细信息，请参阅 [创建用户帐户和设置权限](https://msdn.microsoft.com/partner-center/create-user-accounts-and-set-permissions)。 |
|  是否需要成为 CSP 才能参与 Windows Autopilot？ | 这对于顶级批量 Oem 不是必需的，因为它们可以使用 OEM 直接 API。  选择使用 MPC 注册设备的所有其他人必须变成 Csp 才能访问 MPC。  |
| 在 Windows Autopilot 时，不同的 CSP 级别是否具有相同的功能？   |  对于 Windows Autopilot，有三种不同类型的 Csp，每种类型都具有不同的授权级别和访问权限： <br><br>1. <b>直接 CSP</b>：获取客户用于注册设备的直接授权。 <br><br>2. <b>间接 CSP 提供程序</b>：获取通过其 CSP 分销商合作伙伴与客户的关系注册设备的隐式权限。  间接 CSP 提供商通过 Microsoft 合作伙伴中心注册设备。 <br><br>3. <b>间接 CSP 分销商</b>：直接授权客户注册设备。  同时，其间接 CSP 提供商伙伴也会获得授权，这意味着间接提供商或间接经销商可以为客户注册设备。  但是，间接 CSP 分销商必须通过 MPC UI 注册设备， (手动) 上传 CSV 文件，而间接 CSP 提供商可选择使用 MPC Api 注册设备。 |
| 是否有这样一种方式作为全球的单个 CSP 帐户？   |  不行。 CSP 销售区域依赖于 (AzureAD) 租户的位置。  CSP 合作伙伴只能出售或管理其租户与注册为 CSP 的合作伙伴位于同一 CSP 区域中的客户 (CSP 伙伴用于处理) 的租户的位置。 如果客户租户是在美国创建的，则只有在美国注册了 CSP 的合作伙伴才能与此客户建立分销商关系。 与 Autopilot & Intune 相关，最终用户或设备所在的位置并不重要。 位于德国的员工使用的设备可以使用在美国租户中创建的 Autopilot 配置文件进行注册，并可由美国的 Intune 服务实例进行管理。 德国的用户还将在 US AzureAD 实例中进行身份验证。 如果合作伙伴希望全局管理客户，则他们需要全局存在。 它们必须在每个需要在其上开展业务的 CSP 销售区域中注册多个 CSP。 也无法创建有权访问所有 CSP 租户的用户帐户;此方案将转换为 CSP 管理代理的18个用户帐户，以便能够管理世界各地的所有客户。 总的来说，用户和设备的位置并不重要。 客户租户的位置。 交叉边框设备注册并不是问题;问题是通过 CSP 进行交叉边框销售。 |

## <a name="manufacturing"></a>制造

| 问题 | Answer |
| --- | --- |
| 对于客户配置设置，需要在工厂 OS 映像中进行哪些更改？     |不需要对工厂地面进行任何更改即可启用 Windows Autopilot 部署。  |
| 哪个版本的 OA3 工具满足 Windows Autopilot 部署要求？     | Windows Autopilot 可以使用任何版本的 OA3 工具。 建议使用受支持版本的 Windows 10 半半年通道生成4K 硬件哈希。    |
|  订购订单时，客户是否需要确定是否需要使用或不使用 Windows Autopilot 选项？   | 是的，如果他们想要 Windows Autopilot，他们将需要 Windows 10 半年版频道的受支持版本。 此外，他们还希望接收 CSV 文件或将文件上传 (也就是说，注册) 代表他们完成注册。    |
|  OEM 是否需要管理或收集来自客户的任何自定义图像文件，并向 Microsoft 执行任何图像上传？   | 无更改，Oem 只是将 CBRs 照常发送到 Microsoft。 不会向 Microsoft 发送任何图像以启用 Windows Autopilot。  Windows Autopilot 仅自定义 OOBE，并允许 (禁用管理员帐户的策略配置，例如) 。  |
|  从 Windows 8 升级到 Windows 10 的客户是否有任何影响？    | 设备必须运行受支持版本的 Windows 10 半年频道才能在 Windows Autopilot 部署中进行注册。 否则，不会产生任何影响。    |
| 对于具有4K 硬件哈希的现有 CBR 是否有任何更改？    | 不行。  |
| 需要从 OEM 向 Microsoft 发送哪些新信息？    | 无，除非 OEM 喜欢代表客户注册设备，在这种情况下，他们会使用 CSV 文件将设备 ID 上传到 Microsoft 合作伙伴中心，或使用 OEM 直接 API。  |
| 是否有针对 OEM 参与 Windows Autopilot 部署的合同或修正？    | 不行。  |

## <a name="csv-schema"></a>CSV 架构

| 问题 | Answer |
| --- | --- |
|  CSV 文件中是否可以使用逗号？ | 不行。   |
| 上传文件时，用户可以在合作伙伴中心或 MSfB 中看到哪些错误消息？    | 请参阅本指南中的 Microsoft Store for Business 部分。  |
| CSV 文件中可列出的设备数是否有限制？    | 是的，CSV 文件只能包含1000设备，才能应用到单个配置文件。 如果需要将超过1000台设备应用到配置文件，则需要通过多个 CSV 文件上传设备。    |
| 对于 OEM 应如何向其客户提供 CSV 文件，Microsoft 是否有任何建议？    |  建议通过 MPC、MSfB 或 Intune) 向企业客户发送 Autopilot 设备，以便将其 Windows (设备自行注册，从而对其进行加密。   |


## <a name="hardware-hash"></a>硬件哈希

| 问题 | Answer |
| --- | --- |
| 必须由 OEM 提交的每个硬件哈希都包含 SMBIOS UUID (全局唯一标识符) 、MAC (媒体访问控制) 地址和唯一磁盘序列号 (如果使用 Windows 10 OEM 激活3.0 工具) ？    | 是。 由于 Windows Autopilot 基于唯一标识应用于云配置的设备的功能，因此提交满足所述要求的硬件哈希至关重要。   |
| 需要硬件哈希详细信息中的 SMBIOS UUID、MAC 地址和磁盘序列号的原因是什么？    | 对于创建硬件哈希，这些字段是在添加或删除设备的一部分时标识设备所需的字段。 由于我们没有适用于 Windows 设备的唯一标识符，因此，这是用于识别设备的最佳逻辑。    |
| OA3 硬件哈希、4K 硬件哈希和 Windows Autopilot 硬件哈希之间有何区别？    | 无。  对于同一项，它们的名称是不同的。  OA3 工具输出称为 OA3 哈希，大小为4K，这可用于 Windows Autopilot 部署方案。 注意：使用不受支持的旧版 Windows 版本 OA3Tool 时，会获得不同大小的哈希，而不能用于 Windows Autopilot 部署。  |
|   (网络接口控制器) 和磁盘的 NIC 的部件更换和修复是什么想法？ 硬件哈希是否会无效？   |  是。  如果替换部分，则需要收集新的硬件哈希，但它依赖于所替换的内容和部件的特征。 例如，如果你替换 TPM 或主板，则它是一个新设备，你必须具有新的硬件哈希。 如果替换一个网卡，则它可能不是新设备，并且设备将使用旧的硬件哈希。  但是，最佳做法是，应假定旧的硬件哈希无效，并在硬件更改后获取新的硬件哈希。 替换部件时建议使用此建议。 |

## <a name="motherboard-replacement"></a>主板更换

| 问题 | Answer |
| --- | --- |
| Autopilot 如何处理主板更换方案？  |  对于 Autopilot 的范围，主板更换已过时。 任何修复或提供的、用于改变标识 Windows Autopilot 设备的能力的设备都必须经历正常的 OOBE 过程，并手动选择正确的设置或应用自定义映像，就像今天的情况一样。  <br><br>若要在更换主板后对 Windows Autopilot 重复使用同一设备，需要从 Autopilot 取消注册设备，将主板替换为新的 4K HH 搜集，然后使用新的4K 硬件哈希 (或设备 ID) 重新注册。 <br><br>**注意**： oem 将不能使用 OEM 直接 api 来重新注册设备，因为 OEM 直接 api 只接受元组或 PKID。  在这种情况下，OEM 必须使用 CSV 文件将新的4K 硬件哈希信息发送给客户，并让客户使用 MSfB 或 Intune 重新注册设备。|

## <a name="smbios"></a>SMBIOS

| 问题 | Answer |
| --- | --- |
| 对 SMBIOS UUID 的任何特定要求？    | 它必须唯一，如 Windows 10 硬件要求中所指定。    |
| 在 SMBIOS 表中需要满足 Windows Autopilot 硬件哈希的要求是什么？    | 它必须满足所有 Windows 10 硬件要求。  可在 [此处](/previous-versions/windows/hardware/cert-program/windows-hardware-certification-requirements-for-client-and-server-systems)找到更多详细信息。    |
| 如果 SMBIOS 支持 UUID 和序列号，则是否足以让 OA3 工具生成硬件哈希？    | 不行。  以下 SMBIOS 字段至少需要使用唯一值填充： ProductKeyID SmbiosSystemManufacturer SmbiosSystemProductName SmbiosSystemSerialNumber SmbiosSkuNumber SmbiosSystemFamily MacAddress SmbiosUuid DiskSerialNumber TPM EkPub |

## <a name="technical-interface"></a>技术接口

| 问题 | Answer |
| --- | --- |
|  获取 MAC 地址和磁盘序列号的接口是什么？ OA 工具如何获取 MAC 和磁盘序列号？   | 从带有 StorageDeviceProperty/PropertyStandardQuery 的 IOCTL_STORAGE_QUERY_PROPERTY 中找到了磁盘序列号。   网络 MAC 地址从 OID_802_3_PERMANENT_ADDRESS IOCTL_NDIS_QUERY_GLOBAL_STATS。  但是，执行此操作的方法根据方案的不同而异。  |
| 跟进说明：如果在系统上安装了 2-3 Mac，则 OA 工具如何选择系统上的 MAC 地址和磁盘序列号，因为每个地址有多个实例？ 如果平台具有 LAN 和 WLAN，则会选择哪些 MAC？     |  简而言之，将使用所有可用值。  详细地说明，可能存在特定的使用规则。 系统磁盘序列号比其他可用磁盘更重要。 如果检测到可移动的网络接口，则不应使用这些接口。 LAN vs WLAN 应该不重要，因为这两者都将使用。  |

## <a name="the-end-user-experience"></a>最终用户体验

|问题|Answer|
|----|-----|
|如何实现知道我收到了 Autopilot 吗？|你可以知道收到 Windows Autopilot (如设备接收了配置但尚未应用它) 在跳过选择页面时 (如下面) 所示，并立即转到一般或自定义登录页面。|
|Windows Autopilot 不起作用，现在我该怎么办？| 用于帮助进行故障排除的问题和操作：是否跳过屏幕？   当配置为 "不到" 时，用户是否最终作为管理员使用？ 请记住，Azure AD 管理员将是本地管理员，而不考虑 Windows Autopilot 是否已配置为禁用本地管理员收集信息：运行 licensingdiag.exe 并将生成的 .cab (Cabinet) 文件发送到 AutopilotHelp@microsoft.com 。 如果可能，请从 Windows 性能记录器 (") 收集 ETL。 通常，在这种情况下，用户不会登录到正确的 Azure AD 租户，也不会创建本地用户帐户。  有关支持选项的完整列表，请参阅 [Windows Autopilot 支持](autopilot-support.md)。 |
| 如果管理员对现有配置文件进行更改，则所做的更改将在已分配到已部署的配置文件的设备上生效？ |不行。 Windows Autopilot 配置文件不在设备上。 它们是在 OOBE 期间下载的，应用时定义的设置。 然后，设备上会丢弃该配置文件。 如果设备已重置映像或重置，则新的配置文件设置将在下一次设备进入 OOBE 时生效。|
|如果设备未注册，或 IT 管理员在最终用户尝试自行部署之前未配置 Windows Autopilot，该体验是怎样的？ |如果设备未注册，则不会收到 Windows Autopilot 体验，最终用户会经历正常的 OOBE。 注册后，在用户再次运行 OOBE 之前，将不会应用 Windows Autopilot 配置。 如果在创建 MDM 配置文件之前启动了设备，则设备将经历标准的 OOBE 体验。  然后，IT 管理员必须手动将该设备注册到 MDM，之后重置该设备后，它将经历 Windows Autopilot OOBE 体验。|
|为什么在 Autopilot 期间未收到自定义的登录屏幕？ |租户品牌必须在 portal.azure.com 中进行配置才能接收自定义的登录体验。|
|如果设备已注册到 Azure AD 但未分配 Windows Autopilot 配置文件，会发生什么情况？                                |由于未向设备分配 Windows Autopilot 配置文件，因此将发生 regular Azure AD OOBE。|
|如何在 Autopilot 上收集日志？|在 Windows Autopilot 上收集日志的最佳方式是在 OOBE 期间收集 "跟踪。 可根据请求提供此跟踪 (WPRP 扩展) 的 XML 文件。|

## <a name="mdm"></a>MDM

| 问题 | Answer |
| --- | --- |
| 是否必须为 MDM 使用 Intune？  |  不会，任何 MDM 都将使用 Autopilot，但其他 MDM 可能不会与 Intune 具有相同的完整 Windows Autopilot 功能套件。  你将从 Intune 获得最佳体验。 |
| Intune 是否可以支持 Win32 应用预安装？  | 是。  从 Windows 10 十月更新 (版本 1809) 开始，Intune 支持使用 .msi 和 .msix 包装的 Win32 应用。  |
| 什么是共同管理？  | 共同管理是指结合使用云 MDM 工具 (Intune) 和本地配置工具（如 Microsoft 终结点 Configuration Manager）的组合。 仅当 Intune 不能支持您要对配置文件执行的操作时，才需要使用 Configuration Manager。  如果选择使用 Intune + Configuration Manager 进行共同管理，请在 Intune 配置文件中包含 Configuration Manager 代理来执行此操作。 将该配置文件推送到设备后，设备将看到 Configuration Manager 代理，并向下移动到 Configuration Manager 以拉取任何其他配置文件设置。 |
| 必须使用 Microsoft Endpoint Configuration Manager for Windows Autopilot  |  不行。  上面所述的共同管理 () 是可选的。 |


## <a name="features"></a>功能

| 问题 | Answer |
| --- | --- |
| 自部署模式  | 新版本的 Windows Autopilot，其中用户仅打开了设备，而不打开任何其他版本。  这适用于不需要标准用户帐户 (例如，共享设备或展台设备) 的情况。  |
| 混合 Azure Active Directory 联接  |  除 Azure AD 加入) 外，还允许 Windows Autopilot 设备连接到本地 Active Directory 域控制器 (。 |
| Windows Autopilot reset  | 从设备中删除用户应用和设置，但保留 Azure AD 域加入和 MDM 注册。  在将设备从一个用户转移到另一个用户时非常有用。  |
| 个性化  | 将以下内容添加到 OOBE 体验：可以创建个性化的欢迎消息。 用户名提示可以添加登录页文本。 可以包含公司的徽标 |
| [面向现有设备的 Autopilot](existing-devices.md)  |  为所有基于 Windows 7 和 Windows 8 的现有设备提供 Windows Autopilot 的升级路径。 |



## <a name="general"></a>常规

|问题|Answer
|------------------|-----------------|
| 如果我擦除计算机并重新启动，仍然会收到 Windows Autopilot 吗？|是的，如果设备仍为 Windows Autopilot 注册，并且正在运行受支持的 Windows 10 半半年通道，则将收到 Windows Autopilot 体验。|
| 能否在现有计算机上获取设备指纹？|是的，如果设备运行的是受支持版本的 Windows 10 半年通道，则可获取设备指纹进行注册。 不会计划将功能向后移植旧版本，也无法在运行不受支持的 Windows 版本的设备上获取这些版本。|
| 在其他 Sku 上支持 Windows Autopilot，例如 Surface Hub、HoloLens、Windows Mobile。|否，其他 Sku 不支持 Windows Autopilot。|
| MBR 或映像重新安装后，Windows Autopilot 是否正常工作？ | 是。 有关详细信息，请参阅 [Windows Autopilot 主板更换方案指南](autopilot-mbr.md)。 |
| 是否有几次重置映像的设备会经历 Autopilot？ 错误消息 "此用户无权注册" 是什么意思？ 错误代码801c0003。 |特定 Azure AD 用户可以在 Azure AD 中注册的设备数有限制，以及 Intune 中每个用户支持的设备数。  这些都是可配置的，但并不是无限的。  如果重复使用设备，或即使回滚到以前的虚拟机快照，则会经常遇到此错误。|
| 如果设备已注册到恶意代理，会发生什么情况？ | 按照设计，Windows Autopilot 不会应用配置文件，直到用户使用 Azure AD 登录过程通过配置的配置文件的匹配租户登录。  例如，如果 badguys.com 注册了 contoso.com 拥有的设备，则在最糟糕的情况下，该用户将被定向到 badguys.com。 用户输入其电子邮件和密码后，将通过 Azure AD 重定向到正确的 Azure AD 身份验证，然后系统会提示用户登录到 contoso.com。 由于 contoso.com 不会将 badguys.com 与租户匹配，因此将不会应用 Windows Autopilot 配置文件，并且将发生常规 Azure AD OOBE。|
| Windows Autopilot 数据存储在何处？  |Windows Autopilot 数据存储在美国 (US) ，而不是主权云中，即使 Azure AD 租户注册在主权云中时也是如此。 这适用于所有 Windows Autopilot 数据，而不考虑用于部署 Autopilot 的门户。|
| 为什么 Windows Autopilot 数据存储在美国而不是主权云中？| 不存储客户数据，只是使 Microsoft 能够提供服务的业务数据，因此它适合于数据驻留在美国。 客户随时可以停止订阅服务。 在这种情况下，Microsoft 将删除业务数据。 Autopilot 在任何主权云中当前不受支持。 |
| 为 Windows Autopilot 注册设备有多少方法|注册设备的方法有六种，具体取决于执行注册的人员： <br><br>1. OEM 直接 API (仅适用于 TVOs)  <br>MPC 使用 MPC API (必须是 CSP)  <br>3. 在 UI (中使用 CSV 文件的手动上传的 MPC 必须是 CSP)  <br>4. 使用 CSV 文件上传的 MSfB <br>5. 使用 CSV 文件上传的 Intune <br>6. 使用 CSV 文件上传 Microsoft 365 商业版高级门户|
|有多少种方法可创建 Windows Autopilot 配置文件？|可通过四种方式创建和分配 Windows Autopilot 配置文件： <br><br>1. 通过 MPC (必须是 CSP)  <br>2. 通过 MSfB <br>3. 通过 Intune (或其他 MDM)  <br>4. Microsoft 365 商业版 Premium 门户 <br><br>Microsoft 建议通过 Intune 创建和分配配置文件。  |
| 注册失败的一些常见原因是什么？ |1. 硬件哈希条目损坏或丢失可能导致注册尝试错误 <br>2. CSV 文件中隐藏特殊字符。  <br><br>若要避免此问题，请在创建 CSV 文件后，在记事本中打开它以查找隐藏字符或尾随空格或其他损坏。|
|  IoT 设备是否支持 Autopilot？ |  IoT Core 设备上不支持 Autopilot，当前没有计划添加此支持。 Windows 10 IoT Enterprise SAC 设备支持 Autopilot。 Autopilot 在 Windows 10 Enterprise LTSC 2019 及更高版本上受支持;它在 LTSC 的早期版本中不受支持。|
|  所有地区/国家/地区是否支持 Autopilot？ |  Autopilot 仅支持使用全球 Azure 的客户。 全局 Azure 不包含下面列出的三个实体：<br>-Azure 德国 <br>-Azure 中国世纪互联<br>-Azure 政府版<br>因此，如果客户是在全球 Azure 中设置的，则不存在区域限制。 例如，如果 Contoso 使用全球 Azure，但员工在中国工作，则在中国工作的 Contoso 员工将能够使用 Autopilot 来部署设备。 如果 Contoso 使用 Azure 中国世纪互联，Contoso 员工将无法使用 Autopilot。|

## <a name="glossary"></a>词汇表

| 术语 | 含义 |
| --- | --- |
| CSV  | 逗号分隔的值 (类似于 Excel 电子表格) 的文件类型  |
| MPC  | Microsoft 合作伙伴中心   |
| MDM  | 移动设备管理   |
| OEM  | 原始设备制造商   |
| CSP  |  云解决方案提供商  |
| MSfB  | 适用于企业的 Microsoft Store   |
| Azure AD  | Azure Active Directory   |
| 4K HH  |  4K 硬件哈希 |
| 高于  | 计算机生成报表  |
| EC  |  企业商务  |
| DDS  | 设备目录服务    |
| OOBE  | 全新体验   |
| UUID  | 全局唯一标识符   |