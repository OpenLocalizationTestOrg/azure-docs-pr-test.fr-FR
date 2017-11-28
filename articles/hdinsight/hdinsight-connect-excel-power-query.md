---
title: "tooHadoop d’Excel aaaConnect avec Power Query - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment parti tootake de composants de business intelligence et utilisez Power Query pour les données Excel tooaccess stockées dans Hadoop dans HDInsight."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 01ad2f90-7520-44d9-8c16-4d936faaff9b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jgao
ms.openlocfilehash: 1213849f1bc04e0ed206750b80766ff2268664b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-by-using-power-query"></a><span data-ttu-id="e8ecd-103">Se connecter tooHadoop d’Excel à l’aide de Power Query</span><span class="sxs-lookup"><span data-stu-id="e8ecd-103">Connect Excel tooHadoop by using Power Query</span></span>
<span data-ttu-id="e8ecd-104">Une fonction clé de la solution de données volumineuses Microsoft hello est l’intégration de composants de Microsoft business intelligence (BI) avec des clusters Hadoop dans HDInsight de Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-104">One key feature of hello Microsoft big-data solution is hello integration of Microsoft business intelligence (BI) components with Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="e8ecd-105">Un exemple principal est hello capacité tooconnect Excel toohello compte de stockage Azure qui contient les données hello associées à votre cluster Hadoop à l’aide de hello Microsoft Power Query pour Excel.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-105">A primary example is hello ability tooconnect Excel toohello Azure Storage account that contains hello data associated with your Hadoop cluster by using hello Microsoft Power Query for Excel add-in.</span></span> <span data-ttu-id="e8ecd-106">Cet article vous guide tout au long de comment tooset des et utiliser les données de tooquery Power Query associées à un cluster Hadoop gérés avec HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-106">This article walks you through how tooset up and use Power Query tooquery data associated with a Hadoop cluster managed with HDInsight.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e8ecd-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e8ecd-107">Prerequisites</span></span>
<span data-ttu-id="e8ecd-108">Avant de commencer cet article, vous devez disposer de hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e8ecd-108">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="e8ecd-109">**Un cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-109">**An HDInsight cluster**.</span></span> <span data-ttu-id="e8ecd-110">tooconfigure, consultez [prise en main Azure HDInsight][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="e8ecd-110">tooconfigure one, see [Get started with Azure HDInsight][hdinsight-get-started].</span></span>
* <span data-ttu-id="e8ecd-111">**Une station de travail** fonctionnant sous Windows 7, Windows Server 2008 R2 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-111">**A workstation** that is running Windows 7, Windows Server 2008 R2, or a later operating system.</span></span>
* <span data-ttu-id="e8ecd-112">**Office 2016, Office 2013 Professionnel Plus, Office 365 ProPlus, Excel 2013 autonome ou Office 2010 Professionnel Plus**.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-112">**Office 2016, Office 2013 Professional Plus, Office 365 ProPlus, Excel 2013 Standalone, or Office 2010 Professional Plus**.</span></span>

## <a name="install-power-query"></a><span data-ttu-id="e8ecd-113">Installation de Power Query</span><span class="sxs-lookup"><span data-stu-id="e8ecd-113">Install Power Query</span></span>
<span data-ttu-id="e8ecd-114">Power Query permet d'importer des données produites ou générées par un travail Hadoop s'exécutant sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-114">Power Query can import data that has been output or that has been generated by a Hadoop job running on an HDInsight cluster.</span></span>

<span data-ttu-id="e8ecd-115">Dans Excel 2016, Power Query a été intégré dans le ruban de données hello hello Get & Transform section.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-115">In Excel 2016, Power Query has been integrated into hello Data ribbon under hello Get & Transform section.</span></span> <span data-ttu-id="e8ecd-116">Pour les versions antérieures de Excel, téléchargez Microsoft Power Query pour Excel à partir de hello [Microsoft Download Center] [ powerquery-download] et l’installer.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-116">For older Excel versions, download Microsoft Power Query for Excel from hello [Microsoft Download Center][powerquery-download] and install it.</span></span>

## <a name="import-hdinsight-data-into-excel"></a><span data-ttu-id="e8ecd-117">Importation de données HDInsight dans Excel</span><span class="sxs-lookup"><span data-stu-id="e8ecd-117">Import HDInsight data into Excel</span></span>
<span data-ttu-id="e8ecd-118">Hello complément Power Query pour Excel rend tooimport facilement les données à partir de votre cluster HDInsight dans Excel, où des outils de BI tels que PowerPivot et de mappage de l’alimentation peuvent être tooinspect utilisé, analyser et présenter des données hello.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-118">hello Power Query add-in for Excel makes it easy tooimport data from your HDInsight cluster into Excel, where BI tools such as PowerPivot and Power Map can be used tooinspect, analyze, and present hello data.</span></span>

<span data-ttu-id="e8ecd-119">**tooimport des données à partir d’un cluster HDInsight**</span><span class="sxs-lookup"><span data-stu-id="e8ecd-119">**tooimport data from an HDInsight cluster**</span></span>

1. <span data-ttu-id="e8ecd-120">Ouvrez Excel.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-120">Open Excel.</span></span>
2. <span data-ttu-id="e8ecd-121">Créez un classeur vide.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-121">Create a new blank workbook.</span></span>
3. <span data-ttu-id="e8ecd-122">Effectuez hello selon la version d’Excel hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e8ecd-122">Perform hello following steps based on hello Excel version:</span></span>

    - <span data-ttu-id="e8ecd-123">Excel 2016</span><span class="sxs-lookup"><span data-stu-id="e8ecd-123">Excel 2016</span></span>

        - <span data-ttu-id="e8ecd-124">Cliquez sur hello **données** menu, cliquez sur **obtenir des données** de hello **obtenir et transformer des données** du ruban, cliquez sur **à partir de Azure**, puis cliquez sur  **À partir d’Azure HDInsight(HDFS)**.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-124">Click hello **Data** menu, click **Get Data** from hello **Get & Transform Data** ribbon, click **From Azure**, and then click **From Azure HDInsight(HDFS)**.</span></span>

        ![HDI.PowerQuery.SelectHdiSource](./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.excel2016.png)

    - <span data-ttu-id="e8ecd-126">Excel 2013/2010</span><span class="sxs-lookup"><span data-stu-id="e8ecd-126">Excel 2013/2010</span></span>

        - <span data-ttu-id="e8ecd-127">Cliquez sur hello **Power Query** menu, cliquez sur **à partir de Azure**, puis cliquez sur **à partir de Microsoft Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-127">Click hello **Power Query** menu, click **From Azure**, and then click **From Microsoft Azure HDInsight**.</span></span>
   
        ![HDI.PowerQuery.SelectHdiSource][image-hdi-powerquery-hdi-source]
       
        <span data-ttu-id="e8ecd-129">**Remarque :** si vous ne voyez pas hello **Power Query** menu, accédez trop**fichier** > **Options** > **descompléments**, puis sélectionnez **compléments COM** de déroulante hello **gérer** zone en bas de hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-129">**Note:** If you don't see hello **Power Query** menu, go too**File** > **Options** > **Add-Ins**, and select **COM Add-ins** from hello drop-down **Manage** box at hello bottom of hello page.</span></span> <span data-ttu-id="e8ecd-130">Sélectionnez hello **accédez...**  bouton et vérifier cette zone hello pour hello Power Query pour Excel a été vérifiée.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-130">Select hello **Go...** button and verify that hello box for hello Power Query for Excel add-in has been checked.</span></span>
       
        <span data-ttu-id="e8ecd-131">**Remarque :** Power Query vous permet également de données tooimport de HDFS en cliquant sur **à partir d’autres Sources**.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-131">**Note:** Power Query also allows you tooimport data from HDFS by clicking **From Other Sources**.</span></span>
4. <span data-ttu-id="e8ecd-132">Pour **nom de compte**, entrez le nom hello de compte de stockage d’objets Blob Azure hello associé à votre cluster, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-132">For **Account Name**, enter hello name of hello Azure Blob storage account associated with your cluster, and then click **OK**.</span></span> <span data-ttu-id="e8ecd-133">Ce compte peut être hello [compte de stockage par défaut](hdinsight-administer-use-management-portal.md#find-the-default-storage-account) ou un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-133">This account can be hello [default storage account](hdinsight-administer-use-management-portal.md#find-the-default-storage-account) or a linked storage account.</span></span>  <span data-ttu-id="e8ecd-134">format de Hello est *https://&lt;StorageAccountName >.blob.core.windows.net/*.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-134">hello format is *https://&lt;StorageAccountName>.blob.core.windows.net/*.</span></span>
5. <span data-ttu-id="e8ecd-135">Pour **clé de compte**, entrez la clé hello pour hello compte de stockage Blob, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-135">For **Account Key**, enter hello key for hello Blob storage account, and then click **Save**.</span></span> <span data-ttu-id="e8ecd-136">(Vous devez hello uniquement des informations compte hello tooenter lors du premier qu'accès cette banque d’informations.)</span><span class="sxs-lookup"><span data-stu-id="e8ecd-136">(You need tooenter hello account information only hello first time you access this store.)</span></span>
6. <span data-ttu-id="e8ecd-137">Bonjour **Navigator** volet hello à gauche de l’éditeur de requête de hello, double-cliquez sur le nom de conteneur de stockage Blob hello.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-137">In hello **Navigator** pane on hello left of hello Query Editor, double-click hello Blob storage container name.</span></span> <span data-ttu-id="e8ecd-138">Par défaut, nom du conteneur hello est hello même nom que le nom du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-138">By default, hello container name is hello same name as hello cluster name.</span></span>
7. <span data-ttu-id="e8ecd-139">Recherchez **HiveSampleData.txt** Bonjour **nom** colonne (chemin d’accès du dossier hello **... / hive/de l’entrepôt/hivesampletable/**), puis cliquez sur **binaire** sur gauche hello de HiveSampleData.txt.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-139">Locate **HiveSampleData.txt** in hello **Name** column (hello folder path is **../hive/warehouse/hivesampletable/**), and then click **Binary** on hello left of HiveSampleData.txt.</span></span> <span data-ttu-id="e8ecd-140">HiveSampleData.txt est fourni avec tous les clusters de hello.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-140">HiveSampleData.txt comes with all hello cluster.</span></span> <span data-ttu-id="e8ecd-141">Si vous le souhaitez, vous pouvez utiliser votre propre fichier.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-141">Optionally, you can use your own file.</span></span>
   
    ![HDI.PowerQuery.ImportData][image-hdi-powerquery-importdata]
8. <span data-ttu-id="e8ecd-143">Si vous le souhaitez, vous pouvez renommer les noms de colonne hello.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-143">If you want, you can rename hello column names.</span></span> <span data-ttu-id="e8ecd-144">Lorsque vous êtes prêt, cliquez sur **Fermer et charger**.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-144">When you are ready, click **Close & Load**.</span></span>  <span data-ttu-id="e8ecd-145">les données de salutation a été chargé tooyour classeur :</span><span class="sxs-lookup"><span data-stu-id="e8ecd-145">hello data has been loaded tooyour workbook:</span></span>
   
    ![HDI.PowerQuery.ImportedTable][image-hdi-powerquery-imported-table]

## <a name="next-steps"></a><span data-ttu-id="e8ecd-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e8ecd-147">Next steps</span></span>
<span data-ttu-id="e8ecd-148">Dans cet article, vous avez appris comment toouse Power tooretrieve interroge les données de HDInsight dans Excel.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-148">In this article, you learned how toouse Power Query tooretrieve data from HDInsight into Excel.</span></span> <span data-ttu-id="e8ecd-149">De la même façon, vous pouvez extraire des données de HDInsight et les importer dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-149">Similarly, you can retrieve data from HDInsight into Azure SQL Database.</span></span> <span data-ttu-id="e8ecd-150">Il est également données tooupload possible dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8ecd-150">It is also possible tooupload data into HDInsight.</span></span> <span data-ttu-id="e8ecd-151">toolearn, voir hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="e8ecd-151">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="e8ecd-152">[Rejoignez Excel tooHDInsight hello Microsoft ODBC Driver de la ruche][hdinsight-ODBC]</span><span class="sxs-lookup"><span data-stu-id="e8ecd-152">[Connect Excel tooHDInsight with hello Microsoft Hive ODBC Driver][hdinsight-ODBC]</span></span>
* <span data-ttu-id="e8ecd-153">[Télécharger des données tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="e8ecd-153">[Upload Data tooHDInsight][hdinsight-upload-data]</span></span>

[hdinsight-ODBC]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[image-hdi-powerquery-hdi-source]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.png
[image-hdi-powerquery-importdata]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importdata.png
[image-hdi-powerquery-imported-table]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importedtable.PNG

[powerquery-download]: http://go.microsoft.com/fwlink/?LinkID=286689