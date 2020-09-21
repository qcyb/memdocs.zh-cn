---
title: 准备 Win32 应用以上传到 Microsoft Intune
titleSuffix: ''
description: 了解如何准备 Win32 应用以上传到 Microsoft Intune。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 94626b6cc7e9586ff6b9230206c3e57e6b01b86f
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083791"
---
# <a name="prepare-win32-app-content-for-upload"></a>准备 Win32 应用内容以进行上传

在可以将 Win32 应用添加到 Microsoft Intune 之前，必须使用 [Microsoft Win32 内容准备工具](https://go.microsoft.com/fwlink/?linkid=2065730)来准备应用。

## <a name="prerequisites"></a>必备条件

要使用 Win32 应用管理，请确保满足以下条件：

- 使用 Windows 10 版本 1607 或更高版本（企业版、专业版和教育版）。
- 设备必须加入 Azure Active Directory (Azure AD) 并进行自动注册。 Intune 管理扩展支持已加入 Azure AD、已加入混合域和已注册组策略的设备。 
  > [!NOTE]
  > 对于组策略注册的情况，用户使用本地用户帐户将 Windows 10 设备加入 Azure AD。 用户必须使用其 Azure AD 用户帐户登录设备并注册 Intune。 如果 PowerShell 脚本或 Win32 应用以用户或设备为目标，Intune 将在设备上安装 Intune 管理扩展。
- Windows 应用程序大小的上限为每个应用 8 GB。

## <a name="convert-the-win32-app-content"></a>转换 Win32 应用内容

使用 [Microsoft Win32 内容准备工具](https://go.microsoft.com/fwlink/?linkid=2065730)预处理 Windows 经典 (Win32) 应用。 该工具将应用程序安装文件转换为 .intunewin 格式。 该工具还检测 Intune 所需的某些属性，以确定应用程序安装状态。 在应用安装程序文件夹上使用此工具后，你将能够在 Intune 控制台中创建 Win32 应用。

> [!IMPORTANT]
> [Microsoft Win32 内容准备工具](https://go.microsoft.com/fwlink/?linkid=2065730)在创建 .intunewin 文件时压缩所有文件和子文件夹。 确保将 Microsoft Win32 内容准备工具与安装程序文件和文件夹分开，这样就不会在 .intunewin 文件中包含该工具或其他不必要的文件和文件夹。

可从 GitHub 以 .zip 文件形式下载 [Microsoft Win32 内容准备工具](https://go.microsoft.com/fwlink/?linkid=2065730)。 压缩文件包含名为 Microsoft-Win32-Content-Prep-Tool-master 的文件夹。 该文件夹包含准备工具、许可证、自述文件和发行说明。 

### <a name="process-flow-to-create-a-intunewin-file"></a>.intunewin 文件的创建流程

   <img alt="Flow chart of the process to create a .intunewin file." src="./media/apps-win32-app-management/prepare-win32-app.png" width="700">

### <a name="running-the-microsoft-win32-content-prep-tool"></a>运行 Microsoft Win32 内容准备工具

如果在没有参数的情况下通过命令窗口运行 `IntuneWinAppUtil.exe`，该工具将指导你逐步输入所需参数。 或者，可以根据以下可用命令行参数向命令添加参数。

### <a name="available-command-line-parameters"></a>可用的命令行参数 

|    **命令行参数**    |    **描述**    |
|--------------------------------|------------------------------------------------------------|
|    `-h`     |    帮助    |
|    `-c <setup_folder>`     |    所有安装程序文件的文件夹。 此文件夹中的所有文件将压缩为 .intunewin 文件。    |
|    `-s <setup_file>`     |    安装程序文件（如 setup.exe 或 setup.msi） 。    |
|    `-o <output_folder>`     |    生成的 .intunewin 文件的输出文件夹。    |
|    `-q`       |    静默模式。    |

### <a name="example-commands"></a>示例命令

|    **示例命令**    |    **描述**    |
|-------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `IntuneWinAppUtil -h`    |    该命令将显示工具的使用信息。    |
|    `IntuneWinAppUtil -c c:\testapp\v1.0 -s c:\testapp\v1.0\setup.exe -o c:\testappoutput\v1.0 -q`    |    此命令将从指定的源文件夹和安装文件生成 .intunewin 文件。 对于 MSI 安装文件，此工具将检索 Intune 所需的信息。 如果指定了 `-q`，则该命令将在安静模式下运行。 如果输出文件已存在，则会将其覆盖。 此外，如果输出文件夹不存在，将自动创建该文件夹。    |

生成 .intunewin 文件时，将需要引用的所有文件放入安装程序文件夹的子文件夹中。 然后，使用相对路径引用所需的特定文件。 例如：

**安装程序源文件夹：** c:\testapp\v1.0<br>
**许可文件：** c:\testapp\v1.0\licenses\license.txt

通过使用相对路径 licenses\license.txt 引用 license.txt 文件。

## <a name="next-steps"></a>后续步骤

- [将 Win32 应用添加到 Microsoft Intune](apps-win32-add.md)
