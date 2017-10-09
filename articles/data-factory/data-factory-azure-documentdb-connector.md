---
title: "les données d’aaaMove vers/à partir de la base de données Azure Cosmos | Documents Microsoft"
description: "Découvrez comment déplacer des données vers et à partir de la collection Azure Cosmos DB à l’aide d’Azure Data Factory."
services: data-factory, cosmosdb
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: bd23ce4e004a972ce6f3e4165cfdea4f0c18fecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-cosmos-db-using-azure-data-factory"></a><span data-ttu-id="9df98-103">Déplacer les données tooand à partir de la base de données Azure Cosmos à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9df98-103">Move data tooand from Azure Cosmos DB using Azure Data Factory</span></span>
<span data-ttu-id="9df98-104">Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory à partir de base de données Azure Cosmos (API DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="9df98-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure Cosmos DB (DocumentDB API).</span></span> <span data-ttu-id="9df98-105">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="9df98-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="9df98-106">Vous pouvez copier les données de toute source pris en charge de données tooAzure Cosmos de base de données de stockage ou à partir des données de base de données Azure Cosmos tooany pris en charge récepteur stockage.</span><span class="sxs-lookup"><span data-stu-id="9df98-106">You can copy data from any supported source data store tooAzure Cosmos DB or from Azure Cosmos DB tooany supported sink data store.</span></span> <span data-ttu-id="9df98-107">Pour obtenir la liste des magasins de données pris en charge en tant que sources ou récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="9df98-107">For a list of data stores supported as sources or sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9df98-108">Le connecteur Azure Cosmos DB ne prend en charge que l’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="9df98-108">Azure Cosmos DB connector only support DocumentDB API.</span></span>

<span data-ttu-id="9df98-109">données toocopy sous la forme-est vers/à partir de fichiers JSON ou une autre collection Cosmos DB, consultez [documents JSON d’importation/exportation](#importexport-json-documents).</span><span class="sxs-lookup"><span data-stu-id="9df98-109">toocopy data as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span></span>

## <a name="getting-started"></a><span data-ttu-id="9df98-110">Prise en main</span><span class="sxs-lookup"><span data-stu-id="9df98-110">Getting started</span></span>
<span data-ttu-id="9df98-111">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers ou à partir d’Azure Cosmos DB à l’aide de différents outils et API.</span><span class="sxs-lookup"><span data-stu-id="9df98-111">You can create a pipeline with a copy activity that moves data to/from Azure Cosmos DB by using different tools/APIs.</span></span>

<span data-ttu-id="9df98-112">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="9df98-112">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="9df98-113">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="9df98-113">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="9df98-114">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="9df98-114">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="9df98-115">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="9df98-115">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="9df98-116">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="9df98-116">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="9df98-117">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="9df98-117">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="9df98-118">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="9df98-118">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="9df98-119">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="9df98-119">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="9df98-120">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="9df98-120">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="9df98-121">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="9df98-121">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="9df98-122">Pour obtenir des exemples avec des définitions pour les entités de fabrique de données qui sont utilisées toocopy des données vers/à partir de la base de données Cosmos JSON, consultez [exemples JSON](#json-examples) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="9df98-122">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from Cosmos DB, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="9df98-123">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifiques tooCosmos DB :</span><span class="sxs-lookup"><span data-stu-id="9df98-123">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooCosmos DB:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="9df98-124">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="9df98-124">Linked service properties</span></span>
<span data-ttu-id="9df98-125">Hello tableau suivant fournit la description pour JSON éléments tooAzure spécifique service DB Cosmos lié.</span><span class="sxs-lookup"><span data-stu-id="9df98-125">hello following table provides description for JSON elements specific tooAzure Cosmos DB linked service.</span></span>

| <span data-ttu-id="9df98-126">**Propriété**</span><span class="sxs-lookup"><span data-stu-id="9df98-126">**Property**</span></span> | <span data-ttu-id="9df98-127">**Description**</span><span class="sxs-lookup"><span data-stu-id="9df98-127">**Description**</span></span> | <span data-ttu-id="9df98-128">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="9df98-128">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9df98-129">type</span><span class="sxs-lookup"><span data-stu-id="9df98-129">type</span></span> |<span data-ttu-id="9df98-130">propriété de type Hello doit indiquer : **DocumentDb**</span><span class="sxs-lookup"><span data-stu-id="9df98-130">hello type property must be set to: **DocumentDb**</span></span> |<span data-ttu-id="9df98-131">Oui</span><span class="sxs-lookup"><span data-stu-id="9df98-131">Yes</span></span> |
| <span data-ttu-id="9df98-132">connectionString</span><span class="sxs-lookup"><span data-stu-id="9df98-132">connectionString</span></span> |<span data-ttu-id="9df98-133">Spécifiez les informations nécessaires de base de données de base de données Cosmos tooconnect tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9df98-133">Specify information needed tooconnect tooAzure Cosmos DB database.</span></span> |<span data-ttu-id="9df98-134">Oui</span><span class="sxs-lookup"><span data-stu-id="9df98-134">Yes</span></span> |

<span data-ttu-id="9df98-135">Exemple :</span><span class="sxs-lookup"><span data-stu-id="9df98-135">Example:</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="9df98-136">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="9df98-136">Dataset properties</span></span>
<span data-ttu-id="9df98-137">Pour une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez toohello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="9df98-137">For a full list of sections & properties available for defining datasets please refer toohello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="9df98-138">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="9df98-138">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="9df98-139">section de typeProperties Hello est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="9df98-139">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="9df98-140">section hello le jeu de données de type Hello typeProperties **DocumentDbCollection** a les propriétés suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="9df98-140">hello typeProperties section for hello dataset of type **DocumentDbCollection** has hello following properties.</span></span>

| <span data-ttu-id="9df98-141">**Propriété**</span><span class="sxs-lookup"><span data-stu-id="9df98-141">**Property**</span></span> | <span data-ttu-id="9df98-142">**Description**</span><span class="sxs-lookup"><span data-stu-id="9df98-142">**Description**</span></span> | <span data-ttu-id="9df98-143">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="9df98-143">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9df98-144">collectionName</span><span class="sxs-lookup"><span data-stu-id="9df98-144">collectionName</span></span> |<span data-ttu-id="9df98-145">Nom de collection de documents de base de données Cosmos de hello.</span><span class="sxs-lookup"><span data-stu-id="9df98-145">Name of hello Cosmos DB document collection.</span></span> |<span data-ttu-id="9df98-146">Oui</span><span class="sxs-lookup"><span data-stu-id="9df98-146">Yes</span></span> |

<span data-ttu-id="9df98-147">Exemple :</span><span class="sxs-lookup"><span data-stu-id="9df98-147">Example:</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
### <a name="schema-by-data-factory"></a><span data-ttu-id="9df98-148">Schéma par Data Factory</span><span class="sxs-lookup"><span data-stu-id="9df98-148">Schema by Data Factory</span></span>
<span data-ttu-id="9df98-149">Pour les magasins de données sans schéma comme base de données Azure Cosmos, hello service Data Factory déduit le schéma de hello dans un des hello suivant façons :</span><span class="sxs-lookup"><span data-stu-id="9df98-149">For schema-free data stores such as Azure Cosmos DB, hello Data Factory service infers hello schema in one of hello following ways:</span></span>  

1. <span data-ttu-id="9df98-150">Si vous spécifiez la structure hello des données à l’aide de hello **structure** propriété dans la définition de dataset hello, hello service Data Factory respecte cette structure en tant que schéma de hello.</span><span class="sxs-lookup"><span data-stu-id="9df98-150">If you specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service honors this structure as hello schema.</span></span> <span data-ttu-id="9df98-151">Dans ce cas, si une ligne ne contient pas de valeur pour une colonne, une valeur null est fournie pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="9df98-151">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span></span>
2. <span data-ttu-id="9df98-152">Si vous ne spécifiez pas de structure hello des données à l’aide de hello **structure** propriété dans la définition de dataset hello, hello service Data Factory déduit le schéma de hello à l’aide de la première ligne de hello dans les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="9df98-152">If you do not specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service infers hello schema by using hello first row in hello data.</span></span> <span data-ttu-id="9df98-153">Dans ce cas, si la première ligne de hello ne contient pas de schéma complet de hello, certaines colonnes sera manquants dans le résultat de hello d’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="9df98-153">In this case, if hello first row does not contain hello full schema, some columns will be missing in hello result of copy operation.</span></span>

<span data-ttu-id="9df98-154">Par conséquent, pour les sources de données de schéma, il est recommandé de hello est toospecify hello structure de données à l’aide de hello **structure** propriété.</span><span class="sxs-lookup"><span data-stu-id="9df98-154">Therefore, for schema-free data sources, hello best practice is toospecify hello structure of data using hello **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="9df98-155">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="9df98-155">Copy activity properties</span></span>
<span data-ttu-id="9df98-156">Pour une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez toohello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="9df98-156">For a full list of sections & properties available for defining activities please refer toohello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="9df98-157">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="9df98-157">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="9df98-158">Hello activité de copie accepte uniquement une entrée et produit qu’une seule sortie.</span><span class="sxs-lookup"><span data-stu-id="9df98-158">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="9df98-159">Propriétés disponibles dans la section de typeProperties hello d’activité hello sur hello autre part varie avec chaque type d’activité et en cas d’activité de copie ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="9df98-159">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type and in case of Copy activity they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="9df98-160">En cas d’activité de copie lors de la source est de type **DocumentDbCollectionSource** hello propriétés suivantes est disponible dans **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="9df98-160">In case of Copy activity when source is of type **DocumentDbCollectionSource** hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="9df98-161">**Propriété**</span><span class="sxs-lookup"><span data-stu-id="9df98-161">**Property**</span></span> | <span data-ttu-id="9df98-162">**Description**</span><span class="sxs-lookup"><span data-stu-id="9df98-162">**Description**</span></span> | <span data-ttu-id="9df98-163">**Valeurs autorisées**</span><span class="sxs-lookup"><span data-stu-id="9df98-163">**Allowed values**</span></span> | <span data-ttu-id="9df98-164">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="9df98-164">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9df98-165">query</span><span class="sxs-lookup"><span data-stu-id="9df98-165">query</span></span> |<span data-ttu-id="9df98-166">Spécifier les données de tooread requête hello.</span><span class="sxs-lookup"><span data-stu-id="9df98-166">Specify hello query tooread data.</span></span> |<span data-ttu-id="9df98-167">Chaîne de requête prise en charge par Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9df98-167">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="9df98-168">Exemple : `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="9df98-168">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="9df98-169">Non</span><span class="sxs-lookup"><span data-stu-id="9df98-169">No</span></span> <br/><br/><span data-ttu-id="9df98-170">Si ce n’est pas spécifié, hello instruction SQL exécutée :`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="9df98-170">If not specified, hello SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="9df98-171">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="9df98-171">nestingSeparator</span></span> |<span data-ttu-id="9df98-172">Tooindicate caractère spécial qui hello document est imbriquée.</span><span class="sxs-lookup"><span data-stu-id="9df98-172">Special character tooindicate that hello document is nested</span></span> |<span data-ttu-id="9df98-173">Tout caractère.</span><span class="sxs-lookup"><span data-stu-id="9df98-173">Any character.</span></span> <br/><br/><span data-ttu-id="9df98-174">Azure Cosmos DB est une banque NoSQL de documents JSON, où les structures imbriquées sont autorisées.</span><span class="sxs-lookup"><span data-stu-id="9df98-174">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="9df98-175">Azure Data Factory permet de hiérarchie de toodenote utilisateur via nestingSeparator, qui est «. »</span><span class="sxs-lookup"><span data-stu-id="9df98-175">Azure Data Factory enables user toodenote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="9df98-176">Bonjour exemples ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="9df98-176">in hello above examples.</span></span> <span data-ttu-id="9df98-177">Avec séparateur de hello, activité de copie hello génère un objet de « Name » hello avec des éléments de trois enfants too"Name.First première, intermédiaire et dernière, en fonction », « Name.Middle » et « Name.Last « Bonjour de définition de table.</span><span class="sxs-lookup"><span data-stu-id="9df98-177">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span> |<span data-ttu-id="9df98-178">Non</span><span class="sxs-lookup"><span data-stu-id="9df98-178">No</span></span> |

<span data-ttu-id="9df98-179">**DocumentDbCollectionSink** prend en charge hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="9df98-179">**DocumentDbCollectionSink** supports hello following properties:</span></span>

| <span data-ttu-id="9df98-180">**Propriété**</span><span class="sxs-lookup"><span data-stu-id="9df98-180">**Property**</span></span> | <span data-ttu-id="9df98-181">**Description**</span><span class="sxs-lookup"><span data-stu-id="9df98-181">**Description**</span></span> | <span data-ttu-id="9df98-182">**Valeurs autorisées**</span><span class="sxs-lookup"><span data-stu-id="9df98-182">**Allowed values**</span></span> | <span data-ttu-id="9df98-183">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="9df98-183">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9df98-184">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="9df98-184">nestingSeparator</span></span> |<span data-ttu-id="9df98-185">Un caractère spécial dans tooindicate de nom hello source colonne imbriquées de document est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9df98-185">A special character in hello source column name tooindicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="9df98-186">Par exemple ci-dessus : `Name.First` dans la sortie de hello table génère hello suivant structure JSON dans le document de base de données Cosmos hello :</span><span class="sxs-lookup"><span data-stu-id="9df98-186">For example above: `Name.First` in hello output table produces hello following JSON structure in hello Cosmos DB document:</span></span><br/><br/><span data-ttu-id="9df98-187">"Name": {</span><span class="sxs-lookup"><span data-stu-id="9df98-187">"Name": {</span></span><br/>    <span data-ttu-id="9df98-188">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="9df98-188">"First": "John"</span></span><br/><span data-ttu-id="9df98-189">},</span><span class="sxs-lookup"><span data-stu-id="9df98-189">},</span></span> |<span data-ttu-id="9df98-190">Caractère utilisé tooseparate des niveaux d’imbrication.</span><span class="sxs-lookup"><span data-stu-id="9df98-190">Character that is used tooseparate nesting levels.</span></span><br/><br/><span data-ttu-id="9df98-191">La valeur par défaut est `.` (point).</span><span class="sxs-lookup"><span data-stu-id="9df98-191">Default value is `.` (dot).</span></span> |<span data-ttu-id="9df98-192">Caractère utilisé tooseparate des niveaux d’imbrication.</span><span class="sxs-lookup"><span data-stu-id="9df98-192">Character that is used tooseparate nesting levels.</span></span> <br/><br/><span data-ttu-id="9df98-193">La valeur par défaut est `.` (point).</span><span class="sxs-lookup"><span data-stu-id="9df98-193">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="9df98-194">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="9df98-194">writeBatchSize</span></span> |<span data-ttu-id="9df98-195">Nombre de parallèle demandes documents toocreate de service de base de données Cosmos tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9df98-195">Number of parallel requests tooAzure Cosmos DB service toocreate documents.</span></span><br/><br/><span data-ttu-id="9df98-196">Vous pouvez affiner les performances des hello lors de la copie des données à partir de Cosmos DB à l’aide de cette propriété.</span><span class="sxs-lookup"><span data-stu-id="9df98-196">You can fine-tune hello performance when copying data to/from Cosmos DB by using this property.</span></span> <span data-ttu-id="9df98-197">Vous pouvez vous attendre de meilleures performances lorsque vous augmentez la valeur writeBatchSize, car plusieurs demandes parallèles tooCosmos base de données sont envoyés.</span><span class="sxs-lookup"><span data-stu-id="9df98-197">You can expect a better performance when you increase writeBatchSize because more parallel requests tooCosmos DB are sent.</span></span> <span data-ttu-id="9df98-198">Toutefois, vous devez tooavoid la limitation peut lever de message d’erreur hello : « Requête taux est grand ».</span><span class="sxs-lookup"><span data-stu-id="9df98-198">However you’ll need tooavoid throttling that can throw hello error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="9df98-199">Une limitation dépend de divers facteurs, dont la taille des documents, le nombre de termes qu’ils contiennent, la stratégie d’indexation de la collection cible, etc. Pour les opérations de copie, vous pouvez utiliser la plupart des débit disponible à une meilleure hello de toohave de collection (par exemple, S3) (2 500 demande unités par seconde).</span><span class="sxs-lookup"><span data-stu-id="9df98-199">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) toohave hello most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="9df98-200">Entier </span><span class="sxs-lookup"><span data-stu-id="9df98-200">Integer</span></span> |<span data-ttu-id="9df98-201">Non (valeur par défaut : 5)</span><span class="sxs-lookup"><span data-stu-id="9df98-201">No (default: 5)</span></span> |
| <span data-ttu-id="9df98-202">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="9df98-202">writeBatchTimeout</span></span> |<span data-ttu-id="9df98-203">Temps d’attente pour hello opération toocomplete avant d’expirer.</span><span class="sxs-lookup"><span data-stu-id="9df98-203">Wait time for hello operation toocomplete before it times out.</span></span> |<span data-ttu-id="9df98-204">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="9df98-204">timespan</span></span><br/><br/> <span data-ttu-id="9df98-205">Exemple : « 00:30:00 » (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="9df98-205">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="9df98-206">Non</span><span class="sxs-lookup"><span data-stu-id="9df98-206">No</span></span> |

## <a name="importexport-json-documents"></a><span data-ttu-id="9df98-207">Importation/exportation de documents JSON</span><span class="sxs-lookup"><span data-stu-id="9df98-207">Import/Export JSON documents</span></span>
<span data-ttu-id="9df98-208">À l’aide de ce connecteur Cosmos DB, vous pouvez facilement :</span><span class="sxs-lookup"><span data-stu-id="9df98-208">Using this Cosmos DB connector, you can easily</span></span>

* <span data-ttu-id="9df98-209">Importer des documents JSON de différentes sources dans Cosmos DB, notamment le Stockage Blob Azure, Azure Data Lake, un système de fichiers local ou d’autres banques basées sur des fichiers prises en charge par Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9df98-209">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span></span>
* <span data-ttu-id="9df98-210">Exporter des documents JSON d’une collection Cosmos DB vers différentes banques basées sur des fichiers.</span><span class="sxs-lookup"><span data-stu-id="9df98-210">Export JSON documents from Cosmos DB collecton into various file-based stores.</span></span>
* <span data-ttu-id="9df98-211">Migrer des données entre deux collections Cosmos DB en l’état.</span><span class="sxs-lookup"><span data-stu-id="9df98-211">Migrate data between two Cosmos DB collections as-is.</span></span>

<span data-ttu-id="9df98-212">tooachieve ce schéma indépendant de la copier,</span><span class="sxs-lookup"><span data-stu-id="9df98-212">tooachieve such schema-agnostic copy,</span></span> 
* <span data-ttu-id="9df98-213">Lorsque vous utilisez l’Assistant copie de, vérifiez hello **« exporter en tant que-est tooJSON fichiers ou une collection de Cosmos DB »** option.</span><span class="sxs-lookup"><span data-stu-id="9df98-213">When using copy wizard, check hello **"Export as-is tooJSON files or Cosmos DB collection"** option.</span></span>
* <span data-ttu-id="9df98-214">Lorsque, à l’aide de la modification de JSON, ne spécifiez pas de section « structure » de hello dans les jeux de données de base de données Cosmos ni propriété « nestingSeparator » sur la base de données Cosmos source/récepteur dans l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="9df98-214">When using JSON editing, do not specify hello "structure" section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span></span> <span data-ttu-id="9df98-215">tooimport à partir de / tooJSON fichiers d’exportation, hello fichier magasin DataSet spécifier le type de format comme « JsonFormat », « filePattern » de configuration et ignorer les paramètres de format hello rest, consultez [format JSON](data-factory-supported-file-and-compression-formats.md#json-format) section de détails.</span><span class="sxs-lookup"><span data-stu-id="9df98-215">tooimport from/export tooJSON files, in hello file store dataset specify format type as "JsonFormat", config "filePattern" and skip hello rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="9df98-216">Exemples JSON</span><span class="sxs-lookup"><span data-stu-id="9df98-216">JSON examples</span></span>
<span data-ttu-id="9df98-217">Hello exemples suivants proposent des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9df98-217">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="9df98-218">Elles montrent comment tooand de données toocopy à partir de la base de données Azure Cosmos et de stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="9df98-218">They show how toocopy data tooand from Azure Cosmos DB and Azure Blob Storage.</span></span> <span data-ttu-id="9df98-219">Toutefois, les données peuvent être copiées **directement** de n’importe quelle tooany de sources hello de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9df98-219">However, data can be copied **directly** from any of hello sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-azure-cosmos-db-tooazure-blob"></a><span data-ttu-id="9df98-220">Exemple : Copier des données à partir de la base de données Azure Cosmos tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="9df98-220">Example: Copy data from Azure Cosmos DB tooAzure Blob</span></span>
<span data-ttu-id="9df98-221">exemple Hello ci-dessous montre :</span><span class="sxs-lookup"><span data-stu-id="9df98-221">hello sample below shows:</span></span>

1. <span data-ttu-id="9df98-222">Un service lié de type [DocumentDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9df98-222">A linked service of type [DocumentDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="9df98-223">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9df98-223">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="9df98-224">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [DocumentDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9df98-224">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="9df98-225">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9df98-225">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="9df98-226">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [DocumentDbCollectionSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="9df98-226">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="9df98-227">exemple Hello copie des données dans la base de données Azure Cosmos tooAzure Blob.</span><span class="sxs-lookup"><span data-stu-id="9df98-227">hello sample copies data in Azure Cosmos DB tooAzure Blob.</span></span> <span data-ttu-id="9df98-228">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="9df98-228">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="9df98-229">**Service lié Azure Cosmos DB :**</span><span class="sxs-lookup"><span data-stu-id="9df98-229">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="9df98-230">**Service lié Azure Blob Storage :**</span><span class="sxs-lookup"><span data-stu-id="9df98-230">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="9df98-231">**Jeu de données d'entrée Document DB Azure :**</span><span class="sxs-lookup"><span data-stu-id="9df98-231">**Azure Document DB input dataset:**</span></span>

<span data-ttu-id="9df98-232">exemple Hello suppose que vous avez une collection nommée **personne** dans une base de données de la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="9df98-232">hello sample assumes you have a collection named **Person** in an Azure Cosmos DB database.</span></span>

<span data-ttu-id="9df98-233">Paramètre « external » : « true » et spécifiant externalData les informations de stratégie hello Azure Data Factory du service table hello est fabrique de données externe toohello pas produit par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="9df98-233">Setting “external”: ”true” and specifying externalData policy information hello Azure Data Factory service that hello table is external toohello data factory and not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="9df98-234">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="9df98-234">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="9df98-235">Les données sont copiées tooa nouvel objet blob toutes les heures avec un chemin d’accès hello blob hello reflétant hello la date/heure spécifique avec une granularité de l’heure.</span><span class="sxs-lookup"><span data-stu-id="9df98-235">Data is copied tooa new blob every hour with hello path for hello blob reflecting hello specific datetime with hour granularity.</span></span>

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="9df98-236">Exemple de document JSON Bonjour collection personne dans une base de données de la base de données Cosmos :</span><span class="sxs-lookup"><span data-stu-id="9df98-236">Sample JSON document in hello Person collection in a Cosmos DB database:</span></span>

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
<span data-ttu-id="9df98-237">Cosmos DB prend en charge l'interrogation de documents à l'aide d'une syntaxe de type SQL sur des documents JSON hiérarchiques.</span><span class="sxs-lookup"><span data-stu-id="9df98-237">Cosmos DB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span></span>

<span data-ttu-id="9df98-238">Exemple :</span><span class="sxs-lookup"><span data-stu-id="9df98-238">Example:</span></span> 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

<span data-ttu-id="9df98-239">copie des données à partir de hello collection personne Bonjour tooan de base de données de base de données Azure Cosmos blob Azure de pipeline suivants de Hello.</span><span class="sxs-lookup"><span data-stu-id="9df98-239">hello following pipeline copies data from hello Person collection in hello Azure Cosmos DB database tooan Azure blob.</span></span> <span data-ttu-id="9df98-240">Dans le cadre de hello d’activité hello copie les jeux de données d’entrée et de sortie ont été spécifiés.</span><span class="sxs-lookup"><span data-stu-id="9df98-240">As part of hello copy activity hello input and output datasets have been specified.</span></span>  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "DocumentDbCollectionSource",
            "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
            "nestingSeparator": "."
          },
          "sink": {
            "type": "BlobSink",
            "blobWriterAddHeader": true,
            "writeBatchSize": 1000,
            "writeBatchTimeout": "00:00:59"
          }
        },
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-tooazure-cosmos-db"></a><span data-ttu-id="9df98-241">Exemple : Copier des données d’objets Blob Azure tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9df98-241">Example: Copy data from Azure Blob tooAzure Cosmos DB</span></span> 
<span data-ttu-id="9df98-242">exemple Hello ci-dessous montre :</span><span class="sxs-lookup"><span data-stu-id="9df98-242">hello sample below shows:</span></span>

1. <span data-ttu-id="9df98-243">Un service lié de type [DocumentDb](#azure-documentdb-linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9df98-243">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span></span>
2. <span data-ttu-id="9df98-244">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9df98-244">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="9df98-245">un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9df98-245">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="9df98-246">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span><span class="sxs-lookup"><span data-stu-id="9df98-246">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span></span>
5. <span data-ttu-id="9df98-247">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) et [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="9df98-247">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span></span>

<span data-ttu-id="9df98-248">exemple Hello copie les données d’objets blob Azure tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9df98-248">hello sample copies data from Azure blob tooAzure Cosmos DB.</span></span> <span data-ttu-id="9df98-249">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="9df98-249">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="9df98-250">**Service lié Azure Blob Storage :**</span><span class="sxs-lookup"><span data-stu-id="9df98-250">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="9df98-251">**Service lié Azure Cosmos DB :**</span><span class="sxs-lookup"><span data-stu-id="9df98-251">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="9df98-252">**Jeu de données d'entrée d'objet Blob Azure :**</span><span class="sxs-lookup"><span data-stu-id="9df98-252">**Azure Blob input dataset:**</span></span>

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="9df98-253">**Jeu de données de sortie Azure Cosmos DB :**</span><span class="sxs-lookup"><span data-stu-id="9df98-253">**Azure Cosmos DB output dataset:**</span></span>

<span data-ttu-id="9df98-254">exemple Hello copie la collection de tooa de données nommée « Person ».</span><span class="sxs-lookup"><span data-stu-id="9df98-254">hello sample copies data tooa collection named “Person”.</span></span>

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="9df98-255">copie des données d’objets Blob Azure toohello collection personne Bonjour Cosmos DB de pipeline suivants de Hello.</span><span class="sxs-lookup"><span data-stu-id="9df98-255">hello following pipeline copies data from Azure Blob toohello Person collection in hello Cosmos DB.</span></span> <span data-ttu-id="9df98-256">Dans le cadre de hello d’activité hello copie les jeux de données d’entrée et de sortie ont été spécifiés.</span><span class="sxs-lookup"><span data-stu-id="9df98-256">As part of hello copy activity hello input and output datasets have been specified.</span></span>

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "DocumentDbCollectionSink",
            "nestingSeparator": ".",
            "writeBatchSize": 2,
            "writeBatchTimeout": "00:00:00"
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
<span data-ttu-id="9df98-257">Si l’exemple hello d’objets blob entrée est comme</span><span class="sxs-lookup"><span data-stu-id="9df98-257">If hello sample blob input is as</span></span>

```
1,John,,Doe
```
<span data-ttu-id="9df98-258">Puis hello sortie JSON dans la base de données Cosmos sera en tant que :</span><span class="sxs-lookup"><span data-stu-id="9df98-258">Then hello output JSON in Cosmos DB will be as:</span></span>

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
<span data-ttu-id="9df98-259">Azure Cosmos DB est une banque NoSQL de documents JSON, où les structures imbriquées sont autorisées.</span><span class="sxs-lookup"><span data-stu-id="9df98-259">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="9df98-260">Azure Data Factory permet de hiérarchie de toodenote utilisateur via **nestingSeparator**, qui est «. »</span><span class="sxs-lookup"><span data-stu-id="9df98-260">Azure Data Factory enables user toodenote hierarchy via **nestingSeparator**, which is “.”</span></span> <span data-ttu-id="9df98-261">» dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="9df98-261">in this example.</span></span> <span data-ttu-id="9df98-262">Avec séparateur de hello, activité de copie hello génère un objet de « Name » hello avec des éléments de trois enfants too"Name.First première, intermédiaire et dernière, en fonction », « Name.Middle » et « Name.Last « Bonjour de définition de table.</span><span class="sxs-lookup"><span data-stu-id="9df98-262">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span>

## <a name="appendix"></a><span data-ttu-id="9df98-263">Annexe</span><span class="sxs-lookup"><span data-stu-id="9df98-263">Appendix</span></span>
1. <span data-ttu-id="9df98-264">**Question :** hello mise à jour de la prise en charge de l’activité de copie des enregistrements existants ?</span><span class="sxs-lookup"><span data-stu-id="9df98-264">**Question:** Does hello Copy Activity support update of existing records?</span></span>

    <span data-ttu-id="9df98-265">**Réponse :** non.</span><span class="sxs-lookup"><span data-stu-id="9df98-265">**Answer:** No.</span></span>
2. <span data-ttu-id="9df98-266">**Question :** comment fait une nouvelle tentative d’un contrat de base de données Cosmos copie tooAzure avec déjà copié les enregistrements ?</span><span class="sxs-lookup"><span data-stu-id="9df98-266">**Question:** How does a retry of a copy tooAzure Cosmos DB deal with already copied records?</span></span>

    <span data-ttu-id="9df98-267">**Réponse :** si les enregistrements ont un champ « ID » et l’opération de copie hello tente tooinsert un enregistrement avec hello même ID, l’opération de copie hello génère une erreur.</span><span class="sxs-lookup"><span data-stu-id="9df98-267">**Answer:** If records have an "ID" field and hello copy operation tries tooinsert a record with hello same ID, hello copy operation throws an error.</span></span>  
3. <span data-ttu-id="9df98-268">**Question :** Data Factory prend-il en charge le [partitionnement de données basé sur un intervalle ou sur le hachage](../documentdb/documentdb-partition-data.md) ?</span><span class="sxs-lookup"><span data-stu-id="9df98-268">**Question:** Does Data Factory support [range or hash-based data partitioning](../documentdb/documentdb-partition-data.md)?</span></span>

    <span data-ttu-id="9df98-269">**Réponse :** non.</span><span class="sxs-lookup"><span data-stu-id="9df98-269">**Answer:** No.</span></span>
4. <span data-ttu-id="9df98-270">**Question :** puis-je indiquer plusieurs collections Azure Cosmos DB pour une table ?</span><span class="sxs-lookup"><span data-stu-id="9df98-270">**Question:** Can I specify more than one Azure Cosmos DB collection for a table?</span></span>

    <span data-ttu-id="9df98-271">**Réponse :** non.</span><span class="sxs-lookup"><span data-stu-id="9df98-271">**Answer:** No.</span></span> <span data-ttu-id="9df98-272">Il n’est possible d’indiquer qu’une collection pour le moment.</span><span class="sxs-lookup"><span data-stu-id="9df98-272">Only one collection can be specified at this time.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="9df98-273">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="9df98-273">Performance and Tuning</span></span>
<span data-ttu-id="9df98-274">Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="9df98-274">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
