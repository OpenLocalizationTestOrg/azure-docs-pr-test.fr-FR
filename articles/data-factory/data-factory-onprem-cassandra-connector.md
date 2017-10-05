---
title: "Déplacer des données depuis Cassandra à l’aide de Data Factory | Microsoft Docs"
description: "Découvrez comment déplacer des données depuis une base de données Cassandra locale à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: f2b225bdbdf2880d26a6ab5f992301bf0a804b0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a><span data-ttu-id="d9cba-103">Déplacer des données depuis une base de données Cassandra locale à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d9cba-103">Move data from an on-premises Cassandra database using Azure Data Factory</span></span>
<span data-ttu-id="d9cba-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory, afin de déplacer des données à partir d’une base de données Cassandra locale.</span><span class="sxs-lookup"><span data-stu-id="d9cba-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Cassandra database.</span></span> <span data-ttu-id="d9cba-105">Il s’appuie sur l’article [Activités de déplacement des données](data-factory-data-movement-activities.md), qui présente une vue d’ensemble du déplacement de données avec l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="d9cba-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="d9cba-106">Vous pouvez copier et coller les données d’un magasin de données Cassandra local vers tout magasin de données récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="d9cba-106">You can copy data from an on-premises Cassandra data store to any supported sink data store.</span></span> <span data-ttu-id="d9cba-107">Consultez la table [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) pour obtenir la liste des magasins de données pris en charge en tant que récepteurs par l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="d9cba-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="d9cba-108">Actuellement, Data Factory prend uniquement en charge le déplacement de données d’un magasin de données Cassandra vers d’autres magasins de données, mais non l’inverse.</span><span class="sxs-lookup"><span data-stu-id="d9cba-108">Data factory currently supports only moving data from a Cassandra data store to other data stores, but not for moving data from other data stores to a Cassandra data store.</span></span> 

## <a name="supported-versions"></a><span data-ttu-id="d9cba-109">Versions prises en charge</span><span class="sxs-lookup"><span data-stu-id="d9cba-109">Supported versions</span></span>
<span data-ttu-id="d9cba-110">Le connecteur Cassandra prend en charge les versions suivantes de Cassandra : 2.x.</span><span class="sxs-lookup"><span data-stu-id="d9cba-110">The Cassandra connector supports the following versions of Cassandra: 2.X.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9cba-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d9cba-111">Prerequisites</span></span>
<span data-ttu-id="d9cba-112">Pour que le service Azure Data Factory puisse se connecter à la base de données Cassandra locale, vous devez installer une passerelle de gestion de données sur l’ordinateur qui héberge la base de données ou sur un autre ordinateur, afin d’éviter toute mise en concurrence avec la base de données pour les ressources.</span><span class="sxs-lookup"><span data-stu-id="d9cba-112">For the Azure Data Factory service to be able to connect to your on-premises Cassandra database, you must install a Data Management Gateway on the same machine that hosts the database or on a separate machine to avoid competing for resources with the database.</span></span> <span data-ttu-id="d9cba-113">La passerelle de gestion de données est un composant qui connecte des sources de données locales à des services cloud de manière gérée et sécurisée.</span><span class="sxs-lookup"><span data-stu-id="d9cba-113">Data Management Gateway is a component that connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="d9cba-114">Consultez l’article [Passerelle de gestion des données](data-factory-data-management-gateway.md) pour obtenir des informations détaillées sur la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="d9cba-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="d9cba-115">Consultez l’article [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) pour obtenir des instructions détaillées sur la configuration de la passerelle, un pipeline de données, pour déplacer des données.</span><span class="sxs-lookup"><span data-stu-id="d9cba-115">See [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

<span data-ttu-id="d9cba-116">Vous devez utiliser la passerelle pour vous connecter à une base de données Cassandra, même si elle est hébergée dans le cloud, par exemple sur une machine virtuelle IaaS Azure.</span><span class="sxs-lookup"><span data-stu-id="d9cba-116">You must use the gateway to connect to a Cassandra database even if the database is hosted in the cloud, for example, on an Azure IaaS VM.</span></span> <span data-ttu-id="d9cba-117">Vous pouvez installer la passerelle sur la même machine virtuelle que le magasin de données ou sur une autre machine virtuelle, tant que la passerelle peut se connecter à la base de données.</span><span class="sxs-lookup"><span data-stu-id="d9cba-117">Y You can have the gateway on the same VM that hosts the database or on a separate VM as long as the gateway can connect to the database.</span></span>  

<span data-ttu-id="d9cba-118">L’installation de la passerelle engendre automatiquement l’installation d’un pilote Microsoft ODBC Cassandra, utilisé pour se connecter à la base de données Cassandra.</span><span class="sxs-lookup"><span data-stu-id="d9cba-118">When you install the gateway, it automatically installs a Microsoft Cassandra ODBC driver used to connect to Cassandra database.</span></span> <span data-ttu-id="d9cba-119">Par conséquent, vous n’avez pas besoin d’installer manuellement un pilote sur l’ordinateur de passerelle lors de la copie des données à partir de la base de données Cassandra.</span><span class="sxs-lookup"><span data-stu-id="d9cba-119">Therefore, you don't need to manually install any driver on the gateway machine when copying data from the Cassandra database.</span></span> 

> [!NOTE]
> <span data-ttu-id="d9cba-120">Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.</span><span class="sxs-lookup"><span data-stu-id="d9cba-120">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d9cba-121">Prise en main</span><span class="sxs-lookup"><span data-stu-id="d9cba-121">Getting started</span></span>
<span data-ttu-id="d9cba-122">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données Cassandra local à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="d9cba-122">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="d9cba-123">Le moyen le plus simple de créer un pipeline consiste à utiliser **l’Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="d9cba-123">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="d9cba-124">Consultez la page [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant Copier des données.</span><span class="sxs-lookup"><span data-stu-id="d9cba-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="d9cba-125">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="d9cba-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d9cba-126">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="d9cba-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="d9cba-127">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="d9cba-127">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="d9cba-128">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="d9cba-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="d9cba-129">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="d9cba-129">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="d9cba-130">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="d9cba-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="d9cba-131">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="d9cba-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="d9cba-132">Lorsque vous utilisez des outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory au format JSON.</span><span class="sxs-lookup"><span data-stu-id="d9cba-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="d9cba-133">Pour consulter un exemple contenant des définitions JSON pour les entités Data Factory utilisées pour copier des données d’un magasin de données Cassandra local, consultez la section [Exemple JSON : copier des données depuis un système Cassandra vers Azure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) de cet article.</span><span class="sxs-lookup"><span data-stu-id="d9cba-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Cassandra data store, see [JSON example: Copy data from Cassandra to Azure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="d9cba-134">Les sections suivantes contiennent des informations détaillées sur les propriétés JSON utilisées pour définir les entités Data Factory propres à un magasin de données Cassandra :</span><span class="sxs-lookup"><span data-stu-id="d9cba-134">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Cassandra data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d9cba-135">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="d9cba-135">Linked service properties</span></span>
<span data-ttu-id="d9cba-136">Le tableau suivant fournit la description des éléments JSON spécifiques au service lié Cassandra.</span><span class="sxs-lookup"><span data-stu-id="d9cba-136">The following table provides description for JSON elements specific to Cassandra linked service.</span></span>

| <span data-ttu-id="d9cba-137">Propriété</span><span class="sxs-lookup"><span data-stu-id="d9cba-137">Property</span></span> | <span data-ttu-id="d9cba-138">Description</span><span class="sxs-lookup"><span data-stu-id="d9cba-138">Description</span></span> | <span data-ttu-id="d9cba-139">Requis</span><span class="sxs-lookup"><span data-stu-id="d9cba-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d9cba-140">type</span><span class="sxs-lookup"><span data-stu-id="d9cba-140">type</span></span> |<span data-ttu-id="d9cba-141">Le type de propriété doit être défini sur : **OnPremisesCassandra**</span><span class="sxs-lookup"><span data-stu-id="d9cba-141">The type property must be set to: **OnPremisesCassandra**</span></span> |<span data-ttu-id="d9cba-142">Oui</span><span class="sxs-lookup"><span data-stu-id="d9cba-142">Yes</span></span> |
| <span data-ttu-id="d9cba-143">host</span><span class="sxs-lookup"><span data-stu-id="d9cba-143">host</span></span> |<span data-ttu-id="d9cba-144">Une ou plusieurs adresses IP ou noms d’hôte de serveurs Cassandra.</span><span class="sxs-lookup"><span data-stu-id="d9cba-144">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="d9cba-145">Renseignez une liste des adresses IP ou des noms d’hôte séparée par des virgules pour vous connecter simultanément à tous les serveurs.</span><span class="sxs-lookup"><span data-stu-id="d9cba-145">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span></span> |<span data-ttu-id="d9cba-146">Oui</span><span class="sxs-lookup"><span data-stu-id="d9cba-146">Yes</span></span> |
| <span data-ttu-id="d9cba-147">port</span><span class="sxs-lookup"><span data-stu-id="d9cba-147">port</span></span> |<span data-ttu-id="d9cba-148">Le port TCP utilisé par le serveur Cassandra pour écouter les connexions clientes.</span><span class="sxs-lookup"><span data-stu-id="d9cba-148">The TCP port that the Cassandra server uses to listen for client connections.</span></span> |<span data-ttu-id="d9cba-149">Non, valeur par défaut : 9042</span><span class="sxs-lookup"><span data-stu-id="d9cba-149">No, default value: 9042</span></span> |
| <span data-ttu-id="d9cba-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="d9cba-150">authenticationType</span></span> |<span data-ttu-id="d9cba-151">Basique ou anonyme</span><span class="sxs-lookup"><span data-stu-id="d9cba-151">Basic, or Anonymous</span></span> |<span data-ttu-id="d9cba-152">Oui</span><span class="sxs-lookup"><span data-stu-id="d9cba-152">Yes</span></span> |
| <span data-ttu-id="d9cba-153">username</span><span class="sxs-lookup"><span data-stu-id="d9cba-153">username</span></span> |<span data-ttu-id="d9cba-154">Spécifiez le nom d’utilisateur du compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d9cba-154">Specify user name for the user account.</span></span> |<span data-ttu-id="d9cba-155">Oui, si authenticationType est défini sur De base.</span><span class="sxs-lookup"><span data-stu-id="d9cba-155">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="d9cba-156">password</span><span class="sxs-lookup"><span data-stu-id="d9cba-156">password</span></span> |<span data-ttu-id="d9cba-157">Spécifiez le mot de passe du compte d'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d9cba-157">Specify password for the user account.</span></span> |<span data-ttu-id="d9cba-158">Oui, si authenticationType est défini sur De base.</span><span class="sxs-lookup"><span data-stu-id="d9cba-158">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="d9cba-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d9cba-159">gatewayName</span></span> |<span data-ttu-id="d9cba-160">Le nom de la passerelle qui est utilisée pour se connecter à la base de données Cassandra locale.</span><span class="sxs-lookup"><span data-stu-id="d9cba-160">The name of the gateway that is used to connect to the on-premises Cassandra database.</span></span> |<span data-ttu-id="d9cba-161">Oui</span><span class="sxs-lookup"><span data-stu-id="d9cba-161">Yes</span></span> |
| <span data-ttu-id="d9cba-162">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="d9cba-162">encryptedCredential</span></span> |<span data-ttu-id="d9cba-163">Informations d’identification chiffrées par la passerelle.</span><span class="sxs-lookup"><span data-stu-id="d9cba-163">Credential encrypted by the gateway.</span></span> |<span data-ttu-id="d9cba-164">Non</span><span class="sxs-lookup"><span data-stu-id="d9cba-164">No</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="d9cba-165">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="d9cba-165">Dataset properties</span></span>
<span data-ttu-id="d9cba-166">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="d9cba-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="d9cba-167">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="d9cba-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="d9cba-168">La section **typeProperties** est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="d9cba-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="d9cba-169">La section typeProperties pour le jeu de données de type **CassandraTable** a les propriétés suivantes</span><span class="sxs-lookup"><span data-stu-id="d9cba-169">The typeProperties section for dataset of type **CassandraTable** has the following properties</span></span>

| <span data-ttu-id="d9cba-170">Propriété</span><span class="sxs-lookup"><span data-stu-id="d9cba-170">Property</span></span> | <span data-ttu-id="d9cba-171">Description</span><span class="sxs-lookup"><span data-stu-id="d9cba-171">Description</span></span> | <span data-ttu-id="d9cba-172">Requis</span><span class="sxs-lookup"><span data-stu-id="d9cba-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d9cba-173">espace de clé</span><span class="sxs-lookup"><span data-stu-id="d9cba-173">keyspace</span></span> |<span data-ttu-id="d9cba-174">Nom de l’espace de clé ou du schéma dans la base de données Cassandra.</span><span class="sxs-lookup"><span data-stu-id="d9cba-174">Name of the keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="d9cba-175">Oui (si la **requête** pour **CassandraSource** n’est pas définie).</span><span class="sxs-lookup"><span data-stu-id="d9cba-175">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="d9cba-176">TableName</span><span class="sxs-lookup"><span data-stu-id="d9cba-176">tableName</span></span> |<span data-ttu-id="d9cba-177">Nom de la table dans la base de données Cassandra.</span><span class="sxs-lookup"><span data-stu-id="d9cba-177">Name of the table in Cassandra database.</span></span> |<span data-ttu-id="d9cba-178">Oui (si la **requête** pour **CassandraSource** n’est pas définie).</span><span class="sxs-lookup"><span data-stu-id="d9cba-178">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="d9cba-179">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="d9cba-179">Copy activity properties</span></span>
<span data-ttu-id="d9cba-180">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="d9cba-180">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="d9cba-181">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="d9cba-181">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="d9cba-182">En revanche, les propriétés disponibles dans la section typeProperties de l’activité varient pour chaque type d'activité.</span><span class="sxs-lookup"><span data-stu-id="d9cba-182">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="d9cba-183">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="d9cba-183">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="d9cba-184">Lorsque la source est de type **CassandraSource**, les propriétés suivantes sont disponibles dans la section typeProperties :</span><span class="sxs-lookup"><span data-stu-id="d9cba-184">When source is of type **CassandraSource**, the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="d9cba-185">Propriété</span><span class="sxs-lookup"><span data-stu-id="d9cba-185">Property</span></span> | <span data-ttu-id="d9cba-186">Description</span><span class="sxs-lookup"><span data-stu-id="d9cba-186">Description</span></span> | <span data-ttu-id="d9cba-187">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="d9cba-187">Allowed values</span></span> | <span data-ttu-id="d9cba-188">Requis</span><span class="sxs-lookup"><span data-stu-id="d9cba-188">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d9cba-189">query</span><span class="sxs-lookup"><span data-stu-id="d9cba-189">query</span></span> |<span data-ttu-id="d9cba-190">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="d9cba-190">Use the custom query to read data.</span></span> |<span data-ttu-id="d9cba-191">Requête SQL-92 ou requête CQL.</span><span class="sxs-lookup"><span data-stu-id="d9cba-191">SQL-92 query or CQL query.</span></span> <span data-ttu-id="d9cba-192">Reportez-vous à [référence CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="d9cba-192">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="d9cba-193">Lorsque vous utilisez la requête SQL, indiquez **keyspace name.table name** pour représenter la table que vous souhaitez interroger.</span><span class="sxs-lookup"><span data-stu-id="d9cba-193">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span></span> |<span data-ttu-id="d9cba-194">Non (si tableName et keyspace sur le jeu de données sont définis).</span><span class="sxs-lookup"><span data-stu-id="d9cba-194">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="d9cba-195">Niveau de cohérence</span><span class="sxs-lookup"><span data-stu-id="d9cba-195">consistencyLevel</span></span> |<span data-ttu-id="d9cba-196">Le niveau de cohérence spécifie le nombre de réplicas devant répondre à une demande de lecture avant de renvoyer des données à l’application cliente.</span><span class="sxs-lookup"><span data-stu-id="d9cba-196">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span></span> <span data-ttu-id="d9cba-197">Cassandra vérifie le nombre de réplicas spécifié pour permettre aux données de répondre à la demande de lecture.</span><span class="sxs-lookup"><span data-stu-id="d9cba-197">Cassandra checks the specified number of replicas for data to satisfy the read request.</span></span> |<span data-ttu-id="d9cba-198">UN, DEUX, TROIS, QUORUM, TOUT, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="d9cba-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="d9cba-199">Reportez-vous à [Configuring data consistency (Configuration de la cohérence des données)](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="d9cba-199">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="d9cba-200">Non.</span><span class="sxs-lookup"><span data-stu-id="d9cba-200">No.</span></span> <span data-ttu-id="d9cba-201">La valeur par défaut est UN.</span><span class="sxs-lookup"><span data-stu-id="d9cba-201">Default value is ONE.</span></span> |

## <a name="json-example-copy-data-from-cassandra-to-azure-blob"></a><span data-ttu-id="d9cba-202">Exemple JSON : copier des données depuis un système Cassandra vers Azure Blob</span><span class="sxs-lookup"><span data-stu-id="d9cba-202">JSON example: Copy data from Cassandra to Azure Blob</span></span>
<span data-ttu-id="d9cba-203">Cet exemple présente des exemples de définition JSON, que vous pouvez utiliser pour créer un pipeline à l’aide du [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), de [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [d’Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d9cba-203">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="d9cba-204">Il indique comment copier des données à partir d’une base de données Cassandra locale vers un système de Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d9cba-204">It shows how to copy data from an on-premises Cassandra database to an Azure Blob Storage.</span></span> <span data-ttu-id="d9cba-205">Toutefois, les données peuvent être copiées vers l’un des récepteurs indiqués [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) , via l’activité de copie d’Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d9cba-205">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9cba-206">Cet exemple fournit des extraits de code JSON.</span><span class="sxs-lookup"><span data-stu-id="d9cba-206">This sample provides JSON snippets.</span></span> <span data-ttu-id="d9cba-207">Il n’inclut pas d’instructions détaillées pour la création de la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="d9cba-207">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="d9cba-208">Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="d9cba-208">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="d9cba-209">L’exemple contient les entités de fabrique de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="d9cba-209">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="d9cba-210">Un service lié de type [OnPremisesCassandra](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d9cba-210">A linked service of type [OnPremisesCassandra](#linked-service-properties).</span></span>
* <span data-ttu-id="d9cba-211">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d9cba-211">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="d9cba-212">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [CassandraTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d9cba-212">An input [dataset](data-factory-create-datasets.md) of type [CassandraTable](#dataset-properties).</span></span>
* <span data-ttu-id="d9cba-213">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d9cba-213">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="d9cba-214">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [CassandraSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d9cba-214">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [CassandraSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="d9cba-215">**Service lié Cassandra :**</span><span class="sxs-lookup"><span data-stu-id="d9cba-215">**Cassandra linked service:**</span></span>

<span data-ttu-id="d9cba-216">Cet exemple utilise le service lié **Cassandra** .</span><span class="sxs-lookup"><span data-stu-id="d9cba-216">This example uses the **Cassandra** linked service.</span></span> <span data-ttu-id="d9cba-217">Consultez la section [Service lié Cassandra](#linked-service-properties) pour visualiser les propriétés prises en charge par ce service lié.</span><span class="sxs-lookup"><span data-stu-id="d9cba-217">See [Cassandra linked service](#linked-service-properties) section for the properties supported by this linked service.</span></span>  

```json
{
    "name": "CassandraLinkedService",
    "properties":
    {
        "type": "OnPremisesCassandra",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "host": "mycassandraserver",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="d9cba-218">**Service lié Azure Storage :**</span><span class="sxs-lookup"><span data-stu-id="d9cba-218">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="d9cba-219">**Jeu de données d’entrée Cassandra :**</span><span class="sxs-lookup"><span data-stu-id="d9cba-219">**Cassandra input dataset:**</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "mykeyspace"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

<span data-ttu-id="d9cba-220">La définition de **external** sur **true** informe le service Data Factory qu’il s’agit d’un jeu de données qui est externe à la Data Factory et non produit par une activité dans la Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d9cba-220">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="d9cba-221">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="d9cba-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="d9cba-222">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="d9cba-222">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/fromcassandra"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="d9cba-223">**Activité de copie dans un pipeline avec une source Cassandra et un récepteur blob :**</span><span class="sxs-lookup"><span data-stu-id="d9cba-223">**Copy activity in a pipeline with Cassandra source and Blob sink:**</span></span>

<span data-ttu-id="d9cba-224">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="d9cba-224">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="d9cba-225">Dans la définition du pipeline JSON, le type **source** est défini sur **CassandraSource** et le type **sink** est défini sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d9cba-225">In the pipeline JSON definition, the **source** type is set to **CassandraSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="d9cba-226">Pour obtenir la liste des propriétés prises en charge par RelationalSource, consultez [propriétés du type RelationalSource](#copy-activity-properties) .</span><span class="sxs-lookup"><span data-stu-id="d9cba-226">See [RelationalSource type properties](#copy-activity-properties) for the list of properties supported by the RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra to an Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "CassandraInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"

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

### <a name="type-mapping-for-cassandra"></a><span data-ttu-id="d9cba-227">Mappage de type pour Cassandra</span><span class="sxs-lookup"><span data-stu-id="d9cba-227">Type mapping for Cassandra</span></span>
| <span data-ttu-id="d9cba-228">Type Cassandra</span><span class="sxs-lookup"><span data-stu-id="d9cba-228">Cassandra Type</span></span> | <span data-ttu-id="d9cba-229">Type basé sur .Net</span><span class="sxs-lookup"><span data-stu-id="d9cba-229">.Net Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="d9cba-230">ASCII</span><span class="sxs-lookup"><span data-stu-id="d9cba-230">ASCII</span></span> |<span data-ttu-id="d9cba-231">String</span><span class="sxs-lookup"><span data-stu-id="d9cba-231">String</span></span> |
| <span data-ttu-id="d9cba-232">BIGINT</span><span class="sxs-lookup"><span data-stu-id="d9cba-232">BIGINT</span></span> |<span data-ttu-id="d9cba-233">Int64</span><span class="sxs-lookup"><span data-stu-id="d9cba-233">Int64</span></span> |
| <span data-ttu-id="d9cba-234">BLOB</span><span class="sxs-lookup"><span data-stu-id="d9cba-234">BLOB</span></span> |<span data-ttu-id="d9cba-235">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d9cba-235">Byte[]</span></span> |
| <span data-ttu-id="d9cba-236">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="d9cba-236">BOOLEAN</span></span> |<span data-ttu-id="d9cba-237">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="d9cba-237">Boolean</span></span> |
| <span data-ttu-id="d9cba-238">DÉCIMAL</span><span class="sxs-lookup"><span data-stu-id="d9cba-238">DECIMAL</span></span> |<span data-ttu-id="d9cba-239">DÉCIMAL</span><span class="sxs-lookup"><span data-stu-id="d9cba-239">Decimal</span></span> |
| <span data-ttu-id="d9cba-240">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="d9cba-240">DOUBLE</span></span> |<span data-ttu-id="d9cba-241">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="d9cba-241">Double</span></span> |
| <span data-ttu-id="d9cba-242">FLOAT</span><span class="sxs-lookup"><span data-stu-id="d9cba-242">FLOAT</span></span> |<span data-ttu-id="d9cba-243">Single</span><span class="sxs-lookup"><span data-stu-id="d9cba-243">Single</span></span> |
| <span data-ttu-id="d9cba-244">INET</span><span class="sxs-lookup"><span data-stu-id="d9cba-244">INET</span></span> |<span data-ttu-id="d9cba-245">String</span><span class="sxs-lookup"><span data-stu-id="d9cba-245">String</span></span> |
| <span data-ttu-id="d9cba-246">INT</span><span class="sxs-lookup"><span data-stu-id="d9cba-246">INT</span></span> |<span data-ttu-id="d9cba-247">Int32</span><span class="sxs-lookup"><span data-stu-id="d9cba-247">Int32</span></span> |
| <span data-ttu-id="d9cba-248">TEXTE</span><span class="sxs-lookup"><span data-stu-id="d9cba-248">TEXT</span></span> |<span data-ttu-id="d9cba-249">String</span><span class="sxs-lookup"><span data-stu-id="d9cba-249">String</span></span> |
| <span data-ttu-id="d9cba-250">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="d9cba-250">TIMESTAMP</span></span> |<span data-ttu-id="d9cba-251">DateTime</span><span class="sxs-lookup"><span data-stu-id="d9cba-251">DateTime</span></span> |
| <span data-ttu-id="d9cba-252">TIMEUUID</span><span class="sxs-lookup"><span data-stu-id="d9cba-252">TIMEUUID</span></span> |<span data-ttu-id="d9cba-253">Guid</span><span class="sxs-lookup"><span data-stu-id="d9cba-253">Guid</span></span> |
| <span data-ttu-id="d9cba-254">UUID</span><span class="sxs-lookup"><span data-stu-id="d9cba-254">UUID</span></span> |<span data-ttu-id="d9cba-255">Guid</span><span class="sxs-lookup"><span data-stu-id="d9cba-255">Guid</span></span> |
| <span data-ttu-id="d9cba-256">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="d9cba-256">VARCHAR</span></span> |<span data-ttu-id="d9cba-257">String</span><span class="sxs-lookup"><span data-stu-id="d9cba-257">String</span></span> |
| <span data-ttu-id="d9cba-258">VARINT</span><span class="sxs-lookup"><span data-stu-id="d9cba-258">VARINT</span></span> |<span data-ttu-id="d9cba-259">DÉCIMAL</span><span class="sxs-lookup"><span data-stu-id="d9cba-259">Decimal</span></span> |

> [!NOTE]
> <span data-ttu-id="d9cba-260">Pour les types de collections (mappages, ensembles, listes, etc.), reportez-vous à la section [Work with Cassandra collection types using virtual table (Travailler avec les types de collections Cassandra à l’aide d’une table virtuelle)](#work-with-collections-using-virtual-table) .</span><span class="sxs-lookup"><span data-stu-id="d9cba-260">For collection types (map, set, list, etc.), refer to [Work with Cassandra collection types using virtual table](#work-with-collections-using-virtual-table) section.</span></span>
>
> <span data-ttu-id="d9cba-261">Les types définis par l’utilisateur ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="d9cba-261">User-defined types are not supported.</span></span>
>
> <span data-ttu-id="d9cba-262">La longueur des colonnes binaires et des colonnes de chaîne ne peut pas être supérieure à 4 000.</span><span class="sxs-lookup"><span data-stu-id="d9cba-262">The length of Binary Column and String Column lengths cannot be greater than 4000.</span></span>
>
>

## <a name="work-with-collections-using-virtual-table"></a><span data-ttu-id="d9cba-263">Travailler avec des collections à l’aide d’une table virtuelle</span><span class="sxs-lookup"><span data-stu-id="d9cba-263">Work with collections using virtual table</span></span>
<span data-ttu-id="d9cba-264">Azure Data Factory utilise un pilote ODBC intégré pour assurer la connexion à votre base de données Cassandra et copier des données à partir de cette dernière.</span><span class="sxs-lookup"><span data-stu-id="d9cba-264">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your Cassandra database.</span></span> <span data-ttu-id="d9cba-265">Pour les types de collection, notamment les cartes, ensembles et listes, le pilote renormalise les données dans des tables virtuelles correspondantes.</span><span class="sxs-lookup"><span data-stu-id="d9cba-265">For collection types including map, set and list, the driver renormalizes the data into corresponding virtual tables.</span></span> <span data-ttu-id="d9cba-266">En particulier, si une table contient des colonnes de n’importe quelle collection, le pilote génère les tables virtuelles suivantes :</span><span class="sxs-lookup"><span data-stu-id="d9cba-266">Specifically, if a table contains any collection columns, the driver generates the following virtual tables:</span></span>

* <span data-ttu-id="d9cba-267">Une **table de base**, qui contient les mêmes données que la table réelle, à l’exception des colonnes de collection.</span><span class="sxs-lookup"><span data-stu-id="d9cba-267">A **base table**, which contains the same data as the real table except for the collection columns.</span></span> <span data-ttu-id="d9cba-268">La table de base utilise le même nom que la table réelle qu’elle représente.</span><span class="sxs-lookup"><span data-stu-id="d9cba-268">The base table uses the same name as the real table that it represents.</span></span>
* <span data-ttu-id="d9cba-269">Une **table virtuelle** pour chaque colonne de collection, qui étend les données imbriquées.</span><span class="sxs-lookup"><span data-stu-id="d9cba-269">A **virtual table** for each collection column, which expands the nested data.</span></span> <span data-ttu-id="d9cba-270">Le nom des tables virtuelles qui représentent des collections est composé du nom de la table réelle, du séparateur «*vt*» et du nom de la colonne.</span><span class="sxs-lookup"><span data-stu-id="d9cba-270">The virtual tables that represent collections are named using the name of the real table, a separator “*vt*” and the name of the column.</span></span>

<span data-ttu-id="d9cba-271">Les tables virtuelles font référence aux données présentées dans la table réelle, de manière à permettre au pilote d’accéder aux données dénormalisées.</span><span class="sxs-lookup"><span data-stu-id="d9cba-271">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span></span> <span data-ttu-id="d9cba-272">Consultez la section Exemple pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="d9cba-272">See Example section for details.</span></span> <span data-ttu-id="d9cba-273">Vous pouvez accéder au contenu des collections Cassandra en interrogeant et en joignant les tables virtuelles.</span><span class="sxs-lookup"><span data-stu-id="d9cba-273">You can access the content of Cassandra collections by querying and joining the virtual tables.</span></span>

<span data-ttu-id="d9cba-274">Vous pouvez utiliser l’[Assistant de copie](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) afin d’afficher de manière intuitive la liste des tables dans la base de données Cassandra, y compris les tables virtuelles, et de prévisualiser les données qui s’y trouvent.</span><span class="sxs-lookup"><span data-stu-id="d9cba-274">You can use the [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) to intuitively view the list of tables in Cassandra database including the virtual tables, and preview the data inside.</span></span> <span data-ttu-id="d9cba-275">Vous pouvez également construire une requête dans l’Assistant de copie et valider pour voir le résultat.</span><span class="sxs-lookup"><span data-stu-id="d9cba-275">You can also construct a query in the Copy Wizard and validate to see the result.</span></span>

### <a name="example"></a><span data-ttu-id="d9cba-276">Exemple</span><span class="sxs-lookup"><span data-stu-id="d9cba-276">Example</span></span>
<span data-ttu-id="d9cba-277">Par exemple, « ExampleTable » ci-après est une table de base de données Cassandra qui contient une colonne clé primaire entière nommée « pk_int », une colonne de texte nommée « value », une colonne de liste, une colonne de mappage et une colonne de jeu (nommée « StringSet »).</span><span class="sxs-lookup"><span data-stu-id="d9cba-277">For example, the following “ExampleTable” is a Cassandra database table that contains an integer primary key column named “pk_int”, a text column named value, a list column, a map column, and a set column (named “StringSet”).</span></span>

| <span data-ttu-id="d9cba-278">pk_int</span><span class="sxs-lookup"><span data-stu-id="d9cba-278">pk_int</span></span> | <span data-ttu-id="d9cba-279">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9cba-279">Value</span></span> | <span data-ttu-id="d9cba-280">Énumérer</span><span class="sxs-lookup"><span data-stu-id="d9cba-280">List</span></span> | <span data-ttu-id="d9cba-281">Mappage</span><span class="sxs-lookup"><span data-stu-id="d9cba-281">Map</span></span> | <span data-ttu-id="d9cba-282">StringSet</span><span class="sxs-lookup"><span data-stu-id="d9cba-282">StringSet</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="d9cba-283">1</span><span class="sxs-lookup"><span data-stu-id="d9cba-283">1</span></span> |<span data-ttu-id="d9cba-284">« exemple de valeur 1 »</span><span class="sxs-lookup"><span data-stu-id="d9cba-284">"sample value 1"</span></span> |<span data-ttu-id="d9cba-285">[« 1 », « 2 », « 3 »]</span><span class="sxs-lookup"><span data-stu-id="d9cba-285">["1", "2", "3"]</span></span> |<span data-ttu-id="d9cba-286">{« S1 » : « a », « S2 » : « b »}</span><span class="sxs-lookup"><span data-stu-id="d9cba-286">{"S1": "a", "S2": "b"}</span></span> |<span data-ttu-id="d9cba-287">{« A », « B », « C »}</span><span class="sxs-lookup"><span data-stu-id="d9cba-287">{"A", "B", "C"}</span></span> |
| <span data-ttu-id="d9cba-288">3</span><span class="sxs-lookup"><span data-stu-id="d9cba-288">3</span></span> |<span data-ttu-id="d9cba-289">« exemple de valeur 3 »</span><span class="sxs-lookup"><span data-stu-id="d9cba-289">"sample value 3"</span></span> |<span data-ttu-id="d9cba-290">[« 100 », « 101 », « 102 », « 105 »]</span><span class="sxs-lookup"><span data-stu-id="d9cba-290">["100", "101", "102", "105"]</span></span> |<span data-ttu-id="d9cba-291">{« S1 » : « t »}</span><span class="sxs-lookup"><span data-stu-id="d9cba-291">{"S1": "t"}</span></span> |<span data-ttu-id="d9cba-292">{« A », « E »}</span><span class="sxs-lookup"><span data-stu-id="d9cba-292">{"A", "E"}</span></span> |

<span data-ttu-id="d9cba-293">Le pilote génère plusieurs tables virtuelles pour représenter cette table.</span><span class="sxs-lookup"><span data-stu-id="d9cba-293">The driver would generate multiple virtual tables to represent this single table.</span></span> <span data-ttu-id="d9cba-294">Les colonnes de clés étrangères dans les tables virtuelles font référence aux colonnes de clés primaires dans la table réelle, et indiquent à quelles lignes de la table réelle les lignes de la table virtuelle correspondent.</span><span class="sxs-lookup"><span data-stu-id="d9cba-294">The foreign key columns in the virtual tables reference the primary key columns in the real table, and indicate which real table row the virtual table row corresponds to.</span></span>

<span data-ttu-id="d9cba-295">La première table virtuelle est la table de base nommée « ExampleTable » affichée dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="d9cba-295">The first virtual table is the base table named “ExampleTable” is shown in the following table.</span></span> <span data-ttu-id="d9cba-296">La table de base contient les mêmes données que la table de base de données d’origine, à l’exception des collections, qui sont omises de cette table et développées dans d’autres tables virtuelles.</span><span class="sxs-lookup"><span data-stu-id="d9cba-296">The base table contains the same data as the original database table except for the collections, which are omitted from this table and expanded in other virtual tables.</span></span>

| <span data-ttu-id="d9cba-297">pk_int</span><span class="sxs-lookup"><span data-stu-id="d9cba-297">pk_int</span></span> | <span data-ttu-id="d9cba-298">Valeur</span><span class="sxs-lookup"><span data-stu-id="d9cba-298">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d9cba-299">1</span><span class="sxs-lookup"><span data-stu-id="d9cba-299">1</span></span> |<span data-ttu-id="d9cba-300">« exemple de valeur 1 »</span><span class="sxs-lookup"><span data-stu-id="d9cba-300">"sample value 1"</span></span> |
| <span data-ttu-id="d9cba-301">3</span><span class="sxs-lookup"><span data-stu-id="d9cba-301">3</span></span> |<span data-ttu-id="d9cba-302">« exemple de valeur 3 »</span><span class="sxs-lookup"><span data-stu-id="d9cba-302">"sample value 3"</span></span> |

<span data-ttu-id="d9cba-303">Les tableaux suivants montrent les tables virtuelles qui renormalisent les données des colonnes Liste, Mappage et StringSet.</span><span class="sxs-lookup"><span data-stu-id="d9cba-303">The following tables show the virtual tables that renormalize the data from the List, Map, and StringSet columns.</span></span> <span data-ttu-id="d9cba-304">Les colonnes portant des noms se terminant par « _index » ou « _key » indiquent la position des données dans la liste ou le mappage d’origine.</span><span class="sxs-lookup"><span data-stu-id="d9cba-304">The columns with names that end with “_index” or “_key” indicate the position of the data within the original list or map.</span></span> <span data-ttu-id="d9cba-305">Les colonnes portant des noms se terminant par « _value » contiennent les données étendues de la collection.</span><span class="sxs-lookup"><span data-stu-id="d9cba-305">The columns with names that end with “_value” contain the expanded data from the collection.</span></span>

#### <a name="table-exampletablevtlist"></a><span data-ttu-id="d9cba-306">Table « ExampleTable_vt_List » :</span><span class="sxs-lookup"><span data-stu-id="d9cba-306">Table “ExampleTable_vt_List”:</span></span>
| <span data-ttu-id="d9cba-307">pk_int</span><span class="sxs-lookup"><span data-stu-id="d9cba-307">pk_int</span></span> | <span data-ttu-id="d9cba-308">List_index</span><span class="sxs-lookup"><span data-stu-id="d9cba-308">List_index</span></span> | <span data-ttu-id="d9cba-309">List_value</span><span class="sxs-lookup"><span data-stu-id="d9cba-309">List_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d9cba-310">1</span><span class="sxs-lookup"><span data-stu-id="d9cba-310">1</span></span> |<span data-ttu-id="d9cba-311">0</span><span class="sxs-lookup"><span data-stu-id="d9cba-311">0</span></span> |<span data-ttu-id="d9cba-312">1</span><span class="sxs-lookup"><span data-stu-id="d9cba-312">1</span></span> |
| <span data-ttu-id="d9cba-313">1</span><span class="sxs-lookup"><span data-stu-id="d9cba-313">1</span></span> |<span data-ttu-id="d9cba-314">1</span><span class="sxs-lookup"><span data-stu-id="d9cba-314">1</span></span> |<span data-ttu-id="d9cba-315">2</span><span class="sxs-lookup"><span data-stu-id="d9cba-315">2</span></span> |
| <span data-ttu-id="d9cba-316">1</span><span class="sxs-lookup"><span data-stu-id="d9cba-316">1</span></span> |<span data-ttu-id="d9cba-317">2</span><span class="sxs-lookup"><span data-stu-id="d9cba-317">2</span></span> |<span data-ttu-id="d9cba-318">3</span><span class="sxs-lookup"><span data-stu-id="d9cba-318">3</span></span> |
| <span data-ttu-id="d9cba-319">3</span><span class="sxs-lookup"><span data-stu-id="d9cba-319">3</span></span> |<span data-ttu-id="d9cba-320">0</span><span class="sxs-lookup"><span data-stu-id="d9cba-320">0</span></span> |<span data-ttu-id="d9cba-321">100</span><span class="sxs-lookup"><span data-stu-id="d9cba-321">100</span></span> |
| <span data-ttu-id="d9cba-322">3</span><span class="sxs-lookup"><span data-stu-id="d9cba-322">3</span></span> |<span data-ttu-id="d9cba-323">1</span><span class="sxs-lookup"><span data-stu-id="d9cba-323">1</span></span> |<span data-ttu-id="d9cba-324">101</span><span class="sxs-lookup"><span data-stu-id="d9cba-324">101</span></span> |
| <span data-ttu-id="d9cba-325">3</span><span class="sxs-lookup"><span data-stu-id="d9cba-325">3</span></span> |<span data-ttu-id="d9cba-326">2</span><span class="sxs-lookup"><span data-stu-id="d9cba-326">2</span></span> |<span data-ttu-id="d9cba-327">102</span><span class="sxs-lookup"><span data-stu-id="d9cba-327">102</span></span> |
| <span data-ttu-id="d9cba-328">3</span><span class="sxs-lookup"><span data-stu-id="d9cba-328">3</span></span> |<span data-ttu-id="d9cba-329">3</span><span class="sxs-lookup"><span data-stu-id="d9cba-329">3</span></span> |<span data-ttu-id="d9cba-330">103</span><span class="sxs-lookup"><span data-stu-id="d9cba-330">103</span></span> |

#### <a name="table-exampletablevtmap"></a><span data-ttu-id="d9cba-331">Table « ExampleTable_vt_List » :</span><span class="sxs-lookup"><span data-stu-id="d9cba-331">Table “ExampleTable_vt_Map”:</span></span>
| <span data-ttu-id="d9cba-332">pk_int</span><span class="sxs-lookup"><span data-stu-id="d9cba-332">pk_int</span></span> | <span data-ttu-id="d9cba-333">Map_key</span><span class="sxs-lookup"><span data-stu-id="d9cba-333">Map_key</span></span> | <span data-ttu-id="d9cba-334">Map_value</span><span class="sxs-lookup"><span data-stu-id="d9cba-334">Map_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d9cba-335">1</span><span class="sxs-lookup"><span data-stu-id="d9cba-335">1</span></span> |<span data-ttu-id="d9cba-336">S1</span><span class="sxs-lookup"><span data-stu-id="d9cba-336">S1</span></span> |<span data-ttu-id="d9cba-337">Un </span><span class="sxs-lookup"><span data-stu-id="d9cba-337">A</span></span> |
| <span data-ttu-id="d9cba-338">1</span><span class="sxs-lookup"><span data-stu-id="d9cba-338">1</span></span> |<span data-ttu-id="d9cba-339">S2</span><span class="sxs-lookup"><span data-stu-id="d9cba-339">S2</span></span> |<span data-ttu-id="d9cba-340">b</span><span class="sxs-lookup"><span data-stu-id="d9cba-340">b</span></span> |
| <span data-ttu-id="d9cba-341">3</span><span class="sxs-lookup"><span data-stu-id="d9cba-341">3</span></span> |<span data-ttu-id="d9cba-342">S1</span><span class="sxs-lookup"><span data-stu-id="d9cba-342">S1</span></span> |<span data-ttu-id="d9cba-343">t</span><span class="sxs-lookup"><span data-stu-id="d9cba-343">t</span></span> |

#### <a name="table-exampletablevtstringset"></a><span data-ttu-id="d9cba-344">Table « ExampleTable_vt_List » :</span><span class="sxs-lookup"><span data-stu-id="d9cba-344">Table “ExampleTable_vt_StringSet”:</span></span>
| <span data-ttu-id="d9cba-345">pk_int</span><span class="sxs-lookup"><span data-stu-id="d9cba-345">pk_int</span></span> | <span data-ttu-id="d9cba-346">StringSet_value</span><span class="sxs-lookup"><span data-stu-id="d9cba-346">StringSet_value</span></span> |
| --- | --- |
| <span data-ttu-id="d9cba-347">1</span><span class="sxs-lookup"><span data-stu-id="d9cba-347">1</span></span> |<span data-ttu-id="d9cba-348">Un </span><span class="sxs-lookup"><span data-stu-id="d9cba-348">A</span></span> |
| <span data-ttu-id="d9cba-349">1</span><span class="sxs-lookup"><span data-stu-id="d9cba-349">1</span></span> |<span data-ttu-id="d9cba-350">b</span><span class="sxs-lookup"><span data-stu-id="d9cba-350">B</span></span> |
| <span data-ttu-id="d9cba-351">1</span><span class="sxs-lookup"><span data-stu-id="d9cba-351">1</span></span> |<span data-ttu-id="d9cba-352">C</span><span class="sxs-lookup"><span data-stu-id="d9cba-352">C</span></span> |
| <span data-ttu-id="d9cba-353">3</span><span class="sxs-lookup"><span data-stu-id="d9cba-353">3</span></span> |<span data-ttu-id="d9cba-354">Un </span><span class="sxs-lookup"><span data-stu-id="d9cba-354">A</span></span> |
| <span data-ttu-id="d9cba-355">3</span><span class="sxs-lookup"><span data-stu-id="d9cba-355">3</span></span> |<span data-ttu-id="d9cba-356">E</span><span class="sxs-lookup"><span data-stu-id="d9cba-356">E</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="d9cba-357">Mapper les colonnes source aux colonnes du récepteur</span><span class="sxs-lookup"><span data-stu-id="d9cba-357">Map source to sink columns</span></span>
<span data-ttu-id="d9cba-358">Pour en savoir plus sur le mappage de colonnes du jeu de données source à des colonnes du jeu de données récepteur, voir [Mappage des colonnes d’un jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="d9cba-358">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="d9cba-359">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="d9cba-359">Repeatable read from relational sources</span></span>
<span data-ttu-id="d9cba-360">Lorsque vous copiez des données à partir de magasins de données relationnels, gardez à l’esprit la répétabilité de l’opération, afin d’éviter des résultats imprévus.</span><span class="sxs-lookup"><span data-stu-id="d9cba-360">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="d9cba-361">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="d9cba-361">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="d9cba-362">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="d9cba-362">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="d9cba-363">Lorsqu’une tranche est réexécutée d’une manière ou d’une autre, vous devez vous assurer que les mêmes données sont lues et ce, quel que soit le nombre d’exécutions de la tranche.</span><span class="sxs-lookup"><span data-stu-id="d9cba-363">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="d9cba-364">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="d9cba-364">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="d9cba-365">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="d9cba-365">Performance and Tuning</span></span>
<span data-ttu-id="d9cba-366">Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="d9cba-366">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
