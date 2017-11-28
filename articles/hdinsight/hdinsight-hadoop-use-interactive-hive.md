---
title: "Utiliser Hive interactif dans HDInsight - Azure | Microsoft Docs"
description: "Découvrez comment utiliser Hive interactif (Hive sur LLAP) dans HDInsight."
keywords: 
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0957643c-4936-48a3-84a3-5dc83db4ab1a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: e7874b55fc72f14d8e2c801872359e823cb2ba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a><span data-ttu-id="a0059-103">Utilisation de Hive interactif dans HDInsight (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="a0059-103">Use Interactive Hive in HDInsight (Preview)</span></span>
<span data-ttu-id="a0059-104">Hive interactif (également appelé</span><span class="sxs-lookup"><span data-stu-id="a0059-104">Interactive Hive (A.K.A.</span></span> <span data-ttu-id="a0059-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) est un nouveau [type de cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a0059-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is a new HDInsight [cluster type](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>  <span data-ttu-id="a0059-106">Hive interactif permet la mise en mémoire cache ce qui rend les requêtes Hive beaucoup plus interactives et rapides.</span><span class="sxs-lookup"><span data-stu-id="a0059-106">Interactive Hive allows in memory caching that makes Hive queries much more interactive and faster.</span></span> <span data-ttu-id="a0059-107">Cette nouvelle fonctionnalité fait de HDInsight l’une des solutions de Big Data dans le cloud les plus performantes, flexibles et ouvertes, avec des caches in-memory (utilisant Hive et Spark), ainsi que des services d’analyse avancée grâce à une intégration étroite avec R Services.</span><span class="sxs-lookup"><span data-stu-id="a0059-107">This new feature makes HDInsight one of the world’s most performant, flexible, and open Big Data solutions on the cloud with in-memory caches (using Hive and Spark) and advanced analytics through deep integration with R Services.</span></span> 

<span data-ttu-id="a0059-108">Le cluster Hive interactif est différent du cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a0059-108">The Interactive Hive cluster is different from the Hadoop cluster.</span></span> <span data-ttu-id="a0059-109">Il contient uniquement le service Hive.</span><span class="sxs-lookup"><span data-stu-id="a0059-109">It only contains the Hive service.</span></span> 

> [!NOTE]
> <span data-ttu-id="a0059-110">MapReduce, Pig, Sqoop, Oozie et d’autres services seront prochainement supprimés de ce type de cluster.</span><span class="sxs-lookup"><span data-stu-id="a0059-110">MapReduce, Pig, Sqoop, Oozie, and other services will be removed from this cluster type soon.</span></span>
> <span data-ttu-id="a0059-111">Le service Hive du cluster Hive interactif est uniquement accessible via la vue Ambari Hive, Beeline et ODBC Hive.</span><span class="sxs-lookup"><span data-stu-id="a0059-111">The Hive service in the Interactive Hive cluster is only accessible via the Ambari Hive view, Beeline, and Hive ODBC.</span></span> <span data-ttu-id="a0059-112">Il n’est pas accessible via la console Hive, Templeton, l’interface de ligne de commande Azure et Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0059-112">It can’t be accessed via Hive console, Templeton, Azure CLI, and Azure PowerShell.</span></span> 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a><span data-ttu-id="a0059-113">Création d’un cluster Hive interactif</span><span class="sxs-lookup"><span data-stu-id="a0059-113">Create an Interactive Hive cluster</span></span>
<span data-ttu-id="a0059-114">Le cluster Hive interactif est uniquement pris en charge sur les clusters basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="a0059-114">Interactive Hive cluster is only supported on Linux-based clusters.</span></span> <span data-ttu-id="a0059-115">Pour des informations sur la création de clusters HDInsight, consultez [Création de clusters Hadoop basés sur Linux dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="a0059-115">For information about creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="execute-hive-from-interactive-hive"></a><span data-ttu-id="a0059-116">Exécution de Hive à partir de Hive interactif</span><span class="sxs-lookup"><span data-stu-id="a0059-116">Execute Hive from Interactive Hive</span></span>
<span data-ttu-id="a0059-117">Il existe différentes options vous permettant d’exécuter des requêtes Hive :</span><span class="sxs-lookup"><span data-stu-id="a0059-117">There are different options how you can execute Hive queries:</span></span>

* <span data-ttu-id="a0059-118">Exécution de Hive à l’aide de la vue Ambari Hive</span><span class="sxs-lookup"><span data-stu-id="a0059-118">Run Hive using the Ambari Hive view</span></span>
  
    <span data-ttu-id="a0059-119">Pour des informations sur l’utilisation de la vue Hive, consultez [Utiliser la vue Hive avec Hadoop dans HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="a0059-119">For the information about using the Hive View, see [Use the Hive View with Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>
* <span data-ttu-id="a0059-120">Exécution de Hive à l’aide de Beeline</span><span class="sxs-lookup"><span data-stu-id="a0059-120">Run Hive using Beeline</span></span>
  
    <span data-ttu-id="a0059-121">Pour des informations sur l’utilisation de Beeline sur HDInsight, consultez [Utiliser Hive avec Hadoop dans HDInsight avec Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="a0059-121">For the information on using Beeline on HDInsight, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
  
    <span data-ttu-id="a0059-122">Vous utilisez Beeline à partir du nœud principal ou d’un nœud de périmètre vide.</span><span class="sxs-lookup"><span data-stu-id="a0059-122">You use Beeline from either the headnode or an empty edge node.</span></span>  <span data-ttu-id="a0059-123">L’utilisation de Beeline à partir d’un nœud de périmètre vide est recommandée.</span><span class="sxs-lookup"><span data-stu-id="a0059-123">Using Beeline from an empty edge node is recommended.</span></span>  <span data-ttu-id="a0059-124">Pour des informations sur la création d’un cluster HDInsight avec un nœud de périmètre vide, consultez [Utiliser des nœuds de périmètre vides dans HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="a0059-124">For information on creating an HDInsight cluster with an empty edgenode, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>
* <span data-ttu-id="a0059-125">Exécution de Hive à l’aide d’ODBC Hive</span><span class="sxs-lookup"><span data-stu-id="a0059-125">Run Hive using Hive ODBC</span></span>
  
    <span data-ttu-id="a0059-126">Pour des informations sur l’utilisation de Hive ODBC, consultez la page [Connexion d’Excel à Hadoop avec le pilote ODBC Hive de Microsoft](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="a0059-126">For the information on using Hive ODBC, see [Connect Excel to Hadoop with the Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>

<span data-ttu-id="a0059-127">**Pour rechercher la chaîne de connexion JDBC :**</span><span class="sxs-lookup"><span data-stu-id="a0059-127">**To find the JDBC connection string:**</span></span>

1. <span data-ttu-id="a0059-128">Connectez-vous à Ambari à l’aide de l’URL suivante : https://<ClusterName>.AzureHDInsight.net.</span><span class="sxs-lookup"><span data-stu-id="a0059-128">Sign on to Ambari using the following URL: https://<ClusterName>.AzureHDInsight.net.</span></span>
2. <span data-ttu-id="a0059-129">Cliquez sur **Hive** dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="a0059-129">Click **Hive** from the left menu.</span></span>
3. <span data-ttu-id="a0059-130">Cliquez sur l’icône en surbrillance pour copier l’URL :</span><span class="sxs-lookup"><span data-stu-id="a0059-130">Click the highlighted icon to copy the URL:</span></span>
   
   ![HDInsight Hadoop Hive interactif LLAP JDBC](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a><span data-ttu-id="a0059-132">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a0059-132">See also</span></span>
* <span data-ttu-id="a0059-133">[Créer des clusters Hadoop dans HDInsight basés sur Linux](hdinsight-hadoop-provision-linux-clusters.md) : apprenez à créer des clusters Hive interactif dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a0059-133">[Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Learn how to create Interactive Hive clusters in HDInsight.</span></span>
* <span data-ttu-id="a0059-134">[Utilisation de Hive avec Hadoop dans HDInsight avec Beeline](hdinsight-hadoop-use-hive-beeline.md) : apprenez à utiliser Beeline pour envoyer des requêtes Hive.</span><span class="sxs-lookup"><span data-stu-id="a0059-134">[Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md): Learn how to use Beeline to submit Hive queries.</span></span>
* <span data-ttu-id="a0059-135">[Connexion d’Excel à Hadoop avec le pilote ODBC Microsoft Hive](hdinsight-connect-excel-hive-odbc-driver.md) : apprenez à connecter Excel à Hive.</span><span class="sxs-lookup"><span data-stu-id="a0059-135">[Connect Excel to Hadoop with the Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): learn how to connect Excel to Hive.</span></span>

