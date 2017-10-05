---
title: "Utiliser Redgate pour charger des données sur votre entrepôt de données Azure | Microsoft Docs"
description: "Apprenez à utiliser Redgate Data Platform Studio pour les scénarios d’entreposage de données."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 670aef98-31f7-4436-86c0-cc989a39fe7f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: a38b237d5bfc0450c1ca79b53a5784dbb9bf8602
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a><span data-ttu-id="1acbe-103">Chargement de données avec Redgate Data Platform Studio</span><span class="sxs-lookup"><span data-stu-id="1acbe-103">Load data with Redgate Data Platform Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1acbe-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="1acbe-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)
> * [<span data-ttu-id="1acbe-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="1acbe-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [<span data-ttu-id="1acbe-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="1acbe-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)
> * [<span data-ttu-id="1acbe-107">BCP</span><span class="sxs-lookup"><span data-stu-id="1acbe-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="1acbe-108">Ce didacticiel vous montre comment utiliser [Redgate Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) pour déplacer des données d’un serveur SQL Server local vers Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1acbe-108">This tutorial shows you how to use [Redgate's Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) to move data from an on-premises SQL Server to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="1acbe-109">Data Platform Studio applique les correctifs de compatibilité et optimisations les plus appropriés. Il s’agit donc du moyen le plus rapide pour vous familiariser avec SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1acbe-109">Data Platform Studio applies the most appropriate compatibility fixes and optimizations, so it's the quickest way to get started with SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="1acbe-110">[Redgate](http://www.red-gate.com) est un partenaire Microsoft de longue date, et fournit divers outils SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1acbe-110">[Redgate](http://www.red-gate.com) is a long-time Microsoft partner that delivers various SQL Server tools.</span></span> <span data-ttu-id="1acbe-111">Cette fonctionnalité de Data Platform Studio est disponible gratuitement pour un usage commercial et non commercial.</span><span class="sxs-lookup"><span data-stu-id="1acbe-111">This feature in Data Platform Studio has been made available freely for both commercial and non-commercial use.</span></span>
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="1acbe-112">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="1acbe-112">Before you begin</span></span>
### <a name="create-or-identify-resources"></a><span data-ttu-id="1acbe-113">Créer ou identifier des ressources</span><span class="sxs-lookup"><span data-stu-id="1acbe-113">Create or identify resources</span></span>
<span data-ttu-id="1acbe-114">Avant de commencer ce didacticiel, vous devez disposer des ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="1acbe-114">Before starting this tutorial, you need to have:</span></span>

* <span data-ttu-id="1acbe-115">**Base de données SQL Server locale** : les données que vous souhaitez importer dans SQL Data Warehouse doivent provenir d’un serveur SQL Server local (version 2008R2 ou ultérieure).</span><span class="sxs-lookup"><span data-stu-id="1acbe-115">**on-premises SQL Server Database**: The data you want to import to SQL Data Warehouse needs to come from an on-premises SQL Server (version 2008R2 or above).</span></span> <span data-ttu-id="1acbe-116">Data Platform Studio ne peut pas importer les données directement à partir d’une base de données Azure SQL Database, ni à partir de fichiers texte.</span><span class="sxs-lookup"><span data-stu-id="1acbe-116">Data Platform Studio cannot import data directly from an Azure SQL Database or from text files.</span></span>
* <span data-ttu-id="1acbe-117">**Compte de stockage Azure** : Data Platform Studio organise les données dans le stockage Blob Azure avant de les charger dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1acbe-117">**Azure Storage Account**: Data Platform Studio stages the data in Azure Blob Storage before loading it into SQL Data Warehouse.</span></span> <span data-ttu-id="1acbe-118">Le compte de stockage doit utiliser le modèle de déploiement « Resource Manager » (la valeur par défaut) plutôt que le modèle de déploiement « Classic ».</span><span class="sxs-lookup"><span data-stu-id="1acbe-118">The storage account must be using the “Resource Manager” deployment model (the default) rather than the “Classic” deployment model.</span></span> <span data-ttu-id="1acbe-119">Si vous ne possédez pas de compte de stockage, découvrez comment créer un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="1acbe-119">If you don't have a storage account, learn how to Create a storage account.</span></span> 
* <span data-ttu-id="1acbe-120">**SQL Data Warehouse** : ce didacticiel déplace les données d’un serveur SQL Server local vers SQL Data Warehouse ; vous devez donc disposer d’un entrepôt de données en ligne.</span><span class="sxs-lookup"><span data-stu-id="1acbe-120">**SQL Data Warehouse**: This tutorial moves the data from on-premises SQL Server to SQL Data Warehouse, so you need to have a data warehouse online.</span></span> <span data-ttu-id="1acbe-121">Si vous n’en possédez pas encore, découvrez comment créer un entrepôt Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1acbe-121">If you do not already have a data warehouse, learn how to Create an Azure SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="1acbe-122">Les performances se trouvent améliorées si le compte de stockage et l’entrepôt de données sont créés dans la même région.</span><span class="sxs-lookup"><span data-stu-id="1acbe-122">Performance is improved if the storage account and the data warehouse are created in the same region.</span></span>
> 
> 

## <a name="step-1-sign-in-to-data-platform-studio-with-your-azure-account"></a><span data-ttu-id="1acbe-123">Étape 1 : se connecter à Data Platform Studio avec votre compte Azure</span><span class="sxs-lookup"><span data-stu-id="1acbe-123">Step 1: Sign in to Data Platform Studio with your Azure account</span></span>
<span data-ttu-id="1acbe-124">Ouvrez votre navigateur Web et accédez au site [Data Platform Studio](https://www.dataplatformstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="1acbe-124">Open your web browser and navigate to the [Data Platform Studio](https://www.dataplatformstudio.com/) website.</span></span> <span data-ttu-id="1acbe-125">Connectez-vous avec le même compte Azure que celui que vous avez utilisé pour créer le compte de stockage et l’entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="1acbe-125">Sign in with the same Azure account that you used to create the storage account and data warehouse.</span></span> <span data-ttu-id="1acbe-126">Si votre adresse de messagerie est associée à un compte professionnel ou scolaire et à un compte Microsoft, veillez à choisir le compte qui a accès à vos ressources.</span><span class="sxs-lookup"><span data-stu-id="1acbe-126">If your email address is associated with both a work or school account and a Microsoft account, be sure to choose the account that has access to your resources.</span></span>

> [!NOTE]
> <span data-ttu-id="1acbe-127">S’il s’agit de votre première utilisation de Data Platform Studio, vous êtes invité à autoriser l’application à gérer vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="1acbe-127">If this is your first time using Data Platform Studio, you are asked to grant the application permission to manage your Azure resources.</span></span>
> 
> 

## <a name="step-2-start-the-import-wizard"></a><span data-ttu-id="1acbe-128">Étape 2 : démarrer l’Assistant Importation</span><span class="sxs-lookup"><span data-stu-id="1acbe-128">Step 2: Start the Import Wizard</span></span>
<span data-ttu-id="1acbe-129">Dans l’écran principal de DPS, sélectionnez le lien Import to Azure SQL Data Warehouse (Importer dans Azure SQL Data Warehouse) pour démarrer l’Assistant Importation.</span><span class="sxs-lookup"><span data-stu-id="1acbe-129">From the DPS main screen, select the Import to Azure SQL Data Warehouse link to start the import wizard.</span></span>

![][1]

## <a name="step-3-install-the-data-platform-studio-gateway"></a><span data-ttu-id="1acbe-130">Étape 3 : installer la passerelle Data Platform Studio</span><span class="sxs-lookup"><span data-stu-id="1acbe-130">Step 3: Install the Data Platform Studio Gateway</span></span>
<span data-ttu-id="1acbe-131">Pour vous connecter à votre base de données SQL Server locale, vous devez installer la passerelle DPS.</span><span class="sxs-lookup"><span data-stu-id="1acbe-131">To connect to your on-premises SQL Server database, you need to install the DPS Gateway.</span></span> <span data-ttu-id="1acbe-132">La passerelle est un agent client qui donne accès à votre environnement local, extrait les données et les télécharge vers votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="1acbe-132">The gateway is a client agent that provides access to your on-premises environment, extracts the data, and uploads it to your storage account.</span></span> <span data-ttu-id="1acbe-133">Vos données ne transitent jamais via les serveurs de Redgate.</span><span class="sxs-lookup"><span data-stu-id="1acbe-133">Your data never passes through Redgate’s servers.</span></span> <span data-ttu-id="1acbe-134">Pour installer la passerelle :</span><span class="sxs-lookup"><span data-stu-id="1acbe-134">To install the Gateway:</span></span>

1. <span data-ttu-id="1acbe-135">Cliquez sur le lien **Create Gateway** (Créer une passerelle).</span><span class="sxs-lookup"><span data-stu-id="1acbe-135">Click the **Create Gateway** link</span></span>
2. <span data-ttu-id="1acbe-136">Téléchargez et installez la passerelle via le programme d’installation fourni.</span><span class="sxs-lookup"><span data-stu-id="1acbe-136">Download and install the Gateway using the provided installer</span></span>

![][2]

> [!NOTE]
> <span data-ttu-id="1acbe-137">La passerelle peut être installée sur n’importe quel ordinateur ayant un accès réseau à la base de données SQL Server source.</span><span class="sxs-lookup"><span data-stu-id="1acbe-137">The Gateway can be installed on any machine with network access to the source SQL Server database.</span></span> <span data-ttu-id="1acbe-138">Elle accède à la base de données SQL Server en utilisant les identifiants d’authentification Windows de l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="1acbe-138">It accesses the SQL Server database using Windows authentication with the credentials of the current user.</span></span>
> 
> 

<span data-ttu-id="1acbe-139">Une fois la passerelle installée, elle passe à l’état Connected (Connecté) et vous pouvez sélectionner Next (Suivant).</span><span class="sxs-lookup"><span data-stu-id="1acbe-139">Once installed, the Gateway status changes to Connected and you can select Next.</span></span>

## <a name="step-4-identify-the-source-database"></a><span data-ttu-id="1acbe-140">Étape 4 : identifier la base de données source</span><span class="sxs-lookup"><span data-stu-id="1acbe-140">Step 4: Identify the source database</span></span>
<span data-ttu-id="1acbe-141">Dans la zone de texte *Enter Server Name* (Entrer le nom du serveur), saisissez le nom du serveur qui héberge votre base de données et sélectionnez **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="1acbe-141">In the *Enter Server Name* textbox, enter the name of the server that hosts your database and select **Next**.</span></span> <span data-ttu-id="1acbe-142">Ensuite, dans le menu déroulant, sélectionnez la base de données à partir de laquelle vous souhaitez importer les données.</span><span class="sxs-lookup"><span data-stu-id="1acbe-142">Then, from the drop-down menu, select the database you want to import data from.</span></span>

![][3]

<span data-ttu-id="1acbe-143">DPS recherche les tables à importer dans la base de données sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="1acbe-143">DPS inspects the selected database for tables to import.</span></span> <span data-ttu-id="1acbe-144">Par défaut, DPS importe toutes les tables de la base de données.</span><span class="sxs-lookup"><span data-stu-id="1acbe-144">By default, DPS imports all the tables in the database.</span></span> <span data-ttu-id="1acbe-145">Vous pouvez sélectionner ou désélectionner des tables en développant le lien All Tables (Toutes les tables).</span><span class="sxs-lookup"><span data-stu-id="1acbe-145">You can select or deselect tables by expanding the All Tables link.</span></span> <span data-ttu-id="1acbe-146">Sélectionnez le bouton Next (Suivant) pour continuer.</span><span class="sxs-lookup"><span data-stu-id="1acbe-146">Select the Next button to move forward.</span></span>

## <a name="step-5-choose-a-storage-account-to-stage-the-data"></a><span data-ttu-id="1acbe-147">Étape 5 : choisir un compte de stockage à utiliser pour stocker les données</span><span class="sxs-lookup"><span data-stu-id="1acbe-147">Step 5: Choose a storage account to stage the data</span></span>
<span data-ttu-id="1acbe-148">DPS vous invite à entrer un emplacement à utiliser pour stocker les données.</span><span class="sxs-lookup"><span data-stu-id="1acbe-148">DPS prompts you for a location to stage the data.</span></span> <span data-ttu-id="1acbe-149">Choisissez un compte de stockage existant dans votre abonnement, puis sélectionnez **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="1acbe-149">Choose an existing storage account from your subscription and select **Next**.</span></span>

> [!NOTE]
> <span data-ttu-id="1acbe-150">DPS crée un nouveau conteneur d’objets blob dans le compte de stockage choisi et utilise un dossier distinct pour chaque importation.</span><span class="sxs-lookup"><span data-stu-id="1acbe-150">DPS will create a new blob container in the chosen storage account and use a distinct folder for each import.</span></span>
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a><span data-ttu-id="1acbe-151">Étape 6 : créer un entrepôt de données</span><span class="sxs-lookup"><span data-stu-id="1acbe-151">Step 6: Select a data warehouse</span></span>
<span data-ttu-id="1acbe-152">Sélectionnez ensuite une base de données [Azure SQL Data Warehouse](http://aka.ms/sqldw) en ligne dans laquelle importer les données.</span><span class="sxs-lookup"><span data-stu-id="1acbe-152">Next, you select an online [Azure SQL Data Warehouse](http://aka.ms/sqldw) database to import the data into.</span></span> <span data-ttu-id="1acbe-153">Une fois que vous avez sélectionné votre base de données, vous devez entrer les informations d’identification pour vous connecter à la base de données et sélectionner **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="1acbe-153">Once you've selected your database, you need to enter the credentials to connect to the database and select **Next**.</span></span>

![][5]

> [!NOTE]
> <span data-ttu-id="1acbe-154">DPS fusionne les tables de données source dans l’entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="1acbe-154">DPS merges the source data tables into the data warehouse.</span></span> <span data-ttu-id="1acbe-155">DPS vous avertit si le nom de la table nécessite d’écraser des tables existantes dans l’entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="1acbe-155">DPS warns you if the table name requires it to overwrite existing tables in the data warehouse.</span></span> <span data-ttu-id="1acbe-156">Vous pouvez supprimer des objets existants dans l’entrepôt de données en cochant Delete all existing objects before import (Supprimer tous les objets existants avant l’importation).</span><span class="sxs-lookup"><span data-stu-id="1acbe-156">You may optionally delete any existing objects in the data warehouse by ticking Delete all existing objects before import.</span></span>
> 
> 

## <a name="step-7-import-the-data"></a><span data-ttu-id="1acbe-157">Étape 7 : importer les données</span><span class="sxs-lookup"><span data-stu-id="1acbe-157">Step 7: Import the data</span></span>
<span data-ttu-id="1acbe-158">DPS vous demande de confirmer que vous souhaitez importer les données.</span><span class="sxs-lookup"><span data-stu-id="1acbe-158">DPS confirms that you would like to import the data.</span></span> <span data-ttu-id="1acbe-159">Cliquez simplement sur le bouton de démarrage de l’importation pour commencer l’importation de données.</span><span class="sxs-lookup"><span data-stu-id="1acbe-159">Simply click the Start import button to begin the data import.</span></span>

![][6]

<span data-ttu-id="1acbe-160">DPS indique la progression de l’extraction et du chargement des données à partir du serveur SQL Server local, ainsi que la progression de l’importation dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1acbe-160">DPS displays a visualization that shows the progress of extracting and uploading the data from the on-premises SQL Server and the progress of the import into SQL Data Warehouse.</span></span>

![][7]

<span data-ttu-id="1acbe-161">Une fois l’importation terminée, DPS affiche un résumé de l’importation des données et un rapport de modification des correctifs de compatibilité qui ont été effectués.</span><span class="sxs-lookup"><span data-stu-id="1acbe-161">Once the import is complete, DPS displays a summary of the data import and a change report of the compatibility fixes that have been performed.</span></span>

![][8]

## <a name="next-steps"></a><span data-ttu-id="1acbe-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1acbe-162">Next steps</span></span>
<span data-ttu-id="1acbe-163">Pour explorer les données dans SQL Data Warehouse, reportez-vous à :</span><span class="sxs-lookup"><span data-stu-id="1acbe-163">To explore your data within SQL Data Warehouse, start by viewing:</span></span>

* <span data-ttu-id="1acbe-164">[Interroger Azure SQL Data Warehouse (sqlcmd) (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span><span class="sxs-lookup"><span data-stu-id="1acbe-164">[Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span></span>
* <span data-ttu-id="1acbe-165">[Visualiser des données avec Power BI][Visualize data with Power BI]</span><span class="sxs-lookup"><span data-stu-id="1acbe-165">[Visualize data with Power BI][Visualize data with Power BI]</span></span>

<span data-ttu-id="1acbe-166">Pour en savoir plus sur Redgate Data Platform Studio :</span><span class="sxs-lookup"><span data-stu-id="1acbe-166">To learn more about Redgate’s Data Platform Studio:</span></span>

* [<span data-ttu-id="1acbe-167">Visitez la page d’accueil de DPS</span><span class="sxs-lookup"><span data-stu-id="1acbe-167">Visit the DPS homepage</span></span>](http://www.dataplatformstudio.com/)
* [<span data-ttu-id="1acbe-168">Regardez une démonstration de DPS sur Channel9</span><span class="sxs-lookup"><span data-stu-id="1acbe-168">Watch a demo of DPS on Channel9</span></span>](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

<span data-ttu-id="1acbe-169">Pour obtenir une vue d’ensemble d’autres méthodes de migration et de chargement de vos données dans SQL Data Warehouse, voir :</span><span class="sxs-lookup"><span data-stu-id="1acbe-169">For an overview of other ways to migrate and load your data in SQL Data Warehouse see:</span></span>

* <span data-ttu-id="1acbe-170">[Migration de votre solution vers SQL Data Warehouse][Migrate your solution to SQL Data Warehouse]</span><span class="sxs-lookup"><span data-stu-id="1acbe-170">[Migrate your solution to SQL Data Warehouse][Migrate your solution to SQL Data Warehouse]</span></span>
* [<span data-ttu-id="1acbe-171">Chargement de données dans Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1acbe-171">Load data into Azure SQL Data Warehouse</span></span>](sql-data-warehouse-overview-load.md)

<span data-ttu-id="1acbe-172">Pour obtenir des conseils supplémentaires en matière de développement, consultez l’article [Vue d’ensemble sur le développement SQL Data Warehouse](sql-data-warehouse-overview-develop.md).</span><span class="sxs-lookup"><span data-stu-id="1acbe-172">For more development tips, see the [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-redgate/2016-10-05_15-59-56.png
[2]: media/sql-data-warehouse-redgate/2016-10-05_11-16-07.png
[3]: media/sql-data-warehouse-redgate/2016-10-05_11-17-46.png
[4]: media/sql-data-warehouse-redgate/2016-10-05_11-20-41.png
[5]: media/sql-data-warehouse-redgate/2016-10-05_11-31-24.png
[6]: media/sql-data-warehouse-redgate/2016-10-05_11-32-20.png
[7]: media/sql-data-warehouse-redgate/2016-10-05_11-49-53.png
[8]: media/sql-data-warehouse-redgate/2016-10-05_12-57-10.png

<!--Article references-->
[Query Azure SQL Data Warehouse (Visual Studio)]: ./sql-data-warehouse-query-visual-studio.md
[Visualize data with Power BI]: ./sql-data-warehouse-get-started-visualize-with-power-bi.md
[Migrate your solution to SQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
