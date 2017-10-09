---
title: "aaaMove des données à partir de la Table Web à l’aide d’Azure Data Factory | Documents Microsoft"
description: "Découvrez comment toomove les données d’une table dans un site Web page à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e52216305583ebbe71ed896522f361bb22f01278
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a><span data-ttu-id="098e0-103">Déplacer des données depuis une source de table web à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="098e0-103">Move data from a Web table source using Azure Data Factory</span></span>
<span data-ttu-id="098e0-104">Cet article décrit comment toouse hello activité de copie de données de toomove Azure Data Factory à partir d’une table dans une page Web de tooa prises en charge le magasin de données récepteur.</span><span class="sxs-lookup"><span data-stu-id="098e0-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from a table in a Web page tooa supported sink data store.</span></span> <span data-ttu-id="098e0-105">Cet article s’appuie sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article qui présente une vue d’ensemble du déplacement des données avec la liste des activités et hello copie de banques de données pris en charge en tant que sources/récepteurs.</span><span class="sxs-lookup"><span data-stu-id="098e0-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="098e0-106">Fabrique de données prend en charge uniquement déplacer les données à partir de données Web table tooother stocke, mais ne pas déplacer les données à partir d’autres données stocke à destination de table tooa Web.</span><span class="sxs-lookup"><span data-stu-id="098e0-106">Data factory currently supports only moving data from a Web table tooother data stores, but not moving data from other data stores tooa Web table destination.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="098e0-107">Pour l’instant, ce connecteur web prend uniquement en charge l’extraction du contenu d’une table à partir d’une page HTML.</span><span class="sxs-lookup"><span data-stu-id="098e0-107">This Web connector currently supports only extracting table content from an HTML page.</span></span> <span data-ttu-id="098e0-108">tooretrieve des données à partir d’un point de terminaison HTTP/s, utilisez [connecteur HTTP](data-factory-http-connector.md) à la place.</span><span class="sxs-lookup"><span data-stu-id="098e0-108">tooretrieve data from a HTTP/s endpoint, use [HTTP connector](data-factory-http-connector.md) instead.</span></span>

## <a name="getting-started"></a><span data-ttu-id="098e0-109">Prise en main</span><span class="sxs-lookup"><span data-stu-id="098e0-109">Getting started</span></span>
<span data-ttu-id="098e0-110">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données Cassandra local à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="098e0-110">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="098e0-111">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="098e0-111">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="098e0-112">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="098e0-112">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="098e0-113">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="098e0-113">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="098e0-114">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="098e0-114">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="098e0-115">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="098e0-115">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="098e0-116">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="098e0-116">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="098e0-117">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="098e0-117">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="098e0-118">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="098e0-118">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="098e0-119">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="098e0-119">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="098e0-120">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="098e0-120">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="098e0-121">Pour voir un exemple avec des définitions pour les entités de fabrique de données qui sont utilisés toocopy des données à partir d’une table de web JSON, [exemple de JSON : copier des données à partir de la table de Web tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="098e0-121">For a sample with JSON definitions for Data Factory entities that are used toocopy data from a web table, see [JSON example: Copy data from Web table tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="098e0-122">Hello les sections suivantes fournit des détails sur les propriétés JSON de table de Web utilisés toodefine Data Factory entités tooa spécifique :</span><span class="sxs-lookup"><span data-stu-id="098e0-122">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Web table:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="098e0-123">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="098e0-123">Linked service properties</span></span>
<span data-ttu-id="098e0-124">Hello tableau suivant fournit la description du service de tooWeb spécifique lié éléments JSON.</span><span class="sxs-lookup"><span data-stu-id="098e0-124">hello following table provides description for JSON elements specific tooWeb linked service.</span></span>

| <span data-ttu-id="098e0-125">Propriété</span><span class="sxs-lookup"><span data-stu-id="098e0-125">Property</span></span> | <span data-ttu-id="098e0-126">Description</span><span class="sxs-lookup"><span data-stu-id="098e0-126">Description</span></span> | <span data-ttu-id="098e0-127">Requis</span><span class="sxs-lookup"><span data-stu-id="098e0-127">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="098e0-128">type</span><span class="sxs-lookup"><span data-stu-id="098e0-128">type</span></span> |<span data-ttu-id="098e0-129">propriété de type Hello doit indiquer : **Web**</span><span class="sxs-lookup"><span data-stu-id="098e0-129">hello type property must be set to: **Web**</span></span> |<span data-ttu-id="098e0-130">Oui</span><span class="sxs-lookup"><span data-stu-id="098e0-130">Yes</span></span> |
| <span data-ttu-id="098e0-131">Url</span><span class="sxs-lookup"><span data-stu-id="098e0-131">Url</span></span> |<span data-ttu-id="098e0-132">Source de l’URL toohello Web</span><span class="sxs-lookup"><span data-stu-id="098e0-132">URL toohello Web source</span></span> |<span data-ttu-id="098e0-133">Oui</span><span class="sxs-lookup"><span data-stu-id="098e0-133">Yes</span></span> |
| <span data-ttu-id="098e0-134">authenticationType</span><span class="sxs-lookup"><span data-stu-id="098e0-134">authenticationType</span></span> |<span data-ttu-id="098e0-135">Anonyme</span><span class="sxs-lookup"><span data-stu-id="098e0-135">Anonymous.</span></span> |<span data-ttu-id="098e0-136">Oui</span><span class="sxs-lookup"><span data-stu-id="098e0-136">Yes</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="098e0-137">Utilisation de l’authentification anonyme</span><span class="sxs-lookup"><span data-stu-id="098e0-137">Using Anonymous authentication</span></span>

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="098e0-138">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="098e0-138">Dataset properties</span></span>
<span data-ttu-id="098e0-139">Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="098e0-139">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="098e0-140">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="098e0-140">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="098e0-141">Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="098e0-141">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="098e0-142">jeu de données de type Hello typeProperties section **WebTable** a les propriétés suivantes de hello</span><span class="sxs-lookup"><span data-stu-id="098e0-142">hello typeProperties section for dataset of type **WebTable** has hello following properties</span></span>

| <span data-ttu-id="098e0-143">Propriété</span><span class="sxs-lookup"><span data-stu-id="098e0-143">Property</span></span> | <span data-ttu-id="098e0-144">Description</span><span class="sxs-lookup"><span data-stu-id="098e0-144">Description</span></span> | <span data-ttu-id="098e0-145">Requis</span><span class="sxs-lookup"><span data-stu-id="098e0-145">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="098e0-146">type</span><span class="sxs-lookup"><span data-stu-id="098e0-146">type</span></span> |<span data-ttu-id="098e0-147">Type de jeu de données hello.</span><span class="sxs-lookup"><span data-stu-id="098e0-147">type of hello dataset.</span></span> <span data-ttu-id="098e0-148">doit être défini trop**WebTable**</span><span class="sxs-lookup"><span data-stu-id="098e0-148">must be set too**WebTable**</span></span> |<span data-ttu-id="098e0-149">Oui</span><span class="sxs-lookup"><span data-stu-id="098e0-149">Yes</span></span> |
| <span data-ttu-id="098e0-150">path</span><span class="sxs-lookup"><span data-stu-id="098e0-150">path</span></span> |<span data-ttu-id="098e0-151">Une ressource URL toohello relative qui contient la table de hello.</span><span class="sxs-lookup"><span data-stu-id="098e0-151">A relative URL toohello resource that contains hello table.</span></span> |<span data-ttu-id="098e0-152">Non.</span><span class="sxs-lookup"><span data-stu-id="098e0-152">No.</span></span> <span data-ttu-id="098e0-153">Lorsque le chemin d’accès n’est pas spécifié, seul hello URL spécifiée dans la définition de service hello lié est utilisé.</span><span class="sxs-lookup"><span data-stu-id="098e0-153">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> |
| <span data-ttu-id="098e0-154">index</span><span class="sxs-lookup"><span data-stu-id="098e0-154">index</span></span> |<span data-ttu-id="098e0-155">index de Hello de table hello dans la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="098e0-155">hello index of hello table in hello resource.</span></span> <span data-ttu-id="098e0-156">Consultez [Get index d’une table dans une page HTML](#get-index-of-a-table-in-an-html-page) section pour l’index de toogetting étapes d’une table dans une page HTML.</span><span class="sxs-lookup"><span data-stu-id="098e0-156">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span> |<span data-ttu-id="098e0-157">Oui</span><span class="sxs-lookup"><span data-stu-id="098e0-157">Yes</span></span> |

<span data-ttu-id="098e0-158">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="098e0-158">**Example:**</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="098e0-159">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="098e0-159">Copy activity properties</span></span>
<span data-ttu-id="098e0-160">Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="098e0-160">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="098e0-161">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="098e0-161">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="098e0-162">Alors que les propriétés disponibles dans la section typeProperties hello activité hello varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="098e0-162">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="098e0-163">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="098e0-163">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="098e0-164">Actuellement, lorsque source hello dans l’activité de copie est de type **WebSource**, aucune des propriétés supplémentaires ne sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="098e0-164">Currently, when hello source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>


## <a name="json-example-copy-data-from-web-table-tooazure-blob"></a><span data-ttu-id="098e0-165">Exemple de JSON : copier des données à partir de la table de Web tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="098e0-165">JSON example: Copy data from Web table tooAzure Blob</span></span>
<span data-ttu-id="098e0-166">Hello ci-dessous illustre d’exemple :</span><span class="sxs-lookup"><span data-stu-id="098e0-166">hello following sample shows:</span></span>

1. <span data-ttu-id="098e0-167">Un service lié de type [Web](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="098e0-167">A linked service of type [Web](#linked-service-properties).</span></span>
2. <span data-ttu-id="098e0-168">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="098e0-168">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="098e0-169">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [WebTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="098e0-169">An input [dataset](data-factory-create-datasets.md) of type [WebTable](#dataset-properties).</span></span>
4. <span data-ttu-id="098e0-170">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="098e0-170">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="098e0-171">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [WebSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="098e0-171">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [WebSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="098e0-172">exemple Hello copie des données à partir d’un tooan de table Azure blob Web toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="098e0-172">hello sample copies data from a Web table tooan Azure blob every hour.</span></span> <span data-ttu-id="098e0-173">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="098e0-173">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="098e0-174">Hello suivant l’exemple montre comment toocopy des données à partir d’un tooan de table Web Azure blob.</span><span class="sxs-lookup"><span data-stu-id="098e0-174">hello following sample shows how toocopy data from a Web table tooan Azure blob.</span></span> <span data-ttu-id="098e0-175">Toutefois, les données peuvent être copiées directement tooany Hello récepteurs hello est indiqué dans [les activités de déplacement des données](data-factory-data-movement-activities.md) article à l’aide de l’activité de copie de hello dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="098e0-175">However, data can be copied directly tooany of hello sinks stated in hello [Data Movement Activities](data-factory-data-movement-activities.md) article by using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="098e0-176">**Service lié de Web** cet exemple utilise hello Web lié à service avec l’authentification anonyme.</span><span class="sxs-lookup"><span data-stu-id="098e0-176">**Web linked service** This example uses hello Web linked service with anonymous authentication.</span></span> <span data-ttu-id="098e0-177">Consultez la section [Service lié Web](#linked-service-properties) pour connaître les différents types d’authentification que vous pouvez utiliser.</span><span class="sxs-lookup"><span data-stu-id="098e0-177">See [Web linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="098e0-178">**Service lié Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="098e0-178">**Azure Storage linked service**</span></span>

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="098e0-179">**Jeu de données d’entrée WebTable** paramètre **externe** trop**true** informe le service de fabrique de données hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité Bonjour fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="098e0-179">**WebTable input dataset** Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="098e0-180">Consultez [Get index d’une table dans une page HTML](#get-index-of-a-table-in-an-html-page) section pour l’index de toogetting étapes d’une table dans une page HTML.</span><span class="sxs-lookup"><span data-stu-id="098e0-180">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span>  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```


<span data-ttu-id="098e0-181">**Jeu de données de sortie d’objet Blob Azure**</span><span class="sxs-lookup"><span data-stu-id="098e0-181">**Azure Blob output dataset**</span></span>

<span data-ttu-id="098e0-182">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="098e0-182">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```



<span data-ttu-id="098e0-183">**Pipeline avec activité de copie**</span><span class="sxs-lookup"><span data-stu-id="098e0-183">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="098e0-184">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="098e0-184">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="098e0-185">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**WebSource** et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="098e0-185">In hello pipeline JSON definition, hello **source** type is set too**WebSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="098e0-186">Consultez [WebSource les propriétés de type](#copy-activity-type-properties) pour la liste des propriétés prises en charge par hello WebSource hello.</span><span class="sxs-lookup"><span data-stu-id="098e0-186">See [WebSource type properties](#copy-activity-type-properties) for hello list of properties supported by hello WebSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
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

## <a name="get-index-of-a-table-in-an-html-page"></a><span data-ttu-id="098e0-187">Obtenir l’index d’une table dans une page HTML</span><span class="sxs-lookup"><span data-stu-id="098e0-187">Get index of a table in an HTML page</span></span>
1. <span data-ttu-id="098e0-188">Lancez **Excel 2016** et basculez toohello **données** onglet.</span><span class="sxs-lookup"><span data-stu-id="098e0-188">Launch **Excel 2016** and switch toohello **Data** tab.</span></span>  
2. <span data-ttu-id="098e0-189">Cliquez sur **nouvelle requête** dans la barre d’outils de hello, pointez trop**à partir d’autres Sources** et cliquez sur **à partir du Web**.</span><span class="sxs-lookup"><span data-stu-id="098e0-189">Click **New Query** on hello toolbar, point too**From Other Sources** and click **From Web**.</span></span>

    ![Menu Power Query](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. <span data-ttu-id="098e0-191">Bonjour **à partir du Web** boîte de dialogue, entrez **URL** où vous souhaitez utiliser dans des service JSON lié (par exemple : https://en.wikipedia.org/wiki/), ainsi que le chemin d’accès que vous spécifiez pour le jeu de données hello (par exemple : AFI % 27s_100_Years... 100_Movies), puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="098e0-191">In hello **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for hello dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span></span>

    ![Boîte de dialogue À partir du web](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    <span data-ttu-id="098e0-193">URL utilisée dans cet exemple : https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span><span class="sxs-lookup"><span data-stu-id="098e0-193">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span></span>
4. <span data-ttu-id="098e0-194">Si vous voyez **contenu Access Web** boîte de dialogue, à droite de hello sélectionnez **URL**, **authentification**, puis cliquez sur **Connect**.</span><span class="sxs-lookup"><span data-stu-id="098e0-194">If you see **Access Web content** dialog box, select hello right **URL**, **authentication**, and click **Connect**.</span></span>

   ![Boîte de dialogue Accéder au contenu web](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. <span data-ttu-id="098e0-196">Cliquez sur un **table** hello arborescence afficher toosee le contenu à partir de la table de hello d’élément, puis cliquez sur **modifier** bouton bas hello.</span><span class="sxs-lookup"><span data-stu-id="098e0-196">Click a **table** item in hello tree view toosee content from hello table and then click **Edit** button at hello bottom.</span></span>  

   ![Boîte de dialogue Navigateur](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. <span data-ttu-id="098e0-198">Bonjour **l’éditeur de requête** fenêtre, cliquez sur **éditeur avancé** bouton de barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="098e0-198">In hello **Query Editor** window, click **Advanced Editor** button on hello toolbar.</span></span>

    ![Bouton Éditeur avancé](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. <span data-ttu-id="098e0-200">Dans la boîte de dialogue Éditeur avancé hello, hello nombre suivant trop « Source » est index de hello.</span><span class="sxs-lookup"><span data-stu-id="098e0-200">In hello Advanced Editor dialog box, hello number next too"Source" is hello index.</span></span>

    ![Éditeur avancé - Index](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

<span data-ttu-id="098e0-202">Si vous utilisez Excel 2013, utilisez [Microsoft Power Query pour Excel](https://www.microsoft.com/download/details.aspx?id=39379) index de hello tooget.</span><span class="sxs-lookup"><span data-stu-id="098e0-202">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) tooget hello index.</span></span> <span data-ttu-id="098e0-203">Consultez [page de connexion tooa web](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="098e0-203">See [Connect tooa web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span></span> <span data-ttu-id="098e0-204">étapes de Hello sont identiques si vous utilisez [Microsoft Power BI pour Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="098e0-204">hello steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span></span>

> [!NOTE]
> <span data-ttu-id="098e0-205">colonnes de toomap de toocolumns du jeu de données source à partir du jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="098e0-205">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="098e0-206">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="098e0-206">Performance and Tuning</span></span>
<span data-ttu-id="098e0-207">Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="098e0-207">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
