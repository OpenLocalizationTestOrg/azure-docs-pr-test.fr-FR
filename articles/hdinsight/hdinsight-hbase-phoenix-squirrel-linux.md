---
title: Utiliser Apache Phoenix et SQuirreL avec HBase - Azure HDInsight | Microsoft Docs
description: "Découvrez comment utiliser Apache Phoenix dans HDInsight et comment installer et configurer SQuirreL sur votre poste de travail pour vous connecter à un cluster HBase dans HDInsight."
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
ms.openlocfilehash: 13d17083bbe26fa9745ce4c5fef9f56859243c2e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="aa4cd-103">Utilisation d’Apache Phoenix avec les clusters HBase basés sur Linux dans HDinsight</span><span class="sxs-lookup"><span data-stu-id="aa4cd-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="aa4cd-104">Découvrez comment utiliser [Apache Phoenix](http://phoenix.apache.org/) dans HDInsight et comment utiliser SQLLine.</span><span class="sxs-lookup"><span data-stu-id="aa4cd-104">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how to use SQLLine.</span></span> <span data-ttu-id="aa4cd-105">Pour plus d'informations sur Phoenix, consultez [Phoenix en 15 minutes ou moins](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="aa4cd-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="aa4cd-106">Pour en savoir plus sur la grammaire Phoenix, consultez la page [Grammaire Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="aa4cd-106">For the Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="aa4cd-107">Pour plus d’informations sur la version de Phoenix dans HDInsight, consultez [Nouveautés des versions de cluster Hadoop fournies par HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="aa4cd-107">For the Phoenix version information in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="aa4cd-108">Utiliser SQLLine</span><span class="sxs-lookup"><span data-stu-id="aa4cd-108">Use SQLLine</span></span>
<span data-ttu-id="aa4cd-109">[SQLLine](http://sqlline.sourceforge.net/) est un utilitaire de ligne de commande pour exécuter SQL.</span><span class="sxs-lookup"><span data-stu-id="aa4cd-109">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility to execute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="aa4cd-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="aa4cd-110">Prerequisites</span></span>
<span data-ttu-id="aa4cd-111">Avant de pouvoir utiliser SQLLine, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="aa4cd-111">Before you can use SQLLine, you must have the following:</span></span>

* <span data-ttu-id="aa4cd-112">**Un cluster HBase dans HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="aa4cd-112">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="aa4cd-113">Pour plus d’informations sur l’approvisionnement d’un cluster HBase, consultez [Prise en main d’Apache HBase dans HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="aa4cd-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="aa4cd-114">**Une connexion au cluster HBase à l'aide du protocole RDP (Remote Desktop Protocol)**.</span><span class="sxs-lookup"><span data-stu-id="aa4cd-114">**Connect to the HBase cluster via the remote desktop protocol**.</span></span> <span data-ttu-id="aa4cd-115">Pour des instructions, voir [Gestion des clusters Hadoop dans HDInsight au moyen du portail Azure][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="aa4cd-115">For instructions, see [Manage Hadoop clusters in HDInsight by using the Azure portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="aa4cd-116">Quand vous vous connectez à un cluster HBase, vous devez vous connecter à l’un des serveurs Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="aa4cd-116">When you connect to an HBase cluster, you need to connect to one of the Zookeepers.</span></span> <span data-ttu-id="aa4cd-117">Chaque cluster HDInsight a trois serveurs Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="aa4cd-117">Each HDInsight cluster has three Zookeepers.</span></span>

<span data-ttu-id="aa4cd-118">**Pour connaître le nom d’hôte du Zookeeper**</span><span class="sxs-lookup"><span data-stu-id="aa4cd-118">**To find out the Zookeeper host name**</span></span>

1. <span data-ttu-id="aa4cd-119">Ouvrez Ambari en accédant à **https://<ClusterName>.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="aa4cd-119">Open Ambari by browsing to **https://<ClusterName>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="aa4cd-120">Entrez le nom d’utilisateur HTTP (cluster) et le mot de passe de connexion.</span><span class="sxs-lookup"><span data-stu-id="aa4cd-120">Enter the HTTP (cluster) username and password to login.</span></span>
3. <span data-ttu-id="aa4cd-121">Dans le menu de gauche, cliquez sur **ZooKeeper** .</span><span class="sxs-lookup"><span data-stu-id="aa4cd-121">Click **ZooKeeper** from the left menu.</span></span> <span data-ttu-id="aa4cd-122">Trois **serveurs Zookeeper** sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="aa4cd-122">You see three **ZooKeeper Server** listed.</span></span>
4. <span data-ttu-id="aa4cd-123">Cliquez sur l’un des **ZooKeeper Server** répertoriés.</span><span class="sxs-lookup"><span data-stu-id="aa4cd-123">Click one of the **ZooKeeper Server** listed.</span></span> <span data-ttu-id="aa4cd-124">Dans le volet Résumé, recherchez le **nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="aa4cd-124">On the Summary pane, find the **Hostname**.</span></span> <span data-ttu-id="aa4cd-125">Il ressemble à *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="aa4cd-125">It is similar to *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="aa4cd-126">**Pour utiliser SQLLine**</span><span class="sxs-lookup"><span data-stu-id="aa4cd-126">**To use SQLLine**</span></span>

1. <span data-ttu-id="aa4cd-127">Connectez-vous au cluster à l'aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="aa4cd-127">Connect to the cluster using SSH.</span></span> <span data-ttu-id="aa4cd-128">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="aa4cd-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="aa4cd-129">Depuis SSH, exécutez les commandes suivantes pour exécuter SQLLine :</span><span class="sxs-lookup"><span data-stu-id="aa4cd-129">From SSH, run the following commands to run SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. <span data-ttu-id="aa4cd-130">Exécutez les commandes suivantes pour créer une table HBase et insérer des données :</span><span class="sxs-lookup"><span data-stu-id="aa4cd-130">Run the following commands to create a HBase table, and insert some data:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="aa4cd-131">Pour plus d’informations, consultez le [manuel SQLLine](http://sqlline.sourceforge.net/#manual) et la [grammaire Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="aa4cd-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa4cd-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aa4cd-132">Next steps</span></span>
<span data-ttu-id="aa4cd-133">Dans cet article, vous avez appris comment utiliser Apache Phoenix dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aa4cd-133">In this article, you have learned how to use Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="aa4cd-134">Pour plus d'informations, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="aa4cd-134">To learn more, see:</span></span>

* <span data-ttu-id="aa4cd-135">[Vue d’ensemble de HDInsight HBase][hdinsight-hbase-overview] : HBase est une base de données NoSQL open source Apache basée sur Hadoop qui fournit un accès aléatoire et une forte cohérence pour de grandes quantités de données non structurées et semi-structurées.</span><span class="sxs-lookup"><span data-stu-id="aa4cd-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="aa4cd-136">[Approvisionnement de clusters HBase sur Azure Virtual Network][hdinsight-hbase-provision-vnet] : avec l’intégration du réseau virtuel, les clusters HBase peuvent être déployés sur le même réseau virtuel que vos applications pour permettre à celles-ci de communiquer directement avec HBase.</span><span class="sxs-lookup"><span data-stu-id="aa4cd-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="aa4cd-137">[Configurer la réplication HBase dans HDInsight](hdinsight-hbase-replication.md): découvrez comment configurer la réplication HBase entre deux centres de données Azure.</span><span class="sxs-lookup"><span data-stu-id="aa4cd-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how to configure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="aa4cd-138">[Analyse de sentiments Twitter avec HBase dans HDInsight][hbase-twitter-sentiment] : découvrez comment effectuer une [analyse de sentiments](http://en.wikipedia.org/wiki/Sentiment_analysis) en temps réel des données volumineuses à l’aide de HBase dans un cluster Hadoop sous HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aa4cd-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

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
