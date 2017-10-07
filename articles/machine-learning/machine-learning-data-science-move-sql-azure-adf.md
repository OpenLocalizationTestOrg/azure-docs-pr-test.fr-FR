---
title: "aaaMove des données à partir d’un tooSQL de SQL Server sur site Azure avec Azure Data Factory | Documents Microsoft"
description: "Configurer un pipeline de définition d’application qui se compose de deux activités de migration de données qui déplacent les données entre eux sur une base quotidienne entre bases de données locale et dans le cloud de hello."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 7f7e78c7a84a259539221d3235b76bb5a3cf9866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-sql-server-toosql-azure-with-azure-data-factory"></a><span data-ttu-id="7b915-103">Déplacement des données à partir d’un ordinateur local SQL server tooSQL Azure avec Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7b915-103">Move data from an on-premises SQL server tooSQL Azure with Azure Data Factory</span></span>
<span data-ttu-id="7b915-104">Cette rubrique montre comment toomove des données à partir d’un tooa de base de données SQL Server locale base de données SQL Azure via à l’aide du stockage d’objets Blob Azure hello fabrique de données Azure (ADF).</span><span class="sxs-lookup"><span data-stu-id="7b915-104">This topic shows how toomove data from an on-premises SQL Server Database tooa SQL Azure Database via Azure Blob Storage using hello Azure Data Factory (ADF).</span></span>

<span data-ttu-id="7b915-105">Pour une table qui résume les différentes options de déplacement tooan de données base de données SQL Azure, consultez [déplacer les données tooan base de données SQL Azure pour Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="7b915-105">For a table that summarizes various options for moving data tooan Azure SQL Database, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

## <span data-ttu-id="7b915-106"><a name="intro"></a>Présentation : Nouveautés ADF et quand il doit être utilisé toomigrate données ?</span><span class="sxs-lookup"><span data-stu-id="7b915-106"><a name="intro"></a>Introduction: What is ADF and when should it be used toomigrate data?</span></span>
<span data-ttu-id="7b915-107">Azure Data Factory est un service d’intégration des données cloud entièrement géré qui orchestre et automatise le déplacement de hello et la transformation de données.</span><span class="sxs-lookup"><span data-stu-id="7b915-107">Azure Data Factory is a fully managed cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="7b915-108">concept clé de Hello dans le modèle de définition d’application hello est le pipeline.</span><span class="sxs-lookup"><span data-stu-id="7b915-108">hello key concept in hello ADF model is pipeline.</span></span> <span data-ttu-id="7b915-109">Un pipeline est un regroupement logique des activités, chacune définissant hello actions tooperform sur les données de hello contenues dans les jeux de données.</span><span class="sxs-lookup"><span data-stu-id="7b915-109">A pipeline is a logical grouping of Activities, each of which defines hello actions tooperform on hello data contained in Datasets.</span></span> <span data-ttu-id="7b915-110">Services liés sont des informations de hello toodefine utilisé nécessaires pour les ressources de données de Data Factory tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="7b915-110">Linked services are used toodefine hello information needed for Data Factory tooconnect toohello data resources.</span></span>

<span data-ttu-id="7b915-111">Avec la définition d’application, les services de traitement de données existants peuvent être composées dans des pipelines de données qui sont hautement disponible et gérée dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="7b915-111">With ADF, existing data processing services can be composed into data pipelines that are highly available and managed in hello cloud.</span></span> <span data-ttu-id="7b915-112">Ces pipelines de données peuvent être planifiée tooingest, préparer, transformer, analyser et publier des données et ADF gère et orchestre les données complexes hello et le traitement des dépendances.</span><span class="sxs-lookup"><span data-stu-id="7b915-112">These data pipelines can be scheduled tooingest, prepare, transform, analyze, and publish data, and ADF manages and orchestrates hello complex data and processing dependencies.</span></span> <span data-ttu-id="7b915-113">Solutions peuvent être cloud hello rapidement générées et déployées dans, la connexion d’un nombre croissant de locaux et cloud des sources de données.</span><span class="sxs-lookup"><span data-stu-id="7b915-113">Solutions can be quickly built and deployed in hello cloud, connecting a growing number of on-premises and cloud data sources.</span></span>

<span data-ttu-id="7b915-114">Utilisez plutôt ADF :</span><span class="sxs-lookup"><span data-stu-id="7b915-114">Consider using ADF:</span></span>

* <span data-ttu-id="7b915-115">Lorsque besoins toobe migré en permanence dans un scénario hybride qui accède à la fois des données sur site et ressources de cloud</span><span class="sxs-lookup"><span data-stu-id="7b915-115">when data needs toobe continually migrated in a hybrid scenario that accesses both on-premises and cloud resources</span></span>
* <span data-ttu-id="7b915-116">Lorsque les données de salutation sont traitées ou besoins toobe modifiée ou avoir une logique métier ajouté tooit en cours de migration.</span><span class="sxs-lookup"><span data-stu-id="7b915-116">when hello data is transacted or needs toobe modified or have business logic added tooit when being migrated.</span></span>

<span data-ttu-id="7b915-117">ADF permet hello de planification et de surveillance des travaux à l’aide de simples scripts JSON qui gèrent le déplacement de hello des données sur une base périodique.</span><span class="sxs-lookup"><span data-stu-id="7b915-117">ADF allows for hello scheduling and monitoring of jobs using simple JSON scripts that manage hello movement of data on a periodic basis.</span></span> <span data-ttu-id="7b915-118">ADF dispose également d'autres fonctionnalités comme la prise en charge des opérations complexes.</span><span class="sxs-lookup"><span data-stu-id="7b915-118">ADF also has other capabilities such as support for complex operations.</span></span> <span data-ttu-id="7b915-119">Pour plus d’informations sur la définition d’application, consultez documentation hello [fabrique de données Azure (ADF)](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="7b915-119">For more information on ADF, see hello documentation at [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span></span>

## <span data-ttu-id="7b915-120"><a name="scenario"></a>Hello scénario</span><span class="sxs-lookup"><span data-stu-id="7b915-120"><a name="scenario"></a>hello Scenario</span></span>
<span data-ttu-id="7b915-121">Nous allons configurer un pipeline ADF qui se compose de deux activités de migration de données.</span><span class="sxs-lookup"><span data-stu-id="7b915-121">We set up an ADF pipeline that composes two data migration activities.</span></span> <span data-ttu-id="7b915-122">Ensemble, ils passent données quotidiennement entre une base de données SQL locale et une base de données SQL Azure dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="7b915-122">Together they move data on a daily basis between an on-premises SQL database and an Azure SQL Database in hello cloud.</span></span> <span data-ttu-id="7b915-123">Hello deux activités sont :</span><span class="sxs-lookup"><span data-stu-id="7b915-123">hello two activities are:</span></span>

* <span data-ttu-id="7b915-124">copier des données d’une tooan de base de données SQL Server sur site compte de stockage d’objets Blob Azure</span><span class="sxs-lookup"><span data-stu-id="7b915-124">copy data from an on-premises SQL Server database tooan Azure Blob Storage account</span></span>
* <span data-ttu-id="7b915-125">copier des données à partir de tooan de compte de stockage d’objets Blob Azure hello base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7b915-125">copy data from hello Azure Blob Storage account tooan Azure SQL Database.</span></span>

> [!NOTE]
> <span data-ttu-id="7b915-126">Hello les étapes indiquées ici ont été adaptées à partir de hello plus didacticiel fourni par l’équipe ADF hello : [déplacement des données entre des sources locales et cloud avec la passerelle de gestion des données](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) toohello les sections correspondantes de cette rubrique de référence Vous trouverez lorsque cela est approprié.</span><span class="sxs-lookup"><span data-stu-id="7b915-126">hello steps shown here have been adapted from hello more detailed tutorial provided by hello ADF team: [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) References toohello relevant sections of that topic are provided when appropriate.</span></span>
>
>

## <span data-ttu-id="7b915-127"><a name="prereqs"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="7b915-127"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="7b915-128">Ce didacticiel part du principe que vous disposez de :</span><span class="sxs-lookup"><span data-stu-id="7b915-128">This tutorial assumes you have:</span></span>

* <span data-ttu-id="7b915-129">Un **abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="7b915-129">An **Azure subscription**.</span></span> <span data-ttu-id="7b915-130">Si vous n’avez pas d’abonnement, vous pouvez vous inscrire à un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7b915-130">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7b915-131">Un **compte de stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="7b915-131">An **Azure storage account**.</span></span> <span data-ttu-id="7b915-132">Vous utilisez un compte de stockage Azure pour stocker les données de hello dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="7b915-132">You use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="7b915-133">Si vous n’avez pas un compte de stockage Azure, consultez hello [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) l’article.</span><span class="sxs-lookup"><span data-stu-id="7b915-133">If you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="7b915-134">Une fois que vous avez créé le compte de stockage hello, vous devez le compte de hello tooobtain clé utilisé le stockage de hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="7b915-134">After you have created hello storage account, you need tooobtain hello account key used tooaccess hello storage.</span></span> <span data-ttu-id="7b915-135">Voir [Gérer vos clés d’accès de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="7b915-135">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="7b915-136">Accès tooan **base de données SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="7b915-136">Access tooan **Azure SQL Database**.</span></span> <span data-ttu-id="7b915-137">Si vous devez configurer une base de données SQL Azure, hello phrase sujet [prise en main de Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) fournit des informations sur la façon de tooprovision une nouvelle instance de la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7b915-137">If you must set up an Azure SQL Database, hello tpoic [Getting Started with Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) provides information on how tooprovision a new instance of an Azure SQL Database.</span></span>
* <span data-ttu-id="7b915-138">**Azure PowerShell** installé et configuré localement.</span><span class="sxs-lookup"><span data-stu-id="7b915-138">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="7b915-139">Pour obtenir des instructions, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7b915-139">For instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!NOTE]
> <span data-ttu-id="7b915-140">Cette procédure utilise hello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7b915-140">This procedure uses hello [Azure portal](https://portal.azure.com/).</span></span>
>
>

## <span data-ttu-id="7b915-141"><a name="upload-data"></a>Téléchargement hello données tooyour local SQL Server</span><span class="sxs-lookup"><span data-stu-id="7b915-141"><a name="upload-data"></a> Upload hello data tooyour on-premises SQL Server</span></span>
<span data-ttu-id="7b915-142">Nous utilisons hello [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) processus de migration toodemonstrate hello.</span><span class="sxs-lookup"><span data-stu-id="7b915-142">We use hello [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) toodemonstrate hello migration process.</span></span> <span data-ttu-id="7b915-143">Hello NYC Taxi dataset est disponible, comme indiqué dans cette publication, sur le stockage d’objets blob Azure [NYC Taxi données](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="7b915-143">hello NYC Taxi dataset is available, as noted in that post, on Azure blob storage [NYC Taxi Data](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="7b915-144">les données de salutation possède deux fichiers, fichier hello trip_data.csv, qui contient les détails de voyage, et fichier hello trip_far.csv, qui contient les détails des prix hello payé pour chaque sortie.</span><span class="sxs-lookup"><span data-stu-id="7b915-144">hello data has two files, hello trip_data.csv file, which contains trip details, and hello  trip_far.csv file, which contains details of hello fare paid for each trip.</span></span> <span data-ttu-id="7b915-145">Un échantillon et une description de ces fichiers sont fournis dans la [description du jeu de données des voyages NYC Taxi](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span><span class="sxs-lookup"><span data-stu-id="7b915-145">A sample and description of these files are provided in [NYC Taxi Trips Dataset Description](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span></span>

<span data-ttu-id="7b915-146">Vous pouvez adapter procédure hello fourni ici ensemble tooa de vos propres données ou suivez les étapes de hello comme décrit à l’aide de hello NYC Taxi le jeu de données.</span><span class="sxs-lookup"><span data-stu-id="7b915-146">You can either adapt hello procedure provided here tooa set of your own data or follow hello steps as described by using hello NYC Taxi dataset.</span></span> <span data-ttu-id="7b915-147">hello de tooupload NYC Taxi le jeu de données dans votre base de données SQL Server locale, procédez comme procédure hello [importer en bloc des données dans la base de données SQL Server](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span><span class="sxs-lookup"><span data-stu-id="7b915-147">tooupload hello NYC Taxi dataset into your on-premises SQL Server database, follow hello procedure outlined in [Bulk Import Data into SQL Server Database](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span></span> <span data-ttu-id="7b915-148">Ces instructions concernent un serveur SQL Server sur une Machine virtuelle de Azure, mais la procédure hello pour le téléchargement toohello local SQL Server est hello identiques.</span><span class="sxs-lookup"><span data-stu-id="7b915-148">These instructions are for a SQL Server on an Azure Virtual Machine, but hello procedure for uploading toohello on-premises SQL Server is hello same.</span></span>

## <span data-ttu-id="7b915-149"><a name="create-adf"></a> Création d’une Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7b915-149"><a name="create-adf"></a> Create an Azure Data Factory</span></span>
<span data-ttu-id="7b915-150">Hello des instructions sur la création d’une fabrique de données Azure et un groupe de ressources Bonjour [portail Azure](https://portal.azure.com/) sont fournies [créer une fabrique de données Azure](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span><span class="sxs-lookup"><span data-stu-id="7b915-150">hello instructions for creating a new Azure Data Factory and a resource group in hello [Azure portal](https://portal.azure.com/) are provided [Create an Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span></span> <span data-ttu-id="7b915-151">Nom hello nouvelle ADF instance *adfdsp* et nom du groupe de ressources hello créé *adfdsprg*.</span><span class="sxs-lookup"><span data-stu-id="7b915-151">Name hello new ADF instance *adfdsp* and name hello resource group created *adfdsprg*.</span></span>

## <a name="install-and-configure-up-hello-data-management-gateway"></a><span data-ttu-id="7b915-152">Installer et configurer des hello passerelle de gestion des données</span><span class="sxs-lookup"><span data-stu-id="7b915-152">Install and configure up hello Data Management Gateway</span></span>
<span data-ttu-id="7b915-153">tooenable vos pipelines dans un toowork de fabrique de données Azure avec un serveur de SQL Server locale, vous devez tooadd sous la forme d’une fabrique de données toohello Service lié.</span><span class="sxs-lookup"><span data-stu-id="7b915-153">tooenable your pipelines in an Azure data factory toowork with an on-premises SQL Server, you need tooadd it as a Linked Service toohello data factory.</span></span> <span data-ttu-id="7b915-154">toocreate un Service lié pour un ordinateur local SQL Server, vous devez :</span><span class="sxs-lookup"><span data-stu-id="7b915-154">toocreate a Linked Service for an on-premises SQL Server, you must:</span></span>

* <span data-ttu-id="7b915-155">Téléchargez et installez la passerelle de gestion des données de Microsoft sur l’ordinateur local de hello.</span><span class="sxs-lookup"><span data-stu-id="7b915-155">download and install Microsoft Data Management Gateway onto hello on-premises computer.</span></span>
* <span data-ttu-id="7b915-156">configurer service hello lié pour passerelle hello toouse des source de données hello localement.</span><span class="sxs-lookup"><span data-stu-id="7b915-156">configure hello linked service for hello on-premises data source toouse hello gateway.</span></span>

<span data-ttu-id="7b915-157">Hello passerelle de gestion des données sérialise et désérialise les données source et le récepteur de hello sur ordinateur hello où il est hébergé.</span><span class="sxs-lookup"><span data-stu-id="7b915-157">hello Data Management Gateway serializes and deserializes hello source and sink data on hello computer where it is hosted.</span></span>

<span data-ttu-id="7b915-158">Pour obtenir des détails et des instructions d’installation sur la passerelle de gestion des données, consultez [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="7b915-158">For set-up instructions and details on Data Management Gateway, see [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span></span>

## <span data-ttu-id="7b915-159"><a name="adflinkedservices"></a>Créer des ressources de données de services liés tooconnect toohello</span><span class="sxs-lookup"><span data-stu-id="7b915-159"><a name="adflinkedservices"></a>Create linked services tooconnect toohello data resources</span></span>
<span data-ttu-id="7b915-160">Un service lié définit les informations de hello nécessaires pour la ressource de données Azure Data Factory tooconnect tooa.</span><span class="sxs-lookup"><span data-stu-id="7b915-160">A linked service defines hello information needed for Azure Data Factory tooconnect tooa data resource.</span></span> <span data-ttu-id="7b915-161">procédure pas à pas de Hello pour la création de services liés est fourni dans [créer des services liés](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span><span class="sxs-lookup"><span data-stu-id="7b915-161">hello step-by-step procedure for creating linked services is provided in [Create linked services](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span></span>

<span data-ttu-id="7b915-162">Dans ce scénario, nous avons trois ressources pour lesquelles les services liés sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="7b915-162">We have three resources in this scenario for which linked services are needed.</span></span>

1. [<span data-ttu-id="7b915-163">Service lié pour SQL Server local</span><span class="sxs-lookup"><span data-stu-id="7b915-163">Linked service for on-premises SQL Server</span></span>](#adf-linked-service-onprem-sql)
2. [<span data-ttu-id="7b915-164">Service lié pour Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="7b915-164">Linked service for Azure Blob Storage</span></span>](#adf-linked-service-blob-store)
3. [<span data-ttu-id="7b915-165">Service lié pour base de données Azure SQL</span><span class="sxs-lookup"><span data-stu-id="7b915-165">Linked service for Azure SQL database</span></span>](#adf-linked-service-azure-sql)

### <span data-ttu-id="7b915-166"><a name="adf-linked-service-onprem-sql"></a>Service lié pour base de données SQL Server locale</span><span class="sxs-lookup"><span data-stu-id="7b915-166"><a name="adf-linked-service-onprem-sql"></a>Linked service for on-premises SQL Server database</span></span>
<span data-ttu-id="7b915-167">service de hello lié toocreate pour hello local SQL Server :</span><span class="sxs-lookup"><span data-stu-id="7b915-167">toocreate hello linked service for hello on-premises SQL Server:</span></span>

* <span data-ttu-id="7b915-168">Cliquez sur hello **magasin de données** dans la page d’accueil hello ADF sur le portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="7b915-168">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="7b915-169">Sélectionnez **SQL** et entrez hello *nom d’utilisateur* et *mot de passe* les informations d’identification pour hello local SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7b915-169">select **SQL** and enter hello *username* and *password* credentials for hello on-premises SQL Server.</span></span> <span data-ttu-id="7b915-170">Vous devez servername de hello tooenter comme un **nom de l’instance complet servername barre oblique inverse (nomserveur\nominstance)**.</span><span class="sxs-lookup"><span data-stu-id="7b915-170">You need tooenter hello servername as a **fully qualified servername backslash instance name (servername\instancename)**.</span></span> <span data-ttu-id="7b915-171">Hello du nom de service lié *adfonpremsql*.</span><span class="sxs-lookup"><span data-stu-id="7b915-171">Name hello linked service *adfonpremsql*.</span></span>

### <span data-ttu-id="7b915-172"><a name="adf-linked-service-blob-store"></a>Service lié pour les objets blob</span><span class="sxs-lookup"><span data-stu-id="7b915-172"><a name="adf-linked-service-blob-store"></a>Linked service for Blob</span></span>
<span data-ttu-id="7b915-173">toocreate hello service lié pour le compte de stockage d’objets Blob Azure hello :</span><span class="sxs-lookup"><span data-stu-id="7b915-173">toocreate hello linked service for hello Azure Blob Storage account:</span></span>

* <span data-ttu-id="7b915-174">Cliquez sur hello **magasin de données** dans la page d’accueil hello ADF sur le portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="7b915-174">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="7b915-175">Sélectionnez **Azure Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="7b915-175">select **Azure Storage Account**</span></span>
* <span data-ttu-id="7b915-176">entrez hello du compte clé et le conteneur du nom du stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7b915-176">enter hello Azure Blob Storage account key and container name.</span></span> <span data-ttu-id="7b915-177">Hello du nom du Service lié *adfds*.</span><span class="sxs-lookup"><span data-stu-id="7b915-177">Name hello Linked Service *adfds*.</span></span>

### <span data-ttu-id="7b915-178"><a name="adf-linked-service-azure-sql"></a>Service lié pour la base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="7b915-178"><a name="adf-linked-service-azure-sql"></a>Linked service for Azure SQL database</span></span>
<span data-ttu-id="7b915-179">toocreate hello service lié pour hello de base de données SQL Azure :</span><span class="sxs-lookup"><span data-stu-id="7b915-179">toocreate hello linked service for hello Azure SQL Database:</span></span>

* <span data-ttu-id="7b915-180">Cliquez sur hello **magasin de données** dans la page d’accueil hello ADF sur le portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="7b915-180">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="7b915-181">Sélectionnez **SQL Azure** et entrez hello *nom d’utilisateur* et *mot de passe* informations d’identification pour hello de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7b915-181">select **Azure SQL** and enter hello *username* and *password* credentials for hello Azure SQL Database.</span></span> <span data-ttu-id="7b915-182">Hello *nom d’utilisateur* doit être spécifié en tant que  *user@servername* .</span><span class="sxs-lookup"><span data-stu-id="7b915-182">hello *username* must be specified as *user@servername*.</span></span>   

## <span data-ttu-id="7b915-183"><a name="adf-tables"></a>Définir et créer des tables toospecify comment tooaccess hello des jeux de données</span><span class="sxs-lookup"><span data-stu-id="7b915-183"><a name="adf-tables"></a>Define and create tables toospecify how tooaccess hello datasets</span></span>
<span data-ttu-id="7b915-184">Créer des tables qui spécifient la structure de hello, l’emplacement et la disponibilité de jeux de données hello avec hello script basé sur les procédures suivantes.</span><span class="sxs-lookup"><span data-stu-id="7b915-184">Create tables that specify hello structure, location, and availability of hello datasets with hello following script-based procedures.</span></span> <span data-ttu-id="7b915-185">Fichiers JSON sont des tables de hello toodefine utilisé.</span><span class="sxs-lookup"><span data-stu-id="7b915-185">JSON files are used toodefine hello tables.</span></span> <span data-ttu-id="7b915-186">Pour plus d’informations sur la structure hello de ces fichiers, consultez [jeux de données](../data-factory/data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="7b915-186">For more information on hello structure of these files, see [Datasets](../data-factory/data-factory-create-datasets.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7b915-187">Vous devez exécuter hello `Add-AzureAccount` applet de commande avant d’exécuter hello [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) tooconfirm d’applet de commande qui hello abonnement Azure à droite est sélectionné pour l’exécution de la commande hello.</span><span class="sxs-lookup"><span data-stu-id="7b915-187">You should execute hello `Add-AzureAccount` cmdlet before executing hello [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet tooconfirm that hello right Azure subscription is selected for hello command execution.</span></span> <span data-ttu-id="7b915-188">Pour obtenir la documentation de cette applet de commande, consultez [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="7b915-188">For documentation of this cmdlet, see [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span></span>
>
>

<span data-ttu-id="7b915-189">définitions Hello JSON dans les tables de hello utilisent hello nom :</span><span class="sxs-lookup"><span data-stu-id="7b915-189">hello JSON-based definitions in hello tables use hello following names:</span></span>

* <span data-ttu-id="7b915-190">Hello **nom de la table** Bonjour local SQL server est *nyctaxi_data*</span><span class="sxs-lookup"><span data-stu-id="7b915-190">hello **table name** in hello on-premises SQL server is *nyctaxi_data*</span></span>
* <span data-ttu-id="7b915-191">Hello **nom du conteneur** Bonjour Azure Blob Storage est compte *containername*</span><span class="sxs-lookup"><span data-stu-id="7b915-191">hello **container name** in hello Azure Blob Storage account is *containername*</span></span>  

<span data-ttu-id="7b915-192">Trois définitions de table sont nécessaires pour ce pipeline ADF :</span><span class="sxs-lookup"><span data-stu-id="7b915-192">Three table definitions are needed for this ADF pipeline:</span></span>

1. [<span data-ttu-id="7b915-193">Table SQL locale</span><span class="sxs-lookup"><span data-stu-id="7b915-193">SQL on-premises Table</span></span>](#adf-table-onprem-sql)
2. [<span data-ttu-id="7b915-194">Table d'objets blob </span><span class="sxs-lookup"><span data-stu-id="7b915-194">Blob Table </span></span>](#adf-table-blob-store)
3. [<span data-ttu-id="7b915-195">Table SQL Azure</span><span class="sxs-lookup"><span data-stu-id="7b915-195">SQL Azure Table</span></span>](#adf-table-azure-sql)

> [!NOTE]
> <span data-ttu-id="7b915-196">Ces procédures utilisent Azure PowerShell toodefine et créer des activités ADF hello.</span><span class="sxs-lookup"><span data-stu-id="7b915-196">These procedures use Azure PowerShell toodefine and create hello ADF activities.</span></span> <span data-ttu-id="7b915-197">Mais ces tâches peuvent également être accomplies à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7b915-197">But these tasks can also be accomplished using hello Azure portal.</span></span> <span data-ttu-id="7b915-198">Pour plus d’informations, consultez [Créer des jeux de données](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span><span class="sxs-lookup"><span data-stu-id="7b915-198">For details, see [Create datasets](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span></span>
>
>

### <span data-ttu-id="7b915-199"><a name="adf-table-onprem-sql"></a>Table SQL locale</span><span class="sxs-lookup"><span data-stu-id="7b915-199"><a name="adf-table-onprem-sql"></a>SQL on-premises Table</span></span>
<span data-ttu-id="7b915-200">définition de la table Hello pour hello local SQL Server est spécifié dans hello le fichier JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="7b915-200">hello table definition for hello on-premises SQL Server is specified in hello following JSON file:</span></span>

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

<span data-ttu-id="7b915-201">les noms de colonne Hello n’étaient pas inclus ici.</span><span class="sxs-lookup"><span data-stu-id="7b915-201">hello column names were not included here.</span></span> <span data-ttu-id="7b915-202">Vous pouvez sélectionner des noms de colonne hello en les incluant ici (pour plus d’informations, consultez hello [documentation d’ADF](../data-factory/data-factory-data-movement-activities.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="7b915-202">You can sub-select on hello column names by including them here (for details check hello [ADF documentation](../data-factory/data-factory-data-movement-activities.md) topic.</span></span>

<span data-ttu-id="7b915-203">Copier la définition de JSON hello de table de hello dans un fichier appelé *onpremtabledef.json* de fichier et l’enregistrer tooa connus d’emplacement (ici supposé toobe *C:\temp\onpremtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="7b915-203">Copy hello JSON definition of hello table into a file called *onpremtabledef.json* file and save it tooa known location (here assumed toobe *C:\temp\onpremtabledef.json*).</span></span> <span data-ttu-id="7b915-204">Créer les table hello dans ADF par hello suivant l’applet de commande PowerShell de Azure :</span><span class="sxs-lookup"><span data-stu-id="7b915-204">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <span data-ttu-id="7b915-205"><a name="adf-table-blob-store"></a>Table d'objets blob</span><span class="sxs-lookup"><span data-stu-id="7b915-205"><a name="adf-table-blob-store"></a>Blob Table</span></span>
<span data-ttu-id="7b915-206">Définition de table hello pour hello de sortie blob emplacement est suivante hello (cela mappe les données de hello ingéré à partir de l’objet blob de tooAzure local) :</span><span class="sxs-lookup"><span data-stu-id="7b915-206">Definition for hello table for hello output blob location is in hello following (this maps hello ingested data from on-premises tooAzure blob):</span></span>

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

<span data-ttu-id="7b915-207">Copier la définition de JSON hello de table de hello dans un fichier appelé *bloboutputtabledef.json* de fichier et l’enregistrer tooa connus d’emplacement (ici supposé toobe *C:\temp\bloboutputtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="7b915-207">Copy hello JSON definition of hello table into a file called *bloboutputtabledef.json* file and save it tooa known location (here assumed toobe *C:\temp\bloboutputtabledef.json*).</span></span> <span data-ttu-id="7b915-208">Créer les table hello dans ADF par hello suivant l’applet de commande PowerShell de Azure :</span><span class="sxs-lookup"><span data-stu-id="7b915-208">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <span data-ttu-id="7b915-209"><a name="adf-table-azure-sq"></a>Table SQL Azure</span><span class="sxs-lookup"><span data-stu-id="7b915-209"><a name="adf-table-azure-sq"></a>SQL Azure Table</span></span>
<span data-ttu-id="7b915-210">Définition de table hello pour hello de sortie SQL Azure est suivante hello (ce schéma mappe les données hello provenant d’un objet blob de hello) :</span><span class="sxs-lookup"><span data-stu-id="7b915-210">Definition for hello table for hello SQL Azure output is in hello following (this schema maps hello data coming from hello blob):</span></span>

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

<span data-ttu-id="7b915-211">Copier la définition de JSON hello de table de hello dans un fichier appelé *AzureSqlTable.json* de fichier et l’enregistrer tooa connus d’emplacement (ici supposé toobe *C:\temp\AzureSqlTable.json*).</span><span class="sxs-lookup"><span data-stu-id="7b915-211">Copy hello JSON definition of hello table into a file called *AzureSqlTable.json* file and save it tooa known location (here assumed toobe *C:\temp\AzureSqlTable.json*).</span></span> <span data-ttu-id="7b915-212">Créer les table hello dans ADF par hello suivant l’applet de commande PowerShell de Azure :</span><span class="sxs-lookup"><span data-stu-id="7b915-212">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <span data-ttu-id="7b915-213"><a name="adf-pipeline"></a>Définir et créer le pipeline de hello</span><span class="sxs-lookup"><span data-stu-id="7b915-213"><a name="adf-pipeline"></a>Define and create hello pipeline</span></span>
<span data-ttu-id="7b915-214">Spécifiez les activités de hello appartenant toohello de pipeline et créer un pipeline de hello avec hello script basé sur les procédures suivantes.</span><span class="sxs-lookup"><span data-stu-id="7b915-214">Specify hello activities that belong toohello pipeline and create hello pipeline with hello following script-based procedures.</span></span> <span data-ttu-id="7b915-215">Un fichier JSON est propriétés de pipeline utilisé toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="7b915-215">A JSON file is used toodefine hello pipeline properties.</span></span>

* <span data-ttu-id="7b915-216">Hello script suppose que hello **nom du pipeline** est *AMLDSProcessPipeline*.</span><span class="sxs-lookup"><span data-stu-id="7b915-216">hello script assumes that hello **pipeline name** is *AMLDSProcessPipeline*.</span></span>
* <span data-ttu-id="7b915-217">Notez également que nous périodicité hello de hello pipeline toobe est exécutée sur tous les jours base et utilisez hello durée par défaut d’exécution pour le travail hello (0 h 00 UTC).</span><span class="sxs-lookup"><span data-stu-id="7b915-217">Also note that we set hello periodicity of hello pipeline toobe executed on daily basis and use hello default execution time for hello job (12 am UTC).</span></span>

> [!NOTE]
> <span data-ttu-id="7b915-218">Bonjour procédures suivantes utilisent Azure PowerShell toodefine et créer hello ADF pipeline.</span><span class="sxs-lookup"><span data-stu-id="7b915-218">hello following procedures use Azure PowerShell toodefine and create hello ADF pipeline.</span></span> <span data-ttu-id="7b915-219">Toutefois, cette tâche peut également être accomplie à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7b915-219">But this task can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="7b915-220">Pour plus d’informations, consultez [Création d’un pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span><span class="sxs-lookup"><span data-stu-id="7b915-220">For details, see [Create pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span></span>
>
>

<span data-ttu-id="7b915-221">À l’aide des définitions de table hello fournies précédemment, définition de pipeline hello pour hello QU'ADF est spécifiée comme suit :</span><span class="sxs-lookup"><span data-stu-id="7b915-221">Using hello table definitions provided previously, hello pipeline definition for hello ADF is specified as follows:</span></span>

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL tooAzure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server tooblob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data tooSql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

<span data-ttu-id="7b915-222">Copiez cette définition JSON de pipeline de hello dans un fichier appelé *pipelinedef.json* de fichier et l’enregistrer tooa connus d’emplacement (ici supposé toobe *C:\temp\pipelinedef.json*).</span><span class="sxs-lookup"><span data-stu-id="7b915-222">Copy this JSON definition of hello pipeline into a file called *pipelinedef.json* file and save it tooa known location (here assumed toobe *C:\temp\pipelinedef.json*).</span></span> <span data-ttu-id="7b915-223">Créer le pipeline de hello dans ADF avec hello suivant l’applet de commande PowerShell de Azure :</span><span class="sxs-lookup"><span data-stu-id="7b915-223">Create hello pipeline in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

<span data-ttu-id="7b915-224">Vérifiez que vous pouvez voir les pipeline hello sur hello ADF Bonjour portail classique Azure s’affichent comme suit (si vous cliquez sur le diagramme de hello)</span><span class="sxs-lookup"><span data-stu-id="7b915-224">Confirm that you can see hello pipeline on hello ADF in hello Azure Classic Portal show up as following (when you click hello diagram)</span></span>

![Pipeline ADF](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <span data-ttu-id="7b915-226"><a name="adf-pipeline-start"></a>Démarrer hello Pipeline</span><span class="sxs-lookup"><span data-stu-id="7b915-226"><a name="adf-pipeline-start"></a>Start hello Pipeline</span></span>
<span data-ttu-id="7b915-227">pipeline de Hello peut maintenant être exécuté à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7b915-227">hello pipeline can now be run using hello following command:</span></span>

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

<span data-ttu-id="7b915-228">Hello *startdate* et *enddate* toobe remplacée par les dates réelles hello entre lesquels vous souhaitez hello pipeline toorun est nécessaire que les valeurs de paramètre.</span><span class="sxs-lookup"><span data-stu-id="7b915-228">hello *startdate* and *enddate* parameter values need toobe replaced with hello actual dates between which you want hello pipeline toorun.</span></span>

<span data-ttu-id="7b915-229">Une fois que le pipeline de hello s’exécute, vous devez être en mesure de toosee hello données qui s’affichent dans le conteneur hello sélectionné pour l’objet blob hello, un seul fichier par jour.</span><span class="sxs-lookup"><span data-stu-id="7b915-229">Once hello pipeline executes, you should be able toosee hello data show up in hello container selected for hello blob, one file per day.</span></span>

<span data-ttu-id="7b915-230">Notez que nous n’avons pas réutilisé fonctionnalité hello fournie par les données de toopipe ADF incrémentielle.</span><span class="sxs-lookup"><span data-stu-id="7b915-230">Note that we have not leveraged hello functionality provided by ADF toopipe data incrementally.</span></span> <span data-ttu-id="7b915-231">Pour plus d’informations sur comment toodo cela et autres fonctionnalités fournies par le chargeur automatique, consultez hello [documentation d’ADF](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="7b915-231">For more information on how toodo this and other capabilities provided by ADF, see hello [ADF documentation](https://azure.microsoft.com/services/data-factory/).</span></span>
