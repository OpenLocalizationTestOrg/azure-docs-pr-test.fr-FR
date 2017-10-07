---
title: "entrepôt de données Azure aaaUse Redgate tooload données tooyour | Documents Microsoft"
description: "Découvrez comment Data Platform Studio de toouse Redgate pour les scénarios d’entreposage de données."
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
ms.openlocfilehash: 6082390c07c8ffa73ebd8ab272ace00ba8bb1897
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a><span data-ttu-id="83341-103">Chargement de données avec Redgate Data Platform Studio</span><span class="sxs-lookup"><span data-stu-id="83341-103">Load data with Redgate Data Platform Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="83341-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="83341-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)
> * [<span data-ttu-id="83341-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="83341-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [<span data-ttu-id="83341-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="83341-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)
> * [<span data-ttu-id="83341-107">BCP</span><span class="sxs-lookup"><span data-stu-id="83341-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="83341-108">Ce didacticiel vous montre comment toouse [données plateforme Studio de Redgate](http://www.red-gate.com/products/azure-development/data-platform-studio/) données de toomove (STD) à partir d’un tooAzure de SQL Server locale SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="83341-108">This tutorial shows you how toouse [Redgate's Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) toomove data from an on-premises SQL Server tooAzure SQL Data Warehouse.</span></span> <span data-ttu-id="83341-109">Studio de plateforme de données applique des correctifs de compatibilité plus appropriés hello et optimisations, donc il a hello plus rapidement moyen tooget en main de l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="83341-109">Data Platform Studio applies hello most appropriate compatibility fixes and optimizations, so it's hello quickest way tooget started with SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="83341-110">[Redgate](http://www.red-gate.com) est un partenaire Microsoft de longue date, et fournit divers outils SQL Server.</span><span class="sxs-lookup"><span data-stu-id="83341-110">[Redgate](http://www.red-gate.com) is a long-time Microsoft partner that delivers various SQL Server tools.</span></span> <span data-ttu-id="83341-111">Cette fonctionnalité de Data Platform Studio est disponible gratuitement pour un usage commercial et non commercial.</span><span class="sxs-lookup"><span data-stu-id="83341-111">This feature in Data Platform Studio has been made available freely for both commercial and non-commercial use.</span></span>
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="83341-112">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="83341-112">Before you begin</span></span>
### <a name="create-or-identify-resources"></a><span data-ttu-id="83341-113">Créer ou identifier des ressources</span><span class="sxs-lookup"><span data-stu-id="83341-113">Create or identify resources</span></span>
<span data-ttu-id="83341-114">Avant de commencer ce didacticiel, vous devez toohave :</span><span class="sxs-lookup"><span data-stu-id="83341-114">Before starting this tutorial, you need toohave:</span></span>

* <span data-ttu-id="83341-115">**base de données SQL Server locale**: hello les données que vous souhaitez tooimport tooSQL l’entrepôt de données doit toocome à partir d’un ordinateur local SQL Server (version 2008R2 ou version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="83341-115">**on-premises SQL Server Database**: hello data you want tooimport tooSQL Data Warehouse needs toocome from an on-premises SQL Server (version 2008R2 or above).</span></span> <span data-ttu-id="83341-116">Data Platform Studio ne peut pas importer les données directement à partir d’une base de données Azure SQL Database, ni à partir de fichiers texte.</span><span class="sxs-lookup"><span data-stu-id="83341-116">Data Platform Studio cannot import data directly from an Azure SQL Database or from text files.</span></span>
* <span data-ttu-id="83341-117">**Compte de stockage Azure**: données plateforme Studio prépare les données hello dans le stockage d’objets Blob Azure avant de les charger dans l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="83341-117">**Azure Storage Account**: Data Platform Studio stages hello data in Azure Blob Storage before loading it into SQL Data Warehouse.</span></span> <span data-ttu-id="83341-118">compte de stockage Hello doit utiliser le modèle de déploiement « Gestionnaire de ressources » hello (valeur par défaut de hello) au lieu du modèle de déploiement « Classiques » hello.</span><span class="sxs-lookup"><span data-stu-id="83341-118">hello storage account must be using hello “Resource Manager” deployment model (hello default) rather than hello “Classic” deployment model.</span></span> <span data-ttu-id="83341-119">Si vous n’avez pas un compte de stockage, découvrez comment tooCreate un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="83341-119">If you don't have a storage account, learn how tooCreate a storage account.</span></span> 
* <span data-ttu-id="83341-120">**SQL Data Warehouse**: ce didacticiel déplace hello données locale SQL Server tooSQL entrepôt de données, par conséquent, vous devez toohave un entrepôt de données en ligne.</span><span class="sxs-lookup"><span data-stu-id="83341-120">**SQL Data Warehouse**: This tutorial moves hello data from on-premises SQL Server tooSQL Data Warehouse, so you need toohave a data warehouse online.</span></span> <span data-ttu-id="83341-121">Si vous n’avez pas déjà d’un entrepôt de données, découvrez comment tooCreate un entrepôt de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="83341-121">If you do not already have a data warehouse, learn how tooCreate an Azure SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="83341-122">Les performances sont améliorées si le compte de stockage hello et entrepôt de données hello sont créés dans hello même région.</span><span class="sxs-lookup"><span data-stu-id="83341-122">Performance is improved if hello storage account and hello data warehouse are created in hello same region.</span></span>
> 
> 

## <a name="step-1-sign-in-toodata-platform-studio-with-your-azure-account"></a><span data-ttu-id="83341-123">Étape 1 : Se connecter tooData plateforme Studio avec votre compte Azure</span><span class="sxs-lookup"><span data-stu-id="83341-123">Step 1: Sign in tooData Platform Studio with your Azure account</span></span>
<span data-ttu-id="83341-124">Ouvrez votre navigateur web et accédez toohello [Data Platform Studio](https://www.dataplatformstudio.com/) site Web.</span><span class="sxs-lookup"><span data-stu-id="83341-124">Open your web browser and navigate toohello [Data Platform Studio](https://www.dataplatformstudio.com/) website.</span></span> <span data-ttu-id="83341-125">Connectez-vous avec hello même compte Azure que vous toocreate utilisé hello stockage compte et les données de l’entrepôt.</span><span class="sxs-lookup"><span data-stu-id="83341-125">Sign in with hello same Azure account that you used toocreate hello storage account and data warehouse.</span></span> <span data-ttu-id="83341-126">Si votre adresse de messagerie est associée à un travail ou compte scolaire et un compte Microsoft, que compte hello toochoose a tooyour d’accéder aux ressources.</span><span class="sxs-lookup"><span data-stu-id="83341-126">If your email address is associated with both a work or school account and a Microsoft account, be sure toochoose hello account that has access tooyour resources.</span></span>

> [!NOTE]
> <span data-ttu-id="83341-127">S’il s’agit de la première fois à l’aide de données plateforme Studio, vous êtes invité à toogrant hello application autorisation toomanage vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="83341-127">If this is your first time using Data Platform Studio, you are asked toogrant hello application permission toomanage your Azure resources.</span></span>
> 
> 

## <a name="step-2-start-hello-import-wizard"></a><span data-ttu-id="83341-128">Étape 2 : Démarrer l’Assistant Importation de hello</span><span class="sxs-lookup"><span data-stu-id="83341-128">Step 2: Start hello Import Wizard</span></span>
<span data-ttu-id="83341-129">À partir de l’écran principal de hello STD, sélectionnez Assistant Importation de hello toostart lien hello importation tooAzure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="83341-129">From hello DPS main screen, select hello Import tooAzure SQL Data Warehouse link toostart hello import wizard.</span></span>

![][1]

## <a name="step-3-install-hello-data-platform-studio-gateway"></a><span data-ttu-id="83341-130">Étape 3 : Installer hello passerelle de données plateforme Studio</span><span class="sxs-lookup"><span data-stu-id="83341-130">Step 3: Install hello Data Platform Studio Gateway</span></span>
<span data-ttu-id="83341-131">tooconnect tooyour de données SQL Server locale, vous devez tooinstall hello STD passerelle.</span><span class="sxs-lookup"><span data-stu-id="83341-131">tooconnect tooyour on-premises SQL Server database, you need tooinstall hello DPS Gateway.</span></span> <span data-ttu-id="83341-132">passerelle de Hello est un agent de client qui fournit l’accès tooyour environnement local, extrait des données de hello et il télécharge le compte de stockage tooyour.</span><span class="sxs-lookup"><span data-stu-id="83341-132">hello gateway is a client agent that provides access tooyour on-premises environment, extracts hello data, and uploads it tooyour storage account.</span></span> <span data-ttu-id="83341-133">Vos données ne transitent jamais via les serveurs de Redgate.</span><span class="sxs-lookup"><span data-stu-id="83341-133">Your data never passes through Redgate’s servers.</span></span> <span data-ttu-id="83341-134">hello tooinstall passerelle :</span><span class="sxs-lookup"><span data-stu-id="83341-134">tooinstall hello Gateway:</span></span>

1. <span data-ttu-id="83341-135">Cliquez sur hello **créer une passerelle** lien</span><span class="sxs-lookup"><span data-stu-id="83341-135">Click hello **Create Gateway** link</span></span>
2. <span data-ttu-id="83341-136">Téléchargement et installation de passerelle hello à l’aide de programme d’installation fourni hello</span><span class="sxs-lookup"><span data-stu-id="83341-136">Download and install hello Gateway using hello provided installer</span></span>

![][2]

> [!NOTE]
> <span data-ttu-id="83341-137">Hello passerelle peut être installé sur n’importe quel ordinateur avec la base de données de réseau accès toohello source SQL Server.</span><span class="sxs-lookup"><span data-stu-id="83341-137">hello Gateway can be installed on any machine with network access toohello source SQL Server database.</span></span> <span data-ttu-id="83341-138">Elle accède à base de données SQL Server hello à l’aide de l’authentification Windows avec informations d’identification hello de l’utilisateur actuel hello.</span><span class="sxs-lookup"><span data-stu-id="83341-138">It accesses hello SQL Server database using Windows authentication with hello credentials of hello current user.</span></span>
> 
> 

<span data-ttu-id="83341-139">Une fois installé, hello tooConnected de modifications de statut de passerelle et vous pouvez sélectionner suivant.</span><span class="sxs-lookup"><span data-stu-id="83341-139">Once installed, hello Gateway status changes tooConnected and you can select Next.</span></span>

## <a name="step-4-identify-hello-source-database"></a><span data-ttu-id="83341-140">Étape 4 : Identifier la base de données source hello</span><span class="sxs-lookup"><span data-stu-id="83341-140">Step 4: Identify hello source database</span></span>
<span data-ttu-id="83341-141">Bonjour *entrer le nom du serveur* zone de texte, entrez le nom hello du serveur hello qui héberge votre base de données et sélectionnez **suivant**.</span><span class="sxs-lookup"><span data-stu-id="83341-141">In hello *Enter Server Name* textbox, enter hello name of hello server that hosts your database and select **Next**.</span></span> <span data-ttu-id="83341-142">Puis, à partir du menu déroulant de hello, sélectionnez tooimport des données à partir de la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="83341-142">Then, from hello drop-down menu, select hello database you want tooimport data from.</span></span>

![][3]

<span data-ttu-id="83341-143">STD inspecte la base de données sélectionnée hello pour les tables tooimport.</span><span class="sxs-lookup"><span data-stu-id="83341-143">DPS inspects hello selected database for tables tooimport.</span></span> <span data-ttu-id="83341-144">Par défaut, std importe toutes les tables hello hello de base de données.</span><span class="sxs-lookup"><span data-stu-id="83341-144">By default, DPS imports all hello tables in hello database.</span></span> <span data-ttu-id="83341-145">Vous pouvez sélectionner ou désélectionner des tables en développant hello lier de toutes les Tables.</span><span class="sxs-lookup"><span data-stu-id="83341-145">You can select or deselect tables by expanding hello All Tables link.</span></span> <span data-ttu-id="83341-146">Sélectionnez hello suivant bouton toomove vers l’avant.</span><span class="sxs-lookup"><span data-stu-id="83341-146">Select hello Next button toomove forward.</span></span>

## <a name="step-5-choose-a-storage-account-toostage-hello-data"></a><span data-ttu-id="83341-147">Étape 5 : Choisissez une données hello compte toostage de stockage</span><span class="sxs-lookup"><span data-stu-id="83341-147">Step 5: Choose a storage account toostage hello data</span></span>
<span data-ttu-id="83341-148">STD vous invite à entrer un emplacement toostage hello de données.</span><span class="sxs-lookup"><span data-stu-id="83341-148">DPS prompts you for a location toostage hello data.</span></span> <span data-ttu-id="83341-149">Choisissez un compte de stockage existant dans votre abonnement, puis sélectionnez **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="83341-149">Choose an existing storage account from your subscription and select **Next**.</span></span>

> [!NOTE]
> <span data-ttu-id="83341-150">STD crée un conteneur d’objets blob Bonjour choisi le compte de stockage et utiliser un dossier distinct pour chaque importation.</span><span class="sxs-lookup"><span data-stu-id="83341-150">DPS will create a new blob container in hello chosen storage account and use a distinct folder for each import.</span></span>
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a><span data-ttu-id="83341-151">Étape 6 : créer un entrepôt de données</span><span class="sxs-lookup"><span data-stu-id="83341-151">Step 6: Select a data warehouse</span></span>
<span data-ttu-id="83341-152">Ensuite, vous sélectionnez une ligne [Azure SQL Data Warehouse](http://aka.ms/sqldw) tooimport des données hello dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="83341-152">Next, you select an online [Azure SQL Data Warehouse](http://aka.ms/sqldw) database tooimport hello data into.</span></span> <span data-ttu-id="83341-153">Une fois que vous avez sélectionné votre base de données, vous devez toohello de tooconnect tooenter hello informations d’identification de base de données et sélectionnez **suivant**.</span><span class="sxs-lookup"><span data-stu-id="83341-153">Once you've selected your database, you need tooenter hello credentials tooconnect toohello database and select **Next**.</span></span>

![][5]

> [!NOTE]
> <span data-ttu-id="83341-154">STD fusionne les tables de données source hello dans l’entrepôt de données hello.</span><span class="sxs-lookup"><span data-stu-id="83341-154">DPS merges hello source data tables into hello data warehouse.</span></span> <span data-ttu-id="83341-155">STD vous avertit si le nom de table hello il requiert toooverwrite des tables existantes dans l’entrepôt de données hello.</span><span class="sxs-lookup"><span data-stu-id="83341-155">DPS warns you if hello table name requires it toooverwrite existing tables in hello data warehouse.</span></span> <span data-ttu-id="83341-156">Vous pouvez supprimer les objets existants dans l’entrepôt de données hello en cochant supprimer tous les objets existants avant l’importation.</span><span class="sxs-lookup"><span data-stu-id="83341-156">You may optionally delete any existing objects in hello data warehouse by ticking Delete all existing objects before import.</span></span>
> 
> 

## <a name="step-7-import-hello-data"></a><span data-ttu-id="83341-157">Étape 7 : Importer des données de hello</span><span class="sxs-lookup"><span data-stu-id="83341-157">Step 7: Import hello data</span></span>
<span data-ttu-id="83341-158">STD confirme que vous souhaitez que les données de salutation tooimport.</span><span class="sxs-lookup"><span data-stu-id="83341-158">DPS confirms that you would like tooimport hello data.</span></span> <span data-ttu-id="83341-159">Cliquez simplement sur hello démarrer Importation bouton toobegin hello l’importation des données.</span><span class="sxs-lookup"><span data-stu-id="83341-159">Simply click hello Start import button toobegin hello data import.</span></span>

![][6]

<span data-ttu-id="83341-160">STD affiche une visualisation qui affiche la progression de hello d’extraction et chargement des données de hello depuis hello local SQL Server et hello la progression de l’importation de hello dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="83341-160">DPS displays a visualization that shows hello progress of extracting and uploading hello data from hello on-premises SQL Server and hello progress of hello import into SQL Data Warehouse.</span></span>

![][7]

<span data-ttu-id="83341-161">Une fois l’importation hello est terminée, std affiche un résumé de l’importation de données hello et un rapport des modifications des correctifs de compatibilité hello qui ont été effectuées.</span><span class="sxs-lookup"><span data-stu-id="83341-161">Once hello import is complete, DPS displays a summary of hello data import and a change report of hello compatibility fixes that have been performed.</span></span>

![][8]

## <a name="next-steps"></a><span data-ttu-id="83341-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="83341-162">Next steps</span></span>
<span data-ttu-id="83341-163">tooexplore vos données dans l’entrepôt de données SQL, commencez par affichage :</span><span class="sxs-lookup"><span data-stu-id="83341-163">tooexplore your data within SQL Data Warehouse, start by viewing:</span></span>

* <span data-ttu-id="83341-164">[Interroger Azure SQL Data Warehouse (sqlcmd) (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span><span class="sxs-lookup"><span data-stu-id="83341-164">[Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span></span>
* <span data-ttu-id="83341-165">[Visualiser des données avec Power BI][Visualize data with Power BI]</span><span class="sxs-lookup"><span data-stu-id="83341-165">[Visualize data with Power BI][Visualize data with Power BI]</span></span>

<span data-ttu-id="83341-166">toolearn plus en détail Data Platform Studio de Redgate :</span><span class="sxs-lookup"><span data-stu-id="83341-166">toolearn more about Redgate’s Data Platform Studio:</span></span>

* [<span data-ttu-id="83341-167">Visitez la page d’accueil de hello STD</span><span class="sxs-lookup"><span data-stu-id="83341-167">Visit hello DPS homepage</span></span>](http://www.dataplatformstudio.com/)
* [<span data-ttu-id="83341-168">Regardez une démonstration de DPS sur Channel9</span><span class="sxs-lookup"><span data-stu-id="83341-168">Watch a demo of DPS on Channel9</span></span>](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

<span data-ttu-id="83341-169">Pour une vue d’ensemble d’autres façons toomigrate et les charge vos données dans l’entrepôt de données SQL voir :</span><span class="sxs-lookup"><span data-stu-id="83341-169">For an overview of other ways toomigrate and load your data in SQL Data Warehouse see:</span></span>

* <span data-ttu-id="83341-170">[Migrer votre tooSQL solution entrepôt de données][Migrate your solution tooSQL Data Warehouse]</span><span class="sxs-lookup"><span data-stu-id="83341-170">[Migrate your solution tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse]</span></span>
* [<span data-ttu-id="83341-171">Chargement de données dans Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="83341-171">Load data into Azure SQL Data Warehouse</span></span>](sql-data-warehouse-overview-load.md)

<span data-ttu-id="83341-172">Pour plus de conseils de développement, consultez hello [vue d’ensemble du développement de SQL Data Warehouse](sql-data-warehouse-overview-develop.md).</span><span class="sxs-lookup"><span data-stu-id="83341-172">For more development tips, see hello [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span></span>

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
[Migrate your solution tooSQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
