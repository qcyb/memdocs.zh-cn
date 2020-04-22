---
title: 更新和停用应用程序
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 修订、取代或卸载部署的应用程序。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 68ac8a07-8e54-4a3c-91e3-e50dc1cabf5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7770f1db0e311186a908890dc339401ed3cbeb4b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689885"
---
# <a name="update-and-retire-applications-with-configuration-manager"></a>使用 Configuration Manager 更新和停用应用程序

适用范围：  Configuration Manager (Current Branch)


最后，用户可能希望更改、卸载应用程序，或者将已部署的应用程序替换为新的应用程序。 Configuration Manager 可为用户提供这些功能，帮助更新和停用应用程序：  

- **修订应用程序**。 对应用程序或部署类型进行更改时，Configuration Manager 将维护这些更改的历史记录。 你可以随时将应用程序还原到以前的修订版本。 也可以查看其属性、还原应用程序的以前版本或删除旧版本。  

  有关详细信息，请参阅[应用程序修订](revise-and-supersede-applications.md#application-revisions)。  

- **取代应用程序**。 可通过使用取代相关来替换或升级现有应用程序。 取代应用程序时，可以指定新的部署类型来替换被取代应用程序的部署类型。 另外，还可决定安装取代应用程序前，是否升级或卸载被取代应用程序。  

  有关详细信息，请参阅[应用程序取代](revise-and-supersede-applications.md#application-supersedence)。  

- **卸载应用程序**。 Configuration Manager 可轻松卸载应用程序。 此操作可以在在无提示的情况下完成，而不需要应用程序或设备用户干预。  

  有关详细信息，请参阅[卸载应用程序](uninstall-applications.md)。  
