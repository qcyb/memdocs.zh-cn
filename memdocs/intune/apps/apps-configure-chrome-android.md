---
title: 使用 Intune 配置适用于 Android 设备的 Google Chrome
titleSuffix: Microsoft Intune
description: 将 Intune 配置策略用于适用于 Android 设备的 Google Chrome。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 89d9fce6579b0fdf89299e342969f647c457cc84
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2020
ms.locfileid: "80324828"
---
# <a name="configure-google-chrome-for-android-devices-using-intune"></a>使用 Intune 配置适用于 Android 设备的 Google Chrome 

可以使用 Intune 应用配置策略配置适用于 Android 设备的 Google Chrome。 应用设置可自动应用。 例如，可以专门设置想要阻止或允许的书签或 URL。

## <a name="prerequisites"></a>必备条件

- 用户的 Android Enterprise 设备必须已在 Intune 中注册。 有关详细信息，请参阅[设置 Android Enterprise 工作配置文件设备的注册](../enrollment/android-work-profile-enroll.md)。
- 将 Google Chrome 添加为托管的 Google Play 应用。 有关托管的 Google Play 的详细信息，请参阅[如何将 Intune 帐户连接到托管的 Google Play 帐户](../enrollment/connect-intune-android-enterprise.md)。

## <a name="add-the-google-chrome-app-to-intune"></a>将 Google Chrome 应用添加到 Intune

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“应用”   > “所有应用”   > “添加”  ，然后添加“托管的 Google Play”  应用。
3. 转到“托管的 Google Play”，搜索并批准 Google Chrome。 

    ![搜索并批准 Google Chrome](./media/apps-configure-chrome-android/search.png)

4. 将 Google Chrome 作为必需的应用类型分配给用户组。 在 Intune 中注册设备时，将自动部署 Google Chrome。

有关将托管的 Google Play 应用添加到 Intune 的详细信息，请参阅[托管的 Google Play 商店应用](apps-add-android-for-work.md#managed-google-play-store-apps)。

## <a name="add-app-configuration-for-managed-ae-devices"></a>添加托管 AE 设备的应用配置

1. 在 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“应用”   > “应用配置策略”   > “添加”   > “托管设备”  。
2. 设置以下详细信息：
    - **名称** - 在 Azure 门户中显示的配置文件名。
    - **说明** - 在 Azure 门户中显示的配置文件说明。
    - **设备注册类型** - 此设置设为“托管设备”。 
    - **平台** - 选择 Android  。

    ![添加 Google Chrome 配置策略](./media/apps-configure-chrome-android/add-policy.png)

3. 单击“关联应用”，以显示“关联应用”窗格。   找到并选择“Google Chrome”。  此列表包含[已批准并与 Intune 同步的托管 Google Play 应用](apps-add-android-for-work.md)。

    ![从“关联应用”下选择“Google Chrome”](./media/apps-configure-chrome-android/associated-app.png)

4. 单击“配置设置”，选择“使用配置设计器”，然后单击“添加”，以选择配置键。   

    ![添加“使用配置设计器”](./media/apps-configure-chrome-android/configuration.png)

    下面是通用设置的示例：
    - **阻止访问 URL 列表**：`["*"]`
    - **允许访问 URL 列表**：`["baidu.com", "youtube.com", "chromium.org", "chrome://*"]`
    - **托管的书签**：`[{"toplevel_name": "My managed bookmarks folder"  },  {"url": "baidu.com",   "name": "Baidu"},  {"url": "youtube.com", "name": "Youtube"},  {"name": "Chrome links",  "children": [{"url": "chromium.org", "name": "Chromium"},    {"url": "dev.chromium.org", "name": "Chromium Developers"}]}]`
    - **隐身模式可用性**：`Incognito mode disabled`

    使用配置设计器添加配置设置后，会在表中列出这些设置。 

    ![通用设置](./media/apps-configure-chrome-android/common-settings.png)

    上述设置将创建书签，并阻止访问除 `baidu.com``yahoo.com``chromium.org` 和 `chrome://` 之外的所有 URL。

5. 单击“确定”和“添加”，将配置策略添加到 Intune。  
6. 将此配置策略分配给用户组。 有关详细信息，请参阅[使用 Microsoft Intune 将应用分配到组](apps-deploy.md)。

## <a name="verify-the-device-settings"></a>验证设备设置

在 Android Enterprise 中注册 Android 设备后，将自动部署托管的 Google Chrome 应用以及项目组合图标。

   <img alt="Managed Google Chrome with the portfolio icon" src="./media/apps-configure-chrome-android/chrome-icon.png" width="350">

启动 Google Chrome，设置将生效。

   书签：<br>
   <img alt="Bookmarks" src="./media/apps-configure-chrome-android/bookmarks.png" width="350">

   阻止的 URL：<br>
   <img alt="Blocked URL" src="./media/apps-configure-chrome-android/blocked-url.png" width="350">

   允许 URL：<br>
   <img alt="Allow URL" src="./media/apps-configure-chrome-android/allowed-url.png" width="350">

   隐身选项卡：<br>
   <img alt="Incognito tab" src="./media/apps-configure-chrome-android/incognito-tab.png" width="350">

## <a name="troubleshooting"></a>疑难解答

1. 查看 Intune 门户，以监视策略部署状态。

    ![监视策略部署状态](./media/apps-configure-chrome-android/monitor-status.png)

2. 启动 Google Chrome，访问 chrome://policy。  可以确认设置是否已成功应用。

    ![确认设置已成功应用](./media/apps-configure-chrome-android/confirm.png)

## <a name="additional-information"></a>其他信息

- [为托管的 Android Enterprise 设备添加应用配置策略](app-configuration-policies-use-android.md)
- [Chrome Enterprise 策略列表](https://cloud.google.com/docs/chrome-enterprise/policies/)

## <a name="next-steps"></a>后续步骤

- 有关 Android Enterprise 完全托管设备的详细信息，请参阅[设置 Android Enterprise 完全托管设备的 Intune 注册](../enrollment/android-fully-managed-enroll.md)。
