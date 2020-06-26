---
title: 如何使用文档
titleSuffix: Configuration Manager
description: 了解关于使用 Configuration Manager 技术文档库的技巧。
ms.date: 04/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b3d755bd-0870-4f1f-a56d-bfd3c7b492b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 31f9b1cb083400abd36858a177e87804a916362c
ms.sourcegitcommit: 7a099ff53668f50b37adab97ecd7ba98c5324676
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2020
ms.locfileid: "84746505"
---
# <a name="how-to-use-the-configuration-manager-docs"></a>如何使用 Configuration Manager 文档

适用范围：Configuration Manager (Current Branch)

本文提供有关使用 Configuration Manager 文档库的资源和提示。

- 如何搜索
- 提交文档的 bug、增强功能、问题和新想法
- 如何获取更改通知
- 如何参与编辑文档

有关产品的常规帮助，请参阅[查找帮助](find-help.md)。

## <a name="search"></a><a name="bkmk_searchtips"></a> 搜索

使用以下搜索提示可帮助你找到需要的信息：

- 在使用首选搜索引擎查找 Configuration Manager 的内容时，请同时使用 `ConfigMgr` 和搜索关键字。

  - 请从 `docs.microsoft.com/mem/configmgr` 查找 Configuration Manager Current Branch 的结果。 `docs.microsoft.com/previous-versions` 的结果适用于较旧的产品版本。

  - 若要进一步将搜索结果集中到当前内容库，请包含 `site:docs.microsoft.com` 以限定搜索引擎的范围。

- 使用和用户界面以及在线文档中的术语相匹配的搜索词。 避免使用可能在社区内容中见过的非正式术语或缩写。 例如，搜索：

  - “管理点 (management point)”而不是“MP”
  - “部署类型 (deployment type)”而不是“DT”
  - “软件更新 (software updates)”而不是“SUM”

- 若要在当前文章中进行搜索，请使用浏览器的“查找”功能。 对于大多数新式 Web 浏览器，请按 Ctrl+F，然后输入搜索词 。

- `docs.microsoft.com` 上的每篇文章都包括以下字段，可帮助搜索内容：

  - 右上角的“搜索”。 若要在所有文章中进行搜索，请在此字段中输入搜索词。 Configuration Manager 库中的文章自动包含 `ConfigMgr` 范围，以便仅搜索此文档库。

  - 左侧目录上方的“按标题筛选”。 若要对当前目录进行搜索，请在此字段中输入搜索词。 此字段仅匹配出现在当前节点的文章标题中的搜索词。 例如，**核心基础结构 (Core Infrastructure)** (`docs.microsoft.com/configmgr/core`) 或 **应用程序管理 (Application Management)** (`docs.microsoft.com/configmgr/apps`)。

- 查找时遇到问题？ [提供反馈！](#bkmk_docfeedback) 提出问题时，请提供使用的搜索引擎、尝试搜索的关键字以及目标文章。 此反馈有助于 Microsoft 优化内容以实现更好的搜索。

> [!TIP]
> 从 Configuration Manager 1902 版开始，Configuration Manager 控制台的新“社区”工作区包含“文档”节点 。 此节点包含有关 Configuration Manager 文档和支持文章的最新信息。 有关详细信息，请参阅[使用 Configuration Manager 控制台](../servers/manage/admin-console.md#bkmk_doc-dashboard)。

## <a name="feedback"></a><a name="bkmk_docfeedback"></a> 反馈

选择任意文章右上方的“反馈”链接，转到底部的“反馈”部分。 此部分与 GitHub 问题集成。 有关与 GitHub 问题集成的详细信息，请参阅[文档平台博客文章](https://docs.microsoft.com/teamblog/a-new-feedback-system-is-coming-to-docs)。

若要分享有关 Configuration Manager 产品本身的反馈，请选择“产品反馈”。 有关详细信息，请参阅[产品反馈](find-help.md#product-feedback)。

[GitHub 帐户](https://github.com/join)是提供文档反馈的先决条件。 用户登录后，会获得 MicrosoftDocs 组织的一次性授权。 然后，选择“内容反馈”，输入标题和评论，再单击“提交反馈” 。 此操作可为 [SCCMdocs 存储库](https://github.com/MicrosoftDocs/SCCMdocs/issues)中的目标文章提出一个新问题。

此集成还显示目标文章的任何现有未解决的问题或已关闭的问题。 如果存在任何此类问题，请在提交新问题之前先查看这些问题。 如果发现相关问题，请选择人脸图标以添加回应，或者可展开添加评论。

#### <a name="types-of-feedback"></a>反馈类型

使用 GitHub 问题提交以下反馈类型：

- 文档 bug：内容过期、不清楚、令人混淆或不完整。
- 文档增强功能：改善文章的建议。
- 文档问题：查找现有文档时需要帮助。
- 文档想法：撰写新文章的建议。 使用此方法代替 UserVoice 提供文档反馈。
- 称赞：关于有用或信息性文章的积极反馈！
- 本地化：关于内容翻译的反馈。
- 搜索引擎优化 (SEO)：关于搜索内容时所遇到的问题的反馈。 在评论中包含搜索引擎、关键字和目标文章。

如果为非文档相关主题创建问题，Microsoft 将关闭这些问题。 例如：

- [产品反馈](find-help.md#product-feedback)
- [产品问题](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)
- [支持请求](https://aka.ms/cmcbsupport)

若要分享有关 docs.microsoft.com 基本平台的反馈，请参阅[文档反馈](https://aka.ms/sitefeedback)。 该平台包含所有包装组件，如标题、目录和右侧菜单。 以及文章在浏览器中的呈现方式，如字体、警报框和页面书签。

## <a name="notifications"></a><a name="bkmk_notifications"></a> 通知

若要在文档库中的内容更改时接收通知，请使用以下步骤：

1. 使用[文档搜索](https://docs.microsoft.com/search/index?scope=ConfigMgr)查找一篇文章或一组文章。 例如：

    - 按标题[“故障排除的日志文件 - Configuration Manager (Log files for troubleshooting - Configuration Manager)”](https://docs.microsoft.com/search/index?search=%22Log+files+for+troubleshooting+-+Configuration+Manager%22&scope=ConfigMgr)搜索单篇文章

    - 搜索有关 [SQL](https://docs.microsoft.com/search/index?search=SQL&scope=ConfigMgr) 的任何文章

2. 在右上角选择“RSS”链接。

3. 在任何 RSS 应用程序中使用此源接收有关任何搜索结果发生更改的通知。

> [!TIP]
> 也可在 GitHub 上监视 [SCCMdocs 存储库](https://github.com/MicrosoftDocs/SCCMdocs)。 此方法会生成许多通知。 但其中不包括 Microsoft 使用的专用存储库中的更改。

## <a name="contribute"></a><a name="bkmk_contribute"></a> 参与

与 docs.microsoft.com 上的大多数内容一样，Configuration Manager 文档库在 GitHub 上也是使用开放源代码编写的。 此库接受并鼓励社区参与。 有关如何参与的详细信息，请参阅[参与者指南](https://docs.microsoft.com/contribute)。 唯一的先决条件是创建 [GitHub 帐户](https://github.com/join)。

### <a name="basic-steps-to-contribute-to-sccmdocs"></a>参与编辑 SCCM 文档的基本步骤

1. 从目标文章中，选择“编辑”。 此操作可在 GitHub 中打开源文件。

2. 若要编辑源文件，请选择铅笔图标。

3. 在 Markdown 源中进行更改。 有关详细信息，请参阅 [How to use Markdown for writing Docs](https://docs.microsoft.com/contribute/markdown-reference)（如何使用 Markdown 编写文档）。

4. 在“建议文件更改”部分中，输入描述已更改内容的公开提交评论。 然后选择“建议文件更改”。

5. 向下滚动然后验证所做的更改。 选择“创建拉取请求”以打开窗体。 描述进行此更改的原因。 标记文章作者并请求他们查看。 选择“创建拉取请求”。

### <a name="what-to-contribute"></a>要参与的内容

如果想要参与但不知道从何处着手，请参阅以下建议：

- 搜索针对社区的标签的问题列表：

  - [精选问题](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:good-first-issue)
  - [需要帮助](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:help-wanted)  

    Microsoft 作者会将这些标签分配给适合社区贡献的候选问题。

- 查看文章以确保准确性。 然后使用 `mm/dd/yyyy` 格式更新 ms.date 元数据。 此贡献有助于内容保持最新状态。

- 根据经验添加说明、示例或指导。 此贡献借助社区的力量共享知识。

- 以非英语语言更正翻译。 此贡献可提高本地化内容的可用性。

> [!NOTE]
> 如果你不是 Microsoft 员工，那么对于较大的贡献，需要签署贡献许可协议 (CLA)。 当贡献达到阈值，GitHub 会自动要求你签署此协议。

### <a name="tips"></a>提示

参与 Configuration Manager 文档时，请遵循以下通用准则：

- 不要使用大型拉取请求来制造惊喜。 相反，请[提出问题](#bkmk_docfeedback)并开始讨论。 然后，在你投入大量时间之前，我们会就某个方向表示同意。

- 阅读 [Microsoft 风格指南](https://aka.ms/MicrosoftStyle)。 了解[有关 Microsoft 风格和语态的前 10 个提示](https://docs.microsoft.com/style-guide/top-10-tips-style-voice)。

- 使用[拉取请求模板](https://github.com/MicrosoftDocs/SCCMdocs/blob/master/PULL_REQUEST_TEMPLATE.md)作为工作的起始点。

- 请按照 [GitHub 流工作流](https://guides.github.com/introduction/flow/)操作。

- 会经常推出有关你发布内容的博客和推文（或任何内容）！

（此列表借用自 [.NET 参与指南](https://github.com/dotnet/docs/blob/master/CONTRIBUTING.md#dos-and-donts)。）

## <a name="consolidation-of-documentation-for-microsoft-endpoint-manager"></a>Microsoft 终结点管理器的文档整合

为了更好地支持 Intune 和 Configuration Manager 的组合方案，它们的文档库已合并到 [Microsoft Endpoint Manager 站点](https://docs.microsoft.com/mem)上。 Intune 文档现在位于 [docs.microsoft.com/mem/intune](https://docs.microsoft.com/mem/intune)，Configuration Manager 文档现在位于 [docs.microsoft.com/mem/configmgr](https://docs.microsoft.com/mem/configmgr)。 如果你仍在使用旧的 URL，它会自动重定向，因此你无需进行任何更改就能读到此内容。

如果向文章提供反馈或做出贡献，则需要进行一些更改：

- 现有 GitHub 问题仍然保留在原始存储库 [IntuneDocs](https://github.com/MicrosoftDocs/IntuneDocs/issues) 或 [SCCMDocs](https://github.com/MicrosoftDocs/SCCMDocs/issues) 中。

  - 这些问题不会在链接文章的反馈部分中显示为开放或关闭的问题。

  - 我们将继续努力解决这些问题。

  - 在某些情况下，我们可能会做出艰难决定，关闭我们认为无法解决的问题。

  - 如果你有问题在现有存储库中并对它充满热情，请在 [MEMDocs 存储库](https://github.com/MicrosoftDocs/MEMDocs)中就已迁移的文章提供反馈。

- 现在，当你提交反馈或编辑文章时，问题或拉取请求会进入到 MEMDocs 存储库。
