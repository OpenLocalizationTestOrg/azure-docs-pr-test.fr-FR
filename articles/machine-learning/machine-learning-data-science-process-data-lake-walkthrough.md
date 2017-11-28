---
title: "Science des données scalable avec Azure Data Lake : procédure complète | Microsoft Docs"
description: "Des tâches de toouse Azure Data Lake toodo exploration et binary classification des données sur un jeu de données."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 91a8207f-1e57-4570-b7fc-7c5fa858ffeb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: bradsev;weig
ms.openlocfilehash: 8b05457ae7045a7aaed350a7502469f2247161e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a><span data-ttu-id="301a5-103">Science des données scalable avec Azure Data Lake : procédure complète</span><span class="sxs-lookup"><span data-stu-id="301a5-103">Scalable Data Science with Azure Data Lake: An end-to-end Walkthrough</span></span>
<span data-ttu-id="301a5-104">Cette procédure pas à pas montre comment l’exploration de données Azure Data Lake toodo toouse et les tâches de classification binaire d’un échantillon de hello NYC taxi voyage et tarif toopredict de dataset ou non une info-bulle sera versée à un tarif.</span><span class="sxs-lookup"><span data-stu-id="301a5-104">This walkthrough shows how toouse Azure Data Lake toodo data exploration and binary classification tasks on a sample of hello NYC taxi trip and fare dataset toopredict whether or not a tip will be paid by a fare.</span></span> <span data-ttu-id="301a5-105">Il vous guide à travers les étapes de hello Hello [processus de science des données équipe](http://aka.ms/datascienceprocess), de bout en bout, à partir de la formation de toomodel d’acquisition de données, puis déploiement toohello d’un service web qui publie le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="301a5-105">It walks you through hello steps of hello [Team Data Science Process](http://aka.ms/datascienceprocess), end-to-end, from data acquisition toomodel training, and then toohello deployment of a web service that publishes hello model.</span></span>

### <a name="azure-data-lake-analytics"></a><span data-ttu-id="301a5-106">Service Analytique Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="301a5-106">Azure Data Lake Analytics</span></span>
<span data-ttu-id="301a5-107">Hello [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) a toutes les hello fonctionnalités requis toomake plus facile pour les données scientifiques toostore de tout traitement de données de taille, forme et la vitesse et tooconduct, advanced analytique et une modélisation machine learning avec une haute évolutivité à moindre coût.</span><span class="sxs-lookup"><span data-stu-id="301a5-107">hello [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) has all hello capabilities required toomake it easy for data scientists toostore data of any size, shape and speed, and tooconduct data processing, advanced analytics, and machine learning modeling with high scalability in a cost-effective way.</span></span>   <span data-ttu-id="301a5-108">Le paiement s’effectue par travail effectué, seulement lorsque les données sont réellement en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="301a5-108">You pay on a per-job basis, only when data is actually being processed.</span></span> <span data-ttu-id="301a5-109">Analytique de LAC de données Azure inclut U-SQL, un autre langage que fusion hello nature déclarative de SQL avec la puissance expressive hello c# tooprovide évolutive distributed capacité de requête.</span><span class="sxs-lookup"><span data-stu-id="301a5-109">Azure Data Lake Analytics includes U-SQL, a language that blends hello declarative nature of SQL with hello expressive power of C# tooprovide scalable distributed query capability.</span></span> <span data-ttu-id="301a5-110">Il vous permet de tooprocess une logique personnalisée d’insertion de données non structurées en appliquant le schéma lors de la lecture, et défini par l’utilisateur (UDF) de fonctions et inclut l’extensibilité tooenable un contrôle fin sur la façon tooexecute à grande échelle.</span><span class="sxs-lookup"><span data-stu-id="301a5-110">It enables you tooprocess unstructured data by applying schema on read, insert custom logic and user defined functions (UDFs), and includes extensibility tooenable fine grained control over how tooexecute at scale.</span></span> <span data-ttu-id="301a5-111">toolearn en savoir plus sur la philosophie de conception hello derrière U-SQL, consultez [billet de blog de Visual Studio](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="301a5-111">toolearn more about hello design philosophy behind U-SQL, see [Visual Studio blog post](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

<span data-ttu-id="301a5-112">Il est également un composant essentiel de Cortana Analytics Suite et fonctionne avec Azure SQL Data Warehouse, Power BI et Data Factory.</span><span class="sxs-lookup"><span data-stu-id="301a5-112">Data Lake Analytics is also a key part of Cortana Analytics Suite and works with Azure SQL Data Warehouse, Power BI, and Data Factory.</span></span> <span data-ttu-id="301a5-113">Cela vous offre une plateforme d’analyse avancée et de Big Data cloud complète.</span><span class="sxs-lookup"><span data-stu-id="301a5-113">This gives you a complete cloud big data and advanced analytics platform.</span></span>

<span data-ttu-id="301a5-114">Cette procédure pas à pas commence par décrire les conditions préalables de hello et les ressources qui sont nécessaires toocomplete hello tâches avec des données de LAC Analytique qui forment le processus de science des données hello et comment tooinstall les.</span><span class="sxs-lookup"><span data-stu-id="301a5-114">This walkthrough begins by describing hello prerequisites and resources that are needed toocomplete hello tasks with Data Lake Analytics that form hello data science process and how tooinstall them.</span></span> <span data-ttu-id="301a5-115">Il décrit les étapes de traitement des données hello à l’aide de U-SQL et se termine en montrant comment toouse Python et Hive avec Azure Machine Learning Studio toobuild et déployer des modèles prédictifs hello.</span><span class="sxs-lookup"><span data-stu-id="301a5-115">Then it outlines hello data processing steps using U-SQL and concludes by showing how toouse Python and Hive with Azure Machine Learning Studio toobuild and deploy hello predictive models.</span></span> 

### <a name="u-sql-and-visual-studio"></a><span data-ttu-id="301a5-116">U-SQL et Visual Studio</span><span class="sxs-lookup"><span data-stu-id="301a5-116">U-SQL and Visual Studio</span></span>
<span data-ttu-id="301a5-117">Cette procédure pas à pas recommande l’utilisation de Visual Studio tooedit U-SQL scripts tooprocess hello dataset.</span><span class="sxs-lookup"><span data-stu-id="301a5-117">This walkthrough recommends using Visual Studio tooedit U-SQL scripts tooprocess hello dataset.</span></span> <span data-ttu-id="301a5-118">les scripts Hello U-SQL sont décrites ici et dans un fichier distinct.</span><span class="sxs-lookup"><span data-stu-id="301a5-118">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="301a5-119">processus de Hello inclut absorber, Explorer et d’échantillonnage des données de salutation.</span><span class="sxs-lookup"><span data-stu-id="301a5-119">hello process includes ingesting, exploring, and sampling hello data.</span></span> <span data-ttu-id="301a5-120">Il montre également comment toorun U-SQL un script de travail à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="301a5-120">It also shows how toorun a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="301a5-121">Tables de la ruche sont créés pour les données de salutation dans une construction d’hello toofacilitate de cluster HDInsight associée et le déploiement d’un modèle de classification binaire dans Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="301a5-121">Hive tables are created for hello data in an associated HDInsight cluster toofacilitate hello building and deployment of a binary classification model in Azure Machine Learning Studio.</span></span>  

### <a name="python"></a><span data-ttu-id="301a5-122">Python</span><span class="sxs-lookup"><span data-stu-id="301a5-122">Python</span></span>
<span data-ttu-id="301a5-123">Cette procédure pas à pas contient également une section qui montre comment toobuild et déployer un modèle de prévision à l’aide de Python avec Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="301a5-123">This walkthrough also contains a section that shows how toobuild and deploy a predictive model using Python with Azure Machine Learning Studio.</span></span>  <span data-ttu-id="301a5-124">Nous fournissons un bloc-notes jupyter avec des scripts Python hello pour ces étapes de ce processus.</span><span class="sxs-lookup"><span data-stu-id="301a5-124">We provide a Jupyter notebook with hello Python scripts for these steps in this process.</span></span> <span data-ttu-id="301a5-125">ordinateur portable de Hello inclut du code pour certaines étapes ingénierie de fonctionnalité supplémentaire et la construction de modèles tels que la classification multiclasse et le modèle de classification binaire toohello décrite ici en outre de modélisation de régression.</span><span class="sxs-lookup"><span data-stu-id="301a5-125">hello notebook includes code for some additional feature engineering steps and models construction such as multiclass classification and regression modeling in addition toohello binary classification model outlined here.</span></span> <span data-ttu-id="301a5-126">tâche de régression Hello est toopredict hello Conseil hello basé sur d’autres fonctionnalités de l’info-bulle.</span><span class="sxs-lookup"><span data-stu-id="301a5-126">hello regression task is toopredict hello amount of hello tip based on other tip features.</span></span> 

### <a name="azure-machine-learning"></a><span data-ttu-id="301a5-127">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="301a5-127">Azure Machine Learning</span></span>
<span data-ttu-id="301a5-128">Azure Machine Learning Studio est utilisé toobuild et déployer des modèles prédictifs hello.</span><span class="sxs-lookup"><span data-stu-id="301a5-128">Azure Machine Learning Studio is used toobuild and deploy hello predictive models.</span></span> <span data-ttu-id="301a5-129">Cette opération est effectuée selon deux approches : tout d’abord avec des scripts Python, puis avec des tables Hive sur un cluster HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="301a5-129">This is done using two approaches: first with Python scripts and then with Hive tables on an HDInsight (Hadoop) cluster.</span></span>

### <a name="scripts"></a><span data-ttu-id="301a5-130">Scripts</span><span class="sxs-lookup"><span data-stu-id="301a5-130">Scripts</span></span>
<span data-ttu-id="301a5-131">Uniquement hello deux principales étapes sont décrites dans cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="301a5-131">Only hello principal steps are outlined in this walkthrough.</span></span> <span data-ttu-id="301a5-132">Vous pouvez télécharger hello complète **script U-SQL** et **bloc-notes Jupyter** de [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="301a5-132">You can download hello full **U-SQL script** and **Jupyter Notebook** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="301a5-133">Composants requis</span><span class="sxs-lookup"><span data-stu-id="301a5-133">Prerequisites</span></span>
<span data-ttu-id="301a5-134">Avant de commencer ces rubriques, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="301a5-134">Before you begin these topics, you must have hello following:</span></span>

* <span data-ttu-id="301a5-135">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="301a5-135">An Azure subscription.</span></span> <span data-ttu-id="301a5-136">Si vous n’en avez pas, consultez [Obtenir une version d’évaluation gratuite Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="301a5-136">If you do not already have one, see [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="301a5-137">[Recommandé] Visual Studio 2013 ou ultérieur.</span><span class="sxs-lookup"><span data-stu-id="301a5-137">[Recommended] Visual Studio 2013 or later.</span></span> <span data-ttu-id="301a5-138">Si vous ne disposez pas d’une de ces versions, vous pouvez télécharger une version Community gratuite depuis [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span><span class="sxs-lookup"><span data-stu-id="301a5-138">If you do not already have one of these versions installed, you can download a free Community version from [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span></span>

> [!NOTE]
> <span data-ttu-id="301a5-139">Au lieu de Visual Studio, vous pouvez également utiliser des requêtes de Azure Data Lake toosubmit hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="301a5-139">Instead of Visual Studio, you can also use hello Azure Portal toosubmit Azure Data Lake queries.</span></span> <span data-ttu-id="301a5-140">Il fournit des instructions sur comment toodo donc avec Visual Studio et sur le portail dans la section de hello hello intitulée **traiter les données avec U-SQL**.</span><span class="sxs-lookup"><span data-stu-id="301a5-140">We will provide instructions on how toodo so both with Visual Studio and on hello portal in hello section titled **Process data with U-SQL**.</span></span> 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a><span data-ttu-id="301a5-141">Préparer l’environnement de science des données pour Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="301a5-141">Prepare data science environment for Azure Data Lake</span></span>
<span data-ttu-id="301a5-142">environnement de science des données tooprepare hello pour cette procédure pas à pas, créez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="301a5-142">tooprepare hello data science environment for this walkthrough, create hello following resources:</span></span>

* <span data-ttu-id="301a5-143">Azure Data Lake Store (ADLS)</span><span class="sxs-lookup"><span data-stu-id="301a5-143">Azure Data Lake Store (ADLS)</span></span> 
* <span data-ttu-id="301a5-144">Azure Data Lake Analytics (ADLA)</span><span class="sxs-lookup"><span data-stu-id="301a5-144">Azure Data Lake Analytics (ADLA)</span></span>
* <span data-ttu-id="301a5-145">Compte de stockage d’objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="301a5-145">Azure Blob storage account</span></span>
* <span data-ttu-id="301a5-146">Compte Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="301a5-146">Azure Machine Learning Studio account</span></span>
* <span data-ttu-id="301a5-147">Outils Azure Data Lake pour Visual Studio (Recommandé)</span><span class="sxs-lookup"><span data-stu-id="301a5-147">Azure Data Lake Tools for Visual Studio (Recommended)</span></span>

<span data-ttu-id="301a5-148">Cette section fournit des instructions sur la façon de toocreate de ces ressources.</span><span class="sxs-lookup"><span data-stu-id="301a5-148">This section provides instructions on how toocreate each of these resources.</span></span> <span data-ttu-id="301a5-149">Si vous choisissez toouse tables Hive avec Azure Machine Learning, au lieu de Python, toobuild un modèle, vous devez également tooprovision un cluster HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="301a5-149">If you choose toouse Hive tables with Azure Machine Learning, instead of Python, toobuild a model,you will also need tooprovision an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="301a5-150">Cette procédure de remplacement dans décrits dans la section appropriée de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="301a5-150">This alternative procedure in described in hello appropriate section below.</span></span>


> [!NOTE]
> <span data-ttu-id="301a5-151">Hello **Azure Data Lake Store** peuvent être créés séparément ou lorsque vous créez hello **Analytique de LAC de données Azure** comme stockage par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="301a5-151">hello **Azure Data Lake Store** can be created either separately or when you create hello **Azure Data Lake Analytics** as hello default storage.</span></span> <span data-ttu-id="301a5-152">Des instructions sont référencées pour la création de chacune de ces ressources ci-dessous séparément, mais hello compte de stockage lac de données ne doive pas être créée séparément.</span><span class="sxs-lookup"><span data-stu-id="301a5-152">Instructions are referenced for creating each of these resources separately below, but hello Data Lake storage account need not be created separately.</span></span>
>
> 

### <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="301a5-153">Créer un Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="301a5-153">Create an Azure Data Lake Store</span></span>


<span data-ttu-id="301a5-154">Créer un ADLS de hello [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="301a5-154">Create an ADLS from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="301a5-155">Pour en savoir plus, consultez [Créer un cluster HDInsight avec Data Lake Store à l’aide du portail Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="301a5-155">For details, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="301a5-156">Être tooset que des hello Cluster AAD identité Bonjour **DataSource** Panneau de hello **Configuration facultative** panneau décrit il.</span><span class="sxs-lookup"><span data-stu-id="301a5-156">Be sure tooset up hello Cluster AAD Identity in hello **DataSource** blade of hello **Optional Configuration** blade described there.</span></span> 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a><span data-ttu-id="301a5-158">Créer un compte Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="301a5-158">Create an Azure Data Lake Analytics account</span></span>
<span data-ttu-id="301a5-159">Créer un compte ADLA à partir de hello [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="301a5-159">Create an ADLA account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="301a5-160">Pour en savoir plus, consultez [Didacticiel : Prise en main du service Azure Data Lake Analytics à l’aide du portail Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="301a5-160">For details, see [Tutorial: get started with Azure Data Lake Analytics using Azure Portal](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span> 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="301a5-162">Créer un compte de stockage d’objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="301a5-162">Create an Azure Blob storage account</span></span>
<span data-ttu-id="301a5-163">Créer un compte de stockage d’objets Blob Azure à partir de hello [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="301a5-163">Create an Azure Blob storage account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="301a5-164">Pour plus d’informations, consultez hello créer un compte de stockage section [comptes de stockage sur Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="301a5-164">For details, see hello Create a storage account section in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a><span data-ttu-id="301a5-166">Configurer un compte Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="301a5-166">Set up an Azure Machine Learning Studio account</span></span>
<span data-ttu-id="301a5-167">Signer/dans Azure Machine Learning Studio à partir de hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) page.</span><span class="sxs-lookup"><span data-stu-id="301a5-167">Sign up/into Azure Machine Learning Studio from hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) page.</span></span> <span data-ttu-id="301a5-168">Cliquez sur hello **prise en main** bouton, puis choisissez un « Espace de travail libre » ou un « Espace de travail Standard ».</span><span class="sxs-lookup"><span data-stu-id="301a5-168">Click on hello **Get started now** button and then choose a "Free Workspace" or "Standard Workspace".</span></span> <span data-ttu-id="301a5-169">Après cela, vous serez en mesure de toocreate des expériences dans Azure ML Studio.</span><span class="sxs-lookup"><span data-stu-id="301a5-169">After this you will be able toocreate experiments in Azure ML Studio.</span></span>  

### <a name="install-azure-data-lake-tools-recommended"></a><span data-ttu-id="301a5-170">Installer les outils Azure Data Lake [Recommandé]</span><span class="sxs-lookup"><span data-stu-id="301a5-170">Install Azure Data Lake Tools [Recommended]</span></span>
<span data-ttu-id="301a5-171">Installez les outils Azure Data Lake pour votre version de Visual Studio sur la page [Outils Azure Data Lake pour Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="301a5-171">Install Azure Data Lake Tools for your version of Visual Studio from [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

<span data-ttu-id="301a5-173">Une fois l’installation de hello terminée, ouvrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="301a5-173">After hello installation finishes successfully, open up Visual Studio.</span></span> <span data-ttu-id="301a5-174">Vous devez voir les menus de hello hello Data Lake onglet en haut de hello.</span><span class="sxs-lookup"><span data-stu-id="301a5-174">You should see hello Data Lake tab hello menu at hello top.</span></span> <span data-ttu-id="301a5-175">Vos ressources Azure doivent apparaître dans le panneau gauche hello lorsque vous vous connectez à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="301a5-175">Your Azure resources should appear in hello left panel when you sign into your Azure account.</span></span>

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="hello-nyc-taxi-trips-dataset"></a><span data-ttu-id="301a5-177">jeu de données Hello NYC Taxi allers-retours</span><span class="sxs-lookup"><span data-stu-id="301a5-177">hello NYC Taxi Trips dataset</span></span>
<span data-ttu-id="301a5-178">Bonjour jeu de données que nous avons utilisé ici est un jeu de données disponible publiquement--hello [NYC Taxi allers-retours dataset](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="301a5-178">hello data set we used here is a publicly available dataset -- hello [NYC Taxi Trips dataset](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="301a5-179">Hello les données NYC Taxi voyage se compose d’environ 20 Go de fichiers CSV compressées (Go ~ 48 non compressé), l’enregistrement de plus de 173 millions hello et des boucles tarifs payé pour chaque sortie.</span><span class="sxs-lookup"><span data-stu-id="301a5-179">hello NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="301a5-180">Chaque enregistrement de voyage inclut les emplacements de collecte et de remise de hello et de, présentées de façon anonyme hack numéro de licence (du pilote), hello nombre de medallion (id unique de taxi).</span><span class="sxs-lookup"><span data-stu-id="301a5-180">Each trip record includes hello pickup and drop-off locations and times, anonymized hack (driver's) license number, and hello medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="301a5-181">les données de salutation couvre toutes les boucles dans l’année hello 2013 et sont fournies dans hello suivant deux jeux de données pour chaque mois :</span><span class="sxs-lookup"><span data-stu-id="301a5-181">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

* <span data-ttu-id="301a5-182">Hello 'trip_data' CSV contient les détails de voyage, telles que le nombre de personnes, collecte et cette chute points, durée de voyage, longueur de voyage.</span><span class="sxs-lookup"><span data-stu-id="301a5-182">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="301a5-183">Voici quelques exemples d’enregistrements :</span><span class="sxs-lookup"><span data-stu-id="301a5-183">Here are a few sample records:</span></span>
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* <span data-ttu-id="301a5-184">Hello 'trip_fare' CSV contient les détails des prix hello payé pour chaque sortie, comme type de paiement, montant de frais, surcharge et taxes, conseils et péage et montant total de hello payé.</span><span class="sxs-lookup"><span data-stu-id="301a5-184">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="301a5-185">Voici quelques exemples d’enregistrements :</span><span class="sxs-lookup"><span data-stu-id="301a5-185">Here are a few sample records:</span></span>
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="301a5-186">voyage toojoin de clé unique de Hello\_données et voyage\_tarif est composé de hello suivant trois champs : medallion, hack\_licence et pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="301a5-186">hello unique key toojoin trip\_data and trip\_fare is composed of hello following three fields: medallion, hack\_license and pickup\_datetime.</span></span> <span data-ttu-id="301a5-187">les fichiers CSV bruts Hello est accessible à partir d’un objet blob de stockage Azure publique.</span><span class="sxs-lookup"><span data-stu-id="301a5-187">hello raw CSV files can be accessed from a public Azure storage blob.</span></span> <span data-ttu-id="301a5-188">Hello script U-SQL pour cette jointure est Bonjour [joindre des tables voyage et tarif](#join) section.</span><span class="sxs-lookup"><span data-stu-id="301a5-188">hello U-SQL script for this join is in hello [Join trip and fare tables](#join) section.</span></span>

## <a name="process-data-with-u-sql"></a><span data-ttu-id="301a5-189">Traiter des données avec U-SQL</span><span class="sxs-lookup"><span data-stu-id="301a5-189">Process data with U-SQL</span></span>
<span data-ttu-id="301a5-190">Hello le traitement des données décrit notamment les tâches de cette section incluent absorber, la vérification de la qualité, Explorer et d’échantillonnage des données de salutation.</span><span class="sxs-lookup"><span data-stu-id="301a5-190">hello data processing tasks illustrated in this section include ingesting, checking quality, exploring, and sampling hello data.</span></span> <span data-ttu-id="301a5-191">Nous montrent également comment les tables voyage et tarif toojoin.</span><span class="sxs-lookup"><span data-stu-id="301a5-191">We also show how toojoin trip and fare tables.</span></span> <span data-ttu-id="301a5-192">section finale de Hello montre exécuter un travail par script U-SQL à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="301a5-192">hello final section shows run a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="301a5-193">Voici des liens tooeach sous-section :</span><span class="sxs-lookup"><span data-stu-id="301a5-193">Here are links tooeach subsection:</span></span>

* [<span data-ttu-id="301a5-194">Ingestion de données : données lues à partir d’un objet blob public</span><span class="sxs-lookup"><span data-stu-id="301a5-194">Data ingestion: read in data from public blob</span></span>](#ingest)
* [<span data-ttu-id="301a5-195">Contrôles de qualité des données</span><span class="sxs-lookup"><span data-stu-id="301a5-195">Data quality checks</span></span>](#quality)
* [<span data-ttu-id="301a5-196">Exploration des données</span><span class="sxs-lookup"><span data-stu-id="301a5-196">Data exploration</span></span>](#explore)
* [<span data-ttu-id="301a5-197">Joindre des tables relatives aux courses et aux tarifs</span><span class="sxs-lookup"><span data-stu-id="301a5-197">Join trip and fare tables</span></span>](#join)
* [<span data-ttu-id="301a5-198">Échantillonnage des données</span><span class="sxs-lookup"><span data-stu-id="301a5-198">Data sampling</span></span>](#sample)
* [<span data-ttu-id="301a5-199">Exécuter des travaux U-SQL</span><span class="sxs-lookup"><span data-stu-id="301a5-199">Run U-SQL jobs</span></span>](#run)

<span data-ttu-id="301a5-200">les scripts Hello U-SQL sont décrites ici et dans un fichier distinct.</span><span class="sxs-lookup"><span data-stu-id="301a5-200">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="301a5-201">Vous pouvez télécharger hello complète **scripts U-SQL** de [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="301a5-201">You can download hello full **U-SQL scripts** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

<span data-ttu-id="301a5-202">tooexecute U-SQL, ouvrez Visual Studio, cliquez sur **fichier--> Nouveau--> projet**, choisissez **U-SQL projet**, la nommer et enregistrer tooa dossier.</span><span class="sxs-lookup"><span data-stu-id="301a5-202">tooexecute U-SQL, Open Visual Studio, click **File --> New --> Project**, choose **U-SQL Project**, name and save it tooa folder.</span></span>

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> <span data-ttu-id="301a5-204">Il est possible de toouse hello Azure Portal tooexecute U-SQL au lieu de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="301a5-204">It is possible toouse hello Azure Portal tooexecute U-SQL instead of Visual Studio.</span></span> <span data-ttu-id="301a5-205">Vous pouvez rechercher des ressources d’Analytique de LAC de données Azure toohello sur le portail hello et soumettre des requêtes directement, comme illustré dans la figure suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="301a5-205">You can navigate toohello Azure Data Lake Analytics resource on hello portal and submit queries directly as illustrated in hello following figure.</span></span>
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <span data-ttu-id="301a5-207"><a name="ingest"></a>Ingestion de données : données lues à partir d’un objet blob public</span><span class="sxs-lookup"><span data-stu-id="301a5-207"><a name="ingest"></a>Data Ingestion: Read in data from public blob</span></span>
<span data-ttu-id="301a5-208">emplacement Hello de données hello Bonjour Azure blob est référencé en tant que  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**  et peuvent être extraites à l’aide de **Extractors.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="301a5-208">hello location of hello data in hello Azure blob is referenced as **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** and can be extracted using **Extractors.Csv()**.</span></span> <span data-ttu-id="301a5-209">Remplacez par votre propre nom de conteneur et le nom de compte de stockage dans les scripts suivants pour container_name@blob_storage_account_name dans l’adresse de wasb hello.</span><span class="sxs-lookup"><span data-stu-id="301a5-209">Substitute your own container name and storage account name in following scripts for container_name@blob_storage_account_name in hello wasb address.</span></span> <span data-ttu-id="301a5-210">Étant donné que les noms de fichiers hello sont au même format, nous pouvons utiliser **voyage\_data_ {\*\}.csv** tooread dans tous les fichiers de voyage 12.</span><span class="sxs-lookup"><span data-stu-id="301a5-210">Since hello file names are in same format, we can use **trip\_data_{\*\}.csv** tooread in all 12 trip files.</span></span> 

    ///Read in Trip data
    @trip0 =
        EXTRACT 
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string
    // This is reading 12 trip data from blob
    FROM "wasb://container_name@blob_storage_account_name.blob.core.windows.net/nyctaxitrip/trip_data_{*}.csv"
    USING Extractors.Csv();

<span data-ttu-id="301a5-211">Étant donné que les en-têtes dans la première ligne de hello, nous avons besoin des en-têtes de hello tooremove et modifier les types de colonne dans les colonnes appropriées.</span><span class="sxs-lookup"><span data-stu-id="301a5-211">Since there are headers in hello first row, we need tooremove hello headers and change column types into appropriate ones.</span></span> <span data-ttu-id="301a5-212">Nous pouvons enregistrer hello traité données tooAzure stockage lac de données à l’aide **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**à l’aide de compte de stockage d’objets Blob _ ou tooAzure  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** .</span><span class="sxs-lookup"><span data-stu-id="301a5-212">We can either save hello processed data tooAzure Data Lake Storage using **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ or tooAzure Blob storage account using  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**.</span></span> 

    // change data types
    @trip =
        SELECT 
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        DateTime.Parse(pickup_datetime) AS pickup_datetime,
        DateTime.Parse(dropoff_datetime) AS dropoff_datetime,
        Int32.Parse(passenger_count) AS passenger_count,
        Double.Parse(trip_time_in_secs) AS trip_time_in_secs,
        Double.Parse(trip_distance) AS trip_distance,
        (pickup_longitude==string.Empty ? 0: float.Parse(pickup_longitude)) AS pickup_longitude,
        (pickup_latitude==string.Empty ? 0: float.Parse(pickup_latitude)) AS pickup_latitude,
        (dropoff_longitude==string.Empty ? 0: float.Parse(dropoff_longitude)) AS dropoff_longitude,
        (dropoff_latitude==string.Empty ? 0: float.Parse(dropoff_latitude)) AS dropoff_latitude
    FROM @trip0
    WHERE medallion != "medallion";

    ////output data tooADL
    OUTPUT @trip   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data tooblob
    OUTPUT @trip   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

<span data-ttu-id="301a5-213">De même, nous pouvons lue dans les jeux de données de prix hello.</span><span class="sxs-lookup"><span data-stu-id="301a5-213">Similarly we can read in hello fare data sets.</span></span> <span data-ttu-id="301a5-214">Cliquez avec le bouton droit sur Azure Data Lake Store, vous pouvez choisir de toolook à vos données dans **portail Azure--> Explorateur de données** ou **l’Explorateur de fichiers** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="301a5-214">Right click Azure Data Lake Store, you can choose toolook at your data in **Azure Portal --> Data Explorer** or **File Explorer** within Visual Studio.</span></span> 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <span data-ttu-id="301a5-217"><a name="quality"></a>Contrôles de qualité des données</span><span class="sxs-lookup"><span data-stu-id="301a5-217"><a name="quality"></a>Data quality checks</span></span>
<span data-ttu-id="301a5-218">Une fois les tables voyage et tarif ont été lus dans, les contrôles de qualité des données est possible Bonjour de configuration suivant.</span><span class="sxs-lookup"><span data-stu-id="301a5-218">After trip and fare tables have been read in, data quality checks can be done in hello following way.</span></span> <span data-ttu-id="301a5-219">Hello, ce qui entraîne des fichiers CSV peut être stockage d’objets Blob tooAzure sortie ou d’Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="301a5-219">hello resulting CSV files can be output tooAzure Blob storage or Azure Data Lake Store.</span></span> 

<span data-ttu-id="301a5-220">Rechercher le nombre hello de medallions et unique de medallions :</span><span class="sxs-lookup"><span data-stu-id="301a5-220">Find hello number of medallions and unique number of medallions:</span></span>

    ///check hello number of medallions and unique number of medallions
    @trip2 =
        SELECT
        medallion,
        vendor_id,
        pickup_datetime.Month AS pickup_month
        FROM @trip;

    @ex_1 =
        SELECT
        pickup_month, 
        COUNT(medallion) AS cnt_medallion,
        COUNT(DISTINCT(medallion)) AS unique_medallion
        FROM @trip2
        GROUP BY pickup_month;
        OUTPUT @ex_1   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="301a5-221">Recherchez les medaillons ayant plus de 100 courses :</span><span class="sxs-lookup"><span data-stu-id="301a5-221">Find those medallions that had more than 100 trips:</span></span>

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="301a5-222">Recherchez les enregistrements non valides en termes de pickup_longitude :</span><span class="sxs-lookup"><span data-stu-id="301a5-222">Find those invalid records in terms of pickup_longitude:</span></span>

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="301a5-223">Recherchez les valeurs manquantes pour certaines variables :</span><span class="sxs-lookup"><span data-stu-id="301a5-223">Find missing values for some variables:</span></span>

    //check missing values
    @res =
        SELECT *,
               (medallion == null? 1 : 0) AS missing_medallion
        FROM @trip;

    @trip_summary6 =
        SELECT 
            vendor_id,
        SUM(missing_medallion) AS medallion_empty, 
        COUNT(medallion) AS medallion_total,
        COUNT(DISTINCT(medallion)) AS medallion_total_unique  
        FROM @res
        GROUP BY vendor_id;
    OUTPUT @trip_summary6
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <span data-ttu-id="301a5-224"><a name="explore"></a>Exploration des données</span><span class="sxs-lookup"><span data-stu-id="301a5-224"><a name="explore"></a>Data exploration</span></span>
<span data-ttu-id="301a5-225">Mieux comprendre les données de salutation, nous pouvons effectuer certains tooget d’exploration de données.</span><span class="sxs-lookup"><span data-stu-id="301a5-225">We can do some data exploration tooget a better understanding of hello data.</span></span>

<span data-ttu-id="301a5-226">Rechercher la distribution hello d’allers-retours pourboires et non a :</span><span class="sxs-lookup"><span data-stu-id="301a5-226">Find hello distribution of tipped and non-tipped trips:</span></span>

    ///tipped vs. not tipped distribution
    @tip_or_not =
        SELECT *,
               (tip_amount > 0 ? 1: 0) AS tipped
        FROM @fare;

    @ex_4 =
        SELECT tipped,
               COUNT(*) AS tip_freq
        FROM @tip_or_not
        GROUP BY tipped;
        OUTPUT @ex_4   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="301a5-227">Rechercher la distribution hello du montant de Conseil avec les valeurs limites : 0,5,10 et 20 dollars.</span><span class="sxs-lookup"><span data-stu-id="301a5-227">Find hello distribution of tip amount with cut-off values: 0,5,10,and 20 dollars.</span></span>

    //tip class/range distribution
    @tip_class =
        SELECT *,
               (tip_amount >20? 4: (tip_amount >10? 3:(tip_amount >5 ? 2:(tip_amount > 0 ? 1: 0)))) AS tip_class
        FROM @fare;
    @ex_5 =
        SELECT tip_class,
               COUNT(*) AS tip_freq
        FROM @tip_class
        GROUP BY tip_class;
        OUTPUT @ex_5   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="301a5-228">Recherchez les statistiques de base de la distance de la course :</span><span class="sxs-lookup"><span data-stu-id="301a5-228">Find basic statistics of trip distance:</span></span>

    // find basic statistics for trip_distance
    @trip_summary4 =
        SELECT 
            vendor_id,
            COUNT(*) AS cnt_row,
            MIN(trip_distance) AS min_trip_distance,
            MAX(trip_distance) AS max_trip_distance,
            AVG(trip_distance) AS avg_trip_distance 
        FROM @trip
        GROUP BY vendor_id;
    OUTPUT @trip_summary4
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

<span data-ttu-id="301a5-229">Rechercher des centiles hello de distance de voyage :</span><span class="sxs-lookup"><span data-stu-id="301a5-229">Find hello percentiles of trip distance:</span></span>

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="301a5-230"><a name="join"></a>Joindre des tables relatives aux courses et aux tarifs</span><span class="sxs-lookup"><span data-stu-id="301a5-230"><a name="join"></a>Join trip and fare tables</span></span>
<span data-ttu-id="301a5-231">Les tables relatives aux courses et aux tarifs peuvent être jointes par médaillon, hack_license et pickup_time.</span><span class="sxs-lookup"><span data-stu-id="301a5-231">Trip and fare tables can be joined by medallion, hack_license, and pickup_time.</span></span>

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output tooblob
    OUTPUT @model_data_full   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data tooADL
    OUTPUT @model_data_full   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


<span data-ttu-id="301a5-232">Pour chaque niveau du nombre de passagers, calculez le nombre de hello d’enregistrements, montant du Conseil moyenne, variance du montant de l’info-bulle, pourcentage de pourboires allers-retours.</span><span class="sxs-lookup"><span data-stu-id="301a5-232">For each level of passenger count, calculate hello number of records, average tip amount, variance of tip amount, percentage of tipped trips.</span></span>

    // contigency table
    @trip_summary8 =
        SELECT passenger_count,
               COUNT(*) AS cnt,
               AVG(tip_amount) AS avg_tip_amount,
               VAR(tip_amount) AS var_tip_amount,
               SUM(tipped) AS cnt_tipped,
               (float)SUM(tipped)/COUNT(*) AS pct_tipped
        FROM @model_data_full
        GROUP BY passenger_count;
        OUTPUT @trip_summary8
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <span data-ttu-id="301a5-233"><a name="sample"></a>Échantillonnage des données</span><span class="sxs-lookup"><span data-stu-id="301a5-233"><a name="sample"></a>Data sampling</span></span>
<span data-ttu-id="301a5-234">Tout d’abord, nous allons sélectionner aléatoirement 0,1 % de données de salutation à partir de la table jointe de hello :</span><span class="sxs-lookup"><span data-stu-id="301a5-234">First we randomly select 0.1% of hello data from hello joined table:</span></span>

    //random select 1/1000 data for modeling purpose
    @addrownumberres_randomsample =
    SELECT *,
            ROW_NUMBER() OVER() AS rownum
    FROM @model_data_full;

    @model_data_random_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_randomsample
    WHERE rownum % 1000 == 0;

    OUTPUT @model_data_random_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="301a5-235">Ensuite, nous procédons à un échantillonnage stratifié par variable binaire tip_class :</span><span class="sxs-lookup"><span data-stu-id="301a5-235">Then we do stratified sampling by binary variable tip_class:</span></span>

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output tooblob
    OUTPUT @model_data_stratified_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data tooADL
    OUTPUT @model_data_stratified_sample_1_1000   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="301a5-236"><a name="run"></a>Exécuter des travaux U-SQL</span><span class="sxs-lookup"><span data-stu-id="301a5-236"><a name="run"></a>Run U-SQL jobs</span></span>
<span data-ttu-id="301a5-237">Lorsque vous avez terminé la modification de scripts U-SQL, vous pouvez envoyer les serveur toohello à l’aide de votre compte Analytique de LAC de données Azure.</span><span class="sxs-lookup"><span data-stu-id="301a5-237">When you finish editing U-SQL scripts, you can submit them toohello server using your Azure Data Lake Analytics account.</span></span> <span data-ttu-id="301a5-238">Cliquez sur **Data Lake**, **Envoyer le travail**, sélectionnez votre **Compte Analytics**, choisissez **Parallélisme**, puis cliquez sur le bouton **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="301a5-238">Click **Data Lake**, **Submit Job**, select your **Analytics Account**, choose **Parallelism**, and click **Submit** button.</span></span>  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

<span data-ttu-id="301a5-240">Lors de la tâche de hello est lancé avec succès, état hello de votre travail s’affichera dans Visual Studio pour l’analyse.</span><span class="sxs-lookup"><span data-stu-id="301a5-240">When hello job is complied successfully, hello status of your job will be displayed in Visual Studio for monitoring.</span></span> <span data-ttu-id="301a5-241">Une fois le travail de hello terminée, vous pouvez même les processus de l’exécution du travail relecture hello et découvrez hello goulot d’étranglement étapes tooimprove l’efficacité de votre travail.</span><span class="sxs-lookup"><span data-stu-id="301a5-241">After hello job finishes running, you can even replay hello job execution process and find out hello bottleneck steps tooimprove your job efficiency.</span></span> <span data-ttu-id="301a5-242">Vous pouvez également passer tooAzure statut de hello toocheck Portal de vos travaux U-SQL.</span><span class="sxs-lookup"><span data-stu-id="301a5-242">You can also go tooAzure Portal toocheck hello status of your U-SQL jobs.</span></span>

 ![13.](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

<span data-ttu-id="301a5-245">Maintenant, vous pouvez vérifier les fichiers de sortie hello dans le stockage Blob Azure ou portail Azure.</span><span class="sxs-lookup"><span data-stu-id="301a5-245">Now you can check hello output files in either Azure Blob storage or Azure Portal.</span></span> <span data-ttu-id="301a5-246">Nous allons utiliser des données d’exemple hello stratifié pour notre modélisation à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="301a5-246">We will use hello stratified sample data for our modeling in hello next step.</span></span>

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a><span data-ttu-id="301a5-249">Créer et déployer des modèles dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="301a5-249">Build and deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="301a5-250">Nous allons montrer deux options disponibles pour les données toopull dans Azure Machine Learning toobuild et</span><span class="sxs-lookup"><span data-stu-id="301a5-250">We demonstrate two options available for you toopull data into Azure Machine Learning toobuild and</span></span> 

* <span data-ttu-id="301a5-251">Dans la première option de hello, vous utilisez des données hello échantillonnée a été écrit tooan d’objets Blob Azure (Bonjour **d’échantillonnage des données** étape ci-dessus) et utiliser Python toobuild et déployer des modèles à partir d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="301a5-251">In hello first option, you use hello sampled data that has been written tooan Azure Blob (in hello **Data sampling** step above) and use Python toobuild and deploy models from Azure Machine Learning.</span></span> 
* <span data-ttu-id="301a5-252">Dans la deuxième option de hello, vous interrogez des données de hello dans Azure Data Lake directement à l’aide d’une requête Hive.</span><span class="sxs-lookup"><span data-stu-id="301a5-252">In hello second option, you query hello data in Azure Data Lake directly using a Hive query.</span></span> <span data-ttu-id="301a5-253">Cette option nécessite que vous créez un nouveau cluster HDInsight ou utilisez un cluster HDInsight existant où hello ruche tables de données de NY Taxi toohello de point dans le stockage de LAC de données Azure.</span><span class="sxs-lookup"><span data-stu-id="301a5-253">This option requires that you create a new HDInsight cluster or use an existing HDInsight cluster where hello Hive tables point toohello NY Taxi data in Azure Data Lake Storage.</span></span>  <span data-ttu-id="301a5-254">Nous abordons ces deux options ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="301a5-254">We discuss both these options below.</span></span> 

## <a name="option-1-use-python-toobuild-and-deploy-machine-learning-models"></a><span data-ttu-id="301a5-255">Option 1 : Utilisation de Python toobuild et déployer des modèles d’apprentissage automatique</span><span class="sxs-lookup"><span data-stu-id="301a5-255">Option 1: Use Python toobuild and deploy machine learning models</span></span>
<span data-ttu-id="301a5-256">toobuild et le déploiement des modèles d’apprentissage automatique à l’aide de Python, créez un bloc-notes Jupyter sur votre ordinateur local ou dans Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="301a5-256">toobuild and deploy machine learning models using Python, create a Jupyter Notebook on your local machine or in Azure Machine Learning Studio.</span></span> <span data-ttu-id="301a5-257">Hello bloc-notes Jupyter fourni sur [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contient hello tooexplore de code complet, de visualiser les données, de l’ingénierie de fonctionnalité, de modélisation et de déploiement.</span><span class="sxs-lookup"><span data-stu-id="301a5-257">hello Jupyter Notebook  provided on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contains hello full code tooexplore, visualize data, feature engineering, modeling and deployment.</span></span> <span data-ttu-id="301a5-258">Dans cet article, nous indiquons simplement hello modélisation et déploiement.</span><span class="sxs-lookup"><span data-stu-id="301a5-258">In this article, we show just hello modeling and deployment.</span></span> 

### <a name="import-python-libraries"></a><span data-ttu-id="301a5-259">Importer des bibliothèques Python</span><span class="sxs-lookup"><span data-stu-id="301a5-259">Import Python libraries</span></span>
<span data-ttu-id="301a5-260">Bonjour toorun de commande exemple Bloc-notes Jupyter ou hello du fichier de script Python, hello Python packages suivants sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="301a5-260">In order toorun hello sample Jupyter Notebook or hello Python script file, hello following Python packages are needed.</span></span> <span data-ttu-id="301a5-261">Si vous utilisez hello service de AzureML bloc-notes, ces packages ont été préinstallés.</span><span class="sxs-lookup"><span data-stu-id="301a5-261">If you are using hello AzureML Notebook service, these packages have been pre-installed.</span></span>

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random
    import sklearn
    from sklearn.linear_model import LogisticRegression
    from sklearn.cross_validation import train_test_split
    from sklearn import metrics
    from __future__ import division
    from sklearn import linear_model
    from azureml import services


### <a name="read-in-hello-data-from-blob"></a><span data-ttu-id="301a5-262">Lire à partir de l’objet blob de données hello</span><span class="sxs-lookup"><span data-stu-id="301a5-262">Read in hello data from blob</span></span>
* <span data-ttu-id="301a5-263">Chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="301a5-263">Connection String</span></span>   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* <span data-ttu-id="301a5-264">Lire sous forme de texte</span><span class="sxs-lookup"><span data-stu-id="301a5-264">Read in as text</span></span>
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds tooread in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* <span data-ttu-id="301a5-266">Ajouter des noms de colonnes et des colonnes distinctes</span><span class="sxs-lookup"><span data-stu-id="301a5-266">Add column names and separate columns</span></span>
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* <span data-ttu-id="301a5-267">Modifier certaines toonumeric de colonnes</span><span class="sxs-lookup"><span data-stu-id="301a5-267">Change some columns toonumeric</span></span>
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a><span data-ttu-id="301a5-268">Créer des modèles Machine Learning</span><span class="sxs-lookup"><span data-stu-id="301a5-268">Build machine learning models</span></span>
<span data-ttu-id="301a5-269">Ici, nous créons un toopredict de modèle de classification binaire si un voyage est incliné ou non.</span><span class="sxs-lookup"><span data-stu-id="301a5-269">Here we build a binary classification model toopredict whether a trip is tipped or not.</span></span> <span data-ttu-id="301a5-270">Bonjour bloc-notes Jupyter vous trouverez deux autres modèles : classification multiclasse et les modèles de régression.</span><span class="sxs-lookup"><span data-stu-id="301a5-270">In hello Jupyter Notebook you can find other two models: multiclass classification, and regression models.</span></span>

* <span data-ttu-id="301a5-271">Tout d’abord, nous devons toocreate variables factice qui peuvent être utilisés dans scikit-en savoir plus les modèles</span><span class="sxs-lookup"><span data-stu-id="301a5-271">First we need toocreate dummy variables that can be used in scikit-learn models</span></span>
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* <span data-ttu-id="301a5-272">Créer la trame de données pour la modélisation de hello</span><span class="sxs-lookup"><span data-stu-id="301a5-272">Create data frame for hello modeling</span></span>
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* <span data-ttu-id="301a5-273">Apprentissage et test de fractionnement de 60 à 40</span><span class="sxs-lookup"><span data-stu-id="301a5-273">Training and testing 60-40 split</span></span>
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* <span data-ttu-id="301a5-274">Régression logistique dans le jeu d’apprentissage</span><span class="sxs-lookup"><span data-stu-id="301a5-274">Logistic Regression in training set</span></span>
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* <span data-ttu-id="301a5-275">Noter le jeu de données de test</span><span class="sxs-lookup"><span data-stu-id="301a5-275">Score testing data set</span></span>
  
        Y_test_pred = logit_fit.predict(X_test)
* <span data-ttu-id="301a5-276">Calculer les mesures d’évaluation</span><span class="sxs-lookup"><span data-stu-id="301a5-276">Calculate Evaluation metrics</span></span>
  
        fpr_train, tpr_train, thresholds_train = metrics.roc_curve(Y_train, Y_train_pred)
        print fpr_train, tpr_train, thresholds_train
  
        fpr_test, tpr_test, thresholds_test = metrics.roc_curve(Y_test, Y_test_pred) 
        print fpr_test, tpr_test, thresholds_test
  
        #AUC
        print metrics.auc(fpr_train,tpr_train)
        print metrics.auc(fpr_test,tpr_test)
  
        #Confusion Matrix
        print metrics.confusion_matrix(Y_train,Y_train_pred)
        print metrics.confusion_matrix(Y_test,Y_test_pred)
  
       ![c2](./media/machine-learning-data-science-process-data-lake-walkthrough/c2-py-logit-evaluation.PNG)

### <a name="build-web-service-api-and-consume-it-in-python"></a><span data-ttu-id="301a5-277">Créer une API de service web et l’exploiter dans Python</span><span class="sxs-lookup"><span data-stu-id="301a5-277">Build Web Service API and consume it in Python</span></span>
<span data-ttu-id="301a5-278">Nous souhaitons toooperationalize hello modèle d’apprentissage après que qu’il a été généré.</span><span class="sxs-lookup"><span data-stu-id="301a5-278">We want toooperationalize hello machine learning model after it has been built.</span></span> <span data-ttu-id="301a5-279">Nous utilisons ici un modèle de logistique binaire hello comme exemple.</span><span class="sxs-lookup"><span data-stu-id="301a5-279">Here we use hello binary logistic model as an example.</span></span> <span data-ttu-id="301a5-280">Vérifiez que hello scikit-en savoir plus de la version de votre ordinateur local est 0.15.1.</span><span class="sxs-lookup"><span data-stu-id="301a5-280">Make sure hello scikit-learn version in your local machine is 0.15.1.</span></span> <span data-ttu-id="301a5-281">Vous n’avez tooworry à ce sujet si vous utilisez Azure ML studio service.</span><span class="sxs-lookup"><span data-stu-id="301a5-281">You don't have tooworry about this if you use Azure ML studio service.</span></span>

* <span data-ttu-id="301a5-282">Recherchez vos informations d’identification à partir des paramètres du service Azure ML studio.</span><span class="sxs-lookup"><span data-stu-id="301a5-282">Find your workspace credentials from Azure ML studio settings.</span></span> <span data-ttu-id="301a5-283">Dans Azure Machine Learning Studio, cliquez sur **Paramètres** --> **Nom** --> **Jetons d'autorisation**.</span><span class="sxs-lookup"><span data-stu-id="301a5-283">In Azure Machine Learning Studio, click **Settings** --> **Name** --> **Authorization Tokens**.</span></span> 
  
    ![c3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* <span data-ttu-id="301a5-285">Créer un service web</span><span class="sxs-lookup"><span data-stu-id="301a5-285">Create Web Service</span></span>
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* <span data-ttu-id="301a5-286">Obtenir des informations d’identification du service web</span><span class="sxs-lookup"><span data-stu-id="301a5-286">Get web service credentials</span></span>
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* <span data-ttu-id="301a5-287">Appeler une API de service web</span><span class="sxs-lookup"><span data-stu-id="301a5-287">Call Web service API.</span></span> <span data-ttu-id="301a5-288">Vous avez toowait 5 à 10 secondes après l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="301a5-288">You have toowait 5-10 seconds after hello previous step.</span></span>
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a><span data-ttu-id="301a5-289">Option 2 : Créer et déployer des modèles directement dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="301a5-289">Option 2: Create and deploy models directly in Azure Machine Learning</span></span>
<span data-ttu-id="301a5-290">Azure Machine Learning Studio peut lire les données directement à partir d’Azure Data Lake Store et être toocreate utilisé et déployé des modèles.</span><span class="sxs-lookup"><span data-stu-id="301a5-290">Azure Machine Learning Studio can read data directly from Azure Data Lake Store and then be used toocreate and deploy models.</span></span> <span data-ttu-id="301a5-291">Cette approche utilise une table Hive qui pointe à hello Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="301a5-291">This approach uses a Hive table that points at hello Azure Data Lake Store.</span></span> <span data-ttu-id="301a5-292">Cela nécessite que les configurer un cluster Azure HDInsight distinct, sur quel hello ruche table est créée.</span><span class="sxs-lookup"><span data-stu-id="301a5-292">This requires that a separate Azure HDInsight cluster be provisioned, on which hello Hive table is created.</span></span> <span data-ttu-id="301a5-293">Hello suivant sections indiquent comment toodo cela.</span><span class="sxs-lookup"><span data-stu-id="301a5-293">hello following sections show how toodo this.</span></span> 

### <a name="create-an-hdinsight-linux-cluster"></a><span data-ttu-id="301a5-294">Créer un cluster HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="301a5-294">Create an HDInsight Linux Cluster</span></span>
<span data-ttu-id="301a5-295">Créer un HDInsight Cluster (Linux) à partir de hello [Azure Portal](http://portal.azure.com). Pour plus d’informations, consultez hello **créer un cluster HDInsight avec accès tooAzure Data Lake Store** section [créer un cluster HDInsight à l’aide du portail Azure Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="301a5-295">Create an HDInsight Cluster (Linux) from hello [Azure Portal](http://portal.azure.com).For details, see hello **Create an HDInsight cluster with access tooAzure Data Lake Store** section in [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a><span data-ttu-id="301a5-297">Créer une table Hive dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="301a5-297">Create Hive table in HDInsight</span></span>
<span data-ttu-id="301a5-298">Maintenant, nous créons ruche toobe de tables utilisée dans Azure Machine Learning Studio dans le cluster HDInsight de hello à l’aide de données hello stockées dans Azure Data Lake Store à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="301a5-298">Now we create Hive tables toobe used in Azure Machine Learning Studio in hello HDInsight cluster using hello data stored in Azure Data Lake Store in hello previous step.</span></span> <span data-ttu-id="301a5-299">Accédez toohello cluster HDInsight venez de créer.</span><span class="sxs-lookup"><span data-stu-id="301a5-299">Go toohello HDInsight cluster just created.</span></span> <span data-ttu-id="301a5-300">Cliquez sur **paramètres** --> **propriétés** --> **Cluster identité AAD** --> **accès ADLS**, Vérifiez que votre compte Azure Data Lake Store est ajoutée dans la liste hello en lecture, écriture et des droits d’exécution.</span><span class="sxs-lookup"><span data-stu-id="301a5-300">Click **Settings** --> **Properties** --> **Cluster AAD Identity** --> **ADLS Access**, make sure your Azure Data Lake Store account is added in hello list with read, write and execute rights.</span></span> 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

<span data-ttu-id="301a5-302">Puis cliquez sur **tableau de bord** toohello suivant **paramètres** bouton et une fenêtre seront affiche.</span><span class="sxs-lookup"><span data-stu-id="301a5-302">Then click **Dashboard** next toohello **Settings** button and a window will pop up.</span></span> <span data-ttu-id="301a5-303">Cliquez sur **affichage de la ruche** Bonjour coin supérieur droit de la page de hello et vous verrez hello **l’éditeur de requête**.</span><span class="sxs-lookup"><span data-stu-id="301a5-303">Click **Hive View** in hello upper right corner of hello page and you will see hello **Query Editor**.</span></span>

 ![20](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

<span data-ttu-id="301a5-306">Collez une table hello suivant toocreate des scripts Hive.</span><span class="sxs-lookup"><span data-stu-id="301a5-306">Paste in hello following Hive scripts toocreate a table.</span></span> <span data-ttu-id="301a5-307">Hello de source de données se trouve dans la référence d’Azure Data Lake Store de cette façon : **adl://data_lake_store_name.azuredatalakestore.net:443/nom_dossier nom_fichier**.</span><span class="sxs-lookup"><span data-stu-id="301a5-307">hello location of data source is in Azure Data Lake Store reference in this way: **adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**.</span></span>

    CREATE EXTERNAL TABLE nyc_stratified_sample
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string,
      payment_type string,
      fare_amount string,
      surcharge string,
      mta_tax string,
      tolls_amount string,
      total_amount string,
      tip_amount string,
      tipped string,
      tip_class string,
      rownum string
      )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    LOCATION 'adl://data_lake_storage_name.azuredatalakestore.net:443/nyctaxi_folder/demo_ex_9_stratified_1_1000_copy.csv';


<span data-ttu-id="301a5-308">Lors de la requête de hello a terminé son exécution, des résultats hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="301a5-308">When hello query finishes running, you will see hello results like this:</span></span>

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a><span data-ttu-id="301a5-310">Créer et déployer des modèles dans Azure Machine Studio</span><span class="sxs-lookup"><span data-stu-id="301a5-310">Build and deploy models in Azure Machine Learning Studio</span></span>
<span data-ttu-id="301a5-311">Nous sont désormais prêt toobuild et que vous déployez un modèle qui prédit ou non une info-bulle est payée avec Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="301a5-311">We are now ready toobuild and deploy a model that predicts whether or not a tip is paid with Azure Machine Learning.</span></span> <span data-ttu-id="301a5-312">Bonjour stratifié d’exemples de données est prêt toobe utilisé dans cette classification binaire (Conseil ou non) problème.</span><span class="sxs-lookup"><span data-stu-id="301a5-312">hello stratified sample data is ready toobe used in this binary classification (tip or not) problem.</span></span> <span data-ttu-id="301a5-313">Hello modèles prédictifs à l’aide de la classification multiclasse (tip_class) et de régression (tip_amount) peut également être générée et déployée avec Azure Machine Learning Studio, mais nous seulement montrer ici comment la case utilisant toohandle hello hello modèle de classification binaire.</span><span class="sxs-lookup"><span data-stu-id="301a5-313">hello predictive models using multiclass classification (tip_class) and regression (tip_amount) can also be built and deployed with Azure Machine Learning Studio, but here we only show how toohandle hello case using hello binary classification model.</span></span>

1. <span data-ttu-id="301a5-314">Obtenir des données de hello dans Azure ML à l’aide de hello **importer des données** module, disponible dans hello **données d’entrée et sortie** section.</span><span class="sxs-lookup"><span data-stu-id="301a5-314">Get hello data into Azure ML using hello **Import Data** module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="301a5-315">Pour plus d’informations, consultez hello [module d’importer des données](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) page de référence.</span><span class="sxs-lookup"><span data-stu-id="301a5-315">For more information, see hello [Import Data module](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) reference page.</span></span>
2. <span data-ttu-id="301a5-316">Sélectionnez **requête de la ruche** comme hello **source de données** Bonjour **propriétés** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="301a5-316">Select **Hive Query** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="301a5-317">Hello coller script Hive Bonjour suivant **requête de base de données Hive** éditeur</span><span class="sxs-lookup"><span data-stu-id="301a5-317">Paste hello following Hive script in hello **Hive database query** editor</span></span>
   
        select * from nyc_stratified_sample;
4. <span data-ttu-id="301a5-318">Entrez le cluster d’URI de HDInsight hello (vous pouvez trouver dans le portail Azure), informations d’identification Hadoop, l’emplacement des données de sortie et nom de conteneur/clé/nom de compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="301a5-318">Enter hello URI of HDInsight cluster (this can be found in Azure Portal), Hadoop credentials, location of output data, and Azure storage account name/key/container name.</span></span>
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

<span data-ttu-id="301a5-320">Figure hello ci-dessous montre une expérience de classification binaire la lecture des données à partir de la table Hive.</span><span class="sxs-lookup"><span data-stu-id="301a5-320">An example of a binary classification experiment reading data from Hive table is shown in hello figure below.</span></span>

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

<span data-ttu-id="301a5-322">Après la création de l’expérience de hello, cliquez sur **configurer le Service Web** --> **prédictive Service Web**</span><span class="sxs-lookup"><span data-stu-id="301a5-322">After hello experiment is created, click  **Set Up Web Service** --> **Predictive Web Service**</span></span>

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

<span data-ttu-id="301a5-324">Exécution hello créé automatiquement score expérience, lorsqu’elle est terminée, cliquez sur **déployer le Service Web**</span><span class="sxs-lookup"><span data-stu-id="301a5-324">Run hello automatically created scoring experiment, when it finishes, click **Deploy Web Service**</span></span>

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

<span data-ttu-id="301a5-326">tableau de bord de service Hello web s’affiche peu de temps :</span><span class="sxs-lookup"><span data-stu-id="301a5-326">hello web service dashboard will be displayed shortly:</span></span>

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a><span data-ttu-id="301a5-328">Résumé</span><span class="sxs-lookup"><span data-stu-id="301a5-328">Summary</span></span>
<span data-ttu-id="301a5-329">En suivant cette procédure pas à pas, vous avez créé un environnement de science des données pour créer des solutions de bout en bout évolutives dans Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="301a5-329">By completing this walkthrough you have created a data science environment for building scalable end-to-end solutions in Azure Data Lake.</span></span> <span data-ttu-id="301a5-330">Cet environnement a été utilisé tooanalyze un dataset volumineux public, en mettant sur les étapes canonique de hello Hello processus de science des données, de l’acquisition des données via l’apprentissage du modèle, et puis de modèle de déploiement toohello Hello comme un service web.</span><span class="sxs-lookup"><span data-stu-id="301a5-330">This environment was used tooanalyze a large public dataset, taking it through hello canonical steps of hello Data Science Process, from data acquisition through model training, and then toohello deployment of hello model as a web service.</span></span> <span data-ttu-id="301a5-331">U-SQL a été utilisé tooprocess, Explorer et les exemples de données de hello.</span><span class="sxs-lookup"><span data-stu-id="301a5-331">U-SQL was used tooprocess, explore and sample hello data.</span></span> <span data-ttu-id="301a5-332">Python et Hive ont été utilisés avec Azure Machine Learning Studio toobuild et déploiement des modèles prédictifs.</span><span class="sxs-lookup"><span data-stu-id="301a5-332">Python and Hive were used with Azure Machine Learning Studio toobuild and deploy predictive models.</span></span>

## <a name="whats-next"></a><span data-ttu-id="301a5-333">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="301a5-333">What's next?</span></span>
<span data-ttu-id="301a5-334">Hello cursus pour le [processus de science des données équipe (TDSP)](http://aka.ms/datascienceprocess) fournit tootopics liens décrivant chaque étape dans hello avancé du processus de l’analytique.</span><span class="sxs-lookup"><span data-stu-id="301a5-334">hello learning path for the [Team Data Science Process (TDSP)](http://aka.ms/datascienceprocess) provides links tootopics describing each step in hello advanced analytics process.</span></span> <span data-ttu-id="301a5-335">Il existe une série de procédures pas à pas détaillé sur hello [procédures pas à pas du processus de science des données équipe](data-science-process-walkthroughs.md) page ce showcase comment toouse services dans différents scénarios d’analytique prédictive et des ressources :</span><span class="sxs-lookup"><span data-stu-id="301a5-335">There are a series of walkthroughs itemized on hello [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) page that showcase how toouse resources and services in various predictive analytics scenarios:</span></span>

* [<span data-ttu-id="301a5-336">Hello processus de science des données équipe en action : à l’aide de l’entrepôt de données SQL</span><span class="sxs-lookup"><span data-stu-id="301a5-336">hello Team Data Science Process in action: using SQL Data Warehouse</span></span>](machine-learning-data-science-process-sqldw-walkthrough.md)
* [<span data-ttu-id="301a5-337">Hello processus de science des données équipe en action : à l’aide de clusters HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="301a5-337">hello Team Data Science Process in action: using HDInsight Hadoop clusters</span></span>](machine-learning-data-science-process-hive-walkthrough.md)
* [<span data-ttu-id="301a5-338">Hello, processus de science des données équipe : à l’aide de SQL Server</span><span class="sxs-lookup"><span data-stu-id="301a5-338">hello Team Data Science Process: using SQL Server</span></span>](machine-learning-data-science-process-sql-walkthrough.md)
* [<span data-ttu-id="301a5-339">Vue d’ensemble de l’utilisation de processus de science des données hello nouvelles sur Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="301a5-339">Overview of hello Data Science Process using Spark on Azure HDInsight</span></span>](machine-learning-data-science-spark-overview.md)

