---
title: "Déplacement de données à partir d’un serveur SQL local vers SQL Azure avec Azure Data Factory | Microsoft Docs"
description: "Configuration d’un pipeline ADF composé de deux activités de migration des données qui déplacent quotidiennement les données entre des bases de données locales et sur le cloud."
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
ms.openlocfilehash: 39fe26d3388be8b558f05063a8965889c013a41e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-from-an-on-premises-sql-server-to-sql-azure-with-azure-data-factory"></a><span data-ttu-id="55cae-103">Déplacement de données à partir d’un serveur SQL local vers SQL Azure avec Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="55cae-103">Move data from an on-premises SQL server to SQL Azure with Azure Data Factory</span></span>
<span data-ttu-id="55cae-104">Cette rubrique montre comment déplacer des données d’une base de données SQL Server locale vers une base de données SQL Azure via le stockage d’objets blob Azure à l’aide d’Azure Data Factory (ADF).</span><span class="sxs-lookup"><span data-stu-id="55cae-104">This topic shows how to move data from an on-premises SQL Server Database to a SQL Azure Database via Azure Blob Storage using the Azure Data Factory (ADF).</span></span>

<span data-ttu-id="55cae-105">Pour accéder à un tableau résumant les différentes options de déplacement de données dans une base de données SQL Azure, consultez [Déplacer des données dans une base de données SQL Azure pour Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="55cae-105">For a table that summarizes various options for moving data to an Azure SQL Database, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

## <span data-ttu-id="55cae-106"><a name="intro"></a>Présentation : Qu’est-ce qu’ADF et quand doit-il être utilisé pour migrer des données ?</span><span class="sxs-lookup"><span data-stu-id="55cae-106"><a name="intro"></a>Introduction: What is ADF and when should it be used to migrate data?</span></span>
<span data-ttu-id="55cae-107">Azure Data Factory est un service d’intégration de données dans le cloud entièrement géré qui gère et automatise le déplacement et la transformation des données.</span><span class="sxs-lookup"><span data-stu-id="55cae-107">Azure Data Factory is a fully managed cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="55cae-108">Le concept clé du modèle ADF est le pipeline.</span><span class="sxs-lookup"><span data-stu-id="55cae-108">The key concept in the ADF model is pipeline.</span></span> <span data-ttu-id="55cae-109">Un pipeline est un regroupement logique d’activités, chacune d'elles définissant les actions à effectuer sur les données contenues dans des groupes de données.</span><span class="sxs-lookup"><span data-stu-id="55cae-109">A pipeline is a logical grouping of Activities, each of which defines the actions to perform on the data contained in Datasets.</span></span> <span data-ttu-id="55cae-110">Les services liés sont utilisés pour définir les informations nécessaires à Data Factory pour se connecter à des ressources de données.</span><span class="sxs-lookup"><span data-stu-id="55cae-110">Linked services are used to define the information needed for Data Factory to connect to the data resources.</span></span>

<span data-ttu-id="55cae-111">Avec ADF, les services de traitement de données existants peuvent être composés dans des pipelines de données, à disponibilité élevée et gérés dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="55cae-111">With ADF, existing data processing services can be composed into data pipelines that are highly available and managed in the cloud.</span></span> <span data-ttu-id="55cae-112">Ces pipelines de données peuvent être soumis à planification pour la réception, la préparation, la transformation, l’analyse et la publication de données. ADF gère et orchestre les données et les dépendances de traitement complexes.</span><span class="sxs-lookup"><span data-stu-id="55cae-112">These data pipelines can be scheduled to ingest, prepare, transform, analyze, and publish data, and ADF manages and orchestrates the complex data and processing dependencies.</span></span> <span data-ttu-id="55cae-113">Les solutions peuvent être rapidement créées et déployées dans le cloud, afin de connecter un nombre croissant de sources de données locales et cloud.</span><span class="sxs-lookup"><span data-stu-id="55cae-113">Solutions can be quickly built and deployed in the cloud, connecting a growing number of on-premises and cloud data sources.</span></span>

<span data-ttu-id="55cae-114">Utilisez plutôt ADF :</span><span class="sxs-lookup"><span data-stu-id="55cae-114">Consider using ADF:</span></span>

* <span data-ttu-id="55cae-115">lorsque les données doivent être migrées en permanence dans un scénario hybride qui accède à la fois aux ressources locales et cloud ;</span><span class="sxs-lookup"><span data-stu-id="55cae-115">when data needs to be continually migrated in a hybrid scenario that accesses both on-premises and cloud resources</span></span>
* <span data-ttu-id="55cae-116">lorsque les données sont traitées ou doivent être modifiées ou complétées par une logique métier lors de leur migration.</span><span class="sxs-lookup"><span data-stu-id="55cae-116">when the data is transacted or needs to be modified or have business logic added to it when being migrated.</span></span>

<span data-ttu-id="55cae-117">ADF permet la planification et la surveillance des travaux à l'aide de scripts JSON simples qui gèrent le déplacement des données sur une base périodique.</span><span class="sxs-lookup"><span data-stu-id="55cae-117">ADF allows for the scheduling and monitoring of jobs using simple JSON scripts that manage the movement of data on a periodic basis.</span></span> <span data-ttu-id="55cae-118">ADF dispose également d'autres fonctionnalités comme la prise en charge des opérations complexes.</span><span class="sxs-lookup"><span data-stu-id="55cae-118">ADF also has other capabilities such as support for complex operations.</span></span> <span data-ttu-id="55cae-119">Pour plus d'informations sur ADF, consultez la documentation relative à [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="55cae-119">For more information on ADF, see the documentation at [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span></span>

## <span data-ttu-id="55cae-120"><a name="scenario"></a>Scénario</span><span class="sxs-lookup"><span data-stu-id="55cae-120"><a name="scenario"></a>The Scenario</span></span>
<span data-ttu-id="55cae-121">Nous allons configurer un pipeline ADF qui se compose de deux activités de migration de données.</span><span class="sxs-lookup"><span data-stu-id="55cae-121">We set up an ADF pipeline that composes two data migration activities.</span></span> <span data-ttu-id="55cae-122">Ensemble, ces activités déplacent les données quotidiennement entre une base de données SQL locale et une base de données Azure SQL dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="55cae-122">Together they move data on a daily basis between an on-premises SQL database and an Azure SQL Database in the cloud.</span></span> <span data-ttu-id="55cae-123">Les deux activités sont :</span><span class="sxs-lookup"><span data-stu-id="55cae-123">The two activities are:</span></span>

* <span data-ttu-id="55cae-124">copie de données depuis une base de données SQL Server locale vers un compte de stockage d’objets blob Azure ;</span><span class="sxs-lookup"><span data-stu-id="55cae-124">copy data from an on-premises SQL Server database to an Azure Blob Storage account</span></span>
* <span data-ttu-id="55cae-125">copie de données à partir du compte de stockage d'objets blob Azure vers une base de données Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="55cae-125">copy data from the Azure Blob Storage account to an Azure SQL Database.</span></span>

> [!NOTE]
> <span data-ttu-id="55cae-126">Les étapes présentées ici ont été adaptées du didacticiel plus détaillé [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) , fourni par l’équipe ADF, et des références aux sections appropriées de cette rubrique sont fournies quand cela s’avère approprié.</span><span class="sxs-lookup"><span data-stu-id="55cae-126">The steps shown here have been adapted from the more detailed tutorial provided by the ADF team: [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) References to the relevant sections of that topic are provided when appropriate.</span></span>
>
>

## <span data-ttu-id="55cae-127"><a name="prereqs"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="55cae-127"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="55cae-128">Ce didacticiel part du principe que vous disposez de :</span><span class="sxs-lookup"><span data-stu-id="55cae-128">This tutorial assumes you have:</span></span>

* <span data-ttu-id="55cae-129">Un **abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="55cae-129">An **Azure subscription**.</span></span> <span data-ttu-id="55cae-130">Si vous n’avez pas d’abonnement, vous pouvez vous inscrire à un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="55cae-130">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="55cae-131">Un **compte de stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="55cae-131">An **Azure storage account**.</span></span> <span data-ttu-id="55cae-132">Dans ce didacticiel, vous utilisez un compte de stockage Azure pour stocker des données.</span><span class="sxs-lookup"><span data-stu-id="55cae-132">You use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="55cae-133">Si vous ne possédez pas de compte de stockage Azure, consultez l’article [Créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) .</span><span class="sxs-lookup"><span data-stu-id="55cae-133">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="55cae-134">Après avoir créé le compte de stockage, vous devez obtenir la clé du compte utilisée pour accéder au stockage.</span><span class="sxs-lookup"><span data-stu-id="55cae-134">After you have created the storage account, you need to obtain the account key used to access the storage.</span></span> <span data-ttu-id="55cae-135">Voir [Gérer vos clés d’accès de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="55cae-135">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="55cae-136">Un accès à une **base de données Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="55cae-136">Access to an **Azure SQL Database**.</span></span> <span data-ttu-id="55cae-137">Si vous devez configurer une base de données Azure SQL Database, l’article [Bien démarrer avec Microsoft Azure SQL Database](../sql-database/sql-database-get-started.md) fournit des informations sur la configuration d’une nouvelle instance de base de données Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="55cae-137">If you must set up an Azure SQL Database, the tpoic [Getting Started with Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) provides information on how to provision a new instance of an Azure SQL Database.</span></span>
* <span data-ttu-id="55cae-138">**Azure PowerShell** installé et configuré localement.</span><span class="sxs-lookup"><span data-stu-id="55cae-138">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="55cae-139">Pour obtenir des instructions, consultez la rubrique [Installation et configuration d'Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="55cae-139">For instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!NOTE]
> <span data-ttu-id="55cae-140">Cette procédure utilise le [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="55cae-140">This procedure uses the [Azure portal](https://portal.azure.com/).</span></span>
>
>

## <span data-ttu-id="55cae-141"><a name="upload-data"></a> Téléchargement des données sur votre SQL Server local</span><span class="sxs-lookup"><span data-stu-id="55cae-141"><a name="upload-data"></a> Upload the data to your on-premises SQL Server</span></span>
<span data-ttu-id="55cae-142">Nous utilisons le [jeu de données NYC Taxi](http://chriswhong.com/open-data/foil_nyc_taxi/) pour illustrer le processus de migration.</span><span class="sxs-lookup"><span data-stu-id="55cae-142">We use the [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) to demonstrate the migration process.</span></span> <span data-ttu-id="55cae-143">Le jeu de données NYC Taxi est disponible, comme mentionné dans cet article, sur Azure Blob Storage [données NYC Taxi](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="55cae-143">The NYC Taxi dataset is available, as noted in that post, on Azure blob storage [NYC Taxi Data](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="55cae-144">Les données comprennent deux fichiers : le fichier trip_data.csv qui contient les détails de voyage et le fichier trip_far.csv qui contient les détails des prix payés pour chaque voyage.</span><span class="sxs-lookup"><span data-stu-id="55cae-144">The data has two files, the trip_data.csv file, which contains trip details, and the  trip_far.csv file, which contains details of the fare paid for each trip.</span></span> <span data-ttu-id="55cae-145">Un échantillon et une description de ces fichiers sont fournis dans la [description du jeu de données des voyages NYC Taxi](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span><span class="sxs-lookup"><span data-stu-id="55cae-145">A sample and description of these files are provided in [NYC Taxi Trips Dataset Description](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span></span>

<span data-ttu-id="55cae-146">Vous pouvez adapter les procédures fournies ici à un jeu de vos propres données ou suivre les étapes décrites à l'aide du jeu de données NYC Taxi.</span><span class="sxs-lookup"><span data-stu-id="55cae-146">You can either adapt the procedure provided here to a set of your own data or follow the steps as described by using the NYC Taxi dataset.</span></span> <span data-ttu-id="55cae-147">Pour télécharger le jeu de données NYC Taxi dans votre base de données SQL Server locale, suivez la procédure décrite dans [Importer des données en bloc dans SQL Server Database](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span><span class="sxs-lookup"><span data-stu-id="55cae-147">To upload the NYC Taxi dataset into your on-premises SQL Server database, follow the procedure outlined in [Bulk Import Data into SQL Server Database](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span></span> <span data-ttu-id="55cae-148">Ces instructions concernent un SQL Server sur une machine virtuelle Azure, mais la procédure de téléchargement vers le serveur local SQL Server est la même.</span><span class="sxs-lookup"><span data-stu-id="55cae-148">These instructions are for a SQL Server on an Azure Virtual Machine, but the procedure for uploading to the on-premises SQL Server is the same.</span></span>

## <span data-ttu-id="55cae-149"><a name="create-adf"></a> Création d’une Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="55cae-149"><a name="create-adf"></a> Create an Azure Data Factory</span></span>
<span data-ttu-id="55cae-150">Les instructions pour la création d’une fabrique de données Azure Data Factory et d’un groupe de ressources dans le [portail Azure](https://portal.azure.com/) sont fournies dans [Créer une fabrique de données Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span><span class="sxs-lookup"><span data-stu-id="55cae-150">The instructions for creating a new Azure Data Factory and a resource group in the [Azure portal](https://portal.azure.com/) are provided [Create an Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span></span> <span data-ttu-id="55cae-151">Nommez la nouvelle instance ADF *adfdsp* et nommez le groupe de ressources créé *adfdsprg*.</span><span class="sxs-lookup"><span data-stu-id="55cae-151">Name the new ADF instance *adfdsp* and name the resource group created *adfdsprg*.</span></span>

## <a name="install-and-configure-up-the-data-management-gateway"></a><span data-ttu-id="55cae-152">Installez et configurez la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="55cae-152">Install and configure up the Data Management Gateway</span></span>
<span data-ttu-id="55cae-153">Pour permettre à vos pipelines d’une fabrique de données Azure de fonctionner avec un SQL Server local, vous devez les ajouter en tant que service lié.</span><span class="sxs-lookup"><span data-stu-id="55cae-153">To enable your pipelines in an Azure data factory to work with an on-premises SQL Server, you need to add it as a Linked Service to the data factory.</span></span> <span data-ttu-id="55cae-154">Pour créer un service lié pour un serveur SQL Server local, vous devez :</span><span class="sxs-lookup"><span data-stu-id="55cae-154">To create a Linked Service for an on-premises SQL Server, you must:</span></span>

* <span data-ttu-id="55cae-155">télécharger et installer la passerelle de gestion des données Microsoft sur l’ordinateur local ;</span><span class="sxs-lookup"><span data-stu-id="55cae-155">download and install Microsoft Data Management Gateway onto the on-premises computer.</span></span>
* <span data-ttu-id="55cae-156">configurer le service lié pour la source de données locale afin d’utiliser la passerelle.</span><span class="sxs-lookup"><span data-stu-id="55cae-156">configure the linked service for the on-premises data source to use the gateway.</span></span>

<span data-ttu-id="55cae-157">La passerelle de gestion des données sérialise et désérialise les données sources et de récepteur sur l'ordinateur sur lequel elles sont hébergées.</span><span class="sxs-lookup"><span data-stu-id="55cae-157">The Data Management Gateway serializes and deserializes the source and sink data on the computer where it is hosted.</span></span>

<span data-ttu-id="55cae-158">Pour obtenir des détails et des instructions d’installation sur la passerelle de gestion des données, consultez [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="55cae-158">For set-up instructions and details on Data Management Gateway, see [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span></span>

## <span data-ttu-id="55cae-159"><a name="adflinkedservices"></a>Création de services liés pour la connexion aux ressources de données</span><span class="sxs-lookup"><span data-stu-id="55cae-159"><a name="adflinkedservices"></a>Create linked services to connect to the data resources</span></span>
<span data-ttu-id="55cae-160">Un service lié définit les informations nécessaires à Azure Data Factory pour se connecter à des ressources de données.</span><span class="sxs-lookup"><span data-stu-id="55cae-160">A linked service defines the information needed for Azure Data Factory to connect to a data resource.</span></span> <span data-ttu-id="55cae-161">La procédure pas à pas pour la création de services liés est fournie dans [Créer des services liés](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span><span class="sxs-lookup"><span data-stu-id="55cae-161">The step-by-step procedure for creating linked services is provided in [Create linked services](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span></span>

<span data-ttu-id="55cae-162">Dans ce scénario, nous avons trois ressources pour lesquelles les services liés sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="55cae-162">We have three resources in this scenario for which linked services are needed.</span></span>

1. [<span data-ttu-id="55cae-163">Service lié pour SQL Server local</span><span class="sxs-lookup"><span data-stu-id="55cae-163">Linked service for on-premises SQL Server</span></span>](#adf-linked-service-onprem-sql)
2. [<span data-ttu-id="55cae-164">Service lié pour Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="55cae-164">Linked service for Azure Blob Storage</span></span>](#adf-linked-service-blob-store)
3. [<span data-ttu-id="55cae-165">Service lié pour base de données Azure SQL</span><span class="sxs-lookup"><span data-stu-id="55cae-165">Linked service for Azure SQL database</span></span>](#adf-linked-service-azure-sql)

### <span data-ttu-id="55cae-166"><a name="adf-linked-service-onprem-sql"></a>Service lié pour base de données SQL Server locale</span><span class="sxs-lookup"><span data-stu-id="55cae-166"><a name="adf-linked-service-onprem-sql"></a>Linked service for on-premises SQL Server database</span></span>
<span data-ttu-id="55cae-167">Pour créer un service lié pour le serveur SQL Server local :</span><span class="sxs-lookup"><span data-stu-id="55cae-167">To create the linked service for the on-premises SQL Server:</span></span>

* <span data-ttu-id="55cae-168">Cliquez sur le **magasin de données** dans la page d’accueil ADF du portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="55cae-168">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="55cae-169">Sélectionnez **SQL**, puis entrez le *nom d’utilisateur* et le *mot de passe* du serveur SQL local.</span><span class="sxs-lookup"><span data-stu-id="55cae-169">select **SQL** and enter the *username* and *password* credentials for the on-premises SQL Server.</span></span> <span data-ttu-id="55cae-170">Vous devez entrer le nom du serveur sous la forme d’un **nom d’instance avec barre oblique inverse et nom de serveur entièrement qualifié (nomserveur\nominstance)**.</span><span class="sxs-lookup"><span data-stu-id="55cae-170">You need to enter the servername as a **fully qualified servername backslash instance name (servername\instancename)**.</span></span> <span data-ttu-id="55cae-171">Nommez le service lié *adfonpremsql*.</span><span class="sxs-lookup"><span data-stu-id="55cae-171">Name the linked service *adfonpremsql*.</span></span>

### <span data-ttu-id="55cae-172"><a name="adf-linked-service-blob-store"></a>Service lié pour les objets blob</span><span class="sxs-lookup"><span data-stu-id="55cae-172"><a name="adf-linked-service-blob-store"></a>Linked service for Blob</span></span>
<span data-ttu-id="55cae-173">Pour créer un service lié pour le compte de stockage d’objets Blob Azure :</span><span class="sxs-lookup"><span data-stu-id="55cae-173">To create the linked service for the Azure Blob Storage account:</span></span>

* <span data-ttu-id="55cae-174">Cliquez sur le **magasin de données** dans la page d’accueil ADF du portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="55cae-174">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="55cae-175">Sélectionnez **Azure Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="55cae-175">select **Azure Storage Account**</span></span>
* <span data-ttu-id="55cae-176">Entrez la clé et le nom de conteneur du compte de stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="55cae-176">enter the Azure Blob Storage account key and container name.</span></span> <span data-ttu-id="55cae-177">Nommez le service lié *adfds*.</span><span class="sxs-lookup"><span data-stu-id="55cae-177">Name the Linked Service *adfds*.</span></span>

### <span data-ttu-id="55cae-178"><a name="adf-linked-service-azure-sql"></a>Service lié pour la base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="55cae-178"><a name="adf-linked-service-azure-sql"></a>Linked service for Azure SQL database</span></span>
<span data-ttu-id="55cae-179">Pour créer le service lié pour la base de données SQL Azure :</span><span class="sxs-lookup"><span data-stu-id="55cae-179">To create the linked service for the Azure SQL Database:</span></span>

* <span data-ttu-id="55cae-180">Cliquez sur le **magasin de données** dans la page d’accueil ADF du portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="55cae-180">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="55cae-181">Sélectionnez **Azure SQL**, puis entrez le *nom d’utilisateur* et le *mot de passe* de la base de données Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="55cae-181">select **Azure SQL** and enter the *username* and *password* credentials for the Azure SQL Database.</span></span> <span data-ttu-id="55cae-182">Le *nom d’utilisateur* doit être spécifié en tant que *user@servername*.</span><span class="sxs-lookup"><span data-stu-id="55cae-182">The *username* must be specified as *user@servername*.</span></span>   

## <span data-ttu-id="55cae-183"><a name="adf-tables"></a>Définir et créer des tables pour spécifier l’accès aux jeux de données</span><span class="sxs-lookup"><span data-stu-id="55cae-183"><a name="adf-tables"></a>Define and create tables to specify how to access the datasets</span></span>
<span data-ttu-id="55cae-184">Créez des tables qui spécifient la structure, l'emplacement et la disponibilité des jeux de données avec les procédures reposant sur des scripts suivantes.</span><span class="sxs-lookup"><span data-stu-id="55cae-184">Create tables that specify the structure, location, and availability of the datasets with the following script-based procedures.</span></span> <span data-ttu-id="55cae-185">Les fichiers JSON sont utilisés pour définir les tables.</span><span class="sxs-lookup"><span data-stu-id="55cae-185">JSON files are used to define the tables.</span></span> <span data-ttu-id="55cae-186">Pour plus d'informations sur la structure de ces fichiers, consultez [Jeux de données](../data-factory/data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="55cae-186">For more information on the structure of these files, see [Datasets](../data-factory/data-factory-create-datasets.md).</span></span>

> [!NOTE]
> <span data-ttu-id="55cae-187">Vous devez exécuter l’applet de commande `Add-AzureAccount` avant d’exécuter l’applet de commande [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx), afin de vérifier que l’abonnement Azure approprié est sélectionné pour l’exécution de la commande.</span><span class="sxs-lookup"><span data-stu-id="55cae-187">You should execute the `Add-AzureAccount` cmdlet before executing the [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet to confirm that the right Azure subscription is selected for the command execution.</span></span> <span data-ttu-id="55cae-188">Pour obtenir la documentation de cette applet de commande, consultez [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="55cae-188">For documentation of this cmdlet, see [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span></span>
>
>

<span data-ttu-id="55cae-189">Les définitions reposant sur JSON dans les tables utilisent les noms suivants :</span><span class="sxs-lookup"><span data-stu-id="55cae-189">The JSON-based definitions in the tables use the following names:</span></span>

* <span data-ttu-id="55cae-190">Le **nom de table** sur le serveur SQL local est *nyctaxi_data*</span><span class="sxs-lookup"><span data-stu-id="55cae-190">the **table name** in the on-premises SQL server is *nyctaxi_data*</span></span>
* <span data-ttu-id="55cae-191">the **nom de conteneur** dans le compte de stockage d’objets blob Azure est *containername*</span><span class="sxs-lookup"><span data-stu-id="55cae-191">the **container name** in the Azure Blob Storage account is *containername*</span></span>  

<span data-ttu-id="55cae-192">Trois définitions de table sont nécessaires pour ce pipeline ADF :</span><span class="sxs-lookup"><span data-stu-id="55cae-192">Three table definitions are needed for this ADF pipeline:</span></span>

1. [<span data-ttu-id="55cae-193">Table SQL locale</span><span class="sxs-lookup"><span data-stu-id="55cae-193">SQL on-premises Table</span></span>](#adf-table-onprem-sql)
2. [<span data-ttu-id="55cae-194">Table d'objets blob </span><span class="sxs-lookup"><span data-stu-id="55cae-194">Blob Table </span></span>](#adf-table-blob-store)
3. [<span data-ttu-id="55cae-195">Table SQL Azure</span><span class="sxs-lookup"><span data-stu-id="55cae-195">SQL Azure Table</span></span>](#adf-table-azure-sql)

> [!NOTE]
> <span data-ttu-id="55cae-196">Ces procédures utilisent Azure PowerShell pour définir et créer les activités ADF.</span><span class="sxs-lookup"><span data-stu-id="55cae-196">These procedures use Azure PowerShell to define and create the ADF activities.</span></span> <span data-ttu-id="55cae-197">Toutefois, ces tâches peuvent également être accomplies à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="55cae-197">But these tasks can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="55cae-198">Pour plus d’informations, consultez [Créer des jeux de données](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span><span class="sxs-lookup"><span data-stu-id="55cae-198">For details, see [Create datasets](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span></span>
>
>

### <span data-ttu-id="55cae-199"><a name="adf-table-onprem-sql"></a>Table SQL locale</span><span class="sxs-lookup"><span data-stu-id="55cae-199"><a name="adf-table-onprem-sql"></a>SQL on-premises Table</span></span>
<span data-ttu-id="55cae-200">La définition de table pour le SQL Server local est spécifié dans le fichier JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="55cae-200">The table definition for the on-premises SQL Server is specified in the following JSON file:</span></span>

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

<span data-ttu-id="55cae-201">Les noms de colonnes n’étaient pas inclus ici.</span><span class="sxs-lookup"><span data-stu-id="55cae-201">The column names were not included here.</span></span> <span data-ttu-id="55cae-202">Vous pouvez sélectionner des noms de colonnes en les incluant ici (pour plus d’informations, consultez la rubrique [documentation ADF](../data-factory/data-factory-data-movement-activities.md) ).</span><span class="sxs-lookup"><span data-stu-id="55cae-202">You can sub-select on the column names by including them here (for details check the [ADF documentation](../data-factory/data-factory-data-movement-activities.md) topic.</span></span>

<span data-ttu-id="55cae-203">Copiez la définition JSON de la table dans un fichier appelé *onpremtabledef.json* et enregistrez-le dans un emplacement connu (ici supposé comme étant *C:\temp\onpremtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="55cae-203">Copy the JSON definition of the table into a file called *onpremtabledef.json* file and save it to a known location (here assumed to be *C:\temp\onpremtabledef.json*).</span></span> <span data-ttu-id="55cae-204">Créez la table dans ADF avec la cmdlet Azure PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="55cae-204">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <span data-ttu-id="55cae-205"><a name="adf-table-blob-store"></a>Table d'objets blob</span><span class="sxs-lookup"><span data-stu-id="55cae-205"><a name="adf-table-blob-store"></a>Blob Table</span></span>
<span data-ttu-id="55cae-206">La définition de la table pour l’emplacement d’objets blob de sortie est la suivante (cela mappe les données ingérées localement vers un objet blob Azure) :</span><span class="sxs-lookup"><span data-stu-id="55cae-206">Definition for the table for the output blob location is in the following (this maps the ingested data from on-premises to Azure blob):</span></span>

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

<span data-ttu-id="55cae-207">Copiez la définition JSON de la table dans un fichier appelé *bloboutputtabledef.json* et enregistrez-le dans un emplacement connu (ici supposé comme étant *C:\temp\bloboutputtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="55cae-207">Copy the JSON definition of the table into a file called *bloboutputtabledef.json* file and save it to a known location (here assumed to be *C:\temp\bloboutputtabledef.json*).</span></span> <span data-ttu-id="55cae-208">Créez la table dans ADF avec la cmdlet Azure PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="55cae-208">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <span data-ttu-id="55cae-209"><a name="adf-table-azure-sq"></a>Table SQL Azure</span><span class="sxs-lookup"><span data-stu-id="55cae-209"><a name="adf-table-azure-sq"></a>SQL Azure Table</span></span>
<span data-ttu-id="55cae-210">La définition de la table pour la sortie SQL Azure est la suivante (ce schéma mappe les données provenant de l'objet blob) :</span><span class="sxs-lookup"><span data-stu-id="55cae-210">Definition for the table for the SQL Azure output is in the following (this schema maps the data coming from the blob):</span></span>

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

<span data-ttu-id="55cae-211">Copiez la définition JSON de la table dans un fichier appelé *AzureSqlTable.json* et enregistrez-le dans un emplacement connu (ici supposé comme étant *C:\temp\AzureSqlTable.json*).</span><span class="sxs-lookup"><span data-stu-id="55cae-211">Copy the JSON definition of the table into a file called *AzureSqlTable.json* file and save it to a known location (here assumed to be *C:\temp\AzureSqlTable.json*).</span></span> <span data-ttu-id="55cae-212">Créez la table dans ADF avec la cmdlet Azure PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="55cae-212">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <span data-ttu-id="55cae-213"><a name="adf-pipeline"></a>Définir et créer le pipeline</span><span class="sxs-lookup"><span data-stu-id="55cae-213"><a name="adf-pipeline"></a>Define and create the pipeline</span></span>
<span data-ttu-id="55cae-214">Spécifiez les activités appartenant au pipeline et créez le pipeline avec les procédures reposant sur des scripts suivantes.</span><span class="sxs-lookup"><span data-stu-id="55cae-214">Specify the activities that belong to the pipeline and create the pipeline with the following script-based procedures.</span></span> <span data-ttu-id="55cae-215">Un fichier JSON est utilisé pour définir les propriétés du pipeline.</span><span class="sxs-lookup"><span data-stu-id="55cae-215">A JSON file is used to define the pipeline properties.</span></span>

* <span data-ttu-id="55cae-216">Le script suppose que le **nom du pipeline** est *AMLDSProcessPipeline*.</span><span class="sxs-lookup"><span data-stu-id="55cae-216">The script assumes that the **pipeline name** is *AMLDSProcessPipeline*.</span></span>
* <span data-ttu-id="55cae-217">Notez également que nous avons défini la périodicité du pipeline sur une exécution quotidienne et avec un temps d'exécution par défaut pour la tâche (12 h 00 UTC).</span><span class="sxs-lookup"><span data-stu-id="55cae-217">Also note that we set the periodicity of the pipeline to be executed on daily basis and use the default execution time for the job (12 am UTC).</span></span>

> [!NOTE]
> <span data-ttu-id="55cae-218">Les procédures suivantes utilisent Azure PowerShell pour définir et créer le pipeline ADF.</span><span class="sxs-lookup"><span data-stu-id="55cae-218">The following procedures use Azure PowerShell to define and create the ADF pipeline.</span></span> <span data-ttu-id="55cae-219">Toutefois, cette tâche peut également être accomplie à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="55cae-219">But this task can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="55cae-220">Pour plus d’informations, consultez [Création d’un pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span><span class="sxs-lookup"><span data-stu-id="55cae-220">For details, see [Create pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span></span>
>
>

<span data-ttu-id="55cae-221">En utilisant les définitions de table fournies précédemment, la définition de pipeline pour ADF est spécifiée comme suit :</span><span class="sxs-lookup"><span data-stu-id="55cae-221">Using the table definitions provided previously, the pipeline definition for the ADF is specified as follows:</span></span>

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL to Azure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server to blob",     
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
                        "description": "Push data to Sql Azure",        
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

<span data-ttu-id="55cae-222">Copiez cette définition JSON du pipeline dans un fichier appelé *pipelinedef.json* et enregistrez-le dans un emplacement connu (ici supposé comme étant *C:\temp\pipelinedef.json*).</span><span class="sxs-lookup"><span data-stu-id="55cae-222">Copy this JSON definition of the pipeline into a file called *pipelinedef.json* file and save it to a known location (here assumed to be *C:\temp\pipelinedef.json*).</span></span> <span data-ttu-id="55cae-223">Créez le pipeline dans ADF avec l’applet de commande Azure PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="55cae-223">Create the pipeline in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

<span data-ttu-id="55cae-224">Vérifiez que le pipeline s’affiche sur l’ADF dans le portail Azure Classic comme suit (lorsque vous cliquez sur le schéma)</span><span class="sxs-lookup"><span data-stu-id="55cae-224">Confirm that you can see the pipeline on the ADF in the Azure Classic Portal show up as following (when you click the diagram)</span></span>

![Pipeline ADF](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <span data-ttu-id="55cae-226"><a name="adf-pipeline-start"></a>Lancer le pipeline</span><span class="sxs-lookup"><span data-stu-id="55cae-226"><a name="adf-pipeline-start"></a>Start the Pipeline</span></span>
<span data-ttu-id="55cae-227">Le pipeline peut maintenant être exécuté à l'aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="55cae-227">The pipeline can now be run using the following command:</span></span>

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

<span data-ttu-id="55cae-228">Les valeurs de paramètres *startdate* et *enddate* doivent être remplacées par les dates entre lesquelles le pipeline doit s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="55cae-228">The *startdate* and *enddate* parameter values need to be replaced with the actual dates between which you want the pipeline to run.</span></span>

<span data-ttu-id="55cae-229">Une fois que le pipeline s'exécute, vous devez être en mesure de voir des données apparaître dans le conteneur sélectionné pour l'objet blob, à compter d’un fichier par jour.</span><span class="sxs-lookup"><span data-stu-id="55cae-229">Once the pipeline executes, you should be able to see the data show up in the container selected for the blob, one file per day.</span></span>

<span data-ttu-id="55cae-230">Notez que nous n'avons pas tiré parti de la fonctionnalité fournie par ADF de canaliser les données de manière incrémentielle.</span><span class="sxs-lookup"><span data-stu-id="55cae-230">Note that we have not leveraged the functionality provided by ADF to pipe data incrementally.</span></span> <span data-ttu-id="55cae-231">Pour plus d’informations sur son utilisation et d’autres fonctionnalités fournies par ADF, consultez la [documentation ADF](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="55cae-231">For more information on how to do this and other capabilities provided by ADF, see the [ADF documentation](https://azure.microsoft.com/services/data-factory/).</span></span>
