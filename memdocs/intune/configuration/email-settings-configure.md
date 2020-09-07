---
title: 在 Microsoft Intune 中配置电子邮件设置 - Azure | Microsoft Docs
titleSuffix: ''
description: 在 Microsoft Intune 中创建电子邮件配置文件，并将此配置文件部署到 Android 设备管理员、Android Enterprise、iOS、iPadOS 和 Windows 设备。 使用电子邮件配置文件以配置常见的电子邮件设置，包括电子邮件服务器和身份验证方法，以便在管理的设备上连接到公司电子邮件。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 99f3dcd944270acef98cc0f1f06138d75dba4453
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996412"
---
# <a name="add-email-settings-to-devices-using-intune"></a>使用 Intune 向设备添加电子邮件设置

Microsoft Intune 包括各种电子邮件设置，可将这些设置部署到组织中的设备。 IT 管理员创建包含特定设置的电子邮件配置文件，以连接到邮件服务器，如 Microsoft 365 和 Gmail。 然后，最终用户在移动设备上连接、验证和同步自己的组织电子邮件帐户。 通过创建和部署电子邮件配置文件，可以确认设置跨多个设备是标准的。 而且，有助于减少不知道正确电子邮件设置的最终用户的求助致电
。

可以使用电子邮件配置文件为以下设备配置内置电子邮件设置：

- Samsung Knox Standard 5.0 和更高版本上的 Android 设备管理员
- Android Enterprise
- iOS 11.0 及更高版本
- iPadOS 13.0 及更高版本
- Windows 10（桌面版）

本文介绍如何在 Microsoft Intune 中创建电子邮件配置文件。 此外，还包括指向不同平台的链接，以获得更具体的设置。

## <a name="create-the-profile"></a>创建配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备” > “配置文件” > “创建配置文件”。
3. 输入以下属性：

    - **平台**：选择设备平台。 选项包括：  

        - **Android 设备管理员**（仅限 Samsung Android Knox Standard）
        - **Android Enterprise**
        - **iOS/iPadOS**
        - **Windows 10 及更高版本**

    - **配置文件**：选择“电子邮件”。

4. 选择“创建”。
5. 在“基本信息”中，输入以下属性：

    - **名称**：输入策略的描述性名称。 为策略命名，以便稍后可以轻松地识别它们。 例如，将策略名称命名为“Windows 10: 适用于所有 Windows 10 设备的电子邮件设置。
    - **描述**：输入策略的说明。 此设置是可选的，但建议进行。

6. 选择“下一步”。

7. 在“配置设置”中，根据所选择的平台，可配置的设置有所不同。 选择平台，以了解详细设置：

    - [Android 设备管理员 (Samsung Knox Standard)](email-settings-android.md)
    - [Android Enterprise](email-settings-android-enterprise.md)
    - [iOS/iPadOS](email-settings-ios.md)
    - [Windows 10](email-settings-windows-10.md)

8. 选择“下一步”。
9. 在“作用域标记”（可选）中，分配一个标记以将配置文件筛选到特定 IT 组（如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`）。 有关范围标记的详细信息，请参阅[将 RBAC 和范围标记用于分布式 IT](../fundamentals/scope-tags.md)。

    选择“下一步”。

10. 在“分配”中，选择可以接收配置文件的用户或设备组。 若要了解分配配置文件的详细信息，请参阅 [须知内容](#what-you-need-to-know)（在本文中）。 [分配用户和设备配置文件](device-profile-assign.md)也提供了一些指导。

    选择“下一步”。

11. 在“查看并创建”中查看设置。 选择“创建”时，将保存所做的更改并分配配置文件。 该策略也会显示在配置文件列表中。

## <a name="what-you-need-to-know"></a>须知内容

- 电子邮件配置文件是为注册设备的用户部署的。 为了配置电子邮件配置文件，Intune 会在注册期间使用用户的电子邮件配置文件中的 Azure Active Directory (AD) 属性。

- 适用于 iOS/iPadOS 和 Android 设备的 Microsoft Outlook 不支持电子邮件配置文件。 应为它们部署应用配置策略。 有关详细信息，请参阅 [Outlook 配置设置](../apps/app-configuration-policies-outlook.md)。

  在 Android Enterprise 设备上，使用托管的 Google Play 商店部署 Gmail 或 Nine for Work。 [添加托管 Google Play 应用](../apps/apps-add-android-for-work.md)中列出了相关步骤。

- 电子邮件基于标识和用户设置。 通常会将电子邮件配置文件分配给用户组而非设备组。 注意事项：

  - 如果电子邮件配置文件包括用户证书，则将电子邮件配置文件分配给用户组。 你可能分配了多个用户证书配置文件。 这些配置文件创建了一个配置文件部署链。 将此配置文件链部署到用户组。

    如果此链中的一个配置文件部署到了设备组，则可能会持续提示用户输入密码。

  - 如果没有主要用户或不知道该用户是谁，通常使用设备组。 可能无法将针对设备组（不是用户组）的电子邮件配置文件传递到设备。

    例如，如果你的电子邮件配置文件针对所有 iOS/iPadOS 设备组，请确保所有这些设备都有用户。 如果所有设备都没有用户，则电子邮件配置文件可能不会部署。 然后，限制该配置文件，这可能会丢失某些设备。 如果设备具有主要用户，则部署到设备组应正常工作。

    如需深入了解使用设备组时可能出现的问题，请参阅[电子邮件配置文件的常见问题](troubleshoot-email-profiles-in-microsoft-intune.md)。

## <a name="remove-an-email-profile"></a>删除电子邮件配置文件

可以通过不同的方式从设备删除电子邮件配置文件，即使设备上只有一个电子邮件配置文件：

- **选项 1**：打开电子邮件配置文件（“设备” > “配置文件” > 选择你的配置文件），然后选择“分配”。 “包含”选项卡将显示已分配配置文件的组。 右键单击“组”，然后单击“删除”。 务必保存你的更改。

- **选项 2**：[擦除或停用设备](../remote-actions/devices-wipe.md)。 这些操作可用于有选择地或完全删除数据和设置。

## <a name="secure-email-access"></a>保护电子邮件访问

可以使用以下选项来帮助保护电子邮件配置文件：

- **证书**：创建电子邮件配置文件时，选择之前在 Intune 中创建的证书配置文件。 该证书又称为标识证书。 它根据受信任的证书配置文件（或根证书）进行身份验证，以确定用户的设备可以连接。 受信任的证书会分配到对电子邮件连接进行身份验证的计算机。 通常，此计算机是本机邮件服务器。

  如果对电子邮件配置文件使用基于证书的身份验证，则将电子邮件配置文件、证书配置文件和受信任的根配置文件部署到相同的组。 此部署可确保每台设备都能识别证书颁发机构的合法性。

  有关如何在 Intune 中创建和使用证书配置文件的详细信息，请参阅[如何使用 Intune 配置证书](../protect/certificates-configure.md)。

- **用户名和密码**：最终用户通过输入用户名和密码向本机邮件服务器进行身份验证。 电子邮件配置文件中不存在密码。 因此，最终用户需要在连接到电子邮件时输入密码。

## <a name="how-intune-handles-existing-email-accounts"></a>Intune 如何处理现有电子邮件帐户

如果用户已配置电子邮件帐户，则电子邮件配置文件的分配方式因平台而异。

- **iOS/iPadOS**：基于主机名和电子邮件地址检测到现有的重复电子邮件配置文件。 重复的电子邮件配置文件会阻止分配 Intune 配置文件。 在这种情况下，公司门户应用通知用户它们不符合要求，并提示最终用户手动删除已配置的配置文件。 为了有助于防止这种情况发生，请告诉最终用户在安装电子邮件配置文件前先注册，这样一来 Intune 就可以设置配置文件了。

- **Windows：** 基于主机名和电子邮件地址检测到现有的重复电子邮件配置文件。 Intune 覆盖最终用户创建的现有电子邮件配置文件。

- **Android Samsung Knox Standard**：基于电子邮件地址检测到现有的重复电子邮件帐户，并使用 Intune 配置文件将其覆盖。 Android 不使用主机名验证配置文件。 请勿在不同主机上使用相同的电子邮件地址创建多个电子邮件配置文件。 配置文件相互覆盖。

- **Android 工作配置文件**：Intune 提供了两个 Android 工作电子邮件配置文件：一个用于 Gmail 应用，另一个用于 Nine Work 应用。 这些应用在 Google Play 商店中提供，并且安装在设备工作配置文件中。 这些应用不会重复创建配置文件。 这两个应用支持到 Exchange 的连接。 要使用电子邮件连接，请将其中某个电子邮件应用部署到用户的设备上。 然后，创建并部署电子邮件配置文件。 可以使用适用于“工作配置文件”和“公司拥有的完全托管式专用工作配置文件”类型的 Gmail 和 Nine 电子邮件配置文件，包括对这两种电子邮件配置类型使用证书文件。 你在设备配置中为工作配置文件创建的任何 Gmail 或 Nine 策略都继续应用于该设备。 无需将它们移至应用配置策略。 Nine Work 等电子邮件应用可能需付费使用。 若有任何问题，请查看应用的许可详细信息或与应用公司联系。

## <a name="changes-to-assigned-email-profiles"></a>对已分配的电子邮件配置文件的更改

如果更改以前分配的电子邮件配置文件，最终用户可能会看到一条消息，请求他们批准重新配置其电子邮件设置。

## <a name="next-steps"></a>后续步骤

配置文件已创建，但它尚未起到任何作用。 下一步，[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。
