---
title: "Apache Kafka on HDInsight 简介 - Azure | Microsoft Docs"
description: "了解 Apache Kafka on HDInsight：它的涵义和用途以及在何处可找到示例和入门信息。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: f284b6e3-5f3b-4a50-b455-917e77588069
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/07/2017
ms.author: larryfr
ms.openlocfilehash: 09a661b2a100245dd424e24d8a8ddef56c573b02
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="introducing-apache-kafka-on-hdinsight"></a>Apache Kafka on HDInsight 简介

[Apache Kafka](https://kafka.apache.org) 是一个分布式流式处理平台，以开源方式提供，可用于构建实时流式处理数据管道和应用程序。 Kafka 还提供了类似于消息队列的消息中转站，可在其中发布和订阅命名数据流。 Kafka on HDInsight 可在 Microsoft Azure 云中提供高度可扩展和高度可用的托管服务。

## <a name="why-use-kafka-on-hdinsight"></a>为何要使用 Kafka on HDInsight？

Kafka on HDInsight 提供以下功能：

* 服务级别协议 (SLA)：[HDInsight 的 SLA 信息](https://azure.microsoft.com/support/legal/sla/hdinsight/v1_0/)。

* 发布-订阅消息传送模式：Kafka 提供了一个 Producer API，用于将记录发布到 Kafka 主题。 订阅主题时，将使用 Consumer API。

* 流处理：Kafka 通常与 Apache Storm 或 Spark 配合使用，以实现实时流式处理。 Kafka 0.10.0.0（HDInsight 版本 3.5 和 3.6）引入了流式处理 API，可用于构建流式处理解决方案，而无需使用 Storm 或 Spark。

* 水平规模：Kafka 分区可对 HDInsight 群集中节点进行流式处理。 使用者进程可与单个分区关联，以便在使用记录时提供负载均衡。

* 按顺序传递：在每个分区中，记录按照被接收的顺序存储在流中。 通过为每个分区关联一个使用者进程，可保证按顺序处理记录。

* 容错：可在节点之间复制分区以提供容错。

* 与 Azure 托管磁盘集成：托管磁盘为 HDInsight 群集中虚拟机使用的磁盘提供更高的规模和吞吐量。

    默认情况下，已为 Kafka on HDInsight 启用托管磁盘。 可以在 HDInsight 创建过程中配置每个节点使用的磁盘数。 有关托管磁盘的详细信息，请参阅 [Azure 托管磁盘](../../virtual-machines/windows/managed-disks-overview.md)。

    有关为 Kafka on HDInsight 配置托管磁盘的信息，请参阅[提高 Kafka on HDInsight 的可伸缩性](apache-kafka-scalability.md)。

## <a name="use-cases"></a>用例

* **消息传送**：由于 Kafka 支持发布-订阅消息模式，因此它通常用作消息中转站。

* **活动跟踪**：由于 Kafka 提供按顺序进行日志记录的记录，因此它还可用于跟踪和重新创建活动。 例如，网站上或应用程序内的用户操作。

* **聚合**：使用流处理可从不同的流中聚合信息，将信息合并和集中到操作数据中。

* **转换**：使用流处理可将多个输入主题中的数据合并到一个或多个输出主题中，丰富其内容。

## <a name="architecture"></a>体系结构

![Kafka 群集配置](./media/apache-kafka-introduction/kafka-cluster.png)

下图显示了一个典型 Kafka 配置，该配置利用使用者组、分区和复制提供带容错功能的事件并行读取。 Apache ZooKeeper 专为并发、能恢复和低延迟的事务构建，因为它管理 Kafka 群集的状态。 Kafka 将记录存储在主题中。 记录由生成者生成，由使用者使用。 生成者从 Kafka 代理检索记录。 HDInsight 群集中的每个辅助角色节点都是 Kafka 代理。 将为每个使用者创建一个分区，从而允许对流数据进行并行处理。 利用复制功能将分区分布到各个节点上，以防止发生节点（中转站）服务中断。 用 *(L)* 表示的分区是给定分区的前导者。 生成方流量将根据由 ZooKeeper 管理的状态路由到每个节点的前导者。

每个 Kafka 中转站都使用 Azure 托管磁盘。 磁盘数是用户定义的，可以为每个中转站提供高达 16 TB 的存储。

> [!IMPORTANT]
> Kafka 无法识别 Azure 数据中心内的基础硬件（机架）。 若要确保基础硬件上的所有分区都正确地进行平衡，请参阅[配置数据的高可用性 (Kafka)](apache-kafka-high-availability.md)。

## <a name="next-steps"></a>后续步骤

使用以下链接了解如何使用 Apache Kafka on HDInsight：

* [Kafka on HDInsight 入门](apache-kafka-get-started.md)

* [使用 MirrorMaker 创建 Kafka on HDInsight 的副本](apache-kafka-mirroring.md)

* [将 Apache Storm 与 Kafka on HDInsight 结合使用](../hdinsight-apache-storm-with-kafka.md)

* [将 Apache Spark 与 Kafka on HDInsight 结合使用](../hdinsight-apache-spark-with-kafka.md)

* [通过 Azure 虚拟网络连接到 Kafka](apache-kafka-connect-vpn-gateway.md)