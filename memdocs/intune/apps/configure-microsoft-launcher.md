---
title: 使用 Intune 为 Android Enterprise 配置 Microsoft Launcher
titleSuffix: ''
description: 将 Intune 配置策略用于 Microsoft Launcher。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 09ebf7fde0cedb907e105e42abe7338237d231af
ms.sourcegitcommit: c333fc6627f5577cde9d2fa8f59e642202a7027b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2020
ms.locfileid: "84795697"
---
# <a name="configure-microsoft-launcher"></a>配置 Microsoft Launcher

Microsoft Launcher 是一款 Android 应用程序，它允许用户对手机进行个性化设置、随时随地整理并由从手机工作转换为从电脑工作。 

在由 Android Enterprise 完全托管的设备上，Launcher 允许企业 IT 管理员选择壁纸、应用和图标位置，来自定义托管设备。 这将各个 OEM 设备和系统版本的所有 Android 托管设备的外观标准化。 

## <a name="how-to-configure-the-microsoft-launcher-app"></a>如何配置 Microsoft Launcher 应用 

将 Microsoft Launcher 应用程序[添加到 Intune](../apps/apps-add.md)后，导航到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，然后选择“应用” > “应用配置策略” 。 为运行“Android”的“托管设备”添加配置策略，并选择“Microsoft Launcher”作为关联应用 。 单击“配置设置”以配置可用的各种 Microsoft Launcher 设置。 

## <a name="choosing-a-configuration-settings-format"></a>选择配置设置格式 

可以使用两种方法来定义 Microsoft Launcher 的配置设置： 

- **配置设计器**：通过易于使用的 UI 来配置设置，使你能够切换功能的开关和设置值。 在此方法中，有一些值类型为 BundleArray 的已禁用的配置项。 只有通过输入 JSON 数据才能配置这些配置项。 

- **JSON 数据**：使你能够使用 JSON 脚本来定义所有可能的配置项。 

如果使用配置设计器来添加属性，则可以通过从“配置设置格式”下拉列表中选择“输入 JSON 数据”来自动将这些属性转换为 JSON ，如下所示。

   ![配置设置格式 - 使用配置设计器](./media/configure-microsoft-launcher/configure-microsoft-launcher-01.png)

   > [!NOTE]
   > 通过配置设计器配置属性后，JSON 数据也将更新为只反映这些属性。 若要将其他配置键添加到 JSON 数据中，请使用[JSON 脚本示例](../apps/configure-microsoft-launcher.md#microsoft-launcher-configuration-example)复制每个配置键所需的行。 

在编辑先前创建的应用配置策略时，如果已配置复杂属性，编辑过程将显示 JSON 数据编辑器。 将保留所有先前配置的设置，并可以切换为使用配置设计器来修改支持的设置。

## <a name="using-configuration-designer"></a>使用配置设计器

配置设计器使你能够选择预填充的设置及其关联值。

   ![配置设置格式 - 输入 JSON 数据](./media/configure-microsoft-launcher/configure-microsoft-launcher-02.png)

下表列出了 Microsoft Launcher 可用的配置项、值类型、默认值和描述。 描述将提供基于所选值的预期设备行为。 配置设计器中已禁用的配置项未在表中列出。

|    Configuration 注册表项    |    值类型    |    默认值    |    说明     |
|---------------------------------------------------|------------------|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    注册类型    |    字符串     |    默认    |    允许设置此策略应应用到的注册类型。 当前值“默认”表示“CorporateOwnedBuisnessOnly”。  目前没有其他支持的注册类型。        JSON 键名称：management_mode_key        |
|    允许“主屏幕应用顺序”用户更改    |    布尔值    |    True    |    允许指定最终用户是否可以更改“主屏幕应用顺序”设置。<ul><li>若设置为 True，将仅对初始部署执行策略定义的应用顺序。 随后，将不再执行此策略，以便采用用户可能作出的任何更改。</li><li>若设置为“False”，每次同步时都将执行此应用顺序。</li></ul><br>**注意:** 只能通过 JSON 编辑器配置主屏幕应用顺序。<br><br>JSON 键名称：<br>`com.microsoft.launcher.HomeScreen.AppOrder.UserChangeAllowed`    |
|    设置网格大小    |    字符串    |    自动    |    使你能够设置要在主屏幕上定位的应用的网格大小。 可以设置应用行数和列数来按以下格式定义网格大小：`columns;rows`。 如果定义网格大小，主屏幕上的一行中将显示的最大应用数量就是设置的行数，主屏幕上的一列中将显示的最大应用数量就是设置的列数。<br><br>        JSON 键名称：<br>`com.microsoft.launcher.HomeScreen.GridSize`    |
|    设置设备墙纸    |    字符串    |    Null    |    使你能够通过输入要设置为壁纸的图像的 URL 来设置所选的壁纸。<br><br>JSON 键名称：<br>`com.microsoft.launcher.Wallpaper.URL`    |
|    允许“设置设备墙纸”用户更改    |    Bool    |    True    |    允许指定最终用户是否可以更改“设置设备墙纸”设置。<ul><li>若设置为 True，将仅对初始部署执行策略中的墙纸。 随后，将不再执行此策略，以便采用用户可能作出的任何更改。</li><li>若设置为“False”，每次同步时都将执行此墙纸。</li></ul><br>JSON 键名称：<br>`com.microsoft.launcher.Wallpaper.URL.UserChangeAllowed`        |
|    源启用    |    布尔值    |    True    |    在用户轻扫到主屏幕右侧时，允许你在设备上启用启动器源。<ul><li>若设置为“True”，将启用源。</li><li>若设置为“False”，将禁用源。</li></ul><br>JSON 键名称：<br>`com.microsoft.launcher.Feed.Enabled`    |
|    允许“源启用”用户更改    |    布尔值    |    True    |     允许指定最终用户是否可以更改“源启用”设置。<ul><li>若设置为 True，将仅对初始部署执行源。 随后，将不再执行此策略，以便采用用户可能作出的任何更改。</li><li>若设置为“False”，每次同步时都将执行源。</li></ul><br>JSON 键名称：`com.microsoft.launcher.Feed.Enabled.UserChangeAllowed`    |
|    搜索栏放置   |    字符串    |    底部    |  允许在主屏幕上指定“搜索栏的位置”。 <ul><li>如果设置为“底部”，搜索栏将位于主屏幕的底部。</li><li>如果设置为“顶部”，搜索栏将位于主屏幕的顶部。</li><li>如果设置为“隐藏”，搜索栏将从主屏幕中移除。</li></ul><br>JSON 键名称：<br>`com.microsoft.launcher.Search.SearchBar.Placement`    |
|    允许用户更改搜索栏放置位置   |    Bool    |    True    |  允许指定最终用户是否可以更改“搜索栏放置”设置。 <ul><li>若设置为 True，将仅对初始部署强制执行搜索栏放置。 随后，将不再执行此策略，以便采用用户可能作出的任何更改。</li><li>若设置为“False”，则搜索栏的位置将在每次同步时强制执行。</li></ul><br>JSON 键名称：<br>`com.microsoft.launcher.Search.SearchBar.Placement.UserChangeAllowed`<p>**注意：** 对于微软桌面 v 6.2 及更高版本，将不再强制执行此设置。 因此，将此值设置为 `True` 将不起作用。 最终用户将无法自定义设备上搜索栏的位置。    |
|    停靠模式  |    字符串    |    显示    | 在用户轻扫到主屏幕右侧时，允许在设备上启用停靠。<ul><li>如果设置为“显示”，则停靠将启用。</li><li>如果设置为“隐藏”，停靠将从主屏幕隐藏，但用户可以在需要时显示它。</li><li>如果设置为“禁用”，则将禁用停靠。</li></ul><br>JSON 键名称：<br>`com.microsoft.launcher.Dock.Mode`    |
|   允许用户更改“停靠模式”   |    字符串    |    True    |  允许指定最终用户是否可以更改“停靠模式”设置。<ul><li>若设置为 True，将仅对初始部署强制执行停靠模式设置。 随后，将不再执行此策略，以便采用用户可能作出的任何更改。</li><li>若设置为“False”，每次同步时都将执行停靠模式设置。</li></ul><br>JSON 键名称：<br>`com.microsoft.launcher.Dock.Mode.UserChangeAllowed`    |

## <a name="enter-json-data"></a>输入 JSON 数据

输入 JSON 数据来配置托管主屏幕的所有可用设置以及“Microsoft Launcher”中禁用的设置，如下所示。

   ![配置设计器 - JSON 数据](./media/configure-microsoft-launcher/configure-microsoft-launcher-03.png)

除了“配置设计器”表中列出的可配置设置的列表之外（如上所述），下表还提供了只能通过 JSON 数据进行配置的配置项。

|    Configuration 注册表项    |    值类型    |    默认值    |    说明     |
|----------------------------------------------------------------------------------------------------|-------------------|-------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    设置已列入允许列表的应用程序<br>JSON 键：`com.microsoft.launcher.HomeScreen.Applications`    |    BundleArray    | 请参阅：[设置已列入允许列表的应用程序](configure-microsoft-launcher.md#set-allow-listed-applications)</sup>    |    使你能够从设备上安装的应用中定义主屏幕上可见的应用集。 可以通过输入要使其可见的应用的应用包名称来定义应用，例如 `com.android.settings` 可以使设置在主屏幕上可访问。 已在此部分中列入允许列表的应用应已安装在设备上，以使其在主屏幕上可见。<p>属性:<ul><li>**包：** 应用程序包名称</li><li>**类：** 特定于某个应用页的应用程序活动。 若此值为空，它将使用默认的应用页。</li></ul>      |
|    主屏幕应用顺序<br>JSON 键：`com.microsoft.launcher.HomeScreen.AppOrder`    |    BundleArray    |    请参阅：[主屏幕应用顺序](configure-microsoft-launcher.md#home-screen-app-order)      |    允许你指定主屏幕上的应用顺序。<p>属性:<br><ul><li>**类型：** 如果要指定应用的位置，唯一支持的类型为 `application`。 如果要指定 Web 链接的位置，则类型为 `weblink`。</li><li>**位置：** 这将指定主屏幕上的应用程序图标槽。 它从左上方的位置 1 开始，并从左到右从上到下延伸。</li><li>**包：** 这是用于指定应用顺序的应用程序包名称。</li><li>**类：** 这是特定于某个应用页的应用程序活动。 若此值为空，将使用默认的应用页。 此属性用于应用。</li><li>**标签：** 这是特定于某个应用页的应用程序活动。 若此值为空，将使用默认的应用页。 此属性用于应用。</li><li>**链接：** 最终用户单击 Web 链接图标后启动的 URL。 此属性用于 Web 链接。</li></ul>    |
|    设置固定的 Web 链接<br>JSON 键：`com.microsoft.launcher.HomeScreen.WebLinks`    |    BundleArray    |    请参阅：[设置固定的 Web 链接](configure-microsoft-launcher.md#set-pinned-web-link)      |    此键可用于将网站固定到主屏幕作为快速启动图标。 这样就可以确保最终用户能够快速方便地访问重要的网站。 可以在“主屏幕应用顺序”配置中修改每个 Web 链接图标的位置。<p>属性:<br><ul><li>**• 标签：** 显示在 MS Launcher 主屏幕上的 Web 链接标题。</li><li>**链接：** 最终用户单击 Web 链接图标后启动的 URL。</li></ul>    |


### <a name="set-allow-listed-applications"></a>设置已列入允许列表的应用程序

```JSON
{
    "key": "com.microsoft.launcher.HomeScreen.Applications",
    "valueBundleArray": 
    [
        {
            "managedProperty": [
                {
                    "key": "package",
                    "valueString": ""
                },
                {
                    "key": "class",
                    "valueString": ""
                }
            ]
        }
    ]
}
```

### <a name="home-screen-app-order"></a>主屏幕应用顺序

```JSON
{
    "key": "com.microsoft.launcher.HomeScreen.AppOrder",
    "valueBundleArray": 
    [
        {
            "managedProperty": [
                {
                    "key": "type",
                    "valueString": "application"
                },
                {
                    "key": "position",
                    "valueInteger": 0
                },
                {
                    "key": "package",
                    "valueString": ""
                },
                {
                    "key": "class",
                    "valueString": ""
                }
            ]
        }
    ]
}
```

### <a name="set-pinned-web-link"></a>设置固定的 Web 链接

```JSON
{ 
    "key": "com.microsoft.launcher.HomeScreen.WebLinks",  
    "valueBundleArray": [ 
        { 
            "managedProperty": [ 
                { 
                    "key": "label",
                    "valueString": "" 
                },  
                { 
                    "key": "link", 
                    "valueString": "" 
                } 
            ] 
        }
    ] 
},
{ 
    "key": "com.microsoft.launcher.HomeScreen.AppOrder",  
    "valueBundleArray": [ 
        { 
            "managedProperty": [ 
                { 
                    "key": "type",  
                    "valueString": "" 
                },  
                { 
                    "key": "position",  
                    "valueInteger": 
                },  
                { 
                    "key": "label",  
                    "valueString": "" 
                },  
                { 
                    "key": "link",  
                    "valueString": "" 
                } 
            ] 
        }
    ] 
}
```



### <a name="microsoft-launcher-configuration-example"></a>Microsoft Launcher 配置示例

以下是包含所有可用配置项的示例 JSON 脚本：

```JSON
{
    "kind": "androidenterprise#managedConfiguration", 
    "productId": "app:com.microsoft.launcher", 
    "managedProperty": [
        {
            "key": "management_mode_key", 
            "valueString": "Default"
        }, 
        {
            "key": "com.microsoft.launcher.Feed.Enable.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.Feed.Enable", 
            "valueBool": true
        }, 
        {
            "key": "com.microsoft.launcher.Wallpaper.Url.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.Wallpaper.Url", 
            "valueBool": "http://www.contoso.com/wallpaper.png"
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.GridSize", 
            "valueString": "5;5"
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.Applications", 
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.ups.mobile.android"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.teams"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.bing"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }
            ]
        }, 
        { 
            "key": "com.microsoft.launcher.HomeScreen.WebLinks",  
            "valueBundleArray": [ 
                { 
                    "managedProperty": [ 
                        { 
                            "key": "label",
                            "valueString": "News" 
                        },  
                        { 
                            "key": "link", 
                            "valueString": "https://www.bbc.com" 
                        } 
                    ] 
                }
            ] 
        },
        {
            "key": "com.microsoft.launcher.HomeScreen.AppOrder.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.AppOrder", 
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 17
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.ups.mobile.android"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 18
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.teams"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 19
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.bing"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "weblink"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 20
                        }, 
                        {
                            "key": "label", 
                            "valueString": "News"
                        }, 
                        {
                            "key": "link", 
                            "valueString": "https://www.bbc.com"
                        }
                    ]
                }
            ]
        }
    ]
}

```

## <a name="next-steps"></a>后续步骤

- 有关 Android Enterprise 完全托管设备的详细信息，请参阅[设置 Android Enterprise 完全托管设备的 Intune 注册](../enrollment/android-fully-managed-enroll.md)。
