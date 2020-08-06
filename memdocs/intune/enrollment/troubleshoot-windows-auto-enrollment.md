---
title: 在 Intune 中对 Windows 10 自动注册进行故障排除
titleSuffix: Microsoft Intune
description: 了解如何解决有关自动注册的问题。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 8/3/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: jchombe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 968aa9b2f7127e9b7f092f36a99b491a75f0b78c
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546860"
---
# <a name="troubleshoot-windows-10-group-policy-based-auto-enrollment-in-intune"></a>在 Intune 中对基于 Windows 10 组策略的自动注册进行故障排除

可以使用组策略为已加入 Active Directory (AD) 域的设备触发对 MDM 的自动注册。 有关此功能的详细信息，请参阅[通过组策略自动注册 Windows 10 设备](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)。

## <a name="verify-the-configuration"></a>验证配置

在开始故障排除之前，最好验证是否已正确配置所有项。 如果在验证过程中无法解决该问题，则可以通过检查某些重要的日志文件来进一步排查问题。

- 验证有效的 Intune 许可证已分配给尝试注册设备的用户。

   ![验证 Intune 许可证](./media/troubleshoot-windows-auto-enrollment/intune-license.png)

- 验证是否已为将在 Intune 中注册设备的所有用户启用自动注册。 有关更多信息，请参阅 [Azure AD 和 Microsoft Intune：新门户中的自动 MDM 注册](https://docs.microsoft.com/windows/client-management/mdm/azure-ad-and-microsoft-intune-automatic-mdm-enrollment-in-the-new-portal)。

   ![验证自动注册](./media/troubleshoot-windows-auto-enrollment/verify-auto-enrollment.png)

   - 验证“MDM 用户范围”是否设置为“全部”，以允许所有用户在 Intune 中注册设备 。
   - 验证“MAM 用户范围”是否设置为“无” 。 否则，此设置将优先于 MDM 范围并导致问题。
   - 验证“MDM 发现 URL”是否设置为  https://enrollment.manage.microsoft.com/enrollmentserver/discovery 。

- 验证设备是否正在运行 Windows 10 版本 1709 或更高版本。

- 验证是否已将设备设置为“已加入混合 Azure AD” **** 。 此设置表示设备已加入域和 Azure AD。

   若要验证设置，请在命令行中运行 dsregcmd /status。 然后，在输出中验证以下状态值：

   - 设备状态
 
     ```asciidoc
     AzureAdJoined: YES
     DomainJoined: YES
     ```

   - SSO 状态

     ```asciidoc
     AzureAdPrt: YES
     ```

   可以在已加入 Azure AD 的设备列表中找到此信息：

   ![已加入 Azure AD 的设备列表](./media/troubleshoot-windows-auto-enrollment/ad-joined-devices.png)

- Microsoft Intune 和 Microsoft Intune Enrollment 可能都在 Azure AD 边栏选项卡中的“移动性(MDM 和 MAM)”下列出  ****  ****  。 如果两者都存在，请确保在“Microsoft Intune”下配置自动注册设置 **** 。

- 验证以下“组策略”策略设置是否已成功部署到应在 Intune 中注册的所有设备：

   “计算机配置” > “策略” > “管理模板” > “Windows 组件” > “MDM” > “使用默认 Azure AD 凭据启用自动 MDM 注册”

   可以与域管理员联系，以验证是否成功部署了“组策略”策略设置。

- 确保未使用经典电脑代理在 Intune 中注册设备。
- 验证 Azure AD 和 Intune 中的以下设置：

   **在 Azure AD 设备设置中：**

   ![Azure AD 设备设置](./media/troubleshoot-windows-auto-enrollment/device-setting.png)

   - “用户可以将设备加入 Azure AD”设置已设置为“全部” 。
   - 用户在 Azure AD 中拥有的设备数量不超过“每个用户最大设备数”配额。
   
   **在 Intune 注册限制中：**

   - 允许注册 Windows 设备。

     ![允许注册Windows 设备](./media/troubleshoot-windows-auto-enrollment/restrictions.png)

## <a name="troubleshooting"></a>疑难解答

如果问题仍然存在，请在事件查看器中的以下位置检查设备上的 MDM 日志：

“应用程序和服务日志” > “Microsoft” > “Windows” > “DeviceManagement-Enterprise-Diagnostic-Provider” > “管理员”

查找事件 ID 75（事件消息“自动 MDM 注册：已成功”）。 此事件表示自动注册已成功。

在下列情况下，不会记录事件 ID 75：

- 注册失败。

  若要验证此错误，请查找事件 ID 76 （事件消息：自动注册 MDM：失败(未知 Win32 错误代码: 0x8018002b)）。 此事件表示自动注册失败。

  如需此错误的解决方法，请参阅[Microsoft Intune 中的 Windows 设备注册问题疑难解答](https://docs.microsoft.com/intune/troubleshoot-windows-enrollment-errors)。

- 注册根本没有触发。 在这种情况下，不记录事件 ID 75 和事件 ID 76。
  
  自动注册过程由“由注册客户端创建的用于从 AAD 自动注册 MDM 的计划”任务触发，该任务位于任务计划程序的“Microsoft” > “Windows” > “EnterpriseMgmt”下   。

  ![注册未触发](./media/troubleshoot-windows-auto-enrollment/trigger.png)

  此任务在以下情况下创建：“使用默认 Azure AD 凭据启用自动 MDM 注册”组策略策略设置被成功部署到目标设备。 按照计划，此任务在一天内每 5 分钟运行一次。

  若要验证任务是否已启动，请在事件查看器中查看以下位置的任务计划程序事件日志：

  **“应用程序和服务日志”>“Microsoft”>“Windows”>“任务计划程序”>“操作性”**

  任务在计划程序上触发时，事件 ID 107 会被记录。

  任务完成后，事件 ID 102 会被记录。 无论自动注册是否成功，该事件都会被记录。

  > [!NOTE]
  > 可以使用任务计划程序日志来查看是否触发了自动注册。 但是，不能使用日志来确定自动注册是否成功。

  以下情况可能会导致由注册客户端创建的用于从 AAD 任务自动注册 MDM 的计划不启动：

  - 该设备已经在另一个 MDM 解决方案中注册。 在这种情况下，事件 ID 7016 以及错误代码 2149056522 会在“应用程序和服务日志” > “Microsoft” > “Windows” > “任务计划程序” > “操作性”事件日志中记录    。

    若要解决此问题，请从 MDM 取消注册设备。

  - 存在组策略问题。 在这种情况下，可通过运行以下命令强制更新组策略设置：

    **gpupdate /force**

    如果问题仍然存在，请在 Active Directory 中执行其他故障排除操作。

## <a name="next-steps"></a>后续步骤
[Windows 设备注册疑难解答](troubleshoot-windows-enrollment-errors.md)