---
title: 快速入门 - 创建适用于 iOS/iPadOS 设备的电子邮件设备配置文件
titleSuffix: Microsoft Intune
description: 了解如何使用 Microsoft Intune 创建电子邮件设备配置文件，以便 iOS/iPadOS 设备可以安全地连接到公司电子邮件。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6bc170c5260dc099d0a2b4109ed119572e0dbaff
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086849"
---
# <a name="quickstart-create-an-email-device-profile-for-iosipados"></a>快速入门：创建适用于 iOS/iPadOS 的电子邮件设备配置文件

在本快速入门中，你将了解如何创建适用于 iOS/iPadOS 设备的电子邮件设备配置文件。 本配置文件指定了 iOS/iPadOS 设备上内置电子邮件应用连接到公司电子邮件所需的设置。 电子邮件设备配置文件有助于跨设备标准化设置，并允许最终用户在不进行任何所需设置的情况下在其个人设备上访问公司电子邮件。 要进一步保护电子邮件，可以使用电子邮件配置文件来确定设备是否符合要求，然后设置条件访问权限以仅允许兼容设备访问电子邮件。 有关电子邮件配置文件的详细信息，请参阅[如何在 Microsoft Intune 中配置电子邮件设置](email-settings-configure.md)

如果没有 Intune 订阅，请[注册免费试用帐户](../fundamentals/free-trial-sign-up.md)。

## <a name="sign-in-to-intune"></a>登录到 Intune

以全局管理员或 Intune 服务管理员身份登录 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。 如果已创建 Intune 试用版订阅，则用于创建订阅的帐户就是全局管理员。

## <a name="create-an-iosipados-email-profile"></a>创建 iOS/iPadOS 电子邮件配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择并转到“设备”   > “配置文件”   > “创建配置文件”  。
   ![在 Intune 中创建适用于 iOS/iPadOS 的电子邮件配置文件](./media/quickstart-email-profile/ios-create-profile.png)

3. 输入以下属性：
   - **平台**：选择“iOS/iPadOS” 
   - **配置文件**：选择“电子邮件” 
  
4. 选择“创建”。 

5. 在“基本信息”  中，输入以下属性：
   - **名称**：输入新配置文件的描述性名称。 对于本示例，请输入“iOS 需要的工作电子邮件”  。
   - **描述**：输入“需要 iOS/iPadOS 设备使用工作电子邮件” 


        ![在 Intune 中创建适用于 iOS/iPadOS 设备的电子邮件配置文件](./media/quickstart-email-profile/ios-email-profile-name.png)

6. 选择“下一步”  。

7. 在“配置设置”中，输入以下设置（保留其他设置的默认值）： 
   - **电子邮件服务器**：对于本快速入门，请输入“outlook.office365.com”  。 本设置指定 iOS/iPadOS 邮件应用用于连接到电子邮件的电子邮件服务器的 Exchange 位置 (URL)。
   - **帐户名**：输入公司电子邮件  。
   - **AAD 中的用户名属性**：此名称是 Intune 从 Azure Active Directory (Azure AD) 获取的属性。 Intune 使用此名称动态生成此配置文件的用户名。 在本快速入门中，我们假设希望将“用户主体名称”用作配置文件的用户名（例如，user1@contoso.com）  。
   - **AAD 中的电子邮件地址属性**：此设置将设置 Azure AD 中用于登录 Exchange 的电子邮件地址。 在本快速入门中，选择“用户主体名称”  。
   - **身份验证方法**：在本快速入门中，请选择“用户名和密码”  。 （如果已经为 Intune 设置了证书，也可以选择“证书”  。）

8. 选择“下一步”  。

9. 在“作用域标记”  （可选），选择“下一步”  。 将不会对此配置文件使用作用域标记。

10. 在“分配”  中，使用“分配到”  下拉列表，并选择“所有用户和所有设备”  。  然后选择“下一步”  。

11. 在“查看并创建”中查看设置  。 选择“创建”时，将保存所做的更改并分配配置文件  。 

## <a name="clean-up-resources"></a>清理资源

如果不想使用为其他教程或测试创建的配置文件，可以立即删除它。

1. 在 Intune 中，选择“设备”   > “设备配置”  。
2. 选择创建的测试配置文件，“iOS/iPadOS 需要的工作电子邮件”  ，然后选择“删除”  。 

## <a name="next-steps"></a>后续步骤

在本快速入门中，创建适用于 iOS/iPadOS 设备的电子邮件配置文件。 现在可以使用此配置文件来确定 iOS/iPadOS 设备是否合规，方法是创建合规性策略，将任何与该配置文件不匹配的 iOS/iPadOS 设备标记为不合规。 对于进一步保护，可以创建条件访问策略，阻止不合规的 iOS/iPadOS 设备访问电子邮件。 有关设备符合性策略的详细信息，请参阅 [Intune 中的设备符合性策略入门](../protect/device-compliance-get-started.md)。

> [!div class="nextstepaction"]
> [教程：保护托管设备上的 Exchange Online 电子邮件](../protect/tutorial-protect-email-on-enrolled-devices.md)
