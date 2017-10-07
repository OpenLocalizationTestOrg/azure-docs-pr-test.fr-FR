---
title: "les données de capteur aaaAnalyze à l’aide de la ruche et Hadoop - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment les données de capteur tooanalyze à l’aide de hello Console de requête Hive hdinsight (Hadoop), puis visualiser des données dans Microsoft Excel avec PowerView hello."
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
ms.openlocfilehash: 70e595705c33d9835dc9809161f79c3ac5ece870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-using-hello-hive-query-console-on-hadoop-in-hdinsight"></a><span data-ttu-id="0bb6d-103">Analyser les données de capteur à l’aide de hello Console de requête Hive sur Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="0bb6d-103">Analyze sensor data using hello Hive Query Console on Hadoop in HDInsight</span></span>

<span data-ttu-id="0bb6d-104">Découvrez comment les données de capteur tooanalyze à l’aide de hello Console de requête Hive hdinsight (Hadoop), puis visualiser les données de hello dans Microsoft Excel à l’aide de Power View.</span><span class="sxs-lookup"><span data-stu-id="0bb6d-104">Learn how tooanalyze sensor data by using hello Hive Query Console with HDInsight (Hadoop), then visualize hello data in Microsoft Excel by using Power View.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0bb6d-105">les étapes dans ce travail seul document avec des clusters HDInsight de basés sur Windows Hello.</span><span class="sxs-lookup"><span data-stu-id="0bb6d-105">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="0bb6d-106">HDInsight est uniquement disponible sur Windows pour les versions antérieures à HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="0bb6d-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="0bb6d-107">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="0bb6d-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0bb6d-108">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0bb6d-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


<span data-ttu-id="0bb6d-109">Dans cet exemple, les données d’historique tooprocess Hive et d’identifier des problèmes avec les systèmes de chauffage et la climatisation.</span><span class="sxs-lookup"><span data-stu-id="0bb6d-109">In this sample, you use Hive tooprocess historical data and identify problems with heating and air conditioning systems.</span></span> <span data-ttu-id="0bb6d-110">Plus précisément, vous identifiez les systèmes sont tooreliably n’a pas pu mettre à jour une jeu de température en effectuant hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="0bb6d-110">Specifically, you identify systems are not able tooreliably maintain a set temperature by performing hello following tasks:</span></span>

* <span data-ttu-id="0bb6d-111">Créer des tables de la ruche tooquery les données stockées dans les fichiers de valeurs séparées par des virgules (CSV).</span><span class="sxs-lookup"><span data-stu-id="0bb6d-111">Create HIVE tables tooquery data stored in comma-separated value (CSV) files.</span></span>
* <span data-ttu-id="0bb6d-112">Créer des requêtes HIVE tooanalyze les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="0bb6d-112">Create HIVE queries tooanalyze hello data.</span></span>
* <span data-ttu-id="0bb6d-113">les données analysée de hello tooretrieve, utilisez tooHDInsight tooconnect de Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="0bb6d-113">tooretrieve hello analyzed data, use Microsoft Excel tooconnect tooHDInsight.</span></span>
* <span data-ttu-id="0bb6d-114">les données de salutation toovisualize, utilisez Power View.</span><span class="sxs-lookup"><span data-stu-id="0bb6d-114">toovisualize hello data, use Power View.</span></span>

![Un diagramme d’architecture de solution hello](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a><span data-ttu-id="0bb6d-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0bb6d-116">Prerequisites</span></span>

* <span data-ttu-id="0bb6d-117">Un cluster HDInsight (Hadoop) : consultez la rubrique [Créer des clusters Hadoop dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md) pour des informations sur la création d’un cluster.</span><span class="sxs-lookup"><span data-stu-id="0bb6d-117">An HDInsight (Hadoop) cluster: See [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster.</span></span>
* <span data-ttu-id="0bb6d-118">Microsoft Excel 2013</span><span class="sxs-lookup"><span data-stu-id="0bb6d-118">Microsoft Excel 2013</span></span>

  > [!NOTE]
  > <span data-ttu-id="0bb6d-119">Microsoft Excel est utilisé pour la visualisation des données avec [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="0bb6d-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span></span>

* [<span data-ttu-id="0bb6d-120">Pilote ODBC Microsoft Hive</span><span class="sxs-lookup"><span data-stu-id="0bb6d-120">Microsoft Hive ODBC Driver</span></span>](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="toorun-hello-sample"></a><span data-ttu-id="0bb6d-121">hello, exemple toorun</span><span class="sxs-lookup"><span data-stu-id="0bb6d-121">toorun hello sample</span></span>

1. <span data-ttu-id="0bb6d-122">À partir de votre navigateur web, accédez à toohello suivant l’URL :</span><span class="sxs-lookup"><span data-stu-id="0bb6d-122">From your web browser, navigate toohello following URL:</span></span> 

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="0bb6d-123">Remplacez `<clustername>` par nom de hello de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0bb6d-123">Replace `<clustername>` with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="0bb6d-124">Lorsque vous y êtes invité, s’authentifier en utilisant le nom d’utilisateur administrateur hello et le mot de passe utilisé lors de la configuration de ce cluster.</span><span class="sxs-lookup"><span data-stu-id="0bb6d-124">When prompted, authenticate by using hello administrator user name and password you used when provisioning this cluster.</span></span>

2. <span data-ttu-id="0bb6d-125">Hello page web qui s’ouvre, cliquez sur hello **prise en main galerie** onglet, puis sous hello **Solutions avec des exemples de données** catégorie, cliquez sur hello **analyse des données de capteur** exemple.</span><span class="sxs-lookup"><span data-stu-id="0bb6d-125">From hello web page that opens, click hello **Getting Started Gallery** tab, and then under hello **Solutions with Sample Data** category, click hello **Sensor Data Analysis** sample.</span></span>

    ![Image Galerie de mise en route](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. <span data-ttu-id="0bb6d-127">Suivez les instructions hello de toofinish hello exemple hello page web.</span><span class="sxs-lookup"><span data-stu-id="0bb6d-127">Follow hello instructions provided on hello web page toofinish hello sample.</span></span>
