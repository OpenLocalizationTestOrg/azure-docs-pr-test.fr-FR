---
title: "Déplacer des données vers/depuis Azure Table | Microsoft Docs"
description: "Découvrez comment déplacer des données depuis et vers le stockage Azure Table à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 792a551ae3dae46c503e5f0dda74cd0ac3a69c3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-azure-table-using-azure-data-factory"></a><span data-ttu-id="0fab6-103">Déplacer des données vers et depuis Azure Table à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="0fab6-103">Move data to and from Azure Table using Azure Data Factory</span></span>
<span data-ttu-id="0fab6-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour déplacer des données vers ou à partir du Stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="0fab6-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Table Storage.</span></span> <span data-ttu-id="0fab6-105">Il s’appuie sur l’article [Activités de déplacement des données](data-factory-data-movement-activities.md), qui présente une vue d’ensemble du déplacement de données avec l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="0fab6-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="0fab6-106">Vous pouvez copier des données à partir de tout magasin de données source pris en charge vers le Stockage Table Azure, ou entre ce dernier et tout magasin de données récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="0fab6-106">You can copy data from any supported source data store to Azure Table Storage or from Azure Table Storage to any supported sink data store.</span></span> <span data-ttu-id="0fab6-107">Pour obtenir la liste des magasins de données pris en charge en tant que sources ou récepteurs pour l’activité de copie, consultez le tableau [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="0fab6-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="0fab6-108">Prise en main</span><span class="sxs-lookup"><span data-stu-id="0fab6-108">Getting started</span></span>
<span data-ttu-id="0fab6-109">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers/depuis un Stockage Table Azure à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="0fab6-109">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span></span>

<span data-ttu-id="0fab6-110">Le moyen le plus simple de créer un pipeline consiste à utiliser l’**Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="0fab6-110">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="0fab6-111">Consultez la page [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant Copier des données.</span><span class="sxs-lookup"><span data-stu-id="0fab6-111">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="0fab6-112">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="0fab6-112">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="0fab6-113">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="0fab6-113">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="0fab6-114">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="0fab6-114">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="0fab6-115">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="0fab6-115">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="0fab6-116">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="0fab6-116">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="0fab6-117">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="0fab6-117">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="0fab6-118">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="0fab6-118">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="0fab6-119">Lorsque vous utilisez des outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory au format JSON.</span><span class="sxs-lookup"><span data-stu-id="0fab6-119">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="0fab6-120">Pour obtenir des exemples comportant des définitions JSON pour les entités Data Factory utilisées pour copier les données vers ou à partir du Stockage Table Azure, consultez la section [Exemples JSON](#json-examples) de cet article.</span><span class="sxs-lookup"><span data-stu-id="0fab6-120">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="0fab6-121">Les sections suivantes offrent des informations détaillées sur les propriétés JSON utilisées pour définir les entités Data Factory propres au Stockage Table Azure :</span><span class="sxs-lookup"><span data-stu-id="0fab6-121">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Table Storage:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="0fab6-122">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="0fab6-122">Linked service properties</span></span>
<span data-ttu-id="0fab6-123">Il existe deux types de services liés que vous pouvez utiliser pour lier un stockage d'objets blob Azure à une fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="0fab6-123">There are two types of linked services you can use to link an Azure blob storage to an Azure data factory.</span></span> <span data-ttu-id="0fab6-124">Il s’agit des services liés **AzureStorage** et **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="0fab6-124">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="0fab6-125">Le service lié Azure Storage fournit à la fabrique de données un accès global à Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0fab6-125">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="0fab6-126">Tandis que le service lié Azure de stockage SAP (signature d'accès partagé) fournit à la fabrique de données un accès restreint/limité dans le temps à Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0fab6-126">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span></span> <span data-ttu-id="0fab6-127">Il n'existe aucune différence entre ces deux services liés.</span><span class="sxs-lookup"><span data-stu-id="0fab6-127">There are no other differences between these two linked services.</span></span> <span data-ttu-id="0fab6-128">Choisissez le service lié qui répond à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="0fab6-128">Choose the linked service that suits your needs.</span></span> <span data-ttu-id="0fab6-129">Les sections suivantes expliquent plus en détail ces deux services liés.</span><span class="sxs-lookup"><span data-stu-id="0fab6-129">The following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="0fab6-130">Propriétés de jeu de données</span><span class="sxs-lookup"><span data-stu-id="0fab6-130">Dataset properties</span></span>
<span data-ttu-id="0fab6-131">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="0fab6-131">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="0fab6-132">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="0fab6-132">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="0fab6-133">La section typeProperties est différente pour chaque type de jeu de données et fournit des informations sur l'emplacement des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="0fab6-133">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="0fab6-134">La section **typeProperties** pour le jeu de données de type **AzureTable** a les propriétés suivantes.</span><span class="sxs-lookup"><span data-stu-id="0fab6-134">The **typeProperties** section for the dataset of type **AzureTable** has the following properties.</span></span>

| <span data-ttu-id="0fab6-135">Propriété</span><span class="sxs-lookup"><span data-stu-id="0fab6-135">Property</span></span> | <span data-ttu-id="0fab6-136">Description</span><span class="sxs-lookup"><span data-stu-id="0fab6-136">Description</span></span> | <span data-ttu-id="0fab6-137">Requis</span><span class="sxs-lookup"><span data-stu-id="0fab6-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0fab6-138">TableName</span><span class="sxs-lookup"><span data-stu-id="0fab6-138">tableName</span></span> |<span data-ttu-id="0fab6-139">Nom de la table dans l'instance de base de données Table Azure à laquelle le service lié fait référence.</span><span class="sxs-lookup"><span data-stu-id="0fab6-139">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="0fab6-140">Oui.</span><span class="sxs-lookup"><span data-stu-id="0fab6-140">Yes.</span></span> <span data-ttu-id="0fab6-141">Lorsqu’un tableName est spécifié sans azureTableSourceQuery, tous les enregistrements de la table sont copiés vers la destination.</span><span class="sxs-lookup"><span data-stu-id="0fab6-141">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="0fab6-142">Si un azureTableSourceQuery est également spécifié, les enregistrements de la table qui satisfont à la requête sont copiés vers la destination.</span><span class="sxs-lookup"><span data-stu-id="0fab6-142">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

### <a name="schema-by-data-factory"></a><span data-ttu-id="0fab6-143">Schéma par Data Factory</span><span class="sxs-lookup"><span data-stu-id="0fab6-143">Schema by Data Factory</span></span>
<span data-ttu-id="0fab6-144">Pour les magasins de données sans schéma comme Azure Table, le service Data Factory déduit le schéma de l’une des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="0fab6-144">For schema-free data stores such as Azure Table, the Data Factory service infers the schema in one of the following ways:</span></span>

1. <span data-ttu-id="0fab6-145">Si vous spécifiez la structure des données à l’aide de la propriété **structure** dans la définition du jeu de données, le service Data Factory respecte cette structure en tant que schéma.</span><span class="sxs-lookup"><span data-stu-id="0fab6-145">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="0fab6-146">Dans ce cas, si une ligne ne contient pas de valeur pour une colonne, une valeur null est fournie pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="0fab6-146">In this case, if a row does not contain a value for a column, a null value is provided for it.</span></span>
2. <span data-ttu-id="0fab6-147">Si vous ne spécifiez pas la structure des données à l’aide de la propriété **structure** dans la définition du jeu de données, Data Factory déduit le schéma à l’aide de la première ligne dans les données.</span><span class="sxs-lookup"><span data-stu-id="0fab6-147">If you don't specify the structure of data by using the **structure** property in the dataset definition, Data Factory infers the schema by using the first row in the data.</span></span> <span data-ttu-id="0fab6-148">Dans ce cas, si la première ligne ne contient pas le schéma complet, certaines colonnes ne sont pas incluses dans le résultat de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="0fab6-148">In this case, if the first row does not contain the full schema, some columns are missed in the result of copy operation.</span></span>

<span data-ttu-id="0fab6-149">Par conséquent, pour les sources de données sans schéma, la meilleure pratique consiste à définir la structure des données à l’aide de la propriété **structure** .</span><span class="sxs-lookup"><span data-stu-id="0fab6-149">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="0fab6-150">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0fab6-150">Copy activity properties</span></span>
<span data-ttu-id="0fab6-151">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="0fab6-151">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="0fab6-152">Les propriétés comme le nom, la description, les jeux de données d’entrée et de sortie et les stratégies sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="0fab6-152">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span>

<span data-ttu-id="0fab6-153">En revanche, les propriétés disponibles dans la section typeProperties de l'activité varient pour chaque type d'activité.</span><span class="sxs-lookup"><span data-stu-id="0fab6-153">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="0fab6-154">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="0fab6-154">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="0fab6-155">**AzureTableSource** prend en charge les propriétés suivantes dans la section typeProperties :</span><span class="sxs-lookup"><span data-stu-id="0fab6-155">**AzureTableSource** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="0fab6-156">Propriété</span><span class="sxs-lookup"><span data-stu-id="0fab6-156">Property</span></span> | <span data-ttu-id="0fab6-157">Description</span><span class="sxs-lookup"><span data-stu-id="0fab6-157">Description</span></span> | <span data-ttu-id="0fab6-158">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0fab6-158">Allowed values</span></span> | <span data-ttu-id="0fab6-159">Requis</span><span class="sxs-lookup"><span data-stu-id="0fab6-159">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0fab6-160">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="0fab6-160">azureTableSourceQuery</span></span> |<span data-ttu-id="0fab6-161">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="0fab6-161">Use the custom query to read data.</span></span> |<span data-ttu-id="0fab6-162">Chaîne de requête de table Azure.</span><span class="sxs-lookup"><span data-stu-id="0fab6-162">Azure table query string.</span></span> <span data-ttu-id="0fab6-163">Consultez les exemples dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="0fab6-163">See examples in the next section.</span></span> |<span data-ttu-id="0fab6-164">Non.</span><span class="sxs-lookup"><span data-stu-id="0fab6-164">No.</span></span> <span data-ttu-id="0fab6-165">Lorsqu’un tableName est spécifié sans azureTableSourceQuery, tous les enregistrements de la table sont copiés vers la destination.</span><span class="sxs-lookup"><span data-stu-id="0fab6-165">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="0fab6-166">Si un azureTableSourceQuery est également spécifié, les enregistrements de la table qui satisfont à la requête sont copiés vers la destination.</span><span class="sxs-lookup"><span data-stu-id="0fab6-166">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="0fab6-167">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="0fab6-167">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="0fab6-168">Indiquer si l'exception de la table n'existe pas.</span><span class="sxs-lookup"><span data-stu-id="0fab6-168">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="0fab6-169">TRUE</span><span class="sxs-lookup"><span data-stu-id="0fab6-169">TRUE</span></span><br/><span data-ttu-id="0fab6-170">FALSE</span><span class="sxs-lookup"><span data-stu-id="0fab6-170">FALSE</span></span> |<span data-ttu-id="0fab6-171">Non</span><span class="sxs-lookup"><span data-stu-id="0fab6-171">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="0fab6-172">Exemples azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="0fab6-172">azureTableSourceQuery examples</span></span>
<span data-ttu-id="0fab6-173">Si la colonne de table Azure est de type chaîne :</span><span class="sxs-lookup"><span data-stu-id="0fab6-173">If Azure Table column is of string type:</span></span>

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

<span data-ttu-id="0fab6-174">Si la colonne de table Azure est de type datetime:</span><span class="sxs-lookup"><span data-stu-id="0fab6-174">If Azure Table column is of datetime type:</span></span>

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

<span data-ttu-id="0fab6-175">**AzureTableSink** prend en charge les propriétés suivantes dans la section typeProperties :</span><span class="sxs-lookup"><span data-stu-id="0fab6-175">**AzureTableSink** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="0fab6-176">Propriété</span><span class="sxs-lookup"><span data-stu-id="0fab6-176">Property</span></span> | <span data-ttu-id="0fab6-177">Description</span><span class="sxs-lookup"><span data-stu-id="0fab6-177">Description</span></span> | <span data-ttu-id="0fab6-178">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="0fab6-178">Allowed values</span></span> | <span data-ttu-id="0fab6-179">Requis</span><span class="sxs-lookup"><span data-stu-id="0fab6-179">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0fab6-180">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="0fab6-180">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="0fab6-181">Valeur de clé de partition par défaut qui peut être utilisée par le récepteur.</span><span class="sxs-lookup"><span data-stu-id="0fab6-181">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="0fab6-182">Valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="0fab6-182">A string value.</span></span> |<span data-ttu-id="0fab6-183">Non</span><span class="sxs-lookup"><span data-stu-id="0fab6-183">No</span></span> |
| <span data-ttu-id="0fab6-184">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="0fab6-184">azureTablePartitionKeyName</span></span> |<span data-ttu-id="0fab6-185">Spécifiez le nom de la colonne dont les valeurs sont utilisées comme clés de partition.</span><span class="sxs-lookup"><span data-stu-id="0fab6-185">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="0fab6-186">Si aucune valeur n'est spécifiée, AzureTableDefaultPartitionKeyValue est utilisée comme clé de partition.</span><span class="sxs-lookup"><span data-stu-id="0fab6-186">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="0fab6-187">Nom de colonne.</span><span class="sxs-lookup"><span data-stu-id="0fab6-187">A column name.</span></span> |<span data-ttu-id="0fab6-188">Non</span><span class="sxs-lookup"><span data-stu-id="0fab6-188">No</span></span> |
| <span data-ttu-id="0fab6-189">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="0fab6-189">azureTableRowKeyName</span></span> |<span data-ttu-id="0fab6-190">Spécifiez le nom de la colonne dont les valeurs sont utilisées comme clé de ligne.</span><span class="sxs-lookup"><span data-stu-id="0fab6-190">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="0fab6-191">Si aucune valeur n'est spécifiée, un GUID est utilisé pour chaque ligne.</span><span class="sxs-lookup"><span data-stu-id="0fab6-191">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="0fab6-192">Nom de colonne.</span><span class="sxs-lookup"><span data-stu-id="0fab6-192">A column name.</span></span> |<span data-ttu-id="0fab6-193">Non</span><span class="sxs-lookup"><span data-stu-id="0fab6-193">No</span></span> |
| <span data-ttu-id="0fab6-194">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="0fab6-194">azureTableInsertType</span></span> |<span data-ttu-id="0fab6-195">Le mode d’insertion des données dans une table Azure.</span><span class="sxs-lookup"><span data-stu-id="0fab6-195">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="0fab6-196">Cette propriété détermine le remplacement ou la fusion des valeurs des lignes existantes dans la table de sortie avec des clés de partition et de ligne correspondantes.</span><span class="sxs-lookup"><span data-stu-id="0fab6-196">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="0fab6-197">Consultez [Insertion ou fusion d’entité](https://msdn.microsoft.com/library/azure/hh452241.aspx) et [Insertion ou remplacement d’entité](https://msdn.microsoft.com/library/azure/hh452242.aspx) pour en savoir plus sur le fonctionnement de ces paramètres (fusion et remplacement).</span><span class="sxs-lookup"><span data-stu-id="0fab6-197">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="0fab6-198">Ce paramètre s’applique au niveau de la ligne, non au niveau de la table, et aucune option ne supprime des lignes de la table de sortie qui n’existent pas dans l’entrée.</span><span class="sxs-lookup"><span data-stu-id="0fab6-198">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="0fab6-199">fusionner (par défaut)</span><span class="sxs-lookup"><span data-stu-id="0fab6-199">merge (default)</span></span><br/><span data-ttu-id="0fab6-200">remplacer</span><span class="sxs-lookup"><span data-stu-id="0fab6-200">replace</span></span> |<span data-ttu-id="0fab6-201">Non</span><span class="sxs-lookup"><span data-stu-id="0fab6-201">No</span></span> |
| <span data-ttu-id="0fab6-202">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="0fab6-202">writeBatchSize</span></span> |<span data-ttu-id="0fab6-203">Insère des données dans la table Azure lorsque la valeur de writeBatchSize ou writeBatchTimeout est atteinte.</span><span class="sxs-lookup"><span data-stu-id="0fab6-203">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="0fab6-204">Nombre entier (nombre de lignes)</span><span class="sxs-lookup"><span data-stu-id="0fab6-204">Integer (number of rows)</span></span> |<span data-ttu-id="0fab6-205">Non (valeur par défaut : 10000)</span><span class="sxs-lookup"><span data-stu-id="0fab6-205">No (default: 10000)</span></span> |
| <span data-ttu-id="0fab6-206">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="0fab6-206">writeBatchTimeout</span></span> |<span data-ttu-id="0fab6-207">Insère des données dans la table Azure lorsque la valeur de writeBatchSize ou writeBatchTimeout est atteinte</span><span class="sxs-lookup"><span data-stu-id="0fab6-207">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="0fab6-208">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="0fab6-208">timespan</span></span><br/><br/><span data-ttu-id="0fab6-209">Exemple : « 00: 20:00 » (20 minutes)</span><span class="sxs-lookup"><span data-stu-id="0fab6-209">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="0fab6-210">Non (Valeur par défaut du délai d'attente du stockage client par défaut : 90 secondes)</span><span class="sxs-lookup"><span data-stu-id="0fab6-210">No (Default to storage client default timeout value 90 sec)</span></span> |

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="0fab6-211">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="0fab6-211">azureTablePartitionKeyName</span></span>
<span data-ttu-id="0fab6-212">Mappez une colonne source sur une colonne de destination à l’aide de la propriété JSON translator pour pouvoir utiliser la colonne de destination comme azureTablePartitionKeyName.</span><span class="sxs-lookup"><span data-stu-id="0fab6-212">Map a source column to a destination column using the translator JSON property before you can use the destination column as the azureTablePartitionKeyName.</span></span>

<span data-ttu-id="0fab6-213">Dans l’exemple suivant, la colonne source DivisionID est mappée sur la colonne de destination DivisionID.</span><span class="sxs-lookup"><span data-stu-id="0fab6-213">In the following example, source column DivisionID is mapped to the destination column: DivisionID.</span></span>  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
<span data-ttu-id="0fab6-214">DivisionID est spécifié en tant que clé de partition.</span><span class="sxs-lookup"><span data-stu-id="0fab6-214">The DivisionID is specified as the partition key.</span></span>

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a><span data-ttu-id="0fab6-215">Exemples JSON</span><span class="sxs-lookup"><span data-stu-id="0fab6-215">JSON examples</span></span>
<span data-ttu-id="0fab6-216">Les exemples suivants présentent des exemples de définitions de JSON que vous pouvez utiliser pour créer un pipeline à l’aide [du Portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [de Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [d’Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0fab6-216">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="0fab6-217">Ils indiquent comment copier des données vers et depuis Azure Table Storage et une base de données Azure d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="0fab6-217">They show how to copy data to and from Azure Table Storage and Azure Blob Database.</span></span> <span data-ttu-id="0fab6-218">Toutefois, les données peuvent être copiées **directement** à partir de n’importe quelle source, vers n’importe quel récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="0fab6-218">However, data can be copied **directly** from any of the sources to any of the supported sinks.</span></span> <span data-ttu-id="0fab6-219">Pour plus d’informations, consultez la section « Banques de données et formats pris en charge » de l’article [Déplacer des données à l’aide de l’activité de copie](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="0fab6-219">For more information, see the section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>

## <a name="example-copy-data-from-azure-table-to-azure-blob"></a><span data-ttu-id="0fab6-220">Exemple : copie de données à partir de Table Azure vers un objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="0fab6-220">Example: Copy data from Azure Table to Azure Blob</span></span>
<span data-ttu-id="0fab6-221">L’exemple suivant montre :</span><span class="sxs-lookup"><span data-stu-id="0fab6-221">The following sample shows:</span></span>

1. <span data-ttu-id="0fab6-222">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (utilisé pour la table et l’objet blob).</span><span class="sxs-lookup"><span data-stu-id="0fab6-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span></span>
2. <span data-ttu-id="0fab6-223">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0fab6-223">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
3. <span data-ttu-id="0fab6-224">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0fab6-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="0fab6-225">Le [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [AzureTableSource](#activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0fab6-225">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="0fab6-226">L'exemple copie des données appartenant à la partition par défaut dans une Table Azure vers un objet Blob, toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="0fab6-226">The sample copies data belonging to the default partition in an Azure Table to a blob every hour.</span></span> <span data-ttu-id="0fab6-227">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="0fab6-227">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="0fab6-228">**Service lié Azure Storage :**</span><span class="sxs-lookup"><span data-stu-id="0fab6-228">**Azure storage linked service:**</span></span>

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
<span data-ttu-id="0fab6-229">Azure Data Factory prend en charge deux types de service lié Azure Storage : **AzureStorage** et **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="0fab6-229">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="0fab6-230">Pour le premier, vous spécifiez la chaîne de connexion qui inclut la clé de compte, et pour le second, vous spécifiez l'Uri de signature d’accès partagé (SAP).</span><span class="sxs-lookup"><span data-stu-id="0fab6-230">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="0fab6-231">Pour plus d’informations, consultez la section [Services liés](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="0fab6-231">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="0fab6-232">**Jeu de données d'entrée Table Azure :**</span><span class="sxs-lookup"><span data-stu-id="0fab6-232">**Azure Table input dataset:**</span></span>

<span data-ttu-id="0fab6-233">L'exemple suppose que vous avez créé une table « MyTable » dans la Table Azure.</span><span class="sxs-lookup"><span data-stu-id="0fab6-233">The sample assumes you have created a table “MyTable” in Azure Table.</span></span>

<span data-ttu-id="0fab6-234">La définition de « external » : « true» informe le service Data Factory qu’il s’agit d’un jeu de données qui est externe à Data Factory et non produit par une activité dans Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0fab6-234">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureTableInput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

<span data-ttu-id="0fab6-235">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="0fab6-235">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="0fab6-236">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="0fab6-236">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="0fab6-237">Le chemin d’accès du dossier pour l’objet blob est évalué dynamiquement en fonction de l’heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="0fab6-237">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="0fab6-238">Le chemin d'accès du dossier utilise l'année, le mois, le jour et l'heure de l'heure de début.</span><span class="sxs-lookup"><span data-stu-id="0fab6-238">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="0fab6-239">**Activité de copie dans un pipeline avec AzureTableSource et BlobSink :**</span><span class="sxs-lookup"><span data-stu-id="0fab6-239">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span></span>

<span data-ttu-id="0fab6-240">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="0fab6-240">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="0fab6-241">Dans la définition du pipeline JSON, le type **source** est défini sur **AzureTableSource** et le type **sink** est défini sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="0fab6-241">In the pipeline JSON definition, the **source** type is set to **AzureTableSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="0fab6-242">La requête SQL spécifiée avec la propriété **AzureTableSourceQuery** sélectionne les données à copier de la partition par défaut toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="0fab6-242">The SQL query specified with **AzureTableSourceQuery** property selects the data from the default partition every hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "AzureTabletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                      {
                        "name": "AzureTableInput"
                    }
                ],
                "outputs": [
                      {
                            "name": "AzureBlobOutput"
                      }
                ],
                "typeProperties": {
                      "source": {
                        "type": "AzureTableSource",
                        "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
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

## <a name="example-copy-data-from-azure-blob-to-azure-table"></a><span data-ttu-id="0fab6-243">Exemple : copie de données à partir d'un objet Blob Azure vers Table Azure</span><span class="sxs-lookup"><span data-stu-id="0fab6-243">Example: Copy data from Azure Blob to Azure Table</span></span>
<span data-ttu-id="0fab6-244">L’exemple suivant montre :</span><span class="sxs-lookup"><span data-stu-id="0fab6-244">The following sample shows:</span></span>

1. <span data-ttu-id="0fab6-245">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (utilisé pour la table et l’objet blob)</span><span class="sxs-lookup"><span data-stu-id="0fab6-245">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span></span>
2. <span data-ttu-id="0fab6-246">un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0fab6-246">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="0fab6-247">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0fab6-247">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
4. <span data-ttu-id="0fab6-248">Le [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) et [AzureTableSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0fab6-248">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span></span>

<span data-ttu-id="0fab6-249">L’exemple copie des données de série horaire à partir d’un objet blob Azure vers une table Azure, toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="0fab6-249">The sample copies time-series data from an Azure blob to an Azure table hourly.</span></span> <span data-ttu-id="0fab6-250">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="0fab6-250">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="0fab6-251">**Service lié Azure Storage (pour Table Azure et objet Blob Azure) :**</span><span class="sxs-lookup"><span data-stu-id="0fab6-251">**Azure storage (for both Azure Table & Blob) linked service:**</span></span>

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

<span data-ttu-id="0fab6-252">Azure Data Factory prend en charge deux types de service lié Azure Storage : **AzureStorage** et **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="0fab6-252">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="0fab6-253">Pour le premier, vous spécifiez la chaîne de connexion qui inclut la clé de compte, et pour le second, vous spécifiez l'Uri de signature d’accès partagé (SAP).</span><span class="sxs-lookup"><span data-stu-id="0fab6-253">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="0fab6-254">Pour plus d’informations, consultez la section [Services liés](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="0fab6-254">See [Linked Services](#linked-service-properties) section for details.</span></span>

<span data-ttu-id="0fab6-255">**Jeu de données d'entrée d'objet Blob Azure :**</span><span class="sxs-lookup"><span data-stu-id="0fab6-255">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="0fab6-256">Les données sont récupérées à partir d'un nouvel objet Blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="0fab6-256">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="0fab6-257">Le nom du chemin d'accès et du fichier de dossier pour l'objet blob sont évalués dynamiquement en fonction de l'heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="0fab6-257">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="0fab6-258">Le chemin d’accès du dossier utilise l’année, le mois et le jour de l’heure de début et le nom de fichier utilise la partie heure de l’heure de début.</span><span class="sxs-lookup"><span data-stu-id="0fab6-258">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="0fab6-259">Le paramètre « external » : « true » informe le service Data Factory que ce jeu de données est externe à la Data Factory et non produit par une activité dans la Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0fab6-259">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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

<span data-ttu-id="0fab6-260">**Jeu de données de sortie Table Azure :**</span><span class="sxs-lookup"><span data-stu-id="0fab6-260">**Azure Table output dataset:**</span></span>

<span data-ttu-id="0fab6-261">L'exemple copie les données dans une table nommée « MyTable » dans Table Azure.</span><span class="sxs-lookup"><span data-stu-id="0fab6-261">The sample copies data to a table named “MyTable” in Azure Table.</span></span> <span data-ttu-id="0fab6-262">Créez une table Azure avec le même nombre de colonnes que le fichier CSV des objets blob doit contenir.</span><span class="sxs-lookup"><span data-stu-id="0fab6-262">Create an Azure table with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="0fab6-263">De nouvelles lignes sont ajoutées à la table toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="0fab6-263">New rows are added to the table every hour.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

<span data-ttu-id="0fab6-264">**Activité de copie dans un pipeline avec BlobSource et AzureTableSink :**</span><span class="sxs-lookup"><span data-stu-id="0fab6-264">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span></span>

<span data-ttu-id="0fab6-265">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="0fab6-265">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="0fab6-266">Dans la définition du pipeline JSON, le type **source** est défini sur **BlobSource** et le type **sink** est défini sur **AzureTableSink**.</span><span class="sxs-lookup"><span data-stu-id="0fab6-266">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **AzureTableSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoTable",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureTableOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "AzureTableSink",
            "writeBatchSize": 100,
            "writeBatchTimeout": "01:00:00"
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
## <a name="type-mapping-for-azure-table"></a><span data-ttu-id="0fab6-267">Mappage de type de Table Azure</span><span class="sxs-lookup"><span data-stu-id="0fab6-267">Type Mapping for Azure Table</span></span>
<span data-ttu-id="0fab6-268">Comme mentionné dans l’article consacré aux [activités de déplacement de données](data-factory-data-movement-activities.md) , l’activité de copie convertit automatiquement les types source en types récepteur à l’aide de l’approche en deux étapes suivante.</span><span class="sxs-lookup"><span data-stu-id="0fab6-268">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span></span>

1. <span data-ttu-id="0fab6-269">Conversion de types natifs source en types .NET</span><span class="sxs-lookup"><span data-stu-id="0fab6-269">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="0fab6-270">Conversion de types .NET en types récepteur natifs</span><span class="sxs-lookup"><span data-stu-id="0fab6-270">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="0fab6-271">Pendant le déplacement de données à partir de et vers Table Azure, les [mappages suivants définis par le service de Table Azure](https://msdn.microsoft.com/library/azure/dd179338.aspx) sont utilisés à partir des types OData Table Azure vers le type .NET et vice versa.</span><span class="sxs-lookup"><span data-stu-id="0fab6-271">When moving data to & from Azure Table, the following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types to .NET type and vice versa.</span></span>

| <span data-ttu-id="0fab6-272">Type de données OData</span><span class="sxs-lookup"><span data-stu-id="0fab6-272">OData Data Type</span></span> | <span data-ttu-id="0fab6-273">Type .NET</span><span class="sxs-lookup"><span data-stu-id="0fab6-273">.NET Type</span></span> | <span data-ttu-id="0fab6-274">Détails</span><span class="sxs-lookup"><span data-stu-id="0fab6-274">Details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0fab6-275">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="0fab6-275">Edm.Binary</span></span> |<span data-ttu-id="0fab6-276">byte[]</span><span class="sxs-lookup"><span data-stu-id="0fab6-276">byte[]</span></span> |<span data-ttu-id="0fab6-277">Tableau d’octets jusqu’à 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="0fab6-277">An array of bytes up to 64 KB.</span></span> |
| <span data-ttu-id="0fab6-278">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="0fab6-278">Edm.Boolean</span></span> |<span data-ttu-id="0fab6-279">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="0fab6-279">bool</span></span> |<span data-ttu-id="0fab6-280">Valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="0fab6-280">A Boolean value.</span></span> |
| <span data-ttu-id="0fab6-281">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="0fab6-281">Edm.DateTime</span></span> |<span data-ttu-id="0fab6-282">DateTime</span><span class="sxs-lookup"><span data-stu-id="0fab6-282">DateTime</span></span> |<span data-ttu-id="0fab6-283">Valeur de 64 bits exprimée en temps universel coordonné (UTC).</span><span class="sxs-lookup"><span data-stu-id="0fab6-283">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="0fab6-284">La plage DateHeure prise en charge commence à partir de 12:00 minuit, le 1er janvier 1601 apr. J.C.</span><span class="sxs-lookup"><span data-stu-id="0fab6-284">The supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="0fab6-285">(NOTRE ÈRE), UTC.</span><span class="sxs-lookup"><span data-stu-id="0fab6-285">(C.E.), UTC.</span></span> <span data-ttu-id="0fab6-286">La plage se termine le 31 décembre 9999.</span><span class="sxs-lookup"><span data-stu-id="0fab6-286">The range ends at December 31, 9999.</span></span> |
| <span data-ttu-id="0fab6-287">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="0fab6-287">Edm.Double</span></span> |<span data-ttu-id="0fab6-288">double</span><span class="sxs-lookup"><span data-stu-id="0fab6-288">double</span></span> |<span data-ttu-id="0fab6-289">Valeur à virgule flottante de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="0fab6-289">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="0fab6-290">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="0fab6-290">Edm.Guid</span></span> |<span data-ttu-id="0fab6-291">Guid</span><span class="sxs-lookup"><span data-stu-id="0fab6-291">Guid</span></span> |<span data-ttu-id="0fab6-292">Identificateur global unique de 128 bits.</span><span class="sxs-lookup"><span data-stu-id="0fab6-292">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="0fab6-293">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="0fab6-293">Edm.Int32</span></span> |<span data-ttu-id="0fab6-294">Int32</span><span class="sxs-lookup"><span data-stu-id="0fab6-294">Int32</span></span> |<span data-ttu-id="0fab6-295">Nombre entier 32 bits.</span><span class="sxs-lookup"><span data-stu-id="0fab6-295">A 32-bit integer.</span></span> |
| <span data-ttu-id="0fab6-296">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="0fab6-296">Edm.Int64</span></span> |<span data-ttu-id="0fab6-297">Int64</span><span class="sxs-lookup"><span data-stu-id="0fab6-297">Int64</span></span> |<span data-ttu-id="0fab6-298">Nombre entier 64 bits.</span><span class="sxs-lookup"><span data-stu-id="0fab6-298">A 64-bit integer.</span></span> |
| <span data-ttu-id="0fab6-299">Edm.String</span><span class="sxs-lookup"><span data-stu-id="0fab6-299">Edm.String</span></span> |<span data-ttu-id="0fab6-300">String</span><span class="sxs-lookup"><span data-stu-id="0fab6-300">String</span></span> |<span data-ttu-id="0fab6-301">Valeur encodée en UTF-16.</span><span class="sxs-lookup"><span data-stu-id="0fab6-301">A UTF-16-encoded value.</span></span> <span data-ttu-id="0fab6-302">Les valeurs de chaîne peuvent aller jusqu’à 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="0fab6-302">String values may be up to 64 KB.</span></span> |

### <a name="type-conversion-sample"></a><span data-ttu-id="0fab6-303">Exemple de conversion de type</span><span class="sxs-lookup"><span data-stu-id="0fab6-303">Type Conversion Sample</span></span>
<span data-ttu-id="0fab6-304">L'exemple suivant montre la copie de données à partir d'un objet Blob Azure vers Table Azure avec des conversions de type.</span><span class="sxs-lookup"><span data-stu-id="0fab6-304">The following sample is for copying data from an Azure Blob to Azure Table with type conversions.</span></span>

<span data-ttu-id="0fab6-305">Supposons que le jeu de données Blob soit au format CSV et contienne trois colonnes.</span><span class="sxs-lookup"><span data-stu-id="0fab6-305">Suppose the Blob dataset is in CSV format and contains three columns.</span></span> <span data-ttu-id="0fab6-306">L'une d'elles est une colonne datetime avec un format de date et d'heure personnalisé comprenant un nom abrégé en français pour le jour de la semaine.</span><span class="sxs-lookup"><span data-stu-id="0fab6-306">One of them is a datetime column with a custom datetime format using abbreviated French names for day of the week.</span></span>

<span data-ttu-id="0fab6-307">Définissez le jeu de données des objets blob source comme suit, ainsi que des définitions de type pour les colonnes.</span><span class="sxs-lookup"><span data-stu-id="0fab6-307">Define the Blob Source dataset as follows along with type definitions for the columns.</span></span>

```JSON
{
    "name": " AzureBlobInput",
    "properties":
    {
         "structure":
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1,
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
<span data-ttu-id="0fab6-308">Étant donné le mappage de type OData Table Azure vers le type .NET, vous devez définir la table dans Table Azure avec le schéma suivant.</span><span class="sxs-lookup"><span data-stu-id="0fab6-308">Given the type mapping from Azure Table OData type to .NET type, you would define the table in Azure Table with the following schema.</span></span>

<span data-ttu-id="0fab6-309">**Schéma de Table Azure :**</span><span class="sxs-lookup"><span data-stu-id="0fab6-309">**Azure Table schema:**</span></span>

| <span data-ttu-id="0fab6-310">Nom de la colonne</span><span class="sxs-lookup"><span data-stu-id="0fab6-310">Column name</span></span> | <span data-ttu-id="0fab6-311">Type</span><span class="sxs-lookup"><span data-stu-id="0fab6-311">Type</span></span> |
| --- | --- |
| <span data-ttu-id="0fab6-312">userid</span><span class="sxs-lookup"><span data-stu-id="0fab6-312">userid</span></span> |<span data-ttu-id="0fab6-313">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="0fab6-313">Edm.Int64</span></span> |
| <span data-ttu-id="0fab6-314">name</span><span class="sxs-lookup"><span data-stu-id="0fab6-314">name</span></span> |<span data-ttu-id="0fab6-315">Edm.String</span><span class="sxs-lookup"><span data-stu-id="0fab6-315">Edm.String</span></span> |
| <span data-ttu-id="0fab6-316">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="0fab6-316">lastlogindate</span></span> |<span data-ttu-id="0fab6-317">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="0fab6-317">Edm.DateTime</span></span> |

<span data-ttu-id="0fab6-318">Ensuite, définissez le jeu de données Table Azure comme suit.</span><span class="sxs-lookup"><span data-stu-id="0fab6-318">Next, define the Azure Table dataset as follows.</span></span> <span data-ttu-id="0fab6-319">Il est inutile de spécifier la section « structure » à l'aide des informations de type, car celles-ci sont déjà spécifiées dans le magasin de données sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="0fab6-319">You do not need to specify “structure” section with the type information since the type information is already specified in the underlying data store.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

<span data-ttu-id="0fab6-320">Dans ce cas, Data Factory effectue automatiquement les conversions de type, y compris pour le champ Datetime avec son format date/heure personnalisé, en utilisant la culture fr-fr lors du déplacement des données à partir de l’objet blob vers Table Azure.</span><span class="sxs-lookup"><span data-stu-id="0fab6-320">In this case, Data Factory automatically does type conversions including the Datetime field with the custom datetime format using the "fr-fr" culture when moving data from Blob to Azure Table.</span></span>

> [!NOTE]
> <span data-ttu-id="0fab6-321">Pour savoir comment mapper des colonnes d’un jeu de données source à des colonnes d’un jeu de données récepteur, consultez [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Mappage des colonnes des jeux de données dans Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="0fab6-321">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="0fab6-322">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="0fab6-322">Performance and Tuning</span></span>
<span data-ttu-id="0fab6-323">Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="0fab6-323">To learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
