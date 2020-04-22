---
title: 从 Intune 公司门户网站获取 macOS 设备的恢复密钥
description: 查看已注册的托管 macOS 设备的恢复密钥。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/04/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 5a15f3a05f96333eba19cf69c5778e6c8bd04f59
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "79336753"
---
# <a name="get-a-recovery-key-for-a-macos-device"></a>获取 macOS 设备的恢复密钥

使用公司门户网站获取已锁定 macOS 设备的恢复密钥。 如果忘记了设备密码，可以从另一台设备登录到公司门户以检索密钥。  

## <a name="get-recovery-key-from-company-portal-website"></a>从公司门户网站获取恢复密钥

此选项适用于你的组织使用 FileVault 加密的设备。 它不适用于已进行个人加密的设备。

1. 在任何设备上，登录到[公司门户网站](https://portal.manage.microsoft.com)，然后选择“菜单”按钮 >“设备”   。  
2. 选择加密的 macOS 设备。  
3. 选择“获取恢复密钥”  。  

    ![公司门户网站的屏幕截图，其中突出显示了“获取恢复密钥”部分。](./media/1907-recovery2-cpweb-intune.PNG)  

4. 将显示你的恢复密钥。

    ![公司门户网站的屏幕截图，其中显示了恢复密钥。](./media/1907-recovery-cpweb-intune.PNG)  

    出于安全原因，密钥将在五分钟后消失。 若要再次查看密钥，请选择“获取恢复密钥”  。

如果未找到密钥，但设备已正确加密，请与组织的支持人员联系。 有关联系信息，请查看[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)。  

## <a name="get-recovery-key-from-company-portal-app-for-ios"></a>从 iOS 的公司门户应用获取恢复密钥

可以使用 iOS 的公司门户应用检索个人恢复密钥（FileVault 密钥）。 拥有个人恢复密钥的设备必须已注册 Intune，并且通过 Intune 使用 FileVault 加密。 此选项不适用于已进行个人加密的设备。 

使用公司门户应用，你可以打开 Safari Web 视图并检索个人恢复密钥。 

1. 打开公司门户。
2. 单击“获取恢复密钥”  。

    ![iOS 的公司门户应用的屏幕截图，其中显示了恢复密钥](./media/get-recovery-key-cpweb-02.png)  

公司门户网站将在 Safari Web 视图中打开并显示密钥。 

## <a name="it-pro-support"></a>IT 专业支持

如果你是 IT 支持人员，并且想要为 macOS 设备配置和管理 FileVault 加密，请参阅[结合使用设备加密与 Intune](/intune/protect/encrypt-devices)。

## <a name="next-steps"></a>后续步骤

从公司门户网站了解还可以执行的操作。 若要获取操作列表，请参阅[使用 Intune 公司门户网站](using-the-intune-company-portal-website.md)。  

仍需帮助？ 请与 IT 支持人员联系。 有关联系信息，请查看[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)。  
