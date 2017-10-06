---
title: "les données d’aaaMove vers/à partir de la Table Azure | Documents Microsoft"
description: "Découvrez comment les données de toomove vers/depuis le stockage de Table Azure à l’aide d’Azure Data Factory."
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
ms.openlocfilehash: 3dc3da6d88854674a9108b600534bc5d07575f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-table-using-azure-data-factory"></a><span data-ttu-id="8b972-103">Déplacer les données tooand à partir de la Table Azure à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="8b972-103">Move data tooand from Azure Table using Azure Data Factory</span></span>
<span data-ttu-id="8b972-104">Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory vers ou depuis le stockage de Table Azure.</span><span class="sxs-lookup"><span data-stu-id="8b972-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure Table Storage.</span></span> <span data-ttu-id="8b972-105">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="8b972-106">Vous pouvez copier les données de toute source pris en charge stocker tooAzure le stockage de Table de données ou à partir de données de récepteur tooany pris en charge le stockage Table store.</span><span class="sxs-lookup"><span data-stu-id="8b972-106">You can copy data from any supported source data store tooAzure Table Storage or from Azure Table Storage tooany supported sink data store.</span></span> <span data-ttu-id="8b972-107">Pour obtenir la liste des magasins de données pris en charge en tant que sources ou récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="8b972-107">For a list of data stores supported as sources or sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="8b972-108">Prise en main</span><span class="sxs-lookup"><span data-stu-id="8b972-108">Getting started</span></span>
<span data-ttu-id="8b972-109">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers/depuis un Stockage Table Azure à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="8b972-109">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span></span>

<span data-ttu-id="8b972-110">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="8b972-110">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="8b972-111">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-111">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="8b972-112">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="8b972-112">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="8b972-113">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="8b972-113">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="8b972-114">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="8b972-114">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="8b972-115">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="8b972-115">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="8b972-116">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-116">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="8b972-117">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="8b972-117">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="8b972-118">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="8b972-118">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="8b972-119">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-119">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="8b972-120">Pour plus d’exemples de définitions de JSON pour les entités de fabrique de données qui sont utilisés toocopy des données vers/depuis un stockage de tables Azure, consultez [exemples JSON](#json-examples) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="8b972-120">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="8b972-121">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifique tooAzure le stockage de Table :</span><span class="sxs-lookup"><span data-stu-id="8b972-121">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Table Storage:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="8b972-122">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="8b972-122">Linked service properties</span></span>
<span data-ttu-id="8b972-123">Il existe deux types de services liés, vous pouvez utiliser toolink une fabrique de données Azure tooan stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="8b972-123">There are two types of linked services you can use toolink an Azure blob storage tooan Azure data factory.</span></span> <span data-ttu-id="8b972-124">Il s’agit des services liés **AzureStorage** et **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="8b972-124">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="8b972-125">Hello service lié Azure Storage fournit la fabrique de données hello avec accès global toohello le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="8b972-125">hello Azure Storage linked service provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="8b972-126">Alors que hello Azure stockage SAS (Shared Access Signature) lié service fournit fabrique de données hello avec l’accès restreint/temps toohello le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="8b972-126">Whereas, hello Azure Storage SAS (Shared Access Signature) linked service provides hello data factory with restricted/time-bound access toohello Azure Storage.</span></span> <span data-ttu-id="8b972-127">Il n'existe aucune différence entre ces deux services liés.</span><span class="sxs-lookup"><span data-stu-id="8b972-127">There are no other differences between these two linked services.</span></span> <span data-ttu-id="8b972-128">Sélectionnez service hello lié qui correspond le mieux à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="8b972-128">Choose hello linked service that suits your needs.</span></span> <span data-ttu-id="8b972-129">Hello sections suivantes fournissent plus d’informations sur ces deux services liés.</span><span class="sxs-lookup"><span data-stu-id="8b972-129">hello following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="8b972-130">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="8b972-130">Dataset properties</span></span>
<span data-ttu-id="8b972-131">Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="8b972-131">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="8b972-132">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="8b972-132">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="8b972-133">section de typeProperties Hello est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-133">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="8b972-134">Hello **typeProperties** section hello le jeu de données de type **AzureTable** a les propriétés suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-134">hello **typeProperties** section for hello dataset of type **AzureTable** has hello following properties.</span></span>

| <span data-ttu-id="8b972-135">Propriété</span><span class="sxs-lookup"><span data-stu-id="8b972-135">Property</span></span> | <span data-ttu-id="8b972-136">Description</span><span class="sxs-lookup"><span data-stu-id="8b972-136">Description</span></span> | <span data-ttu-id="8b972-137">Requis</span><span class="sxs-lookup"><span data-stu-id="8b972-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b972-138">TableName</span><span class="sxs-lookup"><span data-stu-id="8b972-138">tableName</span></span> |<span data-ttu-id="8b972-139">Nom de table hello dans l’instance de base de données de Table Azure hello ce service lié fait référence à.</span><span class="sxs-lookup"><span data-stu-id="8b972-139">Name of hello table in hello Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="8b972-140">Oui.</span><span class="sxs-lookup"><span data-stu-id="8b972-140">Yes.</span></span> <span data-ttu-id="8b972-141">Lorsqu’un nom de table est spécifié sans un azureTableSourceQuery, tous les enregistrements à partir de la table de hello sont copiés toohello destination.</span><span class="sxs-lookup"><span data-stu-id="8b972-141">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="8b972-142">Si un azureTableSourceQuery est également spécifiée, les enregistrements de la table hello qui répond aux requêtes de hello sont copiés toohello destination.</span><span class="sxs-lookup"><span data-stu-id="8b972-142">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |

### <a name="schema-by-data-factory"></a><span data-ttu-id="8b972-143">Schéma par Data Factory</span><span class="sxs-lookup"><span data-stu-id="8b972-143">Schema by Data Factory</span></span>
<span data-ttu-id="8b972-144">Pour les magasins de données sans schéma comme Table de Azure, hello service Data Factory déduit le schéma de hello dans un des hello suivant façons :</span><span class="sxs-lookup"><span data-stu-id="8b972-144">For schema-free data stores such as Azure Table, hello Data Factory service infers hello schema in one of hello following ways:</span></span>

1. <span data-ttu-id="8b972-145">Si vous spécifiez la structure hello des données à l’aide de hello **structure** propriété dans la définition de dataset hello, hello service Data Factory respecte cette structure en tant que schéma de hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-145">If you specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service honors this structure as hello schema.</span></span> <span data-ttu-id="8b972-146">Dans ce cas, si une ligne ne contient pas de valeur pour une colonne, une valeur null est fournie pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="8b972-146">In this case, if a row does not contain a value for a column, a null value is provided for it.</span></span>
2. <span data-ttu-id="8b972-147">Si vous ne spécifiez pas structure hello des données à l’aide de hello **structure** propriété dans la définition de dataset hello, Data Factory déduit le schéma de hello à l’aide de la première ligne de hello dans les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="8b972-147">If you don't specify hello structure of data by using hello **structure** property in hello dataset definition, Data Factory infers hello schema by using hello first row in hello data.</span></span> <span data-ttu-id="8b972-148">Dans ce cas, si la première ligne de hello ne contient pas de schéma complet de hello, certaines colonnes sont ignorés dans le résultat de hello d’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="8b972-148">In this case, if hello first row does not contain hello full schema, some columns are missed in hello result of copy operation.</span></span>

<span data-ttu-id="8b972-149">Par conséquent, pour les sources de données de schéma, il est recommandé de hello est toospecify hello structure de données à l’aide de hello **structure** propriété.</span><span class="sxs-lookup"><span data-stu-id="8b972-149">Therefore, for schema-free data sources, hello best practice is toospecify hello structure of data using hello **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="8b972-150">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="8b972-150">Copy activity properties</span></span>
<span data-ttu-id="8b972-151">Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="8b972-151">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="8b972-152">Les propriétés comme le nom, la description, les jeux de données d’entrée et de sortie et les stratégies sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="8b972-152">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span>

<span data-ttu-id="8b972-153">Propriétés disponibles dans la section de typeProperties hello d’activité hello sur hello autre part varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="8b972-153">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="8b972-154">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-154">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="8b972-155">**AzureTableSource** prend en charge hello propriétés dans la section de typeProperties suivantes :</span><span class="sxs-lookup"><span data-stu-id="8b972-155">**AzureTableSource** supports hello following properties in typeProperties section:</span></span>

| <span data-ttu-id="8b972-156">Propriété</span><span class="sxs-lookup"><span data-stu-id="8b972-156">Property</span></span> | <span data-ttu-id="8b972-157">Description</span><span class="sxs-lookup"><span data-stu-id="8b972-157">Description</span></span> | <span data-ttu-id="8b972-158">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="8b972-158">Allowed values</span></span> | <span data-ttu-id="8b972-159">Requis</span><span class="sxs-lookup"><span data-stu-id="8b972-159">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b972-160">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="8b972-160">azureTableSourceQuery</span></span> |<span data-ttu-id="8b972-161">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="8b972-161">Use hello custom query tooread data.</span></span> |<span data-ttu-id="8b972-162">Chaîne de requête de table Azure.</span><span class="sxs-lookup"><span data-stu-id="8b972-162">Azure table query string.</span></span> <span data-ttu-id="8b972-163">Consultez les exemples dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-163">See examples in hello next section.</span></span> |<span data-ttu-id="8b972-164">Non.</span><span class="sxs-lookup"><span data-stu-id="8b972-164">No.</span></span> <span data-ttu-id="8b972-165">Lorsqu’un nom de table est spécifié sans un azureTableSourceQuery, tous les enregistrements à partir de la table de hello sont copiés toohello destination.</span><span class="sxs-lookup"><span data-stu-id="8b972-165">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="8b972-166">Si un azureTableSourceQuery est également spécifiée, les enregistrements de la table hello qui répond aux requêtes de hello sont copiés toohello destination.</span><span class="sxs-lookup"><span data-stu-id="8b972-166">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |
| <span data-ttu-id="8b972-167">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="8b972-167">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="8b972-168">Indiquer si exception de hello avale de table n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="8b972-168">Indicate whether swallow hello exception of table not exist.</span></span> |<span data-ttu-id="8b972-169">TRUE</span><span class="sxs-lookup"><span data-stu-id="8b972-169">TRUE</span></span><br/><span data-ttu-id="8b972-170">FALSE</span><span class="sxs-lookup"><span data-stu-id="8b972-170">FALSE</span></span> |<span data-ttu-id="8b972-171">Non</span><span class="sxs-lookup"><span data-stu-id="8b972-171">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="8b972-172">Exemples azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="8b972-172">azureTableSourceQuery examples</span></span>
<span data-ttu-id="8b972-173">Si la colonne de table Azure est de type chaîne :</span><span class="sxs-lookup"><span data-stu-id="8b972-173">If Azure Table column is of string type:</span></span>

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

<span data-ttu-id="8b972-174">Si la colonne de table Azure est de type datetime:</span><span class="sxs-lookup"><span data-stu-id="8b972-174">If Azure Table column is of datetime type:</span></span>

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

<span data-ttu-id="8b972-175">**AzureTableSink** prend en charge hello propriétés dans la section de typeProperties suivantes :</span><span class="sxs-lookup"><span data-stu-id="8b972-175">**AzureTableSink** supports hello following properties in typeProperties section:</span></span>

| <span data-ttu-id="8b972-176">Propriété</span><span class="sxs-lookup"><span data-stu-id="8b972-176">Property</span></span> | <span data-ttu-id="8b972-177">Description</span><span class="sxs-lookup"><span data-stu-id="8b972-177">Description</span></span> | <span data-ttu-id="8b972-178">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="8b972-178">Allowed values</span></span> | <span data-ttu-id="8b972-179">Requis</span><span class="sxs-lookup"><span data-stu-id="8b972-179">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b972-180">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="8b972-180">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="8b972-181">Valeur par défaut partition clé qui peut être utilisé par le récepteur de hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-181">Default partition key value that can be used by hello sink.</span></span> |<span data-ttu-id="8b972-182">Valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="8b972-182">A string value.</span></span> |<span data-ttu-id="8b972-183">Non</span><span class="sxs-lookup"><span data-stu-id="8b972-183">No</span></span> |
| <span data-ttu-id="8b972-184">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="8b972-184">azureTablePartitionKeyName</span></span> |<span data-ttu-id="8b972-185">Spécifiez le nom de colonne hello dont les valeurs sont utilisées comme clés de partition.</span><span class="sxs-lookup"><span data-stu-id="8b972-185">Specify name of hello column whose values are used as partition keys.</span></span> <span data-ttu-id="8b972-186">Si non spécifié, AzureTableDefaultPartitionKeyValue est utilisé comme clé de partition hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-186">If not specified, AzureTableDefaultPartitionKeyValue is used as hello partition key.</span></span> |<span data-ttu-id="8b972-187">Nom de colonne.</span><span class="sxs-lookup"><span data-stu-id="8b972-187">A column name.</span></span> |<span data-ttu-id="8b972-188">Non</span><span class="sxs-lookup"><span data-stu-id="8b972-188">No</span></span> |
| <span data-ttu-id="8b972-189">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="8b972-189">azureTableRowKeyName</span></span> |<span data-ttu-id="8b972-190">Spécifiez le nom de colonne hello dont les valeurs de colonne sont utilisées comme clé de ligne.</span><span class="sxs-lookup"><span data-stu-id="8b972-190">Specify name of hello column whose column values are used as row key.</span></span> <span data-ttu-id="8b972-191">Si aucune valeur n'est spécifiée, un GUID est utilisé pour chaque ligne.</span><span class="sxs-lookup"><span data-stu-id="8b972-191">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="8b972-192">Nom de colonne.</span><span class="sxs-lookup"><span data-stu-id="8b972-192">A column name.</span></span> |<span data-ttu-id="8b972-193">Non</span><span class="sxs-lookup"><span data-stu-id="8b972-193">No</span></span> |
| <span data-ttu-id="8b972-194">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="8b972-194">azureTableInsertType</span></span> |<span data-ttu-id="8b972-195">Hello mode tooinsert les données dans Azure table.</span><span class="sxs-lookup"><span data-stu-id="8b972-195">hello mode tooinsert data into Azure table.</span></span><br/><br/><span data-ttu-id="8b972-196">Cette propriété contrôle si les lignes existantes dans la table de sortie hello avec les clés de partition et de ligne correspondantes ont leurs valeurs remplacé ou fusionnées.</span><span class="sxs-lookup"><span data-stu-id="8b972-196">This property controls whether existing rows in hello output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="8b972-197">toolearn sur le fonctionnement de ces paramètres (fusion et remplacement), consultez [insertion ou l’entité de fusion](https://msdn.microsoft.com/library/azure/hh452241.aspx) et [insérer ou remplacer une entité](https://msdn.microsoft.com/library/azure/hh452242.aspx) rubriques.</span><span class="sxs-lookup"><span data-stu-id="8b972-197">toolearn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="8b972-198">Ce paramètre s’applique au niveau de ligne hello, pas de niveau de table d’hello, et aucune de ces options supprime des lignes dans la table de sortie hello qui n’existent pas dans l’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-198">This setting applies at hello row level, not hello table level, and neither option deletes rows in hello output table that do not exist in hello input.</span></span> |<span data-ttu-id="8b972-199">fusionner (par défaut)</span><span class="sxs-lookup"><span data-stu-id="8b972-199">merge (default)</span></span><br/><span data-ttu-id="8b972-200">remplacer</span><span class="sxs-lookup"><span data-stu-id="8b972-200">replace</span></span> |<span data-ttu-id="8b972-201">Non</span><span class="sxs-lookup"><span data-stu-id="8b972-201">No</span></span> |
| <span data-ttu-id="8b972-202">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="8b972-202">writeBatchSize</span></span> |<span data-ttu-id="8b972-203">Insère des données dans hello table Azure quand la valeur de hello writeBatchSize ou writeBatchTimeout est atteinte.</span><span class="sxs-lookup"><span data-stu-id="8b972-203">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="8b972-204">Nombre entier (nombre de lignes)</span><span class="sxs-lookup"><span data-stu-id="8b972-204">Integer (number of rows)</span></span> |<span data-ttu-id="8b972-205">Non (valeur par défaut : 10000)</span><span class="sxs-lookup"><span data-stu-id="8b972-205">No (default: 10000)</span></span> |
| <span data-ttu-id="8b972-206">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="8b972-206">writeBatchTimeout</span></span> |<span data-ttu-id="8b972-207">Insère des données dans hello table Azure quand la valeur de hello writeBatchSize ou writeBatchTimeout est atteinte</span><span class="sxs-lookup"><span data-stu-id="8b972-207">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="8b972-208">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="8b972-208">timespan</span></span><br/><br/><span data-ttu-id="8b972-209">Exemple : « 00: 20:00 » (20 minutes)</span><span class="sxs-lookup"><span data-stu-id="8b972-209">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="8b972-210">Non (le délai d’expiration de valeur par défaut toostorage client par défaut la valeur 90 s)</span><span class="sxs-lookup"><span data-stu-id="8b972-210">No (Default toostorage client default timeout value 90 sec)</span></span> |

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="8b972-211">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="8b972-211">azureTablePartitionKeyName</span></span>
<span data-ttu-id="8b972-212">Mapper une colonne de destination de tooa de colonne source à l’aide de la propriété JSON de traduction hello avant que vous pouvez utiliser la colonne de destination hello comme hello azureTablePartitionKeyName.</span><span class="sxs-lookup"><span data-stu-id="8b972-212">Map a source column tooa destination column using hello translator JSON property before you can use hello destination column as hello azureTablePartitionKeyName.</span></span>

<span data-ttu-id="8b972-213">Bonjour l’exemple suivant, la colonne de source DivisionID est colonne de destination mappé toohello : DivisionID.</span><span class="sxs-lookup"><span data-stu-id="8b972-213">In hello following example, source column DivisionID is mapped toohello destination column: DivisionID.</span></span>  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
<span data-ttu-id="8b972-214">Hello DivisionID est spécifié en tant que clé de partition hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-214">hello DivisionID is specified as hello partition key.</span></span>

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a><span data-ttu-id="8b972-215">Exemples JSON</span><span class="sxs-lookup"><span data-stu-id="8b972-215">JSON examples</span></span>
<span data-ttu-id="8b972-216">Hello exemples suivants proposent des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8b972-216">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="8b972-217">Elles montrent comment tooand de données toocopy de stockage de Table Azure et base de données des objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="8b972-217">They show how toocopy data tooand from Azure Table Storage and Azure Blob Database.</span></span> <span data-ttu-id="8b972-218">Toutefois, les données peuvent être copiées **directement** de n’importe quelle tooany de sources hello de récepteurs de hello pris en charge.</span><span class="sxs-lookup"><span data-stu-id="8b972-218">However, data can be copied **directly** from any of hello sources tooany of hello supported sinks.</span></span> <span data-ttu-id="8b972-219">Pour plus d’informations, consultez la section hello « magasins de données pris en charge et formats » dans [déplacer des données à l’aide de l’activité de copie](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="8b972-219">For more information, see hello section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>

## <a name="example-copy-data-from-azure-table-tooazure-blob"></a><span data-ttu-id="8b972-220">Exemple : Copier des données à partir de la Table Azure tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="8b972-220">Example: Copy data from Azure Table tooAzure Blob</span></span>
<span data-ttu-id="8b972-221">Hello ci-dessous illustre d’exemple :</span><span class="sxs-lookup"><span data-stu-id="8b972-221">hello following sample shows:</span></span>

1. <span data-ttu-id="8b972-222">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (utilisé pour la table et l’objet blob).</span><span class="sxs-lookup"><span data-stu-id="8b972-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span></span>
2. <span data-ttu-id="8b972-223">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b972-223">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
3. <span data-ttu-id="8b972-224">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b972-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="8b972-225">Hello [pipeline](data-factory-create-pipelines.md) avec l’activité de copie qui utilise [AzureTableSource](#activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b972-225">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="8b972-226">exemple Hello copie les données appartenant à partition par défaut de toohello dans un objet blob tooa de Table Azure toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="8b972-226">hello sample copies data belonging toohello default partition in an Azure Table tooa blob every hour.</span></span> <span data-ttu-id="8b972-227">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-227">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="8b972-228">**Service lié Azure Storage :**</span><span class="sxs-lookup"><span data-stu-id="8b972-228">**Azure storage linked service:**</span></span>

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
<span data-ttu-id="8b972-229">Azure Data Factory prend en charge deux types de service lié Azure Storage : **AzureStorage** et **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="8b972-229">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="8b972-230">Pour hello premier, vous spécifiez la chaîne de connexion hello qui inclut la clé de compte hello et pourquoi une version ultérieure, vous spécifiez hello Uri de Signature d’accès partagé (SAS).</span><span class="sxs-lookup"><span data-stu-id="8b972-230">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="8b972-231">Pour plus d’informations, consultez la section [Services liés](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="8b972-231">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="8b972-232">**Jeu de données d'entrée Table Azure :**</span><span class="sxs-lookup"><span data-stu-id="8b972-232">**Azure Table input dataset:**</span></span>

<span data-ttu-id="8b972-233">exemple Hello suppose que vous avez créé une table « MaTable » dans la Table Azure.</span><span class="sxs-lookup"><span data-stu-id="8b972-233">hello sample assumes you have created a table “MyTable” in Azure Table.</span></span>

<span data-ttu-id="8b972-234">Paramètre « external » : « true » informe service Data Factory de hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-234">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="8b972-235">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="8b972-235">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="8b972-236">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="8b972-236">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="8b972-237">chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="8b972-237">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="8b972-238">chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-238">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="8b972-239">**Activité de copie dans un pipeline avec AzureTableSource et BlobSink :**</span><span class="sxs-lookup"><span data-stu-id="8b972-239">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span></span>

<span data-ttu-id="8b972-240">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="8b972-240">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="8b972-241">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**AzureTableSource** et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="8b972-241">In hello pipeline JSON definition, hello **source** type is set too**AzureTableSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="8b972-242">spécifié avec la requête SQL Hello **AzureTableSourceQuery** propriété sélectionne des données de hello de partition par défaut de hello toocopy de chaque heure.</span><span class="sxs-lookup"><span data-stu-id="8b972-242">hello SQL query specified with **AzureTableSourceQuery** property selects hello data from hello default partition every hour toocopy.</span></span>

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

## <a name="example-copy-data-from-azure-blob-tooazure-table"></a><span data-ttu-id="8b972-243">Exemple : Copier des données d’objets Blob Azure tooAzure Table</span><span class="sxs-lookup"><span data-stu-id="8b972-243">Example: Copy data from Azure Blob tooAzure Table</span></span>
<span data-ttu-id="8b972-244">Hello ci-dessous illustre d’exemple :</span><span class="sxs-lookup"><span data-stu-id="8b972-244">hello following sample shows:</span></span>

1. <span data-ttu-id="8b972-245">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (utilisé pour la table et l’objet blob)</span><span class="sxs-lookup"><span data-stu-id="8b972-245">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span></span>
2. <span data-ttu-id="8b972-246">un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b972-246">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="8b972-247">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b972-247">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
4. <span data-ttu-id="8b972-248">Hello [pipeline](data-factory-create-pipelines.md) avec l’activité de copie qui utilise [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) et [AzureTableSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b972-248">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span></span>

<span data-ttu-id="8b972-249">exemple Hello copie les données de séries chronologiques à partir d’un tooan d’objets blob Azure table Azure toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="8b972-249">hello sample copies time-series data from an Azure blob tooan Azure table hourly.</span></span> <span data-ttu-id="8b972-250">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-250">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="8b972-251">**Service lié Azure Storage (pour Table Azure et objet Blob Azure) :**</span><span class="sxs-lookup"><span data-stu-id="8b972-251">**Azure storage (for both Azure Table & Blob) linked service:**</span></span>

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

<span data-ttu-id="8b972-252">Azure Data Factory prend en charge deux types de service lié Azure Storage : **AzureStorage** et **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="8b972-252">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="8b972-253">Pour hello premier, vous spécifiez la chaîne de connexion hello qui inclut la clé de compte hello et pourquoi une version ultérieure, vous spécifiez hello Uri de Signature d’accès partagé (SAS).</span><span class="sxs-lookup"><span data-stu-id="8b972-253">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="8b972-254">Pour plus d’informations, consultez la section [Services liés](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="8b972-254">See [Linked Services](#linked-service-properties) section for details.</span></span>

<span data-ttu-id="8b972-255">**Jeu de données d'entrée d'objet Blob Azure :**</span><span class="sxs-lookup"><span data-stu-id="8b972-255">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="8b972-256">Les données sont récupérées à partir d'un nouvel objet Blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="8b972-256">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="8b972-257">nom de chemin d’accès et de dossier pour l’objet blob de hello Hello sont dynamiquement évaluées en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="8b972-257">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="8b972-258">chemin d’accès du dossier Hello utilise la partie jour de l’heure de début hello, mois et année et nom de fichier partie d’heure hello de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-258">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="8b972-259">« external » : « true » paramètre informe le service de fabrique de données de hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-259">“external”: “true” setting informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="8b972-260">**Jeu de données de sortie Table Azure :**</span><span class="sxs-lookup"><span data-stu-id="8b972-260">**Azure Table output dataset:**</span></span>

<span data-ttu-id="8b972-261">exemple Hello copie table tooa de données nommé « MyTable » dans la Table Azure.</span><span class="sxs-lookup"><span data-stu-id="8b972-261">hello sample copies data tooa table named “MyTable” in Azure Table.</span></span> <span data-ttu-id="8b972-262">Créer une table Azure avec hello même nombre de colonnes comme vous le souhaitez toocontain de fichier CSV d’objets Blob hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-262">Create an Azure table with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="8b972-263">Nouvelles lignes sont ajoutées à la table de toohello toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="8b972-263">New rows are added toohello table every hour.</span></span>

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

<span data-ttu-id="8b972-264">**Activité de copie dans un pipeline avec BlobSource et AzureTableSink :**</span><span class="sxs-lookup"><span data-stu-id="8b972-264">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span></span>

<span data-ttu-id="8b972-265">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="8b972-265">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="8b972-266">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**BlobSource** et **récepteur** type est défini trop**AzureTableSink**.</span><span class="sxs-lookup"><span data-stu-id="8b972-266">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**AzureTableSink**.</span></span>

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
## <a name="type-mapping-for-azure-table"></a><span data-ttu-id="8b972-267">Mappage de type de Table Azure</span><span class="sxs-lookup"><span data-stu-id="8b972-267">Type Mapping for Azure Table</span></span>
<span data-ttu-id="8b972-268">Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, l’activité de copie effectue les conversions de type automatique à partir de types de sources de toosink types avec hello suivant l’approche en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="8b972-268">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach.</span></span>

1. <span data-ttu-id="8b972-269">Convertir à partir de la source native types too.NET type</span><span class="sxs-lookup"><span data-stu-id="8b972-269">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="8b972-270">Conversion de type de récepteur de toonative de type .NET</span><span class="sxs-lookup"><span data-stu-id="8b972-270">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="8b972-271">Lorsque vous déplacez des données trop & à partir de la Table Azure, hello suivant [des mappages définis par le service de Table Azure](https://msdn.microsoft.com/library/azure/dd179338.aspx) servent de type de too.NET types OData de Table Azure et vice versa.</span><span class="sxs-lookup"><span data-stu-id="8b972-271">When moving data too& from Azure Table, hello following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types too.NET type and vice versa.</span></span>

| <span data-ttu-id="8b972-272">Type de données OData</span><span class="sxs-lookup"><span data-stu-id="8b972-272">OData Data Type</span></span> | <span data-ttu-id="8b972-273">Type .NET</span><span class="sxs-lookup"><span data-stu-id="8b972-273">.NET Type</span></span> | <span data-ttu-id="8b972-274">Détails</span><span class="sxs-lookup"><span data-stu-id="8b972-274">Details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b972-275">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="8b972-275">Edm.Binary</span></span> |<span data-ttu-id="8b972-276">byte[]</span><span class="sxs-lookup"><span data-stu-id="8b972-276">byte[]</span></span> |<span data-ttu-id="8b972-277">Un tableau d’octets des too64 Ko.</span><span class="sxs-lookup"><span data-stu-id="8b972-277">An array of bytes up too64 KB.</span></span> |
| <span data-ttu-id="8b972-278">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="8b972-278">Edm.Boolean</span></span> |<span data-ttu-id="8b972-279">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="8b972-279">bool</span></span> |<span data-ttu-id="8b972-280">Valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="8b972-280">A Boolean value.</span></span> |
| <span data-ttu-id="8b972-281">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="8b972-281">Edm.DateTime</span></span> |<span data-ttu-id="8b972-282">DateTime</span><span class="sxs-lookup"><span data-stu-id="8b972-282">DateTime</span></span> |<span data-ttu-id="8b972-283">Valeur de 64 bits exprimée en temps universel coordonné (UTC).</span><span class="sxs-lookup"><span data-stu-id="8b972-283">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="8b972-284">prise en charge de Hello DateTime commence à partir de 12:00 minuit, le 1er janvier 1601.</span><span class="sxs-lookup"><span data-stu-id="8b972-284">hello supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="8b972-285">(NOTRE ÈRE), UTC.</span><span class="sxs-lookup"><span data-stu-id="8b972-285">(C.E.), UTC.</span></span> <span data-ttu-id="8b972-286">Hello se termine le 31 décembre 9999.</span><span class="sxs-lookup"><span data-stu-id="8b972-286">hello range ends at December 31, 9999.</span></span> |
| <span data-ttu-id="8b972-287">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="8b972-287">Edm.Double</span></span> |<span data-ttu-id="8b972-288">double</span><span class="sxs-lookup"><span data-stu-id="8b972-288">double</span></span> |<span data-ttu-id="8b972-289">Valeur à virgule flottante de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="8b972-289">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="8b972-290">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="8b972-290">Edm.Guid</span></span> |<span data-ttu-id="8b972-291">Guid</span><span class="sxs-lookup"><span data-stu-id="8b972-291">Guid</span></span> |<span data-ttu-id="8b972-292">Identificateur global unique de 128 bits.</span><span class="sxs-lookup"><span data-stu-id="8b972-292">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="8b972-293">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="8b972-293">Edm.Int32</span></span> |<span data-ttu-id="8b972-294">Int32</span><span class="sxs-lookup"><span data-stu-id="8b972-294">Int32</span></span> |<span data-ttu-id="8b972-295">Nombre entier 32 bits.</span><span class="sxs-lookup"><span data-stu-id="8b972-295">A 32-bit integer.</span></span> |
| <span data-ttu-id="8b972-296">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="8b972-296">Edm.Int64</span></span> |<span data-ttu-id="8b972-297">Int64</span><span class="sxs-lookup"><span data-stu-id="8b972-297">Int64</span></span> |<span data-ttu-id="8b972-298">Nombre entier 64 bits.</span><span class="sxs-lookup"><span data-stu-id="8b972-298">A 64-bit integer.</span></span> |
| <span data-ttu-id="8b972-299">Edm.String</span><span class="sxs-lookup"><span data-stu-id="8b972-299">Edm.String</span></span> |<span data-ttu-id="8b972-300">String</span><span class="sxs-lookup"><span data-stu-id="8b972-300">String</span></span> |<span data-ttu-id="8b972-301">Valeur encodée en UTF-16.</span><span class="sxs-lookup"><span data-stu-id="8b972-301">A UTF-16-encoded value.</span></span> <span data-ttu-id="8b972-302">Les valeurs de chaîne peuvent être des too64 Ko.</span><span class="sxs-lookup"><span data-stu-id="8b972-302">String values may be up too64 KB.</span></span> |

### <a name="type-conversion-sample"></a><span data-ttu-id="8b972-303">Exemple de conversion de type</span><span class="sxs-lookup"><span data-stu-id="8b972-303">Type Conversion Sample</span></span>
<span data-ttu-id="8b972-304">Hello suivant l’exemple est pour copier des données à partir d’une Table de tooAzure objets Blob Azure avec des conversions de type.</span><span class="sxs-lookup"><span data-stu-id="8b972-304">hello following sample is for copying data from an Azure Blob tooAzure Table with type conversions.</span></span>

<span data-ttu-id="8b972-305">Supposons que jeu de données Blob hello est au format CSV et comporte trois colonnes.</span><span class="sxs-lookup"><span data-stu-id="8b972-305">Suppose hello Blob dataset is in CSV format and contains three columns.</span></span> <span data-ttu-id="8b972-306">Un d’eux est une colonne datetime avec un format datetime personnalisées à l’aide d’un nom abrégé Français pour le jour de la semaine de hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-306">One of them is a datetime column with a custom datetime format using abbreviated French names for day of hello week.</span></span>

<span data-ttu-id="8b972-307">Définir le dataset de Source de l’objet Blob de hello comme suit, ainsi que des définitions de type pour les colonnes hello.</span><span class="sxs-lookup"><span data-stu-id="8b972-307">Define hello Blob Source dataset as follows along with type definitions for hello columns.</span></span>

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
<span data-ttu-id="8b972-308">Compte tenu de mappage de type hello du type de too.NET type OData de Table Azure, vous devrez définir table de hello dans la Table Azure avec hello suivant le schéma.</span><span class="sxs-lookup"><span data-stu-id="8b972-308">Given hello type mapping from Azure Table OData type too.NET type, you would define hello table in Azure Table with hello following schema.</span></span>

<span data-ttu-id="8b972-309">**Schéma de Table Azure :**</span><span class="sxs-lookup"><span data-stu-id="8b972-309">**Azure Table schema:**</span></span>

| <span data-ttu-id="8b972-310">Nom de la colonne</span><span class="sxs-lookup"><span data-stu-id="8b972-310">Column name</span></span> | <span data-ttu-id="8b972-311">Type</span><span class="sxs-lookup"><span data-stu-id="8b972-311">Type</span></span> |
| --- | --- |
| <span data-ttu-id="8b972-312">userid</span><span class="sxs-lookup"><span data-stu-id="8b972-312">userid</span></span> |<span data-ttu-id="8b972-313">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="8b972-313">Edm.Int64</span></span> |
| <span data-ttu-id="8b972-314">name</span><span class="sxs-lookup"><span data-stu-id="8b972-314">name</span></span> |<span data-ttu-id="8b972-315">Edm.String</span><span class="sxs-lookup"><span data-stu-id="8b972-315">Edm.String</span></span> |
| <span data-ttu-id="8b972-316">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="8b972-316">lastlogindate</span></span> |<span data-ttu-id="8b972-317">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="8b972-317">Edm.DateTime</span></span> |

<span data-ttu-id="8b972-318">Ensuite, définissez le jeu de données de Table Azure hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="8b972-318">Next, define hello Azure Table dataset as follows.</span></span> <span data-ttu-id="8b972-319">Vous n’avez pas besoin de section « structure » de toospecify avec les informations de type hello, car les informations de type hello sont déjà spécifiées dans hello sous-jacent du magasin de données.</span><span class="sxs-lookup"><span data-stu-id="8b972-319">You do not need toospecify “structure” section with hello type information since hello type information is already specified in hello underlying data store.</span></span>

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

<span data-ttu-id="8b972-320">Dans ce cas, la fabrique de données automatiquement conversions de type, y compris le champ de date/heure hello avec le format de date/heure personnalisé hello à l’aide de la culture de hello « fr-fr » lors du déplacement des données à partir de l’objet Blob tooAzure Table.</span><span class="sxs-lookup"><span data-stu-id="8b972-320">In this case, Data Factory automatically does type conversions including hello Datetime field with hello custom datetime format using hello "fr-fr" culture when moving data from Blob tooAzure Table.</span></span>

> [!NOTE]
> <span data-ttu-id="8b972-321">colonnes de toomap de toocolumns du jeu de données source à partir du jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="8b972-321">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="8b972-322">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="8b972-322">Performance and Tuning</span></span>
<span data-ttu-id="8b972-323">impact sur les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize des facteurs toolearn sur la clé, consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="8b972-323">toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
