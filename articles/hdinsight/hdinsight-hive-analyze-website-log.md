---
title: "Utilisation de Hive avec Hadoop pour l’analyse des journaux de site web - Azure HDInsight | Microsoft Docs"
description: "Découvrez comment utiliser Hive avec HDInsight pour analyser les journaux de site web. Vous allez utiliser un fichier journal en tant qu'entrée dans une table HDInsight, puis faire appel à HiveQL pour interroger les données."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6fb7b5c2-8df4-40b1-a9e2-6815080004f9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: e1cdb786bb6049980aafc0213abf53013e342618
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-hive-with-windows-based-hdinsight-to-analyze-logs-from-websites"></a><span data-ttu-id="209dd-104">Utiliser Hive avec HDInsight Windows pour analyser les journaux de site web</span><span class="sxs-lookup"><span data-stu-id="209dd-104">Use Hive with Windows-based HDInsight to analyze logs from websites</span></span>
<span data-ttu-id="209dd-105">Découvrez comment utiliser HiveQL avec HDInsight pour analyser les journaux d'un site web.</span><span class="sxs-lookup"><span data-stu-id="209dd-105">Learn how to use HiveQL with HDInsight to analyze logs from a website.</span></span> <span data-ttu-id="209dd-106">L’analyse des journaux de site web permet de segmenter votre public en fonction d’activités similaires, de classer les visiteurs d’un site sur la base de données démographiques, d’identifier le contenu qu’ils affichent, les sites web qu’ils ont visités avant, etc.</span><span class="sxs-lookup"><span data-stu-id="209dd-106">Website log analysis can be used to segment your audience based on similar activities, categorize site visitors by demographics, and to find out the content they view, the websites they come from, and so on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="209dd-107">Les étapes décrites dans ce document fonctionnent uniquement avec les clusters HDInsight Windows.</span><span class="sxs-lookup"><span data-stu-id="209dd-107">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="209dd-108">HDInsight est uniquement disponible sur Windows pour les versions antérieures à HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="209dd-108">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="209dd-109">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="209dd-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="209dd-110">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="209dd-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="209dd-111">Dans cet exemple, vous allez utiliser un cluster HDInsight pour analyser des fichiers journaux de site web afin d’obtenir des informations sur la fréquence des accès au site web en une journée à partir de sites web externes.</span><span class="sxs-lookup"><span data-stu-id="209dd-111">In this sample, you will use an HDInsight cluster to analyze website log files to get insight into the frequency of visits to the website from external websites in a day.</span></span> <span data-ttu-id="209dd-112">Vous allez également générer un résumé des erreurs de site Web rencontrées par les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="209dd-112">You'll also generate a summary of website errors that the users experience.</span></span> <span data-ttu-id="209dd-113">Vous apprendrez à :</span><span class="sxs-lookup"><span data-stu-id="209dd-113">You will learn how to:</span></span>

* <span data-ttu-id="209dd-114">Vous connecter à un stockage d’objets blob Azure contenant des fichiers journaux de site Web.</span><span class="sxs-lookup"><span data-stu-id="209dd-114">Connect to a Azure Blob storage, which contains website log files.</span></span>
* <span data-ttu-id="209dd-115">Créer des tables HIVE pour interroger ces journaux.</span><span class="sxs-lookup"><span data-stu-id="209dd-115">Create HIVE tables to query those logs.</span></span>
* <span data-ttu-id="209dd-116">Créer des requêtes HIVE pour analyser les données.</span><span class="sxs-lookup"><span data-stu-id="209dd-116">Create HIVE queries to analyze the data.</span></span>
* <span data-ttu-id="209dd-117">Utiliser Microsoft Excel pour vous connecter à HDInsight (au moyen d’une connexion ODBC) pour extraire les données analysées.</span><span class="sxs-lookup"><span data-stu-id="209dd-117">Use Microsoft Excel to connect to HDInsight (by using open database connectivity (ODBC) to retrieve the analyzed data.</span></span>

![HDI.Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a><span data-ttu-id="209dd-119">Composants requis</span><span class="sxs-lookup"><span data-stu-id="209dd-119">Prerequisites</span></span>
* <span data-ttu-id="209dd-120">Vous devez avoir approvisionné un cluster Hadoop sur Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="209dd-120">You must have provisioned a Hadoop cluster on Azure HDInsight.</span></span> <span data-ttu-id="209dd-121">Pour plus d’informations, consultez la rubrique [Approvisionnement de clusters HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="209dd-121">For instructions, see [Provision HDInsight Clusters][hdinsight-provision].</span></span>
* <span data-ttu-id="209dd-122">Microsoft Excel 2013 ou Microsoft Excel 2010 doivent être installés.</span><span class="sxs-lookup"><span data-stu-id="209dd-122">You must have Microsoft Excel 2013 or Excel 2010 installed.</span></span>
* <span data-ttu-id="209dd-123">Vous devez disposer d'un [pilote ODBC Microsoft Hive](http://www.microsoft.com/download/details.aspx?id=40886) pour importer des données à partir de Hive dans Excel.</span><span class="sxs-lookup"><span data-stu-id="209dd-123">You must have [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) to import data from Hive into Excel.</span></span>

## <a name="to-run-the-sample"></a><span data-ttu-id="209dd-124">Exécution de l'exemple</span><span class="sxs-lookup"><span data-stu-id="209dd-124">To run the sample</span></span>
1. <span data-ttu-id="209dd-125">Dans le [portail Azure](https://portal.azure.com/), depuis le tableau d’accueil (si vous y avez épinglé le cluster), cliquez sur la mosaïque du cluster sur lequel vous souhaitez exécuter l’exemple.</span><span class="sxs-lookup"><span data-stu-id="209dd-125">From the [Azure Portal](https://portal.azure.com/), from the Startboard (if you pinned the cluster there), click the cluster tile on which you want to run the sample.</span></span>
2. <span data-ttu-id="209dd-126">Dans le panneau du cluster, sous **Liens rapides**, cliquez sur **Tableau de bord du cluster**, puis dans le panneau **Tableau de bord du cluster**, cliquez sur **Tableau de bord de cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="209dd-126">From the cluster blade, under **Quick Links**, click **Cluster Dashboard**, and then from the **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="209dd-127">Vous pouvez également ouvrir directement le tableau de bord en utilisant l'URL suivante :</span><span class="sxs-lookup"><span data-stu-id="209dd-127">Alternatively, you can directly open the dashboard by using the following URL:</span></span>

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="209dd-128">À l’invite, authentifiez-vous au moyen du nom d’utilisateur et du mot de passe d’administrateur que vous avez utilisés lors de l’approvisionnement du cluster.</span><span class="sxs-lookup"><span data-stu-id="209dd-128">When prompted, authenticate by using the administrator user name and password you used when provisioning the cluster.</span></span>
3. <span data-ttu-id="209dd-129">Dans la page web qui s’ouvre, cliquez sur l’onglet **Galerie de mise en route**, puis sous la catégorie **Solutions avec des exemples de données**, cliquez sur l’exemple **Analyse du journal du site web**.</span><span class="sxs-lookup"><span data-stu-id="209dd-129">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Website Log Analysis** sample.</span></span>
4. <span data-ttu-id="209dd-130">Suivez les instructions fournies dans la page web pour terminer l'exemple.</span><span class="sxs-lookup"><span data-stu-id="209dd-130">Follow the instructions provided on the web page to finish the sample.</span></span>

## <a name="next-steps"></a><span data-ttu-id="209dd-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="209dd-131">Next steps</span></span>
<span data-ttu-id="209dd-132">Essayez l’exemple suivant : [Analyse des données de capteur au moyen de Hive avec HDInsight](hdinsight-hive-analyze-sensor-data.md).</span><span class="sxs-lookup"><span data-stu-id="209dd-132">Try the following sample: [Analyzing sensor data using Hive with HDInsight](hdinsight-hive-analyze-sensor-data.md).</span></span>

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
