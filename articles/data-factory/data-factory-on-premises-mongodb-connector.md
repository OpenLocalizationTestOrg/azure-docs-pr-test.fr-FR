---
title: "Déplacer des données depuis MongoDB à l’aide de Data Factory | Microsoft Docs"
description: "Découvrez comment déplacer des données depuis une base de données MongoDB à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 10ca7d9a-7715-4446-bf59-2d2876584550
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: ac4ff55c765a5b874b81714c3d0063a5b4765a05
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a><span data-ttu-id="d7244-103">Déplacer des données depuis MongoDB à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d7244-103">Move data From MongoDB using Azure Data Factory</span></span>
<span data-ttu-id="d7244-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour déplacer des données à partir d’une base de données MongoDB locale.</span><span class="sxs-lookup"><span data-stu-id="d7244-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MongoDB database.</span></span> <span data-ttu-id="d7244-105">Il s’appuie sur l’article relatif aux [activités de déplacement des données](data-factory-data-movement-activities.md), qui présente une vue d’ensemble du déplacement des données avec l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="d7244-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="d7244-106">Vous pouvez copier les données d’un magasin de données MongoDB local dans tout magasin de données récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="d7244-106">You can copy data from an on-premises MongoDB data store to any supported sink data store.</span></span> <span data-ttu-id="d7244-107">Consultez le tableau [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) pour obtenir la liste des magasins de données pris en charge en tant que récepteurs par l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="d7244-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="d7244-108">Actuellement, les fabriques de données ne prennent en charge que le déplacement des données d’un magasin de données MongoDB vers d’autres magasins de données, mais pas l’inverse.</span><span class="sxs-lookup"><span data-stu-id="d7244-108">Data factory currently supports only moving data from a MongoDB data store to other data stores, but not for moving data from other data stores to an MongoDB datastore.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d7244-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d7244-109">Prerequisites</span></span>
<span data-ttu-id="d7244-110">Pour permettre au service Azure Data Factory de se connecter à votre base de données MongoDB locale, vous devez installer les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="d7244-110">For the Azure Data Factory service to be able to connect to your on-premises MongoDB database, you must install the following components:</span></span>

- <span data-ttu-id="d7244-111">Versions MongoDB prises en charge : 2.4, 2.6, 3.0 et 3.2.</span><span class="sxs-lookup"><span data-stu-id="d7244-111">Supported MongoDB versions are:  2.4, 2.6, 3.0, and 3.2.</span></span>
- <span data-ttu-id="d7244-112">Une passerelle de gestion de données sur l’ordinateur qui héberge la base de données ou sur un autre ordinateur afin d’éviter toute mise en concurrence avec la base de données pour les ressources.</span><span class="sxs-lookup"><span data-stu-id="d7244-112">Data Management Gateway on the same machine that hosts the database or on a separate machine to avoid competing for resources with the database.</span></span> <span data-ttu-id="d7244-113">La passerelle de gestion de données est un logiciel qui connecte des sources de données locales à des services cloud de manière gérée et sécurisée.</span><span class="sxs-lookup"><span data-stu-id="d7244-113">Data Management Gateway is a software that connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="d7244-114">Consultez l’article [Passerelle de gestion des données](data-factory-data-management-gateway.md) pour obtenir des informations détaillées sur la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="d7244-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="d7244-115">Consultez l’article [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) pour obtenir des instructions détaillées sur la configuration de la passerelle, un pipeline de données, pour déplacer des données.</span><span class="sxs-lookup"><span data-stu-id="d7244-115">See [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

    <span data-ttu-id="d7244-116">L’installation de la passerelle engendre automatiquement l’installation d’un pilote Microsoft ODBC MongoDB, utilisé pour se connecter à MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d7244-116">When you install the gateway, it automatically installs a Microsoft MongoDB ODBC driver used to connect to MongoDB.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d7244-117">Vous devez utiliser la passerelle pour vous connecter à MongoDB même si elle est hébergée sur des machines virtuelles IaaS Azure.</span><span class="sxs-lookup"><span data-stu-id="d7244-117">You need to use the gateway to connect to MongoDB even if it is hosted in Azure IaaS VMs.</span></span> <span data-ttu-id="d7244-118">Si vous essayez de vous connecter à une instance MongoDB hébergée dans le cloud, vous pouvez également installer l’instance de la passerelle dans la machine virtuelle IaaS.</span><span class="sxs-lookup"><span data-stu-id="d7244-118">If you are trying to connect to an instance of MongoDB hosted in cloud, you can also install the gateway instance in the IaaS VM.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d7244-119">Prise en main</span><span class="sxs-lookup"><span data-stu-id="d7244-119">Getting started</span></span>
<span data-ttu-id="d7244-120">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données MongoDB local à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="d7244-120">You can create a pipeline with a copy activity that moves data from an on-premises MongoDB data store by using different tools/APIs.</span></span>

<span data-ttu-id="d7244-121">Le moyen le plus simple de créer un pipeline consiste à utiliser **l’Assistant Copie**.</span><span class="sxs-lookup"><span data-stu-id="d7244-121">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="d7244-122">Consultez la page [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant Copier des données.</span><span class="sxs-lookup"><span data-stu-id="d7244-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="d7244-123">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="d7244-123">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d7244-124">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="d7244-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="d7244-125">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="d7244-125">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="d7244-126">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="d7244-126">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="d7244-127">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="d7244-127">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="d7244-128">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="d7244-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="d7244-129">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="d7244-129">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="d7244-130">Lorsque vous utilisez les outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory à l’aide du format JSON.</span><span class="sxs-lookup"><span data-stu-id="d7244-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="d7244-131">Pour consulter un exemple contenant des définitions JSON pour les entités Data Factory qui sont utilisées pour copier des données d’un magasin de données MongoDB local, consultez la section [Exemple JSON : copier des données de MongoDB vers Blob Azure](#json-example-copy-data-from-mongodb-to-azure-blob) de cet article.</span><span class="sxs-lookup"><span data-stu-id="d7244-131">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MongoDB data store, see [JSON example: Copy data from MongoDB to Azure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="d7244-132">Les sections suivantes contiennent des informations détaillées sur les propriétés JSON utilisées pour définir les entités Data Factory propres à la source MongoDB :</span><span class="sxs-lookup"><span data-stu-id="d7244-132">The following sections provide details about JSON properties that are used to define Data Factory entities specific to MongoDB source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d7244-133">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="d7244-133">Linked service properties</span></span>
<span data-ttu-id="d7244-134">La table suivante fournit une description des éléments JSON spécifiques au service lié **OnPremisesMongoDB** .</span><span class="sxs-lookup"><span data-stu-id="d7244-134">The following table provides description for JSON elements specific to **OnPremisesMongoDB** linked service.</span></span>

| <span data-ttu-id="d7244-135">Propriété</span><span class="sxs-lookup"><span data-stu-id="d7244-135">Property</span></span> | <span data-ttu-id="d7244-136">Description</span><span class="sxs-lookup"><span data-stu-id="d7244-136">Description</span></span> | <span data-ttu-id="d7244-137">Requis</span><span class="sxs-lookup"><span data-stu-id="d7244-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d7244-138">type</span><span class="sxs-lookup"><span data-stu-id="d7244-138">type</span></span> |<span data-ttu-id="d7244-139">Le type de propriété doit être défini sur **OnPremisesMongoDb**</span><span class="sxs-lookup"><span data-stu-id="d7244-139">The type property must be set to: **OnPremisesMongoDb**</span></span> |<span data-ttu-id="d7244-140">Oui</span><span class="sxs-lookup"><span data-stu-id="d7244-140">Yes</span></span> |
| <span data-ttu-id="d7244-141">server</span><span class="sxs-lookup"><span data-stu-id="d7244-141">server</span></span> |<span data-ttu-id="d7244-142">Nom d’hôte ou adresse IP du serveur MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d7244-142">IP address or host name of the MongoDB server.</span></span> |<span data-ttu-id="d7244-143">Oui</span><span class="sxs-lookup"><span data-stu-id="d7244-143">Yes</span></span> |
| <span data-ttu-id="d7244-144">port</span><span class="sxs-lookup"><span data-stu-id="d7244-144">port</span></span> |<span data-ttu-id="d7244-145">Le port TCP utilisé par le serveur MongoDB pour écouter les connexions clientes.</span><span class="sxs-lookup"><span data-stu-id="d7244-145">TCP port that the MongoDB server uses to listen for client connections.</span></span> |<span data-ttu-id="d7244-146">Facultatif, valeur par défaut : 27017</span><span class="sxs-lookup"><span data-stu-id="d7244-146">Optional, default value: 27017</span></span> |
| <span data-ttu-id="d7244-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="d7244-147">authenticationType</span></span> |<span data-ttu-id="d7244-148">De base ou anonyme.</span><span class="sxs-lookup"><span data-stu-id="d7244-148">Basic, or Anonymous.</span></span> |<span data-ttu-id="d7244-149">Oui</span><span class="sxs-lookup"><span data-stu-id="d7244-149">Yes</span></span> |
| <span data-ttu-id="d7244-150">username</span><span class="sxs-lookup"><span data-stu-id="d7244-150">username</span></span> |<span data-ttu-id="d7244-151">Compte d’utilisateur pour accéder à MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d7244-151">User account to access MongoDB.</span></span> |<span data-ttu-id="d7244-152">Oui (si l’authentification de base est utilisée).</span><span class="sxs-lookup"><span data-stu-id="d7244-152">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="d7244-153">password</span><span class="sxs-lookup"><span data-stu-id="d7244-153">password</span></span> |<span data-ttu-id="d7244-154">Mot de passe pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d7244-154">Password for the user.</span></span> |<span data-ttu-id="d7244-155">Oui (si l’authentification de base est utilisée).</span><span class="sxs-lookup"><span data-stu-id="d7244-155">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="d7244-156">authSource</span><span class="sxs-lookup"><span data-stu-id="d7244-156">authSource</span></span> |<span data-ttu-id="d7244-157">Nom de la base de données MongoDB que vous souhaitez utiliser pour vérifier vos informations d’identification pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="d7244-157">Name of the MongoDB database that you want to use to check your credentials for authentication.</span></span> |<span data-ttu-id="d7244-158">Facultatif (si l’authentification de base est utilisée).</span><span class="sxs-lookup"><span data-stu-id="d7244-158">Optional (if basic authentication is used).</span></span> <span data-ttu-id="d7244-159">Par défaut : utilise le compte d’administrateur et la base de données spécifiée à l’aide de la propriété databaseName.</span><span class="sxs-lookup"><span data-stu-id="d7244-159">default: uses the admin account and the database specified using databaseName property.</span></span> |
| <span data-ttu-id="d7244-160">databaseName</span><span class="sxs-lookup"><span data-stu-id="d7244-160">databaseName</span></span> |<span data-ttu-id="d7244-161">Nom de la base de données MongoDB à laquelle vous souhaitez accéder.</span><span class="sxs-lookup"><span data-stu-id="d7244-161">Name of the MongoDB database that you want to access.</span></span> |<span data-ttu-id="d7244-162">Oui</span><span class="sxs-lookup"><span data-stu-id="d7244-162">Yes</span></span> |
| <span data-ttu-id="d7244-163">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d7244-163">gatewayName</span></span> |<span data-ttu-id="d7244-164">Nom de la passerelle qui accède au magasin de données.</span><span class="sxs-lookup"><span data-stu-id="d7244-164">Name of the gateway that accesses the data store.</span></span> |<span data-ttu-id="d7244-165">Oui</span><span class="sxs-lookup"><span data-stu-id="d7244-165">Yes</span></span> |
| <span data-ttu-id="d7244-166">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="d7244-166">encryptedCredential</span></span> |<span data-ttu-id="d7244-167">Informations d’identification chiffrées par la passerelle.</span><span class="sxs-lookup"><span data-stu-id="d7244-167">Credential encrypted by gateway.</span></span> |<span data-ttu-id="d7244-168">Facultatif</span><span class="sxs-lookup"><span data-stu-id="d7244-168">Optional</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="d7244-169">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="d7244-169">Dataset properties</span></span>
<span data-ttu-id="d7244-170">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="d7244-170">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="d7244-171">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="d7244-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="d7244-172">La section **typeProperties** est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="d7244-172">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="d7244-173">La section typeProperties pour le jeu de données de type **MongoDbCollection** a les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="d7244-173">The typeProperties section for dataset of type **MongoDbCollection** has the following properties:</span></span>

| <span data-ttu-id="d7244-174">Propriété</span><span class="sxs-lookup"><span data-stu-id="d7244-174">Property</span></span> | <span data-ttu-id="d7244-175">Description</span><span class="sxs-lookup"><span data-stu-id="d7244-175">Description</span></span> | <span data-ttu-id="d7244-176">Requis</span><span class="sxs-lookup"><span data-stu-id="d7244-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d7244-177">collectionName</span><span class="sxs-lookup"><span data-stu-id="d7244-177">collectionName</span></span> |<span data-ttu-id="d7244-178">Nom de la collection dans la base de données MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d7244-178">Name of the collection in MongoDB database.</span></span> |<span data-ttu-id="d7244-179">Oui</span><span class="sxs-lookup"><span data-stu-id="d7244-179">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="d7244-180">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="d7244-180">Copy activity properties</span></span>
<span data-ttu-id="d7244-181">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="d7244-181">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="d7244-182">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="d7244-182">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="d7244-183">En revanche, les propriétés disponibles dans la section **typeProperties** de l'activité varient pour chaque type d'activité.</span><span class="sxs-lookup"><span data-stu-id="d7244-183">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="d7244-184">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="d7244-184">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="d7244-185">Lorsque la source est de type **MongoDbSource** , les propriétés suivantes sont disponibles dans la section typeProperties :</span><span class="sxs-lookup"><span data-stu-id="d7244-185">When the source is of type **MongoDbSource** the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="d7244-186">Propriété</span><span class="sxs-lookup"><span data-stu-id="d7244-186">Property</span></span> | <span data-ttu-id="d7244-187">Description</span><span class="sxs-lookup"><span data-stu-id="d7244-187">Description</span></span> | <span data-ttu-id="d7244-188">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="d7244-188">Allowed values</span></span> | <span data-ttu-id="d7244-189">Requis</span><span class="sxs-lookup"><span data-stu-id="d7244-189">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d7244-190">query</span><span class="sxs-lookup"><span data-stu-id="d7244-190">query</span></span> |<span data-ttu-id="d7244-191">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="d7244-191">Use the custom query to read data.</span></span> |<span data-ttu-id="d7244-192">Chaîne de requête SQL-92.</span><span class="sxs-lookup"><span data-stu-id="d7244-192">SQL-92 query string.</span></span> <span data-ttu-id="d7244-193">Par exemple : select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="d7244-193">For example: select * from MyTable.</span></span> |<span data-ttu-id="d7244-194">Non (si **collectionName** du **jeu de données** est spécifié)</span><span class="sxs-lookup"><span data-stu-id="d7244-194">No (if **collectionName** of **dataset** is specified)</span></span> |



## <a name="json-example-copy-data-from-mongodb-to-azure-blob"></a><span data-ttu-id="d7244-195">Exemple JSON : copier des données de MongoDB vers Blob Azure</span><span class="sxs-lookup"><span data-stu-id="d7244-195">JSON example: Copy data from MongoDB to Azure Blob</span></span>
<span data-ttu-id="d7244-196">Cet exemple présente des exemples de définition JSON que vous pouvez utiliser pour créer un pipeline à l’aide du [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), de [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [d’Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d7244-196">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="d7244-197">Il indique comment copier des données d’un magasin de données MongoDB local vers Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d7244-197">It shows how to copy data from an on-premises MongoDB to an Azure Blob Storage.</span></span> <span data-ttu-id="d7244-198">Toutefois, les données peuvent être copiées vers l’un des récepteurs indiqués [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) , via l’activité de copie d’Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d7244-198">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="d7244-199">L’exemple contient les entités de fabrique de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="d7244-199">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="d7244-200">Un service lié de type [OnPremisesMongoDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d7244-200">A linked service of type [OnPremisesMongoDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="d7244-201">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d7244-201">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="d7244-202">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [MongoDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d7244-202">An input [dataset](data-factory-create-datasets.md) of type [MongoDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="d7244-203">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d7244-203">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="d7244-204">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [MongoDbSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d7244-204">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [MongoDbSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="d7244-205">L’exemple copie toutes les heures les données de résultat d’une requête de base de données MongoDB vers un objet blob.</span><span class="sxs-lookup"><span data-stu-id="d7244-205">The sample copies data from a query result in MongoDB database to a blob every hour.</span></span> <span data-ttu-id="d7244-206">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="d7244-206">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="d7244-207">Dans un premier temps, configurez la passerelle de gestion des données en suivant les instructions de l’article [Passerelle de gestion des données](data-factory-data-management-gateway.md) .</span><span class="sxs-lookup"><span data-stu-id="d7244-207">As a first step, setup the data management gateway as per the instructions in the [Data Management Gateway](data-factory-data-management-gateway.md) article.</span></span>

<span data-ttu-id="d7244-208">**Service lié MongoDB :**</span><span class="sxs-lookup"><span data-stu-id="d7244-208">**MongoDB linked service:**</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< The IP address or host name of the MongoDB server >",  
            "port": "<The number of the TCP port that the MongoDB server uses to listen for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< The database that you want to use to check your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

<span data-ttu-id="d7244-209">**Service lié Azure Storage :**</span><span class="sxs-lookup"><span data-stu-id="d7244-209">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="d7244-210">La définition de « external » sur « true » du **jeu de données d’entrée MongoDB** informe le service Data Factory que la table est externe à la fabrique de données et non produite par une activité dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="d7244-210">**MongoDB input dataset:** Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
     "name":  "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"    
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="d7244-211">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="d7244-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="d7244-212">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="d7244-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d7244-213">Le chemin d’accès du dossier pour l’objet blob est évalué dynamiquement en fonction de l’heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="d7244-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="d7244-214">Le chemin d'accès du dossier utilise l'année, le mois, le jour et l'heure de l'heure de début.</span><span class="sxs-lookup"><span data-stu-id="d7244-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/frommongodb/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="d7244-215">**Activité de copie dans un pipeline avec une source MongoDB et un récepteur d’objets blob :**</span><span class="sxs-lookup"><span data-stu-id="d7244-215">**Copy activity in a pipeline with MongoDB source and Blob sink:**</span></span>

<span data-ttu-id="d7244-216">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d'entrée et de sortie ci-dessus, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="d7244-216">The pipeline contains a Copy Activity that is configured to use the above input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="d7244-217">Dans la définition du pipeline JSON, le type **source** est défini sur **MongoDbSource** et le type **sink** est défini sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d7244-217">In the pipeline JSON definition, the **source** type is set to **MongoDbSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="d7244-218">La requête SQL spécifiée pour la propriété **query** sélectionne les données de la dernière heure à copier.</span><span class="sxs-lookup"><span data-stu-id="d7244-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "MongoDbSource",
                        "query": "$$Text.Format('select * from  MyTable where LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "MongoDbInputDataset"
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
                "name": "MongoDBToAzureBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```


## <a name="schema-by-data-factory"></a><span data-ttu-id="d7244-219">Schéma par Data Factory</span><span class="sxs-lookup"><span data-stu-id="d7244-219">Schema by Data Factory</span></span>
<span data-ttu-id="d7244-220">Le service Azure Data Factory déduit le schéma à partir d’une collection MongoDB à l’aide des 100 derniers documents dans la collection.</span><span class="sxs-lookup"><span data-stu-id="d7244-220">Azure Data Factory service infers schema from a MongoDB collection by using the latest 100 documents in the collection.</span></span> <span data-ttu-id="d7244-221">Si ces 100 documents ne contiennent pas de schéma complet, certaines colonnes peuvent être ignorées lors de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="d7244-221">If these 100 documents do not contain full schema, some columns may be ignored during the copy operation.</span></span>

## <a name="type-mapping-for-mongodb"></a><span data-ttu-id="d7244-222">Mappage de type pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="d7244-222">Type mapping for MongoDB</span></span>
<span data-ttu-id="d7244-223">Comme mentionné dans l’article consacré aux [activités de déplacement des données](data-factory-data-movement-activities.md) , l’activité de copie convertit automatiquement les types source en types récepteur à l’aide de l’approche en 2 étapes suivante :</span><span class="sxs-lookup"><span data-stu-id="d7244-223">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="d7244-224">Conversion de types natifs source en types .NET</span><span class="sxs-lookup"><span data-stu-id="d7244-224">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="d7244-225">Conversion de types .NET en types récepteur natifs</span><span class="sxs-lookup"><span data-stu-id="d7244-225">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="d7244-226">Lors du déplacement de données vers MongoDB, les mappages suivants sont utilisés pour passer des types MongoDB aux types .NET.</span><span class="sxs-lookup"><span data-stu-id="d7244-226">When moving data to MongoDB the following mappings are used from MongoDB types to .NET types.</span></span>

| <span data-ttu-id="d7244-227">Type MongoDB</span><span class="sxs-lookup"><span data-stu-id="d7244-227">MongoDB type</span></span> | <span data-ttu-id="d7244-228">Type de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="d7244-228">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="d7244-229">Fichier binaire</span><span class="sxs-lookup"><span data-stu-id="d7244-229">Binary</span></span> |<span data-ttu-id="d7244-230">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d7244-230">Byte[]</span></span> |
| <span data-ttu-id="d7244-231">Boolean</span><span class="sxs-lookup"><span data-stu-id="d7244-231">Boolean</span></span> |<span data-ttu-id="d7244-232">Boolean</span><span class="sxs-lookup"><span data-stu-id="d7244-232">Boolean</span></span> |
| <span data-ttu-id="d7244-233">Date</span><span class="sxs-lookup"><span data-stu-id="d7244-233">Date</span></span> |<span data-ttu-id="d7244-234">DateTime</span><span class="sxs-lookup"><span data-stu-id="d7244-234">DateTime</span></span> |
| <span data-ttu-id="d7244-235">NumberDouble</span><span class="sxs-lookup"><span data-stu-id="d7244-235">NumberDouble</span></span> |<span data-ttu-id="d7244-236">Double</span><span class="sxs-lookup"><span data-stu-id="d7244-236">Double</span></span> |
| <span data-ttu-id="d7244-237">NumberInt</span><span class="sxs-lookup"><span data-stu-id="d7244-237">NumberInt</span></span> |<span data-ttu-id="d7244-238">Int32</span><span class="sxs-lookup"><span data-stu-id="d7244-238">Int32</span></span> |
| <span data-ttu-id="d7244-239">NumberLong</span><span class="sxs-lookup"><span data-stu-id="d7244-239">NumberLong</span></span> |<span data-ttu-id="d7244-240">Int64</span><span class="sxs-lookup"><span data-stu-id="d7244-240">Int64</span></span> |
| <span data-ttu-id="d7244-241">ObjectID</span><span class="sxs-lookup"><span data-stu-id="d7244-241">ObjectID</span></span> |<span data-ttu-id="d7244-242">Chaîne</span><span class="sxs-lookup"><span data-stu-id="d7244-242">String</span></span> |
| <span data-ttu-id="d7244-243">Chaîne</span><span class="sxs-lookup"><span data-stu-id="d7244-243">String</span></span> |<span data-ttu-id="d7244-244">Chaîne</span><span class="sxs-lookup"><span data-stu-id="d7244-244">String</span></span> |
| <span data-ttu-id="d7244-245">UUID</span><span class="sxs-lookup"><span data-stu-id="d7244-245">UUID</span></span> |<span data-ttu-id="d7244-246">Guid</span><span class="sxs-lookup"><span data-stu-id="d7244-246">Guid</span></span> |
| <span data-ttu-id="d7244-247">Object</span><span class="sxs-lookup"><span data-stu-id="d7244-247">Object</span></span> |<span data-ttu-id="d7244-248">Renormalisé dans des colonnes aplaties avec « _ » comme séparateur imbriqué</span><span class="sxs-lookup"><span data-stu-id="d7244-248">Renormalized into flatten columns with “_” as nested separator</span></span> |

> [!NOTE]
> <span data-ttu-id="d7244-249">Pour en savoir plus sur la prise en charge des tableaux à l’aide de tables virtuelles, reportez-vous à la section [Prise en charge des types complexes à l’aide de tables virtuelles](#support-for-complex-types-using-virtual-tables) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d7244-249">To learn about support for arrays using virtual tables, refer to [Support for complex types using virtual tables](#support-for-complex-types-using-virtual-tables) section below.</span></span>

<span data-ttu-id="d7244-250">Actuellement, les types de données MongoDB suivants ne sont pas pris en charge : DBPointer, JavaScript, clé max./min., expression régulière, symbole, horodatage, non définie</span><span class="sxs-lookup"><span data-stu-id="d7244-250">Currently, the following MongoDB data types are not supported: DBPointer, JavaScript, Max/Min key, Regular Expression, Symbol, Timestamp, Undefined</span></span>

## <a name="support-for-complex-types-using-virtual-tables"></a><span data-ttu-id="d7244-251">Prise en charge des types complexes à l’aide de tables virtuelles</span><span class="sxs-lookup"><span data-stu-id="d7244-251">Support for complex types using virtual tables</span></span>
<span data-ttu-id="d7244-252">Azure Data Factory utilise un pilote ODBC intégré pour assurer la connexion à votre base de données MongoDB et copier des données à partir de cette dernière.</span><span class="sxs-lookup"><span data-stu-id="d7244-252">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your MongoDB database.</span></span> <span data-ttu-id="d7244-253">Pour les types complexes tels que des tableaux ou des objets avec des types différents entre les documents, le pilote normalise de nouveau les données dans les tables virtuelles correspondantes.</span><span class="sxs-lookup"><span data-stu-id="d7244-253">For complex types such as arrays or objects with different types across the documents, the driver re-normalizes data into corresponding virtual tables.</span></span> <span data-ttu-id="d7244-254">En particulier, si une table contient de telles colonnes, le pilote génère les tables virtuelles suivantes :</span><span class="sxs-lookup"><span data-stu-id="d7244-254">Specifically, if a table contains such columns, the driver generates the following virtual tables:</span></span>

* <span data-ttu-id="d7244-255">Une **table de base**, qui contient les mêmes données que la table réelle, à l’exception des colonnes de type complexe.</span><span class="sxs-lookup"><span data-stu-id="d7244-255">A **base table**, which contains the same data as the real table except for the complex type columns.</span></span> <span data-ttu-id="d7244-256">La table de base utilise le même nom que la table réelle qu’elle représente.</span><span class="sxs-lookup"><span data-stu-id="d7244-256">The base table uses the same name as the real table that it represents.</span></span>
* <span data-ttu-id="d7244-257">Une **table virtuelle** pour chaque colonne de type complexe, qui étend les données imbriquées.</span><span class="sxs-lookup"><span data-stu-id="d7244-257">A **virtual table** for each complex type column, which expands the nested data.</span></span> <span data-ttu-id="d7244-258">Le nom des tables virtuelles est composé du nom de la table réelle, d’un séparateur « _ » et du nom du tableau ou de l’objet.</span><span class="sxs-lookup"><span data-stu-id="d7244-258">The virtual tables are named using the name of the real table, a separator “_” and the name of the array or object.</span></span>

<span data-ttu-id="d7244-259">Les tables virtuelles font référence aux données présentées dans la table réelle, de manière à permettre au pilote d’accéder aux données dénormalisées.</span><span class="sxs-lookup"><span data-stu-id="d7244-259">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span></span> <span data-ttu-id="d7244-260">Consultez la section Exemple ci-dessous pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="d7244-260">See Example section below details.</span></span> <span data-ttu-id="d7244-261">Vous pouvez accéder au contenu des tableaux MongoDB en interrogeant et en joignant les tables virtuelles.</span><span class="sxs-lookup"><span data-stu-id="d7244-261">You can access the content of MongoDB arrays by querying and joining the virtual tables.</span></span>

<span data-ttu-id="d7244-262">Vous pouvez utiliser [l’Assistant de copie](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) afin d’afficher de manière intuitive la liste des tables dans la base de données MongoDB, y compris les tables virtuelles, et de prévisualiser les données qui s’y trouvent.</span><span class="sxs-lookup"><span data-stu-id="d7244-262">You can use the [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) to intuitively view the list of tables in MongoDB database including the virtual tables, and preview the data inside.</span></span> <span data-ttu-id="d7244-263">Vous pouvez également construire une requête dans l’Assistant de copie et valider pour voir le résultat.</span><span class="sxs-lookup"><span data-stu-id="d7244-263">You can also construct a query in the Copy Wizard and validate to see the result.</span></span>

### <a name="example"></a><span data-ttu-id="d7244-264">Exemple</span><span class="sxs-lookup"><span data-stu-id="d7244-264">Example</span></span>
<span data-ttu-id="d7244-265">Par exemple, « ExampleTable » ci-dessous est une table MongoDB qui dispose d’une colonne avec un tableau d’objets dans chaque cellule (Factures) et d’une colonne avec un tableau de types scalaires (Évaluations).</span><span class="sxs-lookup"><span data-stu-id="d7244-265">For example, “ExampleTable” below is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.</span></span>

| <span data-ttu-id="d7244-266">_id</span><span class="sxs-lookup"><span data-stu-id="d7244-266">_id</span></span> | <span data-ttu-id="d7244-267">Nom du client</span><span class="sxs-lookup"><span data-stu-id="d7244-267">Customer Name</span></span> | <span data-ttu-id="d7244-268">Factures</span><span class="sxs-lookup"><span data-stu-id="d7244-268">Invoices</span></span> | <span data-ttu-id="d7244-269">Niveau de service</span><span class="sxs-lookup"><span data-stu-id="d7244-269">Service Level</span></span> | <span data-ttu-id="d7244-270">Évaluations</span><span class="sxs-lookup"><span data-stu-id="d7244-270">Ratings</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="d7244-271">1111</span><span class="sxs-lookup"><span data-stu-id="d7244-271">1111</span></span> |<span data-ttu-id="d7244-272">ABC</span><span class="sxs-lookup"><span data-stu-id="d7244-272">ABC</span></span> |<span data-ttu-id="d7244-273">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span><span class="sxs-lookup"><span data-stu-id="d7244-273">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span></span> |<span data-ttu-id="d7244-274">Silver</span><span class="sxs-lookup"><span data-stu-id="d7244-274">Silver</span></span> |<span data-ttu-id="d7244-275">[5,6]</span><span class="sxs-lookup"><span data-stu-id="d7244-275">[5,6]</span></span> |
| <span data-ttu-id="d7244-276">2222</span><span class="sxs-lookup"><span data-stu-id="d7244-276">2222</span></span> |<span data-ttu-id="d7244-277">XYZ</span><span class="sxs-lookup"><span data-stu-id="d7244-277">XYZ</span></span> |<span data-ttu-id="d7244-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span><span class="sxs-lookup"><span data-stu-id="d7244-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span></span> |<span data-ttu-id="d7244-279">Gold</span><span class="sxs-lookup"><span data-stu-id="d7244-279">Gold</span></span> |<span data-ttu-id="d7244-280">[1,2]</span><span class="sxs-lookup"><span data-stu-id="d7244-280">[1,2]</span></span> |

<span data-ttu-id="d7244-281">Le pilote génère plusieurs tables virtuelles pour représenter cette table.</span><span class="sxs-lookup"><span data-stu-id="d7244-281">The driver would generate multiple virtual tables to represent this single table.</span></span> <span data-ttu-id="d7244-282">La première table virtuelle est la table de base ci-dessous nommée « ExampleTable ».</span><span class="sxs-lookup"><span data-stu-id="d7244-282">The first virtual table is the base table named “ExampleTable”, shown below.</span></span> <span data-ttu-id="d7244-283">La table de base contient toutes les données de la table d’origine, mais les données dans les tableaux ont été omises et sont développées dans les tables virtuelles.</span><span class="sxs-lookup"><span data-stu-id="d7244-283">The base table contains all the data of the original table, but the data from the arrays has been omitted and is expanded in the virtual tables.</span></span>

| <span data-ttu-id="d7244-284">_id</span><span class="sxs-lookup"><span data-stu-id="d7244-284">_id</span></span> | <span data-ttu-id="d7244-285">Nom du client</span><span class="sxs-lookup"><span data-stu-id="d7244-285">Customer Name</span></span> | <span data-ttu-id="d7244-286">Niveau de service</span><span class="sxs-lookup"><span data-stu-id="d7244-286">Service Level</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d7244-287">1111</span><span class="sxs-lookup"><span data-stu-id="d7244-287">1111</span></span> |<span data-ttu-id="d7244-288">ABC</span><span class="sxs-lookup"><span data-stu-id="d7244-288">ABC</span></span> |<span data-ttu-id="d7244-289">Silver</span><span class="sxs-lookup"><span data-stu-id="d7244-289">Silver</span></span> |
| <span data-ttu-id="d7244-290">2222</span><span class="sxs-lookup"><span data-stu-id="d7244-290">2222</span></span> |<span data-ttu-id="d7244-291">XYZ</span><span class="sxs-lookup"><span data-stu-id="d7244-291">XYZ</span></span> |<span data-ttu-id="d7244-292">Gold</span><span class="sxs-lookup"><span data-stu-id="d7244-292">Gold</span></span> |

<span data-ttu-id="d7244-293">Les tables suivantes montrent les tables virtuelles qui représentent les tableaux d’origine dans l’exemple.</span><span class="sxs-lookup"><span data-stu-id="d7244-293">The following tables show the virtual tables that represent the original arrays in the example.</span></span> <span data-ttu-id="d7244-294">Ces tables contiennent les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d7244-294">These tables contain the following:</span></span>

* <span data-ttu-id="d7244-295">Une référence à la colonne de clé primaire d’origine correspondant à la ligne du tableau d’origine (via la colonne _id)</span><span class="sxs-lookup"><span data-stu-id="d7244-295">A reference back to the original primary key column corresponding to the row of the original array (via the _id column)</span></span>
* <span data-ttu-id="d7244-296">Une indication de la position des données dans le tableau d’origine</span><span class="sxs-lookup"><span data-stu-id="d7244-296">An indication of the position of the data within the original array</span></span>
* <span data-ttu-id="d7244-297">Les données développées pour chaque élément du tableau</span><span class="sxs-lookup"><span data-stu-id="d7244-297">The expanded data for each element within the array</span></span>

<span data-ttu-id="d7244-298">Table « ExampleTable_Invoices » :</span><span class="sxs-lookup"><span data-stu-id="d7244-298">Table “ExampleTable_Invoices”:</span></span>

| <span data-ttu-id="d7244-299">_id</span><span class="sxs-lookup"><span data-stu-id="d7244-299">_id</span></span> | <span data-ttu-id="d7244-300">ExampleTable_Invoices_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="d7244-300">ExampleTable_Invoices_dim1_idx</span></span> | <span data-ttu-id="d7244-301">invoice_id</span><span class="sxs-lookup"><span data-stu-id="d7244-301">invoice_id</span></span> | <span data-ttu-id="d7244-302">item</span><span class="sxs-lookup"><span data-stu-id="d7244-302">item</span></span> | <span data-ttu-id="d7244-303">price</span><span class="sxs-lookup"><span data-stu-id="d7244-303">price</span></span> | <span data-ttu-id="d7244-304">Remise</span><span class="sxs-lookup"><span data-stu-id="d7244-304">Discount</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="d7244-305">1111</span><span class="sxs-lookup"><span data-stu-id="d7244-305">1111</span></span> |<span data-ttu-id="d7244-306">0</span><span class="sxs-lookup"><span data-stu-id="d7244-306">0</span></span> |<span data-ttu-id="d7244-307">123</span><span class="sxs-lookup"><span data-stu-id="d7244-307">123</span></span> |<span data-ttu-id="d7244-308">grille-pain</span><span class="sxs-lookup"><span data-stu-id="d7244-308">toaster</span></span> |<span data-ttu-id="d7244-309">456</span><span class="sxs-lookup"><span data-stu-id="d7244-309">456</span></span> |<span data-ttu-id="d7244-310">0.2</span><span class="sxs-lookup"><span data-stu-id="d7244-310">0.2</span></span> |
| <span data-ttu-id="d7244-311">1111</span><span class="sxs-lookup"><span data-stu-id="d7244-311">1111</span></span> |<span data-ttu-id="d7244-312">1</span><span class="sxs-lookup"><span data-stu-id="d7244-312">1</span></span> |<span data-ttu-id="d7244-313">124</span><span class="sxs-lookup"><span data-stu-id="d7244-313">124</span></span> |<span data-ttu-id="d7244-314">four</span><span class="sxs-lookup"><span data-stu-id="d7244-314">oven</span></span> |<span data-ttu-id="d7244-315">1235</span><span class="sxs-lookup"><span data-stu-id="d7244-315">1235</span></span> |<span data-ttu-id="d7244-316">0.2</span><span class="sxs-lookup"><span data-stu-id="d7244-316">0.2</span></span> |
| <span data-ttu-id="d7244-317">2222</span><span class="sxs-lookup"><span data-stu-id="d7244-317">2222</span></span> |<span data-ttu-id="d7244-318">0</span><span class="sxs-lookup"><span data-stu-id="d7244-318">0</span></span> |<span data-ttu-id="d7244-319">135</span><span class="sxs-lookup"><span data-stu-id="d7244-319">135</span></span> |<span data-ttu-id="d7244-320">réfrigérateur</span><span class="sxs-lookup"><span data-stu-id="d7244-320">fridge</span></span> |<span data-ttu-id="d7244-321">12543</span><span class="sxs-lookup"><span data-stu-id="d7244-321">12543</span></span> |<span data-ttu-id="d7244-322">0.0</span><span class="sxs-lookup"><span data-stu-id="d7244-322">0.0</span></span> |

<span data-ttu-id="d7244-323">Table « ExampleTable_Ratings » :</span><span class="sxs-lookup"><span data-stu-id="d7244-323">Table “ExampleTable_Ratings”:</span></span>

| <span data-ttu-id="d7244-324">_id</span><span class="sxs-lookup"><span data-stu-id="d7244-324">_id</span></span> | <span data-ttu-id="d7244-325">ExampleTable_Ratings_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="d7244-325">ExampleTable_Ratings_dim1_idx</span></span> | <span data-ttu-id="d7244-326">ExampleTable_Ratings</span><span class="sxs-lookup"><span data-stu-id="d7244-326">ExampleTable_Ratings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d7244-327">1111</span><span class="sxs-lookup"><span data-stu-id="d7244-327">1111</span></span> |<span data-ttu-id="d7244-328">0</span><span class="sxs-lookup"><span data-stu-id="d7244-328">0</span></span> |<span data-ttu-id="d7244-329">5</span><span class="sxs-lookup"><span data-stu-id="d7244-329">5</span></span> |
| <span data-ttu-id="d7244-330">1111</span><span class="sxs-lookup"><span data-stu-id="d7244-330">1111</span></span> |<span data-ttu-id="d7244-331">1</span><span class="sxs-lookup"><span data-stu-id="d7244-331">1</span></span> |<span data-ttu-id="d7244-332">6</span><span class="sxs-lookup"><span data-stu-id="d7244-332">6</span></span> |
| <span data-ttu-id="d7244-333">2222</span><span class="sxs-lookup"><span data-stu-id="d7244-333">2222</span></span> |<span data-ttu-id="d7244-334">0</span><span class="sxs-lookup"><span data-stu-id="d7244-334">0</span></span> |<span data-ttu-id="d7244-335">1</span><span class="sxs-lookup"><span data-stu-id="d7244-335">1</span></span> |
| <span data-ttu-id="d7244-336">2222</span><span class="sxs-lookup"><span data-stu-id="d7244-336">2222</span></span> |<span data-ttu-id="d7244-337">1</span><span class="sxs-lookup"><span data-stu-id="d7244-337">1</span></span> |<span data-ttu-id="d7244-338">2</span><span class="sxs-lookup"><span data-stu-id="d7244-338">2</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="d7244-339">Mapper les colonnes source aux colonnes du récepteur</span><span class="sxs-lookup"><span data-stu-id="d7244-339">Map source to sink columns</span></span>
<span data-ttu-id="d7244-340">Pour en savoir plus sur le mappage de colonnes du jeu de données source à des colonnes du jeu de données récepteur, voir [Mappage des colonnes d’un jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="d7244-340">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="d7244-341">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="d7244-341">Repeatable read from relational sources</span></span>
<span data-ttu-id="d7244-342">Lorsque vous copiez des données à partir de magasins de données relationnels, gardez à l’esprit la répétabilité de l’opération, afin d’éviter des résultats imprévus.</span><span class="sxs-lookup"><span data-stu-id="d7244-342">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="d7244-343">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="d7244-343">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="d7244-344">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="d7244-344">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="d7244-345">Lorsqu’une tranche est réexécutée d’une manière ou d’une autre, vous devez vous assurer que les mêmes données sont lues et ce, quel que soit le nombre d’exécutions de la tranche.</span><span class="sxs-lookup"><span data-stu-id="d7244-345">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="d7244-346">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="d7244-346">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="d7244-347">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="d7244-347">Performance and Tuning</span></span>
<span data-ttu-id="d7244-348">Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="d7244-348">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7244-349">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d7244-349">Next Steps</span></span>
<span data-ttu-id="d7244-350">Consultez l’article [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) pour obtenir des instructions détaillées sur la création d’un pipeline de données qui déplace les données à partir d’un magasin de données local vers un magasin de données Azure.</span><span class="sxs-lookup"><span data-stu-id="d7244-350">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions for creating a data pipeline that moves data from an on-premises data store to an Azure data store.</span></span>
