---
title: 报告的操作和维护
titleSuffix: Configuration Manager
description: 了解管理 Configuration Manager 中的报表和报表订阅的详细信息。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b89bcfbf-f5b6-4fb1-bb5e-a5cc18ec0c78
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 414d1138a7682d6b9acbc7731035fff1842a1fe7
ms.sourcegitcommit: c1afc8abd0d7da48815bd2b0e45147774c72c2df
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2020
ms.locfileid: "87815406"
---
# <a name="operations-and-maintenance-for-reporting-in-configuration-manager"></a>Configuration Manager 中报表的操作和维护

适用范围：  Configuration Manager (Current Branch)

为 Configuration Manager 中的报表准备好基础结构后，通常可以执行多种操作来管理报表和报表订阅。

> [!NOTE]
> 本文重点介绍 SQL Server Reporting Services 中的报表。 从版本 2002 开始，可以将报表与 Power BI 报表服务器集成。 有关详细信息，请参阅[与 Power BI 报表服务器集成](powerbi-report-server.md)。

## <a name="run-a-report-from-reporting-services"></a>从 Reporting Services 运行报表

Configuration Manager 将其报表存储在 SQL Server Reporting Services 中。 报表从 Configuration Manager 站点数据库中检索数据。 你可以在 Configuration Manager 控制台中访问报表，也可以通过 Web 浏览器使用报表管理器进行访问。 在可以访问 Reporting Services 点的任何计算机上通过 Web 浏览器打开报表，且用户需要具有查看报表的足够权限。 若要运行报表，你需要对**站点**权限的**读取**权限，以及针对特定对象的**运行报表**权限。

运行报表时，它以本地操作系统的语言显示报表标题、描述和类别。 有关详细信息，请参阅[报表语言](configuring-reporting.md#-languages-for-reports)。

> [!NOTE]  
> 报表管理器是基于 Web 的报表访问和管理工具。 你可以使用它来通过 HTTPS 连接管理单个报表服务器实例。 使用报表管理器执行操作任务：查看报表、修改报表属性以及管理关联的报表订阅。 本文提供在报表管理器中查看报表和修改报表属性的步骤。 有关报表管理器中的其他选项的详细信息，请参阅[什么是报表管理器？](https://docs.microsoft.com/sql/reporting-services/report-server/manage-a-reporting-services-native-mode-report-server)

使用以下过程运行 Configuration Manager 报表。

### <a name="run-a-report-in-the-configuration-manager-console"></a>在 Configuration Manager 控制台中运行报表

1. 在 Configuration Manager 控制台中，转到“监视”  工作区。 展开“报表”，然后选择“报表”   。 此节点列出可用的报表。

    > [!TIP]
    > 如果此节点未列出任何报表，请验证是否已安装和配置 Reporting Services 点。 有关详细信息，请参阅[配置报表](configuring-reporting.md)。

1. 选择要运行的报表。 在功能区的“主页”选项卡上，在“报表组”部分中，选择“运行”以打开报表    。

1. 如果存在必需的参数，请指定它们，然后选择“查看报表”  。

### <a name="run-a-report-in-a-web-browser"></a>在 Web 浏览器中运行报表

1. 在 Web 浏览器中，转到报表管理器 URL，例如，`https://Server1/Reports`。 在 Reporting Services 配置管理器的“报表管理器 URL”页上找到此地址  。

1. 在报表管理器中，选择 Configuration Manager 的报表文件夹，例如，**ConfigMgr_CAS**。

    > [!TIP]
    > 如果报表管理器未列出任何报表，请验证是否已安装和配置 Reporting Services 点。 有关详细信息，请参阅[配置报表](configuring-reporting.md)。

1. 选择要运行的报表的报表类别，然后选择特定报表。 报表将在报表管理器中打开。

1. 如果存在必需的参数，请指定它们，然后选择“查看报表”  。

## <a name="modify-the-properties-of-a-report"></a>修改报表的属性

报表属性包括报表名称和描述。 可以在 Configuration Manager 控制台中查看报表的属性。

若要更改属性，请使用报表管理器：

1. 在 Web 浏览器中，转到报表管理器 URL，例如，`https://Server1/Reports`。

1. 在报表管理器中，选择 Configuration Manager 的报表文件夹，例如，**ConfigMgr_CAS**。

1. 选择报表类别，然后选择特定报表。 报表将在报表管理器中打开。

1. 选择“属性”选项卡  。修改报表名称和描述，然后选择“应用”  。

报表管理器将报表属性保存在报表服务器上。 Configuration Manager 控制台显示报表的更新报表属性。

## <a name="edit-a-report"></a><a name="bkmk_edit"></a> 编辑报表

如果现有 Configuration Manager 报表未检索所需的信息，请在报表生成器中对其进行编辑。 还可以使用报表生成器更改报表的布局或设计。 虽然可以直接编辑默认报表，但最好将其克隆。 打开要编辑的报表，然后选择“另存为”  。

若要编辑报表，需要对报表中特定对象的**站点修改**权限和**修改报表**权限。

> [!IMPORTANT]
> 站点更新会保留内置报表。 如果修改标准报表，则当站点更新时，它会用下划线前缀 (`_`) 对报表进行重命名。 此行为可以确保站点更新时不会用标准报告覆盖已修改的报表。
>
> 如果修改预定义的报表，则在安装站点更新前，请备份自定义报表。 更新后，在 Reporting Services 中还原报表。 如果对预定义报表进行重大更改，请改为创建新的报表。 不会覆盖在升级站点之前创建的新报表。

使用以下过程来编辑 Configuration Manager 报表的属性。

1. 在 Configuration Manager 控制台中，转到“监视”  工作区。 展开“报表”，然后选择“报表”节点   。

1. 选择要修改的报表。 在功能区的“主页”选项卡上，在“报表组”部分中，选择“编辑”    。 系统可能会提示输入凭据。 如果未在计算机上安装报表生成器，则 Configuration Manager 会提示安装。 需要报表生成器才能修改和创建报表。

1. 在报表生成器中，修改相应的报表设置。 选择“保存”以将报表保存到报表服务器  。

## <a name="create-reports"></a>创建报表

可以创建两种类型的报表：

- **基于模型的报表**使你能够以交互方式选择要包括在报表中的项目。 有关创建自定义报表模型的详细信息，请参阅[在 SQL Server Reporting Services 中为 Configuration Manager 创建自定义报表模型](creating-custom-report-models-in-sql-server-reporting-services.md)。

- **基于 SQL 的报表**使你能够检索基于报表 SQL 语句的数据。

> [!IMPORTANT]
> 若要创建新报表，帐户需要**站点修改**权限。 只能在具有**修改报表**权限的文件夹中创建报表。

### <a name="create-a-model-based-report"></a>创建基于模型的报表

使用以下过程创建基于模型的 Configuration Manager 报表。

1. 在 Configuration Manager 控制台中，转到“监视”工作区，展开“报表”，然后选择“报表”节点    。

1. 在功能区的“主页”选项卡上，在“创建”部分中，选择“创建报表”    。 此操作会打开“创建报表向导”  。

1. 在“信息”  页上，配置下列设置：

    - **类型**：选择“基于模型的报表”  。

    - **名称**：指定报表的名称。

    - **描述**：指定报表的描述。

    - **服务器**：显示在其中创建此报表的报表服务器的名称。

    - **路径**：选择“浏览”以指定要在其中存储报表的文件夹  。

1. 在“模型选择”页上的列表中，选择用于创建此报表的可用模型  。 “预览”部分显示此报表模型中可用的 SQL Server 视图和实体  。

1. 完成“创建报表向导”。

1. 打开报表生成器以配置报表设置。 有关详细信息，请参阅[编辑 Configuration Manager 报表](#bkmk_edit)。

1. 在报表生成器中，创建报表布局、在可用的 SQL Server 视图中选择数据并将参数添加到报表中。

1. 选择“运行”以运行报表  。 验证报表是否提供了预期信息。 如果需要，选择“设计”以进一步修改报表  。

1. 选择“保存”以将报表保存到报表服务器  。

### <a name="create-a-sql-based-report"></a>创建基于 SQL 的报表

为自定义报表创建 SQL 语句时，不要直接引用 SQL Server 表。 始终从站点数据库引用受支持的报表 SQL Server 视图。 这些视图的名称以 `v_` 开头。 有关详细信息，请参阅[在 Configuration Manager 中使用 SQL Server 视图创建自定义报表](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md)。

还可以从站点数据库引用公共存储过程。 这些存储过程的名称以 `sp_` 开头。

使用以下过程创建基于 SQL 的 Configuration Manager 报表。

1. 在 Configuration Manager 控制台中，转到“监视”工作区，展开“报表”，然后选择“报表”节点    。

1. 在功能区的“主页”选项卡上，在“创建”部分中，选择“创建报表”    。 此操作会打开“创建报表向导”  。

1. 在“信息”  页上，配置下列设置：

    - **类型**：选择“基于 SQL 的报表”  。

    - **名称**：指定报表的名称。

    - **描述**：指定报表的描述。

    - **服务器**：显示在其中创建此报表的报表服务器的名称。

    - **路径**：选择“浏览”以指定要在其中存储报表的文件夹  。

1. 完成“创建报表向导”。

1. 打开报表生成器以配置报表设置。 有关详细信息，请参阅[编辑 Configuration Manager 报表](#bkmk_edit)。

1. 在报表生成器中，为报表提供 SQL 语句。 还可以通过使用可用视图中的列来生成 SQL 语句。 如果需要，将参数添加到报表中。

1. 选择“运行”以运行报表  。 验证报表是否提供了预期信息。 如果需要，选择“设计”以进一步修改报表  。

1. 选择“保存”以将报表保存到报表服务器  。

## <a name="manage-report-subscriptions"></a><a name="bkmk_subscription"></a>管理报表订阅

SQL Server Reporting Services 中的报表订阅使你能够配置按计划的间隔通过电子邮件自动交付指定报表或将指定报表自动交付到文件共享。 若要配置报表订阅，请使用 Configuration Manager 中的“创建订阅向导”  。

### <a name="create-a-report-subscription-to-deliver-a-report-to-a-file-share"></a>创建报表订阅以向文件共享传递报表

创建报表订阅以向文件共享传递报表时，Reporting Services 使用指定的格式将报表复制到你指定的文件共享中。 一次只能订阅和请求传递一个报表。

创建使用文件共享的订阅时，将现有共享文件夹指定为目标。 报表服务器不会创建文件夹或网络共享。 在订阅中指定目标文件夹时，请使用 UNC 路径，并且不要在文件夹路径中包含末尾的反斜杠 (`\`)。 以下示例是目标文件夹的有效 UNC 路径：`\\server\reportfiles\operations\2001`。

> [!NOTE]
> 创建订阅时，指定用户名和密码。 此帐户需要对此共享的访问权限以及对目标文件夹的**写入**权限。

Reporting Services 可以采用不同的文件格式呈现报表。 例如，MHTML 或 Excel。 在创建订阅时选择格式。 虽然可以选择任何受支持的呈现格式，但在呈现为文件时，某些格式的效果比另一些好。

### <a name="limitations-for-report-subscriptions-to-a-file-share"></a>文件共享的报表订阅限制

以下列表包括文件共享的报表订阅限制：

- 与在报表服务器上托管和管理的报表不同，Reporting Services 将报表作为静态文件传递到共享文件夹。

- 报表的交互功能不适用于存储为文件的报表。 报表将所有交互功能都表示为静态元素。

- 如果报表包含图表，则使用默认表示形式。

- 如果报表链接到另一个报表，则链接呈现为静态文本。

如果想在传递的报表中保留交互功能，请使用电子邮件传递。 有关详细信息，请参阅[创建报表订阅以通过电子邮件传递报表](#bkmk_subscription-email)。

### <a name="process-to-create-a-report-subscription-for-a-file-share"></a>为文件共享创建报表订阅的过程

使用下列过程来创建向文件共享传递报表的报表订阅。  

1. 在 Configuration Manager 控制台中，转到“监视”工作区，展开“报表”，然后选择“报表”节点    。

1. 选择一个报表文件夹，然后选择要订阅的报表。 在功能区的“主页”选项卡上，在“报表组”部分中，选择“创建订阅”    。 此操作会打开“创建订阅向导”  。

1. 在“订阅传递”  页上，配置下列设置：  

    - **报表传递方式**：选择“Windows 文件共享”  。

    - **文件名**：指定报表的文件名。 默认情况下，报表文件不包含文件扩展名。 选择“创建时添加文件扩展名”，以自动根据格式添加文件扩展名  。

    - **路径**：指定要将此报表传递到的现有文件夹的 UNC 路径。 例如，`\\server\reportfiles\operations`。

    - **呈现格式**：为报表文件选择下列格式之一：

      - **包含报表数据的 XML 文件**
      - **CSV（逗号分隔）**
      - **TIFF 文件**
      - **Acrobat (PDF) 文件**
      - **HTML 4.0**
        > [!NOTE]
        > 如果报表包含图像，则 HTML 4.0 格式不包含这些图像。
      - **MHTML（Web 存档）**
      - **RPL 呈现器**（报表页面布局）
      - **Excel**
      - **Word**

    - **用户名**：指定对指定的**路径**具有*写入*权限的 Windows 用户帐户。

    - **密码**：指定上述 Windows 用户帐户的密码。

    - **覆盖选项**：选择下列选项之一，以配置当目标文件夹中存在同名文件时的行为：

      - **使用较新版本覆盖现有文件**
      - **不覆盖现有文件**
      - **添加较新版本时递增文件名**：此选项在新报表的文件名后追加一个数字，使其与早期版本区分开来。

    - **描述**：（可选）指定有关此报表订阅的其他信息。

1. 在“订阅计划”  页上，为报表订阅选择下列传递计划选项之一：

    - **使用共享计划**：共享计划是以前定义的计划，可以由其他报表订阅使用。 如果选择此选项，另请选择共享计划。 如果没有共享计划，请选择用于创建新计划的选项。

    - **创建新计划**：配置此报表的运行计划。 该计划包括此订阅的间隔、开始时间和日期，以及结束日期。 默认情况下，新订阅会创建新的计划，从当前日期和时间开始每小时运行一次。

1. 在“订阅参数”页上，指定在无人参与的情况下运行此报表时所需的全部参数  。 如果报表没有任何参数，则向导不会显示此页。

1. 完成向导。

1. 验证 Configuration Manager 是否已成功创建报表订阅。 选择“订阅”节点以查看和修改报表订阅  。

### <a name="create-a-report-subscription-to-deliver-a-report-by-email"></a><a name="bkmk_subscription-email"></a>创建报表订阅以通过电子邮件传递报表

在创建报表订阅以通过电子邮件传递报表时，Reporting Services 会向你配置的收件人发送电子邮件。 电子邮件将报表作为附件包含其中。 报表服务器不验证电子邮件地址，也不从电子邮件服务器获取它们。 可以将报表通过电子邮件发送到组织内部或外部的任何有效的电子邮件帐户。

> [!NOTE]
> 若要启用“电子邮件”订阅选项，需要在 Reporting Services 中配置电子邮件设置  。 有关详细信息，请参阅 [Reporting Services 中的电子邮件传递](https://docs.microsoft.com/sql/reporting-services/subscriptions/e-mail-delivery-in-reporting-services)。

可以选择下列一个或全部两个电子邮件传递选项：

- 发送通知和所生成的报表的链接。

- 发送嵌入或附加的报表。 呈现格式和浏览器决定是嵌入还是附加报表。

  - 如果浏览器支持 HTML 4.0 和 MHTML，并选择“MHTML (Web 存档)”格式，则电子邮件将报表嵌入邮件中  。
  - 所有其他格式将报表作为附件传递。
  - Reporting Services 在发送报表前不会检查附件或邮件的大小。 如果附件或邮件超出邮件服务器允许的最大限值，则不会传递报表。

使用下列过程来创建报表订阅，以使用电子邮件传递报表。  

1. 在 Configuration Manager 控制台中，转到“监视”工作区，展开“报表”，然后选择“报表”节点    。

1. 选择一个报表文件夹，然后选择要订阅的报表。 在功能区的“主页”选项卡上，在“报表组”部分中，选择“创建订阅”    。 此操作会打开“创建订阅向导”  。

1. 在“订阅传递”  页上，配置下列设置：  

    - **报表传递方式**：选择“电子邮件”  。

    - **收件人**：指定有效的电子邮件地址作为收件人。

        > [!NOTE]
        > 若要输入多个收件人，请用分号 (`;`) 分隔每个电子邮件地址。

    - **抄送**：（可选）指定要接收此报表副本的电子邮件地址。

    - **密件抄送**：（可选）指定要接收此报表密件副本的电子邮件地址。

    - **回复**：指定回复地址。 如果收件人回复电子邮件，则回复会转到此地址。

    - **主题**：指定订阅电子邮件的主题行。

    - **优先级**：选择此电子邮件的优先级标志：**低**、**普通**或**高**。 Microsoft Exchange 使用此标志指示电子邮件的重要性。

    - **注释**：指定订阅电子邮件的正文文本。

    - **描述**：（可选）指定有关此报表订阅的其他信息。

    - **包括链接**：在电子邮件的正文中包含此报表的 URL。

    - **包括报表**：将报表附加到电子邮件。 使用“呈现格式”选项指定要附加的报表格式  。

    - **呈现格式**：为附加的报表文件选择下列格式之一：

      - **包含报表数据的 XML 文件**
      - **CSV（逗号分隔）**
      - **TIFF 文件**
      - **Acrobat (PDF) 文件**
      - **MHTML（Web 存档）**
      - **Excel**
      - **Word**

1. 在“订阅计划”  页上，为报表订阅选择下列传递计划选项之一：

    - **使用共享计划**：共享计划是以前定义的计划，可以由其他报表订阅使用。 如果选择此选项，另请选择共享计划。 如果没有共享计划，请选择用于创建新计划的选项。

    - **创建新计划**：配置此报表的运行计划。 该计划包括此订阅的间隔、开始时间和日期，以及结束日期。 默认情况下，新订阅会创建新的计划，从当前日期和时间开始每小时运行一次。

1. 在“订阅参数”页上，指定在无人参与的情况下运行此报表时所需的全部参数  。 如果报表没有任何参数，则向导不会显示此页。

1. 完成向导。

1. 验证 Configuration Manager 是否已成功创建报表订阅。 选择“订阅”节点以查看和修改报表订阅  。
