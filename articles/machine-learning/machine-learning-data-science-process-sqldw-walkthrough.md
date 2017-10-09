---
title: "Hello processus de science des données équipe en action : à l’aide de l’entrepôt de données SQL | Documents Microsoft"
description: "Processus d’analyse avancé et technologie en action"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 88ba8e28-0bd7-49fe-8320-5dfa83b65724
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;hangzh;weig
ms.openlocfilehash: b1b6371583a023d32e33db59464cafd8c3b767d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-data-warehouse"></a><span data-ttu-id="0a49d-103">Hello processus de science des données équipe en action : à l’aide de l’entrepôt de données SQL</span><span class="sxs-lookup"><span data-stu-id="0a49d-103">hello Team Data Science Process in action: using SQL Data Warehouse</span></span>
<span data-ttu-id="0a49d-104">Dans ce didacticiel, nous vous guide dans la génération et le déploiement d’un modèle d’apprentissage automatique à l’aide de l’entrepôt de données SQL (SQL DW) pour un jeu de données disponible publiquement--hello [NYC Taxi allers-retours](http://www.andresmh.com/nyctaxitrips/) jeu de données.</span><span class="sxs-lookup"><span data-stu-id="0a49d-104">In this tutorial, we walk you through building and deploying a machine learning model using SQL Data Warehouse (SQL DW) for a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="0a49d-105">modèle de classification binaire Hello construit prédit ou non une info-bulle est payée pour un voyage, et les modèles de classification multiclasse et de régression sont également traités qui prédisent la distribution de hello pour les quantités de conseil hello payées.</span><span class="sxs-lookup"><span data-stu-id="0a49d-105">hello binary classification model constructed predicts whether or not a tip is paid for a trip, and models for multiclass classification and regression are also discussed that predict hello distribution for hello tip amounts paid.</span></span>

<span data-ttu-id="0a49d-106">procédure de Hello suit hello [processus de science des données équipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) flux de travail.</span><span class="sxs-lookup"><span data-stu-id="0a49d-106">hello procedure follows hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) workflow.</span></span> <span data-ttu-id="0a49d-107">Nous allons montrer comment toosetup un environnement de science des données, comment tooload hello des données dans l’entrepôt de données SQL et comment utiliser l’entrepôt de données SQL ou une toomodel de fonctionnalités notebooks bloc-notes tooexplore hello données et d’ingénierie à rebours.</span><span class="sxs-lookup"><span data-stu-id="0a49d-107">We show how toosetup a data science environment, how tooload hello data into SQL DW, and how use either SQL DW or an IPython Notebook tooexplore hello data and engineer features toomodel.</span></span> <span data-ttu-id="0a49d-108">Ensuite, nous montrons comment toobuild et déployer un modèle avec Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0a49d-108">We then show how toobuild and deploy a model with Azure Machine Learning.</span></span>

## <span data-ttu-id="0a49d-109"><a name="dataset"></a>jeu de données Hello NYC Taxi allers-retours</span><span class="sxs-lookup"><span data-stu-id="0a49d-109"><a name="dataset"></a>hello NYC Taxi Trips dataset</span></span>
<span data-ttu-id="0a49d-110">Hello les données NYC Taxi voyage se compose d’environ 20 Go de fichiers CSV compressées (Go ~ 48 non compressé), l’enregistrement de plus de 173 millions hello et des boucles tarifs payé pour chaque sortie.</span><span class="sxs-lookup"><span data-stu-id="0a49d-110">hello NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="0a49d-111">Chaque enregistrement de voyage inclut les emplacements de collecte et de remise de hello et de, présentées de façon anonyme hack numéro de licence (du pilote), hello nombre de medallion (id unique de taxi).</span><span class="sxs-lookup"><span data-stu-id="0a49d-111">Each trip record includes hello pickup and drop-off locations and times, anonymized hack (driver's) license number, and hello medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="0a49d-112">les données de salutation couvre toutes les boucles dans l’année hello 2013 et sont fournies dans hello suivant deux jeux de données pour chaque mois :</span><span class="sxs-lookup"><span data-stu-id="0a49d-112">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="0a49d-113">Hello **trip_data.csv** fichier contient les détails de voyage, telles que le nombre de personnes, points de collecte et cette chute, durée de voyage, longueur de voyage.</span><span class="sxs-lookup"><span data-stu-id="0a49d-113">hello **trip_data.csv** file contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="0a49d-114">Voici quelques exemples d’enregistrements :</span><span class="sxs-lookup"><span data-stu-id="0a49d-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="0a49d-115">Hello **trip_fare.csv** fichier contient les détails des prix hello payé pour chaque sortie, comme type de paiement, montant de frais, surcharge et taxes, conseils et péage et montant total de hello payé.</span><span class="sxs-lookup"><span data-stu-id="0a49d-115">hello **trip_fare.csv** file contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="0a49d-116">Voici quelques exemples d’enregistrements :</span><span class="sxs-lookup"><span data-stu-id="0a49d-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="0a49d-117">Hello **clé unique** utilisé toojoin voyage\_données et voyage\_tarif est composé de hello suivant trois champs :</span><span class="sxs-lookup"><span data-stu-id="0a49d-117">hello **unique key** used toojoin trip\_data and trip\_fare is composed of hello following three fields:</span></span>

* <span data-ttu-id="0a49d-118">medallion (médaillon),</span><span class="sxs-lookup"><span data-stu-id="0a49d-118">medallion,</span></span>
* <span data-ttu-id="0a49d-119">hack\_license (licence de taxi) et</span><span class="sxs-lookup"><span data-stu-id="0a49d-119">hack\_license and</span></span>
* <span data-ttu-id="0a49d-120">pickup\_datetime (date et heure d’embarquement).</span><span class="sxs-lookup"><span data-stu-id="0a49d-120">pickup\_datetime.</span></span>

## <span data-ttu-id="0a49d-121"><a name="mltasks"></a>Traiter trois types de tâches de prédiction</span><span class="sxs-lookup"><span data-stu-id="0a49d-121"><a name="mltasks"></a>Address three types of prediction tasks</span></span>
<span data-ttu-id="0a49d-122">Nous formuler à trois problèmes de prédiction selon hello *Conseil\_quantité* tooillustrate trois des types de tâches de modélisation :</span><span class="sxs-lookup"><span data-stu-id="0a49d-122">We formulate three prediction problems based on hello *tip\_amount* tooillustrate three kinds of modeling tasks:</span></span>

1. <span data-ttu-id="0a49d-123">**Classification binaire**: toopredict ou non un Conseil a été payé un voyage, c'est-à-dire un *Conseil\_quantité* qui est supérieur à $0 est un exemple positif, tandis qu’un *Conseil\_quantité* $ 0 est un exemple négatif.</span><span class="sxs-lookup"><span data-stu-id="0a49d-123">**Binary classification**: toopredict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="0a49d-124">**Classification multiclasse**: plage de hello toopredict d’info-bulle payé pour le voyage de hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-124">**Multiclass classification**: toopredict hello range of tip paid for hello trip.</span></span> <span data-ttu-id="0a49d-125">Nous allons diviser hello *Conseil\_quantité* dans les cinq conteneurs ou les classes :</span><span class="sxs-lookup"><span data-stu-id="0a49d-125">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="0a49d-126">**Tâche de régression**: toopredict hello d’info-bulle montant d’un voyage.</span><span class="sxs-lookup"><span data-stu-id="0a49d-126">**Regression task**: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="0a49d-127"><a name="setup"></a>Configuration d’environnement de science des données Azure hello pour analytique avancée</span><span class="sxs-lookup"><span data-stu-id="0a49d-127"><a name="setup"></a>Set up hello Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="0a49d-128">tooset de votre environnement pour la science des données Azure, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="0a49d-128">tooset up your Azure Data Science environment, follow these steps.</span></span>

<span data-ttu-id="0a49d-129">**Créez votre propre compte de stockage d’objets blob Azure**</span><span class="sxs-lookup"><span data-stu-id="0a49d-129">**Create your own Azure blob storage account**</span></span>

* <span data-ttu-id="0a49d-130">Lorsque vous configurez votre propre stockage d’objets blob Azure, choisissez un emplacement géographique pour le stockage d’objets blob Azure dans ou aussi près que possible trop**Amérique du Sud**, c'est-à-dire où est stockée les données NYC Taxi de hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-130">When you provision your own Azure blob storage, choose a geo-location for your Azure blob storage in or as close as possible too**South Central US**, which is where hello NYC Taxi data is stored.</span></span> <span data-ttu-id="0a49d-131">Hello données seront copiées à l’aide de AzCopy à partir du conteneur tooa conteneur de stockage d’objets blob publics hello dans votre propre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0a49d-131">hello data will be copied using AzCopy from hello public blob storage container tooa container in your own storage account.</span></span> <span data-ttu-id="0a49d-132">Hello rapprocher votre stockage d’objets blob Azure est tooSouth du centre des États-Unis, hello plus rapidement cette tâche (étape 4) se terminera.</span><span class="sxs-lookup"><span data-stu-id="0a49d-132">hello closer your Azure blob storage is tooSouth Central US, hello faster this task (Step 4) will be completed.</span></span>
* <span data-ttu-id="0a49d-133">compte de votre propre stockage Azure toocreate hello suivez la procédure décrite à [comptes de stockage sur Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="0a49d-133">toocreate your own Azure storage account, follow hello steps outlined at [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="0a49d-134">Être sûr de notes toomake sur les valeurs hello pour les informations d’identification de compte de stockage suivantes qu’ils sont reviendrez plus loin dans cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="0a49d-134">Be sure toomake notes on hello values for following storage account credentials as they will be needed later in this walkthrough.</span></span>
  
  * <span data-ttu-id="0a49d-135">**Nom du compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="0a49d-135">**Storage Account Name**</span></span>
  * <span data-ttu-id="0a49d-136">**Clé du compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="0a49d-136">**Storage Account Key**</span></span>
  * <span data-ttu-id="0a49d-137">**Nom du conteneur** (sur lequel vous voulez hello toobe de données stockée dans hello stockage d’objets blob Azure)</span><span class="sxs-lookup"><span data-stu-id="0a49d-137">**Container Name** (which you want hello data toobe stored in hello Azure blob storage)</span></span>

<span data-ttu-id="0a49d-138">**Approvisionnez votre instance Azure SQL DW.**</span><span class="sxs-lookup"><span data-stu-id="0a49d-138">**Provision your Azure SQL DW instance.**</span></span>
<span data-ttu-id="0a49d-139">Suivre la documentation hello à [créer un entrepôt de données SQL](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision une instance de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0a49d-139">Follow hello documentation at [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision a SQL Data Warehouse instance.</span></span> <span data-ttu-id="0a49d-140">Assurez-vous que vous notations sur hello suit les informations d’identification de l’entrepôt de données SQL qui seront utilisées dans les étapes ultérieures.</span><span class="sxs-lookup"><span data-stu-id="0a49d-140">Make sure that you make notations on hello following SQL Data Warehouse credentials which will be used in later steps.</span></span>

* <span data-ttu-id="0a49d-141">**Nom du serveur** : <server Name>.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="0a49d-141">**Server Name**: <server Name>.database.windows.net</span></span>
* <span data-ttu-id="0a49d-142">**Nom SQL DW (base de données)**</span><span class="sxs-lookup"><span data-stu-id="0a49d-142">**SQLDW (Database) Name**</span></span>
* <span data-ttu-id="0a49d-143">**Nom d’utilisateur**</span><span class="sxs-lookup"><span data-stu-id="0a49d-143">**Username**</span></span>
* <span data-ttu-id="0a49d-144">**Mot de passe**</span><span class="sxs-lookup"><span data-stu-id="0a49d-144">**Password**</span></span>

<span data-ttu-id="0a49d-145">**Installez Visual Studio et SQL Server Data Tools.**</span><span class="sxs-lookup"><span data-stu-id="0a49d-145">**Install Visual Studio and SQL Server Data Tools.**</span></span> <span data-ttu-id="0a49d-146">Pour connaître les instructions à suivre, consultez l’article [Installer Visual Studio 2015 et/ou SSDT pour SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="0a49d-146">For instructions, see [Install Visual Studio 2015 and/or SSDT (SQL Server Data Tools) for SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span></span>

<span data-ttu-id="0a49d-147">**Se connecter tooyour entrepôt de données SQL Azure avec Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="0a49d-147">**Connect tooyour Azure SQL DW with Visual Studio.**</span></span> <span data-ttu-id="0a49d-148">Pour obtenir des instructions, consultez les étapes 1 et 2 de [connecter tooAzure SQL Data Warehouse avec Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0a49d-148">For instructions, see steps 1 & 2 in [Connect tooAzure SQL Data Warehouse with Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0a49d-149">Exécution hello requête SQL sur la base de données hello que vous avez créé dans votre entrepôt de données SQL suivante (se connecter rubrique, au lieu de la requête de hello fournie à l’étape 3 de hello) trop**créer une clé principale**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-149">Run hello following SQL query on hello database you created in your SQL Data Warehouse (instead of hello query provided in step 3 of hello connect topic,) too**create a master key**.</span></span>
> 
> 

    BEGIN TRY
           --Try toocreate hello master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If hello master key exists, do nothing
    END CATCH;

<span data-ttu-id="0a49d-150">**Créez un espace de travail Azure Machine Learning dans votre abonnement Azure.**</span><span class="sxs-lookup"><span data-stu-id="0a49d-150">**Create an Azure Machine Learning workspace under your Azure subscription.**</span></span> <span data-ttu-id="0a49d-151">Pour connaître les instructions à suivre, consultez l’article [Création d’un espace de travail Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="0a49d-151">For instructions, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

## <span data-ttu-id="0a49d-152"><a name="getdata"></a>Charger des données de hello dans l’entrepôt de données SQL</span><span class="sxs-lookup"><span data-stu-id="0a49d-152"><a name="getdata"></a>Load hello data into SQL Data Warehouse</span></span>
<span data-ttu-id="0a49d-153">Ouvrez une console de commandes Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0a49d-153">Open a Windows PowerShell command console.</span></span> <span data-ttu-id="0a49d-154">Exécutez hello toodownload hello exemple fichiers de script SQL que nous partagent avec vous sur le répertoire local GitHub tooa que vous spécifiez avec le paramètre hello de commandes PowerShell *- DestDir*.</span><span class="sxs-lookup"><span data-stu-id="0a49d-154">Run hello following PowerShell commands toodownload hello example SQL script files that we share with you on GitHub tooa local directory that you specify with hello parameter *-DestDir*.</span></span> <span data-ttu-id="0a49d-155">Vous pouvez modifier la valeur hello du paramètre *- DestDir* tooany les répertoire local.</span><span class="sxs-lookup"><span data-stu-id="0a49d-155">You can change hello value of parameter *-DestDir* tooany local directory.</span></span> <span data-ttu-id="0a49d-156">Si *- DestDir* n’existe pas, il sera créé par hello script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0a49d-156">If *-DestDir* does not exist, it will be created by hello PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="0a49d-157">Vous devrez peut-être trop**exécuter en tant qu’administrateur** lors de l’exécution hello suite du script PowerShell si votre *DestDir* tooit toocreate ou toowrite du privilège administrateur a besoin de répertoire.</span><span class="sxs-lookup"><span data-stu-id="0a49d-157">You might need too**Run as Administrator** when executing hello following PowerShell script if your *DestDir* directory needs Administrator privilege toocreate or toowrite tooit.</span></span>
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

<span data-ttu-id="0a49d-158">Après l’exécution réussie, votre répertoire de travail actuel change également*- DestDir*.</span><span class="sxs-lookup"><span data-stu-id="0a49d-158">After successful execution, your current working directory changes too*-DestDir*.</span></span> <span data-ttu-id="0a49d-159">Vous devez pouvoir écran toosee comme ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0a49d-159">You should be able toosee screen like below:</span></span>

![][19]

<span data-ttu-id="0a49d-160">Dans votre *- DestDir*, exécutez hello script PowerShell en mode administrateur suivant :</span><span class="sxs-lookup"><span data-stu-id="0a49d-160">In your *-DestDir*, execute hello following PowerShell script in administrator mode:</span></span>

    ./SQLDW_Data_Import.ps1

<span data-ttu-id="0a49d-161">Lorsque hello script PowerShell s’exécute pour hello première fois, vous devez tooinput d’informations hello à partir de votre entrepôt de données SQL Azure et votre compte de stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="0a49d-161">When hello PowerShell script runs for hello first time, you will be asked tooinput hello information from your Azure SQL DW and your Azure blob storage account.</span></span> <span data-ttu-id="0a49d-162">À l’issue de ce script PowerShell en cours d’exécution pour hello première fois, les informations d’identification hello vous entrée auront été écrites le fichier de configuration tooa SQLDW.conf dans le répertoire de travail présent hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-162">When this PowerShell script completes running for hello first time, hello credentials you input will have been written tooa configuration file SQLDW.conf in hello present working directory.</span></span> <span data-ttu-id="0a49d-163">Hello futures l’exécution de ce fichier de script PowerShell a hello option tooread nécessaires tous les paramètres à partir de ce fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="0a49d-163">hello future run of this PowerShell script file has hello option tooread all needed parameters from this configuration file.</span></span> <span data-ttu-id="0a49d-164">Si vous devez toochange certains paramètres, vous pouvez choisir tooinput paramètres hello sur l’écran hello à l’invite en supprimant ce fichier de configuration et de saisie de valeurs de paramètres hello à l’invite ou des valeurs de paramètre toochange hello en modifiant le fichier de SQLDW.conf hello dans votre *- DestDir* active.</span><span class="sxs-lookup"><span data-stu-id="0a49d-164">If you need toochange some parameters, you can choose tooinput hello parameters on hello screen upon prompt by deleting this configuration file and inputting hello parameters values as prompted or toochange hello parameter values by editing hello SQLDW.conf file in your *-DestDir* directory.</span></span>

> [!NOTE]
> <span data-ttu-id="0a49d-165">Commande tooavoid schéma nom est en conflit avec ceux qui existent déjà dans votre entrepôt de données SQL Azure, lors de la lecture des paramètres directement à partir de fichiers de SQLDW.conf hello, un nombre aléatoire à 3 chiffres est ajouté toohello nom du schéma à partir du fichier de SQLDW.conf hello comme nom de schéma par défaut hello pour chaque exécution.</span><span class="sxs-lookup"><span data-stu-id="0a49d-165">In order tooavoid schema name conflicts with those that already exist in your Azure SQL DW, when reading parameters directly from hello SQLDW.conf file, a 3-digit random number is added toohello schema name from hello SQLDW.conf file as hello default schema name for each run.</span></span> <span data-ttu-id="0a49d-166">Hello script PowerShell peut vous inviter à entrer un nom de schéma : nom de hello peut être spécifiée à la discrétion de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0a49d-166">hello PowerShell script may prompt you for a schema name: hello name may be specified at user discretion.</span></span>
> 
> 

<span data-ttu-id="0a49d-167">Cela **script PowerShell** fichier termine hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="0a49d-167">This **PowerShell script** file completes hello following tasks:</span></span>

* <span data-ttu-id="0a49d-168">**Télécharge et installe AzCopy**, si AzCopy n’est pas déjà installé.</span><span class="sxs-lookup"><span data-stu-id="0a49d-168">**Downloads and installs AzCopy**, if AzCopy is not already installed</span></span>
  
        $AzCopy_path = SearchAzCopy
        if ($AzCopy_path -eq $null){
               Write-Host "AzCopy.exe is not found in C:\Program Files*. Now, start installing AzCopy..." -ForegroundColor "Yellow"
            InstallAzCopy
            $AzCopy_path = SearchAzCopy
        }
            $env_path = $env:Path
            for ($i=0; $i -lt $AzCopy_path.count; $i++){
                if ($AzCopy_path.count -eq 1){
                    $AzCopy_path_i = $AzCopy_path
                } else {
                    $AzCopy_path_i = $AzCopy_path[$i]
                }
                if ($env_path -notlike '*' +$AzCopy_path_i+'*'){
                    Write-Host $AzCopy_path_i 'not in system path, add it...'
                    [Environment]::SetEnvironmentVariable("Path", "$AzCopy_path_i;$env_path", "Machine")
                    $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
                    $env_path = $env:Path
                }
* <span data-ttu-id="0a49d-169">**Copie du compte de stockage de données tooyour blob privé** à partir de l’objet blob public de hello avec AzCopy</span><span class="sxs-lookup"><span data-stu-id="0a49d-169">**Copies data tooyour private blob storage account** from hello public blob with AzCopy</span></span>
  
        Write-Host "AzCopy is copying data from public blob tooyo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account tooverify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob tooyour storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* <span data-ttu-id="0a49d-170">**Charge les données à l’aide de Polybase (en exécutant LoadDataToSQLDW.sql) tooyour Azure SQL DW** à partir de votre compte de stockage d’objets blob privé avec hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="0a49d-170">**Loads data using Polybase (by executing LoadDataToSQLDW.sql) tooyour Azure SQL DW** from your private blob storage account with hello following commands.</span></span>
  
  * <span data-ttu-id="0a49d-171">Créer un schéma</span><span class="sxs-lookup"><span data-stu-id="0a49d-171">Create a schema</span></span>
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * <span data-ttu-id="0a49d-172">Créer un fichier d’informations d’identification de niveau base de données</span><span class="sxs-lookup"><span data-stu-id="0a49d-172">Create a database scoped credential</span></span>
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * <span data-ttu-id="0a49d-173">Créer une source de données externe pour un objet blob de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="0a49d-173">Create an external data source for an Azure storage blob</span></span>
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_trip_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_fare_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
  * <span data-ttu-id="0a49d-174">Créer un format de fichier externe pour un fichier csv.</span><span class="sxs-lookup"><span data-stu-id="0a49d-174">Create an external file format for a csv file.</span></span> <span data-ttu-id="0a49d-175">Données ne sont pas compressées et champs sont séparés par une barre verticale hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-175">Data is uncompressed and fields are separated with hello pipe character.</span></span>
    
          CREATE EXTERNAL FILE FORMAT {csv_file_format}
          WITH
          (   
              FORMAT_TYPE = DELIMITEDTEXT,
              FORMAT_OPTIONS  
              (
                  FIELD_TERMINATOR ='','',
                  USE_TYPE_DEFAULT = TRUE
              )
          )
          ;
  * <span data-ttu-id="0a49d-176">Créer des tables externes pour les prix et les courses correspondant au jeu de données NYC Taxi dans le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="0a49d-176">Create external fare and trip tables for NYC taxi dataset in Azure blob storage.</span></span>
    
          CREATE EXTERNAL TABLE {external_nyctaxi_fare}
          (
              medallion varchar(50) not null,
              hack_license varchar(50) not null,
              vendor_id char(3),
              pickup_datetime datetime not null,
              payment_type char(3),
              fare_amount float,
              surcharge float,
              mta_tax float,
              tip_amount float,
              tolls_amount float,
              total_amount float
          )
          with (
              LOCATION    = ''/nyctaxifare/'',
              DATA_SOURCE = {nyctaxi_fare_storage},
              FILE_FORMAT = {csv_file_format},
              REJECT_TYPE = VALUE,
              REJECT_VALUE = 12     
          )  

            CREATE EXTERNAL TABLE {external_nyctaxi_trip}
            (
                   medallion varchar(50) not null,
                   hack_license varchar(50)  not null,
                   vendor_id char(3),
                   rate_code char(3),
                   store_and_fwd_flag char(3),
                   pickup_datetime datetime  not null,
                   dropoff_datetime datetime,
                   passenger_count int,
                   trip_time_in_secs bigint,
                   trip_distance float,
                   pickup_longitude varchar(30),
                   pickup_latitude varchar(30),
                   dropoff_longitude varchar(30),
                   dropoff_latitude varchar(30)
            )
            with (
                LOCATION    = ''/nyctaxitrip/'',
                DATA_SOURCE = {nyctaxi_trip_storage},
                FILE_FORMAT = {csv_file_format},
                REJECT_TYPE = VALUE,
                REJECT_VALUE = 12         
            )

    - <span data-ttu-id="0a49d-177">Charger des données à partir des tables externes tooSQL de stockage d’objets blob Azure Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0a49d-177">Load data from external tables in Azure blob storage tooSQL Data Warehouse</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_fare}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_fare}
            ;

            CREATE TABLE {schemaname}.{nyctaxi_trip}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_trip}
            ;

    - <span data-ttu-id="0a49d-178">Créer un exemple de table de données (NYCTaxi_Sample) et insérez des données tooit à partir de la sélection des requêtes SQL portant sur les tables de voyage et tarif hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-178">Create a sample data table (NYCTaxi_Sample) and insert data tooit from selecting SQL queries on hello trip and fare tables.</span></span> <span data-ttu-id="0a49d-179">(Certaines étapes de cette procédure pas à pas doit toouse cette table d’exemple).</span><span class="sxs-lookup"><span data-stu-id="0a49d-179">(Some steps of this walkthrough needs toouse this sample table.)</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_sample}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            (
                SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount,
                tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
                tip_class = CASE
                        WHEN (tip_amount = 0) THEN 0
                        WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                        WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                        WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                        ELSE 4
                    END
                FROM {schemaname}.{nyctaxi_trip} t, {schemaname}.{nyctaxi_fare} f
                WHERE datepart("mi",t.pickup_datetime) = 1
                AND t.medallion = f.medallion
                AND   t.hack_license = f.hack_license
                AND   t.pickup_datetime = f.pickup_datetime
                AND   pickup_longitude <> ''0''
                AND   dropoff_longitude <> ''0''
            )
            ;

<span data-ttu-id="0a49d-180">emplacement géographique de Hello de vos comptes de stockage affecte le temps de chargement.</span><span class="sxs-lookup"><span data-stu-id="0a49d-180">hello geographic location of your storage accounts affects load times.</span></span>

> [!NOTE]
> <span data-ttu-id="0a49d-181">En fonction de l’emplacement géographique de hello de votre compte de stockage d’objets blob privé, hello les processus de copie des données à partir d’un compte de stockage privé tooyour objet blob public peuvent prend environ 15 minutes ou même plus, hello de processus et de chargement des données à partir de votre compte de stockage tooyour entrepôt de données SQL Azure peut prendre 20 minutes ou plus.</span><span class="sxs-lookup"><span data-stu-id="0a49d-181">Depending on hello geographical location of your private blob storage account, hello process of copying data from a public blob tooyour private storage account can take about 15 minutes, or even longer,and hello process of loading data from your storage account tooyour Azure SQL DW could take 20 minutes or longer.</span></span>  
> 
> 

<span data-ttu-id="0a49d-182">Vous devez toodecide que faire si vous avez une source en double et les fichiers de destination.</span><span class="sxs-lookup"><span data-stu-id="0a49d-182">You will have toodecide what do if you have duplicate source and destination files.</span></span>

> [!NOTE]
> <span data-ttu-id="0a49d-183">Si toobe de fichiers .csv hello provenant de compte de stockage blob privé hello blob publics stockage tooyour déjà existe dans votre compte de stockage d’objets blob privé, AzCopy vous demande si vous souhaitez toooverwrite les.</span><span class="sxs-lookup"><span data-stu-id="0a49d-183">If hello .csv files toobe copied from hello public blob storage tooyour private blob storage account already exist in your private blob storage account, AzCopy will ask you whether you want toooverwrite them.</span></span> <span data-ttu-id="0a49d-184">Si vous ne souhaitez pas toooverwrite leur, d’entrée  **n**  lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="0a49d-184">If you do not want toooverwrite them, input **n** when prompted.</span></span> <span data-ttu-id="0a49d-185">Si vous souhaitez toooverwrite **tous les** , entrée **un** lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="0a49d-185">If you want toooverwrite **all** of them, input **a** when prompted.</span></span> <span data-ttu-id="0a49d-186">Vous pouvez également entrer **y** toooverwrite .csv fichiers individuellement.</span><span class="sxs-lookup"><span data-stu-id="0a49d-186">You can also input **y** toooverwrite .csv files individually.</span></span>
> 
> 

![Diagramme n°21][21]

<span data-ttu-id="0a49d-188">Vous pouvez utiliser vos propres données.</span><span class="sxs-lookup"><span data-stu-id="0a49d-188">You can use your own data.</span></span> <span data-ttu-id="0a49d-189">Si les données de votre ordinateur local dans votre application de la vie réelle, vous pouvez toujours utiliser AzCopy tooupload local données tooyour privé Azure stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="0a49d-189">If your data is in your on-premises machine in your real life application, you can still use AzCopy tooupload on-premises data tooyour private Azure blob storage.</span></span> <span data-ttu-id="0a49d-190">Vous ne devez toochange hello **Source** emplacement, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, Bonjour commande AzCopy d’hello PowerShell script fichier toohello répertoire local qui contient vos données.</span><span class="sxs-lookup"><span data-stu-id="0a49d-190">You only need toochange hello **Source** location, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in hello AzCopy command of hello PowerShell script file toohello local directory that contains your data.</span></span>

> [!TIP]
> <span data-ttu-id="0a49d-191">Si vos données sont déjà dans votre stockage d’objets blob Azure privé dans votre application de la vie réelle, vous pouvez ignorer hello AzCopy étape Bonjour script PowerShell et le télécharger directement hello tooAzure de données SQL DW.</span><span class="sxs-lookup"><span data-stu-id="0a49d-191">If your data is already in your private Azure blob storage in your real life application, you can skip hello AzCopy step in hello PowerShell script and directly upload hello data tooAzure SQL DW.</span></span> <span data-ttu-id="0a49d-192">Vous devrez supplémentaires modifie de hello script tootailor format toohello de vos données.</span><span class="sxs-lookup"><span data-stu-id="0a49d-192">This will require additional edits of hello script tootailor it toohello format of your data.</span></span>
> 
> 

<span data-ttu-id="0a49d-193">Ce script Powershell se connecte également Bonjour informations de l’entrepôt de données SQL Azure dans hello exploration exemple des fichiers de données SQLDW_Explorations.sql, SQLDW_Explorations.ipynb et SQLDW_Explorations_Scripts.py afin que ces trois fichiers sont prêt toobe essayé instantanément une fois hello script PowerShell est terminée.</span><span class="sxs-lookup"><span data-stu-id="0a49d-193">This Powershell script also plugs in hello Azure SQL DW information into hello data exploration example files SQLDW_Explorations.sql, SQLDW_Explorations.ipynb, and SQLDW_Explorations_Scripts.py so that these three files are ready toobe tried out instantly after hello PowerShell script completes.</span></span>

<span data-ttu-id="0a49d-194">À l’issue d’une exécution réussie, un écran semblable à ce qui suit s’affiche :</span><span class="sxs-lookup"><span data-stu-id="0a49d-194">After a successful execution, you will see screen like below:</span></span>

![][20]

## <span data-ttu-id="0a49d-195"><a name="dbexplore"></a>Exploration des données et conception de fonctionnalités dans Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0a49d-195"><a name="dbexplore"></a>Data exploration and feature engineering in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="0a49d-196">Dans cette section, nous effectuons une exploration des données et une génération de caractéristiques en exécutant des requêtes SQL directement dans Azure SQL DW à l’aide de **Visual Studio Data Tools**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-196">In this section, we perform data exploration and feature generation by running SQL queries against Azure SQL DW directly using **Visual Studio Data Tools**.</span></span> <span data-ttu-id="0a49d-197">Toutes les requêtes SQL utilisées dans cette section se trouvent dans le script d’exemple hello nommé *SQLDW_Explorations.sql*.</span><span class="sxs-lookup"><span data-stu-id="0a49d-197">All SQL queries used in this section can be found in hello sample script named *SQLDW_Explorations.sql*.</span></span> <span data-ttu-id="0a49d-198">Ce fichier a déjà été téléchargé tooyour répertoire local par le script PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-198">This file has already been downloaded tooyour local directory by hello PowerShell script.</span></span> <span data-ttu-id="0a49d-199">Vous pouvez également le récupérer à partir de [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql),</span><span class="sxs-lookup"><span data-stu-id="0a49d-199">You can also retrieve it from [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span></span> <span data-ttu-id="0a49d-200">Mais, au fichier hello dans GitHub n’a pas d’informations d’entrepôt de données SQL Azure hello branchées.</span><span class="sxs-lookup"><span data-stu-id="0a49d-200">But hello file in GitHub does not have hello Azure SQL DW information plugged in.</span></span>

<span data-ttu-id="0a49d-201">Se connecter tooyour entrepôt de données SQL Azure à l’aide de Visual Studio avec le nom de connexion SQL DW hello et le mot de passe et ouvrez hello **l’Explorateur d’objets SQL** base de données tooconfirm hello et les tables qui ont été importés.</span><span class="sxs-lookup"><span data-stu-id="0a49d-201">Connect tooyour Azure SQL DW using Visual Studio with hello SQL DW login name and password and open up hello **SQL Object Explorer** tooconfirm hello database and tables have been imported.</span></span> <span data-ttu-id="0a49d-202">Récupérer hello *SQLDW_Explorations.sql* fichier.</span><span class="sxs-lookup"><span data-stu-id="0a49d-202">Retrieve hello *SQLDW_Explorations.sql* file.</span></span>

> [!NOTE]
> <span data-ttu-id="0a49d-203">tooopen un éditeur de requête Parallel Data Warehouse (PDW), utilisez hello **nouvelle requête** commande alors que votre PDW est sélectionné dans hello **l’Explorateur d’objets SQL**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-203">tooopen a Parallel Data Warehouse (PDW) query editor, use hello **New Query** command while your PDW is selected in hello **SQL Object Explorer**.</span></span> <span data-ttu-id="0a49d-204">éditeur de requête SQL standard Hello n’est pas pris en charge par PDW.</span><span class="sxs-lookup"><span data-stu-id="0a49d-204">hello standard SQL query editor is not supported by PDW.</span></span>
> 
> 

<span data-ttu-id="0a49d-205">Voici le type hello de données exploration et la fonctionnalité des tâches de génération effectuée dans cette section :</span><span class="sxs-lookup"><span data-stu-id="0a49d-205">Here are hello type of data exploration and feature generation tasks performed in this section:</span></span>

* <span data-ttu-id="0a49d-206">Explorer les distributions de données de quelques champs portant sur différentes périodes.</span><span class="sxs-lookup"><span data-stu-id="0a49d-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="0a49d-207">Analyser la qualité des données des champs de longitude et de latitude hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-207">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="0a49d-208">Générer des étiquettes de classification binaire et multiclasse selon hello **Conseil\_quantité**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-208">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="0a49d-209">Générer des fonctionnalités et calculer/comparer les distances des trajets.</span><span class="sxs-lookup"><span data-stu-id="0a49d-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="0a49d-210">Joindre hello deux tables et extraire un échantillon aléatoire qui sera utilisé toobuild modèles.</span><span class="sxs-lookup"><span data-stu-id="0a49d-210">Join hello two tables and extract a random sample that will be used toobuild models.</span></span>

### <a name="data-import-verification"></a><span data-ttu-id="0a49d-211">Vérification de l’importation des données</span><span class="sxs-lookup"><span data-stu-id="0a49d-211">Data import verification</span></span>
<span data-ttu-id="0a49d-212">Ces requêtes fournissent une vérification rapide du nombre de hello de lignes et colonnes Bonjour importer des tables remplis précédemment à l’aide de parallèle en bloc de Polybase,</span><span class="sxs-lookup"><span data-stu-id="0a49d-212">These queries provide a quick verification of hello number of rows and columns in hello tables populated earlier using Polybase's parallel bulk import,</span></span>

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

<span data-ttu-id="0a49d-213">**Sortie :** vous devez obtenir 173 179 759 lignes et 14 colonnes.</span><span class="sxs-lookup"><span data-stu-id="0a49d-213">**Output:** You should get 173,179,759 rows and 14 columns.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="0a49d-214">Exploration : distribution des courses par médaillon</span><span class="sxs-lookup"><span data-stu-id="0a49d-214">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="0a49d-215">Cet exemple de requête identifie des medallions hello (numéros taxi) qui s’est terminée de plus de 100 allers-retours au sein d’une période de temps.</span><span class="sxs-lookup"><span data-stu-id="0a49d-215">This example query identifies hello medallions (taxi numbers) that completed more than 100 trips within a specified time period.</span></span> <span data-ttu-id="0a49d-216">requête de Hello tireront parti d’accès à la table hello partitionnée, car il est conditionnée par le schéma de partition hello de **collecte\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-216">hello query would benefit from hello partitioned table access since it is conditioned by hello partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="0a49d-217">Interrogation du jeu de données complet hello rendent également utiliser de table partitionnée de hello et/ou d’analyse d’index.</span><span class="sxs-lookup"><span data-stu-id="0a49d-217">Querying hello full dataset will also make use of hello partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

<span data-ttu-id="0a49d-218">**Sortie :** hello de requêtes doit retourner une table avec des lignes en spécifiant le medallions hello 13,369 (taxi) et de hello nombre de voyage s’est terminée par ces derniers en 2013.</span><span class="sxs-lookup"><span data-stu-id="0a49d-218">**Output:** hello query should return a table with rows specifying hello 13,369 medallions (taxis) and hello number of trip completed by them in 2013.</span></span> <span data-ttu-id="0a49d-219">Hello dernière colonne contient les nombre hello de hello allers-retours s’est terminée.</span><span class="sxs-lookup"><span data-stu-id="0a49d-219">hello last column contains hello count of hello number of trips completed.</span></span>

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="0a49d-220">Exploration : distribution des courses par médaillon et par licence de taxi</span><span class="sxs-lookup"><span data-stu-id="0a49d-220">Exploration: Trip distribution by medallion and hack_license</span></span>
<span data-ttu-id="0a49d-221">Cet exemple identifie le medallions hello (numéros taxi) et hack_license des chiffres (pilotes) qui s’est terminée plus de 100 boucles dans un laps de temps spécifié.</span><span class="sxs-lookup"><span data-stu-id="0a49d-221">This example identifies hello medallions (taxi numbers) and hack_license numbers (drivers) that completed more than 100 trips within a specified time period.</span></span>

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

<span data-ttu-id="0a49d-222">**Sortie :** requête de hello doit retourner une table avec des 13,369 lignes spécifiant hello 13,369 voiture/pilote ID qui ont été effectuées plus que 100 allers-retours dans 2013.</span><span class="sxs-lookup"><span data-stu-id="0a49d-222">**Output:** hello query should return a table with 13,369 rows specifying hello 13,369 car/driver IDs that have completed more that 100 trips in 2013.</span></span> <span data-ttu-id="0a49d-223">Hello dernière colonne contient les nombre hello de hello allers-retours s’est terminée.</span><span class="sxs-lookup"><span data-stu-id="0a49d-223">hello last column contains hello count of hello number of trips completed.</span></span>

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="0a49d-224">Évaluation de la qualité des données : Vérifier les enregistrements indiquant une longitude et/ou une latitude incorrectes</span><span class="sxs-lookup"><span data-stu-id="0a49d-224">Data quality assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="0a49d-225">Cet exemple examine si un des champs de longitude et/ou latitude hello contenir une valeur non valide (les degrés en radians doivent être comprise entre -90 et 90), ou avoir (0, 0) coordonnées.</span><span class="sxs-lookup"><span data-stu-id="0a49d-225">This example investigates if any of hello longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

<span data-ttu-id="0a49d-226">**Sortie :** requête de hello retourne 837,467 boucles qui ont des champs de longitude ou de latitude non valides.</span><span class="sxs-lookup"><span data-stu-id="0a49d-226">**Output:** hello query returns 837,467 trips that have invalid longitude and/or latitude fields.</span></span>

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="0a49d-227">Exploration : Distribution des courses avec et sans pourboire</span><span class="sxs-lookup"><span data-stu-id="0a49d-227">Exploration: Tipped vs. not tipped trips distribution</span></span>
<span data-ttu-id="0a49d-228">Cet exemple recherche le nombre de hello d’allers-retours qui ont été déposés contre le nombre de hello qui ont été déposés pas dans un laps de temps spécifié (ou dans hello jeu de données complet si couvrant an hello comme il est défini ici).</span><span class="sxs-lookup"><span data-stu-id="0a49d-228">This example finds hello number of trips that were tipped vs. hello number that were not tipped in a specified time period (or in hello full dataset if covering hello full year as it is set up here).</span></span> <span data-ttu-id="0a49d-229">Cette distribution reflète hello étiquette binaire distribution toobe utilisée ultérieurement pour la modélisation de classification binaire.</span><span class="sxs-lookup"><span data-stu-id="0a49d-229">This distribution reflects hello binary label distribution toobe later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

<span data-ttu-id="0a49d-230">**Sortie :** hello requête doit suivant de retour hello Conseil fréquences pour l’année hello incliné 2013 : 90,447,622 et 82,264,709 a n’est pas.</span><span class="sxs-lookup"><span data-stu-id="0a49d-230">**Output:** hello query should return hello following tip frequencies for hello year 2013: 90,447,622 tipped and 82,264,709 not-tipped.</span></span>

### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="0a49d-231">Exploration : Distribution des classes/fourchettes de pourboires</span><span class="sxs-lookup"><span data-stu-id="0a49d-231">Exploration: Tip class/range distribution</span></span>
<span data-ttu-id="0a49d-232">Cet exemple calcule la distribution hello des plages de Conseil dans un délai donné période (ou dans hello jeu de données complet si couvrant an hello).</span><span class="sxs-lookup"><span data-stu-id="0a49d-232">This example computes hello distribution of tip ranges in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="0a49d-233">Il s’agit de distribution hello des classes d’étiquette hello qui sera utilisée ultérieurement pour la modélisation de classification multiclasse.</span><span class="sxs-lookup"><span data-stu-id="0a49d-233">This is hello distribution of hello label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

<span data-ttu-id="0a49d-234">**Output:**</span><span class="sxs-lookup"><span data-stu-id="0a49d-234">**Output:**</span></span>

| <span data-ttu-id="0a49d-235">tip_class</span><span class="sxs-lookup"><span data-stu-id="0a49d-235">tip_class</span></span> | <span data-ttu-id="0a49d-236">tip_freq</span><span class="sxs-lookup"><span data-stu-id="0a49d-236">tip_freq</span></span> |
| --- | --- |
| <span data-ttu-id="0a49d-237">1</span><span class="sxs-lookup"><span data-stu-id="0a49d-237">1</span></span> |<span data-ttu-id="0a49d-238">82230915</span><span class="sxs-lookup"><span data-stu-id="0a49d-238">82230915</span></span> |
| <span data-ttu-id="0a49d-239">2</span><span class="sxs-lookup"><span data-stu-id="0a49d-239">2</span></span> |<span data-ttu-id="0a49d-240">6198803</span><span class="sxs-lookup"><span data-stu-id="0a49d-240">6198803</span></span> |
| <span data-ttu-id="0a49d-241">3</span><span class="sxs-lookup"><span data-stu-id="0a49d-241">3</span></span> |<span data-ttu-id="0a49d-242">1932223</span><span class="sxs-lookup"><span data-stu-id="0a49d-242">1932223</span></span> |
| <span data-ttu-id="0a49d-243">0</span><span class="sxs-lookup"><span data-stu-id="0a49d-243">0</span></span> |<span data-ttu-id="0a49d-244">82264625</span><span class="sxs-lookup"><span data-stu-id="0a49d-244">82264625</span></span> |
| <span data-ttu-id="0a49d-245">4</span><span class="sxs-lookup"><span data-stu-id="0a49d-245">4</span></span> |<span data-ttu-id="0a49d-246">85765</span><span class="sxs-lookup"><span data-stu-id="0a49d-246">85765</span></span> |

### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="0a49d-247">Exploration : Calculer et comparer les distances des courses</span><span class="sxs-lookup"><span data-stu-id="0a49d-247">Exploration: Compute and compare trip distance</span></span>
<span data-ttu-id="0a49d-248">L’exemple suivant convertit la longitude de collecte et de remise hello et latitude tooSQL geography pointe, calcule la distance de voyage hello à l’aide de la différence de points SQL geography et retourne un échantillon aléatoire de résultats hello pour la comparaison.</span><span class="sxs-lookup"><span data-stu-id="0a49d-248">This example converts hello pickup and drop-off longitude and latitude tooSQL geography points, computes hello trip distance using SQL geography points difference, and returns a random sample of hello results for comparison.</span></span> <span data-ttu-id="0a49d-249">exemple de Hello limite les résultats de hello toovalid coordonne uniquement à l’aide de la requête d’évaluation de la qualité des données d’hello évoqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="0a49d-249">hello example limits hello results toovalid coordinates only using hello data quality assessment query covered earlier.</span></span>

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function toocalculate hello direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

### <a name="feature-engineering-using-sql-functions"></a><span data-ttu-id="0a49d-250">Conception de fonctionnalités à l’aide de fonctions SQL</span><span class="sxs-lookup"><span data-stu-id="0a49d-250">Feature engineering using SQL functions</span></span>
<span data-ttu-id="0a49d-251">Les fonctions SQL peuvent parfois s’avérer efficaces pour la conception des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="0a49d-251">Sometimes SQL functions can be an efficient option for feature engineering.</span></span> <span data-ttu-id="0a49d-252">Dans cette procédure pas à pas, nous avons défini une SQL fonction toocalculate hello distance directe entre les emplacements de collecte et de cette chute de hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-252">In this walkthrough, we defined a SQL function toocalculate hello direct distance between hello pickup and dropoff locations.</span></span> <span data-ttu-id="0a49d-253">Vous pouvez exécuter hello suivant des scripts SQL dans **outils de données Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-253">You can run hello following SQL scripts in **Visual Studio Data Tools**.</span></span>

<span data-ttu-id="0a49d-254">Voici le script SQL hello qui définit la fonction de distance hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-254">Here is hello SQL script that defines hello distance function.</span></span>

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate hello direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

<span data-ttu-id="0a49d-255">Voici un exemple toocall cette fonctionnalités toogenerate de fonction dans votre requête SQL :</span><span class="sxs-lookup"><span data-stu-id="0a49d-255">Here is an example toocall this function toogenerate features in your SQL query:</span></span>

    -- Sample query toocall hello function toocreate features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="0a49d-256">**Sortie :** cette requête génère une table (avec des 2,803,538 lignes) avec la collecte et cette chute de latitude et de dirigent les distances en miles longitudes et hello correspondant.</span><span class="sxs-lookup"><span data-stu-id="0a49d-256">**Output:** This query generates a table (with 2,803,538 rows) with pickup and dropoff latitudes and longitudes and hello corresponding direct distances in miles.</span></span> <span data-ttu-id="0a49d-257">Voici les résultats de hello pour les 3 premiers lignes :</span><span class="sxs-lookup"><span data-stu-id="0a49d-257">Here are hello results for first 3 rows:</span></span>

|  | <span data-ttu-id="0a49d-258">pickup_latitude</span><span class="sxs-lookup"><span data-stu-id="0a49d-258">pickup_latitude</span></span> | <span data-ttu-id="0a49d-259">pickup_longitude</span><span class="sxs-lookup"><span data-stu-id="0a49d-259">pickup_longitude</span></span> | <span data-ttu-id="0a49d-260">dropoff_latitude</span><span class="sxs-lookup"><span data-stu-id="0a49d-260">dropoff_latitude</span></span> | <span data-ttu-id="0a49d-261">dropoff_longitude</span><span class="sxs-lookup"><span data-stu-id="0a49d-261">dropoff_longitude</span></span> | <span data-ttu-id="0a49d-262">DirectDistance</span><span class="sxs-lookup"><span data-stu-id="0a49d-262">DirectDistance</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="0a49d-263">1</span><span class="sxs-lookup"><span data-stu-id="0a49d-263">1</span></span> |<span data-ttu-id="0a49d-264">40,731804</span><span class="sxs-lookup"><span data-stu-id="0a49d-264">40.731804</span></span> |<span data-ttu-id="0a49d-265">-74,001083</span><span class="sxs-lookup"><span data-stu-id="0a49d-265">-74.001083</span></span> |<span data-ttu-id="0a49d-266">40,736622</span><span class="sxs-lookup"><span data-stu-id="0a49d-266">40.736622</span></span> |<span data-ttu-id="0a49d-267">-73,988953</span><span class="sxs-lookup"><span data-stu-id="0a49d-267">-73.988953</span></span> |<span data-ttu-id="0a49d-268">0,7169601222</span><span class="sxs-lookup"><span data-stu-id="0a49d-268">.7169601222</span></span> |
| <span data-ttu-id="0a49d-269">2</span><span class="sxs-lookup"><span data-stu-id="0a49d-269">2</span></span> |<span data-ttu-id="0a49d-270">40,715794</span><span class="sxs-lookup"><span data-stu-id="0a49d-270">40.715794</span></span> |<span data-ttu-id="0a49d-271">-74,010635</span><span class="sxs-lookup"><span data-stu-id="0a49d-271">-74,010635</span></span> |<span data-ttu-id="0a49d-272">40,725338</span><span class="sxs-lookup"><span data-stu-id="0a49d-272">40.725338</span></span> |<span data-ttu-id="0a49d-273">-74,00399</span><span class="sxs-lookup"><span data-stu-id="0a49d-273">-74.00399</span></span> |<span data-ttu-id="0a49d-274">0,7448343721</span><span class="sxs-lookup"><span data-stu-id="0a49d-274">.7448343721</span></span> |
| <span data-ttu-id="0a49d-275">3</span><span class="sxs-lookup"><span data-stu-id="0a49d-275">3</span></span> |<span data-ttu-id="0a49d-276">40.761456</span><span class="sxs-lookup"><span data-stu-id="0a49d-276">40.761456</span></span> |<span data-ttu-id="0a49d-277">-73.999886</span><span class="sxs-lookup"><span data-stu-id="0a49d-277">-73.999886</span></span> |<span data-ttu-id="0a49d-278">40.766544</span><span class="sxs-lookup"><span data-stu-id="0a49d-278">40.766544</span></span> |<span data-ttu-id="0a49d-279">-73.988228</span><span class="sxs-lookup"><span data-stu-id="0a49d-279">-73.988228</span></span> |<span data-ttu-id="0a49d-280">0,7037227967</span><span class="sxs-lookup"><span data-stu-id="0a49d-280">0.7037227967</span></span> |

### <a name="prepare-data-for-model-building"></a><span data-ttu-id="0a49d-281">Préparer les données pour la création de modèles</span><span class="sxs-lookup"><span data-stu-id="0a49d-281">Prepare data for model building</span></span>
<span data-ttu-id="0a49d-282">hello de jointures de requête suivant de Hello **nyctaxi\_voyage** et **nyctaxi\_tarif** des tables, génère une étiquette de classification binaire **incliné**, un étiquette de classification multiclasse **Conseil\_classe**et extrait un échantillon de jeu de données joint hello complète.</span><span class="sxs-lookup"><span data-stu-id="0a49d-282">hello following query joins hello **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a sample from hello full joined dataset.</span></span> <span data-ttu-id="0a49d-283">échantillonnage de Hello est effectuée par la récupération d’un sous-ensemble des allers-retours hello selon l’heure de collecte.</span><span class="sxs-lookup"><span data-stu-id="0a49d-283">hello sampling is done by retrieving a subset of hello trips based on pickup time.</span></span>  <span data-ttu-id="0a49d-284">Cette requête peut être copiée, puis collée directement dans hello [Azure Machine Learning Studio](https://studio.azureml.net) [importer des données] [ import-data] module pour l’ingestion de données directement à partir de l’instance de base de données SQL hello dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0a49d-284">This query can be copied then pasted directly in hello [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from hello SQL database instance in Azure.</span></span> <span data-ttu-id="0a49d-285">requête de Hello exclut les enregistrements avec incorrect (0, 0) coordonnées.</span><span class="sxs-lookup"><span data-stu-id="0a49d-285">hello query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
    WHERE datepart("mi",t.pickup_datetime) = 1
    AND   t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="0a49d-286">Lorsque vous êtes prêt tooproceed tooAzure Machine Learning, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="0a49d-286">When you are ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="0a49d-287">Enregistrer hello final SQL requête tooextract et exemple hello données et copier-coller hello requête directement dans un [importer des données] [ import-data] module dans Azure Machine Learning, ou</span><span class="sxs-lookup"><span data-stu-id="0a49d-287">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="0a49d-288">Conserver hello échantillonnée et données ingénieries que vous prévoyez toouse pour un nouvel entrepôt de données SQL de création de modèles de table et utilisent la nouvelle table de hello Bonjour [importer des données] [ import-data] module dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0a49d-288">Persist hello sampled and engineered data you plan toouse for model building in a new SQL DW table and use hello new table in hello [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="0a49d-289">Hello script PowerShell à l’étape précédente a fait cela pour vous.</span><span class="sxs-lookup"><span data-stu-id="0a49d-289">hello PowerShell script in earlier step has done this for you.</span></span> <span data-ttu-id="0a49d-290">Vous pouvez lire directement à partir de cette table dans le module d’importation de données hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-290">You can read directly from this table in hello Import Data module.</span></span>

## <span data-ttu-id="0a49d-291"><a name="ipnb"></a>Exploration des données et conception de fonctionnalités dans IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="0a49d-291"><a name="ipnb"></a>Data exploration and feature engineering in IPython notebook</span></span>
<span data-ttu-id="0a49d-292">Dans cette section, nous allons effectuer l’exploration de données et de génération de fonctionnalité à l’aide de deux Python et des requêtes SQL sur hello SQL DW créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="0a49d-292">In this section, we will perform data exploration and feature generation using both Python and SQL queries against hello SQL DW created earlier.</span></span> <span data-ttu-id="0a49d-293">Un bloc-notes de notebooks exemple nommé **SQLDW_Explorations.ipynb** et un fichier de script Python **SQLDW_Explorations_Scripts.py** ont été téléchargés tooyour les répertoire local.</span><span class="sxs-lookup"><span data-stu-id="0a49d-293">A sample IPython notebook named **SQLDW_Explorations.ipynb** and a Python script file **SQLDW_Explorations_Scripts.py** have been downloaded tooyour local directory.</span></span> <span data-ttu-id="0a49d-294">Ils sont également disponibles sur [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span><span class="sxs-lookup"><span data-stu-id="0a49d-294">They are also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span></span> <span data-ttu-id="0a49d-295">Ces deux fichiers sont identiques dans les scripts Python.</span><span class="sxs-lookup"><span data-stu-id="0a49d-295">These two files are identical in Python scripts.</span></span> <span data-ttu-id="0a49d-296">fichier de script Python Hello est fourni tooyou au cas où vous ne disposez pas d’un serveur de notebooks bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="0a49d-296">hello Python script file is provided tooyou in case you do not have an IPython Notebook server.</span></span> <span data-ttu-id="0a49d-297">Ces deux exemples de fichier Python sont conçus sous **Python 2.7**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-297">These two sample Python files are designed under **Python 2.7**.</span></span>

<span data-ttu-id="0a49d-298">Hello les informations d’entrepôt de données SQL Azure nécessaires dans l’exemple hello notebooks bloc-notes et hello Python ordinateur local de script fichier tooyour téléchargé a été branché par script PowerShell de hello précédemment.</span><span class="sxs-lookup"><span data-stu-id="0a49d-298">hello needed Azure SQL DW information in hello sample IPython Notebook and hello Python script file downloaded tooyour local machine has been plugged in by hello PowerShell script previously.</span></span> <span data-ttu-id="0a49d-299">Elles peuvent être exécutées sans aucune modification.</span><span class="sxs-lookup"><span data-stu-id="0a49d-299">They are executable without any modification.</span></span>

<span data-ttu-id="0a49d-300">Si vous avez déjà configuré un espace de travail AzureML, vous pouvez directement télécharger l’exemple hello service de AzureML notebooks bloc-notes toohello notebooks portable et commencer à l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="0a49d-300">If you have already set up an AzureML workspace, you can directly upload hello sample IPython Notebook toohello AzureML IPython Notebook service and start running it.</span></span> <span data-ttu-id="0a49d-301">Voici hello étapes tooupload tooAzureML service des notebooks bloc-notes :</span><span class="sxs-lookup"><span data-stu-id="0a49d-301">Here are hello steps tooupload tooAzureML IPython Notebook service:</span></span>

1. <span data-ttu-id="0a49d-302">Ouvrez une session dans l’espace de travail tooyour AzureML et cliquez sur « Studio » en haut de hello, cliquez sur « Ordinateurs portables » sur le côté gauche de hello de page web de hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-302">Log in tooyour AzureML workspace, click "Studio" at hello top, and click "NOTEBOOKS" on hello left side of hello web page.</span></span>
   
    ![Diagramme n°22][22]
2. <span data-ttu-id="0a49d-304">Cliquez sur « Nouveau » dans le coin inférieur gauche de hello de hello web page, puis sélectionnez « Python 2 ».</span><span class="sxs-lookup"><span data-stu-id="0a49d-304">Click "NEW" on hello left bottom corner of hello web page, and select "Python 2".</span></span> <span data-ttu-id="0a49d-305">Ensuite, un ordinateur portable toohello de nom et cliquez sur hello coche toocreate hello vierge notebooks bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="0a49d-305">Then, provide a name toohello notebook and click hello check mark toocreate hello new blank IPython Notebook.</span></span>
   
    ![Diagramme n°23][23]
3. <span data-ttu-id="0a49d-307">Cliquez sur symboles de « Notebook » hello sur le coin supérieur gauche de hello Hello notebooks bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="0a49d-307">Click hello "Jupyter" symbol on hello left top corner of hello new IPython Notebook.</span></span>
   
    ![Diagramme n°24][24]
4. <span data-ttu-id="0a49d-309">Faites glisser et déposez hello exemple notebooks bloc-notes toohello **arborescence** page de votre service de AzureML notebooks bloc-notes, puis cliquez sur **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-309">Drag and drop hello sample IPython Notebook toohello **tree** page of your AzureML IPython Notebook service, and click **Upload**.</span></span> <span data-ttu-id="0a49d-310">Ensuite, l’exemple hello notebooks bloc-notes sera téléchargé toohello service de AzureML notebooks bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="0a49d-310">Then, hello sample IPython Notebook will be uploaded toohello AzureML IPython Notebook service.</span></span>
   
    ![Diagramme n°25][25]

<span data-ttu-id="0a49d-312">Bonjour toorun de commande exemple notebooks bloc-notes ou hello du fichier de script Python, hello Python packages suivants sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="0a49d-312">In order toorun hello sample IPython Notebook or hello Python script file, hello following Python packages are needed.</span></span> <span data-ttu-id="0a49d-313">Si vous utilisez le service de AzureML notebooks bloc-notes hello, ces packages ont été préinstallés.</span><span class="sxs-lookup"><span data-stu-id="0a49d-313">If you are using hello AzureML IPython Notebook service, these packages have been pre-installed.</span></span>

    - <span data-ttu-id="0a49d-314">pandas</span><span class="sxs-lookup"><span data-stu-id="0a49d-314">pandas</span></span>
    - <span data-ttu-id="0a49d-315">numpy</span><span class="sxs-lookup"><span data-stu-id="0a49d-315">numpy</span></span>
    - <span data-ttu-id="0a49d-316">matplotlib</span><span class="sxs-lookup"><span data-stu-id="0a49d-316">matplotlib</span></span>
    - <span data-ttu-id="0a49d-317">pyodbc</span><span class="sxs-lookup"><span data-stu-id="0a49d-317">pyodbc</span></span>
    - <span data-ttu-id="0a49d-318">PyTables</span><span class="sxs-lookup"><span data-stu-id="0a49d-318">PyTables</span></span>

<span data-ttu-id="0a49d-319">Hello séquence recommandée lors de la génération des solutions analytiques avancées sur AzureML avec des données volumineuses est suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="0a49d-319">hello recommended sequence when building advanced analytical solutions on AzureML with large data is hello following:</span></span>

* <span data-ttu-id="0a49d-320">Lire dans un petit échantillon de données de salutation dans une trame de données en mémoire.</span><span class="sxs-lookup"><span data-stu-id="0a49d-320">Read in a small sample of hello data into an in-memory data frame.</span></span>
* <span data-ttu-id="0a49d-321">Effectuer des visualisations et à l’aide des explorations hello données échantillonnées.</span><span class="sxs-lookup"><span data-stu-id="0a49d-321">Perform some visualizations and explorations using hello sampled data.</span></span>
* <span data-ttu-id="0a49d-322">Faites l’expérience de l’ingénierie de fonctionnalité à l’aide de hello exemples de données.</span><span class="sxs-lookup"><span data-stu-id="0a49d-322">Experiment with feature engineering using hello sampled data.</span></span>
* <span data-ttu-id="0a49d-323">Pour l’exploration de données plus volumineuse, l’ingénierie de fonctionnalité et de manipulation de données utiliser Python tooissue SQL requêtes directement sur hello SQL DW.</span><span class="sxs-lookup"><span data-stu-id="0a49d-323">For larger data exploration, data manipulation and feature engineering, use Python tooissue SQL Queries directly against hello SQL DW.</span></span>
* <span data-ttu-id="0a49d-324">Décidez hello exemple taille toobe approprié pour la construction d’un modèle Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0a49d-324">Decide hello sample size toobe suitable for Azure Machine Learning model building.</span></span>

<span data-ttu-id="0a49d-325">Hello trouverez ci-dessous quelques exemples ingénierie de fonctionnalité, l’exploration de données et visualisation des données.</span><span class="sxs-lookup"><span data-stu-id="0a49d-325">hello followings are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="0a49d-326">Vous trouverez plus d’explorations de données dans l’exemple hello notebooks bloc-notes et fichier de script Python exemple hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-326">More data explorations can be found in hello sample IPython Notebook and hello sample Python script file.</span></span>

### <a name="initialize-database-credentials"></a><span data-ttu-id="0a49d-327">Initialiser les informations d’identification de la base de données</span><span class="sxs-lookup"><span data-stu-id="0a49d-327">Initialize database credentials</span></span>
<span data-ttu-id="0a49d-328">Initialiser vos paramètres de connexion de base de données Bonjour suivant variables :</span><span class="sxs-lookup"><span data-stu-id="0a49d-328">Initialize your database connection settings in hello following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a><span data-ttu-id="0a49d-329">Créer une connexion à la base de données</span><span class="sxs-lookup"><span data-stu-id="0a49d-329">Create database connection</span></span>
<span data-ttu-id="0a49d-330">Voici la chaîne de connexion hello qui crée la base de données toohello hello connexion.</span><span class="sxs-lookup"><span data-stu-id="0a49d-330">Here is hello connection string that creates hello connection toohello database.</span></span>

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="0a49d-331">Afficher le nombre de lignes et de colonnes de la table <nyctaxi_trip></span><span class="sxs-lookup"><span data-stu-id="0a49d-331">Report number of rows and columns in table <nyctaxi_trip></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_trip>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="0a49d-332">Nombre total de lignes = 173 179 759</span><span class="sxs-lookup"><span data-stu-id="0a49d-332">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="0a49d-333">Nombre total de colonnes = 14</span><span class="sxs-lookup"><span data-stu-id="0a49d-333">Total number of columns = 14</span></span>

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a><span data-ttu-id="0a49d-334">Afficher le nombre de lignes et de colonnes de la table <nyctaxi_fare></span><span class="sxs-lookup"><span data-stu-id="0a49d-334">Report number of rows and columns in table <nyctaxi_fare></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_fare>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_fare>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="0a49d-335">Nombre total de lignes = 173 179 759</span><span class="sxs-lookup"><span data-stu-id="0a49d-335">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="0a49d-336">Nombre total de colonnes = 11</span><span class="sxs-lookup"><span data-stu-id="0a49d-336">Total number of columns = 11</span></span>

### <a name="read-in-a-small-data-sample-from-hello-sql-data-warehouse-database"></a><span data-ttu-id="0a49d-337">Lecture dans un échantillon de données de petite taille à partir de hello de base de données de l’entrepôt de données SQL</span><span class="sxs-lookup"><span data-stu-id="0a49d-337">Read-in a small data sample from hello SQL Data Warehouse Database</span></span>
    t0 = time.time()

    query = '''
        SELECT TOP 10000 t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
        WHERE datepart("mi",t.pickup_datetime) = 1
        AND   t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="0a49d-338">Table d’exemple hello temps tooread est 14.096495 secondes.</span><span class="sxs-lookup"><span data-stu-id="0a49d-338">Time tooread hello sample table is 14.096495 seconds.</span></span>  
<span data-ttu-id="0a49d-339">Nombre de lignes et de colonnes récupérées = (1000, 21)</span><span class="sxs-lookup"><span data-stu-id="0a49d-339">Number of rows and columns retrieved = (1000, 21).</span></span>

### <a name="descriptive-statistics"></a><span data-ttu-id="0a49d-340">Statistiques descriptives</span><span class="sxs-lookup"><span data-stu-id="0a49d-340">Descriptive statistics</span></span>
<span data-ttu-id="0a49d-341">Vous êtes maintenant données hello échantillonnée de tooexplore prêt.</span><span class="sxs-lookup"><span data-stu-id="0a49d-341">Now you are ready tooexplore hello sampled data.</span></span> <span data-ttu-id="0a49d-342">Nous allons commencer par envisager des statistiques descriptives pour hello **voyage\_distance** (ou tous les autres champs que vous choisissez toospecify).</span><span class="sxs-lookup"><span data-stu-id="0a49d-342">We start with looking at some descriptive statistics for hello **trip\_distance** (or any other fields you choose toospecify).</span></span>

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a><span data-ttu-id="0a49d-343">Visualisation : Exemple de diagramme à surfaces</span><span class="sxs-lookup"><span data-stu-id="0a49d-343">Visualization: Box plot example</span></span>
<span data-ttu-id="0a49d-344">Ensuite, nous allons examiner les surfaces hello pour hello voyage distance toovisualize hello quantiles.</span><span class="sxs-lookup"><span data-stu-id="0a49d-344">Next we look at hello box plot for hello trip distance toovisualize hello quantiles.</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Diagramme #1][1]

### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="0a49d-346">Visualisation : Exemple de diagramme de distribution</span><span class="sxs-lookup"><span data-stu-id="0a49d-346">Visualization: Distribution plot example</span></span>
<span data-ttu-id="0a49d-347">Les tracés visualiser la distribution de hello et un histogramme pour hello échantillonnées distances de voyage.</span><span class="sxs-lookup"><span data-stu-id="0a49d-347">Plots that visualize hello distribution and a histogram for hello sampled trip distances.</span></span>

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Diagramme #2][2]

### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="0a49d-349">Visualisation : Diagrammes en bâtons et linéaires</span><span class="sxs-lookup"><span data-stu-id="0a49d-349">Visualization: Bar and line plots</span></span>
<span data-ttu-id="0a49d-350">Dans cet exemple, nous bin distance de voyage hello dans cinq compartiments et visualiser hello placement des résultats.</span><span class="sxs-lookup"><span data-stu-id="0a49d-350">In this example, we bin hello trip distance into five bins and visualize hello binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="0a49d-351">Nous pouvons tracer hello au-dessus de distribution d’emplacement dans une barre ou ligne de traçage avec :</span><span class="sxs-lookup"><span data-stu-id="0a49d-351">We can plot hello above bin distribution in a bar or line plot with:</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Diagramme #3][3]

<span data-ttu-id="0a49d-353">and</span><span class="sxs-lookup"><span data-stu-id="0a49d-353">and</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Diagramme #4][4]

### <a name="visualization-scatterplot-examples"></a><span data-ttu-id="0a49d-355">Visualisation : Exemples de nuage de points</span><span class="sxs-lookup"><span data-stu-id="0a49d-355">Visualization: Scatterplot examples</span></span>
<span data-ttu-id="0a49d-356">Nous allons montrer nuage entre **voyage\_temps\_dans\_secondes** et **voyage\_distance** toosee s’il existe une corrélation</span><span class="sxs-lookup"><span data-stu-id="0a49d-356">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** toosee if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Diagramme #6][6]

<span data-ttu-id="0a49d-358">De même, nous pouvons vérifier relation hello entre **taux\_code** et **voyage\_distance**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-358">Similarly we can check hello relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Diagramme #8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="0a49d-360">Exploration des données échantillonnées à l’aide de requêtes SQL dans IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="0a49d-360">Data exploration on sampled data using SQL queries in IPython notebook</span></span>
<span data-ttu-id="0a49d-361">Dans cette section, nous explorons les distributions de données à l’aide de données hello échantillonnée qui sont conservées dans hello nouvelle table créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="0a49d-361">In this section, we explore data distributions using hello sampled data which is persisted in hello new table we created above.</span></span> <span data-ttu-id="0a49d-362">Notez que des explorations similaire peuvent être effectuées à l’aide de tables d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-362">Note that similar explorations can be performed using hello original tables.</span></span>

#### <a name="exploration-report-number-of-rows-and-columns-in-hello-sampled-table"></a><span data-ttu-id="0a49d-363">Exploration : Nombre de rapports de lignes et colonnes Bonjour échantillonnées table</span><span class="sxs-lookup"><span data-stu-id="0a49d-363">Exploration: Report number of rows and columns in hello sampled table</span></span>
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a><span data-ttu-id="0a49d-364">Exploration : Distribution avec et sans pourboire</span><span class="sxs-lookup"><span data-stu-id="0a49d-364">Exploration: Tipped/not tripped Distribution</span></span>
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a><span data-ttu-id="0a49d-365">Exploration : Distribution des classes de pourboires</span><span class="sxs-lookup"><span data-stu-id="0a49d-365">Exploration: Tip class distribution</span></span>
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-hello-tip-distribution-by-class"></a><span data-ttu-id="0a49d-366">Exploration : Tracer la distribution de conseil hello par classe</span><span class="sxs-lookup"><span data-stu-id="0a49d-366">Exploration: Plot hello tip distribution by class</span></span>
    tip_class_dist['tip_freq'].plot(kind='bar')

![Diagramme n°26][26]

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="0a49d-368">Exploration : distribution quotidienne des courses</span><span class="sxs-lookup"><span data-stu-id="0a49d-368">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="0a49d-369">Exploration : distribution des courses par médaillon</span><span class="sxs-lookup"><span data-stu-id="0a49d-369">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a><span data-ttu-id="0a49d-370">Exploration : Distribution des courses par médaillon et par licence de taxi</span><span class="sxs-lookup"><span data-stu-id="0a49d-370">Exploration: Trip distribution by medallion and hack license</span></span>
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a><span data-ttu-id="0a49d-371">Exploration : Distribution des durées de course</span><span class="sxs-lookup"><span data-stu-id="0a49d-371">Exploration: Trip time distribution</span></span>
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a><span data-ttu-id="0a49d-372">Exploration : Distribution des distances de course</span><span class="sxs-lookup"><span data-stu-id="0a49d-372">Exploration: Trip distance distribution</span></span>
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a><span data-ttu-id="0a49d-373">Exploration : Distribution des types de paiement</span><span class="sxs-lookup"><span data-stu-id="0a49d-373">Exploration: Payment type distribution</span></span>
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a><span data-ttu-id="0a49d-374">Vérifiez la forme finale de la table de fonctionnalités hello de hello</span><span class="sxs-lookup"><span data-stu-id="0a49d-374">Verify hello final form of hello featurized table</span></span>
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <span data-ttu-id="0a49d-375"><a name="mlmodel"></a>Créer des modèles dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0a49d-375"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="0a49d-376">Vous voilà prêt tooproceed toomodel génération et déploiement de modèle dans [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="0a49d-376">We are now ready tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="0a49d-377">les données de salutation sont prêt toobe utilisé dans un des problèmes de prédiction hello identifiées précédemment, à savoir :</span><span class="sxs-lookup"><span data-stu-id="0a49d-377">hello data is ready toobe used in any of hello prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="0a49d-378">**Classification binaire**: toopredict ou non un Conseil a été payé un voyage.</span><span class="sxs-lookup"><span data-stu-id="0a49d-378">**Binary classification**: toopredict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="0a49d-379">**Classification multiclasse**: plage de hello toopredict d’info-bulle payé, en fonction de toohello classes précédemment définies.</span><span class="sxs-lookup"><span data-stu-id="0a49d-379">**Multiclass classification**: toopredict hello range of tip paid, according toohello previously defined classes.</span></span>
3. <span data-ttu-id="0a49d-380">**Tâche de régression**: toopredict hello d’info-bulle montant d’un voyage.</span><span class="sxs-lookup"><span data-stu-id="0a49d-380">**Regression task**: toopredict hello amount of tip paid for a trip.</span></span>  

<span data-ttu-id="0a49d-381">toobegin hello exercice de modélisation, connectez-vous à tooyour **Azure Machine Learning** espace de travail.</span><span class="sxs-lookup"><span data-stu-id="0a49d-381">toobegin hello modeling exercise, log in tooyour **Azure Machine Learning** workspace.</span></span> <span data-ttu-id="0a49d-382">Si vous n’avez pas encore créé d’espace de travail d’apprentissage automatique, consultez l’article [Créer un espace de travail Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="0a49d-382">If you have not yet created a machine learning workspace, see [Create an Azure ML workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="0a49d-383">tooget main d’Azure Machine Learning, consultez [Nouveautés d’Azure Machine Learning Studio ?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="0a49d-383">tooget started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="0a49d-384">Connectez-vous trop[Azure Machine Learning Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="0a49d-384">Log in too[Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="0a49d-385">page d’accueil Studio Hello fournit une mine d’informations, des vidéos, didacticiels, des liens toohello référence des Modules et autres ressources.</span><span class="sxs-lookup"><span data-stu-id="0a49d-385">hello Studio Home page provides a wealth of information, videos, tutorials, links toohello Modules Reference, and other resources.</span></span> <span data-ttu-id="0a49d-386">Pour plus d’informations sur Azure Machine Learning, consultez hello [centre de Documentation Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="0a49d-386">For more information about Azure Machine Learning, consult hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="0a49d-387">Une expérience de formation standard se compose de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="0a49d-387">A typical training experiment consists of hello following steps:</span></span>

1. <span data-ttu-id="0a49d-388">Création d’une expérience à l’aide du bouton **+NOUVEAU** .</span><span class="sxs-lookup"><span data-stu-id="0a49d-388">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="0a49d-389">Permet d’obtenir des données de hello dans Azure ML.</span><span class="sxs-lookup"><span data-stu-id="0a49d-389">Get hello data into Azure ML.</span></span>
3. <span data-ttu-id="0a49d-390">Prétraiter, transformer et manipuler des données de hello en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="0a49d-390">Pre-process, transform and manipulate hello data as needed.</span></span>
4. <span data-ttu-id="0a49d-391">Génération des fonctionnalités requises.</span><span class="sxs-lookup"><span data-stu-id="0a49d-391">Generate features as needed.</span></span>
5. <span data-ttu-id="0a49d-392">Fractionner les données de hello en jeux de données d’apprentissage/validation/test (ou avoir des jeux de données distincts pour chaque).</span><span class="sxs-lookup"><span data-stu-id="0a49d-392">Split hello data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="0a49d-393">Sélectionnez un ou plusieurs algorithmes d’apprentissage en fonction de hello toosolve de problème d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="0a49d-393">Select one or more machine learning algorithms depending on hello learning problem toosolve.</span></span> <span data-ttu-id="0a49d-394">Exemples : classification binaire, classification multiclasse, régression.</span><span class="sxs-lookup"><span data-stu-id="0a49d-394">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="0a49d-395">L’apprentissage d’un ou plusieurs modèles à l’aide du jeu de données d’apprentissage hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-395">Train one or more models using hello training dataset.</span></span>
8. <span data-ttu-id="0a49d-396">Un score de jeu de données de validation hello à l’aide de modèles formés de hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-396">Score hello validation dataset using hello trained model(s).</span></span>
9. <span data-ttu-id="0a49d-397">Évaluer hello ou les modèles toocompute hello mesures pour hello problème d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="0a49d-397">Evaluate hello model(s) toocompute hello relevant metrics for hello learning problem.</span></span>
10. <span data-ttu-id="0a49d-398">Réglage de l’ou les modèles hello et sélectionnez hello meilleur modèle toodeploy.</span><span class="sxs-lookup"><span data-stu-id="0a49d-398">Fine tune hello model(s) and select hello best model toodeploy.</span></span>

<span data-ttu-id="0a49d-399">Dans cet exercice, nous avons déjà exploré et conçu données hello SQL Data Warehouse et décidé sur tooingest de taille d’échantillon hello dans Azure ML.</span><span class="sxs-lookup"><span data-stu-id="0a49d-399">In this exercise, we have already explored and engineered hello data in SQL Data Warehouse, and decided on hello sample size tooingest in Azure ML.</span></span> <span data-ttu-id="0a49d-400">Voici hello procédure toobuild une ou plusieurs des modèles de prévision hello :</span><span class="sxs-lookup"><span data-stu-id="0a49d-400">Here is hello procedure toobuild one or more of hello prediction models:</span></span>

1. <span data-ttu-id="0a49d-401">Obtenir des données de hello dans Azure ML à l’aide de hello [importer des données] [ import-data] module, disponible dans hello **données d’entrée et sortie** section.</span><span class="sxs-lookup"><span data-stu-id="0a49d-401">Get hello data into Azure ML using hello [Import Data][import-data] module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="0a49d-402">Pour plus d’informations, consultez hello [importer des données] [ import-data] page de référence de module.</span><span class="sxs-lookup"><span data-stu-id="0a49d-402">For more information, see hello [Import Data][import-data] module reference page.</span></span>
   
    ![Importer les données Azure ML][17]
2. <span data-ttu-id="0a49d-404">Sélectionnez **base de données SQL Azure** comme hello **source de données** Bonjour **propriétés** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="0a49d-404">Select **Azure SQL Database** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="0a49d-405">Entrez le nom DNS de base de données hello Bonjour **nom du serveur de base de données** champ.</span><span class="sxs-lookup"><span data-stu-id="0a49d-405">Enter hello database DNS name in hello **Database server name** field.</span></span> <span data-ttu-id="0a49d-406">Format : `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="0a49d-406">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="0a49d-407">Entrez hello **nom de la base de données** dans le champ correspondant de hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-407">Enter hello **Database name** in hello corresponding field.</span></span>
5. <span data-ttu-id="0a49d-408">Entrez hello *nom d’utilisateur SQL* Bonjour **le nom de compte d’utilisateur Server**et hello *mot de passe* Bonjour **mot de passe utilisateur Server**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-408">Enter hello *SQL user name* in hello **Server user account name**, and hello *password* in hello **Server user account password**.</span></span>
6. <span data-ttu-id="0a49d-409">Vérifiez hello **accepter n’importe quel certificat du serveur** option.</span><span class="sxs-lookup"><span data-stu-id="0a49d-409">Check hello **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="0a49d-410">Bonjour **requête de base de données** modifier la zone de texte, collez la requête hello extrait hello nécessaire (y compris les champs calculés tels que des étiquettes de hello) des champs de base de données et le bas exemples de taille d’échantillon hello données toohello souhaité.</span><span class="sxs-lookup"><span data-stu-id="0a49d-410">In hello **Database query** edit text area, paste hello query which extracts hello necessary database fields (including any computed fields such as hello labels) and down samples hello data toohello desired sample size.</span></span>

<span data-ttu-id="0a49d-411">Un exemple d’une expérience de classification binaire la lecture des données directement à partir de la base de données SQL Data Warehouse hello est dans la figure ci-dessous hello (n’oubliez pas de la table de hello tooreplace les noms nyctaxi_trip et nyctaxi_fare par schéma de hello hello et nom des noms de table utilisé dans votre procédure pas à pas).</span><span class="sxs-lookup"><span data-stu-id="0a49d-411">An example of a binary classification experiment reading data directly from hello SQL Data Warehouse database is in hello figure below (remember tooreplace hello table names nyctaxi_trip and nyctaxi_fare by hello schema name and hello table names you used in your walkthrough).</span></span> <span data-ttu-id="0a49d-412">Vous pouvez créer des expériences similaires pour les problèmes de classification multiclasse et de régression.</span><span class="sxs-lookup"><span data-stu-id="0a49d-412">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Formation Azure Machine Learning][10]

> [!IMPORTANT]
> <span data-ttu-id="0a49d-414">Bonjour, extraction de données de modélisation et de l’échantillonnage des exemples de requêtes fournis dans les sections précédentes, **toutes les étiquettes pour les exercices de modélisation hello trois sont inclus dans la requête de hello**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-414">In hello modeling data extraction and sampling query examples provided in previous sections, **all labels for hello three modeling exercises are included in hello query**.</span></span> <span data-ttu-id="0a49d-415">Une étape importante (obligatoire) dans chacun des exercices de modélisation de hello est trop**exclure** hello étiquettes inutiles pour hello autres deux problèmes, ainsi que tout autre **cible fuites**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-415">An important (required) step in each of hello modeling exercises is too**exclude** hello unnecessary labels for hello other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="0a49d-416">Par exemple, lors de l’utilisation de classification binaire, utilisez les étiquette hello **incliné** et exclure les champs hello **Conseil\_classe**, **Conseil\_quantité**, et **total\_quantité**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-416">For example, when using binary classification, use hello label **tipped** and exclude hello fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="0a49d-417">Hello dernier paiement des fuites de cible, car elles impliquent l’info-bulle hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-417">hello latter are target leaks since they imply hello tip paid.</span></span>
> 
> <span data-ttu-id="0a49d-418">tooexclude toutes les colonnes inutiles ou les fuites de cible, vous pouvez utiliser hello [sélectionner les colonnes dans le jeu de données] [ select-columns] module ou hello [modifier les métadonnées] [ edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="0a49d-418">tooexclude any unnecessary columns or target leaks, you may use hello [Select Columns in Dataset][select-columns] module or hello [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="0a49d-419">Pour plus d’informations, consultez les pages de référence [Sélectionner des colonnes dans le jeu de données][select-columns] et [Modifier les métadonnées][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="0a49d-419">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="0a49d-420"><a name="mldeploy"></a>Déployer des modèles dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0a49d-420"><a name="mldeploy"></a>Deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="0a49d-421">Lorsque votre modèle est prêt, vous pouvez la déployer facilement en tant qu’un service web directement à partir de l’expérience de hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-421">When your model is ready, you can easily deploy it as a web service directly from hello experiment.</span></span> <span data-ttu-id="0a49d-422">Pour plus d’informations sur le déploiement de services web Azure Machine Learning, consultez [Déployer un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="0a49d-422">For more information about deploying Azure ML web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="0a49d-423">toodeploy un nouveau service web, vous devez :</span><span class="sxs-lookup"><span data-stu-id="0a49d-423">toodeploy a new web service, you need to:</span></span>

1. <span data-ttu-id="0a49d-424">créer une expérience de notation ;</span><span class="sxs-lookup"><span data-stu-id="0a49d-424">Create a scoring experiment.</span></span>
2. <span data-ttu-id="0a49d-425">Déployer un service web de hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-425">Deploy hello web service.</span></span>

<span data-ttu-id="0a49d-426">toocreate une expérience d’un score d’un **terminé** expérience d’apprentissage, cliquez sur **créer une expérience de score** dans la barre d’action hello inférieur.</span><span class="sxs-lookup"><span data-stu-id="0a49d-426">toocreate a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in hello lower action bar.</span></span>

![Notation Azure][18]

<span data-ttu-id="0a49d-428">Azure Machine Learning tentera toocreate expérience de score basée sur les composants hello d’expérience de formation hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-428">Azure Machine Learning will attempt toocreate a scoring experiment based on hello components of hello training experiment.</span></span> <span data-ttu-id="0a49d-429">Il va notamment :</span><span class="sxs-lookup"><span data-stu-id="0a49d-429">In particular, it will:</span></span>

1. <span data-ttu-id="0a49d-430">Enregistrer le modèle formé de hello et supprimer des modules de formation du modèle hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-430">Save hello trained model and remove hello model training modules.</span></span>
2. <span data-ttu-id="0a49d-431">Identifier un opérateur logique **port d’entrée** toorepresent hello attendue de schéma de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="0a49d-431">Identify a logical **input port** toorepresent hello expected input data schema.</span></span>
3. <span data-ttu-id="0a49d-432">Identifier un opérateur logique **port de sortie** schéma de sortie de service toorepresent hello web attendu.</span><span class="sxs-lookup"><span data-stu-id="0a49d-432">Identify a logical **output port** toorepresent hello expected web service output schema.</span></span>

<span data-ttu-id="0a49d-433">Lors de la création de hello expérience de score, examiner et rendre l’ajuster en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="0a49d-433">When hello scoring experiment is created, review it and make adjust as needed.</span></span> <span data-ttu-id="0a49d-434">Un ajustement standard est tooreplace hello jeu de données d’entrée et/ou de la requête avec l’une qui exclut les champs d’étiquette, car il ne sera pas disponibles lorsque le service de hello est appelé.</span><span class="sxs-lookup"><span data-stu-id="0a49d-434">A typical adjustment is tooreplace hello input dataset and/or query with one which excludes label fields, as these will not be available when hello service is called.</span></span> <span data-ttu-id="0a49d-435">Il est également qu'une taille de hello tooreduce bonnes pratiques de hello d’entrée tooa de jeu de données et/ou des requêtes peu d’enregistrements, juste assez schéma d’entrée de tooindicate hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-435">It is also a good practice tooreduce hello size of hello input dataset and/or query tooa few records, just enough tooindicate hello input schema.</span></span> <span data-ttu-id="0a49d-436">Pour le port de sortie hello, il est commun tooexclude entrées tous les champs et uniquement inclure hello **Scored Labels** et **des probabilités notées** Bonjour de sortie à l’aide de hello [sélectionner les colonnes dans le jeu de données ] [ select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="0a49d-436">For hello output port, it is common tooexclude all input fields and only include hello **Scored Labels** and **Scored Probabilities** in hello output using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="0a49d-437">Un exemple d’expérience de score est fourni dans la figure ci-dessous hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-437">A sample scoring experiment is provided in hello figure below.</span></span> <span data-ttu-id="0a49d-438">Quand vous êtes prêt toodeploy, cliquez sur hello **publier le SERVICE WEB** bouton dans la barre d’action hello inférieur.</span><span class="sxs-lookup"><span data-stu-id="0a49d-438">When ready toodeploy, click hello **PUBLISH WEB SERVICE** button in hello lower action bar.</span></span>

![Publication Azure Machine Learning][11]

## <a name="summary"></a><span data-ttu-id="0a49d-440">Résumé</span><span class="sxs-lookup"><span data-stu-id="0a49d-440">Summary</span></span>
<span data-ttu-id="0a49d-441">toorecap ce que nous avons effectué dans ce didacticiel de la procédure pas à pas, vous avez créé un environnement de science des données Azure, travaillé avec un jeu de données publique volumineux, il guidant hello processus d’équipe données scientifiques, tous les moyen hello de formation de toomodel d’acquisition de données, puis toohello le déploiement d’un service web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0a49d-441">toorecap what we have done in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset, taking it through hello Team Data Science Process, all hello way from data acquisition toomodel training, and then toohello deployment of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="0a49d-442">Informations de licence</span><span class="sxs-lookup"><span data-stu-id="0a49d-442">License information</span></span>
<span data-ttu-id="0a49d-443">Cet exemple de procédure et accompagne des scripts et des notebooks notebook(s) sont partagées par Microsoft sous licence du MIT hello.</span><span class="sxs-lookup"><span data-stu-id="0a49d-443">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="0a49d-444">Vérifiez fichier hello le répertoire hello hello exemple de code sur GitHub pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="0a49d-444">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="0a49d-445">Références</span><span class="sxs-lookup"><span data-stu-id="0a49d-445">References</span></span>
<span data-ttu-id="0a49d-446">•    [Page de téléchargement des jeux de données NYC Taxi Trips par Andrés Monroy (en anglais)](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="0a49d-446">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="0a49d-447">•    [Page de partage des données relatives aux courses en taxi new-yorkais par Chris Whong (en anglais)](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="0a49d-447">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="0a49d-448">•    [Page de recherche et de statistiques de la Commission des services de taxis et de limousines de la ville de New York (en anglais)](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="0a49d-448">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sqldw-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sqldw-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlscoring.png
[19]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_download_scripts.png
[20]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_load_data.png
[21]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azcopy-overwrite.png
[22]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-1.png
[23]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-2.png
[24]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-3.png
[25]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-4.png
[26]: ./media/machine-learning-data-science-process-sqldw-walkthrough/tip_class_hist_1.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
