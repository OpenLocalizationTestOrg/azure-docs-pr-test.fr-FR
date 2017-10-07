---
title: "aaaUse Hive avec Hadoop pour l’analyse du journal du site Web - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toouse Hive avec un site Web de HDInsight tooanalyze se connecte. Vous allez utiliser un fichier journal en tant qu’entrée dans une table HDInsight et utilisent des données de HiveQL tooquery hello."
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
ms.openlocfilehash: 9cbce3cc8cf8bc3ad104dc4ca6a5628802c8fe89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-windows-based-hdinsight-tooanalyze-logs-from-websites"></a><span data-ttu-id="a8f6b-104">Utilisez la ruche avec des journaux de tooanalyze HDInsight de basé sur Windows à partir de sites Web</span><span class="sxs-lookup"><span data-stu-id="a8f6b-104">Use Hive with Windows-based HDInsight tooanalyze logs from websites</span></span>
<span data-ttu-id="a8f6b-105">Découvrez comment toouse HiveQL avec HDInsight tooanalyze se connecte à partir d’un site Web.</span><span class="sxs-lookup"><span data-stu-id="a8f6b-105">Learn how toouse HiveQL with HDInsight tooanalyze logs from a website.</span></span> <span data-ttu-id="a8f6b-106">L’analyse du journal du site Web peut être utilisé toosegment votre audience en fonction d’activités similaires, classer les visiteurs du site par les données démographiques et toofind contenus hello qu’ils affichent, ils proviennent des sites Web hello et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="a8f6b-106">Website log analysis can be used toosegment your audience based on similar activities, categorize site visitors by demographics, and toofind out hello content they view, hello websites they come from, and so on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8f6b-107">les étapes dans ce travail seul document avec des clusters HDInsight de basés sur Windows Hello.</span><span class="sxs-lookup"><span data-stu-id="a8f6b-107">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="a8f6b-108">HDInsight est uniquement disponible sur Windows pour les versions antérieures à HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="a8f6b-108">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="a8f6b-109">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="a8f6b-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a8f6b-110">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a8f6b-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="a8f6b-111">Dans cet exemple, vous allez utiliser une HDInsight cluster tooanalyze site Web du journal des fichiers tooget idée fréquence hello du site Web de toohello visites à partir des sites Web externes dans un jour.</span><span class="sxs-lookup"><span data-stu-id="a8f6b-111">In this sample, you will use an HDInsight cluster tooanalyze website log files tooget insight into hello frequency of visits toohello website from external websites in a day.</span></span> <span data-ttu-id="a8f6b-112">Vous allez également générer un résumé des erreurs de site Web que les utilisateurs de hello rencontrer.</span><span class="sxs-lookup"><span data-stu-id="a8f6b-112">You'll also generate a summary of website errors that hello users experience.</span></span> <span data-ttu-id="a8f6b-113">Vous apprendrez à :</span><span class="sxs-lookup"><span data-stu-id="a8f6b-113">You will learn how to:</span></span>

* <span data-ttu-id="a8f6b-114">Se connecter tooa stockage d’objets Blob Azure, qui contient les fichiers journaux du site Web.</span><span class="sxs-lookup"><span data-stu-id="a8f6b-114">Connect tooa Azure Blob storage, which contains website log files.</span></span>
* <span data-ttu-id="a8f6b-115">Créer des tables ruche tooquery ces journaux.</span><span class="sxs-lookup"><span data-stu-id="a8f6b-115">Create HIVE tables tooquery those logs.</span></span>
* <span data-ttu-id="a8f6b-116">Créer des requêtes HIVE tooanalyze les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="a8f6b-116">Create HIVE queries tooanalyze hello data.</span></span>
* <span data-ttu-id="a8f6b-117">Utiliser Microsoft Excel tooconnect tooHDInsight (à l’aide de la base de données ouverte (ODBC) tooretrieve hello analysé les données de connectivité.</span><span class="sxs-lookup"><span data-stu-id="a8f6b-117">Use Microsoft Excel tooconnect tooHDInsight (by using open database connectivity (ODBC) tooretrieve hello analyzed data.</span></span>

![HDI.Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a><span data-ttu-id="a8f6b-119">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a8f6b-119">Prerequisites</span></span>
* <span data-ttu-id="a8f6b-120">Vous devez avoir approvisionné un cluster Hadoop sur Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8f6b-120">You must have provisioned a Hadoop cluster on Azure HDInsight.</span></span> <span data-ttu-id="a8f6b-121">Pour plus d’informations, consultez la rubrique [Approvisionnement de clusters HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="a8f6b-121">For instructions, see [Provision HDInsight Clusters][hdinsight-provision].</span></span>
* <span data-ttu-id="a8f6b-122">Microsoft Excel 2013 ou Microsoft Excel 2010 doivent être installés.</span><span class="sxs-lookup"><span data-stu-id="a8f6b-122">You must have Microsoft Excel 2013 or Excel 2010 installed.</span></span>
* <span data-ttu-id="a8f6b-123">Vous devez avoir [Microsoft ODBC Driver de la ruche](http://www.microsoft.com/download/details.aspx?id=40886) tooimport des données à partir de la ruche dans Excel.</span><span class="sxs-lookup"><span data-stu-id="a8f6b-123">You must have [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) tooimport data from Hive into Excel.</span></span>

## <a name="toorun-hello-sample"></a><span data-ttu-id="a8f6b-124">hello, exemple toorun</span><span class="sxs-lookup"><span data-stu-id="a8f6b-124">toorun hello sample</span></span>
1. <span data-ttu-id="a8f6b-125">À partir de hello [Azure Portal](https://portal.azure.com/), à partir du tableau d’accueil (si vous avez épinglé cluster hello) de hello, cliquez sur la vignette de cluster hello sur lequel vous souhaitez toorun hello exemple.</span><span class="sxs-lookup"><span data-stu-id="a8f6b-125">From hello [Azure Portal](https://portal.azure.com/), from hello Startboard (if you pinned hello cluster there), click hello cluster tile on which you want toorun hello sample.</span></span>
2. <span data-ttu-id="a8f6b-126">À partir de hello cluster panneau, sous **liens rapides**, cliquez sur **tableau de bord de Cluster**, puis à partir de hello **tableau de bord de Cluster** panneau, cliquez sur **HDInsight Cluster Tableau de bord**.</span><span class="sxs-lookup"><span data-stu-id="a8f6b-126">From hello cluster blade, under **Quick Links**, click **Cluster Dashboard**, and then from hello **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="a8f6b-127">Ou bien, vous pouvez ouvrir directement du tableau de bord hello à l’aide de hello suivant l’URL :</span><span class="sxs-lookup"><span data-stu-id="a8f6b-127">Alternatively, you can directly open hello dashboard by using hello following URL:</span></span>

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="a8f6b-128">Lorsque vous y êtes invité, s’authentifier en utilisant le nom d’utilisateur administrateur hello et le mot de passe utilisé lors de la configuration de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="a8f6b-128">When prompted, authenticate by using hello administrator user name and password you used when provisioning hello cluster.</span></span>
3. <span data-ttu-id="a8f6b-129">À partir de la page web hello qui s’ouvre, cliquez sur hello **prise en main galerie** onglet, puis, sous hello **Solutions avec des exemples de données** catégorie, cliquez sur hello **l’analyse du journal du site Web** exemple.</span><span class="sxs-lookup"><span data-stu-id="a8f6b-129">From hello web page that opens, click hello **Getting Started Gallery** tab, and then under hello **Solutions with Sample Data** category, click hello **Website Log Analysis** sample.</span></span>
4. <span data-ttu-id="a8f6b-130">Suivez les instructions hello de toofinish hello exemple hello page web.</span><span class="sxs-lookup"><span data-stu-id="a8f6b-130">Follow hello instructions provided on hello web page toofinish hello sample.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8f6b-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a8f6b-131">Next steps</span></span>
<span data-ttu-id="a8f6b-132">Essayez de hello suivant l’exemple : [analyse des données de capteur à l’aide de la ruche hdinsight](hdinsight-hive-analyze-sensor-data.md).</span><span class="sxs-lookup"><span data-stu-id="a8f6b-132">Try hello following sample: [Analyzing sensor data using Hive with HDInsight](hdinsight-hive-analyze-sensor-data.md).</span></span>

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
