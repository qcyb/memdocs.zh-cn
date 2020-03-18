---
title: 配置 Microsoft 托管主屏幕应用
titleSuffix: Microsoft Intune
description: 了解如何配置 Microsoft 托管主屏幕应用。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 865c7f03-f525-4dfa-b3a8-d088a9106502
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b81246598fce3c03c95d9fd052e058749932bff4
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79342772"
---
# <a name="configure-the-microsoft-managed-home-screen-app-for-android-enterprise"></a>配置适用于 Android Enterprise 的 Microsoft 托管主屏幕应用

托管主屏幕是一款应用程序，适用于通过 Intune 注册的并且在多应用展台模式下运行的公司拥有的 Android Enterprise 专用设备。 对于这些设备，托管主屏幕充当要在这些设备上运行的其他已批准应用的启动器。 托管主屏幕使 IT 管理员能够自定义其设备并限制最终用户可以访问的功能。 

## <a name="when-to-configure-the-microsoft-managed-home-screen-app"></a>何时配置 Microsoft 托管主屏幕应用

通常，如果通过设备配置提供了设置，请在此处配置这些设置。 这样可以节省时间，在最大程度上减少错误，并且将获得更佳的 Intune 支持体验。 但是，一些托管主屏幕设置目前仅通过 Intune 控制台中的“应用配置策略”窗格提供  。 使用本文档来了解如何使用配置设计器或 JSON 脚本对不同的设置进行配置。 

> [!NOTE]
> 目前，通过“应用”和“设备配置”来设置已列入允许列表的应用程序和固定的 Web 链接是可行的，也是可取的   。 有关“设备配置”中提供的可影响托管主屏幕的设置的完整列表，请参阅[专用设备设置](../configuration/device-restrictions-android-for-work.md#dedicated-device-settings)  。  

首先，导航到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，然后选择“应用”   > “应用配置策略”  。 为运行“Android”的“托管设备”添加配置策略，并选择“托管主屏幕”作为关联应用   。 单击“配置设置”以配置不同的可用托管主屏幕设置  。 

## <a name="choosing-a-configuration-settings-format"></a>选择配置设置格式

可以使用两种方法来定义托管主屏幕的配置设置：

- **配置设计器**：通过易于使用的 UI 来配置设置，使你能够切换功能的开关和设置值。 在此方法中，有一些值类型为 `BundleArray` 的已禁用的配置项。 只有通过输入 JSON 数据才能配置这些配置项。 
- **JSON 数据**：使你能够使用 JSON 脚本来定义所有可能的配置项。 

如果使用配置设计器来添加属性，则可以通过从“配置设置格式”下拉列表中选择“输入 JSON 数据”来自动将这些属性转换为 JSON   。

![“配置设置格式”选项的屏幕截图](./media/app-configuration-managed-home-screen-app/app-configuration-managed-home-screen-app_01.png)

## <a name="using-configuration-designer"></a>使用配置设计器

配置设计器使你能够选择预填充的设置及其关联值。 

![已添加的配置设置的屏幕截图](./media/app-configuration-managed-home-screen-app/app-configuration-managed-home-screen-app_02.png)

下表列出了托管主屏幕可用的配置项、值类型、默认值和描述。 描述将提供基于所选值的预期设备行为。 配置设计器中已禁用的配置项未在表中列出。

| 配置项 | 值类型 | 默认值 | 说明 |
|---------------------------------------------------------------------------------------------------------------------------|-------------|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 设置网格大小 | 字符串 | 自动 | 使你能够设置要在托管主屏幕上定位的应用的网格大小。 可以设置应用行数和列数来按以下格式 (`columns;rows`) 定义网格大小。 如果定义网格大小，主屏幕上的一行中将显示的最大应用数量就是设置的行数，主屏幕上的一列中将显示的最大应用数量就是设置的列数。 |
| 启用通知锁屏提醒 | 布尔 | FALSE | 为应用图标启用可以显示应用上的新通知数的通知锁屏提醒。 如果启用此设置，最终用户将在有未读通知的应用上看到锁屏提醒。 如果禁用此配置项，最终用户将看不到针对任何可能有未读通知的应用的锁屏提醒。 |
| 锁定主屏幕 | 布尔 | TRUE | 使最终用户无法在主屏幕上移动应用图标。 如果启用此配置项，主屏幕上的应用图标将被锁定，最终用户无法将这些图标拖放到主屏幕上其他的网格位置。 如果设置为 `false`，最终用户将能够在托管主屏幕上移动应用程序和 Web 链接图标。  |
| 设置设备壁纸 | 字符串 | 默认 | 使你能够通过输入要设置为壁纸的图像的 URL 来设置所选的壁纸。 |
| 设置应用图标大小 | integer | 2 | 使你能够设置主屏幕上显示的应用的图标大小。 可以在此配置中选择以下值来使用不同的尺寸：0（最小）、1（小）、2（常规）、3（大）和 4（最大）。 |
| 设置应用文件夹图标 | integer | 0 | 使你能够在主屏幕上定义应用文件夹的外观。 可以从以下值中选择外观：Dark Square(0)；Dark Circle(1)；Light Square(2)；Light Circle(3)。 |
| 设置屏幕方向 | integer | 1 | 使你能够将主屏幕的方向设置为纵向模式、横向模式或允许自动旋转。 可以通过输入值 1（纵向模式）、2（横向模式）或 3（自动旋转）来设置方向。 |
| 启用设备遥测 | 布尔 | FALSE | 启用为托管主屏幕捕获的所有遥测。 如果启用此功能，Microsoft 将能够捕获设备使用情况遥测，例如某一特定应用在此设备上的启动次数。 |
| 设置已列入允许列表的应用程序 | bundleArray | FALSE | 使你能够从设备上安装的应用中定义主屏幕上可见的应用集。 可以通过输入要使其可见的应用的应用包名称来定义应用，例如 com.microsoft.emmx 可以使设置在主屏幕上可访问。 已在此部分中列入允许列表的应用应已安装在设备上，以使其在主屏幕上可见。 |
| 设置固定的 Web 链接 | bundleArray | FALSE | 使你能够将网站固定为主屏幕上的快速启动图标。 通过此配置，可以定义 URL 并将其添加到主屏幕，使最终用户只需轻轻点击一下即可在浏览器中启动。 |
| 启用屏幕保护 | 布尔 | FALSE | 是否启用屏幕保护模式。 如果设置为 true，则可以配置“screen_saver_image”、“screen_saver_show_time”、“inactive_time_to_show_screen_saver”和“media_detect_screen_saver”     。 |
| 屏幕保护图像 | 字符串 |   | 设置屏幕保护图像的 URL。 如果未设置 URL，设备将在屏幕保护激活后显示默认屏幕保护图像。 默认图像显示托管主屏幕应用图标。  |
| 屏幕保护显示时间 | integer | 0 | 提供可以设置设备将在屏幕保护模式期间显示屏幕保护的时间（以秒为单位）的选项。 如果设置为 0，屏幕保护将一直显示在屏幕保护模式中，直到设备变为活动状态为止。  |
| 启用屏幕保护之前处于非活动状态的时间 | integer | 30 | 触发屏幕保护之前设备处于非活动状态的秒数。 如果设置为 0，设备将永远不会进入屏幕保护模式。 |
| 在显示屏幕保护之前检测媒体 | 布尔 | TRUE | 选择当设备上正在播放音频/视频时，设备屏幕是否应显示屏幕保护。 如果设置为 true，设备都将停止播放音频/视频，而不考虑 inactive_time_to_show_scree_saver 中的值  。 如果设置为 false，设备屏幕将根据 inactive_time_to_show_screen_saver 中设置的值来显示屏幕保护  。   |
| 启用虚拟主页按钮 | 布尔 | FALSE | 如果将此设置设置为 `True`，最终用户则可以访问托管主屏幕主页按钮。通过使用此按钮，用户将从当前所处理的任务返回托管主屏幕。  |
| 虚拟主页按钮的类型 | 字符串 | swipe_up | 使用“swipe_up”来通过向上轻扫手势以访问主页按钮  。 使用“float”来访问最终用户可以在屏幕上移动的永久性粘滞的主页按钮  。 |
| 电池和信号强度指示栏 | 布尔 | True  | 将此设置设为 `True` 可以显示电池和信号强度指示栏。 |
| 退出锁定任务模式密码 | 字符串 |   | 输入 4 - 6 位数的代码来用于临时退出锁定任务模式以进行故障排除。 |
| 显示 Wi-Fi 设置 | 布尔 | FALSE | 如果将此设置设为 `True`，最终用户则可以打开或关闭 Wi-Fi，或连接到不同的 Wi-Fi 网络。  |
| 显示蓝牙设置 | 布尔 | FALSE | 如果将此设置设为 `True`，最终用户则可以打开或关闭蓝牙以及连接到支持蓝牙的不同设备。   |
| 文件夹中的应用程序按名称进行排序 | 布尔 | TRUE | 如果将此设置设为 `False`，则可以按指定顺序显示文件夹中的各个项。 否则，它们将按字母顺序显示在文件夹中。   |
| 已启用应用程序顺序 | 布尔 | FALSE | 如果将此设置设为 `True`，则可以在托管主屏幕上设置应用程序、Web 链接和文件夹的顺序。 启用后，使用 app_order  设置顺序，最终用户则可以打开或关闭蓝牙以及连接到支持蓝牙的不同设备。   |
| 应用程序顺序 | bundleArray | FALSE | 允许你在托管主屏幕上指定应用程序、Web 链接和文件夹的顺序。 若要使用此设置，必须启用“锁定主屏幕”，必须定义“设置网格大小”   ，并且必须将“已启用应用程序顺序”  设置为 `True`。   |

## <a name="enter-json-data"></a>输入 JSON 数据

输入 JSON 数据来配置托管主屏幕的所有可用设置以及“配置设计器”中禁用的设置  。

![已添加的 JSON 数据的屏幕截图](./media/app-configuration-managed-home-screen-app/app-configuration-managed-home-screen-app_03.png)

除了“配置设计器”表中列出的可配置设置的列表之外（如上所述），下表还提供了只能通过 JSON 数据进行配置的配置项  。

|    配置项    |    值类型    |    默认值    |    说明    |
|-------------------------------------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    设置已列入允许列表的应用程序    |    bundleArray    | <img alt="JSON - Example 1" src="./media/app-configuration-managed-home-screen-app/defaultvaluejson01.png" width="300"> |    使你能够从设备上安装的应用中定义主屏幕上可见的应用集。 可以通过输入要使其可见的应用的应用包名称来定义应用，例如 com.android.settings 可以使设置在主屏幕上可访问。 已在此部分中列入允许列表的应用应已安装在设备上，以使其在主屏幕上可见。    |
|    设置固定的 Web 链接    |    bundleArray    | <img alt="JSON - Example 2" src="./media/app-configuration-managed-home-screen-app/defaultvaluejson02.png" width="300"> |    使你能够将网站固定为主屏幕上的快速启动图标。 通过此配置，可以定义 URL 并将其添加到主屏幕，使最终用户只需轻轻点击一下即可在浏览器中启动。    |
|    创建托管文件夹来对应用进行分组    |    bundleArray    | <img alt="JSON - Example 3" src="./media/app-configuration-managed-home-screen-app/defaultvaluejson03.png" width="300"> |    使你能够创建和命名文件夹并在这些文件夹中对应用进行分组。 最终用户将无法移动文件夹、重命名文件夹或移动文件夹中的应用。   文件夹将按创建的顺序显示，文件夹中的应用将按字母顺序显示。         注意：要分组到文件夹中的所有应用必须按需分配给设备，并且必须被添加到了托管主屏幕。     |

以下是包含所有可用配置项的示例 JSON 脚本：

```json
{
    "kind": "androidenterprise#managedConfiguration",
    "productId": "com.microsoft.launcher.enterprise",
    "managedProperty": [
        {
            "key": "lock_home_screen",
            "valueBool": true
        },
        {
            "key": "wallpaper",
            "valueString": "default"
        },
        {
            "key": "icon_size",
            "valueInteger": 2
        },
        {
            "key": "app_folder_icon",
            "valueInteger": 0
        },
        {
            "key": "screen_orientation",
            "valueInteger": 1
        },
        {
            "key": "enable_telemetry",
            "valueBool": false
        },
        {
            "key": "applications",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "package",
                            "valueString": “app package name here”
                        }
                    ]
                }
            ]
        },
        {
            "key": "weblinks",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "link",
                            "valueString": “link here”
                        },
                        {
                            "key": "label",
                            "valueString": “weblink label here”
                        }
                    ]
                }
            ]
        },
        {
            "key": "show_virtual_home",
            "valueBool": false
        },
        {
            "key": "virtual_home_type",
            "valueString": "swipe_up"
        },
        {
            "key": "show_virtual_status_bar",
            "valueBool": true
        },
        {
            "key": "exit_lock_task_mode_code",
            "valueString": ""
        },
        {
            "key": "show_wifi_setting",
            "valueBool": false
        },
        {
            "key": "show_bluetooth_setting",
            "valueBool": false
        },
        {
            "key": "grid_size",
            "valueString": "4;5"
        },
        {
            "key": "app_order_enabled",
            "valueBool": true
        },
        {
            "key": "apps_in_folder_ordered_by_name",
            "valueBool": true
        },
        {
            "key": "app_orders",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "package",
                            "valueString": "com.Microsoft.emmx"
                        },
                        {
                            "key": "type",
                            "valueString": "application"
                        },
                        {
                            "key": "container",
                            "valueInteger": 1
                        },
                        {
                            "key": "position",
                            "valueInteger": 1
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "folder_name",
                            "valueString": "Work"
                        },
                        {
                            "key": "type",
                            "valueString": "managed_folder"
                        },
                        {
                            "key": "container",
                            "valueInteger": 1
                        },
                        {
                            "key": "position",
                            "valueInteger": 2
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "package",
                            "valueString": "com.microsoft.launcher.enterprise"
                        },
                        {
                            "key": "type",
                            "valueString": "application"
                        },
                        {
                            "key": "class",
                            "valueString": "com.microsoft.launcher.launcher"
                        },
                        {
                            "key": "container",
                            "valueInteger": 1
                        },
                        {
                            "key": "position",
                            "valueInteger": 3
                        }
                    ]
                }
            ]
        },
        {
            "key": "managed_folders",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "folder_name",
                            "valueString": "Folder name here"
                        },
                        {
                            "key": "applications",
                            "valueBundleArray": [
                                {
                                    "managedProperty": [
                                        {
                                            "key": "package",
                                            "valueString": "com.microsoft.emmx"
                                        }
                                    ]
                                },
                                {
                                    "managedProperty": [
                                        {
                                            "key": "package",
                                            "valueString": "com.microsoft.bing"
                                        }
                                    ]
                                },
                                {
                                    "managedProperty": [
                                        {
                                            "key": "link",
                                            "valueString": "https://microsoft.com/"
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "folder_name",
                            "valueString": "Example folder name 2"
                        },
                        {
                            "key": "applications",
                            "valueBundleArray": [
                                {
                                    "managedProperty": [
                                        {
                                            "key": "package",
                                            "valueString": "com.microsoft.office.word"
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                }
            ]
        }
    ]
}
```

## <a name="googles-android-device-policy-app"></a>Google 的 Android 设备策略应用
托管主屏幕应用现在可以访问 Google 的 Android 设备策略应用。 托管主屏幕应用是一种自定义启动器，用于使用多应用展台模式在 Intune 中注册为 Android Enterprise (AE) 专用设备的设备。 你可以访问 Android 设备策略应用，或引导用户访问 Android 设备策略应用，以获取支持和进行调试。 此启动功能在设备注册并锁定到托管主屏幕时可用。 无需其他安装项，即可使用此功能。

## <a name="managed-home-screen-debug-screen"></a>托管的主屏幕调试屏幕
可以通过单击“后退”按钮访问托管的主屏幕的调试屏幕，直到显示调试屏幕（单击“后退”按钮 15 次或更多次）   。 在此调试屏幕中，可以启动 Android 设备策略应用程序、查看和上传日志，或临时暂停展台模式以更新设备。 有关暂停展台模式的详细信息，请参阅 Android Enterprise [专用设备设置](../configuration/device-restrictions-android-for-work.md#dedicated-device-settings)中的“退出展台模式”  项。

## <a name="next-steps"></a>后续步骤

- 有关 Android Enterprise 专用设备的详细信息，请参阅[设置 Android Enterprise 专用设备的 Intune 注册](../enrollment/android-kiosk-enroll.md)。
