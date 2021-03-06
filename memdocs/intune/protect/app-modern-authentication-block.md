---
title: 屏蔽在 Intune 上不使用现代验证的应用
titleSuffix: Microsoft Intune
description: 了解使用 Microsoft Intune 的应用和新式身份验证 (ADAL)。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/22/2020
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.topic: conceptual
ms.technology: ''
ms.assetid: 73db3070-d033-40fb-a8f1-58b9d198021e
ms.reviewer: chrisgre
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, has-adal-ref
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4703288faac219b40fae08c6551425d6f0d5e4f3
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909408"
---
# <a name="block-apps-that-dont-use-modern-authentication-adal"></a>屏蔽不使用新式身份验证 (ADAL) 的应用

> [!NOTE]
> 将弃用 Azure Active Directory (Azure AD) 身份验证库 (ADAL) 和 Azure AD Graph API。 有关详细信息，请参阅[更新应用程序以使用 Microsoft 身份验证库 (MSAL) 和 Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363)。

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

使用应用保护策略且基于应用的条件访问依赖使用[新式身份验证](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a)（即实现 OAuth2）的应用。 目前大部分 Office 移动和桌面应用都使用新式身份验证。 但也有第三方应用和旧版 Office 应用使用其他身份验证方法（如基本身份验证和基于窗体的身份验证）。

## <a name="block-access-to-apps"></a>阻止访问应用

若要阻止访问不使用新式身份验证的应用，请使用 Intune 应用保护策略实现条件访问。 有关详细信息，请参阅[使用 Intune 且基于应用的条件访问](app-based-conditional-access-intune.md)。

## <a name="additional-information"></a>其他信息

有关 Azure AD 条件访问的详细信息，请参阅以下主题：
- [什么是 Azure Active Directory 中的条件访问？](/azure/active-directory/conditional-access/overview)
- [基于应用的条件访问的工作方式](app-based-conditional-access-intune.md#how-app-based-conditional-access-works)
- [为 Azure Active Directory 条件访问设置 SharePoint Online 和 Exchange Online](/azure/active-directory/conditional-access/conditional-access-for-exo-and-spo)

## <a name="next-steps"></a>后续步骤

- [基于应用的 Intune 条件访问](app-based-conditional-access-intune.md)