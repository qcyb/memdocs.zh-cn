---
title: 将 Android 设备从设备管理员转到工作配置文件管理
titleSuffix: Microsoft Intune
description: 在 Intune 中将 Android 设备从设备管理员转到工作配置文件管理。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2c8c521dc0899b3429de85e95116a6277d724771
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2020
ms.locfileid: "80327277"
---
# <a name="move-android-devices-from-device-administrator-to-work-profile-management"></a>将 Android 设备从设备管理员转到工作配置文件管理

通过使用符合性设置“阻止由设备管理员管理的设备”  ，可以帮助用户将自己的 Android 设备从设备管理员转到工作配置文件管理。 通过此设置，可以将不通过设备管理员管理的设备设为不符合要求。 

当用户看到他们出于此原因不符合要求时，他们可以点击“解决”  。 系统会将他们转到一个清单，将指导他们完成一系列步骤：
1. 从设备管理员管理取消注册
2. 注册到工作配置文件管理
3. 解决符合性问题。 

## <a name="prerequisites"></a>必备条件

- 用户的[已注册 Android 设备管理员的设备](android-enroll-device-administrator.md)必须安装有 Android 公司门户版本 5.0.4720.0 或更高版本。
- 通过[将 Intune 租户帐户连接到 Android Enterprise 帐户](connect-intune-android-enterprise.md)设置 Android 工作配置文件管理。
- 为要转到 Android 工作配置文件的一组用户[设置 Android Enterprise 工作配置文件注册](android-work-profile-enroll.md)。
- 考虑增加用户设备限制。 从设备管理员管理中取消注册设备时，可能不会立即删除设备记录。 若要在此期间提供缓冲，可能需要增加设备限制容量，以便用户可以注册工作配置文件管理。
  - 将 [Azure Active Directory 设备设置](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal#configure-device-settings)配置为每个用户的最大设备数量。
  - 通过设置设备限制调整 [Intune 设备限制](enrollment-restrictions-set.md#create-a-device-limit-restriction)。 

## <a name="create-device-compliance-policy"></a>创建设备符合性策略

1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“设备” > “符合性策略” > “策略” > “创建策略”     。

    ![创建策略](./media/android-move-device-admin-work-profile/create-policy.png)

2. 在“创建策略”  页上，将“平台”  设置为“Android 设备管理员”   > “创建”  。
3. 在“基本信息”页上，键入“名称”和“说明” > “下一步”     。

    ![“基本信息”页](./media/android-move-device-admin-work-profile/basics.png)
    
4. 在“符合性设置”  页上的“设备运行状况”  部分中，将“阻止由设备管理员托管的设备”设置为“是”    > “下一步”  。

    ![阻止设备](./media/android-move-device-admin-work-profile/block-devices.png)

5. 在“位置”  页上，根据需要添加位置，然后单击“下一步”  。
6. 对于“对不符合要求项的操作”  ，可以设置“向最终用户发送电子邮件”  操作。

    ![发送电子邮件](./media/android-move-device-admin-work-profile/send-email.png)


    在电子邮件中，可以在发送给用户的消息中添加以下 URL。 此 URL 将启动 Android 公司门户的“更新设备设置”  页。 可以在此页上开始执行转到工作配置文件管理的步骤。
    - [https://portal.manage.microsoft.com/UpdateSettings.aspx](https://portal.manage.microsoft.com/UpdateSettings.aspx)。
    - 对于美国政府版，可以改用以下链接：[https://portal.manage.microsoft.us/UpdateSettings.aspx](https://portal.manage.microsoft.us/UpdateSettings.aspx)。
  
    > [!NOTE]
    > - 当然，在与用户通信时，可以使用用户友好的超文本链接。 不过，请不要使用 URL 缩短器，这样很可能导致链接失效。
    > - 如果 Android 公司门户在后台处于打开状态，当用户点击该链接时，他们可能会转到上次打开的页面。
    > - 用户必须在 Android 设备上点击此链接。 如果他们将其粘贴到浏览器中，则不会启动 Android 公司门户。 

    选择“下一步”  。

7. 在“范围标记”  页上，选择要包括的任何范围标记。
8. 在“分配”  页上，将策略分配到其中的设备已注册设备管理员管理的组，然后单击“下一步”  。
9. 在“查看 + 创建”  页上，确认所有设置，然后选择“创建”  。

## <a name="troubleshooting"></a>疑难解答

[转到新的设备管理设置的最终用户流程](../user-help/move-to-new-device-management-setup.md)可指导用户从设备管理员管理取消注册，并设置工作配置文件管理。 用户的[已注册 Android 设备管理员的设备](android-enroll-device-administrator.md)必须安装有 Android 公司门户版本 5.0.4720.0 或更高版本。

### <a name="user-sees-an-error-after-tapping-resolve"></a>用户在点击“解决”后看到错误
如果用户在点击“解决”  按钮后出现错误，可能是由于以下原因之一导致的：
- 未正确设置工作配置文件注册（未连接 Android Enterprise 帐户或设置了用于阻止工作配置文件注册的注册限制）。
- 设备运行的是 Android 4.4 或更早版本，不支持注册工作配置文件。 
- 设备制造商不支持在该设备型号上注册工作配置文件。

### <a name="resolve-button-doesnt-appear-on-the-users-device"></a>用户设备上不显示“解决”按钮
如果用户符合上述设备符合性策略的要求并已注册设备管理员管理，用户设备上将不会显示“解决”  按钮。

要显示“解决”按钮，用户必须推迟设置并从通知中重新开始该过程  。

为避免这种情况，请使用注册限制来阻止注册设备管理员管理。

### <a name="user-sees-an-error-after-tapping-url-to-update-device-settings-page"></a>用户点击 URL 转到“更新设备设置”页后看到错误
当用户点击指向 Android 公司门户的“更新设备设置”页的 URL 时，浏览器中可能显示错误页面  。 此错误可能是由于以下原因之一导致的：
- 设备不是 Android 设备。
- Android 设备没有公司门户应用。
- Android 公司门户版本低于 5.0.4720.0。
- Android 设备使用的是 Android 6 或更低版本。 

## <a name="next-steps"></a>后续步骤
[请参阅最终用户流](../user-help/move-to-new-device-management-setup.md)
[使用 Intune 管理 Android 工作配置文件设备](android-enterprise-overview.md)
