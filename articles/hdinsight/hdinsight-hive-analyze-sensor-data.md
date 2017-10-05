---
title: "Analyse des données de capteur au moyen de Hive et de Hadoop - HDInsight | Microsoft Docs"
description: "Découvrez comment analyser des données de capteur au moyen de la console de requête Hive avec HDInsight (Hadoop), puis visualiser les données dans Microsoft Excel avec Power View."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: a8ac160c-1cef-45d9-bf36-7beb5a439105
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 3abb71c12b4769bebd808276f8bdd832aad22d7a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-sensor-data-using-the-hive-query-console-on-hadoop-in-hdinsight"></a><span data-ttu-id="9313d-103">Analyse des données de capteur à l’aide de la console de requête Hive sur Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="9313d-103">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span></span>

<span data-ttu-id="9313d-104">Découvrez comment analyser des données de capteur au moyen de la console de requête Hive avec HDInsight (Hadoop), puis visualiser les données dans Microsoft Excel à l’aide de Power View.</span><span class="sxs-lookup"><span data-stu-id="9313d-104">Learn how to analyze sensor data by using the Hive Query Console with HDInsight (Hadoop), then visualize the data in Microsoft Excel by using Power View.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9313d-105">Les étapes décrites dans ce document fonctionnent uniquement avec les clusters HDInsight Windows.</span><span class="sxs-lookup"><span data-stu-id="9313d-105">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="9313d-106">HDInsight est uniquement disponible sur Windows pour les versions antérieures à HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="9313d-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="9313d-107">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="9313d-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9313d-108">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9313d-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


<span data-ttu-id="9313d-109">Dans cet exemple, vous utilisez Hive pour traiter les données historiques et identifier les problèmes relatifs aux systèmes de chauffage et de climatisation.</span><span class="sxs-lookup"><span data-stu-id="9313d-109">In this sample, you use Hive to process historical data and identify problems with heating and air conditioning systems.</span></span> <span data-ttu-id="9313d-110">Plus précisément, vous identifiez les systèmes qui ne sont pas en mesure de maintenir de façon fiable une température donnée en effectuant les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="9313d-110">Specifically, you identify systems are not able to reliably maintain a set temperature by performing the following tasks:</span></span>

* <span data-ttu-id="9313d-111">Créer des tables HIVE pour interroger des données stockées dans des fichiers au format CSV.</span><span class="sxs-lookup"><span data-stu-id="9313d-111">Create HIVE tables to query data stored in comma-separated value (CSV) files.</span></span>
* <span data-ttu-id="9313d-112">Créer des requêtes HIVE pour analyser les données.</span><span class="sxs-lookup"><span data-stu-id="9313d-112">Create HIVE queries to analyze the data.</span></span>
* <span data-ttu-id="9313d-113">Utiliser Microsoft Excel pour vous connecter à HDInsight et extraire les données analysées.</span><span class="sxs-lookup"><span data-stu-id="9313d-113">To retrieve the analyzed data, use Microsoft Excel to connect to HDInsight.</span></span>
* <span data-ttu-id="9313d-114">Utiliser Power View pour visualiser les données.</span><span class="sxs-lookup"><span data-stu-id="9313d-114">To visualize the data, use Power View.</span></span>

![A diagram of the solution architecture](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a><span data-ttu-id="9313d-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9313d-116">Prerequisites</span></span>

* <span data-ttu-id="9313d-117">Un cluster HDInsight (Hadoop) : consultez la rubrique [Créer des clusters Hadoop dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md) pour des informations sur la création d’un cluster.</span><span class="sxs-lookup"><span data-stu-id="9313d-117">An HDInsight (Hadoop) cluster: See [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster.</span></span>
* <span data-ttu-id="9313d-118">Microsoft Excel 2013</span><span class="sxs-lookup"><span data-stu-id="9313d-118">Microsoft Excel 2013</span></span>

  > [!NOTE]
  > <span data-ttu-id="9313d-119">Microsoft Excel est utilisé pour la visualisation des données avec [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="9313d-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span></span>

* [<span data-ttu-id="9313d-120">Pilote ODBC Microsoft Hive</span><span class="sxs-lookup"><span data-stu-id="9313d-120">Microsoft Hive ODBC Driver</span></span>](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="to-run-the-sample"></a><span data-ttu-id="9313d-121">Exécution de l'exemple</span><span class="sxs-lookup"><span data-stu-id="9313d-121">To run the sample</span></span>

1. <span data-ttu-id="9313d-122">À partir d’un navigateur web, accédez à l'URL suivante :</span><span class="sxs-lookup"><span data-stu-id="9313d-122">From your web browser, navigate to the following URL:</span></span> 

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="9313d-123">Remplacez `<clustername>` par le nom de votre cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="9313d-123">Replace `<clustername>` with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="9313d-124">À l’invite, authentifiez-vous au moyen du nom d’utilisateur et du mot de passe d’administrateur que vous avez utilisés lors de l’approvisionnement de ce cluster.</span><span class="sxs-lookup"><span data-stu-id="9313d-124">When prompted, authenticate by using the administrator user name and password you used when provisioning this cluster.</span></span>

2. <span data-ttu-id="9313d-125">Dans la page web qui s’ouvre, cliquez sur l’onglet **Galerie de mise en route**, puis sous la catégorie **Solutions avec des exemples de données**, cliquez sur l’exemple **Analyse des données de capteur**.</span><span class="sxs-lookup"><span data-stu-id="9313d-125">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Sensor Data Analysis** sample.</span></span>

    ![Image Galerie de mise en route](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. <span data-ttu-id="9313d-127">Suivez les instructions fournies dans la page web pour terminer l'exemple.</span><span class="sxs-lookup"><span data-stu-id="9313d-127">Follow the instructions provided on the web page to finish the sample.</span></span>
