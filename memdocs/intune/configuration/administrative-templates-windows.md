---
title: 使用 Microsoft Intune 中适用于 Windows 10 设备的模板 - Azure | Microsoft Docs
description: 使用 Microsoft Intune 和终结点管理器中的管理模板为 Windows 10 设备创建多组设置。 在设备配置的配置文件中使用这些设置来控制 Office 程序、Microsoft Edge、保护 Internet Explorer、访问 OneDrive、使用远程桌面、启用自动播放、设置电源管理设置、使用 HTTP 打印、控制用户登录以及更改事件日志大小。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: faa217bd5e56a304b80298f2039ad3c541612e54
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88992797"
---
# <a name="use-windows-10-templates-to-configure-group-policy-settings-in-microsoft-intune"></a>使用 Windows 10 模板在 Microsoft Intune 中配置组策略设置

管理组织中的设备时，你希望创建几组应用于不同设备组的设置。 例如，你有多个设备组。 对于 GroupA，要分配一组特定设置。 对于 GroupB，要分配另一组设置。 此外，还需要可配置设置的简单视图。

可以使用 Microsoft Intune 中的“管理模板”完成此任务。 管理模板包括数千个设置，这些设置可控制 Microsoft Edge 77 及更高版本、Internet Explorer、Microsoft Office 程序、远程桌面、OneDrive 中的功能，以及密码和 PIN 等等。 这些设置允许组管理员使用云来管理组策略。

此功能适用于：

- Windows 10 及更高版本

Windows 设置类似于 Active Directory (AD) 中的组策略 (GPO) 设置。 这些设置内置于 Windows 中，是使用 XML 的[支持 ADMX 的设置](/windows/client-management/mdm/understanding-admx-backed-policies)。 Office 和 Microsoft Edge 设置为 ADMX 引入的设置，并使用 [Office 管理模板文件](https://www.microsoft.com/download/details.aspx?id=49030)和 [Microsoft Edge 管理模板文件](https://www.microsoftedgeinsider.com/enterprise)中的 ADMX 设置。 Intune 模板 100% 基于云。 它们提供简单和直接的方法来配置设置，并可查找所需设置。

“管理模板”内置于 Intune 中，不需要任何自定义（包括使用 OMA-URI）。 作为移动设备管理 (MDM) 解决方案的一部分，请将这些模板设置用作一站式服务，以管理 Windows 10 设备。

本文列出为 Windows 10 设备创建模板的步骤，并演示如何筛选 Intune 中的所有可用设置。 创建模板时，模板会创建设备配置配置文件。 然后，可以将此配置文件分配或部署到贵组织中的 Windows 10 设备。

## <a name="before-you-begin"></a>在开始之前

- 其中一些设置从 Windows 10 版本 1709（RS2/内部版本 15063）开始提供。 所有 Windows 版本中均不包含某些设置。 为获得最佳体验，建议使用 Windows 10 企业版 1903（19H1/内部版本 18362）及更高版本。

- Windows 设置使用 [Windows 策略 CSP](/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies)。 CSP 适用于不同版本的 Windows，例如家庭版、专业版和企业版等。 要查看 CSP 是否适用于特定版本，请转到 [Windows 策略 CSP](/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies)。

## <a name="create-the-template"></a>创建模板

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备” > “配置文件” > “创建配置文件”。
3. 输入以下属性：

    - **平台**：选择“Windows 10 及更高版本”。
    - **配置文件**：选择“管理模板”。

4. 选择“创建”。
5. 在“基本信息”中，输入以下属性：

    - **名称**：输入配置文件的描述性名称。 为配置文件命名，以便稍后可以轻松地识别它们。 例如，配置文件名称最好是“管理模板：用于在 Microsoft Edge 中配置 xyz 设置的 Windows 10 管理模板”。
    - **描述**：输入配置文件的说明。 此设置是可选的，但建议进行。

6. 选择“下一步”。

7. 在“配置设置”中，选择“所有设置”，查看所有设置按字母顺序排序的列表 。 或者，配置适用于设备的设置（“计算机配置”）和适用于用户的设置（“用户配置”） ：

    > [!div class="mx-imgBorder"]
    > ![将 ADMX 模板设置应用于 Microsoft Intune 终结点管理器中的用户和设备](./media/administrative-templates-windows/administrative-templates-choose-computer-user-configuration.png)

8. 选择“所有设置”时，将列出所有设置。 向下滚动以使用上一个和下一个箭头查看更多设置：

    > [!div class="mx-imgBorder"]
    > ![请查看设置的示例列表，并使用“上一页”和“下一页”按钮](./media/administrative-templates-windows/administrative-templates-sample-settings-list.png)

9. 选择任意设置。 例如，在 Office 上筛选，然后选择“激活受限浏览”。 列出设置的详细描述。 选择“启用”、“禁用”或将设置保留为“未配置”（默认）。 详细说明还会介绍选择“启用”、“禁用”或“未配置”时发生的情况。

    > [!TIP]
    > Intune 中的 Windows 设置与你在本地组策略编辑器 (`gpedit`) 中看到的本地组策略路径相关

10. 选择“计算机配置”或“用户配置”时，将显示设置类别 。 可以选择任何类别查看可用的设置。

    例如，依次选择“计算机配置” > “Windows 组件” > “Internet Explorer”即可查看适用于 Internet Explorer 的所有设备设置：

    > [!div class="mx-imgBorder"]
    > ![在 Microsoft Intune 终结点管理器中查看适用于 Internet Explorer 的所有设备设置](./media/administrative-templates-windows/administrative-templates-all-internet-explorer-settings-device.png)

11. 选择“确定”，保存所做更改。

    继续浏览设置列表，并在环境中配置所需设置。 下面是一些示例：

    - 使用“VBA 宏通知设置”设置，在不同的 Microsoft Office 程序（包括 Word 和 Excel）中处理 VBA 宏。
    - 使用“允许文件下载”设置，允许或阻止从 Internet Explorer 下载。
    - 使用“唤醒计算机时需要密码(接通电源)”，在从睡眠模式唤醒设备时提示用户输入密码。
    - 使用“下载未签名的 ActiveX 控件”设置，阻止用户从 Internet Explorer 下载未签名的 ActiveX 控件。
    - 使用“关闭系统还原”设置，许可或阻止用户在设备上运行系统还原。
    - 使用“允许导入收藏夹”设置，允许或阻止用户将另一个浏览器中的收藏夹导入 Microsoft Edge。
    - 还有更多...

12. 选择“下一步”。
13. 在“作用域标记”（可选）中，分配一个标记以将配置文件筛选到特定 IT 组（如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`）。 有关范围标记的详细信息，请参阅[将 RBAC 和范围标记用于分布式 IT](..//fundamentals/scope-tags.md)。

    选择“下一步”。

14. 在“分配”中，选择将接收配置文件的用户或组。 有关分配配置文件的详细信息，请参阅[分配用户和设备配置文件](device-profile-assign.md)。

    如果将配置文件分配给用户组，则配置的 ADMX 设置将应用于用户注册和登录的任何设备。 如果将配置文件分配给设备组，则配置的 ADMX 设置将应用于登录该设备的任何用户。 如果 ADMX 设置是计算机配置 (`HKEY_LOCAL_MACHINE`) 或用户配置 (`HKEY_CURRENT_USER`)，则会发生此分配。 对于某些设置，分配给用户的计算机设置还可能会影响该设备上其他用户的体验。

    有关详细信息，请参阅[用户组与设备组](device-profile-assign.md#user-groups-vs-device-groups)。

    选择“下一步”。

15. 在“查看并创建”中查看设置。 选择“创建”时，将保存所做的更改并分配配置文件。 该策略也会显示在配置文件列表中。

下次设备检查配置更新时，将应用你配置的设置。

## <a name="find-some-settings"></a>查找某些设置

这些模板提供数千个设置。 为了更容易查找特定设置，请使用内置功能：

- 在模板中，选择“设置”、“状态”、“设置类型”或“路径”列，对列表进行排序。 例如，选择“路径”列，然后使用下一个箭头查看 `Microsoft Excel` 路径中的设置。

- 在模板中，请使用“搜索”框查找特定设置。 可以通过设置或路径进行搜索。 例如，选择“所有设置”，然后搜索 `copy`。 具有 `copy` 的所有设置均会显示：

  > [!div class="mx-imgBorder"]
  > ![搜索 copy 以显示 Intune 管理模板中的所有设备设置](./media/administrative-templates-windows/search-copy-settings.png) 

  在另一个示例中，搜索 `microsoft word`。 随即便可看到可以为 Microsoft Word 程序设置的设置。 搜索 `explorer` 查看可以添加到模板的 Internet Explorer 设置。

- 还可以通过仅选择“计算机配置”或“用户配置”来缩小搜索范围 。

  例如，要查看所有可用的 Internet Explorer 用户设置，请选择“用户配置”，然后搜索 `Internet Explorer`。 仅显示适用于用户的 IE 设置：

  :::image type="content" source="./media/administrative-templates-windows/show-all-internet-explorer-settings-user-configuration.png" alt-text="在 ADMX 模板中，选择“用户配置”，然后在 Microsoft Intune 中搜索或筛选 Internet Explorer。":::

## <a name="next-steps"></a>后续步骤

模板已创建，但它尚未起到任何作用。 接下来，[分配模板（也称为配置文件）](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。

[使用管理模板更新 Microsoft 365](administrative-templates-update-office.md)。

[教程：通过云使用 ADMX 模板和 Microsoft Intune 为 Windows 10 设备配置组策略](tutorial-walkthrough-administrative-templates.md)