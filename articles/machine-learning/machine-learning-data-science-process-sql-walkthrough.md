---
title: "aaaBuild et déployer un modèle d’apprentissage automatique à l’aide de SQL Server sur une machine virtuelle Azure | Des documents Microsoft"
description: "Processus d’analyse avancé et technologie en action"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6066b083-262c-4453-a712-a5c05acc3df8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: fashah;bradsev
ms.openlocfilehash: 30ba9a9e3cf65f75015e13f9c7876dcbccc5bc47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-server"></a><span data-ttu-id="3751d-103">Hello processus de science des données équipe en action : à l’aide de SQL Server</span><span class="sxs-lookup"><span data-stu-id="3751d-103">hello Team Data Science Process in action: using SQL Server</span></span>
<span data-ttu-id="3751d-104">Dans ce didacticiel, vous voyez hello les processus de génération et de déploiement d’un modèle d’apprentissage automatique à l’aide de SQL Server et un jeu de données disponible publiquement--hello [NYC Taxi allers-retours](http://www.andresmh.com/nyctaxitrips/) jeu de données.</span><span class="sxs-lookup"><span data-stu-id="3751d-104">In this tutorial, you walk through hello process of building and deploying a machine learning model using SQL Server and a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="3751d-105">procédure de Hello suit un flux de travail de science des données standard : réception et Explorer les données hello ingénieur learning toofacilitate de fonctionnalités, puis générer et déployer un modèle.</span><span class="sxs-lookup"><span data-stu-id="3751d-105">hello procedure follows a standard data science workflow: ingest and explore hello data, engineer features toofacilitate learning, then build and deploy a model.</span></span>

## <span data-ttu-id="3751d-106"><a name="dataset"></a>Description du jeu de données NYC Taxi Trips</span><span class="sxs-lookup"><span data-stu-id="3751d-106"><a name="dataset"></a>NYC Taxi Trips Dataset Description</span></span>
<span data-ttu-id="3751d-107">Hello les données NYC Taxi voyage est d’environ 20 Go de fichiers CSV compressées (Go ~ 48 non compressé), qui comprend plus de 173 millions hello et des boucles tarifs payé pour chaque sortie.</span><span class="sxs-lookup"><span data-stu-id="3751d-107">hello NYC Taxi Trip data is about 20GB of compressed CSV files (~48GB uncompressed), comprising more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="3751d-108">Chaque enregistrement de voyage comprend hello collecte et remise l’emplacement et l’heure, hack rendues anonymes (pilote) numéro de licence et nombre de medallion (id unique de taxi).</span><span class="sxs-lookup"><span data-stu-id="3751d-108">Each trip record includes hello pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="3751d-109">les données de salutation couvre toutes les boucles dans l’année hello 2013 et sont fournies dans hello suivant deux jeux de données pour chaque mois :</span><span class="sxs-lookup"><span data-stu-id="3751d-109">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="3751d-110">Hello 'trip_data' CSV contient les détails de voyage, telles que le nombre de personnes, collecte et cette chute points, durée de voyage, longueur de voyage.</span><span class="sxs-lookup"><span data-stu-id="3751d-110">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="3751d-111">Voici quelques exemples d’enregistrements :</span><span class="sxs-lookup"><span data-stu-id="3751d-111">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="3751d-112">Hello 'trip_fare' CSV contient les détails des prix hello payé pour chaque sortie, comme type de paiement, montant de frais, surcharge et taxes, conseils et péage et montant total de hello payé.</span><span class="sxs-lookup"><span data-stu-id="3751d-112">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="3751d-113">Voici quelques exemples d’enregistrements :</span><span class="sxs-lookup"><span data-stu-id="3751d-113">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="3751d-114">voyage toojoin de clé unique de Hello\_données et voyage\_tarif est composée de champs de hello : medallion, hack\_certificat et pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="3751d-114">hello unique key toojoin trip\_data and trip\_fare is composed of hello fields: medallion, hack\_licence and pickup\_datetime.</span></span>

## <span data-ttu-id="3751d-115"><a name="mltasks"></a>Exemples de tâches de prédiction</span><span class="sxs-lookup"><span data-stu-id="3751d-115"><a name="mltasks"></a>Examples of Prediction Tasks</span></span>
<span data-ttu-id="3751d-116">Nous formuler les trois problèmes de prédiction selon hello *Conseil\_quantité*, à savoir :</span><span class="sxs-lookup"><span data-stu-id="3751d-116">We will formulate three prediction problems based on hello *tip\_amount*, namely:</span></span>

1. <span data-ttu-id="3751d-117">Classification binaire : prédire si un pourboire a ou non été versé pour une course ; autrement dit, une valeur *tip\_amount* supérieure à 0 $ constitue un exemple positif, alors qu’une *tip\_amount* de 0 $ est un exemple négatif.</span><span class="sxs-lookup"><span data-stu-id="3751d-117">Binary classification: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="3751d-118">Classification multiclasse : plage de hello toopredict d’info-bulle payé pour le voyage de hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-118">Multiclass classification: toopredict hello range of tip paid for hello trip.</span></span> <span data-ttu-id="3751d-119">Nous allons diviser hello *Conseil\_quantité* dans les cinq conteneurs ou les classes :</span><span class="sxs-lookup"><span data-stu-id="3751d-119">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="3751d-120">Tâche de régression : toopredict hello d’info-bulle montant d’un voyage.</span><span class="sxs-lookup"><span data-stu-id="3751d-120">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="3751d-121"><a name="setup"></a>Configuration des hello Azure science environnement de données analytique avancée</span><span class="sxs-lookup"><span data-stu-id="3751d-121"><a name="setup"></a>Setting Up hello Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="3751d-122">Comme vous pouvez le constater hello [planifier votre environnement](machine-learning-data-science-plan-your-environment.md) guide, il existe plusieurs options toowork, avec jeu de données hello NYC Taxi allers-retours dans Azure :</span><span class="sxs-lookup"><span data-stu-id="3751d-122">As you can see from hello [Plan Your Environment](machine-learning-data-science-plan-your-environment.md) guide, there are several options toowork with hello NYC Taxi Trips dataset in Azure:</span></span>

* <span data-ttu-id="3751d-123">Travailler avec des données hello dans des objets BLOB Azure, puis le modèle dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3751d-123">Work with hello data in Azure blobs then model in Azure Machine Learning</span></span>
* <span data-ttu-id="3751d-124">Charger des données dans une base de données SQL Server, puis le modèle dans Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="3751d-124">Load hello data into a SQL Server database then model in Azure Machine Learning</span></span>

<span data-ttu-id="3751d-125">Dans ce didacticiel, nous allons vous montrer importation parallèle en bloc de hello tooa de données SQL Server, exploration de données, la fonctionnalité d’ingénierie et vers le bas d’échantillonnage à l’aide de SQL Server Management Studio ainsi qu’à l’aide du bloc-notes de notebooks.</span><span class="sxs-lookup"><span data-stu-id="3751d-125">In this tutorial we will demonstrate parallel bulk import of hello data tooa SQL Server, data exploration, feature engineering and down sampling using SQL Server Management Studio as well as using IPython Notebook.</span></span> <span data-ttu-id="3751d-126">Des [exemples de scripts](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) et de [notebooks IPython](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) sont publiquement accessibles dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="3751d-126">[Sample scripts](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) and [IPython notebooks](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) are shared in GitHub.</span></span> <span data-ttu-id="3751d-127">Un toowork de bloc-notes exemple IPython avec des données dans des objets BLOB Azure hello est également disponible dans hello même emplacement.</span><span class="sxs-lookup"><span data-stu-id="3751d-127">A sample IPython notebook toowork with hello data in Azure blobs is also available in hello same location.</span></span>

<span data-ttu-id="3751d-128">tooset votre environnement Azure pour la science des données :</span><span class="sxs-lookup"><span data-stu-id="3751d-128">tooset up your Azure Data Science environment:</span></span>

1. [<span data-ttu-id="3751d-129">Créer un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="3751d-129">Create a storage account</span></span>](../storage/common/storage-create-storage-account.md)
2. [<span data-ttu-id="3751d-130">Création d’un espace de travail Microsoft Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3751d-130">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
3. <span data-ttu-id="3751d-131">[Approvisionnez une machine virtuelle de science des données](machine-learning-data-science-setup-sql-server-virtual-machine.md), qui fournit un serveur SQL Server et un serveur Notebook IPython.</span><span class="sxs-lookup"><span data-stu-id="3751d-131">[Provision a Data Science Virtual Machine](machine-learning-data-science-setup-sql-server-virtual-machine.md), which provides a SQL Server and an IPython Notebook server.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3751d-132">exemples de scripts Hello et IPython Notebook sera téléchargé tooyour science des données virtual machine pendant le processus d’installation de hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-132">hello sample scripts and IPython notebooks will be downloaded tooyour Data Science virtual machine during hello setup process.</span></span> <span data-ttu-id="3751d-133">Hello script post-installation de machine virtuelle est terminée, les exemples hello doivent être dans la bibliothèque de Documents de votre machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="3751d-133">When hello VM post-installation script completes, hello samples will be in your VM's Documents library:</span></span>  
   > 
   > * <span data-ttu-id="3751d-134">Exemples de scripts : `C:\Users\<user_name>\Documents\Data Science Scripts`</span><span class="sxs-lookup"><span data-stu-id="3751d-134">Sample Scripts: `C:\Users\<user_name>\Documents\Data Science Scripts`</span></span>  
   > * <span data-ttu-id="3751d-135">Exemples de notebooks IPython : `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span><span class="sxs-lookup"><span data-stu-id="3751d-135">Sample IPython Notebooks: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span></span>  
   >   <span data-ttu-id="3751d-136">where `<user_name>` est le nom de connexion de votre machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="3751d-136">where `<user_name>` is your VM's Windows login name.</span></span> <span data-ttu-id="3751d-137">Nous appelons toohello dossiers en tant que **exemples de Scripts** et **exemple IPython Notebook**.</span><span class="sxs-lookup"><span data-stu-id="3751d-137">We will refer toohello sample folders as **Sample Scripts** and **Sample IPython Notebooks**.</span></span>
   > 
   > 

<span data-ttu-id="3751d-138">Selon la taille du jeu de données hello, emplacement de source de données et environnement cible Azure sélectionné de hello, ce scénario est similaire trop[scénario \#5 : jeu de données volumineux dans des fichiers locaux, ciblent SQL Server dans Azure VM](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span><span class="sxs-lookup"><span data-stu-id="3751d-138">Based on hello dataset size, data source location, and hello selected Azure target environment, this scenario is similar too[Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span></span>

## <span data-ttu-id="3751d-139"><a name="getdata"></a>Obtenir hello données à partir de la Source publique</span><span class="sxs-lookup"><span data-stu-id="3751d-139"><a name="getdata"></a>Get hello Data from Public Source</span></span>
<span data-ttu-id="3751d-140">tooget hello [NYC Taxi allers-retours](http://www.andresmh.com/nyctaxitrips/) dataset à partir de son emplacement public, vous pouvez utiliser une des méthodes hello décrites dans [tooand de déplacer les données à partir du stockage d’objets Blob Azure](machine-learning-data-science-move-azure-blob.md) toocopy hello données tooyour nouvel ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="3751d-140">tooget hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of hello methods described in [Move Data tooand from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy hello data tooyour new virtual machine.</span></span>

<span data-ttu-id="3751d-141">données de salutation toocopy à l’aide de AzCopy :</span><span class="sxs-lookup"><span data-stu-id="3751d-141">toocopy hello data using AzCopy:</span></span>

1. <span data-ttu-id="3751d-142">Connectez-vous à tooyour virtual machine (VM)</span><span class="sxs-lookup"><span data-stu-id="3751d-142">Log in tooyour virtual machine (VM)</span></span>
2. <span data-ttu-id="3751d-143">Créer un nouveau répertoire de disque de données de la machine virtuelle hello (Remarque : n’utilisez pas hello disque temporaire qui est livré avec hello machine virtuelle comme disque de données).</span><span class="sxs-lookup"><span data-stu-id="3751d-143">Create a new directory in hello VM's data disk (Note: Do not use hello Temporary Disk which comes with hello VM as a Data Disk).</span></span>
3. <span data-ttu-id="3751d-144">Dans une fenêtre d’invite de commandes, exécutez hello suivant la ligne de commande Azcopy, en remplaçant < path_to_data_folder > avec votre dossier de données créée dans (2) :</span><span class="sxs-lookup"><span data-stu-id="3751d-144">In a Command Prompt window, run hello following Azcopy command line, replacing <path_to_data_folder> with your data folder created in (2):</span></span>
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    <span data-ttu-id="3751d-145">Lorsque hello AzCopy est terminée, un total de 24 compressé de fichiers CSV (12 pour le voyage\_données et 12 pour le voyage\_tarif) doit être dans le dossier de données hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-145">When hello AzCopy completes, a total of 24 zipped CSV files (12 for trip\_data and 12 for trip\_fare) should be in hello data folder.</span></span>
4. <span data-ttu-id="3751d-146">Décompressez les fichiers hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="3751d-146">Unzip hello downloaded files.</span></span> <span data-ttu-id="3751d-147">Notez le dossier hello où résident les fichiers de hello non compressé.</span><span class="sxs-lookup"><span data-stu-id="3751d-147">Note hello folder where hello uncompressed files reside.</span></span> <span data-ttu-id="3751d-148">Ce dossier sera référencé tooas hello < chemin d’accès\_à\_données\_fichiers\>.</span><span class="sxs-lookup"><span data-stu-id="3751d-148">This folder will be referred tooas hello <path\_to\_data\_files\>.</span></span>

## <span data-ttu-id="3751d-149"><a name="dbload"></a>Importer en bloc les données dans une base de données SQL Server</span><span class="sxs-lookup"><span data-stu-id="3751d-149"><a name="dbload"></a>Bulk Import Data into SQL Server Database</span></span>
<span data-ttu-id="3751d-150">Hello performances de chargement et de transfert de grandes quantités de base de données de données tooan SQL et les requêtes suivantes peuvent être améliorées en utilisant *Partitioned Tables et vues*.</span><span class="sxs-lookup"><span data-stu-id="3751d-150">hello performance of loading/transferring large amounts of data tooan SQL database and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> <span data-ttu-id="3751d-151">Dans cette section, nous allons suivre les instructions hello décrites dans [parallèle en bloc données à l’aide de SQL Partition Tables d’importation](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate une nouvelle base de données et charger hello les données dans des tables partitionnées en parallèle.</span><span class="sxs-lookup"><span data-stu-id="3751d-151">In this section, we will follow hello instructions described in [Parallel Bulk Data Import Using SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate a new database and load hello data into partitioned tables in parallel.</span></span>

1. <span data-ttu-id="3751d-152">Connecté tooyour machine virtuelle, démarrez **SQL Server Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="3751d-152">While logged in tooyour VM, start **SQL Server Management Studio**.</span></span>
2. <span data-ttu-id="3751d-153">Connectez-vous à l’aide de l’authentification Windows.</span><span class="sxs-lookup"><span data-stu-id="3751d-153">Connect using Windows Authentication.</span></span>
   
    ![Connecter SSMS][12]
3. <span data-ttu-id="3751d-155">Si vous n’avez pas encore modifié le mode d’authentification SQL Server hello et créé un nouveau nom d’utilisateur SQL, ouvrez le fichier de script de hello nommé **modifier\_auth.sql** Bonjour **exemples de Scripts** dossier.</span><span class="sxs-lookup"><span data-stu-id="3751d-155">If you have not yet changed hello SQL Server authentication mode and created a new SQL login user, open hello script file named **change\_auth.sql** in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="3751d-156">Modifier le nom d’utilisateur par défaut hello et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="3751d-156">Change hello  default user name and password.</span></span> <span data-ttu-id="3751d-157">Cliquez sur **! Exécutez** dans le script de hello toorun hello barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="3751d-157">Click **!Execute** in hello toolbar toorun hello script.</span></span>
   
    ![Exécuter le script][13]
4. <span data-ttu-id="3751d-159">Vérifiez et/ou modifiez hello SQL Server par défaut de base de données et journal dossiers tooensure que les bases de données nouvellement créées est stocké dans un disque de données.</span><span class="sxs-lookup"><span data-stu-id="3751d-159">Verify and/or change hello SQL Server default database and log folders tooensure that newly created databases will be stored in a Data Disk.</span></span> <span data-ttu-id="3751d-160">image de machine virtuelle SQL Server Hello qui est optimisé pour les charges datawarehousing est préconfiguré avec des disques de données et du journal.</span><span class="sxs-lookup"><span data-stu-id="3751d-160">hello SQL Server VM image that is optimized for datawarehousing loads is pre-configured with data and log disks.</span></span> <span data-ttu-id="3751d-161">Si votre machine virtuelle n’incluait pas d’un disque de données et que vous avez ajouté des disques durs virtuels pendant hello les processus de configuration de machine virtuelle, modifiez les dossiers par défaut hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3751d-161">If your VM did not include a Data Disk and you added new virtual hard disks during hello VM setup process, change hello default folders as follows:</span></span>
   
   * <span data-ttu-id="3751d-162">Nom de SQL Server avec le bouton hello Bonjour gauche du Panneau de configuration et cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="3751d-162">Right-click hello SQL Server name in hello left panel and click **Properties**.</span></span>
     
       ![Propriétés SQL Server][14]
   * <span data-ttu-id="3751d-164">Sélectionnez **les paramètres de base de données** de hello **sélectionner une page** toohello gauche de la liste.</span><span class="sxs-lookup"><span data-stu-id="3751d-164">Select **Database Settings** from hello **Select a page** list toohello left.</span></span>
   * <span data-ttu-id="3751d-165">Vérifiez et/ou modifiez hello **emplacements par défaut de base de données** toohello **disque de données** les emplacements de votre choix.</span><span class="sxs-lookup"><span data-stu-id="3751d-165">Verify and/or change hello **Database default locations** toohello **Data Disk** locations of your choice.</span></span> <span data-ttu-id="3751d-166">Il s’agit d’emplacement des nouvelles bases de données si créé avec les paramètres d’emplacement par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-166">This is where new databases reside if created with hello default location settings.</span></span>
     
       ![Valeurs par défaut de la base de données SQL][15]  
5. <span data-ttu-id="3751d-168">toocreate une base de données et un ensemble de groupes de fichiers toohold hello tables partitionnées, ouvrez l’exemple de script hello **créer\_db\_default.sql**.</span><span class="sxs-lookup"><span data-stu-id="3751d-168">toocreate a new database and a set of filegroups toohold hello partitioned tables, open hello sample script **create\_db\_default.sql**.</span></span> <span data-ttu-id="3751d-169">Hello script crée une base de données nommée **TaxiNYC** et 12 groupes de fichiers dans un emplacement de données par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-169">hello script will create a new database named **TaxiNYC** and 12 filegroups in hello default data location.</span></span> <span data-ttu-id="3751d-170">Chaque groupe de fichiers contiendra un mois de données trip\_data et trip\_fare.</span><span class="sxs-lookup"><span data-stu-id="3751d-170">Each filegroup will hold one month of trip\_data and trip\_fare data.</span></span> <span data-ttu-id="3751d-171">Modifier le nom de base de données hello, si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="3751d-171">Modify hello database name, if desired.</span></span> <span data-ttu-id="3751d-172">Cliquez sur **! Exécutez** script de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="3751d-172">Click **!Execute** toorun hello script.</span></span>
6. <span data-ttu-id="3751d-173">Ensuite, créez deux tables de partition, une pour le voyage de hello\_et une autre pour le voyage de hello\_tarif.</span><span class="sxs-lookup"><span data-stu-id="3751d-173">Next, create two partition tables, one for hello trip\_data and another for hello trip\_fare.</span></span> <span data-ttu-id="3751d-174">Ouvrez l’exemple de script hello **créer\_partitionnée\_table.sql**, qui sera :</span><span class="sxs-lookup"><span data-stu-id="3751d-174">Open hello sample script **create\_partitioned\_table.sql**, which will:</span></span>
   
   * <span data-ttu-id="3751d-175">Créer un partition fonction toosplit hello de données par mois.</span><span class="sxs-lookup"><span data-stu-id="3751d-175">Create a partition function toosplit hello data by month.</span></span>
   * <span data-ttu-id="3751d-176">Créer un toomap de schéma de partition données tooa autre groupe de fichiers de chaque mois.</span><span class="sxs-lookup"><span data-stu-id="3751d-176">Create a partition scheme toomap each month's data tooa different filegroup.</span></span>
   * <span data-ttu-id="3751d-177">Créer le schéma de partition de deux tables partitionnées toohello mappé : **nyctaxi\_voyage** contiendra voyage de hello\_données et **nyctaxi\_tarif** contiendra voyage de hello \_prix des données.</span><span class="sxs-lookup"><span data-stu-id="3751d-177">Create two partitioned tables mapped toohello partition scheme: **nyctaxi\_trip** will hold hello trip\_data and **nyctaxi\_fare** will hold hello trip\_fare data.</span></span>
     
     <span data-ttu-id="3751d-178">Cliquez sur **! Exécutez** toorun hello script et créer des tables partitionnée de hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-178">Click **!Execute** toorun hello script and create hello partitioned tables.</span></span>
7. <span data-ttu-id="3751d-179">Bonjour **exemples de Scripts** dossier, il existe deux exemples de scripts PowerShell fourni toodemonstrate importations en bloc parallèle tooSQL Server de tables de données.</span><span class="sxs-lookup"><span data-stu-id="3751d-179">In hello **Sample Scripts** folder, there are two sample PowerShell scripts provided toodemonstrate parallel bulk imports of data tooSQL Server tables.</span></span>
   
   * <span data-ttu-id="3751d-180">**bcp\_parallèles\_generic.ps1** est une script générique tooparallel importation des données en bloc dans une table.</span><span class="sxs-lookup"><span data-stu-id="3751d-180">**bcp\_parallel\_generic.ps1** is a generic script tooparallel bulk import data into a table.</span></span> <span data-ttu-id="3751d-181">Modifiez cette tooset hello cible d’entrée et de variables de script comme indiqué dans les lignes de commentaire hello dans le script de hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-181">Modify this script tooset hello input and target variables as indicated in hello comment lines in hello script.</span></span>
   * <span data-ttu-id="3751d-182">**bcp\_parallèles\_nyctaxi.ps1** est une version préconfigurée de script générique de hello et peut être utilisé tootooload les deux tables pour les données NYC Taxi allers-retours hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-182">**bcp\_parallel\_nyctaxi.ps1** is a pre-configured version of hello generic script and can be used tootooload both tables for hello NYC Taxi Trips data.</span></span>  
8. <span data-ttu-id="3751d-183">Avec le bouton hello **bcp\_parallèles\_nyctaxi.ps1** nom de script, cliquez sur **modifier** tooopen dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3751d-183">Right-click hello **bcp\_parallel\_nyctaxi.ps1** script name and click **Edit** tooopen it in PowerShell.</span></span> <span data-ttu-id="3751d-184">Hello de révision variables prédéfinies et modifier le nom de base de données sélectionnée tooyour conséquente, dossier de données d’entrée, dossier de journal cible et les fichiers de format de chemins d’accès toohello exemple **nyctaxi_trip.xml** et **nyctaxi\_ fare.XML** (fourni dans hello **exemples de Scripts** dossier).</span><span class="sxs-lookup"><span data-stu-id="3751d-184">Review hello preset variables and modify according tooyour selected database name, input data folder, target log folder, and paths toohello  sample format files **nyctaxi_trip.xml** and **nyctaxi\_fare.xml** (provided in hello **Sample Scripts** folder).</span></span>
   
    ![Importer les données][16]
   
    <span data-ttu-id="3751d-186">Vous pouvez également sélectionner le mode d’authentification hello, valeur par défaut est l’authentification Windows.</span><span class="sxs-lookup"><span data-stu-id="3751d-186">You may also select hello authentication mode, default is Windows Authentication.</span></span> <span data-ttu-id="3751d-187">Cliquez sur flèche hello vert toorun de barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-187">Click hello green arrow in hello toolbar toorun.</span></span> <span data-ttu-id="3751d-188">script de Hello lancera 24 opérations d’importation en bloc dans les 12 parallèle, pour chaque table partitionnée.</span><span class="sxs-lookup"><span data-stu-id="3751d-188">hello script will launch 24 bulk import operations in parallel, 12 for each partitioned table.</span></span> <span data-ttu-id="3751d-189">Vous pouvez surveiller la progression de l’importation données hello en ouvrant le dossier de données de valeur par défaut de SQL Server hello comme ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="3751d-189">You may monitor hello data import progress by opening hello SQL Server default data folder as set above.</span></span>
9. <span data-ttu-id="3751d-190">rapports de script PowerShell Hello hello de début et de fin des heures.</span><span class="sxs-lookup"><span data-stu-id="3751d-190">hello PowerShell script reports hello starting and ending times.</span></span> <span data-ttu-id="3751d-191">Lorsque tous en bloc d’importation terminée, hello leur heure de fin est signalée.</span><span class="sxs-lookup"><span data-stu-id="3751d-191">When all bulk imports complete, hello ending time is reported.</span></span> <span data-ttu-id="3751d-192">Vérifiez tooverify dossier de journal de cible de hello hello les importations en bloc ont réussi, autrement dit, aucune erreur n’est signalée dans le dossier de journal hello cible.</span><span class="sxs-lookup"><span data-stu-id="3751d-192">Check hello target log folder tooverify that hello bulk imports were successful, i.e., no errors reported in hello target log folder.</span></span>
10. <span data-ttu-id="3751d-193">Votre base de données est désormais prête pour vos opérations d’exploration, de conception de fonctionnalités, etc.</span><span class="sxs-lookup"><span data-stu-id="3751d-193">Your database is now ready for exploration, feature engineering, and other operations as desired.</span></span> <span data-ttu-id="3751d-194">Étant donné que les tables de hello sont partitionnées selon toohello **collecte\_datetime** champ, les requêtes qui incluent des **collecte\_datetime** conditions Bonjour  **OÙ** clause bénéficieront de schéma de partition hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-194">Since hello tables are partitioned according toohello **pickup\_datetime** field, queries which include **pickup\_datetime** conditions in hello **WHERE** clause will benefit from hello partition scheme.</span></span>
11. <span data-ttu-id="3751d-195">Dans **SQL Server Management Studio**, explorez l’exemple de script hello fourni **exemple\_queries.sql**.</span><span class="sxs-lookup"><span data-stu-id="3751d-195">In **SQL Server Management Studio**, explore hello provided sample script **sample\_queries.sql**.</span></span> <span data-ttu-id="3751d-196">toorun un des exemples de requêtes hello, mettez en surbrillance hello lignes de la requête, puis cliquez sur **! Exécutez** dans la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-196">toorun any of hello sample queries, highlight hello query lines then click **!Execute** in hello toolbar.</span></span>
12. <span data-ttu-id="3751d-197">les données NYC Taxi allers-retours de Hello est chargé dans deux tables distinctes.</span><span class="sxs-lookup"><span data-stu-id="3751d-197">hello NYC Taxi Trips data is loaded in two separate tables.</span></span> <span data-ttu-id="3751d-198">tooimprove des opérations de jointure, il est recommandé de tables de hello tooindex.</span><span class="sxs-lookup"><span data-stu-id="3751d-198">tooimprove join operations, it is highly recommended tooindex hello tables.</span></span> <span data-ttu-id="3751d-199">Hello exemple de script **créer\_partitionnée\_index.sql** crée des index partitionnés sur la clé de jointure composite hello **medallion, hack\_licence et capture\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="3751d-199">hello sample script **create\_partitioned\_index.sql** creates partitioned indexes on hello composite join key **medallion, hack\_license, and pickup\_datetime**.</span></span>

## <span data-ttu-id="3751d-200"><a name="dbexplore"></a>Exploration des données et conception de fonctionnalités dans SQL Server</span><span class="sxs-lookup"><span data-stu-id="3751d-200"><a name="dbexplore"></a>Data Exploration and Feature Engineering in SQL Server</span></span>
<span data-ttu-id="3751d-201">Dans cette section, nous allons effectuer la génération de fonctionnalité et d’exploration de données en exécutant des requêtes SQL directement dans hello **SQL Server Management Studio** à l’aide de la base de données SQL Server hello créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="3751d-201">In this section, we will perform data exploration and feature generation by running SQL queries directly in hello **SQL Server Management Studio** using hello SQL Server database created earlier.</span></span> <span data-ttu-id="3751d-202">Un exemple de script nommé **exemple\_queries.sql** est fourni dans hello **exemples de Scripts** dossier.</span><span class="sxs-lookup"><span data-stu-id="3751d-202">A sample script named **sample\_queries.sql** is provided in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="3751d-203">Modifier le nom de base de données hello script toochange hello, si elle est différente de la valeur par défaut hello : **TaxiNYC**.</span><span class="sxs-lookup"><span data-stu-id="3751d-203">Modify hello script toochange hello database name, if it is different from hello default: **TaxiNYC**.</span></span>

<span data-ttu-id="3751d-204">Dans cet exercice, nous allons :</span><span class="sxs-lookup"><span data-stu-id="3751d-204">In this exercise, we will:</span></span>

* <span data-ttu-id="3751d-205">Vous connecter trop**SQL Server Management Studio** en utilisant soit l’authentification Windows ou authentification SQL et hello nom de connexion SQL et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="3751d-205">Connect too**SQL Server Management Studio** using either Windows Authentication or using SQL Authentication and hello SQL login name and password.</span></span>
* <span data-ttu-id="3751d-206">Explorer les distributions de données de quelques champs portant sur différentes périodes.</span><span class="sxs-lookup"><span data-stu-id="3751d-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="3751d-207">Analyser la qualité des données des champs de longitude et de latitude hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-207">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="3751d-208">Générer des étiquettes de classification binaire et multiclasse selon hello **Conseil\_quantité**.</span><span class="sxs-lookup"><span data-stu-id="3751d-208">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="3751d-209">Générer des fonctionnalités et calculer/comparer les distances des trajets.</span><span class="sxs-lookup"><span data-stu-id="3751d-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="3751d-210">Joindre hello deux tables et extraire un échantillon aléatoire qui sera utilisé toobuild modèles.</span><span class="sxs-lookup"><span data-stu-id="3751d-210">Join hello two tables and extract a random sample that will be used toobuild models.</span></span>

<span data-ttu-id="3751d-211">Lorsque vous êtes prêt tooproceed tooAzure Machine Learning, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="3751d-211">When you are ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="3751d-212">Enregistrer hello final SQL requête tooextract et exemple hello données et copier-coller hello requête directement dans un [importer des données] [ import-data] module dans Azure Machine Learning, ou</span><span class="sxs-lookup"><span data-stu-id="3751d-212">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="3751d-213">Conserver hello échantillonnée et données ingénieries que vous prévoyez toouse pour une base de données de création de modèles de table et utilisent la nouvelle table de hello Bonjour [importer des données] [ import-data] module dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3751d-213">Persist hello sampled and engineered data you plan toouse for model building in a new database table and use hello new table in hello [Import Data][import-data] module in Azure Machine Learning.</span></span>

<span data-ttu-id="3751d-214">Dans cette section, nous allons enregistrer hello final interroger tooextract et exemple hello des données.</span><span class="sxs-lookup"><span data-stu-id="3751d-214">In this section we will save hello final query tooextract and sample hello data.</span></span> <span data-ttu-id="3751d-215">méthode deuxième Hello est illustrée dans hello [l’Exploration de données et d’ingénierie de fonctionnalité notebooks bloc-notes](#ipnb) section.</span><span class="sxs-lookup"><span data-stu-id="3751d-215">hello second method is demonstrated in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span>

<span data-ttu-id="3751d-216">Pour une vérification rapide du nombre de hello de lignes et colonnes Bonjour tables remplies précédemment à l’aide d’importation en bloc parallèle,</span><span class="sxs-lookup"><span data-stu-id="3751d-216">For a quick verification of hello number of rows and columns in hello tables populated earlier using parallel bulk import,</span></span>

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="3751d-217">Exploration : distribution des courses par médaillon</span><span class="sxs-lookup"><span data-stu-id="3751d-217">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="3751d-218">Cet exemple identifie le medallion hello (numéros taxi) avec plus de 100 allers-retours pendant une période donnée.</span><span class="sxs-lookup"><span data-stu-id="3751d-218">This example identifies hello medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="3751d-219">requête de Hello tireront parti d’accès à la table hello partitionnée, car il est conditionnée par le schéma de partition hello de **collecte\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="3751d-219">hello query would benefit from hello partitioned table access since it is conditioned by hello partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="3751d-220">Interrogation du jeu de données complet hello rendent également utiliser de table partitionnée de hello et/ou d’analyse d’index.</span><span class="sxs-lookup"><span data-stu-id="3751d-220">Querying hello full dataset will also make use of hello partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="3751d-221">Exploration : distribution des courses par médaillon et par licence de taxi</span><span class="sxs-lookup"><span data-stu-id="3751d-221">Exploration: Trip distribution by medallion and hack_license</span></span>
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="3751d-222">Évaluation de la qualité des données : vérifier les enregistrements avec une longitude et/ou une latitude incorrectes</span><span class="sxs-lookup"><span data-stu-id="3751d-222">Data Quality Assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="3751d-223">Cet exemple examine si un des champs de longitude et/ou latitude hello contenir une valeur non valide (les degrés en radians doivent être comprise entre -90 et 90), ou avoir (0, 0) coordonnées.</span><span class="sxs-lookup"><span data-stu-id="3751d-223">This example investigates if any of hello longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="3751d-224">Exploration : distribution des courses avec et sans pourboire</span><span class="sxs-lookup"><span data-stu-id="3751d-224">Exploration: Tipped vs. Not Tipped Trips distribution</span></span>
<span data-ttu-id="3751d-225">Cet exemple recherche le nombre de hello d’allers-retours qui ont été déposés par rapport aux ne pourboires pas dans un délai donné période (ou dans hello jeu de données complet si couvrant an hello).</span><span class="sxs-lookup"><span data-stu-id="3751d-225">This example finds hello number of trips that were tipped vs. not tipped in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="3751d-226">Cette distribution reflète hello étiquette binaire distribution toobe utilisée ultérieurement pour la modélisation de classification binaire.</span><span class="sxs-lookup"><span data-stu-id="3751d-226">This distribution reflects hello binary label distribution toobe later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="3751d-227">Exploration : distribution des classes/fourchettes de pourboires</span><span class="sxs-lookup"><span data-stu-id="3751d-227">Exploration: Tip Class/Range Distribution</span></span>
<span data-ttu-id="3751d-228">Cet exemple calcule la distribution hello des plages de Conseil dans un délai donné période (ou dans hello jeu de données complet si couvrant an hello).</span><span class="sxs-lookup"><span data-stu-id="3751d-228">This example computes hello distribution of tip ranges in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="3751d-229">Il s’agit de distribution hello des classes d’étiquette hello qui sera utilisée ultérieurement pour la modélisation de classification multiclasse.</span><span class="sxs-lookup"><span data-stu-id="3751d-229">This is hello distribution of hello label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

#### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="3751d-230">Exploration : calculer et comparer les distances des trajets</span><span class="sxs-lookup"><span data-stu-id="3751d-230">Exploration: Compute and Compare Trip Distance</span></span>
<span data-ttu-id="3751d-231">L’exemple suivant convertit la longitude de collecte et de remise hello et latitude tooSQL geography pointe, calcule la distance de voyage hello à l’aide de la différence de points SQL geography et retourne un échantillon aléatoire de résultats hello pour la comparaison.</span><span class="sxs-lookup"><span data-stu-id="3751d-231">This example converts hello pickup and drop-off longitude and latitude tooSQL geography points, computes hello trip distance using SQL geography points difference, and returns a random sample of hello results for comparison.</span></span> <span data-ttu-id="3751d-232">exemple de Hello limite les résultats de hello toovalid coordonne uniquement à l’aide de la requête d’évaluation de la qualité des données d’hello évoqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="3751d-232">hello example limits hello results toovalid coordinates only using hello data quality assessment query covered earlier.</span></span>

    SELECT
    pickup_location=geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326)
    ,dropoff_location=geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326)
    ,trip_distance
    ,computedist=round(geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326).STDistance(geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326))/1000, 2)
    FROM nyctaxi_trip
    tablesample(0.01 percent)
    WHERE CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND   CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

#### <a name="feature-engineering-in-sql-queries"></a><span data-ttu-id="3751d-233">Conception de fonctionnalités dans des requêtes SQL</span><span class="sxs-lookup"><span data-stu-id="3751d-233">Feature Engineering in SQL Queries</span></span>
<span data-ttu-id="3751d-234">Hello étiquette génération geography conversion exploration des requêtes et peuvent également être utilisé toogenerate étiquettes/fonctionnalités en supprimant hello comptage partie.</span><span class="sxs-lookup"><span data-stu-id="3751d-234">hello label generation and geography conversion exploration queries can also be used toogenerate labels/features by removing hello counting part.</span></span> <span data-ttu-id="3751d-235">Exemples SQL ingénieries de fonctionnalités supplémentaires sont fournies dans hello [l’Exploration de données et d’ingénierie de fonctionnalité notebooks bloc-notes](#ipnb) section.</span><span class="sxs-lookup"><span data-stu-id="3751d-235">Additional feature engineering SQL examples are provided in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span> <span data-ttu-id="3751d-236">Il est plus efficace toorun hello fonctionnalités génération de requêtes sur le jeu de données complet hello ou une grande partie de celui-ci à l’aide de requêtes SQL qui s’exécutent directement sur l’instance de base de données SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-236">It is more efficient toorun hello feature generation queries on hello full dataset or a large subset of it using SQL queries which run directly on hello SQL Server database instance.</span></span> <span data-ttu-id="3751d-237">les requêtes Hello peuvent être exécutées dans **SQL Server Management Studio**, notebooks bloc-notes ou n’importe quel outil/environnement de développement permettant d’accéder à hello de base de données localement ou à distance.</span><span class="sxs-lookup"><span data-stu-id="3751d-237">hello queries may be executed in **SQL Server Management Studio**, IPython Notebook or any development tool/environment which can access hello database locally or remotely.</span></span>

#### <a name="preparing-data-for-model-building"></a><span data-ttu-id="3751d-238">Préparation des données pour la création de modèles</span><span class="sxs-lookup"><span data-stu-id="3751d-238">Preparing Data for Model Building</span></span>
<span data-ttu-id="3751d-239">hello de jointures de requête suivant de Hello **nyctaxi\_voyage** et **nyctaxi\_tarif** des tables, génère une étiquette de classification binaire **incliné**, un étiquette de classification multiclasse **Conseil\_classe**et extrait un échantillon aléatoire de 1 % à partir du jeu de données joint hello complète.</span><span class="sxs-lookup"><span data-stu-id="3751d-239">hello following query joins hello **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a 1% random sample from hello full joined dataset.</span></span> <span data-ttu-id="3751d-240">Cette requête peut être copiée, puis collée directement dans hello [Azure Machine Learning Studio](https://studio.azureml.net) [importer des données] [ import-data] module pour l’ingestion de données directement à partir de la base de données SQL Server hello instance dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3751d-240">This query can be copied then pasted directly in hello [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from hello SQL Server database instance in Azure.</span></span> <span data-ttu-id="3751d-241">requête de Hello exclut les enregistrements avec incorrect (0, 0) coordonnées.</span><span class="sxs-lookup"><span data-stu-id="3751d-241">hello query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_trip t, nyctaxi_fare f
    TABLESAMPLE (1 percent)
    WHERE t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'


## <span data-ttu-id="3751d-242"><a name="ipnb"></a>Exploration des données et conception de fonctionnalités dans Notebook IPython</span><span class="sxs-lookup"><span data-stu-id="3751d-242"><a name="ipnb"></a>Data Exploration and Feature Engineering in IPython Notebook</span></span>
<span data-ttu-id="3751d-243">Dans cette section, nous allons effectuer l’exploration de données et de génération de fonctionnalité à l’aide de requêtes de Python et SQL par rapport à la base de données SQL Server hello créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="3751d-243">In this section, we will perform data exploration and feature generation using both Python and SQL queries against hello SQL Server database created earlier.</span></span> <span data-ttu-id="3751d-244">Un bloc-notes de notebooks exemple nommé **machine-Learning-data-science-process-sql-story.ipynb** est fourni dans hello **exemple notebooks Ipython** dossier.</span><span class="sxs-lookup"><span data-stu-id="3751d-244">A sample IPython notebook named **machine-Learning-data-science-process-sql-story.ipynb** is provided in hello **Sample IPython Notebooks** folder.</span></span> <span data-ttu-id="3751d-245">Ce notebook est également disponible sur [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span><span class="sxs-lookup"><span data-stu-id="3751d-245">This notebook is also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span></span>

<span data-ttu-id="3751d-246">Hello séquence recommandée lors de l’utilisation des données volumineuses est suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="3751d-246">hello recommended sequence when working with big data is hello following:</span></span>

* <span data-ttu-id="3751d-247">Lire dans un petit échantillon de données de salutation dans une trame de données en mémoire.</span><span class="sxs-lookup"><span data-stu-id="3751d-247">Read in a small sample of hello data into an in-memory data frame.</span></span>
* <span data-ttu-id="3751d-248">Effectuer des visualisations et à l’aide des explorations hello données échantillonnées.</span><span class="sxs-lookup"><span data-stu-id="3751d-248">Perform some visualizations and explorations using hello sampled data.</span></span>
* <span data-ttu-id="3751d-249">Faites l’expérience de l’ingénierie de fonctionnalité à l’aide de hello exemples de données.</span><span class="sxs-lookup"><span data-stu-id="3751d-249">Experiment with feature engineering using hello sampled data.</span></span>
* <span data-ttu-id="3751d-250">Exploration des données plus volumineux, l’ingénierie de fonctionnalité et de manipulation de données utiliser Python tooissue des requêtes SQL directement sur la base de données SQL Server hello Bonjour Azure VM.</span><span class="sxs-lookup"><span data-stu-id="3751d-250">For larger data exploration, data manipulation and feature engineering, use Python tooissue SQL Queries directly against hello SQL Server database in hello Azure VM.</span></span>
* <span data-ttu-id="3751d-251">Décidez toouse de taille d’échantillon hello pour la construction d’un modèle Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3751d-251">Decide hello sample size toouse for Azure Machine Learning model building.</span></span>

<span data-ttu-id="3751d-252">Quand vous êtes prêt tooproceed tooAzure Machine Learning, vous pouvez soit :</span><span class="sxs-lookup"><span data-stu-id="3751d-252">When ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="3751d-253">Enregistrer hello final SQL requête tooextract et exemple hello données et copier-coller hello requête directement dans un [importer des données] [ import-data] module dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3751d-253">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="3751d-254">Cette méthode est illustrée dans hello [création de modèles dans Azure Machine Learning](#mlmodel) section.</span><span class="sxs-lookup"><span data-stu-id="3751d-254">This method is demonstrated in hello [Building Models in Azure Machine Learning](#mlmodel) section.</span></span>    
2. <span data-ttu-id="3751d-255">Conserver hello échantillonnées et données ingénieries que vous prévoyez toouse pour dans une nouvelle table de base de données de création de modèles, puis utiliser la nouvelle table de hello Bonjour [importer des données] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="3751d-255">Persist hello sampled and engineered data you plan toouse for model building in a new database table, then use hello new table in hello [Import Data][import-data] module.</span></span>

<span data-ttu-id="3751d-256">Hello Voici quelques exemples d’ingénierie de fonctionnalité, exploration de données et visualisation des données.</span><span class="sxs-lookup"><span data-stu-id="3751d-256">hello following are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="3751d-257">Pour plus d’exemples, consultez bloc-notes de SQL notebooks exemple hello Bonjour **exemple notebooks Ipython** dossier.</span><span class="sxs-lookup"><span data-stu-id="3751d-257">For more examples, see hello sample SQL IPython notebook in hello **Sample IPython Notebooks** folder.</span></span>

#### <a name="initialize-database-credentials"></a><span data-ttu-id="3751d-258">Initialiser les informations d’identification de la base de données</span><span class="sxs-lookup"><span data-stu-id="3751d-258">Initialize Database Credentials</span></span>
<span data-ttu-id="3751d-259">Initialiser vos paramètres de connexion de base de données Bonjour suivant variables :</span><span class="sxs-lookup"><span data-stu-id="3751d-259">Initialize your database connection settings in hello following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a><span data-ttu-id="3751d-260">Créer une connexion à la base de données</span><span class="sxs-lookup"><span data-stu-id="3751d-260">Create Database Connection</span></span>
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="3751d-261">Afficher le nombre de lignes et de colonnes de la table nyctaxi_trip</span><span class="sxs-lookup"><span data-stu-id="3751d-261">Report number of rows and columns in table nyctaxi_trip</span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('nyctaxi_trip')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('nyctaxi_trip')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="3751d-262">Nombre total de lignes = 173 179 759</span><span class="sxs-lookup"><span data-stu-id="3751d-262">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="3751d-263">Nombre total de colonnes = 14</span><span class="sxs-lookup"><span data-stu-id="3751d-263">Total number of columns = 14</span></span>

#### <a name="read-in-a-small-data-sample-from-hello-sql-server-database"></a><span data-ttu-id="3751d-264">Lecture dans un échantillon de données de petite taille à partir de hello de base de données SQL Server</span><span class="sxs-lookup"><span data-stu-id="3751d-264">Read-in a small data sample from hello SQL Server Database</span></span>
    t0 = time.time()

    query = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (0.05 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="3751d-265">Table d’exemple hello temps tooread est 6.492000 secondes</span><span class="sxs-lookup"><span data-stu-id="3751d-265">Time tooread hello sample table is 6.492000 seconds</span></span>  
<span data-ttu-id="3751d-266">Nombre de lignes et de colonnes récupérées = (84 952, 21)</span><span class="sxs-lookup"><span data-stu-id="3751d-266">Number of rows and columns retrieved = (84952, 21)</span></span>

#### <a name="descriptive-statistics"></a><span data-ttu-id="3751d-267">Statistiques descriptives</span><span class="sxs-lookup"><span data-stu-id="3751d-267">Descriptive Statistics</span></span>
<span data-ttu-id="3751d-268">Sont maintenant des données de hello échantillonnée de tooexplore prêt.</span><span class="sxs-lookup"><span data-stu-id="3751d-268">Now are ready tooexplore hello sampled data.</span></span> <span data-ttu-id="3751d-269">Nous commençons avec examinant les statistiques descriptives pour hello **voyage\_distance** (ou tout autre) (s) :</span><span class="sxs-lookup"><span data-stu-id="3751d-269">We start with looking at descriptive statistics for hello **trip\_distance** (or any other) field(s):</span></span>

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a><span data-ttu-id="3751d-270">Visualisation : exemple de diagramme à surfaces</span><span class="sxs-lookup"><span data-stu-id="3751d-270">Visualization: Box Plot Example</span></span>
<span data-ttu-id="3751d-271">Examinez maintenant surfaces hello pour hello voyage distance toovisualize hello quantiles</span><span class="sxs-lookup"><span data-stu-id="3751d-271">Next we look at hello box plot for hello trip distance toovisualize hello quantiles</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Diagramme #1][1]

#### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="3751d-273">Visualisation : exemple de diagramme de distribution</span><span class="sxs-lookup"><span data-stu-id="3751d-273">Visualization: Distribution Plot Example</span></span>
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Diagramme #2][2]

#### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="3751d-275">Visualisation : diagrammes en bâtons et linéaires</span><span class="sxs-lookup"><span data-stu-id="3751d-275">Visualization: Bar and Line Plots</span></span>
<span data-ttu-id="3751d-276">Dans cet exemple, nous bin distance de voyage hello dans cinq compartiments et visualiser hello placement des résultats.</span><span class="sxs-lookup"><span data-stu-id="3751d-276">In this example, we bin hello trip distance into five bins and visualize hello binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="3751d-277">Nous pouvons tracer hello au-dessus de distribution d’emplacement dans une barre ou de la ligne de traçage comme indiqué ci-dessous</span><span class="sxs-lookup"><span data-stu-id="3751d-277">We can plot hello above bin distribution in a bar or line plot as below</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Diagramme #3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Diagramme #4][4]

#### <a name="visualization-scatterplot-example"></a><span data-ttu-id="3751d-280">Visualisation : exemple de diagramme de dispersion</span><span class="sxs-lookup"><span data-stu-id="3751d-280">Visualization: Scatterplot Example</span></span>
<span data-ttu-id="3751d-281">Nous allons montrer nuage entre **voyage\_temps\_dans\_secondes** et **voyage\_distance** toosee s’il existe une corrélation</span><span class="sxs-lookup"><span data-stu-id="3751d-281">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** toosee if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Diagramme #6][6]

<span data-ttu-id="3751d-283">De même, nous pouvons vérifier relation hello entre **taux\_code** et **voyage\_distance**.</span><span class="sxs-lookup"><span data-stu-id="3751d-283">Similarly we can check hello relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Diagramme #8][8]

### <a name="sub-sampling-hello-data-in-sql"></a><span data-ttu-id="3751d-285">Hello de sous-échantillonnage données dans SQL</span><span class="sxs-lookup"><span data-stu-id="3751d-285">Sub-Sampling hello Data in SQL</span></span>
<span data-ttu-id="3751d-286">Lorsque vous préparez des données pour le modèle de génération dans [Azure Machine Learning Studio](https://studio.azureml.net), vous pouvez décider soit de hello **toouse de requête SQL directement dans le module d’importation de données hello** ou de les conserver hello conçues et échantillonnées les données dans une nouvelle table, vous pouvez utiliser dans hello [importer des données] [ import-data] module avec un simple **sélectionner * FROM < votre\_nouveau\_table\_nom >**.</span><span class="sxs-lookup"><span data-stu-id="3751d-286">When preparing data for model building in [Azure Machine Learning Studio](https://studio.azureml.net), you may either decide on hello **SQL query toouse directly in hello Import Data module** or persist hello engineered and sampled data in a new table, which you could use in hello [Import Data][import-data] module with a simple **SELECT * FROM <your\_new\_table\_name>**.</span></span>

<span data-ttu-id="3751d-287">Dans cette section, que nous allons créer un nouveau Bonjour de toohold table échantillonnées et conçu des données.</span><span class="sxs-lookup"><span data-stu-id="3751d-287">In this section we will create a new table toohold hello sampled and engineered data.</span></span> <span data-ttu-id="3751d-288">Un exemple d’une requête SQL directe pour la génération de modèle est fourni dans hello [l’Exploration de données et d’ingénierie de fonctionnalité dans SQL Server](#dbexplore) section.</span><span class="sxs-lookup"><span data-stu-id="3751d-288">An example of a direct SQL query for model building is provided in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="create-a-sample-table-and-populate-with-1-of-hello-joined-tables-drop-table-first-if-it-exists"></a><span data-ttu-id="3751d-289">Créer un exemple de Table et la remplir avec 1 % des Tables jointes de hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-289">Create a Sample Table and Populate with 1% of hello Joined Tables.</span></span> <span data-ttu-id="3751d-290">en commençant par supprimer la table si elle existe</span><span class="sxs-lookup"><span data-stu-id="3751d-290">Drop Table First if it Exists.</span></span>
<span data-ttu-id="3751d-291">Dans cette section, nous joindre des tables de hello **nyctaxi\_voyage** et **nyctaxi\_tarif**, extraire un échantillon aléatoire de 1 % et conserver les données de hello échantillonnée dans un nouveau nom de table  **nyctaxi\_un\_%**:</span><span class="sxs-lookup"><span data-stu-id="3751d-291">In this section, we join hello tables **nyctaxi\_trip** and **nyctaxi\_fare**, extract a 1% random sample, and persist hello sampled data in a new table name **nyctaxi\_one\_percent**:</span></span>

    cursor = conn.cursor()

    drop_table_if_exists = '''
        IF OBJECT_ID('nyctaxi_one_percent', 'U') IS NOT NULL DROP TABLE nyctaxi_one_percent
    '''

    nyctaxi_one_percent_insert = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount
        INTO nyctaxi_one_percent
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (1 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
        AND   pickup_longitude <> '0' AND dropoff_longitude <> '0'
    '''

    cursor.execute(drop_table_if_exists)
    cursor.execute(nyctaxi_one_percent_insert)
    cursor.commit()

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="3751d-292">Exploration des données à l’aide de requêtes SQL dans Notebook IPython</span><span class="sxs-lookup"><span data-stu-id="3751d-292">Data Exploration using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="3751d-293">Dans cette section, nous explorons les distributions de données à l’aide des données de 1 % échantillonnée hello qui sont conservées dans hello nouvelle table créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="3751d-293">In this section, we explore data distributions using hello 1% sampled data which is persisted in hello new table we created above.</span></span> <span data-ttu-id="3751d-294">Notez que des explorations similaire peuvent être effectuées à l’aide de tables d’origine hello, éventuellement à l’aide de **TABLESAMPLE** toolimit exploration d’hello exemple ou en limitant hello résultats tooa étant donné la période de temps à l’aide de hello **collecte \_datetime** partitions, comme illustré dans hello [l’Exploration de données et d’ingénierie de fonctionnalité dans SQL Server](#dbexplore) section.</span><span class="sxs-lookup"><span data-stu-id="3751d-294">Note that similar explorations can be performed using hello original tables, optionally using **TABLESAMPLE** toolimit hello exploration sample or by limiting hello results tooa given time period using hello **pickup\_datetime** partitions, as illustrated in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="3751d-295">Exploration : distribution quotidienne des courses</span><span class="sxs-lookup"><span data-stu-id="3751d-295">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="3751d-296">Exploration : distribution des courses par médaillon</span><span class="sxs-lookup"><span data-stu-id="3751d-296">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="3751d-297">Génération de fonctionnalités à l’aide de requêtes SQL dans Notebook IPython</span><span class="sxs-lookup"><span data-stu-id="3751d-297">Feature Generation Using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="3751d-298">Dans cette section, nous allons générer nouvelles étiquettes et fonctionnalités directement à l’aide de requêtes SQL, sur la table de 1 % exemple hello nous avons créé dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-298">In this section we will generate new labels and features directly using SQL queries, operating on hello 1% sample table we created in hello previous section.</span></span>

#### <a name="label-generation-generate-class-labels"></a><span data-ttu-id="3751d-299">Génération d’étiquettes : générer des étiquettes de classe</span><span class="sxs-lookup"><span data-stu-id="3751d-299">Label Generation: Generate Class Labels</span></span>
<span data-ttu-id="3751d-300">Bonjour l’exemple suivant, nous générons deux ensembles de toouse étiquettes pour la modélisation :</span><span class="sxs-lookup"><span data-stu-id="3751d-300">In hello following example, we generate two sets of labels toouse for modeling:</span></span>

1. <span data-ttu-id="3751d-301">Étiquettes de classe binaires **tipped** (prédisant si un pourboire va être versé)</span><span class="sxs-lookup"><span data-stu-id="3751d-301">Binary Class Labels **tipped** (predicting if a tip will be given)</span></span>
2. <span data-ttu-id="3751d-302">Étiquettes multiclasses **Conseil\_classe** (prédiction d’emplacement de conseil hello ou plage)</span><span class="sxs-lookup"><span data-stu-id="3751d-302">Multiclass Labels **tip\_class** (predicting hello tip bin or range)</span></span>
   
        nyctaxi_one_percent_add_col = '''
            ALTER TABLE nyctaxi_one_percent ADD tipped bit, tip_class int
        '''
   
        cursor.execute(nyctaxi_one_percent_add_col)
        cursor.commit()
   
        nyctaxi_one_percent_update_col = '''
            UPDATE nyctaxi_one_percent
            SET
               tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
               tip_class = CASE WHEN (tip_amount = 0) THEN 0
                                WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                                WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                                WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                                ELSE 4
                            END
        '''
   
        cursor.execute(nyctaxi_one_percent_update_col)
        cursor.commit()

#### <a name="feature-engineering-count-features-for-categorical-columns"></a><span data-ttu-id="3751d-303">Conception de fonctionnalités : fonctionnalités de décompte pour les colonnes catégorielles</span><span class="sxs-lookup"><span data-stu-id="3751d-303">Feature Engineering: Count Features for Categorical Columns</span></span>
<span data-ttu-id="3751d-304">Cet exemple transforme un champ de catégorie dans un champ numérique en remplaçant chaque catégorie de nombre de hello de ses occurrences dans les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="3751d-304">This example transforms a categorical field into a numeric field by replacing each category with hello count of its occurrences in hello data.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD cmt_count int, vts_count int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B AS
        (
            SELECT medallion, hack_license,
                SUM(CASE WHEN vendor_id = 'cmt' THEN 1 ELSE 0 END) AS cmt_count,
                SUM(CASE WHEN vendor_id = 'vts' THEN 1 ELSE 0 END) AS vts_count
            FROM nyctaxi_one_percent
            GROUP BY medallion, hack_license
        )

        UPDATE nyctaxi_one_percent
        SET nyctaxi_one_percent.cmt_count = B.cmt_count,
            nyctaxi_one_percent.vts_count = B.vts_count
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion AND A.hack_license = B.hack_license
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a><span data-ttu-id="3751d-305">Conception de fonctionnalités : fonctionnalités de compartimentage pour les colonnes numériques</span><span class="sxs-lookup"><span data-stu-id="3751d-305">Feature Engineering: Bin features for Numerical Columns</span></span>
<span data-ttu-id="3751d-306">Cet exemple transforme un champ numérique continu en plages de catégories prédéfinies ; autrement dit, il transforme un champ numérique en champ catégoriel.</span><span class="sxs-lookup"><span data-stu-id="3751d-306">This example transforms a continuous numeric field into preset category ranges, i.e., transform numeric field into a categorical field.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD trip_time_bin int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B(medallion,hack_license,pickup_datetime,trip_time_in_secs, BinNumber ) AS
        (
            SELECT medallion,hack_license,pickup_datetime,trip_time_in_secs,
            NTILE(5) OVER (ORDER BY trip_time_in_secs) AS BinNumber from nyctaxi_one_percent
        )

        UPDATE nyctaxi_one_percent
        SET trip_time_bin = B.BinNumber
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion
        AND A.hack_license = B.hack_license
        AND A.pickup_datetime = B.pickup_datetime
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a><span data-ttu-id="3751d-307">Conception de fonctionnalités : extraire des fonctionnalités d’emplacement des valeurs décimales de latitude/longitude</span><span class="sxs-lookup"><span data-stu-id="3751d-307">Feature Engineering: Extract Location Features from Decimal Latitude/Longitude</span></span>
<span data-ttu-id="3751d-308">Cet exemple décompose hello décimal à un champ de latitude et/ou longitude en plusieurs champs de la région de granularité différente, par exemple, pays, ville, ville, bloc, etc.. Notez que hello nouvelle géo-champs ne sont pas mappées tooactual emplacements.</span><span class="sxs-lookup"><span data-stu-id="3751d-308">This example breaks down hello decimal representation of a latitude and/or longitude field into multiple region fields of different granularity, such as, country, city, town, block, etc. Note that hello new geo-fields are not mapped tooactual locations.</span></span> <span data-ttu-id="3751d-309">Pour plus d’informations sur le mappage des emplacements associés à un géocode, consultez l’article consacré aux [Services REST de Bing Cartes](https://msdn.microsoft.com/library/ff701710.aspx).</span><span class="sxs-lookup"><span data-stu-id="3751d-309">For information on mapping geocode locations, see [Bing Maps REST Services](https://msdn.microsoft.com/library/ff701710.aspx).</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent
        ADD l1 varchar(6), l2 varchar(3), l3 varchar(3), l4 varchar(3),
            l5 varchar(3), l6 varchar(3), l7 varchar(3)
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        UPDATE nyctaxi_one_percent
        SET l1=round(pickup_longitude,0)
            , l2 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 1 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),1,1) ELSE '0' END     
            , l3 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 2 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),2,1) ELSE '0' END     
            , l4 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 3 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),3,1) ELSE '0' END     
            , l5 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 4 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),4,1) ELSE '0' END     
            , l6 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 5 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),5,1) ELSE '0' END     
            , l7 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 6 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),6,1) ELSE '0' END
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a><span data-ttu-id="3751d-310">Vérifiez la forme finale de la table de fonctionnalités hello de hello</span><span class="sxs-lookup"><span data-stu-id="3751d-310">Verify hello final form of hello featurized table</span></span>
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

<span data-ttu-id="3751d-311">Vous voilà prêt tooproceed toomodel génération et déploiement de modèle dans [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="3751d-311">We are now ready tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="3751d-312">les données de salutation sont prêtes pour un des problèmes de prédiction hello identifiées précédemment, à savoir :</span><span class="sxs-lookup"><span data-stu-id="3751d-312">hello data is ready for any of hello prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="3751d-313">Classification binaire : toopredict ou non un Conseil a été payé un voyage.</span><span class="sxs-lookup"><span data-stu-id="3751d-313">Binary classification: toopredict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="3751d-314">Classification multiclasse : plage de hello toopredict d’info-bulle payé, en fonction de toohello classes précédemment définies.</span><span class="sxs-lookup"><span data-stu-id="3751d-314">Multiclass classification: toopredict hello range of tip paid, according toohello previously defined classes.</span></span>
3. <span data-ttu-id="3751d-315">Tâche de régression : toopredict hello d’info-bulle montant d’un voyage.</span><span class="sxs-lookup"><span data-stu-id="3751d-315">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="3751d-316"><a name="mlmodel"></a>Création de modèles dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3751d-316"><a name="mlmodel"></a>Building Models in Azure Machine Learning</span></span>
<span data-ttu-id="3751d-317">toobegin hello exercice de modélisation, ouvrez une session dans l’espace de travail Azure Machine Learning tooyour.</span><span class="sxs-lookup"><span data-stu-id="3751d-317">toobegin hello modeling exercise, log in tooyour Azure Machine Learning workspace.</span></span> <span data-ttu-id="3751d-318">Si vous n’avez pas encore créé d’espace de travail d’apprentissage automatique, consultez l’article [Créer un espace de travail Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="3751d-318">If you have not yet created a machine learning workspace, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="3751d-319">tooget main d’Azure Machine Learning, consultez [Nouveautés d’Azure Machine Learning Studio ?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="3751d-319">tooget started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="3751d-320">Connectez-vous trop[Azure Machine Learning Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="3751d-320">Log in too[Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="3751d-321">page d’accueil Studio Hello fournit une mine d’informations, des vidéos, didacticiels, des liens toohello référence des Modules et autres ressources.</span><span class="sxs-lookup"><span data-stu-id="3751d-321">hello Studio Home page provides a wealth of information, videos, tutorials, links toohello Modules Reference, and other resources.</span></span> <span data-ttu-id="3751d-322">Pour plus d’informations sur Azure Machine Learning, consultez hello [centre de Documentation Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="3751d-322">Fore more information about Azure Machine Learning, consult hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="3751d-323">Une expérience de formation standard se compose de suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="3751d-323">A typical training experiment consists of hello following:</span></span>

1. <span data-ttu-id="3751d-324">Création d’une expérience à l’aide du bouton **+NOUVEAU** .</span><span class="sxs-lookup"><span data-stu-id="3751d-324">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="3751d-325">Obtenir hello données tooAzure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3751d-325">Get hello data tooAzure Machine Learning.</span></span>
3. <span data-ttu-id="3751d-326">Prétraiter, transformer et manipuler des données de hello en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="3751d-326">Pre-process, transform and manipulate hello data as needed.</span></span>
4. <span data-ttu-id="3751d-327">Génération des fonctionnalités requises.</span><span class="sxs-lookup"><span data-stu-id="3751d-327">Generate features as needed.</span></span>
5. <span data-ttu-id="3751d-328">Fractionner les données de hello en jeux de données d’apprentissage/validation/test (ou avoir des jeux de données distincts pour chaque).</span><span class="sxs-lookup"><span data-stu-id="3751d-328">Split hello data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="3751d-329">Sélectionnez un ou plusieurs algorithmes d’apprentissage en fonction de hello toosolve de problème d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="3751d-329">Select one or more machine learning algorithms depending on hello learning problem toosolve.</span></span> <span data-ttu-id="3751d-330">Exemples : classification binaire, classification multiclasse, régression.</span><span class="sxs-lookup"><span data-stu-id="3751d-330">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="3751d-331">L’apprentissage d’un ou plusieurs modèles à l’aide du jeu de données d’apprentissage hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-331">Train one or more models using hello training dataset.</span></span>
8. <span data-ttu-id="3751d-332">Un score de jeu de données de validation hello à l’aide de modèles formés de hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-332">Score hello validation dataset using hello trained model(s).</span></span>
9. <span data-ttu-id="3751d-333">Évaluer hello ou les modèles toocompute hello mesures pour hello problème d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="3751d-333">Evaluate hello model(s) toocompute hello relevant metrics for hello learning problem.</span></span>
10. <span data-ttu-id="3751d-334">Réglage de l’ou les modèles hello et sélectionnez hello meilleur modèle toodeploy.</span><span class="sxs-lookup"><span data-stu-id="3751d-334">Fine tune hello model(s) and select hello best model toodeploy.</span></span>

<span data-ttu-id="3751d-335">Dans cet exercice, nous avons déjà exploré et conçu données hello dans SQL Server et décidé sur tooingest de taille d’échantillon hello dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3751d-335">In this exercise, we have already explored and engineered hello data in SQL Server, and decided on hello sample size tooingest in Azure Machine Learning.</span></span> <span data-ttu-id="3751d-336">toobuild une ou plusieurs des modèles de prévision hello que nous avons décidé :</span><span class="sxs-lookup"><span data-stu-id="3751d-336">toobuild one or more of hello prediction models we decided:</span></span>

1. <span data-ttu-id="3751d-337">Obtenir des données de hello tooAzure Machine Learning à l’aide de hello [importer des données] [ import-data] module, disponible dans hello **données d’entrée et sortie** section.</span><span class="sxs-lookup"><span data-stu-id="3751d-337">Get hello data tooAzure Machine Learning using hello [Import Data][import-data] module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="3751d-338">Pour plus d’informations, consultez hello [importer des données] [ import-data] page de référence de module.</span><span class="sxs-lookup"><span data-stu-id="3751d-338">For more information, see hello [Import Data][import-data] module reference page.</span></span>
   
    ![Importation de données Azure Machine Learning][17]
2. <span data-ttu-id="3751d-340">Sélectionnez **base de données SQL Azure** comme hello **source de données** Bonjour **propriétés** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="3751d-340">Select **Azure SQL Database** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="3751d-341">Entrez le nom DNS de base de données hello Bonjour **nom du serveur de base de données** champ.</span><span class="sxs-lookup"><span data-stu-id="3751d-341">Enter hello database DNS name in hello **Database server name** field.</span></span> <span data-ttu-id="3751d-342">Format : `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="3751d-342">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="3751d-343">Entrez hello **nom de la base de données** dans le champ correspondant de hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-343">Enter hello **Database name** in hello corresponding field.</span></span>
5. <span data-ttu-id="3751d-344">Entrez hello **nom d’utilisateur SQL** Bonjour ** aqccount nom d’utilisateur et mot de passe hello Bonjour **mot de passe utilisateur Server**.</span><span class="sxs-lookup"><span data-stu-id="3751d-344">Enter hello **SQL user name** in hello **Server user aqccount name, and hello password in hello **Server user account password**.</span></span>
6. <span data-ttu-id="3751d-345">Activez l’option **Accepter tout certificat de serveur** .</span><span class="sxs-lookup"><span data-stu-id="3751d-345">Check **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="3751d-346">Bonjour **requête de base de données** modifier la zone de texte, collez la requête hello extrait hello nécessaire (y compris les champs calculés tels que des étiquettes de hello) des champs de base de données et le bas exemples de taille d’échantillon hello données toohello souhaité.</span><span class="sxs-lookup"><span data-stu-id="3751d-346">In hello **Database query** edit text area, paste hello query which extracts hello necessary database fields (including any computed fields such as hello labels) and down samples hello data toohello desired sample size.</span></span>

<span data-ttu-id="3751d-347">Un exemple d’une expérience de classification binaire la lecture des données directement à partir de la base de données SQL Server hello est figure hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3751d-347">An example of a binary classification experiment reading data directly from hello SQL Server database is in hello figure below.</span></span> <span data-ttu-id="3751d-348">Vous pouvez créer des expériences similaires pour les problèmes de classification multiclasse et de régression.</span><span class="sxs-lookup"><span data-stu-id="3751d-348">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Formation Azure Machine Learning Studio][10]

> [!IMPORTANT]
> <span data-ttu-id="3751d-350">Bonjour, extraction de données de modélisation et de l’échantillonnage des exemples de requêtes fournis dans les sections précédentes, **toutes les étiquettes pour les exercices de modélisation hello trois sont inclus dans la requête de hello**.</span><span class="sxs-lookup"><span data-stu-id="3751d-350">In hello modeling data extraction and sampling query examples provided in previous sections, **all labels for hello three modeling exercises are included in hello query**.</span></span> <span data-ttu-id="3751d-351">Une étape importante (obligatoire) dans chacun des exercices de modélisation de hello est trop**exclure** hello étiquettes inutiles pour hello autres deux problèmes, ainsi que tout autre **cible fuites**.</span><span class="sxs-lookup"><span data-stu-id="3751d-351">An important (required) step in each of hello modeling exercises is too**exclude** hello unnecessary labels for hello other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="3751d-352">Pour, par exemple, lors de l’utilisation de classification binaire, utiliser hello étiquette **incliné** et exclure les champs hello **Conseil\_classe**, **Conseil\_quantité**, et **total\_quantité**.</span><span class="sxs-lookup"><span data-stu-id="3751d-352">For e.g., when using binary classification, use hello label **tipped** and exclude hello fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="3751d-353">Hello dernier paiement des fuites de cible, car elles impliquent l’info-bulle hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-353">hello latter are target leaks since they imply hello tip paid.</span></span>
> 
> <span data-ttu-id="3751d-354">les colonnes inutiles tooexclude et/ou des fuites de cible, vous pouvez utiliser hello [sélectionner les colonnes dans le jeu de données] [ select-columns] module ou hello [modifier les métadonnées] [ edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="3751d-354">tooexclude unnecessary columns and/or target leaks, you may use hello [Select Columns in Dataset][select-columns] module or hello [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="3751d-355">Pour plus d’informations, consultez les pages de référence [Sélectionner des colonnes dans le jeu de données][select-columns] et [Modifier les métadonnées][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="3751d-355">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="3751d-356"><a name="mldeploy"></a>Déploiement de modèles dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3751d-356"><a name="mldeploy"></a>Deploying Models in Azure Machine Learning</span></span>
<span data-ttu-id="3751d-357">Lorsque votre modèle est prêt, vous pouvez la déployer facilement en tant qu’un service web directement à partir de l’expérience de hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-357">When your model is ready, you can easily deploy it as a web service directly from hello experiment.</span></span> <span data-ttu-id="3751d-358">Pour plus d’informations sur le déploiement de services web Azure Machine Learning, consultez [Déployer un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="3751d-358">For more information about deploying Azure Machine Learning web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="3751d-359">toodeploy un nouveau service web, vous devez :</span><span class="sxs-lookup"><span data-stu-id="3751d-359">toodeploy a new web service, you need to:</span></span>

1. <span data-ttu-id="3751d-360">créer une expérience de notation ;</span><span class="sxs-lookup"><span data-stu-id="3751d-360">Create a scoring experiment.</span></span>
2. <span data-ttu-id="3751d-361">Déployer un service web de hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-361">Deploy hello web service.</span></span>

<span data-ttu-id="3751d-362">toocreate une expérience d’un score d’un **terminé** expérience d’apprentissage, cliquez sur **créer une expérience de score** dans la barre d’action hello inférieur.</span><span class="sxs-lookup"><span data-stu-id="3751d-362">toocreate a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in hello lower action bar.</span></span>

![Notation Azure][18]

<span data-ttu-id="3751d-364">Azure Machine Learning tentera toocreate expérience de score basée sur les composants hello d’expérience de formation hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-364">Azure Machine Learning will attempt toocreate a scoring experiment based on hello components of hello training experiment.</span></span> <span data-ttu-id="3751d-365">Il va notamment :</span><span class="sxs-lookup"><span data-stu-id="3751d-365">In particular, it will:</span></span>

1. <span data-ttu-id="3751d-366">Enregistrer le modèle formé de hello et supprimer des modules de formation du modèle hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-366">Save hello trained model and remove hello model training modules.</span></span>
2. <span data-ttu-id="3751d-367">Identifier un opérateur logique **port d’entrée** toorepresent hello attendue de schéma de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="3751d-367">Identify a logical **input port** toorepresent hello expected input data schema.</span></span>
3. <span data-ttu-id="3751d-368">Identifier un opérateur logique **port de sortie** schéma de sortie de service toorepresent hello web attendu.</span><span class="sxs-lookup"><span data-stu-id="3751d-368">Identify a logical **output port** toorepresent hello expected web service output schema.</span></span>

<span data-ttu-id="3751d-369">Lors de la création de hello expérience de score, examiner et ajuster en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="3751d-369">When hello scoring experiment is created, review it and adjust as needed.</span></span> <span data-ttu-id="3751d-370">Un ajustement standard est tooreplace hello jeu de données d’entrée et/ou de la requête avec l’une qui exclut les champs d’étiquette, car il ne sera pas disponibles lorsque le service de hello est appelé.</span><span class="sxs-lookup"><span data-stu-id="3751d-370">A typical adjustment is tooreplace hello input dataset and/or query with one which excludes label fields, as these will not be available when hello service is called.</span></span> <span data-ttu-id="3751d-371">Il est également qu'une taille de hello tooreduce bonnes pratiques de hello d’entrée tooa de jeu de données et/ou des requêtes peu d’enregistrements, juste assez schéma d’entrée de tooindicate hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-371">It is also a good practice tooreduce hello size of hello input dataset and/or query tooa few records, just enough tooindicate hello input schema.</span></span> <span data-ttu-id="3751d-372">Pour le port de sortie hello, il est commun tooexclude entrées tous les champs et uniquement inclure hello **Scored Labels** et **des probabilités notées** Bonjour de sortie à l’aide de hello [sélectionner les colonnes dans le jeu de données ] [ select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="3751d-372">For hello output port, it is common tooexclude all input fields and only include hello **Scored Labels** and **Scored Probabilities** in hello output using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="3751d-373">Un exemple d’expérience de score est figure hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3751d-373">A sample scoring experiment is in hello figure below.</span></span> <span data-ttu-id="3751d-374">Quand vous êtes prêt toodeploy, cliquez sur hello **publier le SERVICE WEB** bouton dans la barre d’action hello inférieur.</span><span class="sxs-lookup"><span data-stu-id="3751d-374">When ready toodeploy, click hello **PUBLISH WEB SERVICE** button in hello lower action bar.</span></span>

![Publication Azure Machine Learning][11]

<span data-ttu-id="3751d-376">toorecap, dans ce didacticiel de la procédure pas à pas, vous avez créé un environnement de science des données Azure, travaillé avec un jeu de données publique volumineux tous les moyen hello de toomodel d’acquisition de données d’apprentissage et de déploiement d’un service web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3751d-376">toorecap, in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset all hello way from data acquisition toomodel training and deploying of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="3751d-377">Informations de licence</span><span class="sxs-lookup"><span data-stu-id="3751d-377">License Information</span></span>
<span data-ttu-id="3751d-378">Cet exemple de procédure et accompagne des scripts et des notebooks notebook(s) sont partagées par Microsoft sous licence du MIT hello.</span><span class="sxs-lookup"><span data-stu-id="3751d-378">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="3751d-379">Vérifiez fichier hello le répertoire hello hello exemple de code sur GitHub pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="3751d-379">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

### <a name="references"></a><span data-ttu-id="3751d-380">Références</span><span class="sxs-lookup"><span data-stu-id="3751d-380">References</span></span>
<span data-ttu-id="3751d-381">•    [Page de téléchargement des jeux de données NYC Taxi Trips par Andrés Monroy (en anglais)](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="3751d-381">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="3751d-382">•    [Page de partage des données relatives aux courses en taxi new-yorkais par Chris Whong (en anglais)](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="3751d-382">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="3751d-383">•    [Page de recherche et de statistiques de la Commission des services de taxis et de limousines de la ville de New York (en anglais)](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="3751d-383">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sql-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sql-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sql-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sql-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sql-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sql-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sql-walkthrough/amlscoring.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
