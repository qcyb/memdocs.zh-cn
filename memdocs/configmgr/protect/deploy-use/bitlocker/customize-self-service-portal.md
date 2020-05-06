---
title: 自定义自助服务门户
titleSuffix: Configuration Manager
description: 将特定于组织的自定义信息添加到 BitLocker 管理自助服务门户
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6bc26e36-9914-4606-ae8d-f7b23218942f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3f4fdb0d6a41c2b40c9e35840dfc27261a42e68b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693495"
---
# <a name="customize-the-self-service-portal"></a>自定义自助服务门户

适用范围：  Configuration Manager (Current Branch)

<!--3601034-->

在[安装 BitLocker 自助服务门户](setup-websites.md)后，可以为组织自定义此门户。 添加自定义通知、组织名称和其他特定于组织的信息。

## <a name="branding"></a>品牌打造

使用组织名称、技术支持 URL 和通知文本，打造自助服务门户的品牌。

1. 在托管自助服务门户的 Web 服务器上，以管理员身份登录。

1. 启动 Internet Information Services (IIS) 管理器  （运行 inetmgr.exe  ）。

1. 依次展开“站点”  和“默认网站”  ，然后选择“SelfService”  节点。 在细节窗格的“ASP.NET”  组中，打开“应用程序设置”  。

    [![IIS 管理器中 SelfService 应用程序设置的 示例屏幕截图](media/bitlocker-self-service-iis-app-settings.png)](media/bitlocker-self-service-iis-app-settings.png#lightbox)

1. 选择要更改的项目，然后选择“操作”  窗格中的“编辑”  。 将“值”  更改为要使用的新名称。

    > [!CAUTION]
    > 请勿更改“名称”  值。 例如，请勿更改 `CompanyName`，而是更改 `Contoso IT`。 如果你更改“名称”  值，自助服务门户会停止运行。

更改将立即生效。

### <a name="supported-branding-values"></a>支持的品牌值

对于可以设置的值，请参阅下表：

|名称|说明|默认&nbsp;值|
|--- |--- |--- |
|CompanyName|自助服务门户在每页顶部显示为标题的组织名称。|`Contoso IT`|
|DisplayNotice|显示用户必须确认收到的初始通知。|`true`|
|HelpdeskText|右侧窗格中“若有其他任何相关问题”下面的字符串|`Contact Helpdesk or IT Department`|
|HelpdeskUrl|HelpdeskText 字符串的链接。|（空）|
|NoticeTextPath|用户必须确认收到的初始通知的文本。 默认情况下，Web 服务器上的完整文件路径是 `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt`。 在纯文本编辑器中编辑并保存文件。 此路径值相对于 SelfService 应用程序。|`Notice.txt`|

<!-- Not sure if we support changing these values. At a minimum need a description.
|ClientValidationEnabled||`true`|
|UnobtrusiveJavaScriptEnabled||`true`|
-->

有关默认自助服务门户的屏幕截图，请参阅 [BitLocker 自助服务门户](self-service-portal.md)。

> [!TIP]
> 如果需要，可以将其中一些字符串本地化为用不同的语言显示。 有关详细信息，请参阅[本地化](#bkmk_localize)。

## <a name="session-time-out"></a>会话超时

若要让用户会话在指定的不活动期限后到期，可以更改自助服务门户的会话超时设置。

1. 在托管自助服务门户的 Web 服务器上，以管理员身份登录。

1. 启动 Internet Information Services (IIS) 管理器  （运行 inetmgr.exe  ）。

1. 依次展开“站点”  和“默认网站”  ，然后选择“SelfService”  节点。 在细节窗格的“ASP.NET”  组中，打开“会话状态”  。

1. 在“Cookie 设置”  组中，更改“超时(分钟)”  值。 这是指用户会话在多少分钟后到期。 默认值为 `5`。 若要禁用此设置以便取消超时，则将值设置为 `0`。

1. 在“操作”  窗格中，选择“应用”  。

## <a name="localize-helpdesk-text-and-url"></a><a name="bkmk_localize"></a> 本地化技术支持文本和 URL

可以配置自助服务门户 `HelpdeskText` 语句和 `HelpdeskUrl` 链接的本地化版本。 此字符串指示用户如何在使用门户时获取更多帮助。 如果你配置本地化文本，门户会为 Web 浏览器显示相应语言的本地化版本。 如果找不到本地化版本，则会显示 `HelpdeskText` 和 `HelpdeskUrl` 设置中的默认值。

1. 在托管自助服务门户的 Web 服务器上，以管理员身份登录。

1. 启动 Internet Information Services (IIS) 管理器  （运行 inetmgr.exe  ）。

1. 依次展开“站点”  和“默认网站”  ，然后选择“SelfService”  节点。 在细节窗格的“ASP.NET”  组中，打开“应用程序设置”  。

1. 在“操作”  窗格中，选择“添加”  。

1. 在“添加应用程序设置”  窗口中，配置以下值：

    - 名称  ：输入“`HelpdeskText_<language>`”，其中 `<language>` 是文本的语言代码。

      例如，若要创建西班牙语（西班牙）的本地化版本 `HelpdeskText` 语句，“名称”为“`HelpdeskText_es-es`”。

    - 值  ：要在自助服务门户的右侧窗格中的“若有其他任何相关问题”下显示的本地化字符串

1. 选择“确定”  ，以保存新设置。

1. 重复此过程，为与关联的 `HelpdeskText_<language>` 设置匹配的新应用程序设置 `HelpdeskUrl_<language>`。

重复此过程，为组织中支持的所有语言添加设置对。

## <a name="localize-the-notice-file"></a>本地化通知文件

可以配置用户必须在自助服务门户上确认收到的初始通知的本地化版本。 默认情况下，Web 服务器上的完整文件路径是 `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt`。

若要显示本地化通知文本，请创建本地化文件 notice.txt。 然后，将它保存到特定的语言文件夹下。 例如：`Self Service Website\es-es\Notice.txt` 代表西班牙语（西班牙）。

自助服务门户根据下列规则显示通知文本：

- 如果缺少默认通知文件，门户显示消息来指明缺少默认文件。

- 如果你在相应语言文件夹中创建本地化通知文件，门户显示本地化通知文本。

- 如果 Web 服务器找不到通知文件的本地化版本，门户显示默认通知。

- 如果用户将浏览器设置为没有本地化通知的语言，门户显示默认通知。

### <a name="create-a-localized-notice-file"></a>创建本地化通知文件

1. 在托管自助服务门户的 Web 服务器上，以管理员身份登录。

1. 在 `Self Service Website` 应用程序路径中，为支持的每种语言创建 `<language>` 文件夹。 例如，`es-es` 代表西班牙语（西班牙）。 默认情况下，完整路径为 `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es`。

    有关你可使用的有效语言代码的列表，请参阅[ National Language Support (NLS) API Reference（区域语言支持 (NLS) API 参考）](https://docs.microsoft.com/windows/win32/intl/locale-identifiers#predefined-locale-identifiers)。

    > [!TIP]
    > 语言文件夹的名称也可以是中性语言名称。 例如，es  代表西班牙语，不像 es-es  代表西班牙语（西班牙）和 es-ar  代表西班牙语（阿根廷）。 如果用户将浏览器设置为“es-es”  ，但此语言没有对应的语言文件夹，Web 服务器会以递归方式检查父区域设置文件夹 (es  )。 （父区域设置是在 .NET 中定义。）例如，`Self Service Website\es\Notice.txt`。 此递归回退模拟的是 .NET 资源加载规则。

1. 创建包含本地化文本的默认通知文件的副本。 将它保存到语言代码对应的文件夹中。 例如，对于西班牙语（西班牙），完整路径默认为 `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es\Notice.txt`。

重复此过程，为组织中支持的所有语言添加本地化通知文件。

## <a name="next-steps"></a>后续步骤

至此，你已安装并自定义自助服务门户，不妨试试吧！ 有关详细信息，请参阅 [BitLocker 自助服务门户](self-service-portal.md)。
