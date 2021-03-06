---
title: "如何将 Azure Redis 缓存与 Java 配合使用 | Microsoft Docs"
description: "开始将 Azure Redis 缓存与 Java 配合使用"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 29275a5e-2e39-4ef2-804f-7ecc5161eab9
ms.service: cache
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 08/31/2017
ms.author: sdanie
ms.openlocfilehash: b433eecb0424db85b616c40c5f0cdfc88692cef1
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/18/2017
---
# <a name="how-to-use-azure-redis-cache-with-java"></a>如何将 Azure Redis 缓存与 Java 配合使用
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Azure Redis 缓存用于访问 Microsoft 管理的专用 Redis 缓存。 可从 Microsoft Azure 内部的任何应用程序访问缓存。

本主题说明如何将Azure Redis 缓存与 Java 配合使用。

## <a name="prerequisites"></a>先决条件
[Jedis](https://github.com/xetorthio/jedis) - Redis 的 Java 客户端

本教程使用 Jedis，但可以使用 [http://redis.io/clients](http://redis.io/clients)中列出的任何 Java 客户端。

## <a name="create-a-redis-cache-on-azure"></a>在 Azure 上创建 Redis 缓存
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a>检索主机名和访问密钥
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-to-the-cache-securely-using-ssl"></a>使用 SSL 安全连接到缓存
最新版本的 [redis](https://github.com/xetorthio/jedis) 支持使用 SSL 连接到 Azure Redis 缓存。 下面的示例展示了如何使用 SSL 终结点 6380 连接到 Azure Redis 缓存。 将 `<name>` 替换为缓存名称，将 `<key>` 替换为主密钥或辅助密钥，如前面的[检索主机名和访问密钥](#retrieve-the-host-name-and-access-keys)部分中所述。

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> 已为新的 Azure Redis 缓存实例禁用了非 SSL 端口。 如果使用的是其他不支持 SSL 的客户端，请参阅[如何启用非 SSL 端口](cache-configure.md#access-ports)。
> 
> 

## <a name="add-something-to-the-cache-and-retrieve-it"></a>在缓存中添加一些内容并检索此内容
    package com.mycompany.app;
    import redis.clients.jedis.Jedis;
    import redis.clients.jedis.JedisShardInfo;

    public class App
    {
      public static void main( String[] args )
      {
        boolean useSsl = true;
        /* In this line, replace <name> with your cache name: */
        JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
        shardInfo.setPassword("<key>"); /* Use your access key. */
        Jedis jedis = new Jedis(shardInfo);
        jedis.set("foo", "bar");
        String value = jedis.get("foo");
      }
    }


## <a name="next-steps"></a>后续步骤
* [启用缓存诊断](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics)，以便可以[监视](https://msdn.microsoft.com/library/azure/dn763945.aspx)缓存的运行状况。
* 阅读官方 [Redis 文档](http://redis.io/documentation)。
* 了解[如何配置 Spring Initializr 应用，以使用 Redis 缓存](cache-java-spring-boot-initializer-with-redis-cache.md)。