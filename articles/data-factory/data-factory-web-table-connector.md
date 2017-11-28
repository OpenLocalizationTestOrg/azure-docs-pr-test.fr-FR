---
title: "Déplacer des données depuis Table web à l’aide d’Azure Data Factory | Microsoft Docs"
description: "Découvrez comment transférer des données à partir d’une table dans une page web à l’aide d’Azure Data Factory."
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
ms.openlocfilehash: 9e006bc7289fa0239f1650ac6ad43dd159e3c7e0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a><span data-ttu-id="cc8b8-103">Déplacer des données depuis une source de table web à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="cc8b8-103">Move data from a Web table source using Azure Data Factory</span></span>
<span data-ttu-id="cc8b8-104">Cet article explique comment utiliser l’activité de copie d’Azure Data Factory afin de déplacer les données d’une table dans une page web vers un magasin de données récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from a table in a Web page to a supported sink data store.</span></span> <span data-ttu-id="cc8b8-105">Cet article s’appuie sur l’article des [activités de déplacement des données](data-factory-data-movement-activities.md) qui présente une vue d’ensemble du déplacement des données avec l’activité de copie et la liste de magasins de données pris en charge comme sources/récepteurs.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="cc8b8-106">Actuellement, Data Factory prend uniquement en charge le déplacement de données depuis une table web vers d’autres magasins de données, mais pas l’inverse.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-106">Data factory currently supports only moving data from a Web table to other data stores, but not moving data from other data stores to a Web table destination.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc8b8-107">Pour l’instant, ce connecteur web prend uniquement en charge l’extraction du contenu d’une table à partir d’une page HTML.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-107">This Web connector currently supports only extracting table content from an HTML page.</span></span> <span data-ttu-id="cc8b8-108">Pour récupérer des données à partir d’un point de terminaison HTTP/S, utilisez plutôt le [Connecteur HTTP](data-factory-http-connector.md).</span><span class="sxs-lookup"><span data-stu-id="cc8b8-108">To retrieve data from a HTTP/s endpoint, use [HTTP connector](data-factory-http-connector.md) instead.</span></span>

## <a name="getting-started"></a><span data-ttu-id="cc8b8-109">Prise en main</span><span class="sxs-lookup"><span data-stu-id="cc8b8-109">Getting started</span></span>
<span data-ttu-id="cc8b8-110">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données Cassandra local à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-110">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="cc8b8-111">Le moyen le plus simple de créer un pipeline consiste à utiliser **l’Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-111">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="cc8b8-112">Consultez la page [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant Copier des données.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-112">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="cc8b8-113">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-113">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="cc8b8-114">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-114">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="cc8b8-115">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="cc8b8-115">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="cc8b8-116">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-116">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="cc8b8-117">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-117">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="cc8b8-118">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-118">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="cc8b8-119">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-119">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="cc8b8-120">Lorsque vous utilisez des outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory à l’aide du format JSON.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-120">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="cc8b8-121">Pour consulter un exemple contenant des définitions JSON des entités Data Factory utilisées pour copier des données d’une table web, consultez la section [Exemple JSON : copier des données d’une table web vers Blob Azure](#json-example-copy-data-from-web-table-to-azure-blob) de cet article.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-121">For a sample with JSON definitions for Data Factory entities that are used to copy data from a web table, see [JSON example: Copy data from Web table to Azure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="cc8b8-122">Les sections suivantes fournissent des informations sur les propriétés JSON utilisées pour définir les entités Data Factory spécifiques d’une table web :</span><span class="sxs-lookup"><span data-stu-id="cc8b8-122">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Web table:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="cc8b8-123">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="cc8b8-123">Linked service properties</span></span>
<span data-ttu-id="cc8b8-124">Le tableau suivant fournit la description des éléments JSON spécifiques du service lié Web.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-124">The following table provides description for JSON elements specific to Web linked service.</span></span>

| <span data-ttu-id="cc8b8-125">Propriété</span><span class="sxs-lookup"><span data-stu-id="cc8b8-125">Property</span></span> | <span data-ttu-id="cc8b8-126">Description</span><span class="sxs-lookup"><span data-stu-id="cc8b8-126">Description</span></span> | <span data-ttu-id="cc8b8-127">Requis</span><span class="sxs-lookup"><span data-stu-id="cc8b8-127">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc8b8-128">type</span><span class="sxs-lookup"><span data-stu-id="cc8b8-128">type</span></span> |<span data-ttu-id="cc8b8-129">La propriété de type doit être définie sur **Web**</span><span class="sxs-lookup"><span data-stu-id="cc8b8-129">The type property must be set to: **Web**</span></span> |<span data-ttu-id="cc8b8-130">Oui</span><span class="sxs-lookup"><span data-stu-id="cc8b8-130">Yes</span></span> |
| <span data-ttu-id="cc8b8-131">Url</span><span class="sxs-lookup"><span data-stu-id="cc8b8-131">Url</span></span> |<span data-ttu-id="cc8b8-132">URL de la source web</span><span class="sxs-lookup"><span data-stu-id="cc8b8-132">URL to the Web source</span></span> |<span data-ttu-id="cc8b8-133">Oui</span><span class="sxs-lookup"><span data-stu-id="cc8b8-133">Yes</span></span> |
| <span data-ttu-id="cc8b8-134">authenticationType</span><span class="sxs-lookup"><span data-stu-id="cc8b8-134">authenticationType</span></span> |<span data-ttu-id="cc8b8-135">Anonyme</span><span class="sxs-lookup"><span data-stu-id="cc8b8-135">Anonymous.</span></span> |<span data-ttu-id="cc8b8-136">Oui</span><span class="sxs-lookup"><span data-stu-id="cc8b8-136">Yes</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="cc8b8-137">Utilisation de l’authentification anonyme</span><span class="sxs-lookup"><span data-stu-id="cc8b8-137">Using Anonymous authentication</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="cc8b8-138">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="cc8b8-138">Dataset properties</span></span>
<span data-ttu-id="cc8b8-139">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="cc8b8-139">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="cc8b8-140">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="cc8b8-140">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="cc8b8-141">La section **typeProperties** est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-141">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="cc8b8-142">La section typeProperties pour le jeu de données de type **WebTable** a les propriétés suivantes</span><span class="sxs-lookup"><span data-stu-id="cc8b8-142">The typeProperties section for dataset of type **WebTable** has the following properties</span></span>

| <span data-ttu-id="cc8b8-143">Propriété</span><span class="sxs-lookup"><span data-stu-id="cc8b8-143">Property</span></span> | <span data-ttu-id="cc8b8-144">Description</span><span class="sxs-lookup"><span data-stu-id="cc8b8-144">Description</span></span> | <span data-ttu-id="cc8b8-145">Requis</span><span class="sxs-lookup"><span data-stu-id="cc8b8-145">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="cc8b8-146">type</span><span class="sxs-lookup"><span data-stu-id="cc8b8-146">type</span></span> |<span data-ttu-id="cc8b8-147">Type du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-147">type of the dataset.</span></span> <span data-ttu-id="cc8b8-148">Doit avoir la valeur **WebTable**</span><span class="sxs-lookup"><span data-stu-id="cc8b8-148">must be set to **WebTable**</span></span> |<span data-ttu-id="cc8b8-149">Oui</span><span class="sxs-lookup"><span data-stu-id="cc8b8-149">Yes</span></span> |
| <span data-ttu-id="cc8b8-150">path</span><span class="sxs-lookup"><span data-stu-id="cc8b8-150">path</span></span> |<span data-ttu-id="cc8b8-151">URL relative de la ressource qui contient la table.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-151">A relative URL to the resource that contains the table.</span></span> |<span data-ttu-id="cc8b8-152">Non.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-152">No.</span></span> <span data-ttu-id="cc8b8-153">Quand le chemin d’accès n’est pas spécifié, seule l’URL spécifiée dans la définition du service lié est utilisée.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-153">When path is not specified, only the URL specified in the linked service definition is used.</span></span> |
| <span data-ttu-id="cc8b8-154">index</span><span class="sxs-lookup"><span data-stu-id="cc8b8-154">index</span></span> |<span data-ttu-id="cc8b8-155">Index de la table dans la ressource.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-155">The index of the table in the resource.</span></span> <span data-ttu-id="cc8b8-156">Pour savoir comment obtenir l’index d’une table dans une page HTML, consultez la section [Obtenir l’index d’une table dans une page HTML](#get-index-of-a-table-in-an-html-page) .</span><span class="sxs-lookup"><span data-stu-id="cc8b8-156">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span> |<span data-ttu-id="cc8b8-157">Oui</span><span class="sxs-lookup"><span data-stu-id="cc8b8-157">Yes</span></span> |

<span data-ttu-id="cc8b8-158">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="cc8b8-158">**Example:**</span></span>

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

## <a name="copy-activity-properties"></a><span data-ttu-id="cc8b8-159">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="cc8b8-159">Copy activity properties</span></span>
<span data-ttu-id="cc8b8-160">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="cc8b8-160">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="cc8b8-161">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-161">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="cc8b8-162">En revanche, les propriétés disponibles dans la section typeProperties de l’activité varient pour chaque type d'activité.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-162">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="cc8b8-163">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-163">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="cc8b8-164">Actuellement, lorsque la source de l’activité de copie est de type **WebSource**, aucune propriété supplémentaire n’est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-164">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>


## <a name="json-example-copy-data-from-web-table-to-azure-blob"></a><span data-ttu-id="cc8b8-165">Exemple JSON : copier des données d’une table web vers Blob Azure</span><span class="sxs-lookup"><span data-stu-id="cc8b8-165">JSON example: Copy data from Web table to Azure Blob</span></span>
<span data-ttu-id="cc8b8-166">L’exemple suivant montre :</span><span class="sxs-lookup"><span data-stu-id="cc8b8-166">The following sample shows:</span></span>

1. <span data-ttu-id="cc8b8-167">Un service lié de type [Web](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cc8b8-167">A linked service of type [Web](#linked-service-properties).</span></span>
2. <span data-ttu-id="cc8b8-168">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cc8b8-168">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="cc8b8-169">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [WebTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cc8b8-169">An input [dataset](data-factory-create-datasets.md) of type [WebTable](#dataset-properties).</span></span>
4. <span data-ttu-id="cc8b8-170">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cc8b8-170">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="cc8b8-171">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [WebSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="cc8b8-171">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [WebSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="cc8b8-172">L’exemple copie des données d’une table web vers un objet blob Azure toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-172">The sample copies data from a Web table to an Azure blob every hour.</span></span> <span data-ttu-id="cc8b8-173">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-173">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="cc8b8-174">L’exemple suivant indique comment copier des données à partir d’une table web vers un objet blob Azure.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-174">The following sample shows how to copy data from a Web table to an Azure blob.</span></span> <span data-ttu-id="cc8b8-175">Toutefois, les données peuvent être copiées directement vers l’un des récepteurs indiqués dans l’article [Activités de déplacement des données](data-factory-data-movement-activities.md) , par le biais de l’activité de copie d’Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-175">However, data can be copied directly to any of the sinks stated in the [Data Movement Activities](data-factory-data-movement-activities.md) article by using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="cc8b8-176">**Service lié Web** Cet exemple utilise le service lié Web avec l’authentification anonyme.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-176">**Web linked service** This example uses the Web linked service with anonymous authentication.</span></span> <span data-ttu-id="cc8b8-177">Consultez la section [Service lié Web](#linked-service-properties) pour connaître les différents types d’authentification que vous pouvez utiliser.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-177">See [Web linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="cc8b8-178">**Service lié Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="cc8b8-178">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="cc8b8-179">**Jeu de données d’entrée WebTable** La définition de **external** sur **true** informe le service Data Factory qu’il s’agit d’un jeu de données qui est externe à Data Factory et non produit par une activité dans Data Factory.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-179">**WebTable input dataset** Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="cc8b8-180">Pour savoir comment obtenir l’index d’une table dans une page HTML, consultez la section [Obtenir l’index d’une table dans une page HTML](#get-index-of-a-table-in-an-html-page) .</span><span class="sxs-lookup"><span data-stu-id="cc8b8-180">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span>  
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


<span data-ttu-id="cc8b8-181">**Jeu de données de sortie d’objet Blob Azure**</span><span class="sxs-lookup"><span data-stu-id="cc8b8-181">**Azure Blob output dataset**</span></span>

<span data-ttu-id="cc8b8-182">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="cc8b8-182">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

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



<span data-ttu-id="cc8b8-183">**Pipeline avec activité de copie**</span><span class="sxs-lookup"><span data-stu-id="cc8b8-183">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="cc8b8-184">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-184">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="cc8b8-185">Dans la définition du pipeline JSON, le type **source** est défini sur **WebSource** et le type **sink** est défini sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-185">In the pipeline JSON definition, the **source** type is set to **WebSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="cc8b8-186">Pour obtenir la liste des propriétés prises en charge par WebSource, consultez [propriétés du type WebSource](#copy-activity-type-properties) .</span><span class="sxs-lookup"><span data-stu-id="cc8b8-186">See [WebSource type properties](#copy-activity-type-properties) for the list of properties supported by the WebSource.</span></span>

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
        "description": "Copy from a Web table to an Azure blob",
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

## <a name="get-index-of-a-table-in-an-html-page"></a><span data-ttu-id="cc8b8-187">Obtenir l’index d’une table dans une page HTML</span><span class="sxs-lookup"><span data-stu-id="cc8b8-187">Get index of a table in an HTML page</span></span>
1. <span data-ttu-id="cc8b8-188">Lancez **Excel 2016** et basculez vers l’onglet **Données**.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-188">Launch **Excel 2016** and switch to the **Data** tab.</span></span>  
2. <span data-ttu-id="cc8b8-189">Cliquez sur **Nouvelle requête** dans la barre d’outils, pointez sur **À partir d’autres sources** et cliquez sur **À partir du web**.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-189">Click **New Query** on the toolbar, point to **From Other Sources** and click **From Web**.</span></span>

    ![Menu Power Query](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. <span data-ttu-id="cc8b8-191">Dans la boîte de dialogue **À partir du web**, entrez **l’URL** que vous utiliseriez dans le service lié JSON (par exemple : https://en.wikipedia.org/wiki/), ainsi que le chemin d’accès à spécifier pour le jeu de données (par exemple : AFI%27s_100_Years...100_Movies), puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-191">In the **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for the dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span></span>

    ![Boîte de dialogue À partir du web](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    <span data-ttu-id="cc8b8-193">URL utilisée dans cet exemple : https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span><span class="sxs-lookup"><span data-stu-id="cc8b8-193">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span></span>
4. <span data-ttu-id="cc8b8-194">Si la boîte de dialogue **Accéder au contenu web** apparaît, sélectionnez **l’URL** et **l’authentification** adéquates, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-194">If you see **Access Web content** dialog box, select the right **URL**, **authentication**, and click **Connect**.</span></span>

   ![Boîte de dialogue Accéder au contenu web](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. <span data-ttu-id="cc8b8-196">Cliquez sur un élément de **table** dans l’arborescence pour afficher le contenu de la table, puis sur le bouton **Modifier** du bas.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-196">Click a **table** item in the tree view to see content from the table and then click **Edit** button at the bottom.</span></span>  

   ![Boîte de dialogue Navigateur](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. <span data-ttu-id="cc8b8-198">Dans la fenêtre **Éditeur de requête**, cliquez sur **Éditeur avancé** dans la barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-198">In the **Query Editor** window, click **Advanced Editor** button on the toolbar.</span></span>

    ![Bouton Éditeur avancé](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. <span data-ttu-id="cc8b8-200">Dans la boîte de dialogue Éditeur avancé, le numéro en regard de « Source » est l’index.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-200">In the Advanced Editor dialog box, the number next to "Source" is the index.</span></span>

    ![Éditeur avancé - Index](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

<span data-ttu-id="cc8b8-202">Si vous utilisez Excel 2013, utilisez [Microsoft Power Query pour Excel](https://www.microsoft.com/download/details.aspx?id=39379) pour obtenir l’index.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-202">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) to get the index.</span></span> <span data-ttu-id="cc8b8-203">Pour plus d’informations, consultez l’article [Se connecter à une page web](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) .</span><span class="sxs-lookup"><span data-stu-id="cc8b8-203">See [Connect to a web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span></span> <span data-ttu-id="cc8b8-204">Les étapes sont identiques si vous utilisez [Microsoft Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="cc8b8-204">The steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span></span>

> [!NOTE]
> <span data-ttu-id="cc8b8-205">Pour savoir comment mapper des colonnes d’un jeu de données source à des colonnes d’un jeu de données récepteur, voir [Mappage des colonnes d’un jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="cc8b8-205">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="cc8b8-206">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="cc8b8-206">Performance and Tuning</span></span>
<span data-ttu-id="cc8b8-207">Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="cc8b8-207">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
