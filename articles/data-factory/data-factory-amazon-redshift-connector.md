---
title: "Déplacer des données à partir d’Amazon Redshift à l’aide de Data Factory | Microsoft Docs"
description: "Apprenez à déplacer des données à partir d’Amazon Redshift à l’aide d’Azure Data Factory."
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
ms.openlocfilehash: bccb941363952bb2251629240a88148a6527d62e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a><span data-ttu-id="1a26b-103">Déplacer des données depuis Amazon Redshift à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1a26b-103">Move data From Amazon Redshift using Azure Data Factory</span></span>
<span data-ttu-id="1a26b-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour déplacer des données à partir de Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="1a26b-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from Amazon Redshift.</span></span> <span data-ttu-id="1a26b-105">L’article s’appuie sur l’article [Activités de déplacement des données](data-factory-data-movement-activities.md), qui présente une vue d’ensemble du déplacement de données avec l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="1a26b-105">The article builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="1a26b-106">Vous pouvez copier les données de Amazon Redshift dans tout magasin de données récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="1a26b-106">You can copy data from Amazon Redshift to any supported sink data store.</span></span> <span data-ttu-id="1a26b-107">Consultez les [magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) pour obtenir la liste des magasins de données pris en charge en tant que récepteurs par l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="1a26b-107">For a list of data stores supported as sinks by the copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="1a26b-108">Actuellement, Data Factory prend en charge le déplacement de données d’Amazon Redshift vers d’autres magasins de données, mais pas l’inverse.</span><span class="sxs-lookup"><span data-stu-id="1a26b-108">Data factory currently supports moving data from Amazon Redshift to other data stores, but not for moving data from other data stores to Amazon Redshift.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a26b-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1a26b-109">Prerequisites</span></span>
* <span data-ttu-id="1a26b-110">Si vous déplacez des données vers un magasin de données local, vous devez installer la [passerelle de gestion des données](data-factory-data-management-gateway.md) sur une machine locale.</span><span class="sxs-lookup"><span data-stu-id="1a26b-110">If you are moving data to an on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span></span> <span data-ttu-id="1a26b-111">Donnez ensuite à la passerelle de gestion des données l’accès au cluster d’Amazon Redshift (en utilisant l’adresse IP de la machine).</span><span class="sxs-lookup"><span data-stu-id="1a26b-111">Then, Grant Data Management Gateway (use IP address of the machine) the access to Amazon Redshift cluster.</span></span> <span data-ttu-id="1a26b-112">Pour davantage d’instructions, consultez la rubrique [Authorize access to the cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) (Autoriser l’accès au cluster).</span><span class="sxs-lookup"><span data-stu-id="1a26b-112">See [Authorize access to the cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span></span>
* <span data-ttu-id="1a26b-113">Si vous déplacez des données vers un magasin de données Azure, consultez la page [Plages IP des centres de données Azure](https://www.microsoft.com/download/details.aspx?id=41653) pour connaître les plages d’adresses IP de calcul et plages SQL utilisées par les centres de données Azure.</span><span class="sxs-lookup"><span data-stu-id="1a26b-113">If you are moving data to an Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for the Compute IP address and SQL ranges used by the Azure data centers.</span></span>

## <a name="getting-started"></a><span data-ttu-id="1a26b-114">Prise en main</span><span class="sxs-lookup"><span data-stu-id="1a26b-114">Getting started</span></span>
<span data-ttu-id="1a26b-115">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’une source Amazon Redshift à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="1a26b-115">You can create a pipeline with a copy activity that moves data from an Amazon Redshift source by using different tools/APIs.</span></span>

<span data-ttu-id="1a26b-116">Le moyen le plus simple de créer un pipeline consiste à utiliser l’**Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="1a26b-116">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="1a26b-117">Consultez la page [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant Copier des données.</span><span class="sxs-lookup"><span data-stu-id="1a26b-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="1a26b-118">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="1a26b-118">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="1a26b-119">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="1a26b-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="1a26b-120">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1a26b-120">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="1a26b-121">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="1a26b-121">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="1a26b-122">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="1a26b-122">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="1a26b-123">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="1a26b-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="1a26b-124">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="1a26b-124">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="1a26b-125">Lorsque vous utilisez des outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory au format JSON.</span><span class="sxs-lookup"><span data-stu-id="1a26b-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="1a26b-126">Pour consulter un exemple contenant des définitions JSON pour les entités Data Factory utilisées pour copier des données d’un magasin de données Amazon Redshift, consultez la section [Exemple JSON : copier des données depuis un système Amazon Redshift vers Blob Azure](#json-example-copy-data-from-amazon-redshift-to-azure-blob) de cet article.</span><span class="sxs-lookup"><span data-stu-id="1a26b-126">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon Redshift data store, see [JSON example: Copy data from Amazon Redshift to Azure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="1a26b-127">Les sections suivantes fournissent des informations sur les propriétés JSON utilisées pour définir les entités Data Factory spécifiques à Amazon Redshift :</span><span class="sxs-lookup"><span data-stu-id="1a26b-127">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon Redshift:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="1a26b-128">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="1a26b-128">Linked service properties</span></span>
<span data-ttu-id="1a26b-129">Le tableau suivant fournit la description des éléments JSON spécifiques au service lié Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="1a26b-129">The following table provides description for JSON elements specific to Amazon Redshift linked service.</span></span>

| <span data-ttu-id="1a26b-130">Propriété</span><span class="sxs-lookup"><span data-stu-id="1a26b-130">Property</span></span> | <span data-ttu-id="1a26b-131">Description</span><span class="sxs-lookup"><span data-stu-id="1a26b-131">Description</span></span> | <span data-ttu-id="1a26b-132">Requis</span><span class="sxs-lookup"><span data-stu-id="1a26b-132">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a26b-133">type</span><span class="sxs-lookup"><span data-stu-id="1a26b-133">type</span></span> |<span data-ttu-id="1a26b-134">La propriété de type doit être définie sur : **AmazonRedshift**.</span><span class="sxs-lookup"><span data-stu-id="1a26b-134">The type property must be set to: **AmazonRedshift**.</span></span> |<span data-ttu-id="1a26b-135">Oui</span><span class="sxs-lookup"><span data-stu-id="1a26b-135">Yes</span></span> |
| <span data-ttu-id="1a26b-136">server</span><span class="sxs-lookup"><span data-stu-id="1a26b-136">server</span></span> |<span data-ttu-id="1a26b-137">Nom d’hôte ou adresse IP du serveur Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="1a26b-137">IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="1a26b-138">Oui</span><span class="sxs-lookup"><span data-stu-id="1a26b-138">Yes</span></span> |
| <span data-ttu-id="1a26b-139">port</span><span class="sxs-lookup"><span data-stu-id="1a26b-139">port</span></span> |<span data-ttu-id="1a26b-140">Le numéro du port TCP utilisé par le serveur Amazon Redshift pour écouter les connexions clientes.</span><span class="sxs-lookup"><span data-stu-id="1a26b-140">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="1a26b-141">Non, valeur par défaut : 5439</span><span class="sxs-lookup"><span data-stu-id="1a26b-141">No, default value: 5439</span></span> |
| <span data-ttu-id="1a26b-142">database</span><span class="sxs-lookup"><span data-stu-id="1a26b-142">database</span></span> |<span data-ttu-id="1a26b-143">Nom de la base de données Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="1a26b-143">Name of the Amazon Redshift database.</span></span> |<span data-ttu-id="1a26b-144">Oui</span><span class="sxs-lookup"><span data-stu-id="1a26b-144">Yes</span></span> |
| <span data-ttu-id="1a26b-145">username</span><span class="sxs-lookup"><span data-stu-id="1a26b-145">username</span></span> |<span data-ttu-id="1a26b-146">Nom d’utilisateur ayant accès à la base de données.</span><span class="sxs-lookup"><span data-stu-id="1a26b-146">Name of user who has access to the database.</span></span> |<span data-ttu-id="1a26b-147">Oui</span><span class="sxs-lookup"><span data-stu-id="1a26b-147">Yes</span></span> |
| <span data-ttu-id="1a26b-148">password</span><span class="sxs-lookup"><span data-stu-id="1a26b-148">password</span></span> |<span data-ttu-id="1a26b-149">Mot de passe du compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1a26b-149">Password for the user account.</span></span> |<span data-ttu-id="1a26b-150">Oui</span><span class="sxs-lookup"><span data-stu-id="1a26b-150">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="1a26b-151">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="1a26b-151">Dataset properties</span></span>
<span data-ttu-id="1a26b-152">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="1a26b-152">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="1a26b-153">Les sections comme la structure, la disponibilité et la stratégie sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="1a26b-153">Sections such as structure, availability, and policy are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="1a26b-154">La section **typeProperties** est différente pour chaque type de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="1a26b-154">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="1a26b-155">Elle fournit des informations sur l’emplacement des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="1a26b-155">It provides information about the location of the data in the data store.</span></span> <span data-ttu-id="1a26b-156">La section typeProperties pour le jeu de données de type **RelationalTable** (qui inclut le jeu de données Amazon Redshift) a les propriétés suivantes</span><span class="sxs-lookup"><span data-stu-id="1a26b-156">The typeProperties section for dataset of type **RelationalTable** (which includes Amazon Redshift dataset) has the following properties</span></span>

| <span data-ttu-id="1a26b-157">Propriété</span><span class="sxs-lookup"><span data-stu-id="1a26b-157">Property</span></span> | <span data-ttu-id="1a26b-158">Description</span><span class="sxs-lookup"><span data-stu-id="1a26b-158">Description</span></span> | <span data-ttu-id="1a26b-159">Requis</span><span class="sxs-lookup"><span data-stu-id="1a26b-159">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a26b-160">TableName</span><span class="sxs-lookup"><span data-stu-id="1a26b-160">tableName</span></span> |<span data-ttu-id="1a26b-161">Nom de la table dans l’instance de base de données Amazon Redshift à laquelle le service lié fait référence.</span><span class="sxs-lookup"><span data-stu-id="1a26b-161">Name of the table in the Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="1a26b-162">Non (si la **requête** de **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="1a26b-162">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="1a26b-163">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="1a26b-163">Copy activity properties</span></span>
<span data-ttu-id="1a26b-164">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="1a26b-164">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="1a26b-165">Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités.</span><span class="sxs-lookup"><span data-stu-id="1a26b-165">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="1a26b-166">En revanche, les propriétés disponibles dans la section **typeProperties** de l’activité varient pour chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="1a26b-166">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="1a26b-167">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="1a26b-167">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="1a26b-168">Lorsque la source d’une activité de copie est de type **RelationalSource** (qui inclut Amazon Redshift), les propriétés suivantes sont disponibles dans la section typeProperties :</span><span class="sxs-lookup"><span data-stu-id="1a26b-168">When source of copy activity is of type **RelationalSource** (which includes Amazon Redshift), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="1a26b-169">Propriété</span><span class="sxs-lookup"><span data-stu-id="1a26b-169">Property</span></span> | <span data-ttu-id="1a26b-170">Description</span><span class="sxs-lookup"><span data-stu-id="1a26b-170">Description</span></span> | <span data-ttu-id="1a26b-171">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="1a26b-171">Allowed values</span></span> | <span data-ttu-id="1a26b-172">Requis</span><span class="sxs-lookup"><span data-stu-id="1a26b-172">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a26b-173">query</span><span class="sxs-lookup"><span data-stu-id="1a26b-173">query</span></span> |<span data-ttu-id="1a26b-174">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="1a26b-174">Use the custom query to read data.</span></span> |<span data-ttu-id="1a26b-175">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="1a26b-175">SQL query string.</span></span> <span data-ttu-id="1a26b-176">Par exemple : select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="1a26b-176">For example: select * from MyTable.</span></span> |<span data-ttu-id="1a26b-177">Non (si **tableName** de **dataset** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="1a26b-177">No (if **tableName** of **dataset** is specified)</span></span> |

## <a name="json-example-copy-data-from-amazon-redshift-to-azure-blob"></a><span data-ttu-id="1a26b-178">Exemple JSON : copie de données à partir d’Amazon Redshift vers le stockage d’objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="1a26b-178">JSON example: Copy data from Amazon Redshift to Azure Blob</span></span>
<span data-ttu-id="1a26b-179">Cet exemple indique comment copier des données à partir d’une base de données Amazon Redshift locale vers un système de stockage Blob Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1a26b-179">This sample shows how to copy data from an Amazon Redshift database to an Azure Blob Storage.</span></span> <span data-ttu-id="1a26b-180">Toutefois, les données peuvent être copiées **directement** vers l’un des récepteurs indiqués [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) , via l’activité de copie d’Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1a26b-180">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="1a26b-181">L’exemple contient les entités de fabrique de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="1a26b-181">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="1a26b-182">Un service lié de type [AmazonRedshift](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a26b-182">A linked service of type [AmazonRedshift](#linked-service-properties).</span></span>
* <span data-ttu-id="1a26b-183">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a26b-183">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="1a26b-184">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a26b-184">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
* <span data-ttu-id="1a26b-185">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a26b-185">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="1a26b-186">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [RelationalSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a26b-186">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span></span>

<span data-ttu-id="1a26b-187">L’exemple copie toutes les heures les données de résultat d’une requête de base de données Amazon Redshift vers un objet blob.</span><span class="sxs-lookup"><span data-stu-id="1a26b-187">The sample copies data from a query result in Amazon Redshift to a blob every hour.</span></span> <span data-ttu-id="1a26b-188">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="1a26b-188">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="1a26b-189">**Service lié Amazon Redshift :**</span><span class="sxs-lookup"><span data-stu-id="1a26b-189">**Amazon Redshift linked service:**</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< The IP address or host name of the Amazon Redshift server >",
            "port": <The number of the TCP port that the Amazon Redshift server uses to listen for client connections.>,
            "database": "<The database name of the Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="1a26b-190">**Service lié Azure Storage :**</span><span class="sxs-lookup"><span data-stu-id="1a26b-190">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="1a26b-191">**Jeu de données d’entrée Amazon Redshift :**</span><span class="sxs-lookup"><span data-stu-id="1a26b-191">**Amazon Redshift input dataset:**</span></span>

<span data-ttu-id="1a26b-192">Le paramètre `"external": true` informe le service Data Factory que ce jeu de données est externe à la fabrique de données et non produit par une activité dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="1a26b-192">Setting `"external": true` informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="1a26b-193">Définissez cette propriété sur true sur un jeu de données d’entrée qui n’est pas produit par une activité dans le pipeline.</span><span class="sxs-lookup"><span data-stu-id="1a26b-193">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span></span>

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

<span data-ttu-id="1a26b-194">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="1a26b-194">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="1a26b-195">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="1a26b-195">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="1a26b-196">Le chemin d’accès du dossier pour l’objet blob est évalué dynamiquement en fonction de l’heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="1a26b-196">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="1a26b-197">Le chemin d'accès du dossier utilise l'année, le mois, le jour et l'heure de l'heure de début.</span><span class="sxs-lookup"><span data-stu-id="1a26b-197">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="1a26b-198">**Activité de copie dans un pipeline, avec une source Azure Redshift (RelationalSource) et un récepteur blob :**</span><span class="sxs-lookup"><span data-stu-id="1a26b-198">**Copy activity in a pipeline with Azure Redshift source (RelationalSource) and Blob sink:**</span></span>

<span data-ttu-id="1a26b-199">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="1a26b-199">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="1a26b-200">Dans la définition du pipeline JSON, le type **source** est défini sur **RelationalSource** et le type **sink** est défini sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="1a26b-200">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="1a26b-201">La requête SQL spécifiée pour la propriété **query** sélectionne les données de la dernière heure à copier.</span><span class="sxs-lookup"><span data-stu-id="1a26b-201">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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
### <a name="type-mapping-for-amazon-redshift"></a><span data-ttu-id="1a26b-202">Mappage de type pour Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="1a26b-202">Type mapping for Amazon Redshift</span></span>
<span data-ttu-id="1a26b-203">Comme mentionné dans l’article consacré aux [activités de déplacement des données](data-factory-data-movement-activities.md) , l’activité de copie convertit automatiquement des types source en types récepteur à l’aide de l’approche en deux étapes suivante :</span><span class="sxs-lookup"><span data-stu-id="1a26b-203">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="1a26b-204">Conversion de types natifs source en types .NET</span><span class="sxs-lookup"><span data-stu-id="1a26b-204">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="1a26b-205">Conversion de types .NET en types récepteur natifs</span><span class="sxs-lookup"><span data-stu-id="1a26b-205">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="1a26b-206">Lors du déplacement de données vers Amazon Redshift, les mappages suivants sont utilisés pour passer des types Amazon Redshift aux types .NET.</span><span class="sxs-lookup"><span data-stu-id="1a26b-206">When moving data to Amazon Redshift, the following mappings are used from Amazon Redshift types to .NET types.</span></span>

| <span data-ttu-id="1a26b-207">Type Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="1a26b-207">Amazon Redshift Type</span></span> | <span data-ttu-id="1a26b-208">Type basé sur .NET</span><span class="sxs-lookup"><span data-stu-id="1a26b-208">.NET Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="1a26b-209">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="1a26b-209">SMALLINT</span></span> |<span data-ttu-id="1a26b-210">Int16</span><span class="sxs-lookup"><span data-stu-id="1a26b-210">Int16</span></span> |
| <span data-ttu-id="1a26b-211">INTEGER</span><span class="sxs-lookup"><span data-stu-id="1a26b-211">INTEGER</span></span> |<span data-ttu-id="1a26b-212">Int32</span><span class="sxs-lookup"><span data-stu-id="1a26b-212">Int32</span></span> |
| <span data-ttu-id="1a26b-213">BIGINT</span><span class="sxs-lookup"><span data-stu-id="1a26b-213">BIGINT</span></span> |<span data-ttu-id="1a26b-214">Int64</span><span class="sxs-lookup"><span data-stu-id="1a26b-214">Int64</span></span> |
| <span data-ttu-id="1a26b-215">DÉCIMAL</span><span class="sxs-lookup"><span data-stu-id="1a26b-215">DECIMAL</span></span> |<span data-ttu-id="1a26b-216">DÉCIMAL</span><span class="sxs-lookup"><span data-stu-id="1a26b-216">Decimal</span></span> |
| <span data-ttu-id="1a26b-217">REAL</span><span class="sxs-lookup"><span data-stu-id="1a26b-217">REAL</span></span> |<span data-ttu-id="1a26b-218">Single</span><span class="sxs-lookup"><span data-stu-id="1a26b-218">Single</span></span> |
| <span data-ttu-id="1a26b-219">DOUBLE PRECISION</span><span class="sxs-lookup"><span data-stu-id="1a26b-219">DOUBLE PRECISION</span></span> |<span data-ttu-id="1a26b-220">Double</span><span class="sxs-lookup"><span data-stu-id="1a26b-220">Double</span></span> |
| <span data-ttu-id="1a26b-221">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="1a26b-221">BOOLEAN</span></span> |<span data-ttu-id="1a26b-222">String</span><span class="sxs-lookup"><span data-stu-id="1a26b-222">String</span></span> |
| <span data-ttu-id="1a26b-223">CHAR</span><span class="sxs-lookup"><span data-stu-id="1a26b-223">CHAR</span></span> |<span data-ttu-id="1a26b-224">String</span><span class="sxs-lookup"><span data-stu-id="1a26b-224">String</span></span> |
| <span data-ttu-id="1a26b-225">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="1a26b-225">VARCHAR</span></span> |<span data-ttu-id="1a26b-226">String</span><span class="sxs-lookup"><span data-stu-id="1a26b-226">String</span></span> |
| <span data-ttu-id="1a26b-227">DATE</span><span class="sxs-lookup"><span data-stu-id="1a26b-227">DATE</span></span> |<span data-ttu-id="1a26b-228">DateTime</span><span class="sxs-lookup"><span data-stu-id="1a26b-228">DateTime</span></span> |
| <span data-ttu-id="1a26b-229">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="1a26b-229">TIMESTAMP</span></span> |<span data-ttu-id="1a26b-230">DateTime</span><span class="sxs-lookup"><span data-stu-id="1a26b-230">DateTime</span></span> |
| <span data-ttu-id="1a26b-231">TEXTE</span><span class="sxs-lookup"><span data-stu-id="1a26b-231">TEXT</span></span> |<span data-ttu-id="1a26b-232">String</span><span class="sxs-lookup"><span data-stu-id="1a26b-232">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="1a26b-233">Mapper les colonnes source aux colonnes du récepteur</span><span class="sxs-lookup"><span data-stu-id="1a26b-233">Map source to sink columns</span></span>
<span data-ttu-id="1a26b-234">Pour en savoir plus sur le mappage de colonnes du jeu de données source à des colonnes du jeu de données récepteur, voir [Mappage des colonnes d’un jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="1a26b-234">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="1a26b-235">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="1a26b-235">Repeatable read from relational sources</span></span>
<span data-ttu-id="1a26b-236">Lorsque vous copiez des données à partir de magasins de données relationnels, gardez à l’esprit la répétabilité de l’opération, afin d’éviter des résultats imprévus.</span><span class="sxs-lookup"><span data-stu-id="1a26b-236">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="1a26b-237">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="1a26b-237">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="1a26b-238">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="1a26b-238">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="1a26b-239">Lorsqu’une tranche est réexécutée d’une manière ou d’une autre, vous devez vous assurer que les mêmes données sont lues et ce, quel que soit le nombre d’exécutions de la tranche.</span><span class="sxs-lookup"><span data-stu-id="1a26b-239">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="1a26b-240">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="1a26b-240">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="1a26b-241">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="1a26b-241">Performance and Tuning</span></span>
<span data-ttu-id="1a26b-242">Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="1a26b-242">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a26b-243">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1a26b-243">Next Steps</span></span>
<span data-ttu-id="1a26b-244">Consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="1a26b-244">See the following articles:</span></span>

* <span data-ttu-id="1a26b-245">[Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec Activité de copie.</span><span class="sxs-lookup"><span data-stu-id="1a26b-245">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
