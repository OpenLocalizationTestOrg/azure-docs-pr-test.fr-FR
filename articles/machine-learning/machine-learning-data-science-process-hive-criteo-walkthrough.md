---
title: "Hello processus de science des données équipe en action - à l’aide d’un Cluster de Hadoop HDInsight Azure sur un jeu de données de 1 to | Documents Microsoft"
description: "À l’aide de hello équipe données science des processus pour un scénario de bout en bout utilisant un HDInsight Hadoop toobuild de cluster et déployer un modèle à l’aide d’un jeu de données disponible publiquement (1 To) volumineux"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 59b2af02e7840cb60a4b5b2f2c8ab0611df198ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a><span data-ttu-id="d7f8e-103">Hello processus de science des données équipe en action - à l’aide d’un Cluster de Hadoop HDInsight Azure sur un jeu de données de 1 to</span><span class="sxs-lookup"><span data-stu-id="d7f8e-103">hello Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset</span></span>

<span data-ttu-id="d7f8e-104">Dans cette procédure pas à pas, nous allons montrer à l’aide de hello du processus de science des données équipe dans un scénario de bout en bout avec un [cluster Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, Explorer, ingénieur de fonctionnalité et vers le bas des exemples de données à partir d’un des hello publiquement disponible [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) jeux de données.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-104">In this walkthrough, we demonstrate using hello Team Data Science Process in an end-to-end scenario with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore, feature engineer, and down sample data from one of hello publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) datasets.</span></span> <span data-ttu-id="d7f8e-105">Nous utilisons Azure Machine Learning toobuild un modèle de classification binaire sur ces données.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-105">We use Azure Machine Learning toobuild a binary classification model on this data.</span></span> <span data-ttu-id="d7f8e-106">Nous montrons également comment toopublish un de ces modèles comme un service Web.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-106">We also show how toopublish one of these models as a Web service.</span></span>

<span data-ttu-id="d7f8e-107">Il est également possible de toouse un tâches de hello notebooks bloc-notes tooaccomplish présentées dans cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-107">It is also possible toouse an IPython notebook tooaccomplish hello tasks presented in this walkthrough.</span></span> <span data-ttu-id="d7f8e-108">Les utilisateurs qui seraient comme tootry cette approche doit consulter hello [procédure pas à pas Criteo à l’aide d’une connexion ODBC de la ruche](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) rubrique.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-108">Users who would like tootry this approach should consult hello [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="d7f8e-109"><a name="dataset"></a>Description du groupe de données Criteo</span><span class="sxs-lookup"><span data-stu-id="d7f8e-109"><a name="dataset"></a>Criteo Dataset Description</span></span>
<span data-ttu-id="d7f8e-110">Hello Criteo de données sont un jeu de données de prédiction cliquez qui est d’environ 370 Go de gzip compressées des fichiers TSV (~1.3TB non compressé), qui comprend plus de 4.3 milliards d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-110">hello Criteo data is a click prediction dataset that is approximately 370GB of gzip compressed TSV files (~1.3TB uncompressed), comprising more than 4.3 billion records.</span></span> <span data-ttu-id="d7f8e-111">Elles proviennent de 24 jours de données de clic, disponibles via [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span><span class="sxs-lookup"><span data-stu-id="d7f8e-111">It is taken from 24 days of click data made available by [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span></span> <span data-ttu-id="d7f8e-112">Pour plus de commodité hello de chercheurs de données, nous avons décompressé tooexperiment toous de données disponibles avec.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-112">For hello convenience of data scientists, we have unzipped data available toous tooexperiment with.</span></span>

<span data-ttu-id="d7f8e-113">Chaque enregistrement de ce groupe de données est constitué de 40 colonnes :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-113">Each record in this dataset contains 40 columns:</span></span>

* <span data-ttu-id="d7f8e-114">Hello première colonne est une colonne d’étiquette qui indique si un utilisateur clique sur un **ajouter** (valeur 1) ou ne cliquez pas sur un (valeur 0)</span><span class="sxs-lookup"><span data-stu-id="d7f8e-114">hello first column is a label column that indicates whether a user clicks an **add** (value 1) or does not click one (value 0)</span></span>
* <span data-ttu-id="d7f8e-115">Les 13 colonnes suivantes sont numériques, et</span><span class="sxs-lookup"><span data-stu-id="d7f8e-115">next 13 columns are numeric, and</span></span>
* <span data-ttu-id="d7f8e-116">les 26 dernières sont des colonnes catégorielles</span><span class="sxs-lookup"><span data-stu-id="d7f8e-116">last 26 are categorical columns</span></span>

<span data-ttu-id="d7f8e-117">colonnes de Hello sont rendues anonymes et utiliser une série de noms énumérés : « Col1 » (pour la colonne d’étiquette hello) trop ' Col40 » (pour la dernière colonne catégorielle hello).</span><span class="sxs-lookup"><span data-stu-id="d7f8e-117">hello columns are anonymized and use a series of enumerated names: "Col1" (for hello label column) too'Col40" (for hello last categorical column).</span></span>            

<span data-ttu-id="d7f8e-118">Voici un extrait de hello tout d’abord 20 colonnes des deux observations (lignes) à partir de ce jeu de données :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-118">Here is an excerpt of hello first 20 columns of two observations (rows) from this dataset:</span></span>

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

<span data-ttu-id="d7f8e-119">Il existe des valeurs manquantes dans les deux colonnes numériques et par catégorie de hello dans ce jeu de données.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-119">There are missing values in both hello numeric and categorical columns in this dataset.</span></span> <span data-ttu-id="d7f8e-120">Nous décrivons une méthode simple pour la gestion des valeurs manquantes de hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-120">We describe a simple method for handling hello missing values.</span></span> <span data-ttu-id="d7f8e-121">Des détails supplémentaires de données de hello sont explorées lorsque nous les stocker dans les tables de la ruche.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-121">Additional details of hello data are explored when we store them into Hive tables.</span></span>

<span data-ttu-id="d7f8e-122">**Définition :** *taux de clic (CTR) :* il s’agit pourcentage hello clics dans les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-122">**Definition:** *Clickthrough rate (CTR):* This is hello percentage of clicks in hello data.</span></span> <span data-ttu-id="d7f8e-123">Dans ce jeu de données Criteo, hello CTR est environ 3.3 % ou 0.033.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-123">In this Criteo dataset, hello CTR is about 3.3% or 0.033.</span></span>

## <span data-ttu-id="d7f8e-124"><a name="mltasks"></a>Exemples de tâches de prédiction</span><span class="sxs-lookup"><span data-stu-id="d7f8e-124"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="d7f8e-125">Cette procédure pas à pas aborde deux exemples de problèmes de prédiction :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-125">Two sample prediction problems are addressed in this walkthrough:</span></span>

1. <span data-ttu-id="d7f8e-126">**Classification binaire**: prédit si un utilisateur a cliqué ou non sur un ajout :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-126">**Binary classification**: Predicts whether a user clicked an add:</span></span>
   
   * <span data-ttu-id="d7f8e-127">Classe 0 : aucun clic</span><span class="sxs-lookup"><span data-stu-id="d7f8e-127">Class 0: No Click</span></span>
   * <span data-ttu-id="d7f8e-128">Classe 1 : clic</span><span class="sxs-lookup"><span data-stu-id="d7f8e-128">Class 1: Click</span></span>
2. <span data-ttu-id="d7f8e-129">**Régression**: prédit la probabilité de hello d’une annonce, cliquez sur à partir des fonctionnalités de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-129">**Regression**: Predicts hello probability of an ad click from user features.</span></span>

## <span data-ttu-id="d7f8e-130"><a name="setup"></a>Configuration d’un cluster Hadoop HDInsight pour la science des données</span><span class="sxs-lookup"><span data-stu-id="d7f8e-130"><a name="setup"></a>Set Up an HDInsight Hadoop cluster for data science</span></span>
<span data-ttu-id="d7f8e-131">**Remarque** : il s’agit généralement d’une tâche d’**administration**.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-131">**Note:** This is typically an **Admin** task.</span></span>

<span data-ttu-id="d7f8e-132">Configurez votre environnement de science des données Azure pour créer des solutions d'analyse prédictives avec les clusters HDInsight en trois étapes :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-132">Set up your Azure Data Science environment for building predictive analytics solutions with HDInsight clusters in three steps:</span></span>

1. <span data-ttu-id="d7f8e-133">[Créer un compte de stockage](../storage/common/storage-create-storage-account.md): ce compte de stockage est données toostore utilisé dans le stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-133">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used toostore data in Azure Blob Storage.</span></span> <span data-ttu-id="d7f8e-134">données Hello utilisées dans les clusters HDInsight sont stockées ici.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-134">hello data used in HDInsight clusters is stored here.</span></span>
2. <span data-ttu-id="d7f8e-135">[Personnalisation des clusters Hadoop Azure HDInsight pour la science des données](machine-learning-data-science-customize-hadoop-cluster.md): cette étape crée un cluster Hadoop Azure HDInsight avec Anaconda Python 2.7 64 bits installé sur tous les nœuds.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-135">[Customize Azure HDInsight Hadoop Clusters for Data Science](machine-learning-data-science-customize-hadoop-cluster.md): This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="d7f8e-136">Il existe deux étapes importantes (décrites dans cette rubrique) toocomplete lors de la personnalisation du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-136">There are two important steps (described in this topic) toocomplete when customizing hello HDInsight cluster.</span></span>
   
   * <span data-ttu-id="d7f8e-137">Vous devez lier le compte de stockage hello créé à l’étape 1 avec votre cluster HDInsight lors de sa création.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-137">You must link hello storage account created in step 1 with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="d7f8e-138">Ce compte de stockage est utilisé pour accéder aux données qui peuvent être traitées au sein du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-138">This storage account is used for accessing data that can be processed within hello cluster.</span></span>
   * <span data-ttu-id="d7f8e-139">Vous devez activer l’accès à distance toohello nœud de tête hello cluster après sa création.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-139">You must enable Remote Access toohello head node of hello cluster after it is created.</span></span> <span data-ttu-id="d7f8e-140">N’oubliez pas d’informations d’identification de l’accès à distance hello vous spécifiez ici (différents de ceux spécifiés pour le cluster hello lors de sa création) : vous avez besoin toocomplete hello les procédures ci-après.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-140">Remember hello remote access credentials you specify here (different from those specified for hello cluster at its creation): you need them toocomplete hello following procedures.</span></span>
3. <span data-ttu-id="d7f8e-141">[Créer un espace de travail Azure ML](machine-learning-create-workspace.md): ce Azure Machine Learning un espace de travail est utilisé pour créer des modèles d’apprentissage automatique après une exploration de données initiales et vers le bas d’échantillonnage sur le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-141">[Create an Azure ML workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used for building machine learning models after an initial data exploration and down sampling on hello HDInsight cluster.</span></span>

## <span data-ttu-id="d7f8e-142"><a name="getdata"></a>Récupération et utilisation des données provenant d’une source publique</span><span class="sxs-lookup"><span data-stu-id="d7f8e-142"><a name="getdata"></a>Get and consume data from a public source</span></span>
<span data-ttu-id="d7f8e-143">Hello [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) jeu de données est accessible en cliquant sur le lien de hello, accepter les conditions d’utilisation de hello, en fournissant un nom.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-143">hello [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset can be accessed by clicking on hello link, accepting hello terms of use, and providing a name.</span></span> <span data-ttu-id="d7f8e-144">Voici une capture de l’écran correspondant :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-144">A snapshot of what this looks like is shown here:</span></span>

![Accepter les conditions de Criteo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

<span data-ttu-id="d7f8e-146">Cliquez sur **continuer tooDownload** tooread plus d’informations sur le jeu de données hello et sa disponibilité.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-146">Click **Continue tooDownload** tooread more about hello dataset and its availability.</span></span>

<span data-ttu-id="d7f8e-147">les données de salutation résident dans un public [stockage d’objets blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) emplacement : wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-147">hello data resides in a public [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) location: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span></span> <span data-ttu-id="d7f8e-148">Hello « wasb » désigne l’emplacement de stockage d’objets Blob tooAzure.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-148">hello "wasb" refers tooAzure Blob Storage location.</span></span> 

1. <span data-ttu-id="d7f8e-149">données Hello dans le stockage de l’objet blob public se comprennent de trois sous-dossiers de données décompressées.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-149">hello data in this public blob storage consists of three subfolders of unzipped data.</span></span>
   
   1. <span data-ttu-id="d7f8e-150">Hello sous-dossier *brut/count/* contient hello première 21 jours de données, à partir du jour\_tooday 00\_20</span><span class="sxs-lookup"><span data-stu-id="d7f8e-150">hello subfolder *raw/count/* contains hello first 21 days of data - from day\_00 tooday\_20</span></span>
   2. <span data-ttu-id="d7f8e-151">Hello sous-dossier *brut/train/* se compose d’un seul jour de données, jour\_21</span><span class="sxs-lookup"><span data-stu-id="d7f8e-151">hello subfolder *raw/train/* consists of a single day of data, day\_21</span></span>
   3. <span data-ttu-id="d7f8e-152">Hello sous-dossier *brut/test/* se compose de deux jours de données, jour\_22 et jour\_23</span><span class="sxs-lookup"><span data-stu-id="d7f8e-152">hello subfolder *raw/test/* consists of two days of data, day\_22 and day\_23</span></span>
2. <span data-ttu-id="d7f8e-153">Pour ceux qui souhaitent toostart avec des données brutes gzip hello, elles sont également disponibles dans le dossier principal de hello *brut /* comme day_NN.gz, où NN s’étende de too23 00.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-153">For those who want toostart with hello raw gzip data, these are also available in hello main folder *raw/* as day_NN.gz, where NN goes from 00 too23.</span></span>

<span data-ttu-id="d7f8e-154">Une autre approche tooaccess, Explorer et modèle de données qui ne nécessitent pas les téléchargements locales est expliquée plus loin dans cette procédure pas à pas, quand vous créez des tables de la ruche.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-154">An alternative approach tooaccess, explore, and model this data that does not require any local downloads is explained later in this walkthrough when we create Hive tables.</span></span>

## <span data-ttu-id="d7f8e-155"><a name="login"></a>Connectez-vous au nœud principal de cluster toohello</span><span class="sxs-lookup"><span data-stu-id="d7f8e-155"><a name="login"></a>Log in toohello cluster headnode</span></span>
<span data-ttu-id="d7f8e-156">toolog dans le nœud principal de toohello du cluster hello, utilisez hello [portail Azure](https://ms.portal.azure.com) cluster hello de toolocate.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-156">toolog in toohello headnode of hello cluster, use hello [Azure portal](https://ms.portal.azure.com) toolocate hello cluster.</span></span> <span data-ttu-id="d7f8e-157">Cliquez sur hello HDInsight éléphant icône sur hello gauche, puis sur nom hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-157">Click hello HDInsight elephant icon on hello left and then double-click hello name of your cluster.</span></span> <span data-ttu-id="d7f8e-158">Accédez toohello **Configuration** onglet, double-cliquez sur icône de connexion hello bas hello de page de hello et entrez vos informations d’identification de l’accès à distance lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-158">Navigate toohello **Configuration** tab, double-click hello CONNECT icon on hello bottom of hello page, and enter your remote access credentials when prompted.</span></span> <span data-ttu-id="d7f8e-159">Cela vous prend un nœud principal de toohello du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-159">This takes you toohello headnode of hello cluster.</span></span>

<span data-ttu-id="d7f8e-160">Un premier journal dans le nœud principal du cluster toohello classique ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-160">Here is what a typical first log in toohello cluster headnode looks like:</span></span>

![Connectez-vous à toocluster](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

<span data-ttu-id="d7f8e-162">Sur la gauche de hello, nous constatons hello « Hadoop ligne de commande », qui est notre exploration de données hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-162">On hello left, we see hello "Hadoop Command Line", which is our workhorse for hello data exploration.</span></span> <span data-ttu-id="d7f8e-163">De même que deux URL : « État Yarn Hadoop » et « Nœud de nom Hadoop ».</span><span class="sxs-lookup"><span data-stu-id="d7f8e-163">We also see two useful URLs - "Hadoop Yarn Status" and "Hadoop Name Node".</span></span> <span data-ttu-id="d7f8e-164">URL d’état Hello fils montre la progression du travail et URL de nom de nœud hello donne des détails sur la configuration de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-164">hello yarn status URL shows job progress and hello name node URL gives details on hello cluster configuration.</span></span>

<span data-ttu-id="d7f8e-165">Maintenant nous sont configurés et prêts toobegin première partie de la procédure pas à pas hello : exploration de données à l’aide de la ruche et la préparation des données pour l’apprentissage d’Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-165">Now we are set up and ready toobegin first part of hello walkthrough: data exploration using Hive and getting data ready for Azure Machine Learning.</span></span>

## <span data-ttu-id="d7f8e-166"><a name="hive-db-tables"></a> Création de la base de données et des tables Hive</span><span class="sxs-lookup"><span data-stu-id="d7f8e-166"><a name="hive-db-tables"></a> Create Hive database and tables</span></span>
<span data-ttu-id="d7f8e-167">toocreate ruche tables pour notre jeu de données Criteo, ouvrez hello ***ligne de commande Hadoop*** hello bureau du nœud principal de hello et entrez le répertoire de ruche hello en entrant la commande hello</span><span class="sxs-lookup"><span data-stu-id="d7f8e-167">toocreate Hive tables for our Criteo dataset, open hello ***Hadoop Command Line*** on hello desktop of hello head node, and enter hello Hive directory by entering hello command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="d7f8e-168">Exécuter toutes les commandes de la ruche dans cette procédure pas à pas d’emplacement de ruche hello / invite du répertoire.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-168">Run all Hive commands in this walkthrough from hello Hive bin/ directory prompt.</span></span> <span data-ttu-id="d7f8e-169">Tout problème lié au chemin d’accès sera résolu automatiquement.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-169">This takes care of any path issues automatically.</span></span> <span data-ttu-id="d7f8e-170">Nous utilisons hello termes « Invite du répertoire ruche », « ruche bin / invite du répertoire » et « ligne de commande Hadoop » indifféremment.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-170">We use hello terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop Command Line" interchangeably.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="d7f8e-171">tooexecute une requête Hive, toujours utiliser hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-171">tooexecute any Hive query, one can always use hello following commands:</span></span>
> 
> 

        cd %hive_home%\bin
        hive

<span data-ttu-id="d7f8e-172">Après hello ruche REPL s’affiche avec un « ruche > « Connectez-vous simplement couper et coller hello requête tooexecute il.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-172">After hello Hive REPL appears with a "hive >"sign, simply cut and paste hello query tooexecute it.</span></span>

<span data-ttu-id="d7f8e-173">Hello de code suivant crée une base de données « criteo » et génère ensuite les 4 tables :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-173">hello following code creates a database "criteo" and then generates 4 tables:</span></span>

* <span data-ttu-id="d7f8e-174">un *table pour la génération de nombres* reposant sur un jour de jours\_tooday 00\_20,</span><span class="sxs-lookup"><span data-stu-id="d7f8e-174">a *table for generating counts* built on days day\_00 tooday\_20,</span></span>
* <span data-ttu-id="d7f8e-175">un *de table pour une utilisation comme hello train dataset* reposant sur jour\_21, et</span><span class="sxs-lookup"><span data-stu-id="d7f8e-175">a *table for use as hello train dataset* built on day\_21, and</span></span>
* <span data-ttu-id="d7f8e-176">deux *jeux de données de test de tables pour une utilisation en tant que hello* reposant sur jour\_22 et jour\_23 respectivement.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-176">two *tables for use as hello test datasets* built on day\_22 and day\_23 respectively.</span></span>

<span data-ttu-id="d7f8e-177">Fractionnées notre jeu de données de test dans deux tables différentes, car un des jours de hello est un jour férié, et nous souhaitons toodetermine si le modèle de hello peut détecter les différences entre un jour férié et non à partir du taux de clics hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-177">We split our test dataset into two different tables because one of hello days is a holiday, and we want toodetermine if hello model can detect differences between a holiday and non-holiday from hello clickthrough rate.</span></span>

<span data-ttu-id="d7f8e-178">Hello script [exemple &#95; ruche & &#95; ; créer &#95; criteo &#95; base de données &#95; et &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) s’affiche ici pour des raisons pratiques :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-178">hello script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) is displayed here for convenience:</span></span>

    CREATE DATABASE IF NOT EXISTS criteo;
    DROP TABLE IF EXISTS criteo.criteo_count;
    CREATE TABLE criteo.criteo_count (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/count';

    DROP TABLE IF EXISTS criteo.criteo_train;
    CREATE TABLE criteo.criteo_train (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/train';

    DROP TABLE IF EXISTS criteo.criteo_test_day_22;
    CREATE TABLE criteo.criteo_test_day_22 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_22';

    DROP TABLE IF EXISTS criteo.criteo_test_day_23;
    CREATE TABLE criteo.criteo_test_day_23 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_23';

<span data-ttu-id="d7f8e-179">Nous Notez que toutes ces tables sont externes que nous avons simplement les emplacements de stockage d’objets Blob (wasb) tooAzure de point.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-179">We note that all these tables are external as we simply point tooAzure Blob Storage (wasb) locations.</span></span>

<span data-ttu-id="d7f8e-180">**Il existe deux façons tooexecute Hive n’importe quelle requête que nous avons maintenant.**</span><span class="sxs-lookup"><span data-stu-id="d7f8e-180">**There are two ways tooexecute ANY Hive query that we now mention.**</span></span>

1. <span data-ttu-id="d7f8e-181">**À l’aide de hello REPL ruche de ligne de commande**: hello tout d’abord est tooissue une « ruche » une commande et les copier et coller une requête à hello REPL ruche de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-181">**Using hello Hive REPL command-line**: hello first is tooissue a "hive" command and copy and paste a query at hello Hive REPL command-line.</span></span> <span data-ttu-id="d7f8e-182">toodo ce, procédez comme :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-182">toodo this, do:</span></span>
   
        cd %hive_home%\bin
        hive
   
     <span data-ttu-id="d7f8e-183">Maintenant à hello REPL de ligne de commande, telles que couper et coller les requêtes hello l’exécute.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-183">Now at hello REPL command-line, cutting and pasting hello query executes it.</span></span>
2. <span data-ttu-id="d7f8e-184">**L’enregistrement des requêtes tooa fichier et l’exécution de commande hello**: hello est ensuite le fichier .hql tooa toosave hello requêtes ([exemple &#95; ruche & &#95; ; créer &#95; criteo &#95; base de données &#95; et &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) et puis suivant de hello problème des commandes query de hello tooexecute :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-184">**Saving queries tooa file and executing hello command**: hello second is toosave hello queries tooa .hql file ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) and then issue hello following command tooexecute hello query:</span></span>
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a><span data-ttu-id="d7f8e-185">Confirmation de la création de la base de données et des tables</span><span class="sxs-lookup"><span data-stu-id="d7f8e-185">Confirm database and table creation</span></span>
<span data-ttu-id="d7f8e-186">Ensuite, nous confirmer la création de hello de base de données hello avec la commande suivante à partir de l’emplacement de ruche hello de hello / invite du répertoire :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-186">Next, we confirm hello creation of hello database with hello following command from hello Hive bin/ directory prompt:</span></span>

        hive -e "show databases;"

<span data-ttu-id="d7f8e-187">Cela donne :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-187">This gives:</span></span>

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

<span data-ttu-id="d7f8e-188">Cela permet de confirmer la création de hello de hello nouvelle base de données « criteo ».</span><span class="sxs-lookup"><span data-stu-id="d7f8e-188">This confirms hello creation of hello new database, "criteo".</span></span>

<span data-ttu-id="d7f8e-189">toosee les tables créées, nous tapez hello commande ici à partir de l’emplacement de ruche hello / invite du répertoire :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-189">toosee what tables we created, we simply issue hello command here from hello Hive bin/ directory prompt:</span></span>

        hive -e "show tables in criteo;"

<span data-ttu-id="d7f8e-190">Ensuite, nous voyons hello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-190">We then see hello following output:</span></span>

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <span data-ttu-id="d7f8e-191"><a name="exploration"></a> Exploration des données dans Hive</span><span class="sxs-lookup"><span data-stu-id="d7f8e-191"><a name="exploration"></a> Data exploration in Hive</span></span>
<span data-ttu-id="d7f8e-192">Est maintenant prêt à toodo une exploration de données de base de données dans la ruche.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-192">Now we are ready toodo some basic data exploration in Hive.</span></span> <span data-ttu-id="d7f8e-193">Nous commencer en comptant le nombre de hello d’exemples de formation de hello et tables de données de test.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-193">We begin by counting hello number of examples in hello train and test data tables.</span></span>

### <a name="number-of-train-examples"></a><span data-ttu-id="d7f8e-194">Nombre d'exemples de formation</span><span class="sxs-lookup"><span data-stu-id="d7f8e-194">Number of train examples</span></span>
<span data-ttu-id="d7f8e-195">Hello le contenu de [exemple &#95; ruche &#95; nombre &#95; train &#95; table &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) sont indiquées ici :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-195">hello contents of [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) are shown here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_train;

<span data-ttu-id="d7f8e-196">Cela donne :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-196">This yields:</span></span>

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

<span data-ttu-id="d7f8e-197">Vous pouvez également une peut également émettre hello de commande suivante à partir de l’emplacement de ruche hello / invite du répertoire :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-197">Alternatively, one may also issue hello following command from hello Hive bin/ directory prompt:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-hello-two-test-datasets"></a><span data-ttu-id="d7f8e-198">Nombre d’exemples de test dans les jeux de données de test hello deux</span><span class="sxs-lookup"><span data-stu-id="d7f8e-198">Number of test examples in hello two test datasets</span></span>
<span data-ttu-id="d7f8e-199">Nous avons maintenant nombre hello d’exemples de jeux de données de test deux hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-199">We now count hello number of examples in hello two test datasets.</span></span> <span data-ttu-id="d7f8e-200">Hello le contenu de [exemple &#95; ruche &#95; nombre &#95; criteo &#95; test &#95; jour &#95; 22 &#95; table &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) sont ici :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-200">hello contents of [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) are here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

<span data-ttu-id="d7f8e-201">Cela donne :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-201">This yields:</span></span>

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

<span data-ttu-id="d7f8e-202">Comme d’habitude, nous pouvons également appeler le script de hello à partir de l’emplacement de ruche hello / directory invite en émettant la commande hello :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-202">As usual, we may also call hello script from hello Hive bin/ directory prompt by issuing hello command:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

<span data-ttu-id="d7f8e-203">Enfin, nous examinons nombre hello des exemples de test dans le jeu de données de test hello selon le jour\_23.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-203">Finally, we examine hello number of test examples in hello test dataset based on day\_23.</span></span>

<span data-ttu-id="d7f8e-204">Hello commande toodo cela est similaire toohello une juste affichée (consultez trop[exemple &#95; ruche &#95; nombre &#95; criteo &#95; test &#95; jour &#95; 23 &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)) :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-204">hello command toodo this is similar toohello one just shown (refer too[sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

<span data-ttu-id="d7f8e-205">Cela donne :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-205">This gives:</span></span>

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-hello-train-dataset"></a><span data-ttu-id="d7f8e-206">Distribution d’étiquette dans le jeu de données de formation hello</span><span class="sxs-lookup"><span data-stu-id="d7f8e-206">Label distribution in hello train dataset</span></span>
<span data-ttu-id="d7f8e-207">distribution d’étiquette Hello hello train DataSet présente un intérêt.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-207">hello label distribution in hello train dataset is of interest.</span></span> <span data-ttu-id="d7f8e-208">toosee, afficher le contenu de [exemple &#95; ruche &#95; criteo &#95; étiquette &#95; distribution &#95; train &#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span><span class="sxs-lookup"><span data-stu-id="d7f8e-208">toosee this, we show contents of [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span></span>

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

<span data-ttu-id="d7f8e-209">Cela donne la distribution d’étiquette hello :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-209">This yields hello label distribution:</span></span>

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

<span data-ttu-id="d7f8e-210">Notez que le pourcentage de hello d’étiquettes positifs est 3.3 % environ (cohérent avec le jeu de données d’origine hello).</span><span class="sxs-lookup"><span data-stu-id="d7f8e-210">Note that hello percentage of positive labels is about 3.3% (consistent with hello original dataset).</span></span>

### <a name="histogram-distributions-of-some-numeric-variables-in-hello-train-dataset"></a><span data-ttu-id="d7f8e-211">Distributions histogramme de certaines variables numériques Bonjour former le jeu de données</span><span class="sxs-lookup"><span data-stu-id="d7f8e-211">Histogram distributions of some numeric variables in hello train dataset</span></span>
<span data-ttu-id="d7f8e-212">Nous pouvons utiliser natif de la ruche du « histogramme\_numérique « toofind out quelles distribution hello des variables numériques de hello ressemble de fonction.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-212">We can use Hive's native "histogram\_numeric" function toofind out what hello distribution of hello numeric variables looks like.</span></span> <span data-ttu-id="d7f8e-213">Voici le contenu de hello de [exemple &#95; ruche &#95; criteo &#95; histogramme &#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span><span class="sxs-lookup"><span data-stu-id="d7f8e-213">Here are hello contents of [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span></span>

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

<span data-ttu-id="d7f8e-214">Cela donne le résultat suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-214">This yields hello following:</span></span>

        26      155878415
        2606    92753
        6755    22086
        11202   6922
        14432   4163
        17815   2488
        21072   1901
        24113   1283
        27429   1225
        30818   906
        34512   723
        38026   387
        41007   290
        43417   312
        45797   571
        49819   428
        53505   328
        56853   527
        61004   160
        65510   3446
        Time taken: 317.851 seconds, Fetched: 20 row(s)

<span data-ttu-id="d7f8e-215">Hello latéral affichage - éclater combinaison dans la ruche sert tooproduce une sortie de type SQL au lieu de la liste de habituel hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-215">hello LATERAL VIEW - explode combination in Hive serves tooproduce a SQL-like output instead of hello usual list.</span></span> <span data-ttu-id="d7f8e-216">Notez que dans hello cette table, la première colonne de hello correspond toohello bin centre et hello deuxième toohello bin fréquence.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-216">Note that in hello this table, hello first column corresponds toohello bin center and hello second toohello bin frequency.</span></span>

### <a name="approximate-percentiles-of-some-numeric-variables-in-hello-train-dataset"></a><span data-ttu-id="d7f8e-217">Centiles approximatives de certaines variables numériques Bonjour former le jeu de données</span><span class="sxs-lookup"><span data-stu-id="d7f8e-217">Approximate percentiles of some numeric variables in hello train dataset</span></span>
<span data-ttu-id="d7f8e-218">Est également un calcul hello des centiles approximatifs d’intérêt avec des variables numériques.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-218">Also of interest with numeric variables is hello computation of approximate percentiles.</span></span> <span data-ttu-id="d7f8e-219">Le « percentile\_approx» natif de Hive le fait pour nous.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-219">Hive's native "percentile\_approx" does this for us.</span></span> <span data-ttu-id="d7f8e-220">Hello le contenu de [exemple &#95; ruche &#95; criteo &#95; approximative &#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) sont :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-220">hello contents of [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) are:</span></span>

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

<span data-ttu-id="d7f8e-221">Cela donne :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-221">This yields:</span></span>

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

<span data-ttu-id="d7f8e-222">Il remarque que distribution hello de centiles est généralement la distribution d’histogramme toohello étroitement liées d’une variable numérique.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-222">We remark that hello distribution of percentiles is closely related toohello histogram distribution of any numeric variable usually.</span></span>         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-hello-train-dataset"></a><span data-ttu-id="d7f8e-223">Rechercher le nombre de valeurs uniques pour certaines colonnes catégorielles dans le jeu de données de formation hello</span><span class="sxs-lookup"><span data-stu-id="d7f8e-223">Find number of unique values for some categorical columns in hello train dataset</span></span>
<span data-ttu-id="d7f8e-224">Poursuite de l’exploration de données hello, nous trouver maintenant, pour certaines colonnes catégorielles, nombre hello de valeurs uniques qu’ils prennent.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-224">Continuing hello data exploration, we now find, for some categorical columns, hello number of unique values they take.</span></span> <span data-ttu-id="d7f8e-225">toodo, afficher le contenu de [exemple &#95; ruche &#95; criteo &#95; unique &#95; valeurs &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span><span class="sxs-lookup"><span data-stu-id="d7f8e-225">toodo this, we show contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span></span>

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

<span data-ttu-id="d7f8e-226">Cela donne :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-226">This yields:</span></span>

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

<span data-ttu-id="d7f8e-227">Nous constatons que Col15 possède des valeurs uniques 19M !</span><span class="sxs-lookup"><span data-stu-id="d7f8e-227">We note that Col15 has 19M unique values!</span></span> <span data-ttu-id="d7f8e-228">Ces variables catégorielles de grande dimension à l’aide de techniques naïve comme « à chaud un codage » de tooencode est impossible.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-228">Using naive techniques like "one-hot encoding" tooencode such high-dimensional categorical variables is infeasible.</span></span> <span data-ttu-id="d7f8e-229">Nous mentionnons notamment une technique puissante et robuste appelée [Apprentissage à l’aide de compteurs](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) pour résoudre ce problème de manière efficace.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-229">In particular, we explain and demonstrate a powerful, robust technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) for tackling this problem efficiently.</span></span>

<span data-ttu-id="d7f8e-230">Nous terminer cette sous-section en examinant le nombre de hello de valeurs uniques pour d’autres colonnes catégorielles également.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-230">We end this sub-section by looking at hello number of unique values for some other categorical columns as well.</span></span> <span data-ttu-id="d7f8e-231">Hello le contenu de [exemple &#95; ruche &#95; criteo &#95; unique &#95; valeurs &#95; plusieurs &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) sont :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-231">hello contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) are:</span></span>

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

<span data-ttu-id="d7f8e-232">Cela donne :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-232">This yields:</span></span>

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

<span data-ttu-id="d7f8e-233">Là encore, nous voyons que, à l’exception de Col20, tous les hello autres colonnes ont de nombreuses valeurs uniques.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-233">Again we see that except for Col20, all hello other columns have many unique values.</span></span>

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-hello-train-dataset"></a><span data-ttu-id="d7f8e-234">Nombres d’occurrence des paires de variables catégorielles dans hello former le jeu de données</span><span class="sxs-lookup"><span data-stu-id="d7f8e-234">Co-occurrence counts of pairs of categorical variables in hello train dataset</span></span>

<span data-ttu-id="d7f8e-235">nombre de coordonnées occurrence Hello de paires de variables catégorielles est également intéressant.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-235">hello co-occurrence counts of pairs of categorical variables is also of interest.</span></span> <span data-ttu-id="d7f8e-236">Cela peut être déterminé à l’aide de code hello dans [exemple &#95; ruche &#95; criteo &#95; appariés &#95; catégorielles &#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span><span class="sxs-lookup"><span data-stu-id="d7f8e-236">This can be determined using hello code in [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span></span>

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

<span data-ttu-id="d7f8e-237">Nous inverser l’ordre hello nombres par leur occurrence et haut hello 15 dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-237">We reverse order hello counts by their occurrence and look at hello top 15 in this case.</span></span> <span data-ttu-id="d7f8e-238">Cela nous donne :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-238">This gives us:</span></span>

        ad98e872        cea68cd3        8964458
        ad98e872        3dbb483e        8444762
        ad98e872        43ced263        3082503
        ad98e872        420acc05        2694489
        ad98e872        ac4c5591        2559535
        ad98e872        fb1e95da        2227216
        ad98e872        8af1edc8        1794955
        ad98e872        e56937ee        1643550
        ad98e872        d1fade1c        1348719
        ad98e872        977b4431        1115528
        e5f3fd8d        a15d1051        959252
        ad98e872        dd86c04a        872975
        349b3fec        a52ef97d        821062
        e5f3fd8d        a0aaffa6        792250
        265366bf        6f5c7c41        782142
        Time taken: 560.22 seconds, Fetched: 15 row(s)

## <span data-ttu-id="d7f8e-239"><a name="downsample"></a>Jeux de données exemple hello pour Azure Machine Learning vers le bas</span><span class="sxs-lookup"><span data-stu-id="d7f8e-239"><a name="downsample"></a> Down sample hello datasets for Azure Machine Learning</span></span>
<span data-ttu-id="d7f8e-240">Ayant des jeux de données explorées hello et illustré comment nous pouvons faire de ce type d’exploration des variables (y compris les combinaisons), nous avons maintenant vers le bas de jeux de données exemple hello afin que nous pouvons créer des modèles dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-240">Having explored hello datasets and demonstrated how we may do this type of exploration for any variables (including combinations), we now down sample hello data sets so that we can build models in Azure Machine Learning.</span></span> <span data-ttu-id="d7f8e-241">Rappelez-vous ce problème hello nous concentrer sur est : étant donné un ensemble d’attributs de l’exemple (valeurs de fonctionnalités à partir de Col2 - Col40), nous pour prédire si Col1 est égal à 0 (aucun clic) ou 1 (clic).</span><span class="sxs-lookup"><span data-stu-id="d7f8e-241">Recall that hello problem we focus on is: given a set of example attributes (feature values from Col2 - Col40), we predict if Col1 is a 0 (no click) or a 1 (click).</span></span>

<span data-ttu-id="d7f8e-242">toodown exemples de notre apprentissage et de test % too1 de jeux de données de taille d’origine de hello, nous utilisons la fonction RAND() native de la ruche.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-242">toodown sample our train and test datasets too1% of hello original size, we use Hive's native RAND() function.</span></span> <span data-ttu-id="d7f8e-243">Hello au script suivant, [exemple &#95; ruche &#95; criteo &#95; sous-échantillonner &#95; train &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) effectue cette opération pour le jeu de données de formation hello :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-243">hello next script, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) does this for hello train dataset:</span></span>

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

<span data-ttu-id="d7f8e-244">Cela donne :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-244">This yields:</span></span>

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

<span data-ttu-id="d7f8e-245">Hello script [exemple &#95; ruche &#95; criteo &#95; sous-échantillonner &#95; test &#95; jour &#95; 22 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) le fait pour les données de test, jour\_22 :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-245">hello script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) does it for test data, day\_22:</span></span>

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

<span data-ttu-id="d7f8e-246">Cela donne :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-246">This yields:</span></span>

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


<span data-ttu-id="d7f8e-247">Enfin, hello script [exemple &#95; ruche &#95; criteo &#95; sous-échantillonner &#95; test &#95; jour &#95; 23 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) le fait pour les données de test, jour\_23 :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-247">Finally, hello script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) does it for test data, day\_23:</span></span>

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

<span data-ttu-id="d7f8e-248">Cela donne :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-248">This yields:</span></span>

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

<span data-ttu-id="d7f8e-249">Cette opération, nous sommes prêt toouse notre bas échantillonné former et tester des jeux de données pour générer des modèles dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-249">With this, we are ready toouse our down sampled train and test datasets for building models in Azure Machine Learning.</span></span>

<span data-ttu-id="d7f8e-250">Est un composant important final avant nous consacrerons tooAzure Machine Learning, qui est une table de nombres préoccupations hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-250">There is a final important component before we move on tooAzure Machine Learning, which is concerns hello count table.</span></span> <span data-ttu-id="d7f8e-251">Dans hello suivante sous-section, nous reviendrons en détail.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-251">In hello next sub-section, we discuss this in some detail.</span></span>

## <span data-ttu-id="d7f8e-252"><a name="count"></a>Une brève description de la table de nombres hello</span><span class="sxs-lookup"><span data-stu-id="d7f8e-252"><a name="count"></a> A brief discussion on hello count table</span></span>
<span data-ttu-id="d7f8e-253">Comme nous avons pu le remarquer, plusieurs variables catégorielles ont une dimensionnalité très élevée.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-253">As we saw, several categorical variables have a very high dimensionality.</span></span> <span data-ttu-id="d7f8e-254">Dans notre procédure pas à pas, nous vous présentons une technique puissante appelée [Learning avec compte](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode ces variables de manière efficace et fiable.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-254">In our walkthrough, we present a powerful technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode these variables in an efficient, robust manner.</span></span> <span data-ttu-id="d7f8e-255">Plus d’informations sur cette technique est dans le lien hello fourni.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-255">More information on this technique is in hello link provided.</span></span>

[!NOTE]
><span data-ttu-id="d7f8e-256">Dans cette procédure pas à pas, nous concentrer sur l’utilisation de count tables tooproduce compact représentations sous forme de grande dimension fonctionnalités catégorielles.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-256">In this walkthrough, we focus on using count tables tooproduce compact representations of high-dimensional categorical features.</span></span> <span data-ttu-id="d7f8e-257">Ce n’est pas hello seule façon tooencode fonctionnalités catégorielles ; Pour plus d’informations sur d’autres techniques, les utilisateurs concernés peuvent extraire [un-à chaud-encoding](http://en.wikipedia.org/wiki/One-hot) et [fonctionnalité hachage](http://en.wikipedia.org/wiki/Feature_hashing).</span><span class="sxs-lookup"><span data-stu-id="d7f8e-257">This is not hello only way tooencode categorical features; for more information on other techniques, interested users can check out [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) and [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).</span></span>
>

<span data-ttu-id="d7f8e-258">tables de nombres toobuild sur les données de nombres hello, nous utilisons des données de la hello dans hello brut/nombre de dossiers.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-258">toobuild count tables on hello count data, we use hello data in hello folder raw/count.</span></span> <span data-ttu-id="d7f8e-259">Bonjour modélisation section, nous montrer aux utilisateurs comment toobuild ces comptent les tables pour les fonctionnalités par catégorie de toutes pièces, ou vous pouvez également toouse une table de nombres prédéfinis pour leurs explorations.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-259">In hello modeling section, we show users how toobuild these count tables for categorical features from scratch, or alternatively toouse a pre-built count table for their explorations.</span></span> <span data-ttu-id="d7f8e-260">Dans ce qui suit, lorsque nous nous référons trop « prégénérées tables de nombres », nous entendons à l’aide de tables de nombres hello que nous fournissons.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-260">In what follows, when we refer too"pre-built count tables", we mean using hello count tables that we provide.</span></span> <span data-ttu-id="d7f8e-261">Obtenir des instructions détaillées sur la manière dont tooaccess ces tables sont fournis dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-261">Detailed instructions on how tooaccess these tables are provided in hello next section.</span></span>

## <span data-ttu-id="d7f8e-262"><a name="aml"></a> Création de modèles dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d7f8e-262"><a name="aml"></a> Build a model with Azure Machine Learning</span></span>
<span data-ttu-id="d7f8e-263">Notre processus de création de modèles dans Azure Machine Learning se déroule comme suit :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-263">Our model building process in Azure Machine Learning follows these steps:</span></span>

1. [<span data-ttu-id="d7f8e-264">Obtenir des données de hello à partir des tables de la ruche dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d7f8e-264">Get hello data from Hive tables into Azure Machine Learning</span></span>](#step1)
2. [<span data-ttu-id="d7f8e-265">Créer l’expérience de hello : nettoyer les données de salutation et générer des fonctionnalités avec les tables de nombres</span><span class="sxs-lookup"><span data-stu-id="d7f8e-265">Create hello experiment: clean hello data and featurize with count tables</span></span>](#step2)
3. [<span data-ttu-id="d7f8e-266">Build, de formation et de modèle de score hello</span><span class="sxs-lookup"><span data-stu-id="d7f8e-266">Build, train, and score hello model</span></span>](#step3)
4. [<span data-ttu-id="d7f8e-267">Évaluation du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="d7f8e-267">Evaluate hello model</span></span>](#step4)
5. [<span data-ttu-id="d7f8e-268">Publier un modèle de hello sous la forme d’un service web</span><span class="sxs-lookup"><span data-stu-id="d7f8e-268">Publish hello model as a web-service</span></span>](#step5)

<span data-ttu-id="d7f8e-269">Vous êtes désormais prêt toobuild des modèles dans Azure Machine Learning studio.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-269">Now we are ready toobuild models in Azure Machine Learning studio.</span></span> <span data-ttu-id="d7f8e-270">Nos données échantillonnées bas sont enregistrées en tant que tables Hive dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-270">Our down sampled data is saved as Hive tables in hello cluster.</span></span> <span data-ttu-id="d7f8e-271">Nous utilisons hello Azure Machine Learning **importer des données** module tooread ces données.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-271">We use hello Azure Machine Learning **Import Data** module tooread this data.</span></span> <span data-ttu-id="d7f8e-272">Hello informations d’identification tooaccess hello compte de stockage de ce cluster sont fournies ci-après.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-272">hello credentials tooaccess hello storage account of this cluster are provided in what follows.</span></span>

### <span data-ttu-id="d7f8e-273"><a name="step1"></a>Étape 1 : Obtenir des données à partir des tables de la ruche dans Azure Machine Learning à l’aide du module d’importation de données hello et sélectionnez-le pour une expérience d’apprentissage</span><span class="sxs-lookup"><span data-stu-id="d7f8e-273"><a name="step1"></a> Step 1: Get data from Hive tables into Azure Machine Learning using hello Import Data module and select it for a machine learning experiment</span></span>
<span data-ttu-id="d7f8e-274">Commencez par sélectionner **+NOUVEAU** -> **EXPÉRIENCE** -> **Expérience vide**.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-274">Start by selecting a **+NEW** -> **EXPERIMENT** -> **Blank Experiment**.</span></span> <span data-ttu-id="d7f8e-275">Ensuite, à partir de hello **recherche** zone hello coin supérieur gauche, recherchez « Importer des données ».</span><span class="sxs-lookup"><span data-stu-id="d7f8e-275">Then, from hello **Search** box on hello top left, search for "Import Data".</span></span> <span data-ttu-id="d7f8e-276">Glisser- déposer hello **importer des données** module sur le module de hello toouse toohello expérience canevas (partie centrale de l’écran hello hello) pour accéder aux données.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-276">Drag and drop hello **Import Data** module on toohello experiment canvas (hello middle portion of hello screen) toouse hello module for data access.</span></span>

<span data-ttu-id="d7f8e-277">Il s’agit de quel hello **importer des données** il semble que lors de l’obtention des données à partir de la table de hello Hive :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-277">This is what hello **Import Data** looks like while getting data from hello Hive table:</span></span>

![Import Data obtient des données](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

<span data-ttu-id="d7f8e-279">Pourquoi **importer des données** module, les valeurs hello de paramètres hello qui sont fournis dans hello graphique sont des exemples simplement de hello tri des valeurs que vous avez besoin de tooprovide.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-279">For hello **Import Data** module, hello values of hello parameters that are provided in hello graphic are just examples of hello sort of values you need tooprovide.</span></span> <span data-ttu-id="d7f8e-280">Voici quelques conseils généraux sur comment toofill le paramètre hello out définie pour hello **importer des données** module.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-280">Here is some general guidance on how toofill out hello parameter set for hello **Import Data** module.</span></span>

1. <span data-ttu-id="d7f8e-281">Choisissez « Requête Hive » pour la **source de données**</span><span class="sxs-lookup"><span data-stu-id="d7f8e-281">Choose "Hive query" for **Data Source**</span></span>
2. <span data-ttu-id="d7f8e-282">Bonjour **requête de base de données Hive** zone, une simple instruction SELECT * FROM < votre\_base de données\_name.your\_table\_nom >-est suffisant.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-282">In hello **Hive database query** box, a simple SELECT * FROM <your\_database\_name.your\_table\_name> - is enough.</span></span>
3. <span data-ttu-id="d7f8e-283">**URI du serveur Hcatalog** : si votre cluster se nomme « abc », vous avez donc : https://abc.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="d7f8e-283">**Hcatalog server URI**: If your cluster is "abc", then this is simply: https://abc.azurehdinsight.net</span></span>
4. <span data-ttu-id="d7f8e-284">**Nom du compte utilisateur Hadoop**: nom d’utilisateur hello choisie au moment de la mise en service de cluster de hello du hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-284">**Hadoop user account name**: hello user name chosen at hello time of commissioning hello cluster.</span></span> <span data-ttu-id="d7f8e-285">(Non hello accès à distance nom d’utilisateur !)</span><span class="sxs-lookup"><span data-stu-id="d7f8e-285">(NOT hello Remote Access user name!)</span></span>
5. <span data-ttu-id="d7f8e-286">**Mot de passe utilisateur Hadoop**: mot de passe hello pour nom d’utilisateur hello choisie au moment de la mise en service de cluster de hello du hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-286">**Hadoop user account password**: hello password for hello user name chosen at hello time of commissioning hello cluster.</span></span> <span data-ttu-id="d7f8e-287">(Pas passe de l’accès à distance hello !)</span><span class="sxs-lookup"><span data-stu-id="d7f8e-287">(NOT hello Remote Access password!)</span></span>
6. <span data-ttu-id="d7f8e-288">**Emplacement des données de sortie**: choisissez « Azure »</span><span class="sxs-lookup"><span data-stu-id="d7f8e-288">**Location of output data**: Choose "Azure"</span></span>
7. <span data-ttu-id="d7f8e-289">**Nom de compte de stockage Azure**: hello compte de stockage associé au cluster de hello</span><span class="sxs-lookup"><span data-stu-id="d7f8e-289">**Azure storage account name**: hello storage account associated with hello cluster</span></span>
8. <span data-ttu-id="d7f8e-290">**Clé de compte de stockage Azure**: clé hello hello du compte de stockage associé au cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-290">**Azure storage account key**: hello key of hello storage account associated with hello cluster.</span></span>
9. <span data-ttu-id="d7f8e-291">**Nom du conteneur Azure**: si le nom du cluster hello est « abc », alors il s’agit simplement « abc », généralement.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-291">**Azure container name**: If hello cluster name is "abc", then this is simply "abc", usually.</span></span>

<span data-ttu-id="d7f8e-292">Une fois hello **importer des données** a fini de l’obtention de données (vous voyez les graduations hello verte sur hello Module), enregistrez ces données comme un jeu de données (avec un nom de votre choix).</span><span class="sxs-lookup"><span data-stu-id="d7f8e-292">Once hello **Import Data** finishes getting data (you see hello green tick on hello Module), save this data as a Dataset (with a name of your choice).</span></span> <span data-ttu-id="d7f8e-293">Cela ressemble à :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-293">What this looks like:</span></span>

![Import Data enregistre des données](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

<span data-ttu-id="d7f8e-295">Avec le bouton hello sortie de hello **importer des données** module.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-295">Right-click hello output port of hello **Import Data** module.</span></span> <span data-ttu-id="d7f8e-296">Ceci fait apparaître une option **Enregistrer comme dataset** et une option **Visualiser**.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-296">This reveals a **Save as dataset** option and a **Visualize** option.</span></span> <span data-ttu-id="d7f8e-297">Hello **visualiser** option, si vous cliquez dessus, affiche les 100 lignes de données hello, ainsi que d’un panneau de droite qui est utile pour des statistiques de résumé.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-297">hello **Visualize** option, if clicked, displays 100 rows of hello data, along with a right panel that is useful for some summary statistics.</span></span> <span data-ttu-id="d7f8e-298">toosave des données, il suffit de sélectionner **enregistrer en tant que jeu de données** et suivez les instructions.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-298">toosave data, simply select **Save as dataset** and follow instructions.</span></span>

<span data-ttu-id="d7f8e-299">jeu de données tooselect hello enregistré pour une utilisation dans une expérience d’apprentissage machine, recherchez hello de jeux de données à l’aide de hello **recherche** zone illustrée dans la figure suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-299">tooselect hello saved dataset for use in a machine learning experiment, locate hello datasets using hello **Search** box shown in hello following figure.</span></span> <span data-ttu-id="d7f8e-300">Puis tapez simplement nom hello vous donnez hello dataset partiellement tooaccess il et faites glisser hello dataset vers hello panneau principal.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-300">Then simply type out hello name you gave hello dataset partially tooaccess it and drag hello dataset onto hello main panel.</span></span> <span data-ttu-id="d7f8e-301">Déplacée dans le panneau de configuration principal hello le sélectionne pour une utilisation dans la modélisation d’apprentissage machine.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-301">Dropping it onto hello main panel selects it for use in machine learning modeling.</span></span>

![Jeu de données Drage sur Panneau de configuration principal hello](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> <span data-ttu-id="d7f8e-303">Le fait pour effectuer l’apprentissage hello et jeux de données de test hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-303">Do this for both hello train and hello test datasets.</span></span> <span data-ttu-id="d7f8e-304">En outre, n’oubliez pas toouse hello base de données et les noms de table que vous avez attribué à cet effet.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-304">Also, remember toouse hello database name and table names that you gave for this purpose.</span></span> <span data-ttu-id="d7f8e-305">les valeurs Hello utilisées dans la figure hello sont uniquement d’illustration purposes.* *</span><span class="sxs-lookup"><span data-stu-id="d7f8e-305">hello values used in hello figure are solely for illustration purposes.**</span></span>
> 
> 

### <span data-ttu-id="d7f8e-306"><a name="step2"></a>Étape 2 : Créer une expérience simple dans Azure Machine Learning toopredict clics / aucun clic</span><span class="sxs-lookup"><span data-stu-id="d7f8e-306"><a name="step2"></a> Step 2: Create a simple experiment in Azure Machine Learning toopredict clicks / no clicks</span></span>
<span data-ttu-id="d7f8e-307">Notre expérience Azure ML ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-307">Our Azure ML experiment looks like this:</span></span>

![Expérience Machine Learning](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

<span data-ttu-id="d7f8e-309">Examinons maintenant hello principaux composants de cette expérience.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-309">We now examine hello key components of this experiment.</span></span> <span data-ttu-id="d7f8e-310">En guise de rappel, nous devons toodrag notre enregistré effectuer l’apprentissage et jeux de données sur le canevas de l’expérience tooour tester au préalable.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-310">As a reminder, we need toodrag our saved train and test datasets on tooour experiment canvas first.</span></span>

#### <a name="clean-missing-data"></a><span data-ttu-id="d7f8e-311">Nettoyage des données manquantes</span><span class="sxs-lookup"><span data-stu-id="d7f8e-311">Clean Missing Data</span></span>
<span data-ttu-id="d7f8e-312">Hello **Clean Missing Data** module est ce que son nom l’indique : il nettoie les données manquantes d’une manière qui peut être spécifié par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-312">hello **Clean Missing Data** module does what its name suggests:  it cleans missing data in ways that can be user-specified.</span></span> <span data-ttu-id="d7f8e-313">Dans ce module, nous pouvons voir ceci :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-313">Looking into this module, we see this:</span></span>

![Nettoyage des données manquantes](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

<span data-ttu-id="d7f8e-315">Ici, nous avons choisi tooreplace toutes les valeurs manquantes par un 0.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-315">Here, we chose tooreplace all missing values with a 0.</span></span> <span data-ttu-id="d7f8e-316">D’autres options sont également, qui peuvent être consultées en examinant les menus déroulants de hello de module de hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-316">There are other options as well, which can be seen by looking at hello dropdowns in hello module.</span></span>

#### <a name="feature-engineering-on-hello-data"></a><span data-ttu-id="d7f8e-317">Ingénierie de fonctionnalité sur les données de salutation</span><span class="sxs-lookup"><span data-stu-id="d7f8e-317">Feature engineering on hello data</span></span>
<span data-ttu-id="d7f8e-318">Certaines fonctionnalités catégorielles de jeux de données volumineux peuvent rassembler des millions de valeurs uniques.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-318">There can be millions of unique values for some categorical features of large datasets.</span></span> <span data-ttu-id="d7f8e-319">L’utilisation des techniques naïves, telles que l’encodage à chaud pour représenter des fonctionnalités catégorielles de grande dimension, est tout bonnement impossible.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-319">Using naive methods such as one-hot encoding for representing such high-dimensional categorical features is entirely unfeasible.</span></span> <span data-ttu-id="d7f8e-320">Dans cette procédure pas à pas, nous allons montrer comment les fonctionnalités de nombre de toouse à l’aide intégrée toogenerate de modules Azure Machine Learning compact représentations de ces variables catégorielles de grande dimension.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-320">In this walkthrough, we demonstrate how toouse count features using built-in Azure Machine Learning modules toogenerate compact representations of these high-dimensional categorical variables.</span></span> <span data-ttu-id="d7f8e-321">Hello résultat final est une plus petite taille de modèle, le temps de formation plus rapides et des métriques de performances sont tout à fait comparable toousing autres techniques.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-321">hello end-result is a smaller model size, faster training times, and performance metrics that are quite comparable toousing other techniques.</span></span>

##### <a name="building-counting-transforms"></a><span data-ttu-id="d7f8e-322">Création de transformations de comptage</span><span class="sxs-lookup"><span data-stu-id="d7f8e-322">Building counting transforms</span></span>
<span data-ttu-id="d7f8e-323">fonctionnalités de nombre toobuild, nous utilisons hello **générer comptage transformer** module qui est disponible dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-323">toobuild count features, we use hello **Build Counting Transform** module that is available in Azure Machine Learning.</span></span> <span data-ttu-id="d7f8e-324">module de Hello ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-324">hello module looks like this:</span></span>

<span data-ttu-id="d7f8e-325">![Créer un module de transformation de comptage](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Créer un module de transformation de comptage](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span><span class="sxs-lookup"><span data-stu-id="d7f8e-325">![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="d7f8e-326">Bonjour **compter les colonnes** , nous, saisissez les colonnes que nous souhaitons tooperform compte.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-326">In hello **Count columns** box, we enter those columns that we wish tooperform counts on.</span></span> <span data-ttu-id="d7f8e-327">En règle générale, il s'agit de colonnes catégorielles de grande dimension (comme indiqué).</span><span class="sxs-lookup"><span data-stu-id="d7f8e-327">Typically, these are (as mentioned) high-dimensional categorical columns.</span></span> <span data-ttu-id="d7f8e-328">Au démarrage de hello, nous l’avons mentionné hello Criteo jeu de données a des colonnes catégorielles 26 : à partir de Col15 tooCol40.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-328">At hello start, we mentioned that hello Criteo dataset has 26 categorical columns: from Col15 tooCol40.</span></span> <span data-ttu-id="d7f8e-329">Ici, nous compter sur chacune d'entre elles et leurs index (de 15 too40 séparés par des virgules, comme indiqué).</span><span class="sxs-lookup"><span data-stu-id="d7f8e-329">Here, we count on all of them and give their indices (from 15 too40 separated by commas as shown).</span></span>
> 

<span data-ttu-id="d7f8e-330">module hello toouse hello mode MapReduce (le cas pour les jeux de données volumineux), nous devons accéder au cluster HDInsight Hadoop de tooan (hello celui utilisé pour l’exploration de la fonctionnalité peut être réutilisé à cet effet ainsi) et ses informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-330">toouse hello module in hello MapReduce mode (appropriate for large datasets), we need access tooan HDInsight Hadoop cluster (hello one used for feature exploration can be reused for this purpose as well) and its credentials.</span></span> <span data-ttu-id="d7f8e-331">les figures précédentes Hello illustrent hello renseignés valeurs ressemble (remplacez les valeurs hello fournies à titre d’illustration avec ceux appropriés pour votre propre cas d’utilisation).</span><span class="sxs-lookup"><span data-stu-id="d7f8e-331">hello  previous figures illustrate what hello filled-in values look like (replace hello values provided for illustration with those relevant for your own use-case).</span></span>

![Paramètres du module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

<span data-ttu-id="d7f8e-333">Dans la figure hello ci-dessus, nous montrons comment tooenter hello d’entrée d’objet blob emplacement.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-333">In hello figure above, we show how tooenter hello input blob location.</span></span> <span data-ttu-id="d7f8e-334">Cet emplacement a réservé pour la création de tables de nombres les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-334">This location has hello data reserved for building count tables on.</span></span>

<span data-ttu-id="d7f8e-335">Une fois ce module a terminé son exécution, nous pouvons enregistrer transformation hello pour ultérieurement en double-cliquant sur le module de hello et en sélectionnant hello **enregistrer en tant que transformation** option :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-335">After this module finishes running, we can save hello transform for later by right-clicking hello module and selecting hello **Save as Transform** option:</span></span>

![Option « Enregistrer en tant que transformation »](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

<span data-ttu-id="d7f8e-337">Dans notre expérience l’architecture illustrée ci-dessus, hello dataset « ytransform2 » correspond précisément les tooa enregistré la transformation de nombre.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-337">In our experiment architecture shown above, hello dataset "ytransform2" corresponds precisely tooa saved count transform.</span></span> <span data-ttu-id="d7f8e-338">Pour le reste de hello de cette expérience, nous partons du principe que lecteur hello utilisé un **générer comptage transformer** module sur certaines données toogenerate nombres et peut ensuite utiliser ces fonctionnalités de nombre de nombres toogenerate train de hello et jeux de données de test.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-338">For hello remainder of this experiment, we assume that hello reader used a **Build Counting Transform** module on some data toogenerate counts, and can then use those counts toogenerate count features on hello train and test datasets.</span></span>

##### <a name="choosing-what-count-features-tooinclude-as-part-of-hello-train-and-test-datasets"></a><span data-ttu-id="d7f8e-339">En choisissant ce que nombre tooinclude de fonctionnalités dans le cadre de l’apprentissage de hello et jeux de données de test</span><span class="sxs-lookup"><span data-stu-id="d7f8e-339">Choosing what count features tooinclude as part of hello train and test datasets</span></span>
<span data-ttu-id="d7f8e-340">Une fois que nous disposons d’un nombre transformer prêt, utilisateur de hello choisir quelles tooinclude de fonctionnalités dans leur apprentissage et tester des jeux de données à l’aide de hello **modifier les paramètres de Table nombre** module.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-340">Once we have a count transform ready, hello user can choose what features tooinclude in their train and test datasets using hello **Modify Count Table Parameters** module.</span></span> <span data-ttu-id="d7f8e-341">Nous montrons ce module ici par souci d’exhaustivité, mais dans un souci de simplification nous ne l’utilisons pas dans notre expérience.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-341">We just show this module here for completeness, but in interests of simplicity do not actually use it in our experiment.</span></span>

![Modifier les paramètres de la table de comptage](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

<span data-ttu-id="d7f8e-343">Dans ce cas, comme le montre, nous avons choisi toouse probabilités de journalisation simplement hello et tooignore hello rétrogradation de la colonne.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-343">In this case, as can be seen, we have chosen toouse just hello log-odds and tooignore hello back off column.</span></span> <span data-ttu-id="d7f8e-344">Nous pouvons également définir des paramètres tels que hello bin plafond, combien tooadd exemples pseudo-aléatoire préalable de lissage, et si toouse tout Laplace parasites ou non.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-344">We can also set parameters such as hello garbage bin threshold, how many pseudo-prior examples tooadd for smoothing, and whether toouse any Laplacian noise or not.</span></span> <span data-ttu-id="d7f8e-345">Tous ces éléments sont des fonctionnalités avancées, et il est toobe de noter que les valeurs par défaut de hello sont un bon point de départ pour les utilisateurs qui sont de nouveau type toothis de la génération de la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-345">All these are advanced features and it is toobe noted that hello default values are a good starting point for users who are new toothis type of feature generation.</span></span>

##### <a name="data-transformation-before-generating-hello-count-features"></a><span data-ttu-id="d7f8e-346">Transformation de données avant de générer des fonctionnalités de nombre hello</span><span class="sxs-lookup"><span data-stu-id="d7f8e-346">Data transformation before generating hello count features</span></span>
<span data-ttu-id="d7f8e-347">Maintenant nous concentrer sur un point important sur la transformation de notre train et tooactually préalable de données des fonctionnalités de comptage de génération de test.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-347">Now we focus on an important point about transforming our train and test data prior tooactually generating count features.</span></span> <span data-ttu-id="d7f8e-348">Notez qu’il existe deux **Execute R Script** modules utilisés avant que nous appliquons hello nombre transformer tooour des données.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-348">Note that there are two **Execute R Script** modules used before we apply hello count transform tooour data.</span></span>

![Modules Exécuter le script R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

<span data-ttu-id="d7f8e-350">Voici le script R de la première hello :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-350">Here is hello first R script:</span></span>

![Premier script R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

<span data-ttu-id="d7f8e-352">Dans ce script R, nous renommer trop notre toonames colonnes « Col1 » « Col40 ».</span><span class="sxs-lookup"><span data-stu-id="d7f8e-352">In this R script, we rename our columns toonames "Col1" too"Col40".</span></span> <span data-ttu-id="d7f8e-353">Il s’agit, car hello count transformation attend des noms de ce format.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-353">This is because hello count transform expects names of this format.</span></span>

<span data-ttu-id="d7f8e-354">Dans le script R de la deuxième hello, nous équilibrer la distribution hello entre classes positifs et négatifs (classes 1 et 0 respectivement) par classe négatif de sous-échantillonnage hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-354">In hello second R script, we balance hello distribution between positive and negative classes (classes 1 and 0 respectively) by downsampling hello negative class.</span></span> <span data-ttu-id="d7f8e-355">Hello R script ici montre comment toodo cela :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-355">hello R script here shows how toodo this:</span></span>

![Deuxième script R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

<span data-ttu-id="d7f8e-357">Dans ce script R simple, nous utilisons « pos\_neg\_rapport « durée hello tooset équilibre entre hello positif et les classes négatif hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-357">In this simple R script, we use "pos\_neg\_ratio" tooset hello amount of balance between hello positive and hello negative classes.</span></span> <span data-ttu-id="d7f8e-358">Ceci est important toodo amélioration déséquilibre de la classe généralement ayant des gains de performance pour les problèmes de classification lorsque la distribution de classe hello est rétrécie (n’oubliez pas que dans le cas présent, nous avons 3.3 % des classes positif et 96,7 % négatif).</span><span class="sxs-lookup"><span data-stu-id="d7f8e-358">This is important toodo since improving class imbalance usually has performance benefits for classification problems where hello class distribution is skewed (recall that in our case, we have 3.3% positive class and 96.7% negative class).</span></span>

##### <a name="applying-hello-count-transformation-on-our-data"></a><span data-ttu-id="d7f8e-359">Application d’une transformation de nombre hello sur nos données</span><span class="sxs-lookup"><span data-stu-id="d7f8e-359">Applying hello count transformation on our data</span></span>
<span data-ttu-id="d7f8e-360">Enfin, nous pouvons utiliser hello **appliquer une Transformation** module tooapply hello nombre des transformations sur notre effectuer l’apprentissage et jeux de données de test.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-360">Finally, we can use hello **Apply Transformation** module tooapply hello count transforms on our train and test datasets.</span></span> <span data-ttu-id="d7f8e-361">Ce module prend la transformation de nombre hello enregistré comme une entrée hello l’apprentissage et jeux de données de test comme hello autres entrées et renvoie des données avec des fonctionnalités de nombre.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-361">This module takes hello saved count transform as one input and hello train or test datasets as hello other input, and returns data with count features.</span></span> <span data-ttu-id="d7f8e-362">En voici l’illustration :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-362">It is shown here:</span></span>

![Appliquer le module de transformation](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-hello-count-features-look-like"></a><span data-ttu-id="d7f8e-364">Un extrait de l’aspect de fonctionnalités de comptage hello</span><span class="sxs-lookup"><span data-stu-id="d7f8e-364">An excerpt of what hello count features look like</span></span>
<span data-ttu-id="d7f8e-365">Il est intéressant toosee les fonctionnalités de comptage hello se présenter comme dans le cas présent.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-365">It is instructive toosee what hello count features look like in our case.</span></span> <span data-ttu-id="d7f8e-366">En voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-366">Here we show an excerpt of this:</span></span>

![Fonctionnalités de comptage](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

<span data-ttu-id="d7f8e-368">Dans cet extrait, nous allons montrer que des colonnes hello recensement sur, nous obtenir le nombre hello et connectez-vous cotes backoffs pertinentes de tooany Ajout.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-368">In this excerpt, we show that for hello columns that we counted on, we get hello counts and log odds in addition tooany relevant backoffs.</span></span>

<span data-ttu-id="d7f8e-369">Nous sommes maintenant prêt toobuild un modèle Azure Machine Learning à l’aide de ces jeux de données transformé.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-369">We are now ready toobuild an Azure Machine Learning model using these transformed datasets.</span></span> <span data-ttu-id="d7f8e-370">Dans la section suivante de hello, nous montrons comment procéder.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-370">In hello next section, we show how this can be done.</span></span>

### <span data-ttu-id="d7f8e-371"><a name="step3"></a>Étape 3 : Créer, assimiler et score hello modèle</span><span class="sxs-lookup"><span data-stu-id="d7f8e-371"><a name="step3"></a> Step 3: Build, train, and score hello model</span></span>

#### <a name="choice-of-learner"></a><span data-ttu-id="d7f8e-372">Choix de l'apprenant</span><span class="sxs-lookup"><span data-stu-id="d7f8e-372">Choice of learner</span></span>
<span data-ttu-id="d7f8e-373">Tout d’abord, nous devons toochoose un apprenant.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-373">First, we need toochoose a learner.</span></span> <span data-ttu-id="d7f8e-374">Nous sommes continu toouse un arbre de décision augmentés de deux classes en tant que notre apprenant.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-374">We are going toouse a two class boosted decision tree as our learner.</span></span> <span data-ttu-id="d7f8e-375">Voici les options par défaut de hello pour cet apprenant :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-375">Here are hello default options for this learner:</span></span>

![Paramètres de l’arbre de décision optimisé à deux classes](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

<span data-ttu-id="d7f8e-377">Pour notre expérience, nous sont les valeurs par défaut de cours toochoose hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-377">For our experiment, we are going toochoose hello default values.</span></span> <span data-ttu-id="d7f8e-378">Vous constatez que hello par défaut sont généralement explicite et une bonne solution tooget rapide lignes de base sur les performances.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-378">We note that hello defaults are usually meaningful and a good way tooget quick baselines on performance.</span></span> <span data-ttu-id="d7f8e-379">Vous pouvez améliorer sur les performances par balayage des paramètres si vous choisissez tooonce que vous avez une ligne de base.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-379">You can improve on performance by sweeping parameters if you choose tooonce you have a baseline.</span></span>

#### <a name="train-hello-model"></a><span data-ttu-id="d7f8e-380">Modèle de hello train</span><span class="sxs-lookup"><span data-stu-id="d7f8e-380">Train hello model</span></span>
<span data-ttu-id="d7f8e-381">Pour l'apprentissage, nous appelons simplement un module **Former le modèle** .</span><span class="sxs-lookup"><span data-stu-id="d7f8e-381">For training, we simply invoke a **Train Model** module.</span></span> <span data-ttu-id="d7f8e-382">Hello deux entrées tooit sont apprenant de Two-Class Boosted Decision Tree hello et notre jeu de données d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-382">hello two inputs tooit are hello Two-Class Boosted Decision Tree learner and our train dataset.</span></span> <span data-ttu-id="d7f8e-383">En voici l’illustration :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-383">This is shown here:</span></span>

![Module de formation de modèle](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-hello-model"></a><span data-ttu-id="d7f8e-385">Modèle de score hello</span><span class="sxs-lookup"><span data-stu-id="d7f8e-385">Score hello model</span></span>
<span data-ttu-id="d7f8e-386">Une fois que nous disposons d’un modèle formé, nous sommes prêts tooscore sur hello tester dataset et tooevaluate ses performances.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-386">Once we have a trained model, we are ready tooscore on hello test dataset and tooevaluate its performance.</span></span> <span data-ttu-id="d7f8e-387">Pour ce faire, nous à l’aide de hello **Score Model** module illustré hello suivant figure, avec un **modèle Evaluate** module :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-387">We do this by using hello **Score Model** module shown in hello following figure, along with an **Evaluate Model** module:</span></span>

![Score Model module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <span data-ttu-id="d7f8e-389"><a name="step4"></a>Étape 4 : Évaluer le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="d7f8e-389"><a name="step4"></a> Step 4: Evaluate hello model</span></span>
<span data-ttu-id="d7f8e-390">Enfin, nous aimerions tooanalyze performances du modèle.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-390">Finally, we would like tooanalyze model performance.</span></span> <span data-ttu-id="d7f8e-391">En règle générale, pour les deux problèmes de classification (binaire) de classe, une bonne mesure est hello AUC.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-391">Usually, for two class (binary) classification problems, a good measure is hello AUC.</span></span> <span data-ttu-id="d7f8e-392">toovisualize, nous raccorder hello **Score Model** module tooan **modèle Evaluate** module pour cela.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-392">toovisualize this, we hook up hello **Score Model** module tooan **Evaluate Model** module for this.</span></span> <span data-ttu-id="d7f8e-393">En cliquant sur **visualiser** sur hello **modèle Evaluate** module génère un graphique comme hello suivant un :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-393">Clicking **Visualize** on hello **Evaluate Model** module yields a graphic like hello following one:</span></span>

![Évaluation du modèle du module BDT](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

<span data-ttu-id="d7f8e-395">Dans le binaire (ou classe deux) des problèmes de classification, une bonne mesure de précision de prédiction est hello zone sous courbe (AUC).</span><span class="sxs-lookup"><span data-stu-id="d7f8e-395">In binary (or two class) classification problems, a good measure of prediction accuracy is hello Area Under Curve (AUC).</span></span> <span data-ttu-id="d7f8e-396">Nous présentons ci-après nos résultats à l’aide de ce modèle sur notre jeu de données de test.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-396">In what follows, we show our results using this model on our test dataset.</span></span> <span data-ttu-id="d7f8e-397">tooget, port de sortie avec le bouton hello Hello **modèle Evaluate** module, puis **visualiser**.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-397">tooget this, right-click hello output port of hello **Evaluate Model** module and then **Visualize**.</span></span>

![Visualisation du module Évaluer le modèle](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <span data-ttu-id="d7f8e-399"><a name="step5"></a>Étape 5 : Publier un modèle de hello comme un service Web</span><span class="sxs-lookup"><span data-stu-id="d7f8e-399"><a name="step5"></a> Step 5: Publish hello model as a Web service</span></span>
<span data-ttu-id="d7f8e-400">possibilité de Hello toopublish un modèle Azure Machine Learning en tant que services web avec un minimum de complications est une fonctionnalité précieuse pour rendre largement disponible.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-400">hello ability toopublish an Azure Machine Learning model as web services with a minimum of fuss is a valuable feature for making it widely available.</span></span> <span data-ttu-id="d7f8e-401">Une fois que vous avez terminé, tout le monde peut rendre les appels toohello web service avec des données d’entrée dont ils ont besoin des prédictions pour que service web de hello utilise hello modèle tooreturn ces prédictions.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-401">Once that is done, anyone can make calls toohello web service with input data that they need predictions for, and hello web service uses hello model tooreturn those predictions.</span></span>

<span data-ttu-id="d7f8e-402">toodo, nous avons tout d’abord enregistrer notre modèle formé en tant qu’objet modèle formé.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-402">toodo this, we first save our trained model as a Trained Model object.</span></span> <span data-ttu-id="d7f8e-403">Cela en double-cliquant sur hello **Train Model** module et à l’aide de hello **enregistrer en tant que modèle formé** option.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-403">This is done by right-clicking hello **Train Model** module and using hello **Save as Trained Model** option.</span></span>

<span data-ttu-id="d7f8e-404">Ensuite, nous devons toocreate entrée et sortie ports pour notre service web :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-404">Next, we need toocreate input and output ports for our web service:</span></span>

* <span data-ttu-id="d7f8e-405">Récupère les données Bonjour même formulaire en tant que données hello dont nous avons besoin des prédictions pour un port d’entrée</span><span class="sxs-lookup"><span data-stu-id="d7f8e-405">an input port takes data in hello same form as hello data that we need predictions for</span></span>
* <span data-ttu-id="d7f8e-406">un port de sortie retourne hello Scored Labels et les probabilités de hello associé.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-406">an output port returns hello Scored Labels and hello associated probabilities.</span></span>

#### <a name="select-a-few-rows-of-data-for-hello-input-port"></a><span data-ttu-id="d7f8e-407">Sélectionnez quelques lignes de données pour le port d’entrée de hello</span><span class="sxs-lookup"><span data-stu-id="d7f8e-407">Select a few rows of data for hello input port</span></span>
<span data-ttu-id="d7f8e-408">Il est pratique toouse un **Apply SQL Transformation** module tooselect seulement 10 lignes tooserve comme hello d’entrée donnée de port.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-408">It is convenient toouse an **Apply SQL Transformation** module tooselect just 10 rows tooserve as hello input port data.</span></span> <span data-ttu-id="d7f8e-409">Sélectionnez les lignes de données pour notre port d’entrée à l’aide de la requête SQL de hello indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-409">Select just these rows of data for our input port using hello SQL query shown here:</span></span>

![Données du port d'entrée](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a><span data-ttu-id="d7f8e-411">Service Web</span><span class="sxs-lookup"><span data-stu-id="d7f8e-411">Web service</span></span>
<span data-ttu-id="d7f8e-412">Est maintenant prêt à toorun une expérience de petite qui peut être utilisé toopublish notre service web.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-412">Now we are ready toorun a small experiment that can be used toopublish our web service.</span></span>

#### <a name="generate-input-data-for-webservice"></a><span data-ttu-id="d7f8e-413">Générer des données d'entrée pour le service Web</span><span class="sxs-lookup"><span data-stu-id="d7f8e-413">Generate input data for webservice</span></span>
<span data-ttu-id="d7f8e-414">Comme une étape de zéro, étant donné que la table de nombres hello est volumineuse, nous prendre de quelques lignes de données de test et générer des données de sortie à partir de celui-ci avec les fonctionnalités de nombre.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-414">As a zeroth step, since hello count table is large, we take a few lines of test data and generate output data from it with count features.</span></span> <span data-ttu-id="d7f8e-415">Cela peut servir de format de données d’entrée hello pour notre service Web.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-415">This can serve as hello input data format for our webservice.</span></span> <span data-ttu-id="d7f8e-416">En voici l’illustration :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-416">This is shown here:</span></span>

![Création des données d'entrée BDT](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> <span data-ttu-id="d7f8e-418">Pour le format de données d’entrée hello, nous utilisons désormais hello sortie Hello **Featurizer** module.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-418">For hello input data format, we now use hello OUTPUT of hello **Count Featurizer** module.</span></span> <span data-ttu-id="d7f8e-419">Une fois que cela tester la fin de son exécution, enregistrer la sortie de hello de hello **Featurizer** module comme un jeu de données.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-419">Once this experiment finishes running, save hello output from hello **Count Featurizer** module as a Dataset.</span></span> <span data-ttu-id="d7f8e-420">Ce jeu de données est utilisé pour les données d’entrée de hello dans hello webservice.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-420">This Dataset is used for hello input data in hello webservice.</span></span>
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a><span data-ttu-id="d7f8e-421">Expérience d’évaluation de la publication du service Web</span><span class="sxs-lookup"><span data-stu-id="d7f8e-421">Scoring experiment for publishing webservice</span></span>
<span data-ttu-id="d7f8e-422">Tout d’abord, nous vous indiquons ci-dessous à quoi cela ressemble.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-422">First, we show what this looks like.</span></span> <span data-ttu-id="d7f8e-423">structure d’essentielles Hello est un **Score Model** module qui accepte notre objet modèle formé et quelques lignes de données d’entrée que nous avons généré dans les étapes précédentes hello à l’aide de hello **Featurizer** module.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-423">hello essential structure is a **Score Model** module that accepts our trained model object and a few lines of input data that we generated in hello previous steps using hello **Count Featurizer** module.</span></span> <span data-ttu-id="d7f8e-424">Nous utilisons tooproject « Sélectionner les colonnes dans Dataset » hello au score calculé étiquettes et les probabilités de Score hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-424">We use "Select Columns in Dataset" tooproject out hello Scored labels and hello Score probabilities.</span></span>

![Sélectionner des colonnes dans le jeu de données](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

<span data-ttu-id="d7f8e-426">Notez comment hello **sélectionner les colonnes dans le jeu de données** module peut être utilisé pour le « filtrage « données à partir d’un jeu de données.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-426">Notice how hello **Select Columns in Dataset** module can be used for 'filtering' data out from a dataset.</span></span> <span data-ttu-id="d7f8e-427">Nous afficher le contenu de hello ici :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-427">We show hello contents here:</span></span>

![Le filtrage avec hello sélectionner les colonnes dans le module de jeu de données](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

<span data-ttu-id="d7f8e-429">les ports tooget hello bleu d’entrée et sortie, cliquez simplement sur **préparer webservice** en bas de hello à droite.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-429">tooget hello blue input and output ports, you simply click **prepare webservice** at hello bottom right.</span></span> <span data-ttu-id="d7f8e-430">Exécutez cette expérience nous permet également de service web de hello toopublish : cliquez sur hello **publier le SERVICE WEB** icône à hello en bas à droite, présenté ici :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-430">Running this experiment also allows us toopublish hello web service: click hello **PUBLISH WEB SERVICE** icon at hello bottom right, shown here:</span></span>

![Publication du service Web](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

<span data-ttu-id="d7f8e-432">Une fois publiée hello webservice, nous obtenons page redirigé tooa qui se présente ainsi :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-432">Once hello webservice is published, we get redirected tooa page that looks thus:</span></span>

![Tableau de bord du service web](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

<span data-ttu-id="d7f8e-434">Nous voyons deux liens pour webservices sur le côté gauche de hello :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-434">We see two links for webservices on hello left side:</span></span>

* <span data-ttu-id="d7f8e-435">Hello **demande/réponse** Service (ou les enregistrements de ressources) est destiné à des prévisions uniques et est ce que nous allons utiliser dans cet atelier.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-435">hello **REQUEST/RESPONSE** Service (or RRS) is meant for single predictions and is what we utilize in this workshop.</span></span>
* <span data-ttu-id="d7f8e-436">Hello **l’exécution par lots** Service (BES) est utilisé pour les prédictions par lot et nécessite que des prédictions toomake de données d’entrée utilisées hello se trouvent dans le stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-436">hello **BATCH EXECUTION** Service (BES) is used for batch predictions and requires that hello input data used toomake predictions reside in Azure Blob Storage.</span></span>

<span data-ttu-id="d7f8e-437">En cliquant sur le lien de hello **demande/réponse** nous prend tooa page nous conserves préalable de code en c#, python et R. Ce code peut être utilisé pour effectuer des appels toohello webservice.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-437">Clicking on hello link **REQUEST/RESPONSE** takes us tooa page that gives us pre-canned code in C#, python, and R. This code can be conveniently used for making calls toohello webservice.</span></span> <span data-ttu-id="d7f8e-438">Notez que cette clé d’API sur cette page hello doit toobe utilisé pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-438">Note that hello API key on this page needs toobe used for authentication.</span></span>

<span data-ttu-id="d7f8e-439">Il est pratique toocopy cette python code sur tooa nouvelle cellule dans le bloc-notes de notebooks hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-439">It is convenient toocopy this python code over tooa new cell in hello IPython notebook.</span></span>

<span data-ttu-id="d7f8e-440">Ici, nous affichons un segment de code python avec la clé d’API correcte hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-440">Here we show a segment of python code with hello correct API key.</span></span>

![Code Python](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

<span data-ttu-id="d7f8e-442">Notez que nous avons remplacé clé d’API hello par défaut avec la clé de l’API de notre webservices.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-442">Note that we replaced hello default API key with our webservices's API key.</span></span> <span data-ttu-id="d7f8e-443">En cliquant sur **exécuter** sur cette cellule dans un notebooks bloc-notes génère hello suivant la réponse :</span><span class="sxs-lookup"><span data-stu-id="d7f8e-443">Clicking **Run** on this cell in an IPython notebook yields hello following response:</span></span>

![Réponse IPython](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

<span data-ttu-id="d7f8e-445">Nous constatons que pour hello deux tester les exemples, que nous avons interrogés (dans le cadre JSON de hello du script de python hello), nous obtenons réponses sous forme de hello « Au score calculé étiquettes, les probabilités au score calculé ».</span><span class="sxs-lookup"><span data-stu-id="d7f8e-445">We see that for hello two test examples we asked about (in hello JSON framework of hello python script), we get back answers in hello form "Scored Labels, Scored Probabilities".</span></span> <span data-ttu-id="d7f8e-446">Notez que dans ce cas, nous avons choisi par défaut hello ce code pré-enregistrée hello fournit (0 pour toutes les colonnes numériques et de chaîne de hello « valeur » pour toutes les colonnes catégorielles).</span><span class="sxs-lookup"><span data-stu-id="d7f8e-446">Note that in this case, we chose hello default values that hello pre-canned code provides (0's for all numeric columns and hello string "value" for all categorical columns).</span></span>

<span data-ttu-id="d7f8e-447">Ceci conclut notre procédure pas à pas de bout en bout de montrant comment toohandle dataset à grande échelle à l’aide d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-447">This concludes our end-to-end walkthrough showing how toohandle large-scale dataset using Azure Machine Learning.</span></span> <span data-ttu-id="d7f8e-448">Nous avons démarré avec un téraoctet de données, construit un modèle de prévision et déployé comme un service web dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="d7f8e-448">We started with a terabyte of data, constructed a prediction model and deployed it as a web service in hello cloud.</span></span>

