---
title: 'Processus TDSP (Team Data Science Process) en action : utilisation de SQL Data Warehouse | Microsoft Docs'
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
ms.openlocfilehash: ce7de48af0f2f21576c66a962b88635a0f9f8333
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action-using-sql-data-warehouse"></a><span data-ttu-id="f2164-103">Processus TDSP (Team Data Science Process) en action : utilisation de SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f2164-103">The Team Data Science Process in action: using SQL Data Warehouse</span></span>
<span data-ttu-id="f2164-104">Dans ce didacticiel, nous vous guidons dans la création et le déploiement d’un modèle d’apprentissage automatique utilisant SQL Data Warehouse (SQL DW) pour un jeu de données disponible publiquement, le jeu de données [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="f2164-104">In this tutorial, we walk you through building and deploying a machine learning model using SQL Data Warehouse (SQL DW) for a publicly available dataset -- the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="f2164-105">Le modèle de classification binaire établi prédit si un pourboire a été donné pour une course. Des modèles de classification multiclasse et de régression sont également présentés, qui prévoient la distribution des montants de pourboire réglés.</span><span class="sxs-lookup"><span data-stu-id="f2164-105">The binary classification model constructed predicts whether or not a tip is paid for a trip, and models for multiclass classification and regression are also discussed that predict the distribution for the tip amounts paid.</span></span>

<span data-ttu-id="f2164-106">La procédure suit le flux de travail [processus TDSP (Team Data Science Process)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) .</span><span class="sxs-lookup"><span data-stu-id="f2164-106">The procedure follows the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) workflow.</span></span> <span data-ttu-id="f2164-107">Nous montrons comment configurer un environnement de science des données, comment charger les données dans SQL DW et comment utiliser SQL DW ou un IPython Notebook pour explorer les données et les caractéristiques d’ingénierie à modéliser.</span><span class="sxs-lookup"><span data-stu-id="f2164-107">We show how to setup a data science environment, how to load the data into SQL DW, and how use either SQL DW or an IPython Notebook to explore the data and engineer features to model.</span></span> <span data-ttu-id="f2164-108">Nous expliquons ensuite comment générer et déployer un modèle avec Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f2164-108">We then show how to build and deploy a model with Azure Machine Learning.</span></span>

## <span data-ttu-id="f2164-109"><a name="dataset"></a>Jeu de données NYC Taxi Trips</span><span class="sxs-lookup"><span data-stu-id="f2164-109"><a name="dataset"></a>The NYC Taxi Trips dataset</span></span>
<span data-ttu-id="f2164-110">Les données NYC Taxi Trip sont constituées de fichiers CSV compressés d’une taille totale approximative de 20 Go (soit environ 48 Go après la décompression des fichiers), correspondant à plus de 173 millions de courses et au prix de chacune.</span><span class="sxs-lookup"><span data-stu-id="f2164-110">The NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="f2164-111">Chaque enregistrement de course inclut le lieu et l’heure d’embarquement et de débarquement, le numéro de licence (du chauffeur) rendu anonyme et le numéro de médaillon (numéro d’identification unique) du taxi.</span><span class="sxs-lookup"><span data-stu-id="f2164-111">Each trip record includes the pickup and drop-off locations and times, anonymized hack (driver's) license number, and the medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="f2164-112">Les données portent sur toutes les courses effectuées en 2013 et sont fournies dans les deux jeux de données ci-après pour chaque mois :</span><span class="sxs-lookup"><span data-stu-id="f2164-112">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

1. <span data-ttu-id="f2164-113">Le fichier **trip_data.csv** contient les détails de chaque course, comme le nombre de passagers, les points d’embarquement et de débarquement, la durée du trajet et la distance parcourue.</span><span class="sxs-lookup"><span data-stu-id="f2164-113">The **trip_data.csv** file contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="f2164-114">Voici quelques exemples d’enregistrements :</span><span class="sxs-lookup"><span data-stu-id="f2164-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="f2164-115">Le fichier **trip_fare.csv** contient les détails du prix de chaque course, comme le type de paiement, le prix de la course, les suppléments et les taxes, les pourboires et les péages, ainsi que le montant total réglé.</span><span class="sxs-lookup"><span data-stu-id="f2164-115">The **trip_fare.csv** file contains details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="f2164-116">Voici quelques exemples d’enregistrements :</span><span class="sxs-lookup"><span data-stu-id="f2164-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="f2164-117">La **clé unique** utilisée pour joindre trip\_data et trip\_fare se compose des trois champs suivants :</span><span class="sxs-lookup"><span data-stu-id="f2164-117">The **unique key** used to join trip\_data and trip\_fare is composed of the following three fields:</span></span>

* <span data-ttu-id="f2164-118">medallion (médaillon),</span><span class="sxs-lookup"><span data-stu-id="f2164-118">medallion,</span></span>
* <span data-ttu-id="f2164-119">hack\_license (licence de taxi) et</span><span class="sxs-lookup"><span data-stu-id="f2164-119">hack\_license and</span></span>
* <span data-ttu-id="f2164-120">pickup\_datetime (date et heure d’embarquement).</span><span class="sxs-lookup"><span data-stu-id="f2164-120">pickup\_datetime.</span></span>

## <span data-ttu-id="f2164-121"><a name="mltasks"></a>Traiter trois types de tâches de prédiction</span><span class="sxs-lookup"><span data-stu-id="f2164-121"><a name="mltasks"></a>Address three types of prediction tasks</span></span>
<span data-ttu-id="f2164-122">Nous formulons trois problèmes de prédiction reposant sur la valeur *tip\_amount* pour illustrer trois genres de tâches de modélisation :</span><span class="sxs-lookup"><span data-stu-id="f2164-122">We formulate three prediction problems based on the *tip\_amount* to illustrate three kinds of modeling tasks:</span></span>

1. <span data-ttu-id="f2164-123">**Classification binaire** : pour prédire si un pourboire a ou non été versé pour une course ; autrement dit, une valeur *tip\_amount* supérieure à 0 $ constitue un exemple positif, alors qu’une *valeur tip\_amount* de 0 $ est un exemple négatif.</span><span class="sxs-lookup"><span data-stu-id="f2164-123">**Binary classification**: To predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="f2164-124">**Classification multiclasse**: prédire la fourchette des pourboires versés pour une course.</span><span class="sxs-lookup"><span data-stu-id="f2164-124">**Multiclass classification**: To predict the range of tip paid for the trip.</span></span> <span data-ttu-id="f2164-125">Nous divisons la valeur *tip\_amount* en cinq compartiments ou classes :</span><span class="sxs-lookup"><span data-stu-id="f2164-125">We divide the *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="f2164-126">**Tâche de régression**: prédire le montant du pourboire versé pour une course.</span><span class="sxs-lookup"><span data-stu-id="f2164-126">**Regression task**: To predict the amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="f2164-127"><a name="setup"></a>Configurer l’environnement de science des données Azure pour l’analyse avancée</span><span class="sxs-lookup"><span data-stu-id="f2164-127"><a name="setup"></a>Set up the Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="f2164-128">Pour configurer votre environnement de science des données Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f2164-128">To set up your Azure Data Science environment, follow these steps.</span></span>

<span data-ttu-id="f2164-129">**Créez votre propre compte de stockage d’objets blob Azure**</span><span class="sxs-lookup"><span data-stu-id="f2164-129">**Create your own Azure blob storage account**</span></span>

* <span data-ttu-id="f2164-130">Quand vous approvisionnez votre propre espace de stockage d’objets blob Azure, choisissez un emplacement géographique pour celui-ci dans le **Centre-Sud des États-Unis**, ou aussi près que possible de cette région, où sont stockées les données NYC Taxi.</span><span class="sxs-lookup"><span data-stu-id="f2164-130">When you provision your own Azure blob storage, choose a geo-location for your Azure blob storage in or as close as possible to **South Central US**, which is where the NYC Taxi data is stored.</span></span> <span data-ttu-id="f2164-131">Les données sont copiées à l’aide d’AzCopy du conteneur de stockage d’objets blob publics vers un conteneur de votre propre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f2164-131">The data will be copied using AzCopy from the public blob storage container to a container in your own storage account.</span></span> <span data-ttu-id="f2164-132">La rapidité d’exécution de cette tâche (étape 4) est proportionnelle à la proximité de votre espace de stockage d’objets blob Azure avec le Sud du centre des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="f2164-132">The closer your Azure blob storage is to South Central US, the faster this task (Step 4) will be completed.</span></span>
* <span data-ttu-id="f2164-133">Pour créer votre propre compte de stockage Azure, suivez les étapes indiquées dans [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="f2164-133">To create your own Azure storage account, follow the steps outlined at [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="f2164-134">Notez les informations d’identification suivantes du compte de stockage, car vous en aurez besoin ultérieurement dans cette procédure.</span><span class="sxs-lookup"><span data-stu-id="f2164-134">Be sure to make notes on the values for following storage account credentials as they will be needed later in this walkthrough.</span></span>
  
  * <span data-ttu-id="f2164-135">**Nom du compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="f2164-135">**Storage Account Name**</span></span>
  * <span data-ttu-id="f2164-136">**Clé du compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="f2164-136">**Storage Account Key**</span></span>
  * <span data-ttu-id="f2164-137">**Nom du conteneur** (dans lequel vous souhaitez stocker les données dans l’espace de stockage d’objets blob Azure)</span><span class="sxs-lookup"><span data-stu-id="f2164-137">**Container Name** (which you want the data to be stored in the Azure blob storage)</span></span>

<span data-ttu-id="f2164-138">**Approvisionnez votre instance Azure SQL DW.**</span><span class="sxs-lookup"><span data-stu-id="f2164-138">**Provision your Azure SQL DW instance.**</span></span>
<span data-ttu-id="f2164-139">Suivez les étapes indiquées dans [Créer un entrepôt de données SQL](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) pour approvisionner une instance SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f2164-139">Follow the documentation at [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) to provision a SQL Data Warehouse instance.</span></span> <span data-ttu-id="f2164-140">Assurez-vous de prendre note des informations d’identification suivantes de SQL Data Warehouse dont vous aurez besoin dans les étapes ultérieures.</span><span class="sxs-lookup"><span data-stu-id="f2164-140">Make sure that you make notations on the following SQL Data Warehouse credentials which will be used in later steps.</span></span>

* <span data-ttu-id="f2164-141">**Nom du serveur** : <server Name>.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="f2164-141">**Server Name**: <server Name>.database.windows.net</span></span>
* <span data-ttu-id="f2164-142">**Nom SQL DW (base de données)**</span><span class="sxs-lookup"><span data-stu-id="f2164-142">**SQLDW (Database) Name**</span></span>
* <span data-ttu-id="f2164-143">**Nom d’utilisateur**</span><span class="sxs-lookup"><span data-stu-id="f2164-143">**Username**</span></span>
* <span data-ttu-id="f2164-144">**Mot de passe**</span><span class="sxs-lookup"><span data-stu-id="f2164-144">**Password**</span></span>

<span data-ttu-id="f2164-145">**Installez Visual Studio et SQL Server Data Tools.**</span><span class="sxs-lookup"><span data-stu-id="f2164-145">**Install Visual Studio and SQL Server Data Tools.**</span></span> <span data-ttu-id="f2164-146">Pour connaître les instructions à suivre, consultez l’article [Installer Visual Studio 2015 et/ou SSDT pour SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="f2164-146">For instructions, see [Install Visual Studio 2015 and/or SSDT (SQL Server Data Tools) for SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span></span>

<span data-ttu-id="f2164-147">**Connectez-vous à votre Azure SQL DW avec Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="f2164-147">**Connect to your Azure SQL DW with Visual Studio.**</span></span> <span data-ttu-id="f2164-148">Pour connaître les instructions à suivre, consultez les étapes 1 et 2 dans [Se connecter à SQL Data Warehouse avec Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f2164-148">For instructions, see steps 1 & 2 in [Connect to Azure SQL Data Warehouse with Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f2164-149">Exécutez la requête SQL suivante sur la base de données que vous avez créée dans votre SQL Data Warehouse (au lieu de la requête fournie à l’étape 3 de la rubrique connexion) pour **créer une clé principale**.</span><span class="sxs-lookup"><span data-stu-id="f2164-149">Run the following SQL query on the database you created in your SQL Data Warehouse (instead of the query provided in step 3 of the connect topic,) to **create a master key**.</span></span>
> 
> 

    BEGIN TRY
           --Try to create the master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If the master key exists, do nothing
    END CATCH;

<span data-ttu-id="f2164-150">**Créez un espace de travail Azure Machine Learning dans votre abonnement Azure.**</span><span class="sxs-lookup"><span data-stu-id="f2164-150">**Create an Azure Machine Learning workspace under your Azure subscription.**</span></span> <span data-ttu-id="f2164-151">Pour connaître les instructions à suivre, consultez l’article [Création d’un espace de travail Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="f2164-151">For instructions, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

## <span data-ttu-id="f2164-152"><a name="getdata"></a>Charger les données dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f2164-152"><a name="getdata"></a>Load the data into SQL Data Warehouse</span></span>
<span data-ttu-id="f2164-153">Ouvrez une console de commandes Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2164-153">Open a Windows PowerShell command console.</span></span> <span data-ttu-id="f2164-154">Exécutez les commandes PowerShell suivantes pour télécharger les fichiers d’exemple de script SQL que nous partageons avec vous sur GitHub dans un répertoire local que vous spécifiez avec le paramètre *-DestDir*.</span><span class="sxs-lookup"><span data-stu-id="f2164-154">Run the following PowerShell commands to download the example SQL script files that we share with you on GitHub to a local directory that you specify with the parameter *-DestDir*.</span></span> <span data-ttu-id="f2164-155">Vous pouvez remplacer la valeur du paramètre *-DestDir* par un répertoire local.</span><span class="sxs-lookup"><span data-stu-id="f2164-155">You can change the value of parameter *-DestDir* to any local directory.</span></span> <span data-ttu-id="f2164-156">Si *-DestDir* n’existe pas, il est créé par le script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2164-156">If *-DestDir* does not exist, it will be created by the PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="f2164-157">Vous devrez peut-être sélectionner **Exécuter en tant qu’administrateur** au moment de l’exécution du script PowerShell suivant si le privilège Administrateur est nécessaire pour créer le répertoire *DestDir* ou pour y écrire.</span><span class="sxs-lookup"><span data-stu-id="f2164-157">You might need to **Run as Administrator** when executing the following PowerShell script if your *DestDir* directory needs Administrator privilege to create or to write to it.</span></span>
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

<span data-ttu-id="f2164-158">Une fois le script exécuté, *-DestDir*devient votre répertoire de travail.</span><span class="sxs-lookup"><span data-stu-id="f2164-158">After successful execution, your current working directory changes to *-DestDir*.</span></span> <span data-ttu-id="f2164-159">Vous devez voir un écran semblable à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="f2164-159">You should be able to see screen like below:</span></span>

![][19]

<span data-ttu-id="f2164-160">Dans *-DestDir*, exécutez le script PowerShell suivant en mode administrateur :</span><span class="sxs-lookup"><span data-stu-id="f2164-160">In your *-DestDir*, execute the following PowerShell script in administrator mode:</span></span>

    ./SQLDW_Data_Import.ps1

<span data-ttu-id="f2164-161">Lorsque le script PowerShell s’exécute pour la première fois, vous devez entrer les informations de votre Azure SQL DW et de votre compte de stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="f2164-161">When the PowerShell script runs for the first time, you will be asked to input the information from your Azure SQL DW and your Azure blob storage account.</span></span> <span data-ttu-id="f2164-162">À l’issue de la première exécution de ce script PowerShell, les informations d’identification que vous avez entrées sont écrites dans le fichier de configuration SQLDW.conf dans le répertoire de travail actuel.</span><span class="sxs-lookup"><span data-stu-id="f2164-162">When this PowerShell script completes running for the first time, the credentials you input will have been written to a configuration file SQLDW.conf in the present working directory.</span></span> <span data-ttu-id="f2164-163">L’exécution suivante de ce fichier de script PowerShell permet de lire tous les paramètres nécessaires de ce fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="f2164-163">The future run of this PowerShell script file has the option to read all needed parameters from this configuration file.</span></span> <span data-ttu-id="f2164-164">Si vous devez en modifier certains, vous pouvez choisir d’entrer les paramètres dans l’écran dès l’invite en supprimant ce fichier de configuration et en entrant les valeurs des paramètres comme demandé ou vous pouvez décider de changer ces valeurs en modifiant le fichier SQLDW.conf dans votre répertoire *-DestDir* .</span><span class="sxs-lookup"><span data-stu-id="f2164-164">If you need to change some parameters, you can choose to input the parameters on the screen upon prompt by deleting this configuration file and inputting the parameters values as prompted or to change the parameter values by editing the SQLDW.conf file in your *-DestDir* directory.</span></span>

> [!NOTE]
> <span data-ttu-id="f2164-165">Pour éviter des conflits de noms de schéma avec ceux qui existent déjà dans votre Azure SQL DW, au moment de la lecture directe des paramètres du fichier SQLDW.conf, un nombre aléatoire à 3 chiffres est ajouté au nom du schéma du fichier SQLDW.conf comme nom de schéma par défaut pour chaque exécution.</span><span class="sxs-lookup"><span data-stu-id="f2164-165">In order to avoid schema name conflicts with those that already exist in your Azure SQL DW, when reading parameters directly from the SQLDW.conf file, a 3-digit random number is added to the schema name from the SQLDW.conf file as the default schema name for each run.</span></span> <span data-ttu-id="f2164-166">Le script PowerShell peut vous demander un nom de schéma : le nom peut être spécifié à la discrétion de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f2164-166">The PowerShell script may prompt you for a schema name: the name may be specified at user discretion.</span></span>
> 
> 

<span data-ttu-id="f2164-167">Ce fichier de **script PowerShell** exécute les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="f2164-167">This **PowerShell script** file completes the following tasks:</span></span>

* <span data-ttu-id="f2164-168">**Télécharge et installe AzCopy**, si AzCopy n’est pas déjà installé.</span><span class="sxs-lookup"><span data-stu-id="f2164-168">**Downloads and installs AzCopy**, if AzCopy is not already installed</span></span>
  
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
* <span data-ttu-id="f2164-169">**Copie des données vers votre compte de stockage privé d’objets blob** depuis l’espace de stockage public d’objets blob avec AzCopy.</span><span class="sxs-lookup"><span data-stu-id="f2164-169">**Copies data to your private blob storage account** from the public blob with AzCopy</span></span>
  
        Write-Host "AzCopy is copying data from public blob to yo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account to verify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob to your storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* <span data-ttu-id="f2164-170">**Charge les données à l’aide de Polybase (en exécutant LoadDataToSQLDW.sql) dans votre Azure SQL DW** à partir de votre compte de stockage privé d’objets blob avec les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="f2164-170">**Loads data using Polybase (by executing LoadDataToSQLDW.sql) to your Azure SQL DW** from your private blob storage account with the following commands.</span></span>
  
  * <span data-ttu-id="f2164-171">Créer un schéma</span><span class="sxs-lookup"><span data-stu-id="f2164-171">Create a schema</span></span>
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * <span data-ttu-id="f2164-172">Créer un fichier d’informations d’identification de niveau base de données</span><span class="sxs-lookup"><span data-stu-id="f2164-172">Create a database scoped credential</span></span>
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * <span data-ttu-id="f2164-173">Créer une source de données externe pour un objet blob de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="f2164-173">Create an external data source for an Azure storage blob</span></span>
    
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
  * <span data-ttu-id="f2164-174">Créer un format de fichier externe pour un fichier csv.</span><span class="sxs-lookup"><span data-stu-id="f2164-174">Create an external file format for a csv file.</span></span> <span data-ttu-id="f2164-175">Les données ne sont pas compressées et les champs sont séparés par le caractère barre verticale.</span><span class="sxs-lookup"><span data-stu-id="f2164-175">Data is uncompressed and fields are separated with the pipe character.</span></span>
    
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
  * <span data-ttu-id="f2164-176">Créer des tables externes pour les prix et les courses correspondant au jeu de données NYC Taxi dans le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="f2164-176">Create external fare and trip tables for NYC taxi dataset in Azure blob storage.</span></span>
    
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

    - <span data-ttu-id="f2164-177">Charger les données à partir des tables externes du stockage d’objets blob Azure dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f2164-177">Load data from external tables in Azure blob storage to SQL Data Warehouse</span></span>

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

    - <span data-ttu-id="f2164-178">Crée un exemple de table de données (NYCTaxi_Sample) et y insère des données résultant de la sélection de requêtes SQL dans les tables des courses et des prix.</span><span class="sxs-lookup"><span data-stu-id="f2164-178">Create a sample data table (NYCTaxi_Sample) and insert data to it from selecting SQL queries on the trip and fare tables.</span></span> <span data-ttu-id="f2164-179">(Certaines étapes de cette procédure nécessitent l’utilisation de cette table d’exemple.)</span><span class="sxs-lookup"><span data-stu-id="f2164-179">(Some steps of this walkthrough needs to use this sample table.)</span></span>

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

<span data-ttu-id="f2164-180">L’emplacement géographique de vos comptes de stockage a une incidence sur les délais de chargement.</span><span class="sxs-lookup"><span data-stu-id="f2164-180">The geographic location of your storage accounts affects load times.</span></span>

> [!NOTE]
> <span data-ttu-id="f2164-181">Selon l’emplacement géographique de votre compte de stockage privé d’objets blob, le processus de copie des données d’un objet blob public vers votre compte de stockage privé peut prendre environ 15 minutes, voire plus, tandis que le processus de chargement des données de votre compte de stockage vers votre Azure SQL DW peut prendre 20 minutes ou plus.</span><span class="sxs-lookup"><span data-stu-id="f2164-181">Depending on the geographical location of your private blob storage account, the process of copying data from a public blob to your private storage account can take about 15 minutes, or even longer,and the process of loading data from your storage account to your Azure SQL DW could take 20 minutes or longer.</span></span>  
> 
> 

<span data-ttu-id="f2164-182">Vous devez décider ce que vous souhaitez faire si vous avez des fichiers source et de destination en double.</span><span class="sxs-lookup"><span data-stu-id="f2164-182">You will have to decide what do if you have duplicate source and destination files.</span></span>

> [!NOTE]
> <span data-ttu-id="f2164-183">Si les fichiers .csv à copier de l’espace de stockage public d’objets blob vers votre compte de stockage privé d’objets blob existent déjà dans ce dernier, AzCopy vous demande si vous souhaitez les remplacer.</span><span class="sxs-lookup"><span data-stu-id="f2164-183">If the .csv files to be copied from the public blob storage to your private blob storage account already exist in your private blob storage account, AzCopy will ask you whether you want to overwrite them.</span></span> <span data-ttu-id="f2164-184">Si vous ne le souhaitez pas, entrez **n** à l’invite.</span><span class="sxs-lookup"><span data-stu-id="f2164-184">If you do not want to overwrite them, input **n** when prompted.</span></span> <span data-ttu-id="f2164-185">Si vous souhaitez les remplacer **tous**, entrez **a** à l’invite.</span><span class="sxs-lookup"><span data-stu-id="f2164-185">If you want to overwrite **all** of them, input **a** when prompted.</span></span> <span data-ttu-id="f2164-186">Vous pouvez également entrer **y** pour remplacer les fichiers .csv un par un.</span><span class="sxs-lookup"><span data-stu-id="f2164-186">You can also input **y** to overwrite .csv files individually.</span></span>
> 
> 

![Diagramme n°21][21]

<span data-ttu-id="f2164-188">Vous pouvez utiliser vos propres données.</span><span class="sxs-lookup"><span data-stu-id="f2164-188">You can use your own data.</span></span> <span data-ttu-id="f2164-189">Si vos données sont stockées sur votre ordinateur sur site dans votre application réelle, vous pouvez toujours utiliser AzCopy pour charger les données locales vers l’espace de stockage privé d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="f2164-189">If your data is in your on-premises machine in your real life application, you can still use AzCopy to upload on-premises data to your private Azure blob storage.</span></span> <span data-ttu-id="f2164-190">Vous devez uniquement modifier l’emplacement **Source**, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, dans la commande AzCopy du fichier de script PowerShell et le remplacer par le répertoire local qui contient vos données.</span><span class="sxs-lookup"><span data-stu-id="f2164-190">You only need to change the **Source** location, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in the AzCopy command of the PowerShell script file to the local directory that contains your data.</span></span>

> [!TIP]
> <span data-ttu-id="f2164-191">Si vos données figurent déjà dans votre espace de stockage privé d’objets blob Azure de votre application réelle, vous pouvez ignorer l’étape AzCopy dans le script PowerShell et charger directement les données vers Azure SQL DW.</span><span class="sxs-lookup"><span data-stu-id="f2164-191">If your data is already in your private Azure blob storage in your real life application, you can skip the AzCopy step in the PowerShell script and directly upload the data to Azure SQL DW.</span></span> <span data-ttu-id="f2164-192">Pour effectuer cette opération, vous devez modifier le script afin de l’adapter au format de vos données.</span><span class="sxs-lookup"><span data-stu-id="f2164-192">This will require additional edits of the script to tailor it to the format of your data.</span></span>
> 
> 

<span data-ttu-id="f2164-193">Ce script Powershell relie également les informations d’Azure SQL DW aux fichiers d’exemple d’exploration de données SQLDW_Explorations.sql, SQLDW_Explorations.ipynb et SQLDW_Explorations_Scripts.py afin que ces trois fichiers soient prêts à être essayés dès la fin de l’exécution du script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2164-193">This Powershell script also plugs in the Azure SQL DW information into the data exploration example files SQLDW_Explorations.sql, SQLDW_Explorations.ipynb, and SQLDW_Explorations_Scripts.py so that these three files are ready to be tried out instantly after the PowerShell script completes.</span></span>

<span data-ttu-id="f2164-194">À l’issue d’une exécution réussie, un écran semblable à ce qui suit s’affiche :</span><span class="sxs-lookup"><span data-stu-id="f2164-194">After a successful execution, you will see screen like below:</span></span>

![][20]

## <span data-ttu-id="f2164-195"><a name="dbexplore"></a>Exploration des données et conception de fonctionnalités dans Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f2164-195"><a name="dbexplore"></a>Data exploration and feature engineering in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="f2164-196">Dans cette section, nous effectuons une exploration des données et une génération de caractéristiques en exécutant des requêtes SQL directement dans Azure SQL DW à l’aide de **Visual Studio Data Tools**.</span><span class="sxs-lookup"><span data-stu-id="f2164-196">In this section, we perform data exploration and feature generation by running SQL queries against Azure SQL DW directly using **Visual Studio Data Tools**.</span></span> <span data-ttu-id="f2164-197">Toutes les requêtes SQL utilisées dans cette section se trouvent dans l’exemple de script nommé *SQLDW_Explorations.sql*.</span><span class="sxs-lookup"><span data-stu-id="f2164-197">All SQL queries used in this section can be found in the sample script named *SQLDW_Explorations.sql*.</span></span> <span data-ttu-id="f2164-198">Ce fichier a déjà été téléchargé dans votre répertoire local par le script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2164-198">This file has already been downloaded to your local directory by the PowerShell script.</span></span> <span data-ttu-id="f2164-199">Vous pouvez également le récupérer à partir de [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql),</span><span class="sxs-lookup"><span data-stu-id="f2164-199">You can also retrieve it from [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span></span> <span data-ttu-id="f2164-200">mais les informations d’Azure SQL DW ne sont pas reliées à ce fichier situé dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="f2164-200">But the file in GitHub does not have the Azure SQL DW information plugged in.</span></span>

<span data-ttu-id="f2164-201">Connectez-vous à votre Azure SQL DW en utilisant Visual Studio avec le nom et le mot de passe de connexion de SQL DW et ouvrez l’ **Explorateur d’objets SQL** pour vérifier que la base de données et les tables ont été importées.</span><span class="sxs-lookup"><span data-stu-id="f2164-201">Connect to your Azure SQL DW using Visual Studio with the SQL DW login name and password and open up the **SQL Object Explorer** to confirm the database and tables have been imported.</span></span> <span data-ttu-id="f2164-202">Récupérez le fichier *SQLDW_Explorations.sql*.</span><span class="sxs-lookup"><span data-stu-id="f2164-202">Retrieve the *SQLDW_Explorations.sql* file.</span></span>

> [!NOTE]
> <span data-ttu-id="f2164-203">Pour ouvrir un éditeur de requête Parallel Data Warehouse (PDW), utilisez la commande **Nouvelle requête** pendant que votre PDW est sélectionné dans **l’Explorateur d’objets SQL**.</span><span class="sxs-lookup"><span data-stu-id="f2164-203">To open a Parallel Data Warehouse (PDW) query editor, use the **New Query** command while your PDW is selected in the **SQL Object Explorer**.</span></span> <span data-ttu-id="f2164-204">L’éditeur de requête SQL standard n’est pas pris en charge par PDW.</span><span class="sxs-lookup"><span data-stu-id="f2164-204">The standard SQL query editor is not supported by PDW.</span></span>
> 
> 

<span data-ttu-id="f2164-205">Voici les types de tâche d’exploration des données et de génération de fonctionnalités qui sont effectués dans cette section :</span><span class="sxs-lookup"><span data-stu-id="f2164-205">Here are the type of data exploration and feature generation tasks performed in this section:</span></span>

* <span data-ttu-id="f2164-206">Explorer les distributions de données de quelques champs portant sur différentes périodes.</span><span class="sxs-lookup"><span data-stu-id="f2164-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="f2164-207">examiner la qualité des données des champs de longitude et de latitude ;</span><span class="sxs-lookup"><span data-stu-id="f2164-207">Investigate data quality of the longitude and latitude fields.</span></span>
* <span data-ttu-id="f2164-208">Générer des étiquettes de classification binaire et multiclasse reposant sur la valeur **tip\_amount**.</span><span class="sxs-lookup"><span data-stu-id="f2164-208">Generate binary and multiclass classification labels based on the **tip\_amount**.</span></span>
* <span data-ttu-id="f2164-209">Générer des fonctionnalités et calculer/comparer les distances des trajets.</span><span class="sxs-lookup"><span data-stu-id="f2164-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="f2164-210">Joindre les deux tables et extraire un échantillon aléatoire que nous utiliserons pour créer les modèles.</span><span class="sxs-lookup"><span data-stu-id="f2164-210">Join the two tables and extract a random sample that will be used to build models.</span></span>

### <a name="data-import-verification"></a><span data-ttu-id="f2164-211">Vérification de l’importation des données</span><span class="sxs-lookup"><span data-stu-id="f2164-211">Data import verification</span></span>
<span data-ttu-id="f2164-212">Les requêtes ci-après procèdent à une vérification rapide du nombre de lignes et de colonnes des tables précédemment remplies à l’aide des importations en bloc en parallèle de Polybase.</span><span class="sxs-lookup"><span data-stu-id="f2164-212">These queries provide a quick verification of the number of rows and columns in the tables populated earlier using Polybase's parallel bulk import,</span></span>

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

<span data-ttu-id="f2164-213">**Sortie :** vous devez obtenir 173 179 759 lignes et 14 colonnes.</span><span class="sxs-lookup"><span data-stu-id="f2164-213">**Output:** You should get 173,179,759 rows and 14 columns.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="f2164-214">Exploration : distribution des courses par médaillon</span><span class="sxs-lookup"><span data-stu-id="f2164-214">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="f2164-215">Cet exemple de requête identifie les médaillons (numéros de taxi) qui ont effectué plus de 100 courses au cours d’une période spécifiée.</span><span class="sxs-lookup"><span data-stu-id="f2164-215">This example query identifies the medallions (taxi numbers) that completed more than 100 trips within a specified time period.</span></span> <span data-ttu-id="f2164-216">Cette requête tire avantage de l’accès aux tables partitionnées, car elle est conditionnée par le schéma de partition de **pickup\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="f2164-216">The query would benefit from the partitioned table access since it is conditioned by the partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="f2164-217">L’exécution d’une requête portant sur le jeu de données complet tire également profit de l’analyse d’index et/ou de table partitionnée.</span><span class="sxs-lookup"><span data-stu-id="f2164-217">Querying the full dataset will also make use of the partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

<span data-ttu-id="f2164-218">**Sortie :** la requête doit retourner une table dont les lignes recensent les 13 369 médaillons (taxis) et le nombre correspondant de courses effectuées en 2013.</span><span class="sxs-lookup"><span data-stu-id="f2164-218">**Output:** The query should return a table with rows specifying the 13,369 medallions (taxis) and the number of trip completed by them in 2013.</span></span> <span data-ttu-id="f2164-219">La dernière colonne contient le nombre de courses effectuées.</span><span class="sxs-lookup"><span data-stu-id="f2164-219">The last column contains the count of the number of trips completed.</span></span>

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="f2164-220">Exploration : distribution des courses par médaillon et par licence de taxi</span><span class="sxs-lookup"><span data-stu-id="f2164-220">Exploration: Trip distribution by medallion and hack_license</span></span>
<span data-ttu-id="f2164-221">Cet exemple identifie les médaillons (numéros de taxi) et les numéros hack_license (chauffeurs) qui ont effectué plus de 100 courses au cours d’une période spécifiée.</span><span class="sxs-lookup"><span data-stu-id="f2164-221">This example identifies the medallions (taxi numbers) and hack_license numbers (drivers) that completed more than 100 trips within a specified time period.</span></span>

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

<span data-ttu-id="f2164-222">**Sortie :** la requête doit retourner une table de 13 369 lignes recensant les 13 369 ID de voiture/chauffeur qui ont effectué plus de 100 courses en 2013.</span><span class="sxs-lookup"><span data-stu-id="f2164-222">**Output:** The query should return a table with 13,369 rows specifying the 13,369 car/driver IDs that have completed more that 100 trips in 2013.</span></span> <span data-ttu-id="f2164-223">La dernière colonne contient le nombre de courses effectuées.</span><span class="sxs-lookup"><span data-stu-id="f2164-223">The last column contains the count of the number of trips completed.</span></span>

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="f2164-224">Évaluation de la qualité des données : Vérifier les enregistrements indiquant une longitude et/ou une latitude incorrectes</span><span class="sxs-lookup"><span data-stu-id="f2164-224">Data quality assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="f2164-225">Cet exemple vérifie si l’un des champs de longitude et/ou de latitude contient une valeur incorrecte (le nombre de degrés doit être compris entre -90 et 90) ou présente des coordonnées (0, 0).</span><span class="sxs-lookup"><span data-stu-id="f2164-225">This example investigates if any of the longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

<span data-ttu-id="f2164-226">**Sortie :** la requête retourne 837 467 courses dont les champs de longitude et/ou de latitude ne sont pas valides.</span><span class="sxs-lookup"><span data-stu-id="f2164-226">**Output:** The query returns 837,467 trips that have invalid longitude and/or latitude fields.</span></span>

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="f2164-227">Exploration : Distribution des courses avec et sans pourboire</span><span class="sxs-lookup"><span data-stu-id="f2164-227">Exploration: Tipped vs. not tipped trips distribution</span></span>
<span data-ttu-id="f2164-228">Cet exemple détermine le nombre de courses qui ont fait l’objet d’un pourboire et celles qui n’ont pas donné lieu à un pourboire pendant une période spécifiée (ou dans le jeu de données complet si la période couvre l’année complète comme dans le cas présent).</span><span class="sxs-lookup"><span data-stu-id="f2164-228">This example finds the number of trips that were tipped vs. the number that were not tipped in a specified time period (or in the full dataset if covering the full year as it is set up here).</span></span> <span data-ttu-id="f2164-229">Cette distribution reflète la distribution des étiquettes binaires à utiliser par la suite pour la modélisation de classification binaire.</span><span class="sxs-lookup"><span data-stu-id="f2164-229">This distribution reflects the binary label distribution to be later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

<span data-ttu-id="f2164-230">**Sortie :** la requête doit retourner la distribution des courses avec et sans pourboire pour l’année 2013 suivante : 90 447 622 avec pourboire et 82 264 709 sans pourboire.</span><span class="sxs-lookup"><span data-stu-id="f2164-230">**Output:** The query should return the following tip frequencies for the year 2013: 90,447,622 tipped and 82,264,709 not-tipped.</span></span>

### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="f2164-231">Exploration : Distribution des classes/fourchettes de pourboires</span><span class="sxs-lookup"><span data-stu-id="f2164-231">Exploration: Tip class/range distribution</span></span>
<span data-ttu-id="f2164-232">Cet exemple calcule la distribution des fourchettes de pourboires sur une période donnée (ou dans le jeu de données complet si la requête porte sur l’année entière).</span><span class="sxs-lookup"><span data-stu-id="f2164-232">This example computes the distribution of tip ranges in a given time period (or in the full dataset if covering the full year).</span></span> <span data-ttu-id="f2164-233">Il s’agit de la distribution des classes d’étiquette à utiliser par la suite pour la modélisation de classification multiclasse.</span><span class="sxs-lookup"><span data-stu-id="f2164-233">This is the distribution of the label classes that will be used later for multiclass classification modeling.</span></span>

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

<span data-ttu-id="f2164-234">**Output:**</span><span class="sxs-lookup"><span data-stu-id="f2164-234">**Output:**</span></span>

| <span data-ttu-id="f2164-235">tip_class</span><span class="sxs-lookup"><span data-stu-id="f2164-235">tip_class</span></span> | <span data-ttu-id="f2164-236">tip_freq</span><span class="sxs-lookup"><span data-stu-id="f2164-236">tip_freq</span></span> |
| --- | --- |
| <span data-ttu-id="f2164-237">1</span><span class="sxs-lookup"><span data-stu-id="f2164-237">1</span></span> |<span data-ttu-id="f2164-238">82230915</span><span class="sxs-lookup"><span data-stu-id="f2164-238">82230915</span></span> |
| <span data-ttu-id="f2164-239">2</span><span class="sxs-lookup"><span data-stu-id="f2164-239">2</span></span> |<span data-ttu-id="f2164-240">6198803</span><span class="sxs-lookup"><span data-stu-id="f2164-240">6198803</span></span> |
| <span data-ttu-id="f2164-241">3</span><span class="sxs-lookup"><span data-stu-id="f2164-241">3</span></span> |<span data-ttu-id="f2164-242">1932223</span><span class="sxs-lookup"><span data-stu-id="f2164-242">1932223</span></span> |
| <span data-ttu-id="f2164-243">0</span><span class="sxs-lookup"><span data-stu-id="f2164-243">0</span></span> |<span data-ttu-id="f2164-244">82264625</span><span class="sxs-lookup"><span data-stu-id="f2164-244">82264625</span></span> |
| <span data-ttu-id="f2164-245">4</span><span class="sxs-lookup"><span data-stu-id="f2164-245">4</span></span> |<span data-ttu-id="f2164-246">85765</span><span class="sxs-lookup"><span data-stu-id="f2164-246">85765</span></span> |

### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="f2164-247">Exploration : Calculer et comparer les distances des courses</span><span class="sxs-lookup"><span data-stu-id="f2164-247">Exploration: Compute and compare trip distance</span></span>
<span data-ttu-id="f2164-248">Cet exemple convertit la longitude et la latitude des points d’embarquement et de débarquement en points géographiques SQL, calcule la distance des trajets en se basant sur la différence entre ces points géographiques et renvoie un échantillon aléatoire des résultats pour comparaison.</span><span class="sxs-lookup"><span data-stu-id="f2164-248">This example converts the pickup and drop-off longitude and latitude to SQL geography points, computes the trip distance using SQL geography points difference, and returns a random sample of the results for comparison.</span></span> <span data-ttu-id="f2164-249">Cet exemple limite les résultats aux coordonnées valides en utilisant la requête d’évaluation de la qualité des données précédemment décrite.</span><span class="sxs-lookup"><span data-stu-id="f2164-249">The example limits the results to valid coordinates only using the data quality assessment query covered earlier.</span></span>

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function to calculate the direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert to radians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert to miles
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

### <a name="feature-engineering-using-sql-functions"></a><span data-ttu-id="f2164-250">Conception de fonctionnalités à l’aide de fonctions SQL</span><span class="sxs-lookup"><span data-stu-id="f2164-250">Feature engineering using SQL functions</span></span>
<span data-ttu-id="f2164-251">Les fonctions SQL peuvent parfois s’avérer efficaces pour la conception des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="f2164-251">Sometimes SQL functions can be an efficient option for feature engineering.</span></span> <span data-ttu-id="f2164-252">Dans cette procédure, nous avons défini une fonction SQL pour calculer la distance directe séparant les lieux d’embarquement et de débarquement.</span><span class="sxs-lookup"><span data-stu-id="f2164-252">In this walkthrough, we defined a SQL function to calculate the direct distance between the pickup and dropoff locations.</span></span> <span data-ttu-id="f2164-253">Vous pouvez exécuter les scripts SQL ci-dessous dans **Visual Studio Data Tools**.</span><span class="sxs-lookup"><span data-stu-id="f2164-253">You can run the following SQL scripts in **Visual Studio Data Tools**.</span></span>

<span data-ttu-id="f2164-254">Voici le script SQL qui définit la fonction de distance.</span><span class="sxs-lookup"><span data-stu-id="f2164-254">Here is the SQL script that defines the distance function.</span></span>

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate the direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert to radians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert to miles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

<span data-ttu-id="f2164-255">Voici un exemple d’appel de cette fonction pour générer des fonctionnalités dans votre requête SQL :</span><span class="sxs-lookup"><span data-stu-id="f2164-255">Here is an example to call this function to generate features in your SQL query:</span></span>

    -- Sample query to call the function to create features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="f2164-256">**Sortie :** cette requête génère une table (de 2 803 538 lignes) indiquant les latitudes et longitudes des points de prise en charge et de dépose, ainsi que les distances directes correspondantes en miles.</span><span class="sxs-lookup"><span data-stu-id="f2164-256">**Output:** This query generates a table (with 2,803,538 rows) with pickup and dropoff latitudes and longitudes and the corresponding direct distances in miles.</span></span> <span data-ttu-id="f2164-257">Voici les résultats pour les 3 premières lignes :</span><span class="sxs-lookup"><span data-stu-id="f2164-257">Here are the results for first 3 rows:</span></span>

|  | <span data-ttu-id="f2164-258">pickup_latitude</span><span class="sxs-lookup"><span data-stu-id="f2164-258">pickup_latitude</span></span> | <span data-ttu-id="f2164-259">pickup_longitude</span><span class="sxs-lookup"><span data-stu-id="f2164-259">pickup_longitude</span></span> | <span data-ttu-id="f2164-260">dropoff_latitude</span><span class="sxs-lookup"><span data-stu-id="f2164-260">dropoff_latitude</span></span> | <span data-ttu-id="f2164-261">dropoff_longitude</span><span class="sxs-lookup"><span data-stu-id="f2164-261">dropoff_longitude</span></span> | <span data-ttu-id="f2164-262">DirectDistance</span><span class="sxs-lookup"><span data-stu-id="f2164-262">DirectDistance</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="f2164-263">1</span><span class="sxs-lookup"><span data-stu-id="f2164-263">1</span></span> |<span data-ttu-id="f2164-264">40,731804</span><span class="sxs-lookup"><span data-stu-id="f2164-264">40.731804</span></span> |<span data-ttu-id="f2164-265">-74,001083</span><span class="sxs-lookup"><span data-stu-id="f2164-265">-74.001083</span></span> |<span data-ttu-id="f2164-266">40,736622</span><span class="sxs-lookup"><span data-stu-id="f2164-266">40.736622</span></span> |<span data-ttu-id="f2164-267">-73,988953</span><span class="sxs-lookup"><span data-stu-id="f2164-267">-73.988953</span></span> |<span data-ttu-id="f2164-268">0,7169601222</span><span class="sxs-lookup"><span data-stu-id="f2164-268">.7169601222</span></span> |
| <span data-ttu-id="f2164-269">2</span><span class="sxs-lookup"><span data-stu-id="f2164-269">2</span></span> |<span data-ttu-id="f2164-270">40,715794</span><span class="sxs-lookup"><span data-stu-id="f2164-270">40.715794</span></span> |<span data-ttu-id="f2164-271">-74,010635</span><span class="sxs-lookup"><span data-stu-id="f2164-271">-74,010635</span></span> |<span data-ttu-id="f2164-272">40,725338</span><span class="sxs-lookup"><span data-stu-id="f2164-272">40.725338</span></span> |<span data-ttu-id="f2164-273">-74,00399</span><span class="sxs-lookup"><span data-stu-id="f2164-273">-74.00399</span></span> |<span data-ttu-id="f2164-274">0,7448343721</span><span class="sxs-lookup"><span data-stu-id="f2164-274">.7448343721</span></span> |
| <span data-ttu-id="f2164-275">3</span><span class="sxs-lookup"><span data-stu-id="f2164-275">3</span></span> |<span data-ttu-id="f2164-276">40.761456</span><span class="sxs-lookup"><span data-stu-id="f2164-276">40.761456</span></span> |<span data-ttu-id="f2164-277">-73.999886</span><span class="sxs-lookup"><span data-stu-id="f2164-277">-73.999886</span></span> |<span data-ttu-id="f2164-278">40.766544</span><span class="sxs-lookup"><span data-stu-id="f2164-278">40.766544</span></span> |<span data-ttu-id="f2164-279">-73.988228</span><span class="sxs-lookup"><span data-stu-id="f2164-279">-73.988228</span></span> |<span data-ttu-id="f2164-280">0,7037227967</span><span class="sxs-lookup"><span data-stu-id="f2164-280">0.7037227967</span></span> |

### <a name="prepare-data-for-model-building"></a><span data-ttu-id="f2164-281">Préparer les données pour la création de modèles</span><span class="sxs-lookup"><span data-stu-id="f2164-281">Prepare data for model building</span></span>
<span data-ttu-id="f2164-282">La requête ci-après joint les tables **nyctaxi\_trip** et **nyctaxi\_fare**, génère une étiquette de classification binaire **tipped** et une étiquette de classification multiclasse **tip\_class**, puis extrait un échantillon des données de l’intégralité du jeu de données joint.</span><span class="sxs-lookup"><span data-stu-id="f2164-282">The following query joins the **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a sample from the full joined dataset.</span></span> <span data-ttu-id="f2164-283">L’échantillonnage est effectué en récupérant un sous-ensemble des courses basé sur l’heure d’embarquement.</span><span class="sxs-lookup"><span data-stu-id="f2164-283">The sampling is done by retrieving a subset of the trips based on pickup time.</span></span>  <span data-ttu-id="f2164-284">Vous pouvez ensuite copier cette requête et la coller directement dans le module [Importer les données][import-data] d’[Azure Machine Learning Studio](https://studio.azureml.net) pour permettre la réception directe de données de l’instance de base de données SQL dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f2164-284">This query can be copied then pasted directly in the [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from the SQL database instance in Azure.</span></span> <span data-ttu-id="f2164-285">La requête exclut les enregistrements qui présentent des coordonnées (0, 0) incorrectes.</span><span class="sxs-lookup"><span data-stu-id="f2164-285">The query excludes records with incorrect (0, 0) coordinates.</span></span>

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

<span data-ttu-id="f2164-286">Lorsque vous êtes prêt à utiliser Azure Machine Learning, vous pouvez au choix :</span><span class="sxs-lookup"><span data-stu-id="f2164-286">When you are ready to proceed to Azure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="f2164-287">enregistrer la requête SQL finale d’extraction et d’échantillonnage des données et copier-coller cette requête directement dans un module [Importer les données][import-data] d’Azure Machine Learning, ou</span><span class="sxs-lookup"><span data-stu-id="f2164-287">Save the final SQL query to extract and sample the data and copy-paste the query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="f2164-288">stocker les données échantillonnées et générées que vous envisagez d’utiliser pour la création de modèles dans une nouvelle table SQL DW et utiliser cette table dans le module [Importer les données][import-data] d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f2164-288">Persist the sampled and engineered data you plan to use for model building in a new SQL DW table and use the new table in the [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="f2164-289">Le script PowerShell de l’étape précédente a effectué cette opération pour vous.</span><span class="sxs-lookup"><span data-stu-id="f2164-289">The PowerShell script in earlier step has done this for you.</span></span> <span data-ttu-id="f2164-290">Vous pouvez lire directement cette table dans le module Importer les données.</span><span class="sxs-lookup"><span data-stu-id="f2164-290">You can read directly from this table in the Import Data module.</span></span>

## <span data-ttu-id="f2164-291"><a name="ipnb"></a>Exploration des données et conception de fonctionnalités dans IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="f2164-291"><a name="ipnb"></a>Data exploration and feature engineering in IPython notebook</span></span>
<span data-ttu-id="f2164-292">Dans cette section, nous allons effectuer des tâches d’exploration des données et de génération de fonctionnalités en exécutant des requêtes Python et SQL dans le SQL DW créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="f2164-292">In this section, we will perform data exploration and feature generation using both Python and SQL queries against the SQL DW created earlier.</span></span> <span data-ttu-id="f2164-293">Un exemple d’IPython Notebook nommé **SQLDW_Explorations.ipynb** et le fichier de script Python **SQLDW_Explorations_Scripts.py** ont été téléchargés dans votre répertoire local.</span><span class="sxs-lookup"><span data-stu-id="f2164-293">A sample IPython notebook named **SQLDW_Explorations.ipynb** and a Python script file **SQLDW_Explorations_Scripts.py** have been downloaded to your local directory.</span></span> <span data-ttu-id="f2164-294">Ils sont également disponibles sur [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span><span class="sxs-lookup"><span data-stu-id="f2164-294">They are also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span></span> <span data-ttu-id="f2164-295">Ces deux fichiers sont identiques dans les scripts Python.</span><span class="sxs-lookup"><span data-stu-id="f2164-295">These two files are identical in Python scripts.</span></span> <span data-ttu-id="f2164-296">Le fichier de script Python vous est fourni dans le cas où vous ne disposeriez pas d’un serveur IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="f2164-296">The Python script file is provided to you in case you do not have an IPython Notebook server.</span></span> <span data-ttu-id="f2164-297">Ces deux exemples de fichier Python sont conçus sous **Python 2.7**.</span><span class="sxs-lookup"><span data-stu-id="f2164-297">These two sample Python files are designed under **Python 2.7**.</span></span>

<span data-ttu-id="f2164-298">Les informations d’Azure SQL DW nécessaires dans l’exemple de IPython Notebook et dans le fichier de script Python téléchargés sur votre ordinateur local ont été reliées précédemment par le script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2164-298">The needed Azure SQL DW information in the sample IPython Notebook and the Python script file downloaded to your local machine has been plugged in by the PowerShell script previously.</span></span> <span data-ttu-id="f2164-299">Elles peuvent être exécutées sans aucune modification.</span><span class="sxs-lookup"><span data-stu-id="f2164-299">They are executable without any modification.</span></span>

<span data-ttu-id="f2164-300">Si vous avez déjà configuré un espace de travail AzureML, vous pouvez directement charger l’exemple de IPython Notebook vers le service AzureML IPython Notebook et commencer à l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="f2164-300">If you have already set up an AzureML workspace, you can directly upload the sample IPython Notebook to the AzureML IPython Notebook service and start running it.</span></span> <span data-ttu-id="f2164-301">Pour effectuer le chargement vers le service AzureML IPython Notebook, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f2164-301">Here are the steps to upload to AzureML IPython Notebook service:</span></span>

1. <span data-ttu-id="f2164-302">Connectez-vous à votre espace de travail AzureML et cliquez successivement sur Studio en haut de l’écran et sur NOTEBOOKS sur la gauche de la page web.</span><span class="sxs-lookup"><span data-stu-id="f2164-302">Log in to your AzureML workspace, click "Studio" at the top, and click "NOTEBOOKS" on the left side of the web page.</span></span>
   
    ![Diagramme n°22][22]
2. <span data-ttu-id="f2164-304">Cliquez sur NOUVEAU dans le coin inférieur gauche de la page web, puis sélectionnez Python 2.</span><span class="sxs-lookup"><span data-stu-id="f2164-304">Click "NEW" on the left bottom corner of the web page, and select "Python 2".</span></span> <span data-ttu-id="f2164-305">Indiquez alors un nom pour le notebook et cochez la case pour créer le IPython Notebook vide.</span><span class="sxs-lookup"><span data-stu-id="f2164-305">Then, provide a name to the notebook and click the check mark to create the new blank IPython Notebook.</span></span>
   
    ![Diagramme n°23][23]
3. <span data-ttu-id="f2164-307">Cliquez sur le symbole Jupyter dans le coin supérieur gauche du nouvel IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="f2164-307">Click the "Jupyter" symbol on the left top corner of the new IPython Notebook.</span></span>
   
    ![Diagramme n°24][24]
4. <span data-ttu-id="f2164-309">Effectuez un glisser-déplacer de l’exemple d’IPython Notebook vers la page **d’arborescence** du service AzureML IPython Notebook, puis cliquez sur **Charger**.</span><span class="sxs-lookup"><span data-stu-id="f2164-309">Drag and drop the sample IPython Notebook to the **tree** page of your AzureML IPython Notebook service, and click **Upload**.</span></span> <span data-ttu-id="f2164-310">L’exemple de IPython Notebook est alors chargé vers le service AzureML IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="f2164-310">Then, the sample IPython Notebook will be uploaded to the AzureML IPython Notebook service.</span></span>
   
    ![Diagramme n°25][25]

<span data-ttu-id="f2164-312">Pour exécuter l’exemple de IPython Notebook ou le fichier de script Python, vous avez besoin des packages Python ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f2164-312">In order to run the sample IPython Notebook or the Python script file, the following Python packages are needed.</span></span> <span data-ttu-id="f2164-313">Si vous utilisez le service AzureML IPython Notebook, ces packages ont été préinstallés.</span><span class="sxs-lookup"><span data-stu-id="f2164-313">If you are using the AzureML IPython Notebook service, these packages have been pre-installed.</span></span>

    - <span data-ttu-id="f2164-314">pandas</span><span class="sxs-lookup"><span data-stu-id="f2164-314">pandas</span></span>
    - <span data-ttu-id="f2164-315">numpy</span><span class="sxs-lookup"><span data-stu-id="f2164-315">numpy</span></span>
    - <span data-ttu-id="f2164-316">matplotlib</span><span class="sxs-lookup"><span data-stu-id="f2164-316">matplotlib</span></span>
    - <span data-ttu-id="f2164-317">pyodbc</span><span class="sxs-lookup"><span data-stu-id="f2164-317">pyodbc</span></span>
    - <span data-ttu-id="f2164-318">PyTables</span><span class="sxs-lookup"><span data-stu-id="f2164-318">PyTables</span></span>

<span data-ttu-id="f2164-319">Il est recommandé de suivre la séquence ci-après lors de la génération de solutions analytiques avancées dans AzureML comportant de nombreuses données :</span><span class="sxs-lookup"><span data-stu-id="f2164-319">The recommended sequence when building advanced analytical solutions on AzureML with large data is the following:</span></span>

* <span data-ttu-id="f2164-320">Lisez un petit échantillon des données dans une trame de données en mémoire.</span><span class="sxs-lookup"><span data-stu-id="f2164-320">Read in a small sample of the data into an in-memory data frame.</span></span>
* <span data-ttu-id="f2164-321">Procédez à certaines visualisations et explorations à l’aide des données échantillonnées.</span><span class="sxs-lookup"><span data-stu-id="f2164-321">Perform some visualizations and explorations using the sampled data.</span></span>
* <span data-ttu-id="f2164-322">Expérimentez la conception de fonctionnalités en utilisant les données échantillonnées.</span><span class="sxs-lookup"><span data-stu-id="f2164-322">Experiment with feature engineering using the sampled data.</span></span>
* <span data-ttu-id="f2164-323">Pour exécuter de plus vastes tâches d’exploration des données, de manipulation des données et de conception de fonctionnalités, utilisez Python pour émettre des requêtes SQL directement dans SQL DW.</span><span class="sxs-lookup"><span data-stu-id="f2164-323">For larger data exploration, data manipulation and feature engineering, use Python to issue SQL Queries directly against the SQL DW.</span></span>
* <span data-ttu-id="f2164-324">Déterminez la taille d’échantillon qui convient pour la création de modèles Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f2164-324">Decide the sample size to be suitable for Azure Machine Learning model building.</span></span>

<span data-ttu-id="f2164-325">Vous trouverez ci-dessous quelques exemples d’exploration des données, de visualisation des données et de conception de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="f2164-325">The followings are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="f2164-326">D’autres exemples d’exploration des données se trouvent dans l’exemple de IPython Notebook et le fichier d’exemple de script Python.</span><span class="sxs-lookup"><span data-stu-id="f2164-326">More data explorations can be found in the sample IPython Notebook and the sample Python script file.</span></span>

### <a name="initialize-database-credentials"></a><span data-ttu-id="f2164-327">Initialiser les informations d’identification de la base de données</span><span class="sxs-lookup"><span data-stu-id="f2164-327">Initialize database credentials</span></span>
<span data-ttu-id="f2164-328">Initialisez vos paramètres de connexion à la base de données dans les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="f2164-328">Initialize your database connection settings in the following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a><span data-ttu-id="f2164-329">Créer une connexion à la base de données</span><span class="sxs-lookup"><span data-stu-id="f2164-329">Create database connection</span></span>
<span data-ttu-id="f2164-330">Voici la chaîne de connexion qui crée la connexion à la base de données.</span><span class="sxs-lookup"><span data-stu-id="f2164-330">Here is the connection string that creates the connection to the database.</span></span>

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="f2164-331">Afficher le nombre de lignes et de colonnes de la table <nyctaxi_trip></span><span class="sxs-lookup"><span data-stu-id="f2164-331">Report number of rows and columns in table <nyctaxi_trip></span></span>
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

* <span data-ttu-id="f2164-332">Nombre total de lignes = 173 179 759</span><span class="sxs-lookup"><span data-stu-id="f2164-332">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="f2164-333">Nombre total de colonnes = 14</span><span class="sxs-lookup"><span data-stu-id="f2164-333">Total number of columns = 14</span></span>

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a><span data-ttu-id="f2164-334">Afficher le nombre de lignes et de colonnes de la table <nyctaxi_fare></span><span class="sxs-lookup"><span data-stu-id="f2164-334">Report number of rows and columns in table <nyctaxi_fare></span></span>
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

* <span data-ttu-id="f2164-335">Nombre total de lignes = 173 179 759</span><span class="sxs-lookup"><span data-stu-id="f2164-335">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="f2164-336">Nombre total de colonnes = 11</span><span class="sxs-lookup"><span data-stu-id="f2164-336">Total number of columns = 11</span></span>

### <a name="read-in-a-small-data-sample-from-the-sql-data-warehouse-database"></a><span data-ttu-id="f2164-337">Lire un petit échantillon de données de la base de données SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f2164-337">Read-in a small data sample from the SQL Data Warehouse Database</span></span>
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
    print 'Time to read the sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="f2164-338">Temps de lecture de la table d’exemple = 14,096495 secondes.</span><span class="sxs-lookup"><span data-stu-id="f2164-338">Time to read the sample table is 14.096495 seconds.</span></span>  
<span data-ttu-id="f2164-339">Nombre de lignes et de colonnes récupérées = (1000, 21)</span><span class="sxs-lookup"><span data-stu-id="f2164-339">Number of rows and columns retrieved = (1000, 21).</span></span>

### <a name="descriptive-statistics"></a><span data-ttu-id="f2164-340">Statistiques descriptives</span><span class="sxs-lookup"><span data-stu-id="f2164-340">Descriptive statistics</span></span>
<span data-ttu-id="f2164-341">Vous êtes désormais prêt à explorer les données échantillonnées.</span><span class="sxs-lookup"><span data-stu-id="f2164-341">Now you are ready to explore the sampled data.</span></span> <span data-ttu-id="f2164-342">Nous allons commencer par examiner certaines statistiques descriptives relatives au champ **trip\_distance** (ou à tout autre champ que vous choisissez de spécifier).</span><span class="sxs-lookup"><span data-stu-id="f2164-342">We start with looking at some descriptive statistics for the **trip\_distance** (or any other fields you choose to specify).</span></span>

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a><span data-ttu-id="f2164-343">Visualisation : Exemple de diagramme à surfaces</span><span class="sxs-lookup"><span data-stu-id="f2164-343">Visualization: Box plot example</span></span>
<span data-ttu-id="f2164-344">Nous examinons ensuite le diagramme à surfaces concernant la distance des courses afin de visualiser les quantiles.</span><span class="sxs-lookup"><span data-stu-id="f2164-344">Next we look at the box plot for the trip distance to visualize the quantiles.</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Diagramme #1][1]

### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="f2164-346">Visualisation : Exemple de diagramme de distribution</span><span class="sxs-lookup"><span data-stu-id="f2164-346">Visualization: Distribution plot example</span></span>
<span data-ttu-id="f2164-347">Graphiques qui visualisent la distribution et histogramme correspondant aux distances des courses échantillonnées.</span><span class="sxs-lookup"><span data-stu-id="f2164-347">Plots that visualize the distribution and a histogram for the sampled trip distances.</span></span>

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Diagramme #2][2]

### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="f2164-349">Visualisation : Diagrammes en bâtons et linéaires</span><span class="sxs-lookup"><span data-stu-id="f2164-349">Visualization: Bar and line plots</span></span>
<span data-ttu-id="f2164-350">Dans cet exemple, nous compartimentons la distance des trajets en cinq zones et nous visualisons les résultats de cette opération.</span><span class="sxs-lookup"><span data-stu-id="f2164-350">In this example, we bin the trip distance into five bins and visualize the binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="f2164-351">Nous pouvons représenter la distribution des compartiments ci-dessus dans un diagramme en bâtons ou dans un diagramme linéaire comme suit :</span><span class="sxs-lookup"><span data-stu-id="f2164-351">We can plot the above bin distribution in a bar or line plot with:</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Diagramme #3][3]

<span data-ttu-id="f2164-353">and</span><span class="sxs-lookup"><span data-stu-id="f2164-353">and</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Diagramme #4][4]

### <a name="visualization-scatterplot-examples"></a><span data-ttu-id="f2164-355">Visualisation : Exemples de nuage de points</span><span class="sxs-lookup"><span data-stu-id="f2164-355">Visualization: Scatterplot examples</span></span>
<span data-ttu-id="f2164-356">Nous représentons le diagramme de dispersion entre **trip\_time\_in\_secs** et **trip\_distance** pour déterminer s’il existe une corrélation.</span><span class="sxs-lookup"><span data-stu-id="f2164-356">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** to see if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Diagramme #6][6]

<span data-ttu-id="f2164-358">De la même façon, nous pouvons vérifier la relation entre **rate\_code** et **trip\_distance**.</span><span class="sxs-lookup"><span data-stu-id="f2164-358">Similarly we can check the relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Diagramme #8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="f2164-360">Exploration des données échantillonnées à l’aide de requêtes SQL dans IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="f2164-360">Data exploration on sampled data using SQL queries in IPython notebook</span></span>
<span data-ttu-id="f2164-361">Dans cette section, nous allons explorer les distributions de données à l’aide de l’échantillon de données que nous avons stocké dans la table créée ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f2164-361">In this section, we explore data distributions using the sampled data which is persisted in the new table we created above.</span></span> <span data-ttu-id="f2164-362">Notez que des explorations similaires peuvent être effectuées à l’aide des tables d’origine.</span><span class="sxs-lookup"><span data-stu-id="f2164-362">Note that similar explorations can be performed using the original tables.</span></span>

#### <a name="exploration-report-number-of-rows-and-columns-in-the-sampled-table"></a><span data-ttu-id="f2164-363">Exploration : Afficher le nombre de lignes et de colonnes dans la table échantillonnée</span><span class="sxs-lookup"><span data-stu-id="f2164-363">Exploration: Report number of rows and columns in the sampled table</span></span>
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a><span data-ttu-id="f2164-364">Exploration : Distribution avec et sans pourboire</span><span class="sxs-lookup"><span data-stu-id="f2164-364">Exploration: Tipped/not tripped Distribution</span></span>
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a><span data-ttu-id="f2164-365">Exploration : Distribution des classes de pourboires</span><span class="sxs-lookup"><span data-stu-id="f2164-365">Exploration: Tip class distribution</span></span>
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-the-tip-distribution-by-class"></a><span data-ttu-id="f2164-366">Exploration : Tracer la distribution des pourboires par classe</span><span class="sxs-lookup"><span data-stu-id="f2164-366">Exploration: Plot the tip distribution by class</span></span>
    tip_class_dist['tip_freq'].plot(kind='bar')

![Diagramme n°26][26]

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="f2164-368">Exploration : distribution quotidienne des courses</span><span class="sxs-lookup"><span data-stu-id="f2164-368">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="f2164-369">Exploration : distribution des courses par médaillon</span><span class="sxs-lookup"><span data-stu-id="f2164-369">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a><span data-ttu-id="f2164-370">Exploration : Distribution des courses par médaillon et par licence de taxi</span><span class="sxs-lookup"><span data-stu-id="f2164-370">Exploration: Trip distribution by medallion and hack license</span></span>
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a><span data-ttu-id="f2164-371">Exploration : Distribution des durées de course</span><span class="sxs-lookup"><span data-stu-id="f2164-371">Exploration: Trip time distribution</span></span>
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a><span data-ttu-id="f2164-372">Exploration : Distribution des distances de course</span><span class="sxs-lookup"><span data-stu-id="f2164-372">Exploration: Trip distance distribution</span></span>
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a><span data-ttu-id="f2164-373">Exploration : Distribution des types de paiement</span><span class="sxs-lookup"><span data-stu-id="f2164-373">Exploration: Payment type distribution</span></span>
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-the-final-form-of-the-featurized-table"></a><span data-ttu-id="f2164-374">Vérifiez le format final de la table affichée</span><span class="sxs-lookup"><span data-stu-id="f2164-374">Verify the final form of the featurized table</span></span>
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <span data-ttu-id="f2164-375"><a name="mlmodel"></a>Créer des modèles dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f2164-375"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="f2164-376">Nous pouvons à présent passer aux phases de création et de déploiement de modèles dans [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="f2164-376">We are now ready to proceed to model building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="f2164-377">Les données sont prêtes à être utilisées dans tous les problèmes de prédiction identifiés précédemment, à savoir :</span><span class="sxs-lookup"><span data-stu-id="f2164-377">The data is ready to be used in any of the prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="f2164-378">**Classification binaire**: prédire si un pourboire a ou non été versé pour une course.</span><span class="sxs-lookup"><span data-stu-id="f2164-378">**Binary classification**: To predict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="f2164-379">**Classification multiclasse**: prédire la fourchette du pourboire versé en fonction des classes précédemment définies.</span><span class="sxs-lookup"><span data-stu-id="f2164-379">**Multiclass classification**: To predict the range of tip paid, according to the previously defined classes.</span></span>
3. <span data-ttu-id="f2164-380">**Tâche de régression**: prédire le montant du pourboire versé pour une course.</span><span class="sxs-lookup"><span data-stu-id="f2164-380">**Regression task**: To predict the amount of tip paid for a trip.</span></span>  

<span data-ttu-id="f2164-381">Pour démarrer l’exercice de modélisation, connectez-vous à votre espace de travail **Azure Machine Learning** .</span><span class="sxs-lookup"><span data-stu-id="f2164-381">To begin the modeling exercise, log in to your **Azure Machine Learning** workspace.</span></span> <span data-ttu-id="f2164-382">Si vous n’avez pas encore créé d’espace de travail d’apprentissage automatique, consultez l’article [Créer un espace de travail Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="f2164-382">If you have not yet created a machine learning workspace, see [Create an Azure ML workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="f2164-383">Pour plus d’informations sur la prise en main d’Azure Machine Learning, consultez la page [Azure Machine Learning Studio - De quoi s’agit-il ?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="f2164-383">To get started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="f2164-384">Connectez-vous à [Azure Machine Learning Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="f2164-384">Log in to [Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="f2164-385">La page d’accueil de Studio permet d’accéder à une multitude d’informations, de vidéos, de didacticiels, de liens vers la documentation de référence des modules et d’autres ressources.</span><span class="sxs-lookup"><span data-stu-id="f2164-385">The Studio Home page provides a wealth of information, videos, tutorials, links to the Modules Reference, and other resources.</span></span> <span data-ttu-id="f2164-386">Pour plus d’informations sur Azure Machine Learning, consultez le [Centre de documentation Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="f2164-386">For more information about Azure Machine Learning, consult the [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="f2164-387">Une expérience de formation classique se déroule comme suit :</span><span class="sxs-lookup"><span data-stu-id="f2164-387">A typical training experiment consists of the following steps:</span></span>

1. <span data-ttu-id="f2164-388">Création d’une expérience à l’aide du bouton **+NOUVEAU** .</span><span class="sxs-lookup"><span data-stu-id="f2164-388">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="f2164-389">Insertion des données dans Azure ML.</span><span class="sxs-lookup"><span data-stu-id="f2164-389">Get the data into Azure ML.</span></span>
3. <span data-ttu-id="f2164-390">Prétraitement, transformation et manipulation des données en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="f2164-390">Pre-process, transform and manipulate the data as needed.</span></span>
4. <span data-ttu-id="f2164-391">Génération des fonctionnalités requises.</span><span class="sxs-lookup"><span data-stu-id="f2164-391">Generate features as needed.</span></span>
5. <span data-ttu-id="f2164-392">Fractionnement des données sous forme de jeux de données d’apprentissage/de validation/de test (ou utilisation de jeux de données distincts pour chacune de ces opérations).</span><span class="sxs-lookup"><span data-stu-id="f2164-392">Split the data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="f2164-393">Sélection d’un ou de plusieurs algorithmes d’apprentissage automatique en fonction du problème d’apprentissage à résoudre.</span><span class="sxs-lookup"><span data-stu-id="f2164-393">Select one or more machine learning algorithms depending on the learning problem to solve.</span></span> <span data-ttu-id="f2164-394">Exemples : classification binaire, classification multiclasse, régression.</span><span class="sxs-lookup"><span data-stu-id="f2164-394">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="f2164-395">Formation d’un ou de plusieurs modèles à l’aide du jeu de données d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="f2164-395">Train one or more models using the training dataset.</span></span>
8. <span data-ttu-id="f2164-396">Notation du jeu de données de validation à l’aide des modèles formés.</span><span class="sxs-lookup"><span data-stu-id="f2164-396">Score the validation dataset using the trained model(s).</span></span>
9. <span data-ttu-id="f2164-397">Évaluation des modèles afin de calculer les métriques pertinents pour le problème d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="f2164-397">Evaluate the model(s) to compute the relevant metrics for the learning problem.</span></span>
10. <span data-ttu-id="f2164-398">Ajustement des modèles et sélection du meilleur modèle à déployer.</span><span class="sxs-lookup"><span data-stu-id="f2164-398">Fine tune the model(s) and select the best model to deploy.</span></span>

<span data-ttu-id="f2164-399">Dans cet exercice, nous avons déjà exploré et généré les données dans SQL Data Warehouse, et déterminé la taille de l’échantillon à ingérer dans Azure ML.</span><span class="sxs-lookup"><span data-stu-id="f2164-399">In this exercise, we have already explored and engineered the data in SQL Data Warehouse, and decided on the sample size to ingest in Azure ML.</span></span> <span data-ttu-id="f2164-400">Pour créer un ou plusieurs des modèles de prédiction, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f2164-400">Here is the procedure to build one or more of the prediction models:</span></span>

1. <span data-ttu-id="f2164-401">Intégrez les données dans Azure Machine Learning avec le module [Importer des données][import-data], disponible dans la section **Entrée et sortie des données**.</span><span class="sxs-lookup"><span data-stu-id="f2164-401">Get the data into Azure ML using the [Import Data][import-data] module, available in the **Data Input and Output** section.</span></span> <span data-ttu-id="f2164-402">Pour plus d’informations, consultez la page de référence du module [Importer les données][import-data] .</span><span class="sxs-lookup"><span data-stu-id="f2164-402">For more information, see the [Import Data][import-data] module reference page.</span></span>
   
    ![Importer les données Azure ML][17]
2. <span data-ttu-id="f2164-404">Dans le panneau **Propriétés**, sélectionnez **Azure SQL Database** dans le champ **Source de données**.</span><span class="sxs-lookup"><span data-stu-id="f2164-404">Select **Azure SQL Database** as the **Data source** in the **Properties** panel.</span></span>
3. <span data-ttu-id="f2164-405">Dans le champ **Nom du serveur de base de données** , entrez le nom DNS de la base de données.</span><span class="sxs-lookup"><span data-stu-id="f2164-405">Enter the database DNS name in the **Database server name** field.</span></span> <span data-ttu-id="f2164-406">Format : `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="f2164-406">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="f2164-407">Dans le champ **Nom de la base de données** , entrez le nom de la base de données.</span><span class="sxs-lookup"><span data-stu-id="f2164-407">Enter the **Database name** in the corresponding field.</span></span>
5. <span data-ttu-id="f2164-408">Entrez le *nom d’utilisateur SQL* dans le champ **Nom de compte d’utilisateur du serveur**, et le *mot de passe* dans le champ **Mot de passe de compte d’utilisateur du serveur**.</span><span class="sxs-lookup"><span data-stu-id="f2164-408">Enter the *SQL user name* in the **Server user account name**, and the *password* in the **Server user account password**.</span></span>
6. <span data-ttu-id="f2164-409">Cochez la case **Accepter tout certificat de serveur** .</span><span class="sxs-lookup"><span data-stu-id="f2164-409">Check the **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="f2164-410">Dans la zone de texte **Requête de base de données** , collez la requête qui extrait les champs de base de données nécessaires (y compris les champs calculés tels que les étiquettes) et qui sous-échantillonne les données pour obtenir la taille d’échantillon souhaitée.</span><span class="sxs-lookup"><span data-stu-id="f2164-410">In the **Database query** edit text area, paste the query which extracts the necessary database fields (including any computed fields such as the labels) and down samples the data to the desired sample size.</span></span>

<span data-ttu-id="f2164-411">Un exemple d’expérience de classification binaire lisant directement les données de la base de données SQL Data Warehouse est illustré dans la figure ci-dessous (pensez à remplacer les noms des tables nyctaxi_trip et nyctaxi_fare par le nom du schéma et les noms des tables que vous avez utilisés dans votre procédure).</span><span class="sxs-lookup"><span data-stu-id="f2164-411">An example of a binary classification experiment reading data directly from the SQL Data Warehouse database is in the figure below (remember to replace the table names nyctaxi_trip and nyctaxi_fare by the schema name and the table names you used in your walkthrough).</span></span> <span data-ttu-id="f2164-412">Vous pouvez créer des expériences similaires pour les problèmes de classification multiclasse et de régression.</span><span class="sxs-lookup"><span data-stu-id="f2164-412">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Formation Azure Machine Learning][10]

> [!IMPORTANT]
> <span data-ttu-id="f2164-414">Dans les exemples de requêtes d’extraction et d’échantillonnage de données de modélisation qui sont fournis aux sections précédentes, **toutes les étiquettes des trois exercices de modélisation sont incluses dans la requête**.</span><span class="sxs-lookup"><span data-stu-id="f2164-414">In the modeling data extraction and sampling query examples provided in previous sections, **all labels for the three modeling exercises are included in the query**.</span></span> <span data-ttu-id="f2164-415">Dans chacun des exercices de modélisation, une étape (obligatoire) importante consiste à **exclure** les étiquettes superflues pour les deux autres problèmes, ainsi que toute autre **fuite cible**.</span><span class="sxs-lookup"><span data-stu-id="f2164-415">An important (required) step in each of the modeling exercises is to **exclude** the unnecessary labels for the other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="f2164-416">Par exemple, si vous avez recours à la classification binaire, utilisez l’étiquette **tipped** et excluez les champs **tip\_class**, **tip\_amount** et **total\_amount**.</span><span class="sxs-lookup"><span data-stu-id="f2164-416">For example, when using binary classification, use the label **tipped** and exclude the fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="f2164-417">Les derniers champs sont des fuites cibles, car ils impliquent le pourboire versé.</span><span class="sxs-lookup"><span data-stu-id="f2164-417">The latter are target leaks since they imply the tip paid.</span></span>
> 
> <span data-ttu-id="f2164-418">Pour exclure les colonnes superflues ou les fuites cibles, vous pouvez utiliser le module [Sélectionner des colonnes dans le jeu de données][select-columns] ou [Modifier les métadonnées][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="f2164-418">To exclude any unnecessary columns or target leaks, you may use the [Select Columns in Dataset][select-columns] module or the [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="f2164-419">Pour plus d’informations, consultez les pages de référence [Sélectionner des colonnes dans le jeu de données][select-columns] et [Modifier les métadonnées][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="f2164-419">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="f2164-420"><a name="mldeploy"></a>Déployer des modèles dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f2164-420"><a name="mldeploy"></a>Deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="f2164-421">Lorsque votre modèle est prêt, vous pouvez facilement le déployer sous la forme d’un service web directement à partir de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="f2164-421">When your model is ready, you can easily deploy it as a web service directly from the experiment.</span></span> <span data-ttu-id="f2164-422">Pour plus d’informations sur le déploiement de services web Azure Machine Learning, consultez [Déployer un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="f2164-422">For more information about deploying Azure ML web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="f2164-423">Pour déployer un nouveau service web, vous devez :</span><span class="sxs-lookup"><span data-stu-id="f2164-423">To deploy a new web service, you need to:</span></span>

1. <span data-ttu-id="f2164-424">créer une expérience de notation ;</span><span class="sxs-lookup"><span data-stu-id="f2164-424">Create a scoring experiment.</span></span>
2. <span data-ttu-id="f2164-425">déployer le service web.</span><span class="sxs-lookup"><span data-stu-id="f2164-425">Deploy the web service.</span></span>

<span data-ttu-id="f2164-426">Pour créer une expérience de notation à partir d’une expérience de formation **terminée**, cliquez sur **CRÉER UNE EXPÉRIENCE DE NOTATION** dans la barre d’action inférieure.</span><span class="sxs-lookup"><span data-stu-id="f2164-426">To create a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in the lower action bar.</span></span>

![Notation Azure][18]

<span data-ttu-id="f2164-428">Azure Machine Learning va essayer de créer une expérience de notation reposant sur les composants de l’expérience d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="f2164-428">Azure Machine Learning will attempt to create a scoring experiment based on the components of the training experiment.</span></span> <span data-ttu-id="f2164-429">Il va notamment :</span><span class="sxs-lookup"><span data-stu-id="f2164-429">In particular, it will:</span></span>

1. <span data-ttu-id="f2164-430">enregistrer le modèle formé et supprimer les modules de formation de modèle ;</span><span class="sxs-lookup"><span data-stu-id="f2164-430">Save the trained model and remove the model training modules.</span></span>
2. <span data-ttu-id="f2164-431">identifier un **port d’entrée** logique pour représenter le schéma de données d’entrée attendu ;</span><span class="sxs-lookup"><span data-stu-id="f2164-431">Identify a logical **input port** to represent the expected input data schema.</span></span>
3. <span data-ttu-id="f2164-432">identifier un **port de sortie** logique pour représenter le schéma de sortie de service web attendu.</span><span class="sxs-lookup"><span data-stu-id="f2164-432">Identify a logical **output port** to represent the expected web service output schema.</span></span>

<span data-ttu-id="f2164-433">Une fois l’expérience de notation créée, vérifiez-la et effectuez les ajustements nécessaires.</span><span class="sxs-lookup"><span data-stu-id="f2164-433">When the scoring experiment is created, review it and make adjust as needed.</span></span> <span data-ttu-id="f2164-434">Un ajustement classique consiste à remplacer le jeu de données d’entrée et/ou la requête par un autre jeu excluant les champs d’étiquette, car ces derniers ne seront pas disponibles lors de l’appel du service.</span><span class="sxs-lookup"><span data-stu-id="f2164-434">A typical adjustment is to replace the input dataset and/or query with one which excludes label fields, as these will not be available when the service is called.</span></span> <span data-ttu-id="f2164-435">Il est également recommandé de restreindre la taille du jeu de données d’entrée et/ou de la requête au nombre d’enregistrements suffisants pour indiquer le schéma d’entrée.</span><span class="sxs-lookup"><span data-stu-id="f2164-435">It is also a good practice to reduce the size of the input dataset and/or query to a few records, just enough to indicate the input schema.</span></span> <span data-ttu-id="f2164-436">Pour le port de sortie, il est courant d’exclure tous les champs d’entrée et de n’inclure que les valeurs **Étiquettes notées** et **Probabilités notées** dans la sortie à l’aide du module [Sélectionner des colonnes dans le jeu de données][select-columns].</span><span class="sxs-lookup"><span data-stu-id="f2164-436">For the output port, it is common to exclude all input fields and only include the **Scored Labels** and **Scored Probabilities** in the output using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="f2164-437">La figure ci-après illustre un exemple d’expérience de notation.</span><span class="sxs-lookup"><span data-stu-id="f2164-437">A sample scoring experiment is provided in the figure below.</span></span> <span data-ttu-id="f2164-438">Quand vous êtes prêt à effectuer le déploiement, cliquez sur le bouton **PUBLIER LE SERVICE WEB** de la barre d’action inférieure.</span><span class="sxs-lookup"><span data-stu-id="f2164-438">When ready to deploy, click the **PUBLISH WEB SERVICE** button in the lower action bar.</span></span>

![Publication Azure Machine Learning][11]

## <a name="summary"></a><span data-ttu-id="f2164-440">Résumé</span><span class="sxs-lookup"><span data-stu-id="f2164-440">Summary</span></span>
<span data-ttu-id="f2164-441">Pour résumer ce didacticiel pas à pas, vous avez créé un environnement de science des données Azure, manipulé un jeu de données public volumineux, depuis l’acquisition des données et la formation de modèles, via le processus TDSP (Team Data Science Process), jusqu’au déploiement d’un service web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f2164-441">To recap what we have done in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset, taking it through the Team Data Science Process, all the way from data acquisition to model training, and then to the deployment of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="f2164-442">Informations de licence</span><span class="sxs-lookup"><span data-stu-id="f2164-442">License information</span></span>
<span data-ttu-id="f2164-443">Cet exemple de procédure pas à pas et les scripts et notebooks IPython qui lui sont associés sont partagés par Microsoft sous licence MIT.</span><span class="sxs-lookup"><span data-stu-id="f2164-443">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under the MIT license.</span></span> <span data-ttu-id="f2164-444">Pour plus d’informations, voir le fichier LICENSE.txt figurant dans le répertoire de l’exemple de code sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="f2164-444">Please check the LICENSE.txt file in in the directory of the sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="f2164-445">Références</span><span class="sxs-lookup"><span data-stu-id="f2164-445">References</span></span>
<span data-ttu-id="f2164-446">•    [Page de téléchargement des jeux de données NYC Taxi Trips par Andrés Monroy (en anglais)](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="f2164-446">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="f2164-447">•    [Page de partage des données relatives aux courses en taxi new-yorkais par Chris Whong (en anglais)](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="f2164-447">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="f2164-448">•    [Page de recherche et de statistiques de la Commission des services de taxis et de limousines de la ville de New York (en anglais)](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="f2164-448">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

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
