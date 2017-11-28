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
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="eb18e-103">Utilisation d’Apache Phoenix avec les clusters HBase basés sur Linux dans HDinsight</span><span class="sxs-lookup"><span data-stu-id="eb18e-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="eb18e-104">Découvrez comment toouse [Apache Phoenix](http://phoenix.apache.org/) dans HDInsight et comment toouse SQLUltraLite.</span><span class="sxs-lookup"><span data-stu-id="eb18e-104">Learn how toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how toouse SQLLine.</span></span> <span data-ttu-id="eb18e-105">Pour plus d'informations sur Phoenix, consultez [Phoenix en 15 minutes ou moins](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="eb18e-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="eb18e-106">Pourquoi la grammaire de Phoenix, consultez [Phoenix grammaire](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="eb18e-106">For hello Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="eb18e-107">Pourquoi les informations de version Phoenix dans HDInsight, consultez [quelles sont les nouveautés dans les versions de cluster Hadoop hello fournies par HDInsight ?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="eb18e-107">For hello Phoenix version information in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="eb18e-108">Utiliser SQLLine</span><span class="sxs-lookup"><span data-stu-id="eb18e-108">Use SQLLine</span></span>
<span data-ttu-id="eb18e-109">[SQLUltraLite](http://sqlline.sourceforge.net/) est un tooexecute de l’utilitaire de ligne de commande SQL.</span><span class="sxs-lookup"><span data-stu-id="eb18e-109">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility tooexecute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="eb18e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="eb18e-110">Prerequisites</span></span>
<span data-ttu-id="eb18e-111">Avant de pouvoir utiliser SQLUltraLite, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="eb18e-111">Before you can use SQLLine, you must have hello following:</span></span>

* <span data-ttu-id="eb18e-112">**Un cluster HBase dans HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="eb18e-112">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="eb18e-113">Pour plus d’informations sur l’approvisionnement d’un cluster HBase, consultez [Prise en main d’Apache HBase dans HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="eb18e-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="eb18e-114">**Connecter le cluster de HBase toohello via le protocole Bureau à distance de hello**.</span><span class="sxs-lookup"><span data-stu-id="eb18e-114">**Connect toohello HBase cluster via hello remote desktop protocol**.</span></span> <span data-ttu-id="eb18e-115">Pour obtenir des instructions, consultez [Hadoop de gérer les clusters dans HDInsight à l’aide de hello portail Azure][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="eb18e-115">For instructions, see [Manage Hadoop clusters in HDInsight by using hello Azure portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="eb18e-116">Lorsque vous vous connectez tooan HBase cluster, vous devez tooone tooconnect Hello envieront.</span><span class="sxs-lookup"><span data-stu-id="eb18e-116">When you connect tooan HBase cluster, you need tooconnect tooone of hello Zookeepers.</span></span> <span data-ttu-id="eb18e-117">Chaque cluster HDInsight a trois serveurs Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="eb18e-117">Each HDInsight cluster has three Zookeepers.</span></span>

<span data-ttu-id="eb18e-118">**toofind nom d’hôte hello soigneur**</span><span class="sxs-lookup"><span data-stu-id="eb18e-118">**toofind out hello Zookeeper host name**</span></span>

1. <span data-ttu-id="eb18e-119">Ouvrez Ambari en parcourant trop**https://<ClusterName>. azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="eb18e-119">Open Ambari by browsing too**https://<ClusterName>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="eb18e-120">Entrez les toologin hello HTTP (cluster) nom d’utilisateur et mot de passe.</span><span class="sxs-lookup"><span data-stu-id="eb18e-120">Enter hello HTTP (cluster) username and password toologin.</span></span>
3. <span data-ttu-id="eb18e-121">Cliquez sur **soigneur** à partir du menu de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="eb18e-121">Click **ZooKeeper** from hello left menu.</span></span> <span data-ttu-id="eb18e-122">Trois **serveurs Zookeeper** sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="eb18e-122">You see three **ZooKeeper Server** listed.</span></span>
4. <span data-ttu-id="eb18e-123">Cliquez sur un des hello **soigneur Server** répertoriés.</span><span class="sxs-lookup"><span data-stu-id="eb18e-123">Click one of hello **ZooKeeper Server** listed.</span></span> <span data-ttu-id="eb18e-124">Dans le volet Résumé hello recherche hello **nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="eb18e-124">On hello Summary pane, find hello **Hostname**.</span></span> <span data-ttu-id="eb18e-125">Il est similaire*zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="eb18e-125">It is similar too*zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="eb18e-126">**toouse SQLUltraLite**</span><span class="sxs-lookup"><span data-stu-id="eb18e-126">**toouse SQLLine**</span></span>

1. <span data-ttu-id="eb18e-127">Connectez le cluster toohello à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="eb18e-127">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="eb18e-128">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="eb18e-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="eb18e-129">À partir de SSH, exécutez hello suivant de commandes toorun SQLUltraLite :</span><span class="sxs-lookup"><span data-stu-id="eb18e-129">From SSH, run hello following commands toorun SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. <span data-ttu-id="eb18e-130">Exécutez hello suivant de commandes toocreate une table HBase et insérez des données :</span><span class="sxs-lookup"><span data-stu-id="eb18e-130">Run hello following commands toocreate a HBase table, and insert some data:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="eb18e-131">Pour plus d’informations, consultez le [manuel SQLLine](http://sqlline.sourceforge.net/#manual) et la [grammaire Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="eb18e-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb18e-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eb18e-132">Next steps</span></span>
<span data-ttu-id="eb18e-133">Dans cet article, vous avez appris comment toouse Phoenix Apache dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eb18e-133">In this article, you have learned how toouse Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="eb18e-134">toolearn, voir :</span><span class="sxs-lookup"><span data-stu-id="eb18e-134">toolearn more, see:</span></span>

* <span data-ttu-id="eb18e-135">[Vue d’ensemble de HDInsight HBase][hdinsight-hbase-overview] : HBase est une base de données NoSQL open source Apache basée sur Hadoop qui fournit un accès aléatoire et une forte cohérence pour de grandes quantités de données non structurées et semi-structurées.</span><span class="sxs-lookup"><span data-stu-id="eb18e-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="eb18e-136">[Configurer des clusters HBase sur un réseau virtuel Azure][hdinsight-hbase-provision-vnet]: avec l’intégration de réseau virtuel, clusters HBase peuvent être déployé toohello même virtuel réseau en tant que vos applications, ainsi que les applications peuvent communiquer avec HBase directement.</span><span class="sxs-lookup"><span data-stu-id="eb18e-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="eb18e-137">[Configurer la réplication de HBase de HDInsight](hdinsight-hbase-replication.md): Découvrez comment tooconfigure HBase la réplication entre deux centres de données Azure.</span><span class="sxs-lookup"><span data-stu-id="eb18e-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how tooconfigure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="eb18e-138">[Analyse des sentiments Twitter avec HBase dans HDInsight][hbase-twitter-sentiment]: Découvrez comment toodo en temps réel [analyse des sentiments](http://en.wikipedia.org/wiki/Sentiment_analysis) de données à l’aide de HBase dans un cluster Hadoop dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eb18e-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how toodo real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

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
