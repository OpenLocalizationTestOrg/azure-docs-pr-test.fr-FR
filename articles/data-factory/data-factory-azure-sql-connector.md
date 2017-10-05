---
title: "Copier des données vers ou à partir de Microsoft Azure SQL Database | Microsoft Docs"
description: "Apprenez à copier des données vers/depuis Azure SQL Database en utilisant Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: a64d13fa7dc5f50c259b98774be80b603dce400a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-to-and-from-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="cde5d-103">Copier des données vers et depuis Azure SQL Database en utilisant Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="cde5d-103">Copy data to and from Azure SQL Database using Azure Data Factory</span></span>
<span data-ttu-id="cde5d-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour déplacer des données vers et depuis Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="cde5d-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to and from Azure SQL Database.</span></span> <span data-ttu-id="cde5d-105">Il s’appuie sur l’article [Activités de déplacement des données](data-factory-data-movement-activities.md), qui présente une vue d’ensemble du déplacement de données avec l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="cde5d-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

## <a name="supported-scenarios"></a><span data-ttu-id="cde5d-106">Scénarios pris en charge</span><span class="sxs-lookup"><span data-stu-id="cde5d-106">Supported scenarios</span></span>
<span data-ttu-id="cde5d-107">Vous pouvez copier des données **depuis Azure SQL Database** vers les magasins de données suivants :</span><span class="sxs-lookup"><span data-stu-id="cde5d-107">You can copy data **from Azure SQL Database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="cde5d-108">Vous pouvez copier des données depuis les magasins de données suivants **vers Azure SQL Database** :</span><span class="sxs-lookup"><span data-stu-id="cde5d-108">You can copy data from the following data stores **to Azure SQL Database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a><span data-ttu-id="cde5d-109">Type d’authentification pris en charge</span><span class="sxs-lookup"><span data-stu-id="cde5d-109">Supported authentication type</span></span>
<span data-ttu-id="cde5d-110">Le connecteur Azure SQL Database prend en charge l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="cde5d-110">Azure SQL Database connector supports basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="cde5d-111">Prise en main</span><span class="sxs-lookup"><span data-stu-id="cde5d-111">Getting started</span></span>
<span data-ttu-id="cde5d-112">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers/depuis Azure SQL Database à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="cde5d-112">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span></span>

<span data-ttu-id="cde5d-113">Le moyen le plus simple de créer un pipeline consiste à utiliser **l’Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="cde5d-113">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="cde5d-114">Consultez la page [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant Copier des données.</span><span class="sxs-lookup"><span data-stu-id="cde5d-114">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="cde5d-115">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="cde5d-115">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="cde5d-116">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="cde5d-116">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="cde5d-117">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="cde5d-117">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="cde5d-118">Création d'une **fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="cde5d-118">Create a **data factory**.</span></span> <span data-ttu-id="cde5d-119">Une fabrique de données peut contenir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="cde5d-119">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="cde5d-120">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="cde5d-120">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="cde5d-121">Par exemple, si vous copiez des données depuis un stockage d’objets blob Azure vers une base de données SQL Azure, vous créez deux services liés pour lier votre compte de stockage Azure et votre base de données SQL Azure à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="cde5d-121">For example, if you are copying data from an Azure blob storage to an Azure SQL database, you create two linked services to link your Azure storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="cde5d-122">Pour les propriétés du service lié qui sont spécifiques à Azure SQL Database, consultez la section [propriétés du service lié](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cde5d-122">For linked service properties that are specific to Azure SQL Database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="cde5d-123">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="cde5d-123">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="cde5d-124">Dans l’exemple mentionné dans la dernière étape, vous créez un jeu de données pour spécifier le conteneur d’objets blob et le dossier qui contient les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="cde5d-124">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="cde5d-125">Vous créez aussi un autre jeu de données pour spécifier la table SQL dans la base de données SQL Azure qui contient les données copiées depuis le stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="cde5d-125">And, you create another dataset to specify the SQL table in the Azure SQL database  that holds the data copied from the blob storage.</span></span> <span data-ttu-id="cde5d-126">Pour les propriétés du jeu de données qui sont spécifiques à Azure Data Lake Store, consultez la section [propriétés du jeu de données](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cde5d-126">For dataset properties that are specific to Azure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="cde5d-127">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="cde5d-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="cde5d-128">Dans l’exemple mentionné plus haut, vous utilisez BlobSource comme source et SqlSink comme récepteur pour l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="cde5d-128">In the example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for the copy activity.</span></span> <span data-ttu-id="cde5d-129">De même, si vous copiez depuis Azure SQL Database vers Stockage Blob Azure, vous utilisez SqlSource et BlobSink dans l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="cde5d-129">Similarly, if you are copying from Azure SQL Database to Azure Blob Storage, you use SqlSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="cde5d-130">Pour les propriétés d’activité de copie qui sont spécifiques à Azure SQL Database, consultez la section [propriétés de l’activité de copie](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="cde5d-130">For copy activity properties that are specific to Azure SQL Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="cde5d-131">Pour plus d’informations sur l’utilisation d’un magasin de données comme source ou comme récepteur, cliquez sur le lien dans la section précédente pour votre magasin de données.</span><span class="sxs-lookup"><span data-stu-id="cde5d-131">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="cde5d-132">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="cde5d-132">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="cde5d-133">Lorsque vous utilisez des outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory au format JSON.</span><span class="sxs-lookup"><span data-stu-id="cde5d-133">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="cde5d-134">Pour obtenir des exemples comportant des définitions JSON pour les entités Data Factory utilisées pour copier les données vers ou à partir d’Azure SQL Database, consultez la section [Exemples JSON](#json-examples-for-copying-data-to-and-from-sql-database) de cet article.</span><span class="sxs-lookup"><span data-stu-id="cde5d-134">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Database, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-database) section of this article.</span></span> 

<span data-ttu-id="cde5d-135">Les sections suivantes offrent des informations détaillées sur les propriétés JSON utilisées pour définir les entités Data Factory propres à Azure SQL Database :</span><span class="sxs-lookup"><span data-stu-id="cde5d-135">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Database:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="cde5d-136">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="cde5d-136">Linked service properties</span></span>
<span data-ttu-id="cde5d-137">Un service lié SQL Azure lie une base de données SQL Azure à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="cde5d-137">An Azure SQL linked service links an Azure SQL database to your data factory.</span></span> <span data-ttu-id="cde5d-138">Le tableau suivant fournit la description des éléments JSON spécifiques au service lié SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cde5d-138">The following table provides description for JSON elements specific to Azure SQL linked service.</span></span>

| <span data-ttu-id="cde5d-139">Propriété</span><span class="sxs-lookup"><span data-stu-id="cde5d-139">Property</span></span> | <span data-ttu-id="cde5d-140">Description</span><span class="sxs-lookup"><span data-stu-id="cde5d-140">Description</span></span> | <span data-ttu-id="cde5d-141">Requis</span><span class="sxs-lookup"><span data-stu-id="cde5d-141">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cde5d-142">type</span><span class="sxs-lookup"><span data-stu-id="cde5d-142">type</span></span> |<span data-ttu-id="cde5d-143">La propriété de type doit être définie sur : **AzureSqlDatabase**</span><span class="sxs-lookup"><span data-stu-id="cde5d-143">The type property must be set to: **AzureSqlDatabase**</span></span> |<span data-ttu-id="cde5d-144">Oui</span><span class="sxs-lookup"><span data-stu-id="cde5d-144">Yes</span></span> |
| <span data-ttu-id="cde5d-145">connectionString</span><span class="sxs-lookup"><span data-stu-id="cde5d-145">connectionString</span></span> |<span data-ttu-id="cde5d-146">Spécifier les informations requises pour la connexion à l’instance de base de données SQL Azure pour la propriété connectionString.</span><span class="sxs-lookup"><span data-stu-id="cde5d-146">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> <span data-ttu-id="cde5d-147">Seule l’authentification de base est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="cde5d-147">Only basic authentication is supported.</span></span> |<span data-ttu-id="cde5d-148">Oui</span><span class="sxs-lookup"><span data-stu-id="cde5d-148">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="cde5d-149">Configurez le [pare-feu Azure SQL Database](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) et le serveur de base de données pour [autoriser les services Azure à accéder au serveur](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="cde5d-149">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="cde5d-150">En outre, si vous copiez des données vers Azure SQL Database à partir d’un emplacement situé en dehors d’Azure, y compris à partir de sources de données locales avec la passerelle de la fabrique de données, configurez la plage d’adresses IP appropriée pour l’ordinateur qui envoie des données à Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="cde5d-150">Additionally, if you are copying data to Azure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Database.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="cde5d-151">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="cde5d-151">Dataset properties</span></span>
<span data-ttu-id="cde5d-152">Pour spécifier un jeu de données afin de représenter les données d’entrée ou de sortie dans une base de données SQL Azure, vous devez définir la propriété de type du jeu de données sur : **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="cde5d-152">To specify a dataset to represent input or output data in an Azure SQL database, you set the type property of the dataset to: **AzureSqlTable**.</span></span> <span data-ttu-id="cde5d-153">Définissez la propriété **linkedServiceName** du jeu de données sur le nom du service lié Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="cde5d-153">Set the **linkedServiceName** property of the dataset to the name of the Azure SQL linked service.</span></span>  

<span data-ttu-id="cde5d-154">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="cde5d-154">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="cde5d-155">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="cde5d-155">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="cde5d-156">La section typeProperties est différente pour chaque type de jeu de données et fournit des informations sur l'emplacement des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="cde5d-156">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="cde5d-157">La section **typeProperties** pour le jeu de données de type **AzureSqlTable** a les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="cde5d-157">The **typeProperties** section for the dataset of type **AzureSqlTable** has the following properties:</span></span>

| <span data-ttu-id="cde5d-158">Propriété</span><span class="sxs-lookup"><span data-stu-id="cde5d-158">Property</span></span> | <span data-ttu-id="cde5d-159">Description</span><span class="sxs-lookup"><span data-stu-id="cde5d-159">Description</span></span> | <span data-ttu-id="cde5d-160">Requis</span><span class="sxs-lookup"><span data-stu-id="cde5d-160">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cde5d-161">TableName</span><span class="sxs-lookup"><span data-stu-id="cde5d-161">tableName</span></span> |<span data-ttu-id="cde5d-162">Nom de la table ou de la vue dans l’instance Azure SQL Database à laquelle le service lié fait référence.</span><span class="sxs-lookup"><span data-stu-id="cde5d-162">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="cde5d-163">Oui</span><span class="sxs-lookup"><span data-stu-id="cde5d-163">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="cde5d-164">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="cde5d-164">Copy activity properties</span></span>
<span data-ttu-id="cde5d-165">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="cde5d-165">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="cde5d-166">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="cde5d-166">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="cde5d-167">L'activité de copie accepte uniquement une entrée et produit une seule sortie.</span><span class="sxs-lookup"><span data-stu-id="cde5d-167">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="cde5d-168">En revanche, les propriétés disponibles dans la section **typeProperties** de l’activité varient pour chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="cde5d-168">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="cde5d-169">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="cde5d-169">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="cde5d-170">Si vous déplacez des données à partir d’une Azure SQL Database, vous définissez le type de source dans l’activité de copie sur **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="cde5d-170">If you are moving data from an Azure SQL database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="cde5d-171">De même, si vous déplacez des données vers une Azure SQL Database, vous définissez le type de récepteur dans l’activité de copie sur **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="cde5d-171">Similarly, if you are moving data to an Azure SQL database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="cde5d-172">Cette section fournit une liste de propriétés prises en charge par SqlSource et SqlSink.</span><span class="sxs-lookup"><span data-stu-id="cde5d-172">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="cde5d-173">SqlSource</span><span class="sxs-lookup"><span data-stu-id="cde5d-173">SqlSource</span></span>
<span data-ttu-id="cde5d-174">Dans le cas d’une activité de copie, quand la source est de type **SqlSource**, les propriétés suivantes sont disponibles dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="cde5d-174">In copy activity, when the source is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="cde5d-175">Propriété</span><span class="sxs-lookup"><span data-stu-id="cde5d-175">Property</span></span> | <span data-ttu-id="cde5d-176">Description</span><span class="sxs-lookup"><span data-stu-id="cde5d-176">Description</span></span> | <span data-ttu-id="cde5d-177">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="cde5d-177">Allowed values</span></span> | <span data-ttu-id="cde5d-178">Requis</span><span class="sxs-lookup"><span data-stu-id="cde5d-178">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cde5d-179">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="cde5d-179">sqlReaderQuery</span></span> |<span data-ttu-id="cde5d-180">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="cde5d-180">Use the custom query to read data.</span></span> |<span data-ttu-id="cde5d-181">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="cde5d-181">SQL query string.</span></span> <span data-ttu-id="cde5d-182">Exemple : `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="cde5d-182">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="cde5d-183">Non</span><span class="sxs-lookup"><span data-stu-id="cde5d-183">No</span></span> |
| <span data-ttu-id="cde5d-184">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="cde5d-184">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="cde5d-185">Nom de la procédure stockée qui lit les données de la table source.</span><span class="sxs-lookup"><span data-stu-id="cde5d-185">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="cde5d-186">Nom de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="cde5d-186">Name of the stored procedure.</span></span> <span data-ttu-id="cde5d-187">La dernière instruction SQL doit être une instruction SELECT dans la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="cde5d-187">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="cde5d-188">Non</span><span class="sxs-lookup"><span data-stu-id="cde5d-188">No</span></span> |
| <span data-ttu-id="cde5d-189">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="cde5d-189">storedProcedureParameters</span></span> |<span data-ttu-id="cde5d-190">Paramètres de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="cde5d-190">Parameters for the stored procedure.</span></span> |<span data-ttu-id="cde5d-191">Paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="cde5d-191">Name/value pairs.</span></span> <span data-ttu-id="cde5d-192">Les noms et la casse des paramètres doivent correspondre aux noms et à la casse des paramètres de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="cde5d-192">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="cde5d-193">Non</span><span class="sxs-lookup"><span data-stu-id="cde5d-193">No</span></span> |

<span data-ttu-id="cde5d-194">Si **sqlReaderQuery** est spécifié pour SqlSource, l'activité de copie exécute cette requête sur la source Azure SQL Database pour obtenir les données.</span><span class="sxs-lookup"><span data-stu-id="cde5d-194">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="cde5d-195">Vous pouvez également spécifier une procédure stockée en indiquant **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si la procédure stockée accepte des paramètres).</span><span class="sxs-lookup"><span data-stu-id="cde5d-195">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="cde5d-196">Si vous ne spécifiez pas sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes définies dans la section Structure du jeu de données JSON sont utilisées pour créer une requête (`select column1, column2 from mytable`) à exécuter sur Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="cde5d-196">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (`select column1, column2 from mytable`) to run against the Azure SQL Database.</span></span> <span data-ttu-id="cde5d-197">Si la définition du jeu de données ne possède pas de structure, toutes les colonnes de la table sont sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="cde5d-197">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="cde5d-198">Quand vous utilisez **sqlReaderStoredProcedureName**, vous devez toujours spécifier une valeur pour la propriété **tableName** du code JSON du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="cde5d-198">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="cde5d-199">Cependant, il n’existe aucune validation effectuée pour cette table.</span><span class="sxs-lookup"><span data-stu-id="cde5d-199">There are no validations performed against this table though.</span></span>
>
>

### <a name="sqlsource-example"></a><span data-ttu-id="cde5d-200">Exemple SqlSource</span><span class="sxs-lookup"><span data-stu-id="cde5d-200">SqlSource example</span></span>

```JSON
"source": {
    "type": "SqlSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```

<span data-ttu-id="cde5d-201">**Définition de la procédure stockée :**</span><span class="sxs-lookup"><span data-stu-id="cde5d-201">**The stored procedure definition:**</span></span>

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqlsink"></a><span data-ttu-id="cde5d-202">SqlSink</span><span class="sxs-lookup"><span data-stu-id="cde5d-202">SqlSink</span></span>
<span data-ttu-id="cde5d-203">**SqlSink** prend en charge les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="cde5d-203">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="cde5d-204">Propriété</span><span class="sxs-lookup"><span data-stu-id="cde5d-204">Property</span></span> | <span data-ttu-id="cde5d-205">Description</span><span class="sxs-lookup"><span data-stu-id="cde5d-205">Description</span></span> | <span data-ttu-id="cde5d-206">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="cde5d-206">Allowed values</span></span> | <span data-ttu-id="cde5d-207">Requis</span><span class="sxs-lookup"><span data-stu-id="cde5d-207">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cde5d-208">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="cde5d-208">writeBatchTimeout</span></span> |<span data-ttu-id="cde5d-209">Temps d’attente pour que l’opération d’insertion de lot soit terminée avant d’expirer.</span><span class="sxs-lookup"><span data-stu-id="cde5d-209">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="cde5d-210">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="cde5d-210">timespan</span></span><br/><br/> <span data-ttu-id="cde5d-211">Exemple : « 00:30:00 » (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="cde5d-211">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="cde5d-212">Non</span><span class="sxs-lookup"><span data-stu-id="cde5d-212">No</span></span> |
| <span data-ttu-id="cde5d-213">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="cde5d-213">writeBatchSize</span></span> |<span data-ttu-id="cde5d-214">Insère des données dans la table SQL lorsque la taille du tampon atteint writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="cde5d-214">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="cde5d-215">Nombre entier (nombre de lignes)</span><span class="sxs-lookup"><span data-stu-id="cde5d-215">Integer (number of rows)</span></span> |<span data-ttu-id="cde5d-216">Non (valeur par défaut : 10000)</span><span class="sxs-lookup"><span data-stu-id="cde5d-216">No (default: 10000)</span></span> |
| <span data-ttu-id="cde5d-217">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="cde5d-217">sqlWriterCleanupScript</span></span> |<span data-ttu-id="cde5d-218">Spécifiez une requête pour exécuter l’activité de copie afin que les données d’un segment spécifique soient nettoyées.</span><span class="sxs-lookup"><span data-stu-id="cde5d-218">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="cde5d-219">Pour en savoir plus, voir [Copie renouvelée](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="cde5d-219">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="cde5d-220">Une instruction de requête.</span><span class="sxs-lookup"><span data-stu-id="cde5d-220">A query statement.</span></span> |<span data-ttu-id="cde5d-221">Non</span><span class="sxs-lookup"><span data-stu-id="cde5d-221">No</span></span> |
| <span data-ttu-id="cde5d-222">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="cde5d-222">sliceIdentifierColumnName</span></span> |<span data-ttu-id="cde5d-223">Spécifiez le nom de la colonne que l’activité de copie doit remplir avec l’identificateur de segment généré automatiquement, qui est utilisé pour nettoyer les données d’un segment spécifique lors de la ré-exécution.</span><span class="sxs-lookup"><span data-stu-id="cde5d-223">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="cde5d-224">Pour en savoir plus, voir [Copie renouvelée](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="cde5d-224">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="cde5d-225">Nom d’une colonne avec le type de données binary(32).</span><span class="sxs-lookup"><span data-stu-id="cde5d-225">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="cde5d-226">Non</span><span class="sxs-lookup"><span data-stu-id="cde5d-226">No</span></span> |
| <span data-ttu-id="cde5d-227">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="cde5d-227">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="cde5d-228">Nom de la procédure stockée qui met à jour/insère les données dans la table cible.</span><span class="sxs-lookup"><span data-stu-id="cde5d-228">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="cde5d-229">Nom de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="cde5d-229">Name of the stored procedure.</span></span> |<span data-ttu-id="cde5d-230">Non</span><span class="sxs-lookup"><span data-stu-id="cde5d-230">No</span></span> |
| <span data-ttu-id="cde5d-231">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="cde5d-231">storedProcedureParameters</span></span> |<span data-ttu-id="cde5d-232">Paramètres de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="cde5d-232">Parameters for the stored procedure.</span></span> |<span data-ttu-id="cde5d-233">Paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="cde5d-233">Name/value pairs.</span></span> <span data-ttu-id="cde5d-234">Les noms et la casse des paramètres doivent correspondre aux noms et à la casse des paramètres de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="cde5d-234">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="cde5d-235">Non</span><span class="sxs-lookup"><span data-stu-id="cde5d-235">No</span></span> |
| <span data-ttu-id="cde5d-236">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="cde5d-236">sqlWriterTableType</span></span> |<span data-ttu-id="cde5d-237">Spécifiez le nom du type de table à utiliser dans la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="cde5d-237">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="cde5d-238">L’activité de copie place les données déplacées disponibles dans une table temporaire avec ce type de table.</span><span class="sxs-lookup"><span data-stu-id="cde5d-238">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="cde5d-239">Le code de procédure stockée peut ensuite fusionner les données copiées avec les données existantes.</span><span class="sxs-lookup"><span data-stu-id="cde5d-239">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="cde5d-240">Nom de type de table.</span><span class="sxs-lookup"><span data-stu-id="cde5d-240">A table type name.</span></span> |<span data-ttu-id="cde5d-241">Non</span><span class="sxs-lookup"><span data-stu-id="cde5d-241">No</span></span> |

#### <a name="sqlsink-example"></a><span data-ttu-id="cde5d-242">Exemple SqlSink</span><span class="sxs-lookup"><span data-stu-id="cde5d-242">SqlSink example</span></span>

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples-for-copying-data-to-and-from-sql-database"></a><span data-ttu-id="cde5d-243">Exemples JSON pour copier des données vers et depuis SQL Database</span><span class="sxs-lookup"><span data-stu-id="cde5d-243">JSON examples for copying data to and from SQL Database</span></span>
<span data-ttu-id="cde5d-244">Les exemples suivants présentent des exemples de définitions de JSON que vous pouvez utiliser pour créer un pipeline à l’aide [du Portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [de Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [d’Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="cde5d-244">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="cde5d-245">Ils indiquent comment copier des données vers et depuis une base de données Azure SQL et Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="cde5d-245">They show how to copy data to and from Azure SQL Database and Azure Blob Storage.</span></span> <span data-ttu-id="cde5d-246">Toutefois, les données peuvent être copiées **directement** vers l’un des récepteurs indiqués [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) , via l’activité de copie de Microsoft Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="cde5d-246">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-database-to-azure-blob"></a><span data-ttu-id="cde5d-247">Exemple : Copie de données depuis Azure SQL Database vers un objet blob Azure</span><span class="sxs-lookup"><span data-stu-id="cde5d-247">Example: Copy data from Azure SQL Database to Azure Blob</span></span>
<span data-ttu-id="cde5d-248">L’exemple définit les entités de fabrique de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="cde5d-248">The same defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="cde5d-249">Un service lié de type [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cde5d-249">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="cde5d-250">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cde5d-250">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="cde5d-251">Un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cde5d-251">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
4. <span data-ttu-id="cde5d-252">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cde5d-252">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="cde5d-253">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [SqlSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="cde5d-253">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="cde5d-254">L’exemple copie toutes les heures les données temporelles (horaire, journalière, etc.) d’une table Azure SQL Database vers un objet blob.</span><span class="sxs-lookup"><span data-stu-id="cde5d-254">The sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database to a blob every hour.</span></span> <span data-ttu-id="cde5d-255">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="cde5d-255">The JSON properties used in these samples are described in sections following the samples.</span></span>  

<span data-ttu-id="cde5d-256">**Service lié Azure SQL Database :**</span><span class="sxs-lookup"><span data-stu-id="cde5d-256">**Azure SQL Database linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="cde5d-257">Consultez la section [Service lié SQL Azure](#linked-service) pour obtenir la liste des propriétés prises en charge par ce service lié.</span><span class="sxs-lookup"><span data-stu-id="cde5d-257">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="cde5d-258">**Service lié Azure Blob Storage :**</span><span class="sxs-lookup"><span data-stu-id="cde5d-258">**Azure Blob storage linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="cde5d-259">Consultez l’article [Objets blob Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) pour obtenir la liste des propriétés prises en charge par ce service lié.</span><span class="sxs-lookup"><span data-stu-id="cde5d-259">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="cde5d-260">**Jeu de données d'entrée SQL Azure :**</span><span class="sxs-lookup"><span data-stu-id="cde5d-260">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="cde5d-261">L'exemple suppose que vous avez créé une table « MyTable » dans SQL Azure et qu'elle contient une colonne appelée « timestampcolumn » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="cde5d-261">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="cde5d-262">La définition de « external » : « true» informe le service Azure Data Factory que le jeu de données est externe à la fabrique de données et n’est pas produit par une activité dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="cde5d-262">Setting “external”: ”true” informs the Azure Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="cde5d-263">Consultez la section [Propriétés de type du jeu de données SQL Azure](#dataset) pour obtenir la liste des propriétés prises en charge par ce type de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="cde5d-263">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="cde5d-264">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="cde5d-264">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="cde5d-265">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="cde5d-265">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="cde5d-266">Le chemin d’accès du dossier pour l’objet blob est évalué dynamiquement en fonction de l’heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="cde5d-266">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="cde5d-267">Le chemin d’accès du dossier utilise l’année, le mois, le jour et l’heure de l’heure de début.</span><span class="sxs-lookup"><span data-stu-id="cde5d-267">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="cde5d-268">Consultez la section [Propriétés de type du jeu de données d’objets blob Azure](data-factory-azure-blob-connector.md#dataset-properties) pour obtenir la liste des propriétés prises en charge par ce type de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="cde5d-268">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="cde5d-269">**Activité de copie dans un pipeline avec une source SQL et un récepteur blob :**</span><span class="sxs-lookup"><span data-stu-id="cde5d-269">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="cde5d-270">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="cde5d-270">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="cde5d-271">Dans la définition du pipeline JSON, le type **source** est défini sur **SqlSource** et le type **sink** est défini sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="cde5d-271">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="cde5d-272">La requête SQL spécifiée pour la propriété **SqlReaderQuery** sélectionne les données de la dernière heure à copier.</span><span class="sxs-lookup"><span data-stu-id="cde5d-272">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```
<span data-ttu-id="cde5d-273">Dans l’exemple, **sqlReaderQuery** est spécifié pour SqlSource.</span><span class="sxs-lookup"><span data-stu-id="cde5d-273">In the example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="cde5d-274">L'activité de copie exécute cette requête sur la source Azure SQL Database pour obtenir les données.</span><span class="sxs-lookup"><span data-stu-id="cde5d-274">The Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="cde5d-275">Vous pouvez également spécifier une procédure stockée en indiquant **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si la procédure stockée accepte des paramètres).</span><span class="sxs-lookup"><span data-stu-id="cde5d-275">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="cde5d-276">Si vous ne spécifiez pas sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes définies dans la section Structure du jeu de données JSON sont utilisées pour créer une requête à exécuter sur Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="cde5d-276">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Database.</span></span> <span data-ttu-id="cde5d-277">Par exemple : `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="cde5d-277">For example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="cde5d-278">Si la définition du jeu de données ne possède pas de structure, toutes les colonnes de la table sont sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="cde5d-278">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="cde5d-279">Consultez la section [Sql Source](#sqlsource) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) pour obtenir la liste des propriétés prises en charge par SqlSource et BlobSink.</span><span class="sxs-lookup"><span data-stu-id="cde5d-279">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

### <a name="example-copy-data-from-azure-blob-to-azure-sql-database"></a><span data-ttu-id="cde5d-280">Exemple : Copie de données d’un objet blob Azure vers Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="cde5d-280">Example: Copy data from Azure Blob to Azure SQL Database</span></span>
<span data-ttu-id="cde5d-281">L’exemple définit les entités Data Factory suivantes :</span><span class="sxs-lookup"><span data-stu-id="cde5d-281">The sample defines the following Data Factory entities:</span></span>  

1. <span data-ttu-id="cde5d-282">Un service lié de type [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cde5d-282">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="cde5d-283">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cde5d-283">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="cde5d-284">Un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cde5d-284">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="cde5d-285">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cde5d-285">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
5. <span data-ttu-id="cde5d-286">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) et [SqlSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="cde5d-286">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span></span>

<span data-ttu-id="cde5d-287">L’exemple copie toutes les heures les données temporelles (horaire, journalière, etc.) d’un objet blob Azure vers Azure SQL Database .</span><span class="sxs-lookup"><span data-stu-id="cde5d-287">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL database every hour.</span></span> <span data-ttu-id="cde5d-288">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="cde5d-288">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="cde5d-289">**Service lié SQL Azure :**</span><span class="sxs-lookup"><span data-stu-id="cde5d-289">**Azure SQL linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="cde5d-290">Consultez la section [Service lié SQL Azure](#linked-service) pour obtenir la liste des propriétés prises en charge par ce service lié.</span><span class="sxs-lookup"><span data-stu-id="cde5d-290">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="cde5d-291">**Service lié Azure Blob Storage :**</span><span class="sxs-lookup"><span data-stu-id="cde5d-291">**Azure Blob storage linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="cde5d-292">Consultez l’article [Objets blob Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) pour obtenir la liste des propriétés prises en charge par ce service lié.</span><span class="sxs-lookup"><span data-stu-id="cde5d-292">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="cde5d-293">**Jeu de données d'entrée d'objet Blob Azure :**</span><span class="sxs-lookup"><span data-stu-id="cde5d-293">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="cde5d-294">Les données sont récupérées à partir d'un nouvel objet Blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="cde5d-294">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="cde5d-295">Le nom du chemin d'accès et du fichier de dossier pour l'objet blob sont évalués dynamiquement en fonction de l'heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="cde5d-295">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="cde5d-296">Le chemin d’accès du dossier utilise l’année, le mois et le jour de début et le nom de fichier utilise l’heure de début.</span><span class="sxs-lookup"><span data-stu-id="cde5d-296">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="cde5d-297">Le paramètre « external » : « true » informe le service Data Factory que cette table est externe à la fabrique de données et n’est pas produite par une activité dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="cde5d-297">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
<span data-ttu-id="cde5d-298">Consultez la section [Propriétés de type du jeu de données d’objets blob Azure](data-factory-azure-blob-connector.md#dataset-properties) pour obtenir la liste des propriétés prises en charge par ce type de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="cde5d-298">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="cde5d-299">**Jeu de données de sortie Azure SQL Database :**</span><span class="sxs-lookup"><span data-stu-id="cde5d-299">**Azure SQL Database output dataset:**</span></span>

<span data-ttu-id="cde5d-300">L'exemple copie les données dans une table nommée « MyTable » dans SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cde5d-300">The sample copies data to a table named “MyTable” in Azure SQL.</span></span> <span data-ttu-id="cde5d-301">Créez la table dans SQL Azure avec le même nombre de colonnes que le fichier CSV d’objets blob doit en contenir.</span><span class="sxs-lookup"><span data-stu-id="cde5d-301">Create the table in Azure SQL with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="cde5d-302">De nouvelles lignes sont ajoutées à la table toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="cde5d-302">New rows are added to the table every hour.</span></span>

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="cde5d-303">Consultez la section [Propriétés de type du jeu de données SQL Azure](#dataset) pour obtenir la liste des propriétés prises en charge par ce type de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="cde5d-303">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="cde5d-304">**Activité de copie dans un pipeline avec une source blob et un récepteur SQL :**</span><span class="sxs-lookup"><span data-stu-id="cde5d-304">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="cde5d-305">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="cde5d-305">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="cde5d-306">Dans la définition du pipeline JSON, le type **source** est défini sur **BlobSource** et le type **sink** est défini sur **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="cde5d-306">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```
<span data-ttu-id="cde5d-307">Consultez la section [Sql Sink](#sqlsink) et [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) pour obtenir la liste des propriétés prises en charge par SqlSink et BlobSource.</span><span class="sxs-lookup"><span data-stu-id="cde5d-307">See the [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSink and BlobSource.</span></span>

## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="cde5d-308">Colonnes d’identité dans la base de données cible</span><span class="sxs-lookup"><span data-stu-id="cde5d-308">Identity columns in the target database</span></span>
<span data-ttu-id="cde5d-309">Cette section fournit un exemple pour copier des données d’une table source sans colonne d’identité vers une table de destination avec une colonne d’identité.</span><span class="sxs-lookup"><span data-stu-id="cde5d-309">This section provides an example for copying data from a source table without an identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="cde5d-310">**Table source :**</span><span class="sxs-lookup"><span data-stu-id="cde5d-310">**Source table:**</span></span>

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="cde5d-311">**Table de destination :**</span><span class="sxs-lookup"><span data-stu-id="cde5d-311">**Destination table:**</span></span>

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
<span data-ttu-id="cde5d-312">Notez que la table cible possède une colonne d’identité.</span><span class="sxs-lookup"><span data-stu-id="cde5d-312">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="cde5d-313">**Définition du jeu de données JSON source**</span><span class="sxs-lookup"><span data-stu-id="cde5d-313">**Source dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleSource",
    "properties": {
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="cde5d-314">**Définition de jeu de données JSON de destination**</span><span class="sxs-lookup"><span data-stu-id="cde5d-314">**Destination dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }    
}
```

<span data-ttu-id="cde5d-315">Notez que vos tables source et cible ont des schémas différents (la cible possède une colonne supplémentaire avec identité).</span><span class="sxs-lookup"><span data-stu-id="cde5d-315">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="cde5d-316">Dans ce scénario, vous devez spécifier la propriété **structure** dans la définition du jeu de données cible, qui n’inclut pas la colonne d’identité.</span><span class="sxs-lookup"><span data-stu-id="cde5d-316">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="cde5d-317">Appel d’une procédure stockée pour un récepteur SQL</span><span class="sxs-lookup"><span data-stu-id="cde5d-317">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="cde5d-318">Pour obtenir un exemple d’appel d’une procédure stockée à partir d’un récepteur SQL dans l’activité de copie d’un pipeline, consultez l’article [Appeler une procédure stockée pour un récepteur SQL dans l’activité de copie](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="cde5d-318">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span></span> 

## <a name="type-mapping-for-azure-sql-database"></a><span data-ttu-id="cde5d-319">Mappage de type pour Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="cde5d-319">Type mapping for Azure SQL Database</span></span>
<span data-ttu-id="cde5d-320">Comme mentionné dans l’article consacré aux [activités de déplacement des données](data-factory-data-movement-activities.md) , l’activité de copie convertit automatiquement les types source en types récepteur à l’aide de l’approche en 2 étapes suivante :</span><span class="sxs-lookup"><span data-stu-id="cde5d-320">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="cde5d-321">Conversion de types natifs source en types .NET</span><span class="sxs-lookup"><span data-stu-id="cde5d-321">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="cde5d-322">Conversion de types .NET en types récepteur natifs</span><span class="sxs-lookup"><span data-stu-id="cde5d-322">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="cde5d-323">Lors du déplacement des données vers et à partir de Microsoft Azure SQL Database, les mappages suivants sont utilisés depuis le type SQL vers le type .NET, et vice-versa.</span><span class="sxs-lookup"><span data-stu-id="cde5d-323">When moving data to and from Azure SQL Database, the following mappings are used from SQL type to .NET type and vice versa.</span></span> <span data-ttu-id="cde5d-324">Le mappage est identique au mappage du type de données SQL Server pour ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="cde5d-324">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="cde5d-325">Type de moteur de base de données SQL Server</span><span class="sxs-lookup"><span data-stu-id="cde5d-325">SQL Server Database Engine type</span></span> | <span data-ttu-id="cde5d-326">Type de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="cde5d-326">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="cde5d-327">bigint</span><span class="sxs-lookup"><span data-stu-id="cde5d-327">bigint</span></span> |<span data-ttu-id="cde5d-328">Int64</span><span class="sxs-lookup"><span data-stu-id="cde5d-328">Int64</span></span> |
| <span data-ttu-id="cde5d-329">binaire</span><span class="sxs-lookup"><span data-stu-id="cde5d-329">binary</span></span> |<span data-ttu-id="cde5d-330">Byte[]</span><span class="sxs-lookup"><span data-stu-id="cde5d-330">Byte[]</span></span> |
| <span data-ttu-id="cde5d-331">bit</span><span class="sxs-lookup"><span data-stu-id="cde5d-331">bit</span></span> |<span data-ttu-id="cde5d-332">Boolean</span><span class="sxs-lookup"><span data-stu-id="cde5d-332">Boolean</span></span> |
| <span data-ttu-id="cde5d-333">char</span><span class="sxs-lookup"><span data-stu-id="cde5d-333">char</span></span> |<span data-ttu-id="cde5d-334">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="cde5d-334">String, Char[]</span></span> |
| <span data-ttu-id="cde5d-335">date</span><span class="sxs-lookup"><span data-stu-id="cde5d-335">date</span></span> |<span data-ttu-id="cde5d-336">DateTime</span><span class="sxs-lookup"><span data-stu-id="cde5d-336">DateTime</span></span> |
| <span data-ttu-id="cde5d-337">DateTime</span><span class="sxs-lookup"><span data-stu-id="cde5d-337">Datetime</span></span> |<span data-ttu-id="cde5d-338">DateTime</span><span class="sxs-lookup"><span data-stu-id="cde5d-338">DateTime</span></span> |
| <span data-ttu-id="cde5d-339">datetime2</span><span class="sxs-lookup"><span data-stu-id="cde5d-339">datetime2</span></span> |<span data-ttu-id="cde5d-340">DateTime</span><span class="sxs-lookup"><span data-stu-id="cde5d-340">DateTime</span></span> |
| <span data-ttu-id="cde5d-341">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="cde5d-341">Datetimeoffset</span></span> |<span data-ttu-id="cde5d-342">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="cde5d-342">DateTimeOffset</span></span> |
| <span data-ttu-id="cde5d-343">Décimal</span><span class="sxs-lookup"><span data-stu-id="cde5d-343">Decimal</span></span> |<span data-ttu-id="cde5d-344">Décimal</span><span class="sxs-lookup"><span data-stu-id="cde5d-344">Decimal</span></span> |
| <span data-ttu-id="cde5d-345">Attribut FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="cde5d-345">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="cde5d-346">Byte[]</span><span class="sxs-lookup"><span data-stu-id="cde5d-346">Byte[]</span></span> |
| <span data-ttu-id="cde5d-347">Float</span><span class="sxs-lookup"><span data-stu-id="cde5d-347">Float</span></span> |<span data-ttu-id="cde5d-348">Double</span><span class="sxs-lookup"><span data-stu-id="cde5d-348">Double</span></span> |
| <span data-ttu-id="cde5d-349">image</span><span class="sxs-lookup"><span data-stu-id="cde5d-349">image</span></span> |<span data-ttu-id="cde5d-350">Byte[]</span><span class="sxs-lookup"><span data-stu-id="cde5d-350">Byte[]</span></span> |
| <span data-ttu-id="cde5d-351">int</span><span class="sxs-lookup"><span data-stu-id="cde5d-351">int</span></span> |<span data-ttu-id="cde5d-352">Int32</span><span class="sxs-lookup"><span data-stu-id="cde5d-352">Int32</span></span> |
| <span data-ttu-id="cde5d-353">money</span><span class="sxs-lookup"><span data-stu-id="cde5d-353">money</span></span> |<span data-ttu-id="cde5d-354">Décimal</span><span class="sxs-lookup"><span data-stu-id="cde5d-354">Decimal</span></span> |
| <span data-ttu-id="cde5d-355">nchar</span><span class="sxs-lookup"><span data-stu-id="cde5d-355">nchar</span></span> |<span data-ttu-id="cde5d-356">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="cde5d-356">String, Char[]</span></span> |
| <span data-ttu-id="cde5d-357">ntext</span><span class="sxs-lookup"><span data-stu-id="cde5d-357">ntext</span></span> |<span data-ttu-id="cde5d-358">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="cde5d-358">String, Char[]</span></span> |
| <span data-ttu-id="cde5d-359">numérique</span><span class="sxs-lookup"><span data-stu-id="cde5d-359">numeric</span></span> |<span data-ttu-id="cde5d-360">Décimal</span><span class="sxs-lookup"><span data-stu-id="cde5d-360">Decimal</span></span> |
| <span data-ttu-id="cde5d-361">nvarchar</span><span class="sxs-lookup"><span data-stu-id="cde5d-361">nvarchar</span></span> |<span data-ttu-id="cde5d-362">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="cde5d-362">String, Char[]</span></span> |
| <span data-ttu-id="cde5d-363">real</span><span class="sxs-lookup"><span data-stu-id="cde5d-363">real</span></span> |<span data-ttu-id="cde5d-364">Single</span><span class="sxs-lookup"><span data-stu-id="cde5d-364">Single</span></span> |
| <span data-ttu-id="cde5d-365">rowversion</span><span class="sxs-lookup"><span data-stu-id="cde5d-365">rowversion</span></span> |<span data-ttu-id="cde5d-366">Byte[]</span><span class="sxs-lookup"><span data-stu-id="cde5d-366">Byte[]</span></span> |
| <span data-ttu-id="cde5d-367">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="cde5d-367">smalldatetime</span></span> |<span data-ttu-id="cde5d-368">DateTime</span><span class="sxs-lookup"><span data-stu-id="cde5d-368">DateTime</span></span> |
| <span data-ttu-id="cde5d-369">smallint</span><span class="sxs-lookup"><span data-stu-id="cde5d-369">smallint</span></span> |<span data-ttu-id="cde5d-370">Int16</span><span class="sxs-lookup"><span data-stu-id="cde5d-370">Int16</span></span> |
| <span data-ttu-id="cde5d-371">smallmoney</span><span class="sxs-lookup"><span data-stu-id="cde5d-371">smallmoney</span></span> |<span data-ttu-id="cde5d-372">Décimal</span><span class="sxs-lookup"><span data-stu-id="cde5d-372">Decimal</span></span> |
| <span data-ttu-id="cde5d-373">sql_variant</span><span class="sxs-lookup"><span data-stu-id="cde5d-373">sql_variant</span></span> |<span data-ttu-id="cde5d-374">Objet *</span><span class="sxs-lookup"><span data-stu-id="cde5d-374">Object *</span></span> |
| <span data-ttu-id="cde5d-375">texte</span><span class="sxs-lookup"><span data-stu-id="cde5d-375">text</span></span> |<span data-ttu-id="cde5d-376">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="cde5d-376">String, Char[]</span></span> |
| <span data-ttu-id="cde5d-377">time</span><span class="sxs-lookup"><span data-stu-id="cde5d-377">time</span></span> |<span data-ttu-id="cde5d-378">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="cde5d-378">TimeSpan</span></span> |
| <span data-ttu-id="cde5d-379">timestamp</span><span class="sxs-lookup"><span data-stu-id="cde5d-379">timestamp</span></span> |<span data-ttu-id="cde5d-380">Byte[]</span><span class="sxs-lookup"><span data-stu-id="cde5d-380">Byte[]</span></span> |
| <span data-ttu-id="cde5d-381">tinyint</span><span class="sxs-lookup"><span data-stu-id="cde5d-381">tinyint</span></span> |<span data-ttu-id="cde5d-382">Byte</span><span class="sxs-lookup"><span data-stu-id="cde5d-382">Byte</span></span> |
| <span data-ttu-id="cde5d-383">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="cde5d-383">uniqueidentifier</span></span> |<span data-ttu-id="cde5d-384">Guid</span><span class="sxs-lookup"><span data-stu-id="cde5d-384">Guid</span></span> |
| <span data-ttu-id="cde5d-385">varbinary</span><span class="sxs-lookup"><span data-stu-id="cde5d-385">varbinary</span></span> |<span data-ttu-id="cde5d-386">Byte[]</span><span class="sxs-lookup"><span data-stu-id="cde5d-386">Byte[]</span></span> |
| <span data-ttu-id="cde5d-387">varchar</span><span class="sxs-lookup"><span data-stu-id="cde5d-387">varchar</span></span> |<span data-ttu-id="cde5d-388">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="cde5d-388">String, Char[]</span></span> |
| <span data-ttu-id="cde5d-389">xml</span><span class="sxs-lookup"><span data-stu-id="cde5d-389">xml</span></span> |<span data-ttu-id="cde5d-390">xml</span><span class="sxs-lookup"><span data-stu-id="cde5d-390">Xml</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="cde5d-391">Mapper les colonnes source aux colonnes de récepteur</span><span class="sxs-lookup"><span data-stu-id="cde5d-391">Map source to sink columns</span></span>
<span data-ttu-id="cde5d-392">Pour en savoir plus sur le mappage de colonnes du jeu de données source à des colonnes du jeu de données récepteur, voir [Mappage des colonnes d’un jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="cde5d-392">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="cde5d-393">Copie renouvelée</span><span class="sxs-lookup"><span data-stu-id="cde5d-393">Repeatable copy</span></span>
<span data-ttu-id="cde5d-394">Lors de la copie de données sur une base de données SQL Server, l’activité de copie ajoute des données à la table de récepteur par défaut.</span><span class="sxs-lookup"><span data-stu-id="cde5d-394">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="cde5d-395">Pour effectuer une opération UPSERT à la place, consultez l’article [Écriture renouvelée sur SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink).</span><span class="sxs-lookup"><span data-stu-id="cde5d-395">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="cde5d-396">Lorsque vous copiez des données à partir de magasins de données relationnels, gardez à l’esprit la répétabilité de l’opération, afin d’éviter des résultats imprévus.</span><span class="sxs-lookup"><span data-stu-id="cde5d-396">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="cde5d-397">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="cde5d-397">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="cde5d-398">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="cde5d-398">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="cde5d-399">Lorsqu’une tranche est réexécutée d’une manière ou d’une autre, vous devez vous assurer que les mêmes données sont lues et ce, quel que soit le nombre d’exécutions de la tranche.</span><span class="sxs-lookup"><span data-stu-id="cde5d-399">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="cde5d-400">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="cde5d-400">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="cde5d-401">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="cde5d-401">Performance and Tuning</span></span>
<span data-ttu-id="cde5d-402">Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="cde5d-402">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
