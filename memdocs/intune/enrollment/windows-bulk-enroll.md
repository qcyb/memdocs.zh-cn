---
title: Windows 10 的批量注册
titleSuffix: Microsoft Intune
description: 为 Microsoft Intune 创建批量注册包
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 5/21/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1f39c02a-8d8a-4911-b4e1-e8d014dbce95
ms.reviewer: spshumwa
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6d50d7f8e4edeaf6d88875fafef977936909d71f
ms.sourcegitcommit: 532a06163f462527254d23e7dc505b18c0c4f938
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/11/2020
ms.locfileid: "88110726"
---
# <a name="bulk-enrollment-for-windows-devices"></a>Windows 设备的批量注册

作为管理员，可以将大量新的 Windows 设备加入到 Azure Active Directory 和 Intune。 若要为你的 Azure AD 租户批量注册设备，可以使用 Windows 配置设计器 (WCD) 应用来创建配置包。 将配置包应用于企业拥有的设备可将设备加入到你的 Azure AD 租户并为其注册 Intune 管理。 应用此包后，即可供你的 Azure AD 用户登录。

Azure AD 用户是这些设备上的标准用户并接收分配的 Intune 策略和必需的应用。 使用 Windows 批量注册注册到 Intune 的 Windows 设备可以使用公司门户应用安装可用的应用。 

## <a name="prerequisites-for-windows-devices-bulk-enrollment"></a>Windows 设备批量注册的先决条件

- 运行 Windows 10 创意者更新（内部版本 1709）或更高版本的设备
- [Windows 自动注册](windows-enroll.md#enable-windows-10-automatic-enrollment)

## <a name="create-a-provisioning-package"></a>创建预配包

1. 从 Microsoft 应用商店下载 [Windows 配置设计器 (WCD)](https://www.microsoft.com/p/windows-configuration-designer/9nblggh4tx22)。
   ![Windows 配置设计器应用商店的屏幕截图](./media/windows-bulk-enroll/bulk-enroll-store.png)

2. 打开“Windows 配置设计器”  应用，然后选择“配置桌面设备”  。
   ![在 Windows 配置设计器应用中选择配置桌面设备的屏幕快照](./media/windows-bulk-enroll/bulk-enroll-select.png)

3. 此时，“新项目”  窗口打开，在其中指定以下信息：
   - **名称** - 你的项目的名称
   - **项目文件夹** - 项目的保存位置
   - **说明** - 项目的可选说明![在 Windows 配置设计器应用中指定名称、项目文件夹和说明的屏幕快照](./media/windows-bulk-enroll/bulk-enroll-name.png)

4. 输入设备的唯一名称。 名称可以包含序列号 (%SERIAL%) 或一组随机字符。 （可选）如果正在升级 Windows 版本，还可以输入产品密钥、将设备配置为共享以及删除预安装的软件。
   
   ![一张屏幕截图，显示在 Windows 配置设计器应用中指定名称和产品密钥](./media/windows-bulk-enroll/bulk-enroll-device.png)

5. （可选）可以配置 Wi-Fi 网络设备首次启动时所连接到的网络。  如果未配置网络设备，在设备首次启动时必须建立有线网络连接。
   ![在 Windows 配置设计器应用中启用包括网络 SSID 和网络类型选项的 Wi-Fi 的屏幕快照](./media/windows-bulk-enroll/bulk-enroll-network.png)

6. 选择“在 Azure AD 中注册”  ，输入“批量令牌到期”  日期，然后选择“获取批量令牌”  。
   ![Windows 配置设计器应用中的帐户管理屏幕截图](./media/windows-bulk-enroll/bulk-enroll-account.png)

7. 提供你的 Azure AD 凭据，以获取批量令牌。
   ![Windows 配置设计器应用的登录屏幕截图](./media/windows-bulk-enroll/bulk-enroll-cred.png)

8. 在“在此设备上的所有位置使用此帐户”页上，选择“仅限此应用”   。

9. 成功提取“批量令牌”  后，单击“下一步”  。

10. （可选）可以“添加应用程序”  和“添加证书”  。 将在此设备上配置应用和证书。

11. （可选）还可以使用密码保护你的配置包。  单击 **“创建”** 。
    ![Windows 配置设计器应用中的包保护屏幕截图](./media/windows-bulk-enroll/bulk-enroll-create.png)

## <a name="provision-devices"></a>配置设备

1. 在应用中所指定的“项目文件夹”  中访问指定位置的配置包。

2. 选择向设备应用预配程序包的方式。  可使用以下方法之一向设备应用配置包：
   - 将预配程序包置于 USB 驱动器中，将 USB 驱动器插入要进行批量注册的设备，并在初始设置时应用它
   - 将预配程序包置于网络文件夹中，并在初始设置后应用它

   有关应用配置包的分步说明，请参阅[应用配置包](https://technet.microsoft.com/itpro/windows/configure/provisioning-apply-package)。

3. 在包得到应用后，设备便会在一分钟内自动重启。
   ![在 Windows 配置设计器应用中指定名称、项目文件夹和说明的屏幕快照](./media/windows-bulk-enroll/bulk-enroll-add.png)

4. 设备重新启动时，将连接到 Azure Active Directory 并在 Microsoft Intune 中注册。

## <a name="troubleshooting-windows-bulk-enrollment"></a>Windows 批量注册的疑难解答

### <a name="provisioning-issues"></a>设置问题
配置旨在用于新的 Windows 设备上。 预配失败可能需要对设备进行擦除或通过启动映像来恢复设备。 这些示例描述了配置失败的一些原因：

- 如果因为缺少网络连接导致域加入过程失败，则尝试加入 Active Directory 域或不创建本地帐户的 Azure Active Directory 租户的配置包可能会使设备无法访问。
- 预配包运行的脚本在系统上下文中运行。 脚本能够对设备文件系统和配置进行任意更改。 恶意或不正确的脚本可将设备置于仅能通过重置映像或擦除才能将其恢复的状态。

可以在“事件查看器”中的“预配-诊断-提供程序”管理日志中查看包中的设置的成功/失败  。

### <a name="bulk-enrollment-with-wi-fi"></a>批量注册到 Wi-Fi 

如果未使用开放网络，则必须使用[设备级证书](../protect/certificates-configure.md)来启动连接。 批量注册的设备无法使用面向用户的证书来访问网络。 

### <a name="conditional-access"></a>条件性访问
条件访问不适用于使用批量注册方式注册的 Windows 设备（Windows 10 1803+ 除外）。
