1.  在 Configuration Manager 控制台中，转到“软件库”工作区，然后选择“软件更新”节点   。  

2.  使用以下方法之一选择要下载的软件更新：  

    -   从“软件更新组”节点中选择一个或多个软件更新组  。 然后，单击功能区中的“下载”  。  

    -   从“所有软件更新”节点中选择一个或多个软件更新  。 然后，单击功能区中的“下载”  。  

        > [!NOTE]  
        >  在“所有软件更新”节点中，Configuration Manager 只显示分类为“严重”和“安全”并且已在过去 30 天内发布的软件更新    。  

        > [!TIP]  
        >  单击“添加条件”以筛选“所有软件更新”节点中显示的软件更新   。 保存经常使用的搜索条件，然后在“搜索”选项卡中管理已保存的搜索  。  


3.  在“下载软件更新向导”的“部署包”页面上，配置以下设置  ：  

    -  “选择部署包”  ：选择此设置以为部署中的软件更新选择现有部署包。  

        > [!NOTE]  
        >  不会重新下载站点已经下载到所选部署包的软件更新。  

    -  “创建新部署包”  ：选择此设置以为部署中的软件更新创建新部署包。 配置下列设置：  

        -   “名称”  ：指定部署包的名称。 此包必须具有简要描述包内容的唯一名称。 限制为不超过 50 个字符。  

        -   说明  ：指定提供有关该部署包的信息的说明。 可选说明限制为不超过 127 个字符。    

        -   包源  ：指定软件更新源文件的位置。 键入源位置的网络路径（例如 `\\server\sharename\path`），或单击“浏览”以查找网络位置  。 在进入到下一页之前，为部署包源文件创建共享文件夹。  

             - 不能将指定的位置用作另一软件部署包的源。  

             - 在 Configuration Manager 创建部署包之后，可在部署包属性中更改包源位置。 如果执行此操作，请先将原始包源中的内容复制到新的包源位置。  

             -  SMS 提供程序的计算机帐户和运行向导以下载软件更新的用户都必须具有对下载位置的“写入”  权限。 限制对下载位置的访问。 此限制可降低攻击者篡改软件更新源文件的风险。  

        - **启用二进制差异复制**：启用此设置可最大程度减少站点之间的网络流量。 二进制差异复制 (BDR) 仅更新包中已更改的内容，而不是更新整个包内容。 有关详细信息，请参阅[二进制差异复制](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication)。  

4.  在“分发点”页面上，指定用于托管软件更新文件的分发点或分发点组  。 有关分发点的详细信息，请参阅 [分发点配置](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs)。 只有当你在创建新的软件更新部署包时才能使用本页。  

5.  只有在创建新的软件更新部署包时才能使用“分发设置”页面  。 指定以下设置：  

    -   “分发优先级”  ：使用此设置以指定部署包的分发优先级。 将部署包发送到子站点中的分发点时，将应用分发优先级。 部署包按高、中或低这三个优先级顺序进行发送。 具有相同优先级的包按照其创建顺序发送。 如果没有积压工作 (backlog)，则立即处理包，而不考虑优先级。 默认情况下，站点会发送优先级为**中**的包。  

    -   **启用按需分发**：使用此设置可启用按需内容分发，以分发到为此功能配置的分发点和客户端当前边界组中的分发点。 如果启用此设置，管理点会为分发管理器创建一个触发器，以便在客户端请求包的内容且内容不可用时将内容分发到所有此类分发点。 有关详细信息，请参阅[按需内容分发](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution)。  

    -   “预留分发点设置”  ：使用此设置以指定希望将内容分发到预留分发点的方式。 选择下列选项之一：  

        -   “在将包分配到分发点时自动下载内容”  ：使用此设置以忽略预留设置，并将内容分发到分发点。   

        -   “仅下载对分发点所做的内容更改”  ：使用此设置以将初始内容预留到分发点，然后将内容更改分发到分发点。  

        -   “手动将此包中的内容复制到分发点”  ：使用此设置以始终在分发点上预留内容。 此选项为默认设置。  

        有关将内容预留到分发点的详细信息，请参阅 [使用预留内容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage)。  


6.  在“下载位置”页面上，指定 Configuration Manager 用于下载软件更新源文件的位置  。 使用以下选项之一：  

    -   **从 Internet 下载软件更新**：选择此设置可从 Internet 上的位置下载软件更新。 此选项为默认设置。  

    -   **从我网络上的位置下载软件更新**：选择此设置可从本地目录或共享文件夹下载软件更新。 运行向导的计算机无法访问 Internet 时，此设置很有用。 任何具有 Internet 访问的计算机都可预先下载软件更新。 然后，将其存储在可从运行向导的计算机访问的本地网络上的某个位置中。  


7.  在“语言选择”页面上，选择站点按哪种语言下载所选的软件更新  。 只有所选语言提供更新时，站点才能下载这些更新。 非语言特定的软件更新可随时下载。 默认情况下，向导会选择你已在软件更新点属性中配置的语言。 在继续进入下一页之前，必须选择至少一种语言。 只选择软件更新不支持的语言时，无法下载更新。  

8. 在“摘要”  页上，验证在向导中选择的设置，然后单击“下一步”  以下载软件更新。  

9. 在“完成”  页上，验证软件更新是否已成功下载，然后单击“关闭”  。  
