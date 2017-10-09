---
title: aaaUse Hive Interactive dans HDInsight - Azure | Documents Microsoft
description: "Découvrez comment toouse Interactive Hive (Hive sur LLAP) dans HDInsight."
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
ms.openlocfilehash: 9e751a08091d18bc1b3d070468feef87f6828c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a><span data-ttu-id="68805-103">Utilisation de Hive interactif dans HDInsight (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="68805-103">Use Interactive Hive in HDInsight (Preview)</span></span>
<span data-ttu-id="68805-104">Hive interactif (également appelé</span><span class="sxs-lookup"><span data-stu-id="68805-104">Interactive Hive (A.K.A.</span></span> <span data-ttu-id="68805-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) est un nouveau [type de cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) HDInsight.</span><span class="sxs-lookup"><span data-stu-id="68805-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is a new HDInsight [cluster type](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>  <span data-ttu-id="68805-106">Hive interactif permet la mise en mémoire cache ce qui rend les requêtes Hive beaucoup plus interactives et rapides.</span><span class="sxs-lookup"><span data-stu-id="68805-106">Interactive Hive allows in memory caching that makes Hive queries much more interactive and faster.</span></span> <span data-ttu-id="68805-107">Cette nouvelle fonctionnalité rend les HDInsight d'entre hello la plupart des performantes, flexible et ouvert Big Data solutions monde de cloud de hello des caches en mémoire (à l’aide de la ruche et Spark) et la gestion avancée analytique via une profonde intégration avec R Services.</span><span class="sxs-lookup"><span data-stu-id="68805-107">This new feature makes HDInsight one of hello world’s most performant, flexible, and open Big Data solutions on hello cloud with in-memory caches (using Hive and Spark) and advanced analytics through deep integration with R Services.</span></span> 

<span data-ttu-id="68805-108">cluster de la ruche interactif Hello est différent de cluster Hadoop de hello.</span><span class="sxs-lookup"><span data-stu-id="68805-108">hello Interactive Hive cluster is different from hello Hadoop cluster.</span></span> <span data-ttu-id="68805-109">Il contient uniquement le service de ruche hello.</span><span class="sxs-lookup"><span data-stu-id="68805-109">It only contains hello Hive service.</span></span> 

> [!NOTE]
> <span data-ttu-id="68805-110">MapReduce, Pig, Sqoop, Oozie et d’autres services seront prochainement supprimés de ce type de cluster.</span><span class="sxs-lookup"><span data-stu-id="68805-110">MapReduce, Pig, Sqoop, Oozie, and other services will be removed from this cluster type soon.</span></span>
> <span data-ttu-id="68805-111">Hello service Hive dans le cluster de la ruche interactif hello est uniquement accessible via hello Ambari ruche vue, Beeline et la ruche ODBC.</span><span class="sxs-lookup"><span data-stu-id="68805-111">hello Hive service in hello Interactive Hive cluster is only accessible via hello Ambari Hive view, Beeline, and Hive ODBC.</span></span> <span data-ttu-id="68805-112">Il n’est pas accessible via la console Hive, Templeton, l’interface de ligne de commande Azure et Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68805-112">It can’t be accessed via Hive console, Templeton, Azure CLI, and Azure PowerShell.</span></span> 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a><span data-ttu-id="68805-113">Création d’un cluster Hive interactif</span><span class="sxs-lookup"><span data-stu-id="68805-113">Create an Interactive Hive cluster</span></span>
<span data-ttu-id="68805-114">Le cluster Hive interactif est uniquement pris en charge sur les clusters basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="68805-114">Interactive Hive cluster is only supported on Linux-based clusters.</span></span> <span data-ttu-id="68805-115">Pour des informations sur la création de clusters HDInsight, consultez [Création de clusters Hadoop basés sur Linux dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="68805-115">For information about creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="execute-hive-from-interactive-hive"></a><span data-ttu-id="68805-116">Exécution de Hive à partir de Hive interactif</span><span class="sxs-lookup"><span data-stu-id="68805-116">Execute Hive from Interactive Hive</span></span>
<span data-ttu-id="68805-117">Il existe différentes options vous permettant d’exécuter des requêtes Hive :</span><span class="sxs-lookup"><span data-stu-id="68805-117">There are different options how you can execute Hive queries:</span></span>

* <span data-ttu-id="68805-118">Exécutez Hive à l’aide de hello Ambari ruche vue</span><span class="sxs-lookup"><span data-stu-id="68805-118">Run Hive using hello Ambari Hive view</span></span>
  
    <span data-ttu-id="68805-119">Pour hello d’informations sur l’utilisation de hello Hive une vue, consultez [hello d’utiliser la ruche de vue avec Hadoop dans HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="68805-119">For hello information about using hello Hive View, see [Use hello Hive View with Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>
* <span data-ttu-id="68805-120">Exécution de Hive à l’aide de Beeline</span><span class="sxs-lookup"><span data-stu-id="68805-120">Run Hive using Beeline</span></span>
  
    <span data-ttu-id="68805-121">Pour plus d’informations hello sur l’utilisation de Beeline sur HDInsight, consultez [utilisez Hive avec Hadoop dans HDInsight avec Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="68805-121">For hello information on using Beeline on HDInsight, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
  
    <span data-ttu-id="68805-122">Vous utilisez Beeline à partir de nœud principal de hello ou un nœud vide.</span><span class="sxs-lookup"><span data-stu-id="68805-122">You use Beeline from either hello headnode or an empty edge node.</span></span>  <span data-ttu-id="68805-123">L’utilisation de Beeline à partir d’un nœud de périmètre vide est recommandée.</span><span class="sxs-lookup"><span data-stu-id="68805-123">Using Beeline from an empty edge node is recommended.</span></span>  <span data-ttu-id="68805-124">Pour des informations sur la création d’un cluster HDInsight avec un nœud de périmètre vide, consultez [Utiliser des nœuds de périmètre vides dans HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="68805-124">For information on creating an HDInsight cluster with an empty edgenode, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>
* <span data-ttu-id="68805-125">Exécution de Hive à l’aide d’ODBC Hive</span><span class="sxs-lookup"><span data-stu-id="68805-125">Run Hive using Hive ODBC</span></span>
  
    <span data-ttu-id="68805-126">Pour plus d’informations hello sur l’utilisation de la ruche de ODBC, consultez [tooHadoop Excel de se connecter avec le pilote Microsoft ODBC de la ruche de hello](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="68805-126">For hello information on using Hive ODBC, see [Connect Excel tooHadoop with hello Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>

<span data-ttu-id="68805-127">**hello toofind chaîne de connexion JDBC :**</span><span class="sxs-lookup"><span data-stu-id="68805-127">**toofind hello JDBC connection string:**</span></span>

1. <span data-ttu-id="68805-128">Ouverture de session tooAmbari à l’aide de hello suivant l’URL : https://<ClusterName>. AzureHDInsight.net.</span><span class="sxs-lookup"><span data-stu-id="68805-128">Sign on tooAmbari using hello following URL: https://<ClusterName>.AzureHDInsight.net.</span></span>
2. <span data-ttu-id="68805-129">Cliquez sur **la ruche** à partir du menu de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="68805-129">Click **Hive** from hello left menu.</span></span>
3. <span data-ttu-id="68805-130">Cliquez sur hello mis en surbrillance icône toocopy hello URL :</span><span class="sxs-lookup"><span data-stu-id="68805-130">Click hello highlighted icon toocopy hello URL:</span></span>
   
   ![HDInsight Hadoop Hive interactif LLAP JDBC](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a><span data-ttu-id="68805-132">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="68805-132">See also</span></span>
* <span data-ttu-id="68805-133">[Créer des clusters basés sur Linux de Hadoop dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Découvrez comment toocreate Hive interactif clusters dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="68805-133">[Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Learn how toocreate Interactive Hive clusters in HDInsight.</span></span>
* <span data-ttu-id="68805-134">[Utiliser la ruche avec Hadoop dans HDInsight avec Beeline](hdinsight-hadoop-use-hive-beeline.md): Découvrez comment requêtes Hive de toouse Beeline toosubmit.</span><span class="sxs-lookup"><span data-stu-id="68805-134">[Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md): Learn how toouse Beeline toosubmit Hive queries.</span></span>
* <span data-ttu-id="68805-135">[Rejoignez Excel tooHadoop hello Hive pilote ODBC de Microsoft](hdinsight-connect-excel-hive-odbc-driver.md): Découvrez comment tooconnect Excel tooHive.</span><span class="sxs-lookup"><span data-stu-id="68805-135">[Connect Excel tooHadoop with hello Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): learn how tooconnect Excel tooHive.</span></span>

