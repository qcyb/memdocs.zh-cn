---
title: 注册加入混合 Azure AD 的设备 - Windows Autopilot
titleSuffix: ''
description: 使用 Windows Autopilot 在 Microsoft Intune 中注册加入混合 Azure AD 的设备。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/07/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 8518d8fa-a0de-449d-89b6-8a33fad7b3eb
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2c78b65dc5b4b228df9dc5884adbc75e63c282ef
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907955"
---
# <a name="deploy-hybrid-azure-ad-joined-devices-by-using-intune-and-windows-autopilot"></a>使用 Intune 和 Windows Autopilot 部署加入混合 Azure AD 的设备
可以使用 Intune 和 Windows Autopilot 设置加入混合 Azure Active Directory (Azure AD) 的设备。 为此，请执行本文中的步骤。

## <a name="prerequisites"></a>必备条件

成功配置[加入混合 Azure AD 的设备](/azure/active-directory/devices/hybrid-azuread-join-plan)。 请确保使用 Get-MsolDevice cmdlet [验证注册](/azure/active-directory/devices/hybrid-azuread-join-managed-domains#verify-the-registration)。

要注册的设备还必须：
- 运行的是 Windows 10 v1809 或更高版本。
- 有权访问[遵守记录的 Windows Autopilot 网络要求](/windows/deployment/windows-autopilot/windows-autopilot-requirements#networking-requirements)的 Internet。
- 有权访问 Active Directory 域控制器，因此必须连接到组织的网络（可以在其中解析 AD 域和 AD 域控制器的 DNS 记录，并与域控制器通信以对用户进行身份验证。
- 能够对尝试加入的域的域控制器执行 ping 操作。
- 如果使用代理，必须启用并配置 WPAD 代理设置选项。
- 体验全新体验 (OOBE)。
- 使用在 OOBE 中 Azure Active Directory 支持的身份验证类型。

## <a name="set-up-windows-10-automatic-enrollment"></a>设置 Windows 10 自动注册

1. 登录到 Azure，在左侧窗格中，选择 " **Azure Active Directory**  >  **移动性 (MDM 和 MAM) **"  >  **Microsoft Intune**"。

2. 确保使用 Intune 和 Windows 部署加入 Azure AD 的设备的用户是“MDM 用户范围”中包含的组成员。

   ![“移动性(MDM 和 MAM)配置”窗格](./media/windows-autopilot-hybrid/auto-enroll-scope.png)

3. 在“MDM 使用条款 URL”、“MDM 发现 URL”和“MDM 符合性 URL”框中使用默认值，然后选择“保存”   。

## <a name="increase-the-computer-account-limit-in-the-organizational-unit"></a>增加组织单位中的计算机帐户限制

可使用适用于 Active Directory 的 Intune Connector 在本地 Active 目录域中创建 Autopilot 注册计算机。 托管 Intune Connector 的计算机必须有权在域中创建计算机对象。 

在某些域中，计算机未被授予创建计算机的权限。 此外，域内置有一个限制（默认值为 10），未获得创建计算机对象的委托权限的所有用户和计算机都要遵循此限制。 因此，权限需要委托给在组织单位上托管 Intune 连接器的计算机（组织单位即为创建加入混合 Azure AD 的设备的位置）。

授予创建计算机权限的组织单位必须与以下内容匹配：
- 在域加入配置文件中输入的组织单位。
- 计算机域的域名（如果未选择配置文件）。

1. 打开“Active Directory 用户和计算机(DSA.msc)”。

1. 右键单击将用于创建加入混合 Azure AD 的计算机的组织单位，然后选择“委派控制”。

    ![“委派控制”命令](./media/windows-autopilot-hybrid/delegate-control.png)

1. 在“委派控制”向导中，选择“下一步” > “添加” > “对象类型”   。

1. 在“对象类型”窗格中，选择“计算机”复选框，然后选择“确定”  。

    ![“对象类型”窗格](./media/windows-autopilot-hybrid/object-types-computers.png)

1. 在“选择用户、计算机或组”窗格的“输入要选择的对象名称”框中，输入安装连接器的计算机的名称 。

    ![“选择用户、计算机或组”窗格](./media/windows-autopilot-hybrid/enter-object-names.png)

1. 选择“检查名称”以验证输入，选择“确定”，然后选择“下一步”  。

1. 选择“创建要委派的自定义任务” > “下一步” 。

1. 选择“仅文件夹中的以下对象”复选框，然后选择“计算机对象”、“在本文件夹中创建选定对象”和“在本文件夹中删除选定对象”复选框   。

    ![“Active Directory 对象类型”窗格](./media/windows-autopilot-hybrid/only-following-objects.png)
    
1. 选择“下一步”。

1. 在“权限”下，选择“完全控制”复选框 。  
    此操作将选择所有其他选项。

    ![“权限”窗格](./media/windows-autopilot-hybrid/full-control.png)

1. 选择“下一步”，然后选择“完成” 。

## <a name="install-the-intune-connector"></a>安装 Intune Connector

用于 Active Directory 的 Intune 连接器必须安装在运行 Windows Server 2016 或更高版本的计算机上。 计算机还必须能够访问 Internet 和 Active Directory。 若要增加规模并提高可用性，可在环境中安装多个连接器。 建议在未运行任何其他 Intune 连接器的服务器上安装连接器。  请注意，每个连接器都必须能够在你希望支持的任何域中创建计算机对象。

> [!NOTE]
> 如果你的组织有多个域，但你安装了多个 Intune 连接器，则必须使用能够在所有域中创建计算机对象的服务帐户，即使你计划仅为特定域实现混合 Azure AD 联接也是如此。 如果这些是不受信任的域，则必须从不希望使用 Windows Autopilot 的域中卸载连接器。 否则，在多个域中具有多个连接器，所有连接器都必须能够在所有域中创建计算机对象。

Intune 连接器需要与 [Intune 相同的终结点](../intune/fundamentals/intune-endpoints.md)。

1. 关闭 IE 增强的安全配置。 默认情况下，Windows Server 已打开 Internet Explorer 增强的安全配置。 如果无法登录到用于 Active Directory 的 Intune 连接器，则为管理员关闭 IE 增强的安全配置。 [如何关闭 Internet Explorer 增强的安全配置](/archive/blogs/chenley/how-to-turn-off-internet-explorer-enhanced-security-configuration)。 
2. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“设备” > “Windows” > “Windows 注册” > “适用于 Active Directory 的 Intune 连接器” > “添加”。 
3. 按照说明下载连接器。
4. 打开下载的连接器安装文件 ODJConnectorBootstrapper.exe，安装连接器。
5. 设置结束时，选择“配置”。
6. 选择“登录”。
7. 输入用户全局管理员或 Intune 管理员角色凭据。  
   必须为用户帐户分配 Intune 许可证。
8. 转到“设备” > “Windows” > “Windows 注册” > “适用于 Active Directory 的 Intune 连接器”，然后确认连接状态为“活动”    。

> [!NOTE]
> 登录到连接器之后，可能需要几分钟才能显示在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中。 它只有在能够成功与 Intune 服务通信时才会显示。

### <a name="configure-web-proxy-settings"></a>配置 Web 代理设置

如果网络环境中有 Web 代理，请参阅[使用现有的本地代理服务器](../intune/enrollment/autopilot-hybrid-connector-proxy.md)，确保适用于 Active Directory 的 Intune 连接器正常工作。


## <a name="create-a-device-group"></a>创建设备组
1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“组” > “新建组”。

1. 在“组”窗格中，执行以下操作：

    a. 对于“组类型”，选择“安全组” 。

    b. 输入“组名称”和“组说明” 。

    c. 选择“成员身份类型”。

1. 如果已在“组”窗格中为成员类型选择了“动态设备”，则选择“动态设备成员”，然后在“高级规则”框中执行以下操作之一：   
    - 若要创建包括所有 Autopilot 设备的组，请输入：`(device.devicePhysicalIDs -any _ -contains "[ZTDId]")`。
    - Intune 的“组标记”字段映射到 Azure AD 设备上的 OrderID 属性。 若要创建包括所有具有特定组标记 (OrderID) 的 Autopilot 设备的组，必须键入：`(device.devicePhysicalIds -any _ -eq "[OrderID]:179887111881")`
    - 若要创建包括所有具有特定购买订单 ID 的 Autopilot 设备的组，请输入：`(device.devicePhysicalIds -any _ -eq "[PurchaseOrderId]:76222342342")`。
    
1. 选择“保存”。

1. 选择“创建”。  

## <a name="register-your-autopilot-devices"></a>注册 Autopilot 设备

选择以下方法之一注册 Autopilot 设备。

### <a name="register-autopilot-devices-that-are-already-enrolled"></a>注册已注册的 Autopilot 设备

1. 创建 Autopilot 部署配置文件，将“将所有目标设备转换为 Autopilot”设置为“是” 。 
2. 将配置文件分配给包含要自动注册 Autopilot 的成员的组。

有关详细信息，请参阅[创建 Autopilot 部署配置文件](enrollment-autopilot.md#create-an-autopilot-deployment-profile)。

### <a name="register-autopilot-devices-that-arent-enrolled"></a>注册未注册的 Autopilot 设备

如果设备尚未注册，可以自行注册。 有关详细信息，请参阅[添加设备](enrollment-autopilot.md#add-devices)。

### <a name="register-devices-from-an-oem"></a>从 OEM 注册设备

如果要购买新设备，某些 OEM 可以为你注册设备。 有关详细信息，请参阅 [OEM 注册](add-devices.md#oem-registration)。

Autopilot 设备“已注册”时，在注册到 Intune 之前，它们会显示在三个地方（名称设置为其序列号）：
- Azure 门户中 Intune 中的“Autopilot 设备”窗格。 选择“设备注册” > “Windows 注册” > “设备”  。
- Azure 门户中 Intune 中的“Azure AD设备”窗格。 选择“设备” > “Azure AD 设备” 。
- Azure 门户中 Azure Active Directory 中的“Azure AD 所有设备”窗格，通过选择“设备” > “所有设备”  。

Autopilot 设备“已注册”后，会在四个地方显示：
- Azure 门户中 Intune 中的“Autopilot 设备”窗格。 选择“设备注册” > “Windows 注册” > “设备”  。
- Azure 门户中 Intune 中的“Azure AD设备”窗格。 选择“设备” > “Azure AD 设备” 。
- Azure 门户中 Azure Active Directory 中的“Azure AD 所有设备”窗格。 选择“设备” > “所有设备” 。
- Azure 门户中 Intune 中的“所有设备”窗格。 选择“设备” > “所有设备” 。

Autopilot 设备已注册后，其设备名称成为设备的主机名。 默认情况下，主机名开头为 DESKTOP-。


## <a name="create-and-assign-an-autopilot-deployment-profile"></a>创建并分配 AutoPilot 部署配置文件
Autopilot 部署配置文件用于配置 Autopilot 设备。

1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“设备” > “Windows” > “Windows 注册” > “部署配置文件” > “创建配置文件”。
2. 在“基本信息”页上，键入名称和可选说明  。
3. 如果希望已分配组中的所有设备自动转换为 Autopilot，请把“将所有目标设备转换为 Autopilot”设置为“是” 。 已分配组中的所有公司拥有的非 Autopilot 设备都将注册 Autopilot 部署服务。 个人拥有的设备不会转换为 Autopilot。 等待 48 小时来处理注册。 取消注册设备并重置后，Autopilot 将对其进行注册。 以这种方式注册设备后，禁用此选项或删除配置文件分配将不会从 Autopilot 部署服务中删除该设备。 必须改为[直接删除该设备](enrollment-autopilot.md#delete-autopilot-devices)。
4. 选择“下一步”。
5. 在“全新体验 (OOBE)”页上，对于“部署模式”，选择“用户驱动”。
6. 在“加入到 Azure AD 时的身份”框中，选择“已加入混合 Azure AD” 。
7.  如果是在利用 VPN 支持的组织网络中部署设备，请将“跳过域连接检查”选项设置为“是”。  有关其他信息，请参阅 [具有 VPN 支持的混合 Azure Active Directory 联接的用户驱动模式](user-driven.md#user-driven-mode-for-hybrid-azure-active-directory-join-with-vpn-support) 。
8. 根据需要，在“全新体验 (OOBE)”上配置剩余选项。
9. 选择“下一步”。
10. 在“作用域标记”页上，为此配置文件选择“[作用域标记](../intune/fundamentals/scope-tags.md)”。
11. 选择“下一步”。
12. 在“分配”页上，选择“要包括的组”> 搜索并选择“设备组”>“选择”。
13. 选择“下一步” > “创建”。

设备配置文件的状态从“未分配”更改为“正在分配”，最后更改为“已分配”，此过程大约用时 15 分钟  。

## <a name="optional-turn-on-the-enrollment-status-page"></a>（可选）打开注册状态页

1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“设备” > “Windows” > “Windows 注册” > “注册状态页”。
1. 在“注册状态页”窗格中，选择“默认” > “设置”  。
1. 在“显示应用和配置文件安装进度”中，选择“确定” 。
1. 根据需要配置其他选项。
1. 选择“保存”。

## <a name="create-and-assign-a-domain-join-profile"></a>创建并分配域加入配置文件

1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“设备” > “配置文件” > “创建配置文件”  。
2. 输入以下属性：
   - **名称**：输入新配置文件的描述性名称。
   - **描述**：输入配置文件的说明。
   - **平台**：选择“Windows 10 及更高版本”。
   - **配置文件类型**：选择“域加入(预览版)”。
3. 选择“设置”，然后提供“计算机名前缀”、“域名”。
4. （可选）提供 [DN 格式](/windows/desktop/ad/object-names-and-identities#distinguished-name)的“组织单位”(OU)。 您的选择包括：
   - 提供一个 OU，在其中已将控制权委派给运行 Intune Connector 的 Windows 2016 设备。
   - 提供一个 OU，在其中已将控制权委派给本地 Active Directory 中的根计算机。
   - 如果将此项保留为空白，将在 Active Directory 默认容器中创建计算机对象（如果从未[更改](https://support.microsoft.com/en-us/help/324949/redirecting-the-users-and-computers-containers-in-active-directory-dom)，则 CN=Computers）。
   
   下面是一些有效示例：
   - OU=Level 1,OU=Level2,DC=contoso,DC=com
   - OU=Mine,DC=contoso,DC=com
   
   下面是一些无效示例：
   - CN=Computers,DC=contoso,DC=com（不能指定容器，而是将值保留为空白以使用域的默认值）
   - OU=Mine（必须通过 DC= attributes 指定域）
     
   > [!NOTE]
   > 请勿在组织单位中的值两边使用引号。
5. 选择“确定” > “创建” 。  
    此时，配置文件创建完成，并显示在列表中。
6. 若要分配配置文件，请遵循[分配设备配置文件](../intune/configuration/device-profile-assign.md#assign-a-device-profile)下的步骤进行操作，并将配置文件分配给[创建设备组](windows-autopilot-hybrid.md#create-a-device-group)步骤中所使用的同一组。 或者，如果需要将设备加入不同的域或 OU，可以使用不同的组。

> [!NOTE]
> 对于混合 Azure AD 联接而言，Windows Autopilot 的命名功能不支持 %SERIAL% 等变量，仅支持使用计算机名称前缀。

## <a name="next-steps"></a>后续步骤

配置 Windows Autopilot 后，了解如何管理这些设备。 有关详细信息，请参阅[什么是 Microsoft Intune 设备管理？](../intune/remote-actions/device-management.md)。