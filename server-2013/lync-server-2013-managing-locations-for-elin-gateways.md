﻿---
title: Lync Server 2013：管理 ELIN 网关的位置
TOCTitle: 管理 ELIN 网关的位置
ms:assetid: ced79c13-4e7e-4034-95cd-6fc913f4f222
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ205288(v=OCS.15)
ms:contentKeyID: 49314293
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中管理 ELIN 网关的位置

 

_**上一次修改主题：** 2016-12-08_

要让 Lync Server 自动为网络内的客户端提供位置，需要执行以下任务：

  - 用网络线路映射填充 位置信息服务数据库，并将紧急位置标识号 (ELIN) 包括在 CompanyName 字段中。

  - 发布位置，以供网络中的客户端使用。

  - 将 ELIN 上载到公用电话交换网 (PSTN) 运营商的自动位置标识 (ALI) 数据库。

有关如何执行这些任务的详细信息，请参阅部署文档中的 [在 Lync Server 2013 中配置位置数据库](lync-server-2013-configure-the-location-database.md)。

> [!NOTE]  
> 在使用 Lync Server 命令行管理程序命令发布已添加到中央位置数据库的位置，并将这些位置复制到池的本地存储之前，这些位置对于客户端不可用。有关详细信息，请参阅部署文档中的 <a href="lync-server-2013-publish-the-location-database.md">发布位置数据库</a>。



本节介绍在计划更新和维护位置数据库时要考虑的事项。

## 规划紧急位置

使用 ELIN 网关时，对于每个位置，用市政地址、建筑物内的具体位置以及至少一个 ELIN 填充 位置信息服务数据库。在规划阶段，最好决定想要如何命名位置和分配 ELIN。

## 规划位置名称

位置信息服务**Location** 字段保存建筑物内的具体位置，最大长度为 20 个字符（包括空格）。在该限制长度内，尽量包括以下内容：

  - 一个容易理解的名称，用于标识 911 呼叫者的位置，以确保紧急响应者在到达市政地址后能迅速找到具体位置。此位置名称可包含建筑物编号、楼层、建筑物标识、房间号等。应避免使用仅对员工可知的昵称，以防紧急响应者去往错误的位置。

  - 一个位置标识符，帮助用户轻松查看其 Lync 客户端选择正确位置。Lync 客户端会自动合并发现的 **Location** 和 **City** 字段并在其标头中显示这两个字段。最好将建筑物的街道地址添加到每个位置标识符（如“1st Floor \<street number\>”）。如果没有街道地址，可能对城市中的任何建筑物都应用常规位置标识符，如“1st Floor”。

  - 如果位置是一个大概位置（因为它是由无线访问点决定的），您可能需要添加词 Near（例如，“Near 1st Floor 1234”）。

## 规划 ELIN

在您决定想要如何将建筑物空间分成多个位置后，需要决定为每个位置分配多少个 ELIN。例如，在多层或多租户建筑物中，可以为建筑物中不同的区域分配不同的紧急区域。通常，建筑物的每层都会被指定为一个位置。每个位置会被分配一个或多个 ELIN，这些 ELIN 用作紧急呼叫时的呼叫号码。请联系您的 PSTN 运营商以获得可用于 ELIN 的电话号码。下表提供了特定街道地址的位置示例。

### 位置和 ELIN 分配示例

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>建筑物区域</th>
<th>位置</th>
<th>ELIN</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>第一层</p></td>
<td><p>1</p></td>
<td><p>425-555-0100</p></td>
</tr>
<tr class="even">
<td><p>第二层</p></td>
<td><p>2</p></td>
<td><p>425-555-0111</p></td>
</tr>
<tr class="odd">
<td><p>第三层</p></td>
<td><p>3</p></td>
<td><p>425-555-0123</p></td>
</tr>
</tbody>
</table>


您定义的位置应满足以下要求：

  - 在每位置最大区域和每街道地址位置数方面符合当地和国家/地区法规。

  - 足够详细到能够轻松找到紧急呼叫者。

## 填充位置数据库

以下问题将帮助您确定如何填充位置数据库。

  - **使用什么过程填充位置数据库？**  
    数据位于何处？需要采取何种步骤将数据转换为位置数据库所需的格式？是逐个添加位置，还是使用 CSV 文件批量添加？

<!-- end list -->

  - **是否具有已包含位置映射的第三方数据库？**  
    通过使用 Lync Server 的辅助 位置信息服务选项连接到第三方数据库，可以使用脱机平台组合和管理位置。除了将位置与网络标识符关联外，此方法的优点还在于将位置与用户关联。这意味着 位置信息服务可返回从辅助 位置信息服务到 Lync Server 客户端的多个地址。然后，用户可以选择最适合的位置。
    
    若要与 位置信息服务集成，第三方数据库必须遵循 Lync Server 位置请求/响应架构。有关详细信息，请参阅 [http://go.microsoft.com/fwlink/?linkid=213819\&clcid=0x804](http://go.microsoft.com/fwlink/?linkid=213819%26clcid=0x804)。有关部署辅助 位置信息服务的详细信息，请参阅部署文档中的 [配置辅助位置信息服务](lync-server-2013-configure-a-secondary-location-information-service.md)。

有关填充位置数据库的详细信息，请参阅部署文档中的 [在 Lync Server 2013 中配置位置数据库](lync-server-2013-configure-the-location-database.md)。

## 维护位置数据库

填充位置数据库之后，需要制定更新数据库的策略，因为网络配置发生了改变。以下问题将帮助您确定如何维护位置数据库。

  - **如何更新位置数据库？**  
    有许多方案需要更新位置数据，包括添加无线接入点 (WAP)、重新布置办公室缆线（需要不同的交换机分配）和子网扩展。是直接更新每个位置，还是使用 CSV 文件执行所有位置的批量更新？

<!-- end list -->

  - **是否使用 SNMP 应用程序将 Lync 客户端 MAC 地址与端口和交换机标识符匹配？**  
    如果使用 SNMP 应用程序，需要设计用于保持 SNMP 应用程序和位置数据库之间的交换机机架和端口信息一致的手动过程。如果 SNMP 应用程序返回不包含在数据库中的机架 IP 地址或端口 ID，则 位置信息服务无法向客户端返回位置。

