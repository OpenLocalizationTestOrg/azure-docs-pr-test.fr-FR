---
title: aaaUse Apache Phoenix et non avec HBase - Azure HDInsight | Documents Microsoft
description: "Découvrez comment toouse Phoenix Apache dans HDInsight et comment tooinstall et configurer non sur votre cluster HBase de station de travail tooconnect tooan dans HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: cda0f33b-a2e8-494c-972f-ae0bb482b818
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/26/2017
ms.author: jgao
ms.openlocfilehash: a63e8c8212b7a992453ec94fa638ec3863a0ede3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a>Utilisation d’Apache Phoenix avec les clusters HBase basés sur Linux dans HDinsight
Découvrez comment toouse [Apache Phoenix](http://phoenix.apache.org/) dans HDInsight et comment toouse SQLUltraLite. Pour plus d'informations sur Phoenix, consultez [Phoenix en 15 minutes ou moins](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html). Pourquoi la grammaire de Phoenix, consultez [Phoenix grammaire](http://phoenix.apache.org/language/index.html).

> [!NOTE]
> Pourquoi les informations de version Phoenix dans HDInsight, consultez [quelles sont les nouveautés dans les versions de cluster Hadoop hello fournies par HDInsight ?](hdinsight-component-versioning.md).
>
>

## <a name="use-sqlline"></a>Utiliser SQLLine
[SQLUltraLite](http://sqlline.sourceforge.net/) est un tooexecute de l’utilitaire de ligne de commande SQL.

### <a name="prerequisites"></a>Composants requis
Avant de pouvoir utiliser SQLUltraLite, vous devez disposer de hello :

* **Un cluster HBase dans HDInsight**. Pour plus d’informations sur l’approvisionnement d’un cluster HBase, consultez [Prise en main d’Apache HBase dans HDInsight][hdinsight-hbase-get-started].
* **Connecter le cluster de HBase toohello via le protocole Bureau à distance de hello**. Pour obtenir des instructions, consultez [Hadoop de gérer les clusters dans HDInsight à l’aide de hello portail Azure][hdinsight-manage-portal].

Lorsque vous vous connectez tooan HBase cluster, vous devez tooone tooconnect Hello envieront. Chaque cluster HDInsight a trois serveurs Zookeeper.

**toofind nom d’hôte hello soigneur**

1. Ouvrez Ambari en parcourant trop**https://<ClusterName>. azurehdinsight.net**.
2. Entrez les toologin hello HTTP (cluster) nom d’utilisateur et mot de passe.
3. Cliquez sur **soigneur** à partir du menu de gauche hello. Trois **serveurs Zookeeper** sont répertoriés.
4. Cliquez sur un des hello **soigneur Server** répertoriés. Dans le volet Résumé hello recherche hello **nom d’hôte**. Il est similaire*zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.

**toouse SQLUltraLite**

1. Connectez le cluster toohello à l’aide de SSH. Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. À partir de SSH, exécutez hello suivant de commandes toorun SQLUltraLite :

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. Exécutez hello suivant de commandes toocreate une table HBase et insérez des données :

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

Pour plus d’informations, consultez le [manuel SQLLine](http://sqlline.sourceforge.net/#manual) et la [grammaire Phoenix](http://phoenix.apache.org/language/index.html).

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris comment toouse Phoenix Apache dans HDInsight.  toolearn, voir :

* [Vue d’ensemble de HDInsight HBase][hdinsight-hbase-overview] : HBase est une base de données NoSQL open source Apache basée sur Hadoop qui fournit un accès aléatoire et une forte cohérence pour de grandes quantités de données non structurées et semi-structurées.
* [Configurer des clusters HBase sur un réseau virtuel Azure][hdinsight-hbase-provision-vnet]: avec l’intégration de réseau virtuel, clusters HBase peuvent être déployé toohello même virtuel réseau en tant que vos applications, ainsi que les applications peuvent communiquer avec HBase directement.
* [Configurer la réplication de HBase de HDInsight](hdinsight-hbase-replication.md): Découvrez comment tooconfigure HBase la réplication entre deux centres de données Azure.
* [Analyse des sentiments Twitter avec HBase dans HDInsight][hbase-twitter-sentiment]: Découvrez comment toodo en temps réel [analyse des sentiments](http://en.wikipedia.org/wiki/Sentiment_analysis) de données à l’aide de HBase dans un cluster Hadoop dans HDInsight.

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
