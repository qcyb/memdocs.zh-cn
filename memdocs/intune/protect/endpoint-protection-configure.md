---
title: 在 Microsoft Intune 中配置终结点保护设置 - Azure | Microsoft Docs
description: 在 Microsoft Intune 中创建 macOS 或 Windows 10 设备配置文件时，创建终结点保护设置。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: karthib
ms.openlocfilehash: 6b5d0f88222c8d48da4f91ff3cf8d4628ccb179d
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "80551576"
---
# <a name="add-endpoint-protection-settings-in-intune"></a>在 Intune 中添加终结点保护设置

使用 Intune，可以使用设备配置文件来管理设备上的公共终结点保护安全功能，包括：

- 防火墙
- BitLocker
- 允许和阻止应用
- Microsoft Defender 和加密

例如，可以创建一个终结点保护配置文件，仅允许 macOS 用户安装来自 Mac App Store 的应用。 或者在 Windows 10 设备上运行应用时启用 Windows SmartScreen。

在创建配置文件之前，请查看详细介绍 Intune 可以针对每个支持平台管理的终结点保护设置的以下文章：

- [macOS 设置](endpoint-protection-macos.md)
- [Windows 10 设置](endpoint-protection-windows-10.md)

> [!NOTE]
> Intune 用户界面 (UI) 正在更新为提供全屏体验，可能需要数周时间才能完成。 在租户收到此更新之前，创建或编辑本文所述的设置时的工作流将略有不同。

## <a name="create-a-device-profile-containing-endpoint-protection-settings"></a>创建包含终结点保护设置的设备配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“设备”   > “配置文件”   > “创建配置文件”  。

3. 输入以下属性：

    - **平台**：选择设备平台。 选项包括：

        - **macOS**
        - **Windows 10 及更高版本**

    - **配置文件**：选择“Endpoint Protection”  。

4. 选择“创建”。 
5. 在“基本信息”  中，输入以下属性：

    - **名称**：输入策略的描述性名称。 为策略命名，以便稍后可以轻松地识别它们。 例如，策略名称最好是“macOS：配置登录屏幕”**为所有 macOS 设备配置防火墙的 Endpoint Protection 配置文件**。
    - **描述**：输入策略的说明。 此设置是可选的，但建议进行。

6. 选择“下一步”  。

7. 在“配置设置”  中，根据所选择的平台，可配置的设置有所不同。 选择平台，以了解详细设置：

   - [macOS 设置](endpoint-protection-macos.md)
   - [Windows 10 设置](endpoint-protection-windows-10.md)

8. 选择“下一步”  。
9. 在“作用域标记”（可选）中，分配一个标记以将配置文件筛选到特定 IT 组（如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`）  。 有关范围标记的详细信息，请参阅[将 RBAC 和范围标记用于分布式 IT](../fundamentals/scope-tags.md)。

    选择“下一步”  。

10. 在“分配”中，选择将接收配置文件的用户或组  。 有关分配配置文件的详细信息，请参阅[分配用户和设备配置文件](../configuration/device-profile-assign.md)。

    选择“下一步”  。

11. 在“查看并创建”中查看设置  。 选择“创建”时，将保存所做的更改并分配配置文件  。 该策略也会显示在配置文件列表中。

## <a name="add-custom-firewall-rules-for-windows-10-devices"></a>为 Windows 10 设备添加自定义防火墙规则

在将 Microsoft Defender 防火墙配置为包含 Windows 10 终结点保护规则的配置文件的一部分后，可以为防火墙配置自定义规则。 通过自定义规则，可以扩展 Windows 10 支持的预定义防火墙规则集。

在计划使用带自定义防火墙规则的配置文件时，请考虑以下信息，这些信息可能会影响在配置文件中对防火墙规则进行分组的方式：

- 每个配置文件最多支持 150 个防火墙规则。 使用超过 150 个规则时，请创建其他配置文件，每个配置文件限制为 150 个规则。

- 对于每个配置文件，如果单个规则无法使用，则该配置文件中的所有规则都无法使用，并且不会将任何规则应用于设备。

- 如果某个规则无法使用，则配置文件中的所有规则都将报告为无法使用。 Intune 无法识别哪个单独的规则无法使用。  

Windows [防火墙配置服务提供程序](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) (CSP) 中详细介绍了 Intune 可以管理的防火墙规则。 若要查看 Intune 支持的 Windows 10 设备自定义防火墙设置列表，请参阅[自定义防火墙规则](endpoint-protection-windows-10.md#firewall-rules)。

### <a name="to-add-custom-firewall-rules-to-an-endpoint-protection-profile"></a>向 Endpoint Protection 配置文件添加自定义防火墙规则

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“设备”   > “配置文件”   > “创建配置文件”  。

3. 对于“平台”，选择“Windows 10 及更高版本”，对于“配置文件”，选择“Endpoint Protection”     。

    选择“创建”。 

4. 输入配置文件的“名称”>“下一步”   。
5. 在“配置设置”中，选择“Microsoft Defender 防火墙”   。 对于“防火墙规则”，选择“添加”以打开“创建规则”页面    。

6. 指定“防火墙规则”的设置，然后选择“确定”以保存该设置  。 若要查看文档中可用的自定义防火墙规则选项，请参阅[自定义防火墙规则](endpoint-protection-windows-10.md#firewall-rules)。

    1. 规则将显示在规则列表中的“Microsoft Defender 防火墙”页上  。
    2. 若要修改规则，请从列表中选择规则，以打开“编辑规则”页  。
    3. 若要从配置文件中删除规则，请选择规则的省略号“(…)”，然后选择“删除”  。
    4. 若要更改规则的显示顺序，请选择规则列表顶部的向上箭头、向下箭头图标  。

7. 选择“下一步”，直到看到“查看 + 创建”   。 选择“创建”时，将保存所做的更改并分配配置文件  。 该策略也会显示在配置文件列表中。

## <a name="next-steps"></a>后续步骤

此时，配置文件创建完成，但它可能尚未执行任何操作。 下一步，[分配配置文件](../configuration/device-profile-assign.md)并[监视其状态](../configuration/device-profile-monitor.md)。
