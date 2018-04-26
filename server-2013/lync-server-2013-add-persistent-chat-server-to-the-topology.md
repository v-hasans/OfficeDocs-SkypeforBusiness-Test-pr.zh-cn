﻿---
title: Lync Server 2013：向拓扑添加持久聊天服务器
TOCTitle: 向拓扑添加持久聊天服务器
ms:assetid: 8389b307-8c17-4e45-b3b5-5dc9fcfc2ffb
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ205049(v=OCS.15)
ms:contentKeyID: 49313442
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中向拓扑添加持久聊天服务器

 

_**上一次修改主题：** 2012-10-06_

您必须先将 Lync Server 2013持久聊天服务器支持纳入拓扑中，然后才能将部署配置为支持 持久聊天服务器。本主题中的信息介绍如何使用 拓扑生成器向现有拓扑添加 持久聊天服务器支持。

## 向拓扑添加 持久聊天服务器

执行下列步骤以安装一个没有灾难恢复配置的 持久聊天服务器池。有关为扩展的 持久聊天服务器池配置高可用性和灾难恢复，请参阅部署文档中的 [在 Lync Server 2013 中为持久聊天服务器配置高可用性和灾难恢复](lync-server-2013-configuring-persistent-chat-server-for-high-availability-and-disaster-recovery.md)。

若要部署多个 持久聊天服务器池，请对每个池重复同一过程。

1.  在运行 Lync Server 2013 或在安装了 Lync Server 管理工具的计算机上，使用是本地用户组成员的帐户（或具有等效用户权限的帐户）登录。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可使用是本地用户组成员的帐户定义拓扑，但发布拓扑需要安装 Lync Server 2013 服务器，您必须使用是 <strong>Domain Admins</strong> 组和 <strong>RTCUniversalServerAdmins</strong> 组成员的帐户（其对您将用于 持久聊天服务器文件存储的文件存储具有完全控制权限（即，读取、写入和修改），这样一来 拓扑生成器便可配置所需 DACL）或具有等效权限的帐户。</td>
    </tr>
    </tbody>
    </table>


2.  启动 拓扑生成器。

3.  在控制台树中，导航到“持久聊天池”节点，并将其展开以选择 持久聊天服务器池，或右键单击此节点并选择“新建 持久聊天池”。您必须定义该池的完全限定的域名 (FQDN)，并指示该池是单服务器池部署还是多服务器池部署。
    
    您可选择“多计算机池”或“单计算机池”。如果您计划在 持久聊天服务器池中部署多个 持久聊天服务器前端服务器，请选择前者。现在或稍后做出此选择，因为在创建单计算机池之后，将无法向其添加其他服务器。如果您选择多计算机池，请输入包含池的各个 持久聊天服务器前端服务器的名称。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398794.important(OCS.15).gif" title="important" alt="important" />重要提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果 持久聊天服务器角色将安装在 Lync Server 2013Standard Edition Server上，则 FQDN 需要与 Standard Edition Server的 FQDN 匹配。</td>
    </tr>
    </tbody>
    </table>


4.  为 持久聊天服务器池定义一个简单的 **显示名称** 。自定义客户端可使用此显示名称，特别是在具有多个 持久聊天服务器池时，可使用它来区分聊天室。

5.  定义 持久聊天服务器用来与 Lync Server前端服务器通信的端口。默认端口为 5041。

6.  如果您的组织需要合规性支持，请选中“启用合规性”复选框。如果选中，则将在安装 持久聊天服务器前端服务器的计算机上安装 持久聊天服务器合规性服务。之后系统将提示您为 持久聊天服务器合规性选择 SQL Server后端服务器。

7.  为 持久聊天服务器池分配站点关联。选中“使用此池作为\<站点名称\>的默认池”复选框或“使用此池作为所有站点的默认池”以将此 持久聊天服务器池指定为当前站点或所有站点的默认池。当 Lync 2013 客户端用于创建和管理聊天室时，与用户站点关联的默认池将用于聊天室创建和管理体验，以便让客户端将聊天室创建和管理操作路由到该池。这仅当您部署了多个 持久聊天服务器池并且要使用持久聊天服务器的聊天室创建和管理功能时适用。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398794.important(OCS.15).gif" title="important" alt="important" />重要提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可使用 持久聊天服务器软件开发工具包 (SDK) 自定义聊天室创建和管理功能。<br />
    有关如何为 SQL Server 备份数据库配置灾难恢复的详细信息，请参阅部署文档中的 <a href="lync-server-2013-configuring-persistent-chat-server-for-high-availability-and-disaster-recovery.md">在 Lync Server 2013 中为持久聊天服务器配置高可用性和灾难恢复</a>。</td>
    </tr>
    </tbody>
    </table>


8.  执行下列操作之一以定义“持久聊天服务器后端的 SQL 存储(其中存储聊天室内容)”：
    
      - 若要使用现有 SQL Server 数据库，请在下拉列表中单击要使用的 SQL Server 数据库的名称。
    
      - 若要指定新的 SQL Server 数据库，请单击“新建”，然后在“定义新的 SQL 存储”中，执行下列操作：
    
    <!-- end list -->
    
      - 在“SQL Server FQDN”中，指定要在其上创建新的 SQL Server 数据库的 SQL Server 的 FQDN。
    
      - 选择“默认实例”以使用默认实例，或指定其他实例，选择“命名实例”，然后指定要使用的实例。

9.  如果启用了合规性，则定义 SQL Server 合规性数据库。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398794.important(OCS.15).gif" title="important" alt="important" />重要提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>有关如何配置 SQL Server 镜像以便获得 持久聊天服务器数据库和 持久聊天服务器合规性数据库的高可用性的详细信息，请参阅部署文档中的 <a href="lync-server-2013-configuring-persistent-chat-server-for-high-availability-and-disaster-recovery.md">在 Lync Server 2013 中为持久聊天服务器配置高可用性和灾难恢复</a>。</td>
    </tr>
    </tbody>
    </table>


10. 定义文件存储。文件存储是一个文件夹，其中存储了已上载到文件存储库的所有文件的副本（例如，存储已发布到聊天室的文件附件）。在多服务器 持久聊天服务器拓扑的情况下，文件存储必须是一个通用命名约定 (UNC) 路径；对于单服务器 持久聊天服务器拓扑，文件存储可能是本地文件路径。
    
    若要使用现有文件存储，请执行下列步骤：
    
      - 在“文件服务器 FQDN”中，指定要在其上创建新的文件存储的文件存储的 FQDN。
    
      - 在“文件共享”中，指定要使用的文件存储。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398794.important(OCS.15).gif" title="important" alt="important" />重要提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在创建文件存储之前，您可使用 拓扑生成器定义文件存储，但您必须在发布拓扑前定义的已定义的位置中创建文件存储。</td>
    </tr>
    </tbody>
    </table>


11. 选择要用作此 持久聊天服务器池的下一个跃点的 前端服务器池。这是能够将 持久聊天服务器请求路由到此池的 前端服务器池。

12. 若要保存配置，请单击“完成”。持久聊天服务器池将出现在拓扑生成器中（附带了特定池设置）。
    
    若要立即发布向其添加了 持久聊天服务器的更新的拓扑，请参阅部署文档中的 [在 Lync Server 2013 中发布更新的拓扑](lync-server-2013-publish-the-updated-topology.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn783119.note(OCS.15).gif" title="note" alt="note" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>打开 拓扑生成器后，您可继续 <a href="lync-server-2013-publish-the-updated-topology.md">在 Lync Server 2013 中发布更新的拓扑</a>中的第 3 步开始发布更新的拓扑。</td>
    </tr>
    </tbody>
    </table>
