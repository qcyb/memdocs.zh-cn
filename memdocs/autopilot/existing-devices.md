---
title: 适用于现有设备的 Windows Autopilot 部署
description: 利用 Windows Autopilot 的新式桌面部署，你可以轻松地将 Windows 10 的最新版本部署到现有的设备。
keywords: mdm, 设置, windows, windows 10, oobe, 管理, 部署, autopilot, ztd, 零接触, 合作伙伴, msfb, intune
ms.reviewer: mniehaus
manager: laurawi
ms.prod: w10
ms.technology: windows
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 685466a9760fa8aa688e76b10e1f44b7ac9eb37e
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643561"
---
# <a name="windows-autopilot-deployment-for-existing-devices"></a>适用于现有设备的 Windows Autopilot 部署

**适用于：Windows 10**

采用 Windows Autopilot 的新式桌面部署可帮助你轻松地将 Windows 10 的最新版本部署到现有设备。 可以自动安装所需的工作应用。 你的工作配置文件已同步，因此你可以立即开始工作。

本主题介绍如何使用 Windows Autopilot 将已加入域的 Windows 7 或 Windows 8.1 的已加入域的计算机转换到加入到 Azure Active Directory 或 Active Directory (混合 Azure AD 联接) 的 Windows 10 设备。

>[!NOTE]
>Windows Autopilot for 现有设备仅支持用户驱动的 Azure Active Directory 和混合 Azure AD 配置文件。 不支持自部署配置文件。

## <a name="prerequisites"></a>先决条件

- 当前支持的 Microsoft Endpoint 版本 Configuration Manager 当前分支或 technical preview 分支。 
- [WINDOWS ADK](https://developer.microsoft.com/en-us/windows/hardware/windows-assessment-deployment-kit) 1803 或更高版本
    - 有关 Configuration Manager 支持的详细信息，请参阅 [对 Windows 10 ADK 的支持](/configmgr/core/plan-design/configs/support-for-windows-10#windows-10-adk)。
- 分配 Microsoft Intune 许可证
- Azure Active Directory Premium
- Windows 10 1809 版或更高版本导入 Configuration Manager 为操作系统映像
  - **重要说明**：如果将 windows 10 1903 与 Configuration Manager 的内置**Windows Autopilot 现有设备**任务序列模板结合使用，请参阅[已知问题](known-issues.md)。 当前，必须编辑此任务序列中的某个步骤，以便在 Windows 10 版本1903上正常工作。

## <a name="procedures"></a>过程

### <a name="configure-the-enrollment-status-page-optional"></a>配置 "注册状态" 页 (可选) 

如果需要，可以使用 Intune 为 Autopilot 设置 [注册状态页](enrollment-status.md) 。

若要启用和配置 "注册和状态" 页：

1. [在 Azure 门户中打开 Intune](https://aka.ms/intuneportal)。
2. 访问 **Intune > 设备注册 > Windows 注册** 并 [设置注册状态页](/intune/windows-enrollment-status)。 
3. 访问 **Azure Active Directory > 移动 (MDM 和 MAM) >** Microsoft Intune 并 [配置自动 mdm 注册](/configmgr/mdm/deploy-use/enroll-hybrid-windows#enable-windows-10-automatic-enrollment) ，并为部分或所有用户配置 mdm 用户作用域。 

请参阅以下示例。

![注册状态页](images/esp-config.png)<br><br>
![mdm](images/mdm-config.png)

### <a name="create-the-json-file"></a>创建 JSON 文件 

>[!TIP]
>若要在运行 Windows Server 2012/2012 R2 或 Windows 7/8.1 的计算机上运行以下命令，你必须首先下载并安装 [Windows Management Framework](https://www.microsoft.com/download/details.aspx?id=54616)。

1. 在连接 Internet 的 Windows 电脑或服务器上，打开提升的 Windows PowerShell 命令窗口
2. 输入以下行来安装所需的模块

    #### <a name="install-required-modules"></a>安装所需的模块

    ```powershell
    Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force
    Install-Module AzureAD -Force
    Install-Module WindowsAutopilotIntune -Force
    Install-Module Microsoft.Graph.Intune -Force
    ```
   
3. 输入以下行并提供 Intune 管理凭据：
   - 确保您指定的用户帐户具有足够的管理权限。

     ```powershell
     Connect-MSGraph
     ```
     将使用标准 Azure AD 表单请求帐户的用户和密码。 键入用户名和密码，并单击 " **登录**"。 
     <br>请参阅以下示例：

     ![Azure AD 身份验证](images/pwd.png)

     如果这是你第一次使用 Intune Graph Api，系统将提示你启用 Microsoft Intune PowerShell 读取和写入权限。 若要启用这些权限：
   - **代表或你的组织选择同意**
   - 单击 "**接受**"

4. 接下来，检索并显示指定的 Intune 租户中可用的 JSON 格式的所有 Autopilot 配置文件：

    #### <a name="retrieve-profiles-in-autopilot-for-existing-devices-json-format"></a>检索现有设备的 Autopilot 中的配置文件 JSON 格式

    ```powershell
    Get-AutopilotProfile | ConvertTo-AutopilotConfigurationJSON
    ```

    请参阅以下示例输出： (使用底部的水平滚动条来查看长行) 
    <pre style="overflow-y: visible">
    PS C:\> Get-AutopilotProfile | ConvertTo-AutopilotConfigurationJSON
    {
        "CloudAssignedTenantId": "1537de22-988c-4e93-b8a5-83890f34a69b",
        "CloudAssignedForcedEnrollment": 1,
        "Version": 2049,
        "Comment_File": "Profile Autopilot Profile",
        "CloudAssignedAadServerData": "{\"ZeroTouchConfig\":{\"CloudAssignedTenantUpn\":\"\",\"ForcedEnrollment\":1,\"CloudAssignedTenantDomain\":\"M365x373186.onmicrosoft.com\"}}",
        "CloudAssignedTenantDomain": "M365x373186.onmicrosoft.com",
        "CloudAssignedDomainJoinMethod": 0,
        "CloudAssignedOobeConfig": 28,
        "ZtdCorrelationId": "7F9E6025-1E13-45F3-BF82-A3E8C5B59EAC"
    }</pre>

    每个配置文件都封装在大括号 **{}** 中。 在上面的示例中，将显示单个配置文件。

    有关 JSON 文件中使用的属性的说明，请参阅下表。


   |                          properties                          |                                                                                                                                                                        说明                                                                                                                                                                         |
   |------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |                 版本 (号，可选)                  | 标识 JSON 文件格式的版本号。 对于 Windows 10 1809，指定的版本必须为2049。                                                                                                                  |
   |           CloudAssignedTenantId (guid，必需)            | 应使用的 Azure Active Directory 租户 ID。 此属性是租户的 GUID，可在租户的属性中找到。 此值不应包含大括号。                                                                                       |
   |        CloudAssignedTenantDomain (字符串，必需)         | 应使用的 Azure Active Directory 租户名称，例如： tenant.onmicrosoft.com。                                                                                                                                  |
   |         CloudAssignedOobeConfig (号，必需)          | 此属性是一个位图，用于显示配置了哪些 Autopilot 设置。 值包括： SkipCortanaOptIn = 1、OobeUserNotLocalAdmin = 2、SkipExpressSettings = 4、SkipOemRegistration = 8、SkipEula = 16                                                                           |
   |      CloudAssignedDomainJoinMethod (号，必需)       |                                                                                                                                    此属性指定设备是否应联接 Azure Active Directory 或 Active Directory (混合 Azure AD 联接) 。 值包括： Active AD Join = 0，混合 Azure AD 联接 = 1                                                        |
   |      CloudAssignedForcedEnrollment (号，必需)       |                                                                                                                         指定设备应该需要 Azure AD 联接和 MDM 注册。 <br>0 = 不需要，1 = 必选。                                                                                                                         |
   |             ZtdCorrelationId (guid，必需)               | 在注册过程中将提供给 Intune 的唯一 GUID (不包含大括号) 。 ZtdCorrelationId 将作为 "OfflineAutoPilotEnrollmentCorrelator" 包含在注册消息中。 仅当注册是在通过脱机注册使用零接触设置注册的设备上进行注册时，此属性才会出现。 |
   | CloudAssignedAadServerData (编码的 JSON 字符串，必需)  |                                                  用于品牌的嵌入 JSON 字符串。 它要求启用了公司品牌 Azure AD。 <br> 示例值： "CloudAssignedAadServerData"： "{ \" ZeroTouchConfig \" ： { \" CloudAssignedTenantUpn \" ： \" \" ， \" CloudAssignedTenantDomain \" ： \" tenant.onmicrosoft.com \" }}"                                                   |
   |         CloudAssignedDeviceName (字符串，可选)          | 自动分配给计算机的名称。 这遵循 Intune Autopilot 配置文件中配置的命名模式约定。 或者，您可以指定要使用的显式名称。 |


5. 必须将 Autopilot 配置文件另存为 ASCII 或 ANSI 格式的 JSON 文件。 Windows PowerShell 默认为 Unicode 格式。 因此，如果将命令的输出重定向到文件，还需要指定文件格式。 例如，若要使用 Windows PowerShell 将文件保存为 ASCII 格式，你可以创建 (ex： c:\Autopilot) 的目录，并保存配置文件，如下所示： (在需要时使用水平滚动条来查看整个命令字符串) 

    ```powershell
    Get-AutopilotProfile | ConvertTo-AutopilotConfigurationJSON | Out-File c:\Autopilot\AutopilotConfigurationFile.json -Encoding ASCII
    ```
    **重要说明**：文件名必须命名为 **AutopilotConfigurationFile.js** ，并编码为 ASCII/ANSI。 

    如果需要，你可以将配置文件保存到文本文件并在记事本中进行编辑。 在记事本中，如果选择 " **另存为** "，则必须选择 "另存为类型： **所有文件** "，然后从 " **编码**" 旁的下拉列表中选择 "ANSI"。 请参阅以下示例。

    ![记事本 JSON](images/notepad.png)

    保存该文件后，将该文件移动到一个位置，该位置 Configuration Manager 包源。

    >[!IMPORTANT]
    >可以使用多个 JSON 配置文件文件，但每个文件都必须命名为 **AutopilotConfigurationFile.js** ，以便 OOBE 遵循 Autopilot 体验。 文件也必须编码为 ANSI。 <br><br>**使用 Unicode 或 utf-8 编码保存文件，或使用不同的文件名保存该文件将导致 Windows 10 OOBE 不遵循 Autopilot 体验**。<br>


### <a name="create-a-package-containing-the-json-file"></a>创建包含 JSON 文件的包

1. 在 Configuration Manager 中，导航到 **\Software Library\Overview\Application Management\Packages**
2. 在功能区上，单击 "**创建包**"
3. 在 " **创建包和程序向导** " 中，输入以下 **包** 和 **程序类型** 详细信息：<br>
    - <u>名称</u>： **用于现有设备配置的 Autopilot**
    - 选中“此包包含源文件”****。
    - <u>源文件夹</u>：单击 " **浏览** " 并指定包含文件 AutopilotConfigurationFile.js的 UNC 路径。 
    - 单击 **“确定”**，然后单击 **“下一步”**。
    - <u>程序类型</u>： **不创建程序**
4. 单击**下一步**两次，然后单击**关闭**。

**注意**：如果以后在 Intune 中更改用户驱动的 Autopilot 配置文件设置，则还必须更新 JSON 文件并重新分发关联的 Configuration Manager 包。

### <a name="create-a-target-collection"></a>创建目标集合

>[!NOTE]
>还可以选择重复使用现有集合

1. 导航到 **\Assets 和 Compliance\Overview\Device 集合**
2. 在功能区上，单击 "**创建**"，然后单击 "**创建设备集合**"
3. 在 " **创建设备集合向导** " 中输入以下 **常规** 详细信息：
   - <u>名称</u>： **Autopilot 用于现有设备集合**
   - Comment： (可选) 
   - <u>限制集合</u>：单击 "**浏览**" 并选择 "**所有系统**"

     >[!NOTE]
     >您可以选择为限制集合使用替代集合。 要升级的设备必须在所选集合中运行 ConfigMgr 代理。

4. 单击 " **下一步**"，然后输入以下 **成员身份规则** 详细信息：
   - 单击 " **添加规则** "，指定直接或基于查询的集合规则，将目标测试 Windows 7 设备添加到新集合。
   - 例如，如果要擦除和重新加载计算机的主机名为 PC 01，并且你想要使用名称作为属性：
      1. 单击 " **添加规则 > 直接规则" > (向导将打开) ">**"。
      2. 在 "**值**" 旁边输入**PC-01** 。
      3. 单击**Next**  >  "**资源**) 下的" 下一**电脑-01** ("。 请参阅以下示例。

         !["查找资源" 对话框 " ](images/pc-01a.png)
          ![ 选择资源" 对话框](images/pc-01b.png)

5. 继续用默认设置创建设备集合：
    - 对此集合使用增量更新：未选择
    - 对此集合计划完全更新：默认值
    - 单击 "**下一步**" 两次，然后单击 "**关闭**"

### <a name="create-an-autopilot-for-existing-devices-task-sequence"></a>为现有设备创建 Autopilot 任务序列

>[!TIP]
>下一过程需要 Windows 10 1803 或更高版本的启动映像。 在 " **Software Library\Overview\Operating Systems\Boot images** " 下的 Configuration Manager 由中查看可用的启动映像，并验证 **OS 版本** 是否 (Windows 10 版本 1803) 或更高版本。

1. 在 Configuration Manager 控制台中，导航到 **\Software Library\Overview\Operating Systems\Task 序列**
2. 在 "主页" 功能区上，单击 "**创建任务序列**"
3. 选择 "**安装现有的映像包**"，然后单击 "**下一步**"
4. 在 "创建任务序列向导" 中，输入以下详细信息：
   - <u>任务序列名称</u>： **适用于现有设备的 Autopilot**
   - <u>启动映像</u>：单击 " **浏览** " 并选择 Windows 10 启动映像 (1803 或更高版本) 
   - 单击 "**下一步**"  >  **浏览**> 选择 Windows 10**映像包**和**映像索引**版本1803或更高版本。
   - 选择 "在 **安装操作系统之前对目标计算机进行分区和格式化** " 复选框。
   - 选中或清除 " **配置任务序列以与 BitLocker 一起使用** " 复选框。 该地址为可选。
   - <u>产品密钥</u> 和 <u>服务器授权模式</u>：根据需要输入产品密钥和服务器授权模式。
   - <u>随机生成本地管理员密码并禁用所有支持平台上的帐户 (建议) </u>：可选。
   - <u>启用帐户并指定本地管理员密码</u>：可选。
   - 单击 " **下一步**"，然后在 "配置网络" 页上选择 " **加入工作组** "，并指定名称 (Ex： workgroup) **workgroup**。

     > [!IMPORTANT]
     > Autopilot for 现有设备任务序列将运行 " **准备 Windows for capture** " 操作，该操作使用系统准备工具 (sysprep) 。 如果目标计算机已加入域，则此操作将失败。
     
     >[!IMPORTANT]
     > 系统准备工具 (sysprep) 将用/Generalize 参数运行，在 Windows 10 版本1903和1909上，该参数将删除 Autopilot 配置文件，并且计算机将启动到 OOBE 阶段，而不是 Autopilot 阶段。 若要解决此问题，请参阅 [Windows Autopilot 的已知问题](known-issues.md)。

5. 单击 " **下一步**"，然后再次单击 " **下一步** " 以接受 "安装 Configuration Manager" 页上的默认设置。
6. 在 "状态迁移" 页上，输入以下详细信息：
   - 清除 " **捕获用户设置和文件** " 复选框。
   - 清除 " **捕获网络设置** " 复选框。
   - 清除 " **捕获 Microsoft Windows 设置** " 复选框。
   - 单击“下一步”。 

     >[!NOTE]
     >由于 Autopilot for 现有设备任务序列在 Windows PE 中完成，因此不支持用户状态迁移 (工具包) 数据迁移，因为无法将用户状态还原到新 OS。 此外，用户状态迁移工具包 (USMT) 不支持 Azure AD 加入的设备。

7. 在 "包括更新" 页上，选择三个可用选项之一。 此选项是可选的。
8. 在 "安装应用程序" 页上，可以选择添加应用程序。
9. 单击 " **下一步**"，确认设置，单击 " **下一步**"，然后单击 " **关闭**"
10. 右键单击 "Autopilot for 现有设备" 任务序列，然后单击 " **编辑**"。
11. 在 " **安装操作系统** " 组下的 "任务序列编辑器" 中，单击 " **应用 Windows 设置** " 操作。
12. 单击 " **添加** "，然后单击 " **新建组**"。
13. 将组 **名称** 从 " **新组** " 更改为 " **现有设备的 Autopilot" 配置**。
14. 单击 " **添加**"，指向 " **常规**"，然后单击 " **运行命令行**"。
15. 验证 " **运行命令行** " 步骤是否嵌套在 " **适用于现有设备的 Autopilot" 配置** 组下。
16. 更改 " **名称** " 若要 **为现有设备配置文件应用 Autopilot**，请将以下内容粘贴到 " **命令行** " 文本框中 > **应用**：
    ```
    cmd.exe /c xcopy AutopilotConfigurationFile.json %OSDTargetSystemDrive%\windows\provisioning\Autopilot\ /c
    ```
    - **AutopilotConfigurationFile.js"** 必须是前面创建的" 现有设备的 Autopilot 中存在的 JSON 文件的名称 "。

17. 在 "**为现有设备应用 Autopilot 配置文件**" 步骤中，选择**包**  >  **浏览**。
18. 选择前面创建 **的现有设备配置** 包的 Autopilot，然后单击 **"确定"**。 本部分末尾显示了一个示例。
19. 在 " **设置** " "操作系统" 组下，单击 " **安装 Windows 和 Configuration Manager** " 任务。
20. 单击 " **添加** "，然后单击 " **新建组**"。
21. 将 **名称** 从 **新组** 更改为 **Autopilot 的准备设备**
22. 验证 Autopilot 组的 **Prepare 设备** 是否为任务序列中的最后一步。 如有必要，请 **使用 "下移** " 按钮。
23. 选择 " **准备设备以进行 Autopilot** " 组后，单击 " **添加**"，指向 " **映像** "，然后单击 " **准备 ConfigMgr 客户端以便捕获**"。
24. 单击 " **添加**"，指向 " **映像**"，然后单击 " **准备 Windows 以便捕获**"，添加第二步。 在此步骤中使用以下设置：
    - <u>自动生成大容量存储驱动程序列表</u>： **未选择**
    - <u>不重置激活标志</u>： **未选择**
    - <u>运行此操作后关闭计算机</u>： **可选**

    ![Autopilot 任务序列](images/ap-ts-1.png)

25. 单击 **"确定"** 关闭任务序列编辑器。

> [!NOTE]
> 在 Windows 10 1903 和1909上，"**准备 Windows For Capture** " 步骤删除了**AutopilotConfigurationFile.js** 。 有关详细信息和解决方法，请参阅 [Windows Autopilot 的已知问题](known-issues.md)。

### <a name="deploy-content-to-distribution-points"></a>将内容部署到分发点

接下来，请确保将任务序列所需的所有内容部署到分发点。

1. 右键单击 " **Autopilot for 现有设备** " 任务序列，然后单击 " **分发内容**"。
2. 单击 " **下一步**"， **查看要分发的内容**，然后单击 " **下一步**"。
3. 在 "指定内容分发" 页面上，单击 " **添加** " 以指定 **分发点** 或 **分发点组**。
4. 在 "添加分发点或添加分发点组向导" 中，指定允许任务序列检索 JSON 文件的内容目标。
5. 完成指定内容分发后，单击 " **下一步** " 两次，然后单击 " **关闭**"。

### <a name="deploy-the-os-with-autopilot-task-sequence"></a>通过 Autopilot 任务序列部署 OS

1. 右键单击 " **Autopilot for 现有设备** " 任务序列，然后单击 " **部署**"。
2. 在 "部署软件" 向导中，输入以下**常规****设置和部署设置**详细信息：
    - <u>任务序列</u>： **Autopilot 用于现有设备**。
    - <u>集合</u>：单击 " **浏览** "，然后选择 " **现有设备的 Autopilot" 集合** (或其他你喜欢) 的集合。
    - 单击 " **下一步** " 以指定 **部署设置**。
    - <u>操作</u>： **安装**。
    - <u>目的</u>： **可用**。 您可以选择 " **必需** " 而不是 " **可用**"。 不建议在测试期间使用此设置，因为无意间配置可能会产生负面影响。
    - <u>适用于以下各</u>项： **仅 Configuration Manager 客户端**。 注意：在此处选择与测试上下文相关的选项。 如果目标客户端未安装 Configuration Manager 代理或 Windows，则必须选择包括 PXE 或启动媒体的选项。
    - 单击 " **下一步** " 以指定 **计划** 详细信息。
    - <u>计划此部署将在何时变为可用</u>：可选
    - <u>计划此部署将在何时过期</u>：可选
    - 单击 " **下一步** " 以指定 **用户体验** 详细信息。
    - <u>显示任务序列进度</u>：已选择。
    - <u>软件安装</u>：未选择。
    - <u>如果需要，系统重新启动 (完成安装) </u>：未选中。
    - <u>在截止时间或在维护时段内更改提交 (需要重启) </u>：可选。
    - <u>允许对 Internet 上的客户端运行任务序列</u>：可选
    - 单击 " **下一步** " 以指定 **警报** 详细信息。
    - <u>当阈值高于以下值时创建部署警报</u>：可选。
    - 单击 " **下一步** " 以指定 **分发点** 详细信息。
    - <u>部署选项</u>： **运行任务序列需要时在本地下载内容**。
    - <u>当没有本地分发点可用时，请使用远程分发点</u>：可选。
    - <u>允许客户端使用默认站点边界组中的分发点</u>：可选。
    - 单击 " **下一步**"，确认设置，单击 " **下一步**"，然后单击 " **关闭**"

### <a name="complete-the-client-installation-process"></a>完成客户端安装过程

1. 在目标 Windows 7 或 Windows 8.1 客户端计算机上，选择 "启动 > 键入 **软件中心** " > 按 enter。

2. 在软件库中，选择 " **Autopilot" 作为 "现有设备** "，然后单击 " **安装**"。 请参阅以下示例：

    !["为现有设备 Autopilot ](images/sc.png) ![ " 页确认对话框](images/sc1.png)

任务序列将：
1. 下载内容
2. 重新启动设备
3. 格式化驱动器
4. 安装 Windows 10
5. 准备 Autopilot

任务序列完成后，设备将启动到 OOBE，并提供 Autopilot 体验。

![刷新-1 ](images/up-1.png)
 ![ 刷新-2 ](images/up-2.png)
 ![ 刷新-3](images/up-3.png)

>[!NOTE]
>如果将设备加入到 Active Directory (混合 Azure AD 联接) ，则需要创建一个针对 "所有设备" 的域加入设备配置配置文件，因为该计算机没有 (的设备对象来执行基于组的目标 Azure Active Directory。 有关详细信息，请参阅 [混合 Azure Active Directory 联接的用户驱动模式](user-driven.md#user-driven-mode-for-hybrid-azure-active-directory-join)。

### <a name="register-the-device-for-windows-autopilot"></a>为 Windows Autopilot 注册设备

仅在首次启动时，通过 Autopilot 预配的设备接收引导式 OOBE Autopilot 体验。 更新到 Windows 10 后，确保注册该设备，使其在电脑重置时具有 Autopilot 体验。 你可以使用 " **将所有目标设备转换为 Autopilot** " 设置为分配的组启用自动注册。 有关详细信息，请参阅[创建 Autopilot 部署配置文件](enrollment-autopilot.md#create-an-autopilot-deployment-profile)。

另请参阅向 [Windows Autopilot 添加设备](add-devices.md)。

## <a name="speeding-up-the-deployment-process"></a>加速部署过程

若要从部署过程中删除20分钟左右，请参阅 Michael Niehaus 的博客，其中包含有关 [加快现有设备的 Windows Autopilot 的](/archive/blogs/mniehaus/speeding-up-windows-autopilot-for-existing-devices)说明。
