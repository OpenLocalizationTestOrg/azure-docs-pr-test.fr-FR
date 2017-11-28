---
title: "aaaExplore des données dans un Hadoop de cluster et créer des modèles dans Azure Machine Learning | Documents Microsoft"
description: "Pour un scénario de bout en bout utilisant un HDInsight Hadoop à l’aide de hello processus de science des données de Team toobuild de cluster et déployer un modèle à l’aide d’un jeu de données disponible publiquement."
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e9e76c91-d0f6-483d-bae7-2d3157b86aa0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: a371032e356ffc366af0d6fbe364af281b6efd19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a><span data-ttu-id="17cd9-103">Hello processus de science des données équipe en action : utilisez Azure HDInsight Hadoop de clusters</span><span class="sxs-lookup"><span data-stu-id="17cd9-103">hello Team Data Science Process in action: Use Azure HDInsight Hadoop clusters</span></span>
<span data-ttu-id="17cd9-104">Dans cette procédure pas à pas, nous utilisons hello [processus de science des données équipe (TDSP)](data-science-process-overview.md) dans un scénario de bout en bout à l’aide un [cluster Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, Explorer et d’une fonctionnalité publiquement les données d’ingénierie à rebours de hello disponible [NYC Taxi allers-retours](http://www.andresmh.com/nyctaxitrips/) dataset et toodown échantillonner les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="17cd9-104">In this walkthrough, we use hello [Team Data Science Process (TDSP)](data-science-process-overview.md) in an end-to-end scenario using an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore and feature engineer data from hello publicly available [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset, and toodown sample hello data.</span></span> <span data-ttu-id="17cd9-105">Modèles de données de hello sont générés avec Azure Machine Learning toohandle binaire et multiclasses classification et la régression tâches prédictives.</span><span class="sxs-lookup"><span data-stu-id="17cd9-105">Models of hello data are built with Azure Machine Learning toohandle binary and multiclass classification and regression predictive tasks.</span></span>

<span data-ttu-id="17cd9-106">Pour une procédure pas à pas qui montre comment toohandle un plus grand jeu de données (1 téraoctet) pour un scénario similaire à l’aide de HDInsight Hadoop de clusters pour le traitement des données, consultez [équipe processus de science des données - à l’aide de Clusters Hadoop HDInsight Azure sur un jeu de données de 1 to](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="17cd9-106">For a walkthrough that shows how toohandle a larger (1 terabyte) dataset for a similar scenario using HDInsight Hadoop clusters for data processing, see [Team Data Science Process - Using Azure HDInsight Hadoop Clusters on a 1 TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span></span>

<span data-ttu-id="17cd9-107">Il est également possible toouse un hello tooaccomplish du bloc-notes notebooks tâches procédure pas à pas hello présenté à l’aide du jeu de données de 1 to hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-107">It is also possible toouse an IPython notebook tooaccomplish hello tasks presented hello walkthrough using hello 1 TB dataset.</span></span> <span data-ttu-id="17cd9-108">Les utilisateurs qui seraient comme tootry cette approche doit consulter hello [procédure pas à pas Criteo à l’aide d’une connexion ODBC de la ruche](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) rubrique.</span><span class="sxs-lookup"><span data-stu-id="17cd9-108">Users who would like tootry this approach should consult hello [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="17cd9-109"><a name="dataset"></a>Description du jeu de données NYC Taxi Trips</span><span class="sxs-lookup"><span data-stu-id="17cd9-109"><a name="dataset"></a>NYC Taxi Trips Dataset description</span></span>
<span data-ttu-id="17cd9-110">Hello les données NYC Taxi voyage est d’environ 20 Go de fichiers de valeurs compressées séparées par des virgules (CSV) (non compressé en ~ 48 Go), qui comprend plus de 173 millions hello et des boucles tarifs payé pour chaque sortie.</span><span class="sxs-lookup"><span data-stu-id="17cd9-110">hello NYC Taxi Trip data is about 20GB of compressed comma-separated values (CSV) files (~48GB uncompressed), comprising more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="17cd9-111">Chaque enregistrement de voyage comprend hello collecte et remise l’emplacement et l’heure, hack rendues anonymes (pilote) numéro de licence et nombre de medallion (id unique de taxi).</span><span class="sxs-lookup"><span data-stu-id="17cd9-111">Each trip record includes hello pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="17cd9-112">les données de salutation couvre toutes les boucles dans l’année hello 2013 et sont fournies dans hello suivant deux jeux de données pour chaque mois :</span><span class="sxs-lookup"><span data-stu-id="17cd9-112">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="17cd9-113">les fichiers CSV Hello 'trip_data' contiennent des détails de voyage, telles que le nombre de personnes, collecte et cette chute points, durée de voyage, longueur de voyage.</span><span class="sxs-lookup"><span data-stu-id="17cd9-113">hello 'trip_data' CSV files contain trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="17cd9-114">Voici quelques exemples d’enregistrements :</span><span class="sxs-lookup"><span data-stu-id="17cd9-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="17cd9-115">fichiers de Hello 'trip_fare' CSV contenant les détails de tarif de hello payé pour chaque sortie, comme type de paiement, montant de frais, surcharge et taxes, conseils et péage et montant total de hello payé.</span><span class="sxs-lookup"><span data-stu-id="17cd9-115">hello 'trip_fare' CSV files contain details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="17cd9-116">Voici quelques exemples d’enregistrements :</span><span class="sxs-lookup"><span data-stu-id="17cd9-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="17cd9-117">voyage toojoin de clé unique de Hello\_données et voyage\_tarif est composée de champs de hello : medallion, hack\_certificat et pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="17cd9-117">hello unique key toojoin trip\_data and trip\_fare is composed of hello fields: medallion, hack\_licence and pickup\_datetime.</span></span>

<span data-ttu-id="17cd9-118">tooget tous les voyage particulier hello détails tooa pertinentes, il est suffisant toojoin avec trois clés : hello « medallion », « hack\_licence » et « pickup\_datetime ».</span><span class="sxs-lookup"><span data-stu-id="17cd9-118">tooget all of hello details relevant tooa particular trip, it is sufficient toojoin with three keys: hello "medallion", "hack\_license" and "pickup\_datetime".</span></span>

<span data-ttu-id="17cd9-119">Nous décrivons certains plus d’informations sur les données de salutation lorsque nous les stocker dans les tables de la ruche peu de temps.</span><span class="sxs-lookup"><span data-stu-id="17cd9-119">We describe some more details of hello data when we store them into Hive tables shortly.</span></span>

## <span data-ttu-id="17cd9-120"><a name="mltasks"></a>Exemples de tâches de prédiction</span><span class="sxs-lookup"><span data-stu-id="17cd9-120"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="17cd9-121">Lors de l’approche des données, détermination de type hello de prédictions que vous souhaitez toomake en fonction de son analyse permet de clarifier les tâches hello que vous devez tooinclude dans votre processus.</span><span class="sxs-lookup"><span data-stu-id="17cd9-121">When approaching data, determining hello kind of predictions you want toomake based on its analysis helps clarify hello tasks that you will need tooinclude in your process.</span></span>
<span data-ttu-id="17cd9-122">Voici trois exemples de problèmes de prédiction qui nous adresse dans cette procédure pas à pas dont formulation repose sur hello *Conseil\_quantité*:</span><span class="sxs-lookup"><span data-stu-id="17cd9-122">Here are three examples of prediction problems that we address in this walkthrough whose formulation is based on hello *tip\_amount*:</span></span>

1. <span data-ttu-id="17cd9-123">**Classification binaire** : prédire si un pourboire a ou non été versé pour une course ; autrement dit, une valeur *tip\_amount* supérieure à 0 $ constitue un exemple positif, alors qu’une *valeur tip\_amount* de 0 $ est un exemple négatif.</span><span class="sxs-lookup"><span data-stu-id="17cd9-123">**Binary classification**: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. <span data-ttu-id="17cd9-124">**Classification multiclasse**: plage de hello toopredict des montants de conseil payé pour le voyage de hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-124">**Multiclass classification**: toopredict hello range of tip amounts paid for hello trip.</span></span> <span data-ttu-id="17cd9-125">Nous allons diviser hello *Conseil\_quantité* dans les cinq conteneurs ou les classes :</span><span class="sxs-lookup"><span data-stu-id="17cd9-125">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="17cd9-126">**Tâche de régression**: toopredict hello d’info-bulle hello montant d’un voyage.</span><span class="sxs-lookup"><span data-stu-id="17cd9-126">**Regression task**: toopredict hello amount of hello tip paid for a trip.</span></span>  

## <span data-ttu-id="17cd9-127"><a name="setup"></a>Configuration d’un cluster Hadoop HDInsight pour une analyse avancée</span><span class="sxs-lookup"><span data-stu-id="17cd9-127"><a name="setup"></a>Set up an HDInsight Hadoop cluster for advanced analytics</span></span>
> [!NOTE]
> <span data-ttu-id="17cd9-128">Il s'agit généralement d’une tâche d’ **administration** .</span><span class="sxs-lookup"><span data-stu-id="17cd9-128">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="17cd9-129">Vous pouvez configurer un environnement Azure pour une analyse avancée qui utilise un cluster HDInsight en trois étapes :</span><span class="sxs-lookup"><span data-stu-id="17cd9-129">You can set up an Azure environment for advanced analytics that employs an HDInsight cluster in three steps:</span></span>

1. <span data-ttu-id="17cd9-130">[Création d’un compte de stockage](../storage/common/storage-create-storage-account.md): ce compte de stockage est utilisé pour stocker des données dans un stockage Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="17cd9-130">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used for storing data in Azure Blob Storage.</span></span> <span data-ttu-id="17cd9-131">données Hello utilisées dans les clusters HDInsight se trouvent également ici.</span><span class="sxs-lookup"><span data-stu-id="17cd9-131">hello data used in HDInsight clusters also resides here.</span></span>
2. <span data-ttu-id="17cd9-132">[Personnaliser Azure HDInsight Hadoop avancé des processus Analytique et la technologie des clusters pour hello](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="17cd9-132">[Customize Azure HDInsight Hadoop clusters for hello Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md).</span></span> <span data-ttu-id="17cd9-133">Cette étape crée un cluster Hadoop Azure HDInsight avec Anaconda Python 2.7 64 bits installé sur tous les nœuds.</span><span class="sxs-lookup"><span data-stu-id="17cd9-133">This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="17cd9-134">Il existe deux étapes importantes tooremember lors de la personnalisation de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="17cd9-134">There are two important steps tooremember while customizing your HDInsight cluster.</span></span>
   
   * <span data-ttu-id="17cd9-135">N’oubliez pas de compte de stockage hello toolink créé à l’étape 1 avec votre cluster HDInsight lors de sa création.</span><span class="sxs-lookup"><span data-stu-id="17cd9-135">Remember toolink hello storage account created in step 1 with your HDInsight cluster when creating it.</span></span> <span data-ttu-id="17cd9-136">Ce compte de stockage donnée tooaccess utilisé est traitée dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-136">This storage account is used tooaccess data that is processed within hello cluster.</span></span>
   * <span data-ttu-id="17cd9-137">Après la création de cluster de hello, activez l’accès à distance toohello nœud de tête hello cluster.</span><span class="sxs-lookup"><span data-stu-id="17cd9-137">After hello cluster is created, enable Remote Access toohello head node of hello cluster.</span></span> <span data-ttu-id="17cd9-138">Accédez toohello **Configuration** onglet et cliquez sur **activer distant**.</span><span class="sxs-lookup"><span data-stu-id="17cd9-138">Navigate toohello **Configuration** tab and click **Enable Remote**.</span></span> <span data-ttu-id="17cd9-139">Cette étape spécifie les informations d’identification de l’utilisateur hello utilisées pour la connexion à distance.</span><span class="sxs-lookup"><span data-stu-id="17cd9-139">This step specifies hello user credentials used for remote login.</span></span>
3. <span data-ttu-id="17cd9-140">[Créer un espace de travail Azure Machine Learning](machine-learning-create-workspace.md): ce Azure Machine Learning espace de travail est utilisé toobuild apprentissage des modèles.</span><span class="sxs-lookup"><span data-stu-id="17cd9-140">[Create an Azure Machine Learning workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used toobuild machine learning models.</span></span> <span data-ttu-id="17cd9-141">Cette tâche est résolue après avoir effectué une exploration de données initiales et vers le bas d’échantillonnage à l’aide du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-141">This task is addressed after completing an initial data exploration and down sampling using hello HDInsight cluster.</span></span>

## <span data-ttu-id="17cd9-142"><a name="getdata"></a>Obtenir des données de hello à partir d’une source publique</span><span class="sxs-lookup"><span data-stu-id="17cd9-142"><a name="getdata"></a>Get hello data from a public source</span></span>
> [!NOTE]
> <span data-ttu-id="17cd9-143">Il s'agit généralement d’une tâche d’ **administration** .</span><span class="sxs-lookup"><span data-stu-id="17cd9-143">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="17cd9-144">tooget hello [NYC Taxi allers-retours](http://www.andresmh.com/nyctaxitrips/) dataset à partir de son emplacement public, vous pouvez utiliser une des méthodes hello décrites dans [tooand de déplacer les données à partir du stockage d’objets Blob Azure](machine-learning-data-science-move-azure-blob.md) machine de tooyour données toocopy hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-144">tooget hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of hello methods described in [Move Data tooand from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy hello data tooyour machine.</span></span>

<span data-ttu-id="17cd9-145">L’exemple suivant décrit comment utiliser AzCopy tootransfer hello fichiers contenant des données.</span><span class="sxs-lookup"><span data-stu-id="17cd9-145">Here we describe how use AzCopy tootransfer hello files containing data.</span></span> <span data-ttu-id="17cd9-146">toodownload et installer AzCopy suivent les instructions de hello à [prise en main de l’utilitaire de ligne de commande AzCopy de hello](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="17cd9-146">toodownload and install AzCopy follow hello instructions at [Getting Started with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

1. <span data-ttu-id="17cd9-147">À partir d’une fenêtre d’invite de commandes, exécutez hello suivant de commandes AzCopy, en remplaçant *< path_to_data_folder >* avec la destination souhaitée de hello :</span><span class="sxs-lookup"><span data-stu-id="17cd9-147">From a Command Prompt window, issue hello following AzCopy commands, replacing *<path_to_data_folder>* with hello desired destination:</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. <span data-ttu-id="17cd9-148">Lors de la copie de hello est terminée, un total de fichiers compressés 24 sont dans le dossier de données hello choisi.</span><span class="sxs-lookup"><span data-stu-id="17cd9-148">When hello copy completes, a total of 24 zipped files are in hello data folder chosen.</span></span> <span data-ttu-id="17cd9-149">Décompressez hello téléchargé les fichiers toohello même répertoire sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="17cd9-149">Unzip hello downloaded files toohello same directory on your local machine.</span></span> <span data-ttu-id="17cd9-150">Prenez note du dossier hello où résident les fichiers de hello non compressé.</span><span class="sxs-lookup"><span data-stu-id="17cd9-150">Make a note of hello folder where hello uncompressed files reside.</span></span> <span data-ttu-id="17cd9-151">Ce dossier sera référencé tooas hello *< chemin d’accès\_à\_unzipped_data\_fichiers\>*  est ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="17cd9-151">This folder will be referred tooas hello *<path\_to\_unzipped_data\_files\>* is what follows.</span></span>

## <span data-ttu-id="17cd9-152"><a name="upload"></a>Télécharger le conteneur de hello données toohello par défaut du cluster Azure HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="17cd9-152"><a name="upload"></a>Upload hello data toohello default container of Azure HDInsight Hadoop cluster</span></span>
> [!NOTE]
> <span data-ttu-id="17cd9-153">Il s'agit généralement d’une tâche d’ **administration** .</span><span class="sxs-lookup"><span data-stu-id="17cd9-153">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="17cd9-154">Bonjour les commandes AzCopy suivantes, remplacez hello paramètres avec les valeurs réelles hello que vous avez spécifié lors de la création de cluster Hadoop de hello suivants et la décompression des fichiers de données hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-154">In hello following AzCopy commands, replace hello following parameters with hello actual values that you specified when creating hello Hadoop cluster and unzipping hello data files.</span></span>

* <span data-ttu-id="17cd9-155">***&#60; path_to_data_folder >*** directory hello (ainsi que le chemin d’accès) sur votre ordinateur qui contiennent les fichiers de données hello décompressé</span><span class="sxs-lookup"><span data-stu-id="17cd9-155">***&#60;path_to_data_folder>*** hello directory (along with path) on your machine that contain hello unzipped data files</span></span>  
* <span data-ttu-id="17cd9-156">***&#60; le nom de compte de stockage de cluster Hadoop >*** hello compte de stockage associé à votre cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="17cd9-156">***&#60;storage account name of Hadoop cluster>*** hello storage account associated with your HDInsight cluster</span></span>
* <span data-ttu-id="17cd9-157">***&#60; le conteneur par défaut du cluster Hadoop >*** conteneur par défaut de hello utilisé par votre cluster.</span><span class="sxs-lookup"><span data-stu-id="17cd9-157">***&#60;default container of Hadoop cluster>*** hello default container used by your cluster.</span></span> <span data-ttu-id="17cd9-158">Notez ce nom hello de valeur par défaut hello conteneur est généralement hello même nom en tant que cluster hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="17cd9-158">Note that hello name of hello default container is usually hello same name as hello cluster itself.</span></span> <span data-ttu-id="17cd9-159">Par exemple, si le cluster de hello est appelée « abc123.azurehdinsight.net », le conteneur par défaut de hello est abc123.</span><span class="sxs-lookup"><span data-stu-id="17cd9-159">For example, if hello cluster is called "abc123.azurehdinsight.net", hello default container is abc123.</span></span>
* <span data-ttu-id="17cd9-160">***&#60; clé de compte de stockage >*** hello clé hello compte de stockage utilisé par votre cluster</span><span class="sxs-lookup"><span data-stu-id="17cd9-160">***&#60;storage account key>*** hello key for hello storage account used by your cluster</span></span>

<span data-ttu-id="17cd9-161">À partir d’une invite de commandes ou une fenêtre Windows PowerShell sur votre ordinateur, exécutez hello suivant deux commandes AzCopy.</span><span class="sxs-lookup"><span data-stu-id="17cd9-161">From a Command Prompt or a Windows PowerShell window in your machine, run hello following two AzCopy commands.</span></span>

<span data-ttu-id="17cd9-162">Cette commande télécharge les données de voyage hello trop***nyctaxitripraw*** répertoire dans un conteneur par défaut hello de cluster Hadoop de hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-162">This command uploads hello trip data too***nyctaxitripraw*** directory in hello default container of hello Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

<span data-ttu-id="17cd9-163">Cette commande télécharge les données de prix hello trop***nyctaxifareraw*** répertoire dans un conteneur par défaut hello de cluster Hadoop de hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-163">This command uploads hello fare data too***nyctaxifareraw*** directory in hello default container of hello Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

<span data-ttu-id="17cd9-164">les données de salutation doivent être présent dans le stockage d’objets Blob Azure et prêt toobe consommés au sein du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-164">hello data should now in Azure Blob Storage and ready toobe consumed within hello HDInsight cluster.</span></span>

## <span data-ttu-id="17cd9-165"><a name="#download-hql-files"></a>Ouvrez une session sur le nœud principal de hello de cluster Hadoop et et le préparer pour l’analyse exploratoire des données</span><span class="sxs-lookup"><span data-stu-id="17cd9-165"><a name="#download-hql-files"></a>Log into hello head node of Hadoop cluster and and prepare for exploratory data analysis</span></span>
> [!NOTE]
> <span data-ttu-id="17cd9-166">Il s'agit généralement d’une tâche d’ **administration** .</span><span class="sxs-lookup"><span data-stu-id="17cd9-166">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="17cd9-167">tooaccess hello nœud de tête hello cluster pour l’analyse exploratoire des données et d’arrêt d’échantillonnage des données de hello, suivez la procédure hello dans [hello d’accès nœud principal de Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="17cd9-167">tooaccess hello head node of hello cluster for exploratory data analysis and down sampling of hello data, follow hello procedure outlined in [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

<span data-ttu-id="17cd9-168">Dans cette procédure pas à pas, nous utilisons principalement les requêtes écrites [Hive](https://hive.apache.org/), un langage de requête de type SQL, des explorations de données préliminaires tooperform.</span><span class="sxs-lookup"><span data-stu-id="17cd9-168">In this walkthrough, we primarily use queries written in [Hive](https://hive.apache.org/), a SQL-like query language, tooperform preliminary data explorations.</span></span> <span data-ttu-id="17cd9-169">les requêtes Hive Hello sont stockés dans les fichiers .hql.</span><span class="sxs-lookup"><span data-stu-id="17cd9-169">hello Hive queries are stored in .hql files.</span></span> <span data-ttu-id="17cd9-170">Nous avons ensuite vers le bas les exemples de cette toobe de données utilisé dans Azure Machine Learning pour générer des modèles.</span><span class="sxs-lookup"><span data-stu-id="17cd9-170">We then down sample this data toobe used within Azure Machine Learning for building models.</span></span>

<span data-ttu-id="17cd9-171">cluster de hello tooprepare pour l’analyse exploratoire des données, nous télécharger hello .hql contenant des scripts Hive pertinentes hello à partir de [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa répertoire local (C:\temp) sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-171">tooprepare hello cluster for exploratory data analysis, we download hello .hql files containing hello relevant Hive scripts from [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa local directory (C:\temp) on hello head node.</span></span> <span data-ttu-id="17cd9-172">toodo, ouvrez hello **invite de commandes** depuis hello nœud principal de hello hello cluster et le problème suivant les deux commandes :</span><span class="sxs-lookup"><span data-stu-id="17cd9-172">toodo this, open hello **Command Prompt** from within hello head node of hello cluster and issue hello following two commands:</span></span>

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

<span data-ttu-id="17cd9-173">Ces deux commandes télécharge tous les fichiers .hql nécessaires dans ce répertoire local de procédure pas à pas toohello ***C:\temp &#92;*** dans le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-173">These two commands will download all .hql files needed in this walkthrough toohello local directory ***C:\temp&#92;*** in hello head node.</span></span>

## <span data-ttu-id="17cd9-174"><a name="#hive-db-tables"></a>Créer la base de données Hive et les tables partitionnées par mois</span><span class="sxs-lookup"><span data-stu-id="17cd9-174"><a name="#hive-db-tables"></a>Create Hive database and tables partitioned by month</span></span>
> [!NOTE]
> <span data-ttu-id="17cd9-175">Il s'agit généralement d’une tâche d’ **administration** .</span><span class="sxs-lookup"><span data-stu-id="17cd9-175">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="17cd9-176">Nous sommes maintenant toocreate prêt ruche tables pour notre jeu de données taxi NYC.</span><span class="sxs-lookup"><span data-stu-id="17cd9-176">We are now ready toocreate Hive tables for our NYC taxi dataset.</span></span>
<span data-ttu-id="17cd9-177">Dans le nœud principal de hello du cluster Hadoop de hello, ouvrez hello ***ligne de commande Hadoop*** hello bureau du nœud principal de hello et entrez le répertoire de ruche hello en entrant la commande hello</span><span class="sxs-lookup"><span data-stu-id="17cd9-177">In hello head node of hello Hadoop cluster, open hello ***Hadoop Command Line*** on hello desktop of hello head node, and enter hello Hive directory by entering hello command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="17cd9-178">**Exécuter toutes les commandes de la ruche dans cette procédure pas à pas de hello ci-dessus ruche bin / invite du répertoire. Il se chargera automatiquement de tout problème lié au chemin d'accès. Nous utilisons hello termes « Invite du répertoire ruche », « ruche bin / invite du répertoire » et « ligne de commande Hadoop « indifféremment dans cette procédure pas à pas.**</span><span class="sxs-lookup"><span data-stu-id="17cd9-178">**Run all Hive commands in this walkthrough from hello above Hive bin/ directory prompt. This will take care of any path issues automatically. We use hello terms "Hive directory prompt", "Hive bin/ directory prompt",  and "Hadoop Command Line" interchangeably in this walkthrough.**</span></span>
> 
> 

<span data-ttu-id="17cd9-179">À partir de l’invite du répertoire hello Hive, entrez hello en ligne de commande Hadoop de tables et hello du nœud principal toosubmit hello ruche requête toocreate ruche de base de données de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="17cd9-179">From hello Hive directory prompt, enter hello following command in Hadoop Command Line of hello head node toosubmit hello Hive query toocreate Hive database and tables:</span></span>

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

<span data-ttu-id="17cd9-180">Voici le contenu de hello hello ***C:\temp\sample\_ruche\_créer\_db\_et\_tables.hql*** fichier qui crée la base de données de la ruche ***nyctaxidb *** et tables ***voyage*** et ***tarif***.</span><span class="sxs-lookup"><span data-stu-id="17cd9-180">Here is hello content of hello ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql*** file which creates Hive database ***nyctaxidb*** and tables ***trip*** and ***fare***.</span></span>

    create database if not exists nyctaxidb;

    create external table if not exists nyctaxidb.trip
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double)  
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');

    create external table if not exists nyctaxidb.fare
    (
        medallion string,
        hack_license string,
        vendor_id string,
        pickup_datetime string,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double)
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');

<span data-ttu-id="17cd9-181">Ce script Hive crée deux tables :</span><span class="sxs-lookup"><span data-stu-id="17cd9-181">This Hive script creates two tables:</span></span>

* <span data-ttu-id="17cd9-182">table de « voyage » Hello contient les détails de voyage de chaque cas (détails du pilote, heure d’extraction, la distance de déplacement et les heures)</span><span class="sxs-lookup"><span data-stu-id="17cd9-182">hello "trip" table contains trip details of each ride (driver details, pickup time, trip distance and times)</span></span>
* <span data-ttu-id="17cd9-183">table de « tarif » Hello contient les détails de prix (montant de frais, montant du Conseil, péage et surcharges).</span><span class="sxs-lookup"><span data-stu-id="17cd9-183">hello "fare" table contains fare details (fare amount, tip amount, tolls and surcharges).</span></span>

<span data-ttu-id="17cd9-184">Si vous avez besoin d’une assistance supplémentaire avec ces procédures ou que vous souhaitiez tooinvestigate autres possibles, consultez la section de hello [la ruche soumettre des requêtes directement à partir de ligne de commande Hadoop hello ](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="17cd9-184">If you need any additional assistance with these procedures or want tooinvestigate alternative ones, see hello section [Submit Hive queries directly from hello Hadoop Command Line ](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="17cd9-185"><a name="#load-data"></a>Charger les tables de données tooHive par partition</span><span class="sxs-lookup"><span data-stu-id="17cd9-185"><a name="#load-data"></a>Load Data tooHive tables by partitions</span></span>
> [!NOTE]
> <span data-ttu-id="17cd9-186">Il s'agit généralement d’une tâche d’ **administration** .</span><span class="sxs-lookup"><span data-stu-id="17cd9-186">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="17cd9-187">jeu de données Hello NYC taxi a un partitionnement naturel par mois, nous utilisons le temps de traitement et de requête plus rapides tooenable.</span><span class="sxs-lookup"><span data-stu-id="17cd9-187">hello NYC taxi dataset has a natural partitioning by month, which we use tooenable faster processing and query times.</span></span> <span data-ttu-id="17cd9-188">Hello des commandes PowerShell ci-dessous (émis à partir du répertoire de ruche hello à l’aide de hello **ligne de commande Hadoop**) charger les données toohello « voyage » et « tarif » ruche tables partitionnées par mois.</span><span class="sxs-lookup"><span data-stu-id="17cd9-188">hello PowerShell commands below (issued from hello Hive directory using hello **Hadoop Command Line**) load data toohello "trip" and "fare" Hive tables partitioned by month.</span></span>

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

<span data-ttu-id="17cd9-189">Hello *exemple\_ruche\_charger\_données\_par\_partitions.hql* fichier contient des éléments suivants de hello **charger** commandes.</span><span class="sxs-lookup"><span data-stu-id="17cd9-189">hello *sample\_hive\_load\_data\_by\_partitions.hql* file contains hello following **LOAD** commands.</span></span>

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

<span data-ttu-id="17cd9-190">Notez qu’un nombre de requêtes Hive que nous utilisons ici dans le processus d’exploration hello implique la recherche au qu’une seule partition ou à un nombre limité de partitions.</span><span class="sxs-lookup"><span data-stu-id="17cd9-190">Note that a number of Hive queries we use here in hello exploration process involve looking at just a single partition or at only a couple of partitions.</span></span> <span data-ttu-id="17cd9-191">Mais ces requêtes peut être exécutées sur les données hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-191">But these queries could be run across hello entire data.</span></span>

### <span data-ttu-id="17cd9-192"><a name="#show-db"></a>Afficher les bases de données dans le cluster HDInsight Hadoop de hello</span><span class="sxs-lookup"><span data-stu-id="17cd9-192"><a name="#show-db"></a>Show databases in hello HDInsight Hadoop cluster</span></span>
<span data-ttu-id="17cd9-193">bases de données de hello de tooshow créés dans le cluster HDInsight Hadoop dans la fenêtre de ligne de commande Hadoop hello, exécutez hello en ligne de commande Hadoop de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="17cd9-193">tooshow hello databases created in HDInsight Hadoop cluster inside hello Hadoop Command Line window, run hello following command in Hadoop Command Line:</span></span>

    hive -e "show databases;"

### <span data-ttu-id="17cd9-194"><a name="#show-tables"></a>Afficher les tables de ruche hello dans la base de données nyctaxidb hello</span><span class="sxs-lookup"><span data-stu-id="17cd9-194"><a name="#show-tables"></a>Show hello Hive tables in hello nyctaxidb database</span></span>
<span data-ttu-id="17cd9-195">tables hello tooshow hello nyctaxidb base de données, exécutez hello en ligne de commande Hadoop de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="17cd9-195">tooshow hello tables in hello nyctaxidb database, run hello following command in Hadoop Command Line:</span></span>

    hive -e "show tables in nyctaxidb;"

<span data-ttu-id="17cd9-196">Nous pouvons vérifier que les tables de hello sont partitionnées en émettant la commande hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="17cd9-196">We can confirm that hello tables are partitioned by issuing hello command below:</span></span>

    hive -e "show partitions nyctaxidb.trip;"

<span data-ttu-id="17cd9-197">Hello attendu la sortie est illustrée ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="17cd9-197">hello expected output is shown below:</span></span>

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 2.075 seconds, Fetched: 12 row(s)

<span data-ttu-id="17cd9-198">De même, nous pouvons vérifier que hello tarif la table est partitionnée en émettant la commande hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="17cd9-198">Similarly, we can ensure that hello fare table is partitioned by issuing hello command below:</span></span>

    hive -e "show partitions nyctaxidb.fare;"

<span data-ttu-id="17cd9-199">Hello attendu la sortie est illustrée ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="17cd9-199">hello expected output is shown below:</span></span>

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 1.887 seconds, Fetched: 12 row(s)

## <span data-ttu-id="17cd9-200"><a name="#explore-hive"></a>Exploration des données et ingénierie des fonctionnalités dans Hive</span><span class="sxs-lookup"><span data-stu-id="17cd9-200"><a name="#explore-hive"></a>Data exploration and feature engineering in Hive</span></span>
> [!NOTE]
> <span data-ttu-id="17cd9-201">Il s'agit généralement d’une tâche de **données scientifiques** .</span><span class="sxs-lookup"><span data-stu-id="17cd9-201">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="17cd9-202">Hello d’exploration de données et d’une fonctionnalité de tâches d’ingénierie pour hello données chargées dans des tables de ruche hello est possible à l’aide de requêtes Hive.</span><span class="sxs-lookup"><span data-stu-id="17cd9-202">hello data exploration and feature engineering tasks for hello data loaded into hello Hive tables can be accomplished using Hive queries.</span></span> <span data-ttu-id="17cd9-203">Voici des exemples de ces tâches que nous vous décrivons dans cette section :</span><span class="sxs-lookup"><span data-stu-id="17cd9-203">Here are examples of such tasks that we walk you through in this section:</span></span>

* <span data-ttu-id="17cd9-204">Afficher les 10 principaux hello dans les deux tables.</span><span class="sxs-lookup"><span data-stu-id="17cd9-204">View hello top 10 records in both tables.</span></span>
* <span data-ttu-id="17cd9-205">Explorer les distributions de données de quelques champs portant sur différentes périodes.</span><span class="sxs-lookup"><span data-stu-id="17cd9-205">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="17cd9-206">Analyser la qualité des données des champs de longitude et de latitude hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-206">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="17cd9-207">Générer des étiquettes de classification binaire et multiclasse selon hello **Conseil\_quantité**.</span><span class="sxs-lookup"><span data-stu-id="17cd9-207">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="17cd9-208">Générer des fonctionnalités en calculant des distances de voyage direct hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-208">Generate features by computing hello direct trip distances.</span></span>

### <a name="exploration-view-hello-top-10-records-in-table-trip"></a><span data-ttu-id="17cd9-209">Exploration : Vue hello top 10 enregistrements voyage de table</span><span class="sxs-lookup"><span data-stu-id="17cd9-209">Exploration: View hello top 10 records in table trip</span></span>
> [!NOTE]
> <span data-ttu-id="17cd9-210">Il s'agit généralement d’une tâche de **données scientifiques** .</span><span class="sxs-lookup"><span data-stu-id="17cd9-210">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="17cd9-211">toosee quelles données hello ressemble, nous allons examiner 10 enregistrements de chaque table.</span><span class="sxs-lookup"><span data-stu-id="17cd9-211">toosee what hello data looks like, we examine 10 records from each table.</span></span> <span data-ttu-id="17cd9-212">Exécutez hello suivant séparément les deux requêtes à partir de l’invite du répertoire ruche hello dans les enregistrements hello tooinspect hello ligne de commande Hadoop console.</span><span class="sxs-lookup"><span data-stu-id="17cd9-212">Run hello following two queries separately from hello Hive directory prompt in hello Hadoop Command Line console tooinspect hello records.</span></span>

<span data-ttu-id="17cd9-213">tooget hello top 10 enregistrements dans la table de hello « voyage » à partir du premier mois de hello :</span><span class="sxs-lookup"><span data-stu-id="17cd9-213">tooget hello top 10 records in hello table "trip" from hello first month:</span></span>

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

<span data-ttu-id="17cd9-214">tooget hello top 10 enregistrements dans la table de hello « tarif » à partir du premier mois de hello :</span><span class="sxs-lookup"><span data-stu-id="17cd9-214">tooget hello top 10 records in hello table "fare" from hello first month:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

<span data-ttu-id="17cd9-215">Il est souvent utile toosave hello enregistrements tooa fichier pour l’affichage pratique.</span><span class="sxs-lookup"><span data-stu-id="17cd9-215">It is often useful toosave hello records tooa file for convenient viewing.</span></span> <span data-ttu-id="17cd9-216">Un toohello petite modification au-dessus de requête effectue cela :</span><span class="sxs-lookup"><span data-stu-id="17cd9-216">A small change toohello above query accomplishes this:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-hello-number-of-records-in-each-of-hello-12-partitions"></a><span data-ttu-id="17cd9-217">Exploration : Afficher hello le nombre d’enregistrements dans chacune des partitions de 12 hello</span><span class="sxs-lookup"><span data-stu-id="17cd9-217">Exploration: View hello number of records in each of hello 12 partitions</span></span>
> [!NOTE]
> <span data-ttu-id="17cd9-218">Il s'agit généralement d’une tâche de **données scientifiques** .</span><span class="sxs-lookup"><span data-stu-id="17cd9-218">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="17cd9-219">D’intérêt est hello comment nombre hello de déplacements varie au cours de l’année civile de hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-219">Of interest is hello how hello number of trips varies during hello calendar year.</span></span> <span data-ttu-id="17cd9-220">Regroupement par mois nous permet de toosee l’aspect de cette distribution d’allers-retours.</span><span class="sxs-lookup"><span data-stu-id="17cd9-220">Grouping by month allows us toosee what this distribution of trips looks like.</span></span>

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

<span data-ttu-id="17cd9-221">Cela nous donne la sortie de hello :</span><span class="sxs-lookup"><span data-stu-id="17cd9-221">This gives us hello output :</span></span>

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 283.406 seconds, Fetched: 12 row(s)

<span data-ttu-id="17cd9-222">Ici, hello première colonne est mois de hello et hello deuxième hello nombre de boucles pour ce mois.</span><span class="sxs-lookup"><span data-stu-id="17cd9-222">Here, hello first column is hello month and hello second is hello number of trips for that month.</span></span>

<span data-ttu-id="17cd9-223">Nous pouvons également nombre hello total d’enregistrements dans notre jeu de données de voyage en émettant hello commande à l’invite de répertoire hello Hive suivante.</span><span class="sxs-lookup"><span data-stu-id="17cd9-223">We can also count hello total number of records in our trip data set by issuing hello following command at hello Hive directory prompt.</span></span>

    hive -e "select count(*) from nyctaxidb.trip;"

<span data-ttu-id="17cd9-224">Cela donne :</span><span class="sxs-lookup"><span data-stu-id="17cd9-224">This yields:</span></span>

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

<span data-ttu-id="17cd9-225">À l’aide des commandes similaires toothose est indiqué pour le jeu de données de voyage hello, nous pouvons émettre des requêtes Hive à partir de l’invite du répertoire ruche hello pour hello tarif jeu de données toovalidate hello nombre d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="17cd9-225">Using commands similar toothose shown for hello trip data set, we can issue Hive queries from hello Hive directory prompt for hello fare data set toovalidate hello number of records.</span></span>

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

<span data-ttu-id="17cd9-226">Cela nous donne la sortie de hello :</span><span class="sxs-lookup"><span data-stu-id="17cd9-226">This gives us hello output:</span></span>

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 253.955 seconds, Fetched: 12 row(s)

<span data-ttu-id="17cd9-227">Notez que hello exacte même nombre de boucles par mois est retournée pour les deux jeux de données.</span><span class="sxs-lookup"><span data-stu-id="17cd9-227">Note that hello exact same number of trips per month is returned for both data sets.</span></span> <span data-ttu-id="17cd9-228">Cela fournit la validation de première de hello que hello données a été chargées correctement.</span><span class="sxs-lookup"><span data-stu-id="17cd9-228">This provides hello first validation that hello data has been loaded correctly.</span></span>

<span data-ttu-id="17cd9-229">Calcul hello le nombre total d’enregistrements dans le jeu de données de prix hello peut être effectuée à l’aide de la commande hello ci-dessous à partir de l’invite du répertoire hello Hive :</span><span class="sxs-lookup"><span data-stu-id="17cd9-229">Counting hello total number of records in hello fare data set can be done using hello command below from hello Hive directory prompt:</span></span>

    hive -e "select count(*) from nyctaxidb.fare;"

<span data-ttu-id="17cd9-230">Cela donne :</span><span class="sxs-lookup"><span data-stu-id="17cd9-230">This yields :</span></span>

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

<span data-ttu-id="17cd9-231">Nombre total de Hello d’enregistrements dans les deux tables est également hello même.</span><span class="sxs-lookup"><span data-stu-id="17cd9-231">hello total number of records in both tables is also hello same.</span></span> <span data-ttu-id="17cd9-232">Cela fournit une validation de seconde que hello données a été chargées correctement.</span><span class="sxs-lookup"><span data-stu-id="17cd9-232">This provides a second validation that hello data has been loaded correctly.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="17cd9-233">Exploration : distribution des courses par médaillon</span><span class="sxs-lookup"><span data-stu-id="17cd9-233">Exploration: Trip distribution by medallion</span></span>
> [!NOTE]
> <span data-ttu-id="17cd9-234">Il s'agit généralement d’une tâche de **données scientifiques** .</span><span class="sxs-lookup"><span data-stu-id="17cd9-234">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="17cd9-235">Cet exemple identifie le medallion hello (numéros taxi) avec plus de 100 allers-retours pendant une période donnée.</span><span class="sxs-lookup"><span data-stu-id="17cd9-235">This example identifies hello medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="17cd9-236">avantages de requête Hello de hello partitionnée accès à la table, car il est conditionnée par la variable de partition hello **mois**.</span><span class="sxs-lookup"><span data-stu-id="17cd9-236">hello query benefits from hello partitioned table access since it is conditioned by hello partition variable **month**.</span></span> <span data-ttu-id="17cd9-237">résultats de la requête Hello écrites tooa fichier local queryoutput.tsv dans `C:\temp` sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-237">hello query results are written tooa local file queryoutput.tsv in `C:\temp` on hello head node.</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="17cd9-238">Voici le contenu de hello *exemple\_ruche\_voyage\_nombre\_par\_medallion.hql* fichier pour inspection.</span><span class="sxs-lookup"><span data-stu-id="17cd9-238">Here is hello content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="17cd9-239">medallion Hello dans le jeu de données hello NYC taxi identifie un fichier cab unique.</span><span class="sxs-lookup"><span data-stu-id="17cd9-239">hello medallion in hello NYC taxi data set identifies a unique cab.</span></span> <span data-ttu-id="17cd9-240">Nous pouvons identifier les taxis « occupés » en demandant quels taxis ont effectué plus d'un certain nombre d'allers-retours sur une période donnée.</span><span class="sxs-lookup"><span data-stu-id="17cd9-240">We can identify which cabs are "busy" by asking which ones made more than a certain number of trips in a particular time period.</span></span> <span data-ttu-id="17cd9-241">Hello exemple suivant identifie les fichiers CAB de plus de cent allers-retours dans hello trois premiers mois et enregistre hello requête résultats tooa fichier local C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="17cd9-241">hello following example identifies cabs that made more than a hundred trips in hello first three months, and saves hello query results tooa local file, C:\temp\queryoutput.tsv.</span></span>

<span data-ttu-id="17cd9-242">Voici le contenu de hello *exemple\_ruche\_voyage\_nombre\_par\_medallion.hql* fichier pour inspection.</span><span class="sxs-lookup"><span data-stu-id="17cd9-242">Here is hello content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="17cd9-243">À partir de hello ruche invite active, commande hello de problème ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="17cd9-243">From hello Hive directory prompt, issue hello command below :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="17cd9-244">Exploration : distribution des courses par médaillon et par licence de taxi</span><span class="sxs-lookup"><span data-stu-id="17cd9-244">Exploration: Trip distribution by medallion and hack_license</span></span>
> [!NOTE]
> <span data-ttu-id="17cd9-245">Il s'agit généralement d’une tâche de **données scientifiques** .</span><span class="sxs-lookup"><span data-stu-id="17cd9-245">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="17cd9-246">Lorsque vous explorez un jeu de données, nous souhaitons fréquemment le nombre de hello tooexamine de co-occurrences des groupes de valeurs.</span><span class="sxs-lookup"><span data-stu-id="17cd9-246">When exploring a dataset, we frequently want tooexamine hello number of co-occurences of groups of values.</span></span> <span data-ttu-id="17cd9-247">Cette section fournit un exemple de comment toodo pour des fichiers CAB et de pilotes.</span><span class="sxs-lookup"><span data-stu-id="17cd9-247">This section provide an example of how toodo this for cabs and drivers.</span></span>

<span data-ttu-id="17cd9-248">Hello *exemple\_ruche\_voyage\_nombre\_par\_medallion\_license.hql* les données de prix hello défini sur « medallion » et « hack_license » des groupes de fichiers et le nombre de retours de chaque combinaison.</span><span class="sxs-lookup"><span data-stu-id="17cd9-248">hello *sample\_hive\_trip\_count\_by\_medallion\_license.hql* file groups hello fare data set on "medallion" and "hack_license" and returns counts of each combination.</span></span> <span data-ttu-id="17cd9-249">Son contenu est présenté ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="17cd9-249">Below are its contents.</span></span>

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

<span data-ttu-id="17cd9-250">Cette requête renvoie les combinaisons de taxi et de chauffeur particulier classées par ordre décroissant de courses.</span><span class="sxs-lookup"><span data-stu-id="17cd9-250">This query returns cab and particular driver combinations ordered by descending number of trips.</span></span>

<span data-ttu-id="17cd9-251">À partir de hello Hive invite du répertoire, exécutez :</span><span class="sxs-lookup"><span data-stu-id="17cd9-251">From hello Hive directory prompt, run :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="17cd9-252">résultats de la requête Hello sont écrites tooa de fichier local C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="17cd9-252">hello query results are written tooa local file C:\temp\queryoutput.tsv.</span></span>

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a><span data-ttu-id="17cd9-253">Exploration : évaluation de la qualité des données en recherchant les enregistrements de longitude et de latitude non valides</span><span class="sxs-lookup"><span data-stu-id="17cd9-253">Exploration: Assessing data quality by checking for invalid longitude/latitude records</span></span>
> [!NOTE]
> <span data-ttu-id="17cd9-254">Il s'agit généralement d’une tâche de **données scientifiques** .</span><span class="sxs-lookup"><span data-stu-id="17cd9-254">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="17cd9-255">Une analyse exploratoire des données communes vise tooweed des enregistrements non valides ou incorrects.</span><span class="sxs-lookup"><span data-stu-id="17cd9-255">A common objective of exploratory data analysis is tooweed out invalid or bad records.</span></span> <span data-ttu-id="17cd9-256">Hello exemple dans cette section détermine si soit hello longitude ou latitude champs contiennent une valeur en dehors de zone de NYC de hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-256">hello example in this section determines whether either hello longitude or latitude fields contain a value far outside hello NYC area.</span></span> <span data-ttu-id="17cd9-257">Dans la mesure où il est probable que ces enregistrements ont un valeurs erronées de latitude de longitude, nous souhaitons tooeliminate à partir des données toobe utilisés pour la modélisation.</span><span class="sxs-lookup"><span data-stu-id="17cd9-257">Since it is likely that such records have an erroneous longitude-latitude values, we want tooeliminate them from any data that is toobe used for modeling.</span></span>

<span data-ttu-id="17cd9-258">Voici le contenu de hello *exemple\_ruche\_qualité\_assessment.hql* fichier pour inspection.</span><span class="sxs-lookup"><span data-stu-id="17cd9-258">Here is hello content of *sample\_hive\_quality\_assessment.hql* file for inspection.</span></span>

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


<span data-ttu-id="17cd9-259">À partir de hello Hive invite du répertoire, exécutez :</span><span class="sxs-lookup"><span data-stu-id="17cd9-259">From hello Hive directory prompt, run :</span></span>

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

<span data-ttu-id="17cd9-260">Hello *-S* argument inclus dans cette commande supprime l’impression d’écran de statut hello des tâches de mappage/réduction Hive hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-260">hello *-S* argument included in this command suppresses hello status screen printout of hello Hive Map/Reduce jobs.</span></span> <span data-ttu-id="17cd9-261">Cela est utile, car elle permet d’impression d’écran hello Hello Hive le résultat de la requête plus lisible.</span><span class="sxs-lookup"><span data-stu-id="17cd9-261">This is useful because it makes hello screen print of hello Hive query output more readable.</span></span>

### <a name="exploration-binary-class-distributions-of-trip-tips"></a><span data-ttu-id="17cd9-262">Exploration : distributions de classe binaire des pourboires de course</span><span class="sxs-lookup"><span data-stu-id="17cd9-262">Exploration: Binary class distributions of trip tips</span></span>
> [!NOTE]
> <span data-ttu-id="17cd9-263">Il s'agit généralement d’une tâche de **données scientifiques** .</span><span class="sxs-lookup"><span data-stu-id="17cd9-263">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="17cd9-264">Problème de classification binaire hello décrites dans hello [des exemples de tâches de prédiction](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section, il est utile tooknow si une info-bulle a été spécifiée ou non.</span><span class="sxs-lookup"><span data-stu-id="17cd9-264">For hello binary classification problem outlined in hello [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section, it is useful tooknow whether a tip was given or not.</span></span> <span data-ttu-id="17cd9-265">Cette distribution de pourboires est binaire :</span><span class="sxs-lookup"><span data-stu-id="17cd9-265">This distribution of tips is binary:</span></span>

* <span data-ttu-id="17cd9-266">pourboire donné (classe 1, tip\_amount > 0 $)</span><span class="sxs-lookup"><span data-stu-id="17cd9-266">tip given(Class 1, tip\_amount > $0)</span></span>  
* <span data-ttu-id="17cd9-267">Aucun pourboire (classe 0, tip\_amount = 0 $).</span><span class="sxs-lookup"><span data-stu-id="17cd9-267">no tip (Class 0, tip\_amount = $0).</span></span>

<span data-ttu-id="17cd9-268">Hello *exemple\_ruche\_incliné\_frequencies.hql* fichier ci-dessous effectue cette opération.</span><span class="sxs-lookup"><span data-stu-id="17cd9-268">hello *sample\_hive\_tipped\_frequencies.hql* file shown below does this.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

<span data-ttu-id="17cd9-269">À partir de hello Hive invite du répertoire, exécutez :</span><span class="sxs-lookup"><span data-stu-id="17cd9-269">From hello Hive directory prompt, run:</span></span>

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-hello-multiclass-setting"></a><span data-ttu-id="17cd9-270">Exploration : Classe distributions dans le paramètre multiclasse de hello</span><span class="sxs-lookup"><span data-stu-id="17cd9-270">Exploration: Class distributions in hello multiclass setting</span></span>
> [!NOTE]
> <span data-ttu-id="17cd9-271">Il s'agit généralement d’une tâche de **données scientifiques** .</span><span class="sxs-lookup"><span data-stu-id="17cd9-271">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="17cd9-272">Problème de classification multiclasse hello décrites dans hello [des exemples de tâches de prédiction](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section ce jeu de données se prête également tooa classification naturel où nous souhaiterions durée hello toopredict conseils hello donné.</span><span class="sxs-lookup"><span data-stu-id="17cd9-272">For hello multiclass classification problem outlined in hello [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section this data set also lends itself tooa natural classification where we would like toopredict hello amount of hello tips given.</span></span> <span data-ttu-id="17cd9-273">Nous pouvons utiliser des plages de conseil toodefine emplacements dans la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-273">We can use bins toodefine tip ranges in hello query.</span></span> <span data-ttu-id="17cd9-274">tooget hello distributions de classe pour hello diverses plages de Conseil, nous utilisons hello *exemple\_ruche\_Conseil\_plage\_frequencies.hql* fichier.</span><span class="sxs-lookup"><span data-stu-id="17cd9-274">tooget hello class distributions for hello various tip ranges, we use hello *sample\_hive\_tip\_range\_frequencies.hql* file.</span></span> <span data-ttu-id="17cd9-275">Son contenu est présenté ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="17cd9-275">Below are its contents.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount=0, 0,
            if(tip_amount>0 and tip_amount<=5, 1,
            if(tip_amount>5 and tip_amount<=10, 2,
            if(tip_amount>10 and tip_amount<=20, 3, 4)))) as tip_class, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tip_class;

<span data-ttu-id="17cd9-276">Exécutez hello de commande suivante à partir de la console de ligne de commande Hadoop :</span><span class="sxs-lookup"><span data-stu-id="17cd9-276">Run hello following command from Hadoop Command Line console:</span></span>

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a><span data-ttu-id="17cd9-277">Exploration : calculer la distance directe entre deux emplacements de latitude-longitude</span><span class="sxs-lookup"><span data-stu-id="17cd9-277">Exploration: Compute Direct Distance Between Two Longitude-Latitude Locations</span></span>
> [!NOTE]
> <span data-ttu-id="17cd9-278">Il s'agit généralement d’une tâche de **données scientifiques** .</span><span class="sxs-lookup"><span data-stu-id="17cd9-278">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="17cd9-279">Ayant une mesure de distance directe de hello permet toofind out des différences entre eux et hello hello réel déclenchement distance.</span><span class="sxs-lookup"><span data-stu-id="17cd9-279">Having a measure of hello direct distance allows us toofind out hello discrepancy between it and hello actual trip distance.</span></span> <span data-ttu-id="17cd9-280">Nous motiver cette fonctionnalité en expliquant que passager peut être inférieur info-bulle probable si elles déterminer ce pilote hello a intentionnellement les pris par voie bien plus longue.</span><span class="sxs-lookup"><span data-stu-id="17cd9-280">We motivate this feature by pointing out that a passenger might be less likely tootip if they figure out that hello driver has intentionally taken them by a much longer route.</span></span>

<span data-ttu-id="17cd9-281">comparaison de hello toosee entre la distance de voyage réelle et hello [distance Haversine](http://en.wikipedia.org/wiki/Haversine_formula) entre deux points de latitude de longitude (« circle great » à distance hello), nous utilisons hello des fonctions trigonométriques disponibles au sein de la ruche, par conséquent :</span><span class="sxs-lookup"><span data-stu-id="17cd9-281">toosee hello comparison between actual trip distance and hello [Haversine distance](http://en.wikipedia.org/wiki/Haversine_formula) between two longitude-latitude points (hello "great circle" distance), we use hello trigonometric functions available within Hive, thus :</span></span>

    set R=3959;
    set pi=radians(180);

    insert overwrite directory 'wasb:///queryoutputdir'

    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
    ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
     *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
     *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
     /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
     +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
     pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
    from nyctaxidb.trip
    where month=1
    and pickup_longitude between -90 and -30
    and pickup_latitude between 30 and 90
    and dropoff_longitude between -90 and -30
    and dropoff_latitude between 30 and 90;

<span data-ttu-id="17cd9-282">Dans la requête de hello ci-dessus, R est rayon hello hello terre en miles et pi est tooradians converti.</span><span class="sxs-lookup"><span data-stu-id="17cd9-282">In hello query above, R is hello radius of hello Earth in miles, and pi is converted tooradians.</span></span> <span data-ttu-id="17cd9-283">Notez que les points de latitude de longitude hello sont les valeurs « filtré » tooremove loin d’être zone NYC de hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-283">Note that hello longitude-latitude points are "filtered" tooremove values that are far from hello NYC area.</span></span>

<span data-ttu-id="17cd9-284">Dans ce cas, nous écrivons notre répertoire tooa de résultats appelée « queryoutputdir ».</span><span class="sxs-lookup"><span data-stu-id="17cd9-284">In this case, we write our results tooa directory called "queryoutputdir".</span></span> <span data-ttu-id="17cd9-285">séquence Hello des commandes ci-dessous crée d’abord ce répertoire de sortie, puis exécute la commande de ruche hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-285">hello sequence of commands shown below first creates this output directory, and then runs hello Hive command.</span></span>

<span data-ttu-id="17cd9-286">À partir de hello Hive invite du répertoire, exécutez :</span><span class="sxs-lookup"><span data-stu-id="17cd9-286">From hello Hive directory prompt, run:</span></span>

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


<span data-ttu-id="17cd9-287">Hello résultats de la requête sont écrits les objets BLOB Azure de too9 ***queryoutputdir/000000\_0*** trop ***queryoutputdir/000008\_0*** sous le conteneur par défaut de hello du cluster Hadoop de hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-287">hello query results are written too9 Azure blobs ***queryoutputdir/000000\_0*** too ***queryoutputdir/000008\_0*** under hello default container of hello Hadoop cluster.</span></span>

<span data-ttu-id="17cd9-288">taille de hello toosee d’objets BLOB individuels de hello, nous exécutons hello de commande suivante à partir de l’invite du répertoire hello Hive :</span><span class="sxs-lookup"><span data-stu-id="17cd9-288">toosee hello size of hello individual blobs, we run hello following command from hello Hive directory prompt :</span></span>

    hdfs dfs -ls wasb:///queryoutputdir

<span data-ttu-id="17cd9-289">contenu de hello toosee d’un fichier donné, par exemple 000000\_0, nous utilisons de Hadoop `copyToLocal` commande ainsi.</span><span class="sxs-lookup"><span data-stu-id="17cd9-289">toosee hello contents of a given file, say 000000\_0, we use Hadoop's `copyToLocal` command, thus.</span></span>

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> <span data-ttu-id="17cd9-290">`copyToLocal` peut être très lent pour les fichiers volumineux et n’est pas recommandé pour une utilisation avec ceux-ci.</span><span class="sxs-lookup"><span data-stu-id="17cd9-290">`copyToLocal` can be very slow for large files, and is not recommended for use with them.</span></span>  
> 
> 

<span data-ttu-id="17cd9-291">Le principal avantage d’avoir ces données résident dans un objet blob Azure est que nous pouvons Explorer les données hello dans Azure Machine Learning à l’aide de hello [importer des données] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="17cd9-291">A key advantage of having this data reside in an Azure blob is that we may explore hello data within Azure Machine Learning using hello [Import Data][import-data] module.</span></span>

## <span data-ttu-id="17cd9-292"><a name="#downsample"></a>Réduire l’échantillon des données et créer des modèles dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="17cd9-292"><a name="#downsample"></a>Down sample data and build models in Azure Machine Learning</span></span>
> [!NOTE]
> <span data-ttu-id="17cd9-293">Il s'agit généralement d’une tâche de **données scientifiques** .</span><span class="sxs-lookup"><span data-stu-id="17cd9-293">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="17cd9-294">Après la phase d’analyse hello analyse exploratoire des données, vous voilà prêt toodown exemples de données hello pour générer des modèles dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="17cd9-294">After hello exploratory data analysis phase, we are now ready toodown sample hello data for building models in Azure Machine Learning.</span></span> <span data-ttu-id="17cd9-295">Dans cette section, nous montrons comment toouse une ruche interroger toodown exemple hello de données, qui sont ensuite accessible à partir de hello [importer des données] [ import-data] module dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="17cd9-295">In this section, we show how toouse a Hive query toodown sample hello data, which is then accessed from hello [Import Data][import-data] module in Azure Machine Learning.</span></span>

### <a name="down-sampling-hello-data"></a><span data-ttu-id="17cd9-296">Vers le bas de l’échantillonnage des données de hello</span><span class="sxs-lookup"><span data-stu-id="17cd9-296">Down sampling hello data</span></span>
<span data-ttu-id="17cd9-297">Il existe deux étapes dans cette procédure.</span><span class="sxs-lookup"><span data-stu-id="17cd9-297">There are two steps in this procedure.</span></span> <span data-ttu-id="17cd9-298">Tout d’abord, nous joindre hello **nyctaxidb.trip** et **nyctaxidb.fare** tables sur trois clés qui sont présents dans tous les enregistrements : « medallion », « hack\_licence », et « pickup\_datetime ».</span><span class="sxs-lookup"><span data-stu-id="17cd9-298">First we join hello **nyctaxidb.trip** and **nyctaxidb.fare** tables on three keys that are present in all records : "medallion", "hack\_license", and "pickup\_datetime".</span></span> <span data-ttu-id="17cd9-299">Nous générons ensuite une étiquette de classification binaire **avec pourboire** et une étiquette de classification multiclasse **tip\_class**.</span><span class="sxs-lookup"><span data-stu-id="17cd9-299">We then generate a binary classification label **tipped** and a multi-class classification label **tip\_class**.</span></span>

<span data-ttu-id="17cd9-300">hello toouse en mesure de toobe vers le bas des données échantillonnées directement à partir de hello [importer des données] [ import-data] module dans Azure Machine Learning, il est nécessaire toostore les résultats de hello Hello au-dessus de table de requête tooan interne Hive.</span><span class="sxs-lookup"><span data-stu-id="17cd9-300">toobe able toouse hello down sampled data directly from hello [Import Data][import-data] module in Azure Machine Learning, it is necessary toostore hello results of hello above query tooan internal Hive table.</span></span> <span data-ttu-id="17cd9-301">Dans ce qui suit, nous créer une table interne de la ruche et remplir son contenu par hello joint et vers le bas les données échantillonnées.</span><span class="sxs-lookup"><span data-stu-id="17cd9-301">In what follows, we create an internal Hive table and populate its contents with hello joined and down sampled data.</span></span>

<span data-ttu-id="17cd9-302">Hello requête s’applique des fonctions de ruche standard directement toogenerate hello heure, la semaine de l’année, la semaine (1 signifie lundi et 7 stands pour dimanche) de hello « pickup\_datetime » champ et hello distance directe entre la collecte de hello et cette chute emplacements.</span><span class="sxs-lookup"><span data-stu-id="17cd9-302">hello query applies standard Hive functions directly toogenerate hello hour of day, week of year, weekday (1 stands for Monday, and 7 stands for Sunday) from hello "pickup\_datetime" field,  and hello direct distance between hello pickup and dropoff locations.</span></span> <span data-ttu-id="17cd9-303">Les utilisateurs peuvent faire référence trop[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) pour une liste complète de ces fonctions.</span><span class="sxs-lookup"><span data-stu-id="17cd9-303">Users can refer too[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) for a complete list of such functions.</span></span>

<span data-ttu-id="17cd9-304">Hello requête, puis vers le bas des données de salutation exemples afin que les résultats de la requête hello s’adaptent à hello Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="17cd9-304">hello query then down samples hello data so that hello query results can fit into hello Azure Machine Learning Studio.</span></span> <span data-ttu-id="17cd9-305">Uniquement 1 % du jeu de données d’origine hello est importé dans hello Studio.</span><span class="sxs-lookup"><span data-stu-id="17cd9-305">Only about 1% of hello original dataset is imported into hello Studio.</span></span>

<span data-ttu-id="17cd9-306">Voici le contenu de hello de *exemple\_ruche\_préparer\_pour\_agréés\_full.hql* fichier qui prépare les données pour le modèle de génération dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="17cd9-306">Below are hello contents of *sample\_hive\_prepare\_for\_aml\_full.hql* file that prepares data for model building in Azure Machine Learning.</span></span>

        set R = 3959;
        set pi=radians(180);

        create table if not exists nyctaxidb.nyctaxi_downsampled_dataset (

        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\n'
        stored as textfile;

        --- now insert contents of hello join into hello above internal table

        insert overwrite table nyctaxidb.nyctaxi_downsampled_dataset
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class

        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
        *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
        +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance,
        rand() as sample_key

        from nyctaxidb.trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from nyctaxidb.fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01

<span data-ttu-id="17cd9-307">toorun cette requête, à partir du répertoire de ruche hello invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="17cd9-307">toorun this query, from hello Hive directory prompt :</span></span>

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

<span data-ttu-id="17cd9-308">Nous avons maintenant une table interne « nyctaxidb.nyctaxi_downsampled_dataset », qui est accessible à l’aide de hello [importer des données] [ import-data] module à partir d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="17cd9-308">We now have an internal table "nyctaxidb.nyctaxi_downsampled_dataset" which can be accessed using hello [Import Data][import-data] module from Azure Machine Learning.</span></span> <span data-ttu-id="17cd9-309">En outre, nous pouvons utiliser ce jeu de données pour générer des modèles d'apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="17cd9-309">Furthermore, we may use this dataset for building Machine Learning models.</span></span>  

### <a name="use-hello-import-data-module-in-azure-machine-learning-tooaccess-hello-down-sampled-data"></a><span data-ttu-id="17cd9-310">Utiliser le module d’importer des données de hello Bonjour de tooaccess Azure Machine Learning vers le bas les données échantillonnées</span><span class="sxs-lookup"><span data-stu-id="17cd9-310">Use hello Import Data module in Azure Machine Learning tooaccess hello down sampled data</span></span>
<span data-ttu-id="17cd9-311">Comme les composants requis pour l’émission de requêtes Hive dans hello [importer des données] [ import-data] module d’Azure Machine Learning, nous devons accéder à l’espace de travail de tooan Azure Machine Learning et accéder aux informations d’identification toohello Hello cluster et son compte de stockage associé.</span><span class="sxs-lookup"><span data-stu-id="17cd9-311">As prerequisites for issuing Hive queries in hello [Import Data][import-data] module of Azure Machine Learning, we need access tooan Azure Machine Learning workspace and access toohello credentials of hello cluster and its associated storage account.</span></span>

<span data-ttu-id="17cd9-312">Certains détails sur hello [importer des données] [ import-data] tooinput de paramètres de module et hello :</span><span class="sxs-lookup"><span data-stu-id="17cd9-312">Some details on hello [Import Data][import-data] module and hello parameters tooinput :</span></span>

<span data-ttu-id="17cd9-313">**URI du serveur HCatalog**: si le nom du cluster hello est abc123, alors il s’agit simplement : https://abc123.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="17cd9-313">**HCatalog server URI**: If hello cluster name is abc123, then this is simply : https://abc123.azurehdinsight.net</span></span>

<span data-ttu-id="17cd9-314">**Nom du compte utilisateur Hadoop** : nom d’utilisateur hello choisi pour le cluster de hello (**pas** nom d’utilisateur l’accès à distance hello)</span><span class="sxs-lookup"><span data-stu-id="17cd9-314">**Hadoop user account name** : hello user name chosen for hello cluster (**not** hello remote access user name)</span></span>

<span data-ttu-id="17cd9-315">**Mot de passe de compte Hadoop ser** : mot de passe hello choisi pour le cluster de hello (**pas** mot de passe de l’accès à distance hello)</span><span class="sxs-lookup"><span data-stu-id="17cd9-315">**Hadoop ser account password** : hello password chosen for hello cluster (**not** hello remote access password)</span></span>

<span data-ttu-id="17cd9-316">**Emplacement des données de sortie** : cela est choisi toobe Azure.</span><span class="sxs-lookup"><span data-stu-id="17cd9-316">**Location of output data** : This is chosen toobe Azure.</span></span>

<span data-ttu-id="17cd9-317">**Nom de compte de stockage Azure** : nom du compte de stockage par défaut hello associé hello cluster.</span><span class="sxs-lookup"><span data-stu-id="17cd9-317">**Azure storage account name** : Name of hello default storage account associated with hello cluster.</span></span>

<span data-ttu-id="17cd9-318">**Nom du conteneur Azure** : cela est le nom de conteneur par défaut hello pour le cluster de hello et est généralement identique hello en tant que nom de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-318">**Azure container name** : This is hello default container name for hello cluster, and is typically hello same as hello cluster name.</span></span> <span data-ttu-id="17cd9-319">Pour un cluster appelé « abc123 », il s'agit simplement d’abc123.</span><span class="sxs-lookup"><span data-stu-id="17cd9-319">For a cluster called "abc123", this is just abc123.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="17cd9-320">**N’importe quelle table que nous souhaitons tooquery à l’aide de hello [importer des données] [ import-data] module dans Azure Machine Learning doit être une table interne.**</span><span class="sxs-lookup"><span data-stu-id="17cd9-320">**Any table we wish tooquery using hello [Import Data][import-data] module in Azure Machine Learning must be an internal table.**</span></span> <span data-ttu-id="17cd9-321">Voici un conseil pour déterminer si une table T dans une base de données D.db est une table interne.</span><span class="sxs-lookup"><span data-stu-id="17cd9-321">A tip for determining if a table T in a database D.db is an internal table is as follows.</span></span>
> 
> 

<span data-ttu-id="17cd9-322">À partir de hello ruche invite active, problème hello commande :</span><span class="sxs-lookup"><span data-stu-id="17cd9-322">From hello Hive directory prompt, issue hello command :</span></span>

    hdfs dfs -ls wasb:///D.db/T

<span data-ttu-id="17cd9-323">Si la table de hello est une table interne et il est rempli, son contenu doit afficher ici.</span><span class="sxs-lookup"><span data-stu-id="17cd9-323">If hello table is an internal table and it is populated, its contents must show here.</span></span> <span data-ttu-id="17cd9-324">Une autre façon toodetermine si une table est une table interne est toouse hello Explorateur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="17cd9-324">Another way toodetermine whether a table is an internal table is toouse hello Azure Storage Explorer.</span></span> <span data-ttu-id="17cd9-325">Utiliser le nom de conteneur par défaut toonavigate toohello du cluster de hello et filtrer par nom de table hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-325">Use it toonavigate toohello default container name of hello cluster, and then filter by hello table name.</span></span> <span data-ttu-id="17cd9-326">Si la table de hello et son contenu s’affiche, cela confirme qu’il est une table interne.</span><span class="sxs-lookup"><span data-stu-id="17cd9-326">If hello table and its contents show up, this confirms that it is an internal table.</span></span>

<span data-ttu-id="17cd9-327">Voici une capture instantanée de la requête Hive de hello et hello [importer des données] [ import-data] module :</span><span class="sxs-lookup"><span data-stu-id="17cd9-327">Here is a snapshot of hello Hive query and hello [Import Data][import-data] module:</span></span>

![Requête Hive pour le module Importer des données](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

<span data-ttu-id="17cd9-329">Notez que depuis notre vers le bas les données échantillonnées résident dans le conteneur de hello par défaut, les requêtes Hive résultant hello à partir d’Azure Machine Learning est très simple est simplement un « sélectionner * à partir de nyctaxidb.nyctaxi\_sous-échantillonnées\_données ».</span><span class="sxs-lookup"><span data-stu-id="17cd9-329">Note that since our down sampled data resides in hello default container, hello resulting Hive query from Azure Machine Learning is very simple and is just a "SELECT * FROM nyctaxidb.nyctaxi\_downsampled\_data".</span></span>

<span data-ttu-id="17cd9-330">Hello dataset peut maintenant être utilisé comme point de départ pour créer des modèles d’apprentissage de hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-330">hello dataset may now be used as hello starting point for building Machine Learning models.</span></span>

### <span data-ttu-id="17cd9-331"><a name="mlmodel"></a>Créer des modèles dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="17cd9-331"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="17cd9-332">Nous sommes en mesure de tooproceed toomodel génération et déploiement de modèle dans [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="17cd9-332">We are now able tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="17cd9-333">les données de salutation sont prêtes pour nous toouse dans la résolution des problèmes de prédiction hello identifiés ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="17cd9-333">hello data is ready for us toouse in addressing hello prediction problems identified above:</span></span>

<span data-ttu-id="17cd9-334">**1. Classification binaire**: toopredict ou non un Conseil a été payé un voyage.</span><span class="sxs-lookup"><span data-stu-id="17cd9-334">**1. Binary classification**: toopredict whether or not a tip was paid for a trip.</span></span>

<span data-ttu-id="17cd9-335">**Apprenant utilisé :** régression logistique à deux classes</span><span class="sxs-lookup"><span data-stu-id="17cd9-335">**Learner used:** Two-class logistic regression</span></span>

<span data-ttu-id="17cd9-336">a.</span><span class="sxs-lookup"><span data-stu-id="17cd9-336">a.</span></span> <span data-ttu-id="17cd9-337">Pour ce problème, notre étiquette (ou classe) cible est « avec pourboire ».</span><span class="sxs-lookup"><span data-stu-id="17cd9-337">For this problem, our target (or class) label is "tipped".</span></span> <span data-ttu-id="17cd9-338">Notre jeu de données original à l’échantillon réduit dispose de quelques colonnes qui sont des fuites cibles pour cette expérience de classification.</span><span class="sxs-lookup"><span data-stu-id="17cd9-338">Our original down-sampled dataset has a few columns that are target leaks for this classification experiment.</span></span> <span data-ttu-id="17cd9-339">En particulier : Conseil\_de classe, le Conseil\_montant et total\_montant révéler des informations sur l’étiquette cible hello qui n’est pas disponible sur le temps de test.</span><span class="sxs-lookup"><span data-stu-id="17cd9-339">In particular : tip\_class, tip\_amount, and total\_amount reveal information about hello target label that is not available at testing time.</span></span> <span data-ttu-id="17cd9-340">Nous supprimer ces colonnes de compte à l’aide de hello [sélectionner les colonnes dans le jeu de données] [ select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="17cd9-340">We remove these columns from consideration using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="17cd9-341">instantané Hello ci-dessous montre toopredict de notre expérience ou non un Conseil a été payé pour une sortie donnée.</span><span class="sxs-lookup"><span data-stu-id="17cd9-341">hello snapshot below shows our experiment toopredict whether or not a tip was paid for a given trip.</span></span>

![Instantané de l’expérience](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

<span data-ttu-id="17cd9-343">b.</span><span class="sxs-lookup"><span data-stu-id="17cd9-343">b.</span></span> <span data-ttu-id="17cd9-344">Pour cette expérience, nos distributions d'étiquette cible ont été d’environ 1:1.</span><span class="sxs-lookup"><span data-stu-id="17cd9-344">For this experiment, our target label distributions were roughly 1:1.</span></span>

<span data-ttu-id="17cd9-345">instantané Hello ci-dessous montre la répartition hello étiquettes de classe de Conseil pour le problème de classification binaire hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-345">hello snapshot below shows hello distribution of tip class labels for hello binary classification problem.</span></span>

![Distribution d'étiquettes de classe de pourboire](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

<span data-ttu-id="17cd9-347">Par conséquent, nous obtenons une AUC de 0.987 comme indiqué dans la figure ci-dessous hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-347">As a result, we obtain an AUC of 0.987 as shown in hello figure below.</span></span>

![Valeur ASC](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

<span data-ttu-id="17cd9-349">**2. Classification multiclasse**: classes définies par la plage de hello toopredict des montants de conseil payé pour le voyage hello, à l’aide de hello précédemment.</span><span class="sxs-lookup"><span data-stu-id="17cd9-349">**2. Multiclass classification**: toopredict hello range of tip amounts paid for hello trip, using hello previously defined classes.</span></span>

<span data-ttu-id="17cd9-350">**Apprenant utilisé :** régression logistique multiclasse</span><span class="sxs-lookup"><span data-stu-id="17cd9-350">**Learner used:** Multiclass logistic regression</span></span>

<span data-ttu-id="17cd9-351">a.</span><span class="sxs-lookup"><span data-stu-id="17cd9-351">a.</span></span> <span data-ttu-id="17cd9-352">Pour ce problème, notre cible (ou classe) est « tip\_class », ce qui peut prendre une des cinq valeurs suivantes (0,1,2,3,4).</span><span class="sxs-lookup"><span data-stu-id="17cd9-352">For this problem, our target (or class) label is "tip\_class" which can take one of five values (0,1,2,3,4).</span></span> <span data-ttu-id="17cd9-353">Comme dans les cas de classification binaire hello, nous avons quelques colonnes qui sont des fuites de cible pour cette expérience.</span><span class="sxs-lookup"><span data-stu-id="17cd9-353">As in hello binary classification case, we have a few columns that are target leaks for this experiment.</span></span> <span data-ttu-id="17cd9-354">En particulier : pourboires, Conseil\_montant total\_montant révéler des informations sur l’étiquette cible hello qui n’est pas disponible sur le temps de test.</span><span class="sxs-lookup"><span data-stu-id="17cd9-354">In particular : tipped, tip\_amount, total\_amount reveal information about hello target label that is not available at testing time.</span></span> <span data-ttu-id="17cd9-355">Nous supprimer ces colonnes à l’aide de hello [sélectionner les colonnes dans le jeu de données] [ select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="17cd9-355">We remove these columns using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="17cd9-356">Hello instantané ci-dessous illustre notre toopredict expérience emplacement dans lequel une info-bulle est probablement toofall (classe 0 : Conseil = 0 $, classe 1 : Conseil > $0 et info-bulle < = 5 $, classe 2 : Conseil > $5 et Conseil < = $10, 3 de la classe : Conseil > $10 et Conseil < = 20 Classe 4 : Conseil > 20)</span><span class="sxs-lookup"><span data-stu-id="17cd9-356">hello snapshot below shows our experiment toopredict in which bin a tip is likely toofall ( Class 0: tip = $0, class 1 : tip > $0 and tip <= $5, Class 2 : tip > $5 and tip <= $10, Class 3 : tip > $10 and tip <= $20, Class 4 : tip > $20)</span></span>

![Instantané de l’expérience](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

<span data-ttu-id="17cd9-358">Nous montrons maintenant à quoi ressemble notre distribution de classe test réelle.</span><span class="sxs-lookup"><span data-stu-id="17cd9-358">We now show what our actual test class distribution looks like.</span></span> <span data-ttu-id="17cd9-359">Nous constatons que lors de la classe 0 et 1 de la classe sont les plus fréquentes, hello d’autres classes sont rares.</span><span class="sxs-lookup"><span data-stu-id="17cd9-359">We see that while Class 0 and Class 1 are prevalent, hello other classes are rare.</span></span>

![Distribution de classe de test](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

<span data-ttu-id="17cd9-361">b.</span><span class="sxs-lookup"><span data-stu-id="17cd9-361">b.</span></span> <span data-ttu-id="17cd9-362">Pour cette expérience, nous utilisons un toolook de matrice de confusion à notre précisions de prédiction.</span><span class="sxs-lookup"><span data-stu-id="17cd9-362">For this experiment, we use a confusion matrix toolook at our prediction accuracies.</span></span> <span data-ttu-id="17cd9-363">Consultez l’illustration ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="17cd9-363">This is shown below.</span></span>

![Matrice de confusion](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

<span data-ttu-id="17cd9-365">Notez que lors de notre précisions de classe sur les classes de largement répandue hello est assez bonne, modèle de hello n’effectue pas un bon de travail de « apprentissage » sur les classes de plus rares hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-365">Note that while our class accuracies on hello prevalent classes is quite good, hello model does not do a good job of "learning" on hello rarer classes.</span></span>

<span data-ttu-id="17cd9-366">**3. Tâche de régression**: toopredict hello d’info-bulle montant d’un voyage.</span><span class="sxs-lookup"><span data-stu-id="17cd9-366">**3. Regression task**: toopredict hello amount of tip paid for a trip.</span></span>

<span data-ttu-id="17cd9-367">**Apprenant utilisé :** arbre de décision optimisé</span><span class="sxs-lookup"><span data-stu-id="17cd9-367">**Learner used:** Boosted decision tree</span></span>

<span data-ttu-id="17cd9-368">a.</span><span class="sxs-lookup"><span data-stu-id="17cd9-368">a.</span></span> <span data-ttu-id="17cd9-369">Pour ce problème, notre étiquette (ou classe) cible est « tip\_amount ».</span><span class="sxs-lookup"><span data-stu-id="17cd9-369">For this problem, our target (or class) label is "tip\_amount".</span></span> <span data-ttu-id="17cd9-370">Fuites de notre cible sont dans ce cas : pourboires, Conseil\_(classe), total\_quantité ; toutes ces variables révèlent des informations sur la quantité de Conseil de hello est généralement pas disponible sur le temps de test.</span><span class="sxs-lookup"><span data-stu-id="17cd9-370">Our target leaks in this case are : tipped, tip\_class, total\_amount ; all these variables reveal information about hello tip amount that is typically unavailable at testing time.</span></span> <span data-ttu-id="17cd9-371">Nous supprimer ces colonnes à l’aide de hello [sélectionner les colonnes dans le jeu de données] [ select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="17cd9-371">We remove these columns using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="17cd9-372">Hello instantané belows illustre notre expérience toopredict hello hello donné d’info-bulle.</span><span class="sxs-lookup"><span data-stu-id="17cd9-372">hello snapshot belows shows our experiment toopredict hello amount of hello given tip.</span></span>

![Instantané de l’expérience](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

<span data-ttu-id="17cd9-374">b.</span><span class="sxs-lookup"><span data-stu-id="17cd9-374">b.</span></span> <span data-ttu-id="17cd9-375">Pour les problèmes de régression, nous précisions hello de notre prédiction de mesures en examinant erreur hello carré dans les prédictions de hello hello coefficient de détermination et hello comme.</span><span class="sxs-lookup"><span data-stu-id="17cd9-375">For regression problems, we measure hello accuracies of our prediction by looking at hello squared error in hello predictions, hello coefficient of determination, and hello like.</span></span> <span data-ttu-id="17cd9-376">Nous présentons ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="17cd9-376">We show these below.</span></span>

![Statistiques de prédiction](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

<span data-ttu-id="17cd9-378">Nous voyons que sur hello coefficient de détermination est 0.709, ce qui implique d’environ 71 % de la variance de hello est expliqué par notre coefficients du modèle.</span><span class="sxs-lookup"><span data-stu-id="17cd9-378">We see that about hello coefficient of determination is 0.709, implying about 71% of hello variance is explained by our model coefficients.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="17cd9-379">toolearn plus d’informations sur Azure Machine Learning et comment tooaccess et l’utiliser, consultez trop[What ' s apprentissage ?](machine-learning-what-is-machine-learning.md).</span><span class="sxs-lookup"><span data-stu-id="17cd9-379">toolearn more about Azure Machine Learning and how tooaccess and use it, please refer too[What's Machine Learning?](machine-learning-what-is-machine-learning.md).</span></span> <span data-ttu-id="17cd9-380">Une ressource très utile pour la lecture avec un ensemble d’expériences d’apprentissage sur Azure Machine Learning est hello [Cortana Intelligence galerie](https://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="17cd9-380">A very useful resource for playing with a bunch of Machine Learning experiments on Azure Machine Learning is hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).</span></span> <span data-ttu-id="17cd9-381">Galerie de Hello couvre une gamme d’expériences et fournit une présentation détaillée dans la plage hello des fonctionnalités d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="17cd9-381">hello Gallery covers a gamut of experiments and provides a thorough introduction into hello range of capabilities of Azure Machine Learning.</span></span>
> 
> 

## <a name="license-information"></a><span data-ttu-id="17cd9-382">Informations de licence</span><span class="sxs-lookup"><span data-stu-id="17cd9-382">License Information</span></span>
<span data-ttu-id="17cd9-383">Cet exemple de procédure et les scripts qui l’accompagne sont partagées par Microsoft sous licence du MIT hello.</span><span class="sxs-lookup"><span data-stu-id="17cd9-383">This sample walkthrough and its accompanying scripts are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="17cd9-384">Vérifiez fichier hello le répertoire hello hello exemple de code sur GitHub pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="17cd9-384">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="17cd9-385">Références</span><span class="sxs-lookup"><span data-stu-id="17cd9-385">References</span></span>
<span data-ttu-id="17cd9-386">•    [Page de téléchargement des jeux de données NYC Taxi Trips par Andrés Monroy (en anglais)](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="17cd9-386">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="17cd9-387">•    [Page de partage des données relatives aux courses en taxi new-yorkais par Chris Whong (en anglais)](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="17cd9-387">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="17cd9-388">•    [Page de recherche et de statistiques de la Commission des services de taxis et de limousines de la ville de New York (en anglais)](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="17cd9-388">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
