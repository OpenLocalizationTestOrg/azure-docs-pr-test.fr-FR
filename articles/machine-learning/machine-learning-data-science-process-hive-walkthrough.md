---
title: "Explorer les données dans un cluster Hadoop et créer des modèles dans Azure Machine Learning | Microsoft Docs"
description: "Utilisation du processus TDSP (Team Data Science Process) pour un scénario de bout en bout employant un cluster Hadoop HDInsight pour créer et déployer un modèle à l'aide d'un groupe de données disponible publiquement."
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
ms.openlocfilehash: e48d59ca467e3e7fd772389e6e48a2d81726f859
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a><span data-ttu-id="28646-103">Processus TDSP (Team Data Science Process) en action : utiliser des clusters Hadoop Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="28646-103">The Team Data Science Process in action: Use Azure HDInsight Hadoop clusters</span></span>
<span data-ttu-id="28646-104">Dans cette procédure pas à pas, nous allons utiliser le [processus TDSP (Team Data Science Process)](data-science-process-overview.md) avec un scénario complet au moyen d’un [cluster Azure Hadoop HDInsight](https://azure.microsoft.com/services/hdinsight/) pour effectuer des opérations sur le jeu de données [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) disponible publiquement, telles que le stockage, l’exploration, la conception de fonctionnalités et la réduction de l’échantillon de données.</span><span class="sxs-lookup"><span data-stu-id="28646-104">In this walkthrough, we use the [Team Data Science Process (TDSP)](data-science-process-overview.md) in an end-to-end scenario using an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore and feature engineer data from the publicly available [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset, and to down sample the data.</span></span> <span data-ttu-id="28646-105">Les modèles de données sont créés avec Azure Machine Learning pour gérer les tâches prédictives de classification et de régression binaires et multiclasses.</span><span class="sxs-lookup"><span data-stu-id="28646-105">Models of the data are built with Azure Machine Learning to handle binary and multiclass classification and regression predictive tasks.</span></span>

<span data-ttu-id="28646-106">Pour une procédure pas à pas qui montre comment gérer un jeu de données plus grand (1 téraoctet) avec un scénario similaire à l’aide de clusters Hadoop HDInsight pour le traitement des données, consultez [Processus TDSP (Team Data Science Process) : utilisation des clusters Hadoop Azure HDInsight sur un jeu de données de 1 To](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="28646-106">For a walkthrough that shows how to handle a larger (1 terabyte) dataset for a similar scenario using HDInsight Hadoop clusters for data processing, see [Team Data Science Process - Using Azure HDInsight Hadoop Clusters on a 1 TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span></span>

<span data-ttu-id="28646-107">Il est également possible d'avoir recours à un interpréteur IPython notebook pour accomplir les tâches présentées dans cette procédure pas à pas au moyen du jeu de données de 1 To.</span><span class="sxs-lookup"><span data-stu-id="28646-107">It is also possible to use an IPython notebook to accomplish the tasks presented the walkthrough using the 1 TB dataset.</span></span> <span data-ttu-id="28646-108">Les utilisateurs qui souhaitent essayer cette approche doivent consulter la rubrique [Procédure pas à pas Criteo à l’aide d’une connexion Hive ODBC](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) .</span><span class="sxs-lookup"><span data-stu-id="28646-108">Users who would like to try this approach should consult the [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="28646-109"><a name="dataset"></a>Description du jeu de données NYC Taxi Trips</span><span class="sxs-lookup"><span data-stu-id="28646-109"><a name="dataset"></a>NYC Taxi Trips Dataset description</span></span>
<span data-ttu-id="28646-110">Pesant environ 20 Go au format compressé (ou 48 Go au format non compressé), le jeu de données NYC Taxi Trip contient des fichiers CSV (valeurs séparées par des virgules) concernant plus de 173 millions de trajets et le prix réglé pour chacun d’entre eux.</span><span class="sxs-lookup"><span data-stu-id="28646-110">The NYC Taxi Trip data is about 20GB of compressed comma-separated values (CSV) files (~48GB uncompressed), comprising more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="28646-111">Chaque enregistrement de course inclut le lieu et l’heure d’embarquement et de débarquement, le numéro de licence (du chauffeur) rendu anonyme et le numéro de médaillon (numéro d’identification unique) du taxi.</span><span class="sxs-lookup"><span data-stu-id="28646-111">Each trip record includes the pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="28646-112">Les données portent sur toutes les courses effectuées en 2013 et sont fournies dans les deux jeux de données ci-après pour chaque mois :</span><span class="sxs-lookup"><span data-stu-id="28646-112">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

1. <span data-ttu-id="28646-113">Les fichiers CSV trip_data contiennent les détails de chaque course, comme le nombre de passagers, les points d’embarquement et de débarquement, la durée du trajet et la distance parcourue.</span><span class="sxs-lookup"><span data-stu-id="28646-113">The 'trip_data' CSV files contain trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="28646-114">Voici quelques exemples d’enregistrements :</span><span class="sxs-lookup"><span data-stu-id="28646-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="28646-115">Les fichiers CSV trip_fare contiennent des informations sur le prix payé pour chaque trajet, comme le type de paiement, le montant, la surcharge et les taxes, les pourboires et péages, ainsi que le montant total réglé.</span><span class="sxs-lookup"><span data-stu-id="28646-115">The 'trip_fare' CSV files contain details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="28646-116">Voici quelques exemples d’enregistrements :</span><span class="sxs-lookup"><span data-stu-id="28646-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="28646-117">La clé unique permettant de joindre trip\_data et trip\_fare se compose des champs suivants : medallion (médaillon), hack\_licence (licence de taxi) et pickup\_datetime (date et heure d’embarquement).</span><span class="sxs-lookup"><span data-stu-id="28646-117">The unique key to join trip\_data and trip\_fare is composed of the fields: medallion, hack\_licence and pickup\_datetime.</span></span>

<span data-ttu-id="28646-118">Pour obtenir tous les détails pertinents pour un voyage en particulier, il suffit de joindre les trois clés suivants : « medallion », « hack\_license » et « pickup\_datetime ».</span><span class="sxs-lookup"><span data-stu-id="28646-118">To get all of the details relevant to a particular trip, it is sufficient to join with three keys: the "medallion", "hack\_license" and "pickup\_datetime".</span></span>

<span data-ttu-id="28646-119">Nous fournissons rapidement des informations supplémentaires relatives aux données lorsque nous les stockons dans les tables Hive.</span><span class="sxs-lookup"><span data-stu-id="28646-119">We describe some more details of the data when we store them into Hive tables shortly.</span></span>

## <span data-ttu-id="28646-120"><a name="mltasks"></a>Exemples de tâches de prédiction</span><span class="sxs-lookup"><span data-stu-id="28646-120"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="28646-121">Le fait de connaître le type de prévisions que vous souhaitez obtenir de l’analyse des données permet de clarifier les tâches à inclure dans votre processus.</span><span class="sxs-lookup"><span data-stu-id="28646-121">When approaching data, determining the kind of predictions you want to make based on its analysis helps clarify the tasks that you will need to include in your process.</span></span>
<span data-ttu-id="28646-122">Voici trois exemples de problèmes de prévisions que nous allons traiter dans ce guide et dont la formulation s’appuie sur le champ *tip\_amount* :</span><span class="sxs-lookup"><span data-stu-id="28646-122">Here are three examples of prediction problems that we address in this walkthrough whose formulation is based on the *tip\_amount*:</span></span>

1. <span data-ttu-id="28646-123">**Classification binaire** : prédire si un pourboire a ou non été versé pour une course ; autrement dit, une valeur *tip\_amount* supérieure à 0 $ constitue un exemple positif, alors qu’une *valeur tip\_amount* de 0 $ est un exemple négatif.</span><span class="sxs-lookup"><span data-stu-id="28646-123">**Binary classification**: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. <span data-ttu-id="28646-124">**Classification multiclasse**: prédire la fourchette du montant des pourboires versés pour une course.</span><span class="sxs-lookup"><span data-stu-id="28646-124">**Multiclass classification**: To predict the range of tip amounts paid for the trip.</span></span> <span data-ttu-id="28646-125">Nous divisons la valeur *tip\_amount* en cinq compartiments ou classes :</span><span class="sxs-lookup"><span data-stu-id="28646-125">We divide the *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="28646-126">**Tâche de régression**: prédire le montant du pourboire versé pour une course.</span><span class="sxs-lookup"><span data-stu-id="28646-126">**Regression task**: To predict the amount of the tip paid for a trip.</span></span>  

## <span data-ttu-id="28646-127"><a name="setup"></a>Configuration d’un cluster Hadoop HDInsight pour une analyse avancée</span><span class="sxs-lookup"><span data-stu-id="28646-127"><a name="setup"></a>Set up an HDInsight Hadoop cluster for advanced analytics</span></span>
> [!NOTE]
> <span data-ttu-id="28646-128">Il s'agit généralement d’une tâche d’ **administration** .</span><span class="sxs-lookup"><span data-stu-id="28646-128">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="28646-129">Vous pouvez configurer un environnement Azure pour une analyse avancée qui utilise un cluster HDInsight en trois étapes :</span><span class="sxs-lookup"><span data-stu-id="28646-129">You can set up an Azure environment for advanced analytics that employs an HDInsight cluster in three steps:</span></span>

1. <span data-ttu-id="28646-130">[Création d’un compte de stockage](../storage/common/storage-create-storage-account.md): ce compte de stockage est utilisé pour stocker des données dans un stockage Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="28646-130">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used for storing data in Azure Blob Storage.</span></span> <span data-ttu-id="28646-131">Les données utilisées dans les clusters HDInsight résident également ici.</span><span class="sxs-lookup"><span data-stu-id="28646-131">The data used in HDInsight clusters also resides here.</span></span>
2. <span data-ttu-id="28646-132">[Personnaliser des clusters Hadoop Azure HDInsight pour le processus et la technologie d'analyse avancée](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="28646-132">[Customize Azure HDInsight Hadoop clusters for the Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md).</span></span> <span data-ttu-id="28646-133">Cette étape crée un cluster Hadoop Azure HDInsight avec Anaconda Python 2.7 64 bits installé sur tous les nœuds.</span><span class="sxs-lookup"><span data-stu-id="28646-133">This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="28646-134">Il existe deux étapes importantes à retenir lors de la personnalisation de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="28646-134">There are two important steps to remember while customizing your HDInsight cluster.</span></span>
   
   * <span data-ttu-id="28646-135">Rappelez-vous de lier le compte de stockage créé à l'étape 1 à votre cluster HDInsight, lorsque vous le créez.</span><span class="sxs-lookup"><span data-stu-id="28646-135">Remember to link the storage account created in step 1 with your HDInsight cluster when creating it.</span></span> <span data-ttu-id="28646-136">Ce compte de stockage est utilisé pour accéder aux données qui peuvent être traitées au sein du cluster.</span><span class="sxs-lookup"><span data-stu-id="28646-136">This storage account is used to access data that is processed within the cluster.</span></span>
   * <span data-ttu-id="28646-137">Une fois le cluster créé, activez l'accès à distance au nœud principal du cluster.</span><span class="sxs-lookup"><span data-stu-id="28646-137">After the cluster is created, enable Remote Access to the head node of the cluster.</span></span> <span data-ttu-id="28646-138">Accédez à l’onglet **Configuration**, puis cliquez sur **Activation à distance**.</span><span class="sxs-lookup"><span data-stu-id="28646-138">Navigate to the **Configuration** tab and click **Enable Remote**.</span></span> <span data-ttu-id="28646-139">Cette étape fournit les informations d'identification d'utilisateur utilisées pour la connexion à distance.</span><span class="sxs-lookup"><span data-stu-id="28646-139">This step specifies the user credentials used for remote login.</span></span>
3. <span data-ttu-id="28646-140">[Création d’un espace de travail Azure Machine Learning](machine-learning-create-workspace.md): cet espace de travail Azure Machine Learning est utilisé pour construire des modèles d'apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="28646-140">[Create an Azure Machine Learning workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used to build machine learning models.</span></span> <span data-ttu-id="28646-141">Cette tâche est entamée après avoir effectué une exploration de données initiales et une réduction de l’échantillon à l'aide du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="28646-141">This task is addressed after completing an initial data exploration and down sampling using the HDInsight cluster.</span></span>

## <span data-ttu-id="28646-142"><a name="getdata"></a>Obtenir les données auprès d’une source publique</span><span class="sxs-lookup"><span data-stu-id="28646-142"><a name="getdata"></a>Get the data from a public source</span></span>
> [!NOTE]
> <span data-ttu-id="28646-143">Il s'agit généralement d’une tâche d’ **administration** .</span><span class="sxs-lookup"><span data-stu-id="28646-143">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="28646-144">Pour récupérer le jeu de données [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) depuis son emplacement public, vous pouvez utiliser l’une des méthodes décrites dans l’article [Déplacer des données vers et depuis le stockage d’objets blob Azure](machine-learning-data-science-move-azure-blob.md) afin de copier les données dans votre machine.</span><span class="sxs-lookup"><span data-stu-id="28646-144">To get the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of the methods described in [Move Data to and from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) to copy the data to your machine.</span></span>

<span data-ttu-id="28646-145">Nous décrivons ici comment utiliser AzCopy pour transférer les fichiers contenant des données.</span><span class="sxs-lookup"><span data-stu-id="28646-145">Here we describe how use AzCopy to transfer the files containing data.</span></span> <span data-ttu-id="28646-146">Pour télécharger et installer AzCopy, suivez les instructions dans [Prise en main de l'utilitaire de ligne de commande AzCopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="28646-146">To download and install AzCopy follow the instructions at [Getting Started with the AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

1. <span data-ttu-id="28646-147">Dans une fenêtre d’invite de commandes, exécutez les commandes AzCopy suivantes en remplaçant *<path_to_data_folder>* par la destination souhaitée :</span><span class="sxs-lookup"><span data-stu-id="28646-147">From a Command Prompt window, issue the following AzCopy commands, replacing *<path_to_data_folder>* with the desired destination:</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. <span data-ttu-id="28646-148">Une fois la copie terminée, un total de 24 fichiers compressés se trouvent dans le dossier de données choisi.</span><span class="sxs-lookup"><span data-stu-id="28646-148">When the copy completes, a total of 24 zipped files are in the data folder chosen.</span></span> <span data-ttu-id="28646-149">Décompressez les fichiers téléchargés dans le même répertoire sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="28646-149">Unzip the downloaded files to the same directory on your local machine.</span></span> <span data-ttu-id="28646-150">Prenez note du dossier où résident les fichiers décompressés.</span><span class="sxs-lookup"><span data-stu-id="28646-150">Make a note of the folder where the uncompressed files reside.</span></span> <span data-ttu-id="28646-151">Ce dossier sera désigné comme *<path\_to\_unzipped_data\_files\>* chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="28646-151">This folder will be referred to as the *<path\_to\_unzipped_data\_files\>* is what follows.</span></span>

## <span data-ttu-id="28646-152"><a name="upload"></a>Charger les données dans le conteneur par défaut du cluster Hadoop Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="28646-152"><a name="upload"></a>Upload the data to the default container of Azure HDInsight Hadoop cluster</span></span>
> [!NOTE]
> <span data-ttu-id="28646-153">Il s'agit généralement d’une tâche d’ **administration** .</span><span class="sxs-lookup"><span data-stu-id="28646-153">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="28646-154">Dans les commandes AzCopy suivantes, remplacez les paramètres suivants par les valeurs réelles que vous avez spécifiées lors de la création du cluster Hadoop et lors de la décompression des fichiers de données.</span><span class="sxs-lookup"><span data-stu-id="28646-154">In the following AzCopy commands, replace the following parameters with the actual values that you specified when creating the Hadoop cluster and unzipping the data files.</span></span>

* <span data-ttu-id="28646-155">***&#60;path_to_data_folder>*** le répertoire (ainsi que le chemin d’accès) sur votre ordinateur qui contiennent les fichiers de données décompressés</span><span class="sxs-lookup"><span data-stu-id="28646-155">***&#60;path_to_data_folder>*** the directory (along with path) on your machine that contain the unzipped data files</span></span>  
* <span data-ttu-id="28646-156">***&#60;storage account name of Hadoop cluster>*** le compte de stockage associé à votre cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="28646-156">***&#60;storage account name of Hadoop cluster>*** the storage account associated with your HDInsight cluster</span></span>
* <span data-ttu-id="28646-157">***&#60;default container of Hadoop cluster>*** le conteneur par défaut utilisé par votre cluster.</span><span class="sxs-lookup"><span data-stu-id="28646-157">***&#60;default container of Hadoop cluster>*** the default container used by your cluster.</span></span> <span data-ttu-id="28646-158">Notez que le nom du conteneur par défaut est généralement le même nom que celui du cluster.</span><span class="sxs-lookup"><span data-stu-id="28646-158">Note that the name of the default container is usually the same name as the cluster itself.</span></span> <span data-ttu-id="28646-159">Par exemple, si le cluster est appelé « abc123.azurehdinsight.net », le conteneur par défaut est abc123.</span><span class="sxs-lookup"><span data-stu-id="28646-159">For example, if the cluster is called "abc123.azurehdinsight.net", the default container is abc123.</span></span>
* <span data-ttu-id="28646-160">***&#60;storage account key>*** la clé du compte de stockage utilisé par votre cluster</span><span class="sxs-lookup"><span data-stu-id="28646-160">***&#60;storage account key>*** the key for the storage account used by your cluster</span></span>

<span data-ttu-id="28646-161">À partir d'une invite de commandes ou d’une fenêtre Windows PowerShell sur votre ordinateur, exécutez les deux commandes AzCopy suivantes.</span><span class="sxs-lookup"><span data-stu-id="28646-161">From a Command Prompt or a Windows PowerShell window in your machine, run the following two AzCopy commands.</span></span>

<span data-ttu-id="28646-162">Cette commande permet de télécharger les données relatives aux courses sur le répertoire ***nyctaxitripraw*** dans le conteneur par défaut du cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="28646-162">This command uploads the trip data to ***nyctaxitripraw*** directory in the default container of the Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

<span data-ttu-id="28646-163">Cette commande télécharge les données de prix sur le répertoire ***nyctaxifareraw*** dans le conteneur par défaut du cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="28646-163">This command uploads the fare data to ***nyctaxifareraw*** directory in the default container of the Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

<span data-ttu-id="28646-164">Les données doivent être désormais dans le stockage Blob Azure et prêtes à être utilisées au sein du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="28646-164">The data should now in Azure Blob Storage and ready to be consumed within the HDInsight cluster.</span></span>

## <span data-ttu-id="28646-165"><a name="#download-hql-files"></a>Connectez-vous au nœud principal du cluster Hadoop et préparez une analyse exploratoire de données</span><span class="sxs-lookup"><span data-stu-id="28646-165"><a name="#download-hql-files"></a>Log into the head node of Hadoop cluster and and prepare for exploratory data analysis</span></span>
> [!NOTE]
> <span data-ttu-id="28646-166">Il s'agit généralement d’une tâche d’ **administration** .</span><span class="sxs-lookup"><span data-stu-id="28646-166">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="28646-167">Pour accéder au nœud principal du cluster afin d’exécuter une analyse exploratoire des données et une réduction de l’échantillon des données, suivez la procédure décrite dans [Accéder au nœud principal du cluster Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="28646-167">To access the head node of the cluster for exploratory data analysis and down sampling of the data, follow the procedure outlined in [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

<span data-ttu-id="28646-168">Dans cette procédure pas à pas, nous utilisons principalement les requêtes écrites dans [Hive](https://hive.apache.org/), un langage de requête similaire à SQL, pour effectuer des explorations de données préliminaires.</span><span class="sxs-lookup"><span data-stu-id="28646-168">In this walkthrough, we primarily use queries written in [Hive](https://hive.apache.org/), a SQL-like query language, to perform preliminary data explorations.</span></span> <span data-ttu-id="28646-169">Les requêtes Hive sont stockées dans des fichiers .hql.</span><span class="sxs-lookup"><span data-stu-id="28646-169">The Hive queries are stored in .hql files.</span></span> <span data-ttu-id="28646-170">Nous réduisons ensuite l’échantillon de ces données à utiliser avec Azure Machine Learning pour la construction de modèles.</span><span class="sxs-lookup"><span data-stu-id="28646-170">We then down sample this data to be used within Azure Machine Learning for building models.</span></span>

<span data-ttu-id="28646-171">Pour préparer le cluster d’analyse exploratoire des données, nous téléchargeons les fichiers .hql contenant les scripts Hive pertinents de [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) dans un répertoire local (C:\temp) sur le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="28646-171">To prepare the cluster for exploratory data analysis, we download the .hql files containing the relevant Hive scripts from [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) to a local directory (C:\temp) on the head node.</span></span> <span data-ttu-id="28646-172">Pour ce faire, ouvrez l’ **invite de commandes** dans le nœud principal du cluster et exécutez les deux commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="28646-172">To do this, open the **Command Prompt** from within the head node of the cluster and issue the following two commands:</span></span>

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

<span data-ttu-id="28646-173">Ces deux commandes téléchargent tous les fichiers .hql nécessaires dans cette procédure pas à pas sur le répertoire local ***C:\temp&#92;*** dans le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="28646-173">These two commands will download all .hql files needed in this walkthrough to the local directory ***C:\temp&#92;*** in the head node.</span></span>

## <span data-ttu-id="28646-174"><a name="#hive-db-tables"></a>Créer la base de données Hive et les tables partitionnées par mois</span><span class="sxs-lookup"><span data-stu-id="28646-174"><a name="#hive-db-tables"></a>Create Hive database and tables partitioned by month</span></span>
> [!NOTE]
> <span data-ttu-id="28646-175">Il s'agit généralement d’une tâche d’ **administration** .</span><span class="sxs-lookup"><span data-stu-id="28646-175">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="28646-176">Nous sommes maintenant prêts à créer des tables Hive pour notre jeu de données NYC taxi.</span><span class="sxs-lookup"><span data-stu-id="28646-176">We are now ready to create Hive tables for our NYC taxi dataset.</span></span>
<span data-ttu-id="28646-177">Dans le nœud principal du cluster Hadoop, ouvrez la ***Ligne de commande Hadoop*** sur le bureau du nœud principal et saisissez le répertoire Hive en entrant la commande</span><span class="sxs-lookup"><span data-stu-id="28646-177">In the head node of the Hadoop cluster, open the ***Hadoop Command Line*** on the desktop of the head node, and enter the Hive directory by entering the command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="28646-178">**Exécutez, dans cette procédure pas à pas, toutes les commandes Hive depuis l’invite de l’emplacement/du répertoire Hive mentionnée ci-dessus. Il se chargera automatiquement de tout problème lié au chemin d'accès. Nous utiliserons les termes « Invite du répertoire Hive », « Invite de l’emplacement/du répertoire Hive » et « Ligne de commande Hadoop » de manière interchangeable dans cette procédure pas à pas.**</span><span class="sxs-lookup"><span data-stu-id="28646-178">**Run all Hive commands in this walkthrough from the above Hive bin/ directory prompt. This will take care of any path issues automatically. We use the terms "Hive directory prompt", "Hive bin/ directory prompt",  and "Hadoop Command Line" interchangeably in this walkthrough.**</span></span>
> 
> 

<span data-ttu-id="28646-179">À partir de l'invite du répertoire Hive, entrez la commande suivante dans la Ligne de commande Hadoop du nœud principal pour soumettre la requête Hive afin de créer des tables et une base de données Hive :</span><span class="sxs-lookup"><span data-stu-id="28646-179">From the Hive directory prompt, enter the following command in Hadoop Command Line of the head node to submit the Hive query to create Hive database and tables:</span></span>

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

<span data-ttu-id="28646-180">Voici le contenu du fichier ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql*** qui crée la base de données Hive ***nyctaxidb*** et les tables ***trip*** et ***fare***.</span><span class="sxs-lookup"><span data-stu-id="28646-180">Here is the content of the ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql*** file which creates Hive database ***nyctaxidb*** and tables ***trip*** and ***fare***.</span></span>

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

<span data-ttu-id="28646-181">Ce script Hive crée deux tables :</span><span class="sxs-lookup"><span data-stu-id="28646-181">This Hive script creates two tables:</span></span>

* <span data-ttu-id="28646-182">la table « trip » contient le détail du trajet de chaque course (détails du chauffeur, heure d’embarquement, durée de la course et distance parcourue)</span><span class="sxs-lookup"><span data-stu-id="28646-182">the "trip" table contains trip details of each ride (driver details, pickup time, trip distance and times)</span></span>
* <span data-ttu-id="28646-183">la table « fare » contient le détail des prix (montant de la course, montant des pourboires, péages et surcharges).</span><span class="sxs-lookup"><span data-stu-id="28646-183">the "fare" table contains fare details (fare amount, tip amount, tolls and surcharges).</span></span>

<span data-ttu-id="28646-184">Si vous avez besoin d’aide sur ces procédures souhaitez examiner d’autres solutions, voir la section [Envoyer des requêtes Hive directement depuis la ligne de commande Hadoop](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="28646-184">If you need any additional assistance with these procedures or want to investigate alternative ones, see the section [Submit Hive queries directly from the Hadoop Command Line ](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="28646-185"><a name="#load-data"></a>Charger les données dans les tables Hive par partitions</span><span class="sxs-lookup"><span data-stu-id="28646-185"><a name="#load-data"></a>Load Data to Hive tables by partitions</span></span>
> [!NOTE]
> <span data-ttu-id="28646-186">Il s'agit généralement d’une tâche d’ **administration** .</span><span class="sxs-lookup"><span data-stu-id="28646-186">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="28646-187">Le jeu de données taxi NYC a un partitionnement naturel par mois, qui nous permet d’accélérer les temps de traitement et de requête.</span><span class="sxs-lookup"><span data-stu-id="28646-187">The NYC taxi dataset has a natural partitioning by month, which we use to enable faster processing and query times.</span></span> <span data-ttu-id="28646-188">Les commandes PowerShell ci-dessous (émises à partir du répertoire Hive à l'aide de la **Ligne de commande Hadoop**) chargent des données dans les tables Hive « trip » et « fare » partitionnées par mois.</span><span class="sxs-lookup"><span data-stu-id="28646-188">The PowerShell commands below (issued from the Hive directory using the **Hadoop Command Line**) load data to the "trip" and "fare" Hive tables partitioned by month.</span></span>

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

<span data-ttu-id="28646-189">Le fichier *sample\_hive\_load\_data\_by\_partitions.hql* contient les commandes **LOAD** suivantes.</span><span class="sxs-lookup"><span data-stu-id="28646-189">The *sample\_hive\_load\_data\_by\_partitions.hql* file contains the following **LOAD** commands.</span></span>

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

<span data-ttu-id="28646-190">Notez que plusieurs des requêtes Hive que nous utilisons ici dans le processus d'exploration impliquent la recherche d'une seule partition ou seulement de quelques partitions.</span><span class="sxs-lookup"><span data-stu-id="28646-190">Note that a number of Hive queries we use here in the exploration process involve looking at just a single partition or at only a couple of partitions.</span></span> <span data-ttu-id="28646-191">Mais ces requêtes peuvent être exécutées pour l'ensemble des données.</span><span class="sxs-lookup"><span data-stu-id="28646-191">But these queries could be run across the entire data.</span></span>

### <span data-ttu-id="28646-192"><a name="#show-db"></a>Afficher les bases de données dans le cluster Hadoop HDInsight</span><span class="sxs-lookup"><span data-stu-id="28646-192"><a name="#show-db"></a>Show databases in the HDInsight Hadoop cluster</span></span>
<span data-ttu-id="28646-193">Pour afficher les bases de données créées dans le cluster Hadoop HDInsight à l’intérieur de fenêtre de commande Hadoop, exécutez la commande suivante dans la ligne de commande Hadoop :</span><span class="sxs-lookup"><span data-stu-id="28646-193">To show the databases created in HDInsight Hadoop cluster inside the Hadoop Command Line window, run the following command in Hadoop Command Line:</span></span>

    hive -e "show databases;"

### <span data-ttu-id="28646-194"><a name="#show-tables"></a>Afficher les tables Hive de la base de données nyctaxidb</span><span class="sxs-lookup"><span data-stu-id="28646-194"><a name="#show-tables"></a>Show the Hive tables in the nyctaxidb database</span></span>
<span data-ttu-id="28646-195">Pour afficher les tables dans la base de données nyctaxidb, exécutez la commande suivante dans la ligne de commande Hadoop :</span><span class="sxs-lookup"><span data-stu-id="28646-195">To show the tables in the nyctaxidb database, run the following command in Hadoop Command Line:</span></span>

    hive -e "show tables in nyctaxidb;"

<span data-ttu-id="28646-196">Nous pouvons confirmer que les tables sont partitionnées en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="28646-196">We can confirm that the tables are partitioned by issuing the command below:</span></span>

    hive -e "show partitions nyctaxidb.trip;"

<span data-ttu-id="28646-197">Le résultat prévu est affiché ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="28646-197">The expected output is shown below:</span></span>

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

<span data-ttu-id="28646-198">De même, nous pouvons vérifier que la table « fare » est partitionnée en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="28646-198">Similarly, we can ensure that the fare table is partitioned by issuing the command below:</span></span>

    hive -e "show partitions nyctaxidb.fare;"

<span data-ttu-id="28646-199">Le résultat prévu est affiché ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="28646-199">The expected output is shown below:</span></span>

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

## <span data-ttu-id="28646-200"><a name="#explore-hive"></a>Exploration des données et ingénierie des fonctionnalités dans Hive</span><span class="sxs-lookup"><span data-stu-id="28646-200"><a name="#explore-hive"></a>Data exploration and feature engineering in Hive</span></span>
> [!NOTE]
> <span data-ttu-id="28646-201">Il s'agit généralement d’une tâche de **données scientifiques** .</span><span class="sxs-lookup"><span data-stu-id="28646-201">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="28646-202">Les tâches d’exploration des données et d’ingénierie des fonctionnalités pour les données chargées dans les tables Hive peuvent être exécutées à l’aide de requêtes Hive.</span><span class="sxs-lookup"><span data-stu-id="28646-202">The data exploration and feature engineering tasks for the data loaded into the Hive tables can be accomplished using Hive queries.</span></span> <span data-ttu-id="28646-203">Voici des exemples de ces tâches que nous vous décrivons dans cette section :</span><span class="sxs-lookup"><span data-stu-id="28646-203">Here are examples of such tasks that we walk you through in this section:</span></span>

* <span data-ttu-id="28646-204">Affichez les 10 premiers enregistrements des deux tables.</span><span class="sxs-lookup"><span data-stu-id="28646-204">View the top 10 records in both tables.</span></span>
* <span data-ttu-id="28646-205">explorer les distributions de données de quelques champs portant sur différentes périodes ;</span><span class="sxs-lookup"><span data-stu-id="28646-205">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="28646-206">examiner la qualité des données des champs de longitude et de latitude ;</span><span class="sxs-lookup"><span data-stu-id="28646-206">Investigate data quality of the longitude and latitude fields.</span></span>
* <span data-ttu-id="28646-207">Générer des étiquettes de classification binaire et multiclasse reposant sur la valeur **tip\_amount**.</span><span class="sxs-lookup"><span data-stu-id="28646-207">Generate binary and multiclass classification labels based on the **tip\_amount**.</span></span>
* <span data-ttu-id="28646-208">Générez des fonctionnalités en calculant les distances des trajets directs.</span><span class="sxs-lookup"><span data-stu-id="28646-208">Generate features by computing the direct trip distances.</span></span>

### <a name="exploration-view-the-top-10-records-in-table-trip"></a><span data-ttu-id="28646-209">Exploration : afficher les 10 premiers enregistrements de la table trip</span><span class="sxs-lookup"><span data-stu-id="28646-209">Exploration: View the top 10 records in table trip</span></span>
> [!NOTE]
> <span data-ttu-id="28646-210">Il s'agit généralement d’une tâche de **données scientifiques** .</span><span class="sxs-lookup"><span data-stu-id="28646-210">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="28646-211">Pour avoir un aperçu des données, nous examinons les 10 enregistrements de chaque table.</span><span class="sxs-lookup"><span data-stu-id="28646-211">To see what the data looks like, we examine 10 records from each table.</span></span> <span data-ttu-id="28646-212">Exécutez les deux requêtes suivantes séparément depuis l’invite de commande du répertoire Hive de la ligne de commande Hadoop pour analyser les enregistrements.</span><span class="sxs-lookup"><span data-stu-id="28646-212">Run the following two queries separately from the Hive directory prompt in the Hadoop Command Line console to inspect the records.</span></span>

<span data-ttu-id="28646-213">Pour obtenir les 10 premiers enregistrements dans la table « trip » du premier mois :</span><span class="sxs-lookup"><span data-stu-id="28646-213">To get the top 10 records in the table "trip" from the first month:</span></span>

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

<span data-ttu-id="28646-214">Pour obtenir les 10 premiers enregistrements dans la table « fare » du premier mois :</span><span class="sxs-lookup"><span data-stu-id="28646-214">To get the top 10 records in the table "fare" from the first month:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

<span data-ttu-id="28646-215">Il est souvent utile de sauvegarder les enregistrements dans un fichier pour un affichage pratique.</span><span class="sxs-lookup"><span data-stu-id="28646-215">It is often useful to save the records to a file for convenient viewing.</span></span> <span data-ttu-id="28646-216">Une petite modification à la requête ci-dessus effectue cette opération :</span><span class="sxs-lookup"><span data-stu-id="28646-216">A small change to the above query accomplishes this:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-the-number-of-records-in-each-of-the-12-partitions"></a><span data-ttu-id="28646-217">Exploration : afficher le nombre d’enregistrements dans chacune des 12 partitions</span><span class="sxs-lookup"><span data-stu-id="28646-217">Exploration: View the number of records in each of the 12 partitions</span></span>
> [!NOTE]
> <span data-ttu-id="28646-218">Il s'agit généralement d’une tâche de **données scientifiques** .</span><span class="sxs-lookup"><span data-stu-id="28646-218">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="28646-219">La façon dont le nombre de courses varie au cours de l'année civile est intéressante.</span><span class="sxs-lookup"><span data-stu-id="28646-219">Of interest is the how the number of trips varies during the calendar year.</span></span> <span data-ttu-id="28646-220">Le regroupement par mois nous permet d’avoir un aperçu de cette distribution de courses.</span><span class="sxs-lookup"><span data-stu-id="28646-220">Grouping by month allows us to see what this distribution of trips looks like.</span></span>

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

<span data-ttu-id="28646-221">Cela nous donne le résultat :</span><span class="sxs-lookup"><span data-stu-id="28646-221">This gives us the output :</span></span>

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

<span data-ttu-id="28646-222">Ici, la première colonne est le mois et la seconde est le nombre de courses pour ce mois.</span><span class="sxs-lookup"><span data-stu-id="28646-222">Here, the first column is the month and the second is the number of trips for that month.</span></span>

<span data-ttu-id="28646-223">Nous pouvons également compter le nombre total d'enregistrements dans notre jeu de données de courses en exécutant la commande suivante à l'invite du répertoire Hive.</span><span class="sxs-lookup"><span data-stu-id="28646-223">We can also count the total number of records in our trip data set by issuing the following command at the Hive directory prompt.</span></span>

    hive -e "select count(*) from nyctaxidb.trip;"

<span data-ttu-id="28646-224">Cela donne :</span><span class="sxs-lookup"><span data-stu-id="28646-224">This yields:</span></span>

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

<span data-ttu-id="28646-225">À l'aide des commandes similaires à celles indiquées pour le jeu de données de course, nous pouvons émettre des requêtes Hive à partir de l'invite du répertoire Hive pour le jeu de données fare afin de valider le nombre d'enregistrements.</span><span class="sxs-lookup"><span data-stu-id="28646-225">Using commands similar to those shown for the trip data set, we can issue Hive queries from the Hive directory prompt for the fare data set to validate the number of records.</span></span>

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

<span data-ttu-id="28646-226">Cela nous donne le résultat :</span><span class="sxs-lookup"><span data-stu-id="28646-226">This gives us the output:</span></span>

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

<span data-ttu-id="28646-227">Notez qu’exactement le même nombre de courses par mois est retourné pour les deux jeux de données.</span><span class="sxs-lookup"><span data-stu-id="28646-227">Note that the exact same number of trips per month is returned for both data sets.</span></span> <span data-ttu-id="28646-228">C’est le premier élément garantissant que les données ont été chargées correctement.</span><span class="sxs-lookup"><span data-stu-id="28646-228">This provides the first validation that the data has been loaded correctly.</span></span>

<span data-ttu-id="28646-229">Le calcul du nombre total d'enregistrements dans le jeu de données fare peut être effectué à l'aide de la commande ci-dessous à partir de l'invite du répertoire Hive :</span><span class="sxs-lookup"><span data-stu-id="28646-229">Counting the total number of records in the fare data set can be done using the command below from the Hive directory prompt:</span></span>

    hive -e "select count(*) from nyctaxidb.fare;"

<span data-ttu-id="28646-230">Cela donne :</span><span class="sxs-lookup"><span data-stu-id="28646-230">This yields :</span></span>

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

<span data-ttu-id="28646-231">Le nombre total d'enregistrements dans les deux tables est également le même.</span><span class="sxs-lookup"><span data-stu-id="28646-231">The total number of records in both tables is also the same.</span></span> <span data-ttu-id="28646-232">C’est le deuxième élément garantissant que les données ont été chargées correctement.</span><span class="sxs-lookup"><span data-stu-id="28646-232">This provides a second validation that the data has been loaded correctly.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="28646-233">Exploration : distribution des courses par médaillon</span><span class="sxs-lookup"><span data-stu-id="28646-233">Exploration: Trip distribution by medallion</span></span>
> [!NOTE]
> <span data-ttu-id="28646-234">Il s'agit généralement d’une tâche de **données scientifiques** .</span><span class="sxs-lookup"><span data-stu-id="28646-234">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="28646-235">Cet exemple identifie le médaillon (numéro de taxi) sur plus de 100 courses au cours d’une période donnée.</span><span class="sxs-lookup"><span data-stu-id="28646-235">This example identifies the medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="28646-236">La requête a accès aux tables partitionnées, car elle est conditionnée par la variable de partition **month**.</span><span class="sxs-lookup"><span data-stu-id="28646-236">The query benefits from the partitioned table access since it is conditioned by the partition variable **month**.</span></span> <span data-ttu-id="28646-237">Les résultats de la requête sont écrits dans un fichier local queryoutput.tsv dans `C:\temp` sur le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="28646-237">The query results are written to a local file queryoutput.tsv in `C:\temp` on the head node.</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="28646-238">Voici le contenu du fichier *sample\_hive\_trip\_count\_by\_medallion.hql* pour l’inspection.</span><span class="sxs-lookup"><span data-stu-id="28646-238">Here is the content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="28646-239">Le médaillon dans le jeu de données NYC taxi identifie un seul taxi.</span><span class="sxs-lookup"><span data-stu-id="28646-239">The medallion in the NYC taxi data set identifies a unique cab.</span></span> <span data-ttu-id="28646-240">Nous pouvons identifier les taxis « occupés » en demandant quels taxis ont effectué plus d'un certain nombre d'allers-retours sur une période donnée.</span><span class="sxs-lookup"><span data-stu-id="28646-240">We can identify which cabs are "busy" by asking which ones made more than a certain number of trips in a particular time period.</span></span> <span data-ttu-id="28646-241">L'exemple suivant identifie les taxis qui ont effectué plus d’une centaine de courses durant les trois premiers mois et enregistre les résultats de la requête dans un fichier local, C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="28646-241">The following example identifies cabs that made more than a hundred trips in the first three months, and saves the query results to a local file, C:\temp\queryoutput.tsv.</span></span>

<span data-ttu-id="28646-242">Voici le contenu du fichier *sample\_hive\_trip\_count\_by\_medallion.hql* pour l’inspection.</span><span class="sxs-lookup"><span data-stu-id="28646-242">Here is the content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="28646-243">À partir de l'invite du répertoire Hive, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="28646-243">From the Hive directory prompt, issue the command below :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="28646-244">Exploration : distribution des courses par médaillon et par licence de taxi</span><span class="sxs-lookup"><span data-stu-id="28646-244">Exploration: Trip distribution by medallion and hack_license</span></span>
> [!NOTE]
> <span data-ttu-id="28646-245">Il s'agit généralement d’une tâche de **données scientifiques** .</span><span class="sxs-lookup"><span data-stu-id="28646-245">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="28646-246">Lors de l'exploration d'un jeu de données, nous devons examiner fréquemment le nombre de co-occurrences des groupes de valeurs.</span><span class="sxs-lookup"><span data-stu-id="28646-246">When exploring a dataset, we frequently want to examine the number of co-occurences of groups of values.</span></span> <span data-ttu-id="28646-247">Cette section fournit un exemple de procédure à suivre pour les chauffeurs et les taxis.</span><span class="sxs-lookup"><span data-stu-id="28646-247">This section provide an example of how to do this for cabs and drivers.</span></span>

<span data-ttu-id="28646-248">Le fichier *sample\_hive\_trip\_count\_by\_medallion\_license.hql* regroupe le jeu de données fare sur « medallion » et « hack_license », et renvoie le nombre de chaque combinaison.</span><span class="sxs-lookup"><span data-stu-id="28646-248">The *sample\_hive\_trip\_count\_by\_medallion\_license.hql* file groups the fare data set on "medallion" and "hack_license" and returns counts of each combination.</span></span> <span data-ttu-id="28646-249">Son contenu est présenté ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="28646-249">Below are its contents.</span></span>

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

<span data-ttu-id="28646-250">Cette requête renvoie les combinaisons de taxi et de chauffeur particulier classées par ordre décroissant de courses.</span><span class="sxs-lookup"><span data-stu-id="28646-250">This query returns cab and particular driver combinations ordered by descending number of trips.</span></span>

<span data-ttu-id="28646-251">À partir de l'invite du répertoire Hive, exécutez :</span><span class="sxs-lookup"><span data-stu-id="28646-251">From the Hive directory prompt, run :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="28646-252">Les résultats de la requête sont écrits dans un fichier local C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="28646-252">The query results are written to a local file C:\temp\queryoutput.tsv.</span></span>

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a><span data-ttu-id="28646-253">Exploration : évaluation de la qualité des données en recherchant les enregistrements de longitude et de latitude non valides</span><span class="sxs-lookup"><span data-stu-id="28646-253">Exploration: Assessing data quality by checking for invalid longitude/latitude records</span></span>
> [!NOTE]
> <span data-ttu-id="28646-254">Il s'agit généralement d’une tâche de **données scientifiques** .</span><span class="sxs-lookup"><span data-stu-id="28646-254">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="28646-255">Un objectif commun d'une analyse exploratoire des données est d'éliminer les enregistrements non valides ou incorrects.</span><span class="sxs-lookup"><span data-stu-id="28646-255">A common objective of exploratory data analysis is to weed out invalid or bad records.</span></span> <span data-ttu-id="28646-256">L'exemple de cette section détermine si les champs de latitude ou de longitude contiennent une valeur en dehors de la zone NYC.</span><span class="sxs-lookup"><span data-stu-id="28646-256">The example in this section determines whether either the longitude or latitude fields contain a value far outside the NYC area.</span></span> <span data-ttu-id="28646-257">Dans la mesure où il est probable que les valeurs de latitude-longitude de ces enregistrements soient erronées, nous souhaitons les éliminer des données devant être utilisées pour la modélisation.</span><span class="sxs-lookup"><span data-stu-id="28646-257">Since it is likely that such records have an erroneous longitude-latitude values, we want to eliminate them from any data that is to be used for modeling.</span></span>

<span data-ttu-id="28646-258">Voici le contenu du fichier *sample\_hive\_quality\_assessment.hql* pour l’inspection.</span><span class="sxs-lookup"><span data-stu-id="28646-258">Here is the content of *sample\_hive\_quality\_assessment.hql* file for inspection.</span></span>

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


<span data-ttu-id="28646-259">À partir de l'invite du répertoire Hive, exécutez :</span><span class="sxs-lookup"><span data-stu-id="28646-259">From the Hive directory prompt, run :</span></span>

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

<span data-ttu-id="28646-260">L’argument *-S* inclus dans la commande supprime l’affichage de l’état des travaux Map/Reduce Hive.</span><span class="sxs-lookup"><span data-stu-id="28646-260">The *-S* argument included in this command suppresses the status screen printout of the Hive Map/Reduce jobs.</span></span> <span data-ttu-id="28646-261">Son utilité réside dans le fait qu’il rend l’affichage de la sortie de la requête Hive plus lisible.</span><span class="sxs-lookup"><span data-stu-id="28646-261">This is useful because it makes the screen print of the Hive query output more readable.</span></span>

### <a name="exploration-binary-class-distributions-of-trip-tips"></a><span data-ttu-id="28646-262">Exploration : distributions de classe binaire des pourboires de course</span><span class="sxs-lookup"><span data-stu-id="28646-262">Exploration: Binary class distributions of trip tips</span></span>
> [!NOTE]
> <span data-ttu-id="28646-263">Il s'agit généralement d’une tâche de **données scientifiques** .</span><span class="sxs-lookup"><span data-stu-id="28646-263">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="28646-264">Pour le problème de classification binaire présenté dans la section [Exemples de tâches de prédiction](machine-learning-data-science-process-hive-walkthrough.md#mltasks) , il est utile de savoir si un pourboire a été donné ou non.</span><span class="sxs-lookup"><span data-stu-id="28646-264">For the binary classification problem outlined in the [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section, it is useful to know whether a tip was given or not.</span></span> <span data-ttu-id="28646-265">Cette distribution de pourboires est binaire :</span><span class="sxs-lookup"><span data-stu-id="28646-265">This distribution of tips is binary:</span></span>

* <span data-ttu-id="28646-266">pourboire donné (classe 1, tip\_amount > 0 $)</span><span class="sxs-lookup"><span data-stu-id="28646-266">tip given(Class 1, tip\_amount > $0)</span></span>  
* <span data-ttu-id="28646-267">Aucun pourboire (classe 0, tip\_amount = 0 $).</span><span class="sxs-lookup"><span data-stu-id="28646-267">no tip (Class 0, tip\_amount = $0).</span></span>

<span data-ttu-id="28646-268">Le fichier *sample\_hive\_tipped\_frequencies.hql* ci-dessous effectue cette opération.</span><span class="sxs-lookup"><span data-stu-id="28646-268">The *sample\_hive\_tipped\_frequencies.hql* file shown below does this.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

<span data-ttu-id="28646-269">À partir de l'invite du répertoire Hive, exécutez :</span><span class="sxs-lookup"><span data-stu-id="28646-269">From the Hive directory prompt, run:</span></span>

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-the-multiclass-setting"></a><span data-ttu-id="28646-270">Exploration : distributions de classe dans le paramètre multiclasse</span><span class="sxs-lookup"><span data-stu-id="28646-270">Exploration: Class distributions in the multiclass setting</span></span>
> [!NOTE]
> <span data-ttu-id="28646-271">Il s'agit généralement d’une tâche de **données scientifiques** .</span><span class="sxs-lookup"><span data-stu-id="28646-271">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="28646-272">Pour le problème de classification multiclasse décrit dans la section [Exemples de tâches de prédiction](machine-learning-data-science-process-hive-walkthrough.md#mltasks) , ce jeu de données se prête également à une classification naturelle où nous aimerions prédire la quantité de pourboires donnés.</span><span class="sxs-lookup"><span data-stu-id="28646-272">For the multiclass classification problem outlined in the [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section this data set also lends itself to a natural classification where we would like to predict the amount of the tips given.</span></span> <span data-ttu-id="28646-273">Nous pouvons utiliser des compartiments pour définir les montants de pourboires dans la requête.</span><span class="sxs-lookup"><span data-stu-id="28646-273">We can use bins to define tip ranges in the query.</span></span> <span data-ttu-id="28646-274">Pour obtenir les distributions de classe pour les différents montants de pourboire, nous utilisons le fichier *sample\_hive\_tip\_range\_frequencies.hql*.</span><span class="sxs-lookup"><span data-stu-id="28646-274">To get the class distributions for the various tip ranges, we use the *sample\_hive\_tip\_range\_frequencies.hql* file.</span></span> <span data-ttu-id="28646-275">Son contenu est présenté ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="28646-275">Below are its contents.</span></span>

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

<span data-ttu-id="28646-276">Exécutez la commande suivante dans la console de ligne de commande Hadoop :</span><span class="sxs-lookup"><span data-stu-id="28646-276">Run the following command from Hadoop Command Line console:</span></span>

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a><span data-ttu-id="28646-277">Exploration : calculer la distance directe entre deux emplacements de latitude-longitude</span><span class="sxs-lookup"><span data-stu-id="28646-277">Exploration: Compute Direct Distance Between Two Longitude-Latitude Locations</span></span>
> [!NOTE]
> <span data-ttu-id="28646-278">Il s'agit généralement d’une tâche de **données scientifiques** .</span><span class="sxs-lookup"><span data-stu-id="28646-278">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="28646-279">Avoir une idée de la distance directe nous permet de déterminer l'écart entre celle-ci et la distance de course réelle.</span><span class="sxs-lookup"><span data-stu-id="28646-279">Having a measure of the direct distance allows us to find out the discrepancy between it and the actual trip distance.</span></span> <span data-ttu-id="28646-280">Nous expliquons cette fonctionnalité par le fait qu’un passager peut être moins susceptible de donner un pourboire s’il se rend compte que le chauffeur a pris intentionnellement un itinéraire beaucoup plus long.</span><span class="sxs-lookup"><span data-stu-id="28646-280">We motivate this feature by pointing out that a passenger might be less likely to tip if they figure out that the driver has intentionally taken them by a much longer route.</span></span>

<span data-ttu-id="28646-281">Pour afficher la comparaison entre la distance de course réelle et la [distance Haversine](http://en.wikipedia.org/wiki/Haversine_formula) entre deux points de latitude-longitude (la distance orthodromique), nous utilisons les fonctions trigonométriques disponibles au sein de Hive, par conséquent :</span><span class="sxs-lookup"><span data-stu-id="28646-281">To see the comparison between actual trip distance and the [Haversine distance](http://en.wikipedia.org/wiki/Haversine_formula) between two longitude-latitude points (the "great circle" distance), we use the trigonometric functions available within Hive, thus :</span></span>

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

<span data-ttu-id="28646-282">Dans la requête ci-dessus, R est le rayon de la Terre en miles et pi est converti en radians.</span><span class="sxs-lookup"><span data-stu-id="28646-282">In the query above, R is the radius of the Earth in miles, and pi is converted to radians.</span></span> <span data-ttu-id="28646-283">Notez que les points de latitude-longitude sont « filtrés » pour supprimer les valeurs éloignées de la zone NYC.</span><span class="sxs-lookup"><span data-stu-id="28646-283">Note that the longitude-latitude points are "filtered" to remove values that are far from the NYC area.</span></span>

<span data-ttu-id="28646-284">Dans ce cas, nous écrivons nos résultats sur un répertoire nommé « queryoutputdir ».</span><span class="sxs-lookup"><span data-stu-id="28646-284">In this case, we write our results to a directory called "queryoutputdir".</span></span> <span data-ttu-id="28646-285">La séquence de commandes affichée ci-dessous crée d'abord ce répertoire de sortie, puis exécute la commande Hive.</span><span class="sxs-lookup"><span data-stu-id="28646-285">The sequence of commands shown below first creates this output directory, and then runs the Hive command.</span></span>

<span data-ttu-id="28646-286">À partir de l'invite du répertoire Hive, exécutez :</span><span class="sxs-lookup"><span data-stu-id="28646-286">From the Hive directory prompt, run:</span></span>

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


<span data-ttu-id="28646-287">Les résultats de la requête sont consignés dans 9 blobs Azure ***queryoutputdir/000000\_0*** à  ***queryoutputdir/000008\_0*** situés dans le conteneur par défaut du cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="28646-287">The query results are written to 9 Azure blobs ***queryoutputdir/000000\_0*** to  ***queryoutputdir/000008\_0*** under the default container of the Hadoop cluster.</span></span>

<span data-ttu-id="28646-288">Pour connaître la taille des objets BLOB individuels, nous exécutons la commande suivante à partir de l'invite du répertoire Hive :</span><span class="sxs-lookup"><span data-stu-id="28646-288">To see the size of the individual blobs, we run the following command from the Hive directory prompt :</span></span>

    hdfs dfs -ls wasb:///queryoutputdir

<span data-ttu-id="28646-289">Pour afficher le contenu d’un fichier donné, par exemple, 000000\_0, nous utilisons la commande Hadoop `copyToLocal`.</span><span class="sxs-lookup"><span data-stu-id="28646-289">To see the contents of a given file, say 000000\_0, we use Hadoop's `copyToLocal` command, thus.</span></span>

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> <span data-ttu-id="28646-290">`copyToLocal` peut être très lent pour les fichiers volumineux et n’est pas recommandé pour une utilisation avec ceux-ci.</span><span class="sxs-lookup"><span data-stu-id="28646-290">`copyToLocal` can be very slow for large files, and is not recommended for use with them.</span></span>  
> 
> 

<span data-ttu-id="28646-291">Le principal avantage lié au fait que ces données résident dans un objet blob Azure est que nous pouvons explorer les données au sein de Azure Machine Learning à l’aide du module [Importer des données][import-data].</span><span class="sxs-lookup"><span data-stu-id="28646-291">A key advantage of having this data reside in an Azure blob is that we may explore the data within Azure Machine Learning using the [Import Data][import-data] module.</span></span>

## <span data-ttu-id="28646-292"><a name="#downsample"></a>Réduire l’échantillon des données et créer des modèles dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="28646-292"><a name="#downsample"></a>Down sample data and build models in Azure Machine Learning</span></span>
> [!NOTE]
> <span data-ttu-id="28646-293">Il s'agit généralement d’une tâche de **données scientifiques** .</span><span class="sxs-lookup"><span data-stu-id="28646-293">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="28646-294">Après la phase d'analyse exploratoire des données, nous sommes prêts à réduire l’échantillon des données pour générer des modèles dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="28646-294">After the exploratory data analysis phase, we are now ready to down sample the data for building models in Azure Machine Learning.</span></span> <span data-ttu-id="28646-295">Dans cette section, nous montrons comment utiliser une requête Hive pour réduire l’échantillon de données, qui est ensuite accessible à partir du module [Importer des données][import-data] dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="28646-295">In this section, we show how to use a Hive query to down sample the data, which is then accessed from the [Import Data][import-data] module in Azure Machine Learning.</span></span>

### <a name="down-sampling-the-data"></a><span data-ttu-id="28646-296">Réduction de l'échantillonnage des données</span><span class="sxs-lookup"><span data-stu-id="28646-296">Down sampling the data</span></span>
<span data-ttu-id="28646-297">Il existe deux étapes dans cette procédure.</span><span class="sxs-lookup"><span data-stu-id="28646-297">There are two steps in this procedure.</span></span> <span data-ttu-id="28646-298">Tout d’abord nous regroupons les tables **nyctaxidb.trip** et **nyctaxidb.fare** sur trois clés présentes dans tous les enregistrements : « medallion », « hack\_license » et « pickup\_datetime ».</span><span class="sxs-lookup"><span data-stu-id="28646-298">First we join the **nyctaxidb.trip** and **nyctaxidb.fare** tables on three keys that are present in all records : "medallion", "hack\_license", and "pickup\_datetime".</span></span> <span data-ttu-id="28646-299">Nous générons ensuite une étiquette de classification binaire **avec pourboire** et une étiquette de classification multiclasse **tip\_class**.</span><span class="sxs-lookup"><span data-stu-id="28646-299">We then generate a binary classification label **tipped** and a multi-class classification label **tip\_class**.</span></span>

<span data-ttu-id="28646-300">Pour pouvoir utiliser les échantillons de données réduits directement à partir du module [Importer des données][import-data] dans Azure Machine Learning, il est nécessaire de stocker les résultats de la requête ci-dessus dans une table Hive interne.</span><span class="sxs-lookup"><span data-stu-id="28646-300">To be able to use the down sampled data directly from the [Import Data][import-data] module in Azure Machine Learning, it is necessary to store the results of the above query to an internal Hive table.</span></span> <span data-ttu-id="28646-301">Dans ce qui suit, nous créons une table interne Hive et remplissons son contenu avec les données regroupées et à échantillon réduit.</span><span class="sxs-lookup"><span data-stu-id="28646-301">In what follows, we create an internal Hive table and populate its contents with the joined and down sampled data.</span></span>

<span data-ttu-id="28646-302">La requête s’applique directement aux fonctions Hive standards pour générer l’heure du jour, la semaine de l’année, le jour de la semaine (1 signifie lundi et 7 signifie dimanche) à partir du champ « pickup\_datetime » et la distance directe entre les emplacements de départ et d’arrivée.</span><span class="sxs-lookup"><span data-stu-id="28646-302">The query applies standard Hive functions directly to generate the hour of day, week of year, weekday (1 stands for Monday, and 7 stands for Sunday) from the "pickup\_datetime" field,  and the direct distance between the pickup and dropoff locations.</span></span> <span data-ttu-id="28646-303">Les utilisateurs peuvent se reporter à la fonction [UDF LanguageManual](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) pour consulter la liste complète de ces fonctions.</span><span class="sxs-lookup"><span data-stu-id="28646-303">Users can refer to [LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) for a complete list of such functions.</span></span>

<span data-ttu-id="28646-304">Ensuite, cette requête réduit l’échantillon des données pour que ses résultats tiennent dans Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="28646-304">The query then down samples the data so that the query results can fit into the Azure Machine Learning Studio.</span></span> <span data-ttu-id="28646-305">Seulement 1 % environ du jeu de données d'origine est importé dans le Studio.</span><span class="sxs-lookup"><span data-stu-id="28646-305">Only about 1% of the original dataset is imported into the Studio.</span></span>

<span data-ttu-id="28646-306">Voici le contenu du fichier *sample\_hive\_prepare\_for\_aml\_full.hql* qui prépare les données pour la création du modèle dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="28646-306">Below are the contents of *sample\_hive\_prepare\_for\_aml\_full.hql* file that prepares data for model building in Azure Machine Learning.</span></span>

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

        --- now insert contents of the join into the above internal table

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

<span data-ttu-id="28646-307">Pour exécuter cette requête, à partir de l'invite du répertoire Hive :</span><span class="sxs-lookup"><span data-stu-id="28646-307">To run this query, from the Hive directory prompt :</span></span>

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

<span data-ttu-id="28646-308">Nous avons maintenant une table interne « nyctaxidb.nyctaxi_downsampled_dataset », qui est accessible à l’aide du module [Importer des données][import-data] d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="28646-308">We now have an internal table "nyctaxidb.nyctaxi_downsampled_dataset" which can be accessed using the [Import Data][import-data] module from Azure Machine Learning.</span></span> <span data-ttu-id="28646-309">En outre, nous pouvons utiliser ce jeu de données pour générer des modèles d'apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="28646-309">Furthermore, we may use this dataset for building Machine Learning models.</span></span>  

### <a name="use-the-import-data-module-in-azure-machine-learning-to-access-the-down-sampled-data"></a><span data-ttu-id="28646-310">Utiliser le module Importer des données dans Azure Machine Learning pour accéder aux données à échantillon réduit</span><span class="sxs-lookup"><span data-stu-id="28646-310">Use the Import Data module in Azure Machine Learning to access the down sampled data</span></span>
<span data-ttu-id="28646-311">En tant que composants requis pour la création de requêtes Hive dans le module [Importer des données][import-data] d’Azure Machine Learning, nous devons accéder à un espace de travail Azure Machine Learning et aux informations d’identification du cluster et de son compte de stockage associé.</span><span class="sxs-lookup"><span data-stu-id="28646-311">As prerequisites for issuing Hive queries in the [Import Data][import-data] module of Azure Machine Learning, we need access to an Azure Machine Learning workspace and access to the credentials of the cluster and its associated storage account.</span></span>

<span data-ttu-id="28646-312">Certains détails sur le module [Importer des données][import-data] et les paramètres à entrer :</span><span class="sxs-lookup"><span data-stu-id="28646-312">Some details on the [Import Data][import-data] module and the parameters to input :</span></span>

<span data-ttu-id="28646-313">**URI du serveur HCatalog** : si le nom du cluster est abc123, c’est simplement : https://abc123.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="28646-313">**HCatalog server URI**: If the cluster name is abc123, then this is simply : https://abc123.azurehdinsight.net</span></span>

<span data-ttu-id="28646-314">**Nom du compte utilisateur Hadoop** : le nom d’utilisateur choisi pour le cluster (et **non** le nom d’utilisateur de l’accès à distance)</span><span class="sxs-lookup"><span data-stu-id="28646-314">**Hadoop user account name** : The user name chosen for the cluster (**not** the remote access user name)</span></span>

<span data-ttu-id="28646-315">**Mot de passe du compte utilisateur Hadoop** : le mot de passe choisi pour le cluster (et **non** le mot de passe d’accès à distance)</span><span class="sxs-lookup"><span data-stu-id="28646-315">**Hadoop ser account password** : The password chosen for the cluster (**not** the remote access password)</span></span>

<span data-ttu-id="28646-316">**Emplacement des données de sortie** : il est choisi pour être Azure.</span><span class="sxs-lookup"><span data-stu-id="28646-316">**Location of output data** : This is chosen to be Azure.</span></span>

<span data-ttu-id="28646-317">**Nom du compte de stockage Azure** : le nom du compte de stockage par défaut associé au cluster.</span><span class="sxs-lookup"><span data-stu-id="28646-317">**Azure storage account name** : Name of the default storage account associated with the cluster.</span></span>

<span data-ttu-id="28646-318">**Nom de conteneur Azure** : c’est le nom de conteneur par défaut pour le cluster et c’est généralement le même que le nom du cluster.</span><span class="sxs-lookup"><span data-stu-id="28646-318">**Azure container name** : This is the default container name for the cluster, and is typically the same as the cluster name.</span></span> <span data-ttu-id="28646-319">Pour un cluster appelé « abc123 », il s'agit simplement d’abc123.</span><span class="sxs-lookup"><span data-stu-id="28646-319">For a cluster called "abc123", this is just abc123.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="28646-320">**Toute table que nous souhaitons interroger à l’aide du module [Importer des données][import-data] dans Azure Machine Learning doit être une table interne.**</span><span class="sxs-lookup"><span data-stu-id="28646-320">**Any table we wish to query using the [Import Data][import-data] module in Azure Machine Learning must be an internal table.**</span></span> <span data-ttu-id="28646-321">Voici un conseil pour déterminer si une table T dans une base de données D.db est une table interne.</span><span class="sxs-lookup"><span data-stu-id="28646-321">A tip for determining if a table T in a database D.db is an internal table is as follows.</span></span>
> 
> 

<span data-ttu-id="28646-322">À partir de l'invite du répertoire Hive, exécutez la commande :</span><span class="sxs-lookup"><span data-stu-id="28646-322">From the Hive directory prompt, issue the command :</span></span>

    hdfs dfs -ls wasb:///D.db/T

<span data-ttu-id="28646-323">Si la table est une table interne et qu’elle est remplie, son contenu doit s’afficher ici.</span><span class="sxs-lookup"><span data-stu-id="28646-323">If the table is an internal table and it is populated, its contents must show here.</span></span> <span data-ttu-id="28646-324">Pour déterminer si une table est une table interne, il est également possible d’utiliser Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="28646-324">Another way to determine whether a table is an internal table is to use the Azure Storage Explorer.</span></span> <span data-ttu-id="28646-325">Utilisez-le pour accéder au nom de conteneur par défaut du cluster, puis filtrez par nom de table.</span><span class="sxs-lookup"><span data-stu-id="28646-325">Use it to navigate to the default container name of the cluster, and then filter by the table name.</span></span> <span data-ttu-id="28646-326">Si la table et son contenu s'affichent, cela confirme qu'il s’agit d’une table interne.</span><span class="sxs-lookup"><span data-stu-id="28646-326">If the table and its contents show up, this confirms that it is an internal table.</span></span>

<span data-ttu-id="28646-327">Voici un aperçu de la requête Hive et du module [Importer des données][import-data] :</span><span class="sxs-lookup"><span data-stu-id="28646-327">Here is a snapshot of the Hive query and the [Import Data][import-data] module:</span></span>

![Requête Hive pour le module Importer des données](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

<span data-ttu-id="28646-329">Notez que, puisque nos données à l’échantillon réduit résident dans le conteneur par défaut, la requête Hive obtenue d’Azure Machine Learning est très simple est consiste simplement en « SELECT * FROM nyctaxidb.nyctaxi\_downsampled\_data ».</span><span class="sxs-lookup"><span data-stu-id="28646-329">Note that since our down sampled data resides in the default container, the resulting Hive query from Azure Machine Learning is very simple and is just a "SELECT * FROM nyctaxidb.nyctaxi\_downsampled\_data".</span></span>

<span data-ttu-id="28646-330">Le jeu de données peut maintenant être utilisé comme point de départ pour générer des modèles d'apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="28646-330">The dataset may now be used as the starting point for building Machine Learning models.</span></span>

### <span data-ttu-id="28646-331"><a name="mlmodel"></a>Créer des modèles dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="28646-331"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="28646-332">Nous sommes désormais capables de passer aux phases de création et de déploiement de modèles dans [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="28646-332">We are now able to proceed to model building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="28646-333">Les données sont exploitables pour répondre aux problèmes de prévision identifiés précédemment :</span><span class="sxs-lookup"><span data-stu-id="28646-333">The data is ready for us to use in addressing the prediction problems identified above:</span></span>

<span data-ttu-id="28646-334">**1. Classification binaire** : prédire si un pourboire a ou non été versé pour une course.</span><span class="sxs-lookup"><span data-stu-id="28646-334">**1. Binary classification**: To predict whether or not a tip was paid for a trip.</span></span>

<span data-ttu-id="28646-335">**Apprenant utilisé :** régression logistique à deux classes</span><span class="sxs-lookup"><span data-stu-id="28646-335">**Learner used:** Two-class logistic regression</span></span>

<span data-ttu-id="28646-336">a.</span><span class="sxs-lookup"><span data-stu-id="28646-336">a.</span></span> <span data-ttu-id="28646-337">Pour ce problème, notre étiquette (ou classe) cible est « avec pourboire ».</span><span class="sxs-lookup"><span data-stu-id="28646-337">For this problem, our target (or class) label is "tipped".</span></span> <span data-ttu-id="28646-338">Notre jeu de données original à l’échantillon réduit dispose de quelques colonnes qui sont des fuites cibles pour cette expérience de classification.</span><span class="sxs-lookup"><span data-stu-id="28646-338">Our original down-sampled dataset has a few columns that are target leaks for this classification experiment.</span></span> <span data-ttu-id="28646-339">En particulier : tip\_class, tip\_amount et total\_amount révèlent des informations sur l’étiquette cible qui n’est pas disponible au moment du test.</span><span class="sxs-lookup"><span data-stu-id="28646-339">In particular : tip\_class, tip\_amount, and total\_amount reveal information about the target label that is not available at testing time.</span></span> <span data-ttu-id="28646-340">Nous supprimons ces colonnes du compte à l’aide du module [Sélectionner des colonnes dans le jeu de données][select-columns].</span><span class="sxs-lookup"><span data-stu-id="28646-340">We remove these columns from consideration using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="28646-341">L'instantané ci-dessous illustre notre expérience pour prédire si un pourboire a été versé pour une course donnée.</span><span class="sxs-lookup"><span data-stu-id="28646-341">The snapshot below shows our experiment to predict whether or not a tip was paid for a given trip.</span></span>

![Instantané de l’expérience](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

<span data-ttu-id="28646-343">b.</span><span class="sxs-lookup"><span data-stu-id="28646-343">b.</span></span> <span data-ttu-id="28646-344">Pour cette expérience, nos distributions d'étiquette cible ont été d’environ 1:1.</span><span class="sxs-lookup"><span data-stu-id="28646-344">For this experiment, our target label distributions were roughly 1:1.</span></span>

<span data-ttu-id="28646-345">L'instantané ci-dessous montre la distribution d’étiquettes de classe de pourboire pour le problème de classification binaire.</span><span class="sxs-lookup"><span data-stu-id="28646-345">The snapshot below shows the distribution of tip class labels for the binary classification problem.</span></span>

![Distribution d'étiquettes de classe de pourboire](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

<span data-ttu-id="28646-347">Par conséquent, nous obtenons une intégration de 0,987 comme indiqué dans la figure ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="28646-347">As a result, we obtain an AUC of 0.987 as shown in the figure below.</span></span>

![Valeur ASC](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

<span data-ttu-id="28646-349">**2. Classification multiclasse** : pour prédire le montant des pourboires réglés pour la course, en utilisant les classes précédemment définies.</span><span class="sxs-lookup"><span data-stu-id="28646-349">**2. Multiclass classification**: To predict the range of tip amounts paid for the trip, using the previously defined classes.</span></span>

<span data-ttu-id="28646-350">**Apprenant utilisé :** régression logistique multiclasse</span><span class="sxs-lookup"><span data-stu-id="28646-350">**Learner used:** Multiclass logistic regression</span></span>

<span data-ttu-id="28646-351">a.</span><span class="sxs-lookup"><span data-stu-id="28646-351">a.</span></span> <span data-ttu-id="28646-352">Pour ce problème, notre cible (ou classe) est « tip\_class », ce qui peut prendre une des cinq valeurs suivantes (0,1,2,3,4).</span><span class="sxs-lookup"><span data-stu-id="28646-352">For this problem, our target (or class) label is "tip\_class" which can take one of five values (0,1,2,3,4).</span></span> <span data-ttu-id="28646-353">Comme dans le cas de classification binaire, nous avons quelques colonnes qui sont des fuites cibles pour cette expérience.</span><span class="sxs-lookup"><span data-stu-id="28646-353">As in the binary classification case, we have a few columns that are target leaks for this experiment.</span></span> <span data-ttu-id="28646-354">En particulier : avec pourboire, tip\_amount et total\_amount révèlent des informations sur l’étiquette cible qui n’est pas disponible au moment du test.</span><span class="sxs-lookup"><span data-stu-id="28646-354">In particular : tipped, tip\_amount, total\_amount reveal information about the target label that is not available at testing time.</span></span> <span data-ttu-id="28646-355">Nous supprimons ces colonnes à l’aide du module [Sélectionner des colonnes dans le jeu de données][select-columns].</span><span class="sxs-lookup"><span data-stu-id="28646-355">We remove these columns using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="28646-356">L'instantané ci-dessous illustre notre expérience pour prédire le compartiment où un pourboire est susceptible de tomber (classe 0 : pourboire = 0 $, classe 1 : pourboire > 0 $ et pourboire <= 5 $, classe 2 : pourboire > 5 $ et pourboire <= 10 $, classe 3 : pourboire > 10 $ et pourboire <= 20 $, classe 4 : pourboire > 20 $)</span><span class="sxs-lookup"><span data-stu-id="28646-356">The snapshot below shows our experiment to predict in which bin a tip is likely to fall ( Class 0: tip = $0, class 1 : tip > $0 and tip <= $5, Class 2 : tip > $5 and tip <= $10, Class 3 : tip > $10 and tip <= $20, Class 4 : tip > $20)</span></span>

![Instantané de l’expérience](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

<span data-ttu-id="28646-358">Nous montrons maintenant à quoi ressemble notre distribution de classe test réelle.</span><span class="sxs-lookup"><span data-stu-id="28646-358">We now show what our actual test class distribution looks like.</span></span> <span data-ttu-id="28646-359">Nous voyons que la classe 0 et la classe 1 prévalent et que les autres classes sont rares.</span><span class="sxs-lookup"><span data-stu-id="28646-359">We see that while Class 0 and Class 1 are prevalent, the other classes are rare.</span></span>

![Distribution de classe de test](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

<span data-ttu-id="28646-361">b.</span><span class="sxs-lookup"><span data-stu-id="28646-361">b.</span></span> <span data-ttu-id="28646-362">Pour cette expérience, nous utilisons une matrice de confusion pour consulter la précision de nos prédictions.</span><span class="sxs-lookup"><span data-stu-id="28646-362">For this experiment, we use a confusion matrix to look at our prediction accuracies.</span></span> <span data-ttu-id="28646-363">Consultez l’illustration ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="28646-363">This is shown below.</span></span>

![Matrice de confusion](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

<span data-ttu-id="28646-365">Notez que la précision des classes sur les classes les plus courantes est assez bonne, mais que le modèle n'effectue pas un bon travail d’« apprentissage » sur les classes plus rares.</span><span class="sxs-lookup"><span data-stu-id="28646-365">Note that while our class accuracies on the prevalent classes is quite good, the model does not do a good job of "learning" on the rarer classes.</span></span>

<span data-ttu-id="28646-366">**3. Tâche de régression** : prédire le montant du pourboire versé pour une course.</span><span class="sxs-lookup"><span data-stu-id="28646-366">**3. Regression task**: To predict the amount of tip paid for a trip.</span></span>

<span data-ttu-id="28646-367">**Apprenant utilisé :** arbre de décision optimisé</span><span class="sxs-lookup"><span data-stu-id="28646-367">**Learner used:** Boosted decision tree</span></span>

<span data-ttu-id="28646-368">a.</span><span class="sxs-lookup"><span data-stu-id="28646-368">a.</span></span> <span data-ttu-id="28646-369">Pour ce problème, notre étiquette (ou classe) cible est « tip\_amount ».</span><span class="sxs-lookup"><span data-stu-id="28646-369">For this problem, our target (or class) label is "tip\_amount".</span></span> <span data-ttu-id="28646-370">Nos fuites cibles dans ce cas sont : avec pourboire, tip\_class, total\_amount. Toutes ces variables révèlent des informations sur le montant du pourboire qui est en général indisponible au moment du test.</span><span class="sxs-lookup"><span data-stu-id="28646-370">Our target leaks in this case are : tipped, tip\_class, total\_amount ; all these variables reveal information about the tip amount that is typically unavailable at testing time.</span></span> <span data-ttu-id="28646-371">Nous supprimons ces colonnes à l’aide du module [Sélectionner des colonnes dans le jeu de données][select-columns].</span><span class="sxs-lookup"><span data-stu-id="28646-371">We remove these columns using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="28646-372">L'instantané ci-dessous illustre notre expérience pour prédire la quantité de pourboire donné.</span><span class="sxs-lookup"><span data-stu-id="28646-372">The snapshot belows shows our experiment to predict the amount of the given tip.</span></span>

![Instantané de l’expérience](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

<span data-ttu-id="28646-374">b.</span><span class="sxs-lookup"><span data-stu-id="28646-374">b.</span></span> <span data-ttu-id="28646-375">Pour les problèmes de régression, nous évaluons la précision de nos prévisions en examinant l'erreur au carré dans les prévisions, le coefficient de détermination, etc.</span><span class="sxs-lookup"><span data-stu-id="28646-375">For regression problems, we measure the accuracies of our prediction by looking at the squared error in the predictions, the coefficient of determination, and the like.</span></span> <span data-ttu-id="28646-376">Nous présentons ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="28646-376">We show these below.</span></span>

![Statistiques de prédiction](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

<span data-ttu-id="28646-378">Nous voyons que le coefficient de détermination est de 0,709, ce qui signifie que 71 % environ de la variance est expliquée par nos coefficients modèles.</span><span class="sxs-lookup"><span data-stu-id="28646-378">We see that about the coefficient of determination is 0.709, implying about 71% of the variance is explained by our model coefficients.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="28646-379">Pour en savoir plus sur Azure Machine Learning, comment y accéder et comment l’utiliser, voir [Qu’est-ce que l’apprentissage automatique ?](machine-learning-what-is-machine-learning.md).</span><span class="sxs-lookup"><span data-stu-id="28646-379">To learn more about Azure Machine Learning and how to access and use it, please refer to [What's Machine Learning?](machine-learning-what-is-machine-learning.md).</span></span> <span data-ttu-id="28646-380">La [galerie Cortana Intelligence](https://gallery.cortanaintelligence.com/)est une ressource très utile pour découvrir de nombreuses expériences d’apprentissage automatique sur Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="28646-380">A very useful resource for playing with a bunch of Machine Learning experiments on Azure Machine Learning is the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).</span></span> <span data-ttu-id="28646-381">La galerie couvre une large gamme d'expériences et fournit une présentation approfondie des fonctionnalités d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="28646-381">The Gallery covers a gamut of experiments and provides a thorough introduction into the range of capabilities of Azure Machine Learning.</span></span>
> 
> 

## <a name="license-information"></a><span data-ttu-id="28646-382">Informations de licence</span><span class="sxs-lookup"><span data-stu-id="28646-382">License Information</span></span>
<span data-ttu-id="28646-383">Ce didacticiel et ses scripts associés sont partagés par Microsoft sous la licence MIT.</span><span class="sxs-lookup"><span data-stu-id="28646-383">This sample walkthrough and its accompanying scripts are shared by Microsoft under the MIT license.</span></span> <span data-ttu-id="28646-384">Pour plus d’informations, voir le fichier LICENSE.txt figurant dans le répertoire de l’exemple de code sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="28646-384">Please check the LICENSE.txt file in in the directory of the sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="28646-385">Références</span><span class="sxs-lookup"><span data-stu-id="28646-385">References</span></span>
<span data-ttu-id="28646-386">•    [Page de téléchargement des jeux de données NYC Taxi Trips par Andrés Monroy (en anglais)](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="28646-386">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="28646-387">•    [Page de partage des données relatives aux courses en taxi new-yorkais par Chris Whong (en anglais)](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="28646-387">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="28646-388">•    [Page de recherche et de statistiques de la Commission des services de taxis et de limousines de la ville de New York (en anglais)](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="28646-388">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
