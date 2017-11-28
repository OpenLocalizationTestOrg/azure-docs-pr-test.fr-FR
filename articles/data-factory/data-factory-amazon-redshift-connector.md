---
title: "données Amazon Redshift à l’aide de la fabrique de données aaaMove | Documents Microsoft"
description: "En savoir plus sur la façon de toomove données Amazon Redshift à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 01d15078-58dc-455c-9d9d-98fbdf4ea51e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 2a097320734ebdd57282d250f7fdba35741777f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a><span data-ttu-id="e56b0-103">Déplacer des données depuis Amazon Redshift à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e56b0-103">Move data From Amazon Redshift using Azure Data Factory</span></span>
<span data-ttu-id="e56b0-104">Cet article explique comment toouse hello activité de copie de données Azure Data Factory toomove Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="e56b0-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from Amazon Redshift.</span></span> <span data-ttu-id="e56b0-105">article de Hello s’appuie sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="e56b0-105">hello article builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="e56b0-106">Vous pouvez copier des données à partir du magasin de données récepteur Amazon Redshift tooany pris en charge.</span><span class="sxs-lookup"><span data-stu-id="e56b0-106">You can copy data from Amazon Redshift tooany supported sink data store.</span></span> <span data-ttu-id="e56b0-107">Pour obtenir la liste des magasins de données pris en charge en tant que les récepteurs par l’activité de copie hello, consultez [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="e56b0-107">For a list of data stores supported as sinks by hello copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="e56b0-108">Fabrique de données prend actuellement en charge le déplacement des données à partir des magasins de données Amazon Redshift tooother, mais ne pas pour le déplacement des données à partir d’autres tooAmazon de magasins de données Redshift.</span><span class="sxs-lookup"><span data-stu-id="e56b0-108">Data factory currently supports moving data from Amazon Redshift tooother data stores, but not for moving data from other data stores tooAmazon Redshift.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e56b0-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e56b0-109">Prerequisites</span></span>
* <span data-ttu-id="e56b0-110">Si vous déplacez une banque de données locale données tooan, installez [passerelle de gestion des données](data-factory-data-management-gateway.md) sur un ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="e56b0-110">If you are moving data tooan on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span></span> <span data-ttu-id="e56b0-111">Ensuite, accordez passerelle de gestion des données (utiliser une adresse IP de l’ordinateur de hello) hello tooAmazon Redshift cluster d’accès.</span><span class="sxs-lookup"><span data-stu-id="e56b0-111">Then, Grant Data Management Gateway (use IP address of hello machine) hello access tooAmazon Redshift cluster.</span></span> <span data-ttu-id="e56b0-112">Consultez [cluster de toohello accès autoriser](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) pour obtenir des instructions.</span><span class="sxs-lookup"><span data-stu-id="e56b0-112">See [Authorize access toohello cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span></span>
* <span data-ttu-id="e56b0-113">Si vous déplacez le magasin de données tooan données Azure, consultez [plages IP de centre de données Azure](https://www.microsoft.com/download/details.aspx?id=41653) pour l’adresse IP de calcul de hello et les plages SQL utilisées par les centres de données Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e56b0-113">If you are moving data tooan Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for hello Compute IP address and SQL ranges used by hello Azure data centers.</span></span>

## <a name="getting-started"></a><span data-ttu-id="e56b0-114">Prise en main</span><span class="sxs-lookup"><span data-stu-id="e56b0-114">Getting started</span></span>
<span data-ttu-id="e56b0-115">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’une source Amazon Redshift à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="e56b0-115">You can create a pipeline with a copy activity that moves data from an Amazon Redshift source by using different tools/APIs.</span></span>

<span data-ttu-id="e56b0-116">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="e56b0-116">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="e56b0-117">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="e56b0-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="e56b0-118">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="e56b0-118">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="e56b0-119">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="e56b0-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="e56b0-120">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="e56b0-120">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="e56b0-121">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="e56b0-121">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="e56b0-122">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="e56b0-122">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="e56b0-123">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="e56b0-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="e56b0-124">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="e56b0-124">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="e56b0-125">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="e56b0-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="e56b0-126">Pour voir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données à partir d’une banque de données Amazon Redshift, [exemple de JSON : copier des données d’Amazon Redshift tooAzure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="e56b0-126">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an Amazon Redshift data store, see [JSON example: Copy data from Amazon Redshift tooAzure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="e56b0-127">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifique tooAmazon Redshift :</span><span class="sxs-lookup"><span data-stu-id="e56b0-127">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAmazon Redshift:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="e56b0-128">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="e56b0-128">Linked service properties</span></span>
<span data-ttu-id="e56b0-129">Hello tableau suivant fournit la description pour JSON éléments tooAmazon spécifique Redshift lié service.</span><span class="sxs-lookup"><span data-stu-id="e56b0-129">hello following table provides description for JSON elements specific tooAmazon Redshift linked service.</span></span>

| <span data-ttu-id="e56b0-130">Propriété</span><span class="sxs-lookup"><span data-stu-id="e56b0-130">Property</span></span> | <span data-ttu-id="e56b0-131">Description</span><span class="sxs-lookup"><span data-stu-id="e56b0-131">Description</span></span> | <span data-ttu-id="e56b0-132">Requis</span><span class="sxs-lookup"><span data-stu-id="e56b0-132">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e56b0-133">type</span><span class="sxs-lookup"><span data-stu-id="e56b0-133">type</span></span> |<span data-ttu-id="e56b0-134">propriété de type Hello doit indiquer : **AmazonRedshift**.</span><span class="sxs-lookup"><span data-stu-id="e56b0-134">hello type property must be set to: **AmazonRedshift**.</span></span> |<span data-ttu-id="e56b0-135">Oui</span><span class="sxs-lookup"><span data-stu-id="e56b0-135">Yes</span></span> |
| <span data-ttu-id="e56b0-136">server</span><span class="sxs-lookup"><span data-stu-id="e56b0-136">server</span></span> |<span data-ttu-id="e56b0-137">Nom hôte ou adresse IP du serveur d’Amazon Redshift hello.</span><span class="sxs-lookup"><span data-stu-id="e56b0-137">IP address or host name of hello Amazon Redshift server.</span></span> |<span data-ttu-id="e56b0-138">Oui</span><span class="sxs-lookup"><span data-stu-id="e56b0-138">Yes</span></span> |
| <span data-ttu-id="e56b0-139">port</span><span class="sxs-lookup"><span data-stu-id="e56b0-139">port</span></span> |<span data-ttu-id="e56b0-140">nombre de Hello de port TCP hello hello Amazon Redshift serveur utilise toolisten pour les connexions client.</span><span class="sxs-lookup"><span data-stu-id="e56b0-140">hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.</span></span> |<span data-ttu-id="e56b0-141">Non, valeur par défaut : 5439</span><span class="sxs-lookup"><span data-stu-id="e56b0-141">No, default value: 5439</span></span> |
| <span data-ttu-id="e56b0-142">database</span><span class="sxs-lookup"><span data-stu-id="e56b0-142">database</span></span> |<span data-ttu-id="e56b0-143">Nom de la base de données Amazon Redshift hello.</span><span class="sxs-lookup"><span data-stu-id="e56b0-143">Name of hello Amazon Redshift database.</span></span> |<span data-ttu-id="e56b0-144">Oui</span><span class="sxs-lookup"><span data-stu-id="e56b0-144">Yes</span></span> |
| <span data-ttu-id="e56b0-145">username</span><span class="sxs-lookup"><span data-stu-id="e56b0-145">username</span></span> |<span data-ttu-id="e56b0-146">Nom d’utilisateur qui a la base de données access toohello.</span><span class="sxs-lookup"><span data-stu-id="e56b0-146">Name of user who has access toohello database.</span></span> |<span data-ttu-id="e56b0-147">Oui</span><span class="sxs-lookup"><span data-stu-id="e56b0-147">Yes</span></span> |
| <span data-ttu-id="e56b0-148">password</span><span class="sxs-lookup"><span data-stu-id="e56b0-148">password</span></span> |<span data-ttu-id="e56b0-149">Mot de passe pour le compte d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="e56b0-149">Password for hello user account.</span></span> |<span data-ttu-id="e56b0-150">Oui</span><span class="sxs-lookup"><span data-stu-id="e56b0-150">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="e56b0-151">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="e56b0-151">Dataset properties</span></span>
<span data-ttu-id="e56b0-152">Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="e56b0-152">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="e56b0-153">Les sections comme la structure, la disponibilité et la stratégie sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="e56b0-153">Sections such as structure, availability, and policy are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="e56b0-154">Hello **typeProperties** section est différente pour chaque type de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="e56b0-154">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="e56b0-155">Il fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="e56b0-155">It provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="e56b0-156">jeu de données de type Hello typeProperties section **RelationalTable** (qui comprend de jeu de données Amazon Redshift) a hello propriétés suivantes</span><span class="sxs-lookup"><span data-stu-id="e56b0-156">hello typeProperties section for dataset of type **RelationalTable** (which includes Amazon Redshift dataset) has hello following properties</span></span>

| <span data-ttu-id="e56b0-157">Propriété</span><span class="sxs-lookup"><span data-stu-id="e56b0-157">Property</span></span> | <span data-ttu-id="e56b0-158">Description</span><span class="sxs-lookup"><span data-stu-id="e56b0-158">Description</span></span> | <span data-ttu-id="e56b0-159">Requis</span><span class="sxs-lookup"><span data-stu-id="e56b0-159">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e56b0-160">TableName</span><span class="sxs-lookup"><span data-stu-id="e56b0-160">tableName</span></span> |<span data-ttu-id="e56b0-161">Nom de table hello dans la base de données Amazon Redshift hello ce service lié fait référence à.</span><span class="sxs-lookup"><span data-stu-id="e56b0-161">Name of hello table in hello Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="e56b0-162">Non (si la **requête** de **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="e56b0-162">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="e56b0-163">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="e56b0-163">Copy activity properties</span></span>
<span data-ttu-id="e56b0-164">Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="e56b0-164">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="e56b0-165">Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités.</span><span class="sxs-lookup"><span data-stu-id="e56b0-165">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="e56b0-166">Tandis que les propriétés disponibles dans hello **typeProperties** section d’activité hello varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="e56b0-166">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="e56b0-167">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="e56b0-167">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="e56b0-168">Lorsque la source de l’activité de copie est de type **RelationalSource** (qui inclut Amazon Redshift), hello propriétés suivantes est disponible dans la section de typeProperties :</span><span class="sxs-lookup"><span data-stu-id="e56b0-168">When source of copy activity is of type **RelationalSource** (which includes Amazon Redshift), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="e56b0-169">Propriété</span><span class="sxs-lookup"><span data-stu-id="e56b0-169">Property</span></span> | <span data-ttu-id="e56b0-170">Description</span><span class="sxs-lookup"><span data-stu-id="e56b0-170">Description</span></span> | <span data-ttu-id="e56b0-171">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="e56b0-171">Allowed values</span></span> | <span data-ttu-id="e56b0-172">Requis</span><span class="sxs-lookup"><span data-stu-id="e56b0-172">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e56b0-173">query</span><span class="sxs-lookup"><span data-stu-id="e56b0-173">query</span></span> |<span data-ttu-id="e56b0-174">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="e56b0-174">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e56b0-175">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="e56b0-175">SQL query string.</span></span> <span data-ttu-id="e56b0-176">Par exemple : select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="e56b0-176">For example: select * from MyTable.</span></span> |<span data-ttu-id="e56b0-177">Non (si **tableName** de **dataset** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="e56b0-177">No (if **tableName** of **dataset** is specified)</span></span> |

## <a name="json-example-copy-data-from-amazon-redshift-tooazure-blob"></a><span data-ttu-id="e56b0-178">Exemple de JSON : copier des données d’Amazon Redshift tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="e56b0-178">JSON example: Copy data from Amazon Redshift tooAzure Blob</span></span>
<span data-ttu-id="e56b0-179">Cet exemple montre la base de données toocopy à partir d’un Amazon Redshift tooan stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="e56b0-179">This sample shows how toocopy data from an Amazon Redshift database tooan Azure Blob Storage.</span></span> <span data-ttu-id="e56b0-180">Toutefois, les données peuvent être copiées **directement** tooany de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e56b0-180">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="e56b0-181">exemple Hello a hello suivant des entités de fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="e56b0-181">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="e56b0-182">Un service lié de type [AmazonRedshift](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e56b0-182">A linked service of type [AmazonRedshift](#linked-service-properties).</span></span>
* <span data-ttu-id="e56b0-183">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e56b0-183">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="e56b0-184">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e56b0-184">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
* <span data-ttu-id="e56b0-185">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e56b0-185">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="e56b0-186">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [RelationalSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="e56b0-186">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span></span>

<span data-ttu-id="e56b0-187">exemple Hello copie des données à partir d’un résultat de requête dans l’objet blob de Amazon Redshift tooa toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="e56b0-187">hello sample copies data from a query result in Amazon Redshift tooa blob every hour.</span></span> <span data-ttu-id="e56b0-188">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="e56b0-188">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="e56b0-189">**Service lié Amazon Redshift :**</span><span class="sxs-lookup"><span data-stu-id="e56b0-189">**Amazon Redshift linked service:**</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< hello IP address or host name of hello Amazon Redshift server >",
            "port": <hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.>,
            "database": "<hello database name of hello Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="e56b0-190">**Service lié Azure Storage :**</span><span class="sxs-lookup"><span data-stu-id="e56b0-190">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="e56b0-191">**Jeu de données d’entrée Amazon Redshift :**</span><span class="sxs-lookup"><span data-stu-id="e56b0-191">**Amazon Redshift input dataset:**</span></span>

<span data-ttu-id="e56b0-192">Paramètre `"external": true` informe le service de fabrique de données hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="e56b0-192">Setting `"external": true` informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="e56b0-193">Définir tootrue de cette propriété sur un jeu de données d’entrée qui n’est pas généré par une activité dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="e56b0-193">Set this property tootrue on an input dataset that is not produced by an activity in hello pipeline.</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="e56b0-194">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="e56b0-194">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="e56b0-195">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="e56b0-195">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="e56b0-196">chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="e56b0-196">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="e56b0-197">chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="e56b0-197">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazonredshift/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="e56b0-198">**Activité de copie dans un pipeline, avec une source Azure Redshift (RelationalSource) et un récepteur blob :**</span><span class="sxs-lookup"><span data-stu-id="e56b0-198">**Copy activity in a pipeline with Azure Redshift source (RelationalSource) and Blob sink:**</span></span>

<span data-ttu-id="e56b0-199">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="e56b0-199">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="e56b0-200">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**RelationalSource** et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="e56b0-200">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="e56b0-201">la requête SQL Hello spécifiée pour hello **requête** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.</span><span class="sxs-lookup"><span data-stu-id="e56b0-201">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonRedshiftInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AmazonRedshiftToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-amazon-redshift"></a><span data-ttu-id="e56b0-202">Mappage de type pour Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="e56b0-202">Type mapping for Amazon Redshift</span></span>
<span data-ttu-id="e56b0-203">Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, l’activité de copie effectue les conversions de type automatique à partir de types de sources de toosink types avec hello suivant l’approche en deux étapes :</span><span class="sxs-lookup"><span data-stu-id="e56b0-203">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="e56b0-204">Convertir à partir de la source native types too.NET type</span><span class="sxs-lookup"><span data-stu-id="e56b0-204">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="e56b0-205">Conversion de type de récepteur de toonative de type .NET</span><span class="sxs-lookup"><span data-stu-id="e56b0-205">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="e56b0-206">Lors du déplacement des données tooAmazon Redshift, hello suivant les mappages est utilisé à partir des types de too.NET Amazon Redshift types.</span><span class="sxs-lookup"><span data-stu-id="e56b0-206">When moving data tooAmazon Redshift, hello following mappings are used from Amazon Redshift types too.NET types.</span></span>

| <span data-ttu-id="e56b0-207">Type Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="e56b0-207">Amazon Redshift Type</span></span> | <span data-ttu-id="e56b0-208">Type basé sur .NET</span><span class="sxs-lookup"><span data-stu-id="e56b0-208">.NET Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="e56b0-209">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="e56b0-209">SMALLINT</span></span> |<span data-ttu-id="e56b0-210">Int16</span><span class="sxs-lookup"><span data-stu-id="e56b0-210">Int16</span></span> |
| <span data-ttu-id="e56b0-211">INTEGER</span><span class="sxs-lookup"><span data-stu-id="e56b0-211">INTEGER</span></span> |<span data-ttu-id="e56b0-212">Int32</span><span class="sxs-lookup"><span data-stu-id="e56b0-212">Int32</span></span> |
| <span data-ttu-id="e56b0-213">BIGINT</span><span class="sxs-lookup"><span data-stu-id="e56b0-213">BIGINT</span></span> |<span data-ttu-id="e56b0-214">Int64</span><span class="sxs-lookup"><span data-stu-id="e56b0-214">Int64</span></span> |
| <span data-ttu-id="e56b0-215">DÉCIMAL</span><span class="sxs-lookup"><span data-stu-id="e56b0-215">DECIMAL</span></span> |<span data-ttu-id="e56b0-216">DÉCIMAL</span><span class="sxs-lookup"><span data-stu-id="e56b0-216">Decimal</span></span> |
| <span data-ttu-id="e56b0-217">REAL</span><span class="sxs-lookup"><span data-stu-id="e56b0-217">REAL</span></span> |<span data-ttu-id="e56b0-218">Single</span><span class="sxs-lookup"><span data-stu-id="e56b0-218">Single</span></span> |
| <span data-ttu-id="e56b0-219">DOUBLE PRECISION</span><span class="sxs-lookup"><span data-stu-id="e56b0-219">DOUBLE PRECISION</span></span> |<span data-ttu-id="e56b0-220">Double</span><span class="sxs-lookup"><span data-stu-id="e56b0-220">Double</span></span> |
| <span data-ttu-id="e56b0-221">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="e56b0-221">BOOLEAN</span></span> |<span data-ttu-id="e56b0-222">String</span><span class="sxs-lookup"><span data-stu-id="e56b0-222">String</span></span> |
| <span data-ttu-id="e56b0-223">CHAR</span><span class="sxs-lookup"><span data-stu-id="e56b0-223">CHAR</span></span> |<span data-ttu-id="e56b0-224">String</span><span class="sxs-lookup"><span data-stu-id="e56b0-224">String</span></span> |
| <span data-ttu-id="e56b0-225">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="e56b0-225">VARCHAR</span></span> |<span data-ttu-id="e56b0-226">String</span><span class="sxs-lookup"><span data-stu-id="e56b0-226">String</span></span> |
| <span data-ttu-id="e56b0-227">DATE</span><span class="sxs-lookup"><span data-stu-id="e56b0-227">DATE</span></span> |<span data-ttu-id="e56b0-228">DateTime</span><span class="sxs-lookup"><span data-stu-id="e56b0-228">DateTime</span></span> |
| <span data-ttu-id="e56b0-229">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="e56b0-229">TIMESTAMP</span></span> |<span data-ttu-id="e56b0-230">DateTime</span><span class="sxs-lookup"><span data-stu-id="e56b0-230">DateTime</span></span> |
| <span data-ttu-id="e56b0-231">TEXTE</span><span class="sxs-lookup"><span data-stu-id="e56b0-231">TEXT</span></span> |<span data-ttu-id="e56b0-232">String</span><span class="sxs-lookup"><span data-stu-id="e56b0-232">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="e56b0-233">Mapper les colonnes de source toosink</span><span class="sxs-lookup"><span data-stu-id="e56b0-233">Map source toosink columns</span></span>
<span data-ttu-id="e56b0-234">toolearn sur le mappage des colonnes dans toocolumns du jeu de données source dans le jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="e56b0-234">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="e56b0-235">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="e56b0-235">Repeatable read from relational sources</span></span>
<span data-ttu-id="e56b0-236">Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="e56b0-236">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="e56b0-237">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="e56b0-237">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="e56b0-238">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="e56b0-238">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="e56b0-239">Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée.</span><span class="sxs-lookup"><span data-stu-id="e56b0-239">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="e56b0-240">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="e56b0-240">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="e56b0-241">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="e56b0-241">Performance and Tuning</span></span>
<span data-ttu-id="e56b0-242">Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="e56b0-242">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e56b0-243">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e56b0-243">Next Steps</span></span>
<span data-ttu-id="e56b0-244">Consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="e56b0-244">See hello following articles:</span></span>

* <span data-ttu-id="e56b0-245">[Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec Activité de copie.</span><span class="sxs-lookup"><span data-stu-id="e56b0-245">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
