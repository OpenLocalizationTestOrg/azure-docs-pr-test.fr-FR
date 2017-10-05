---
title: "Déplacer des données depuis MySQL à l’aide d’Azure Data Factory | Microsoft Docs"
description: "Découvrez comment déplacer des données depuis une base de données MySQL à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 452f4fce-9eb5-40a0-92f8-1e98691bea4c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: jingwang
ms.openlocfilehash: 05159bfd98977d0b57b43fbc02e4579439f7ce4c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="b5b6e-103">Déplacer des données depuis MySQL à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="b5b6e-103">Move data From MySQL using Azure Data Factory</span></span>
<span data-ttu-id="b5b6e-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour déplacer des données à partir d’une base de données MySQL locale.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MySQL database.</span></span> <span data-ttu-id="b5b6e-105">Il s’appuie sur l’article [Activités de déplacement des données](data-factory-data-movement-activities.md), qui présente une vue d’ensemble du déplacement de données avec l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="b5b6e-106">Vous pouvez copier et coller les données d’un magasin de données MySQL local dans tout magasin de données récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-106">You can copy data from an on-premises MySQL data store to any supported sink data store.</span></span> <span data-ttu-id="b5b6e-107">Consultez la table [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) pour obtenir la liste des magasins de données pris en charge en tant que récepteurs par l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="b5b6e-108">Actuellement, Data Factory prend uniquement en charge le déplacement de données d’un magasin de données MySQL vers d’autres magasins de données, mais non l’inverse.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-108">Data factory currently supports only moving data from a MySQL data store to other data stores, but not for moving data from other data stores to an MySQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b5b6e-109">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="b5b6e-109">Prerequisites</span></span>
<span data-ttu-id="b5b6e-110">Le service Data Factory prend en charge la connexion à des sources MySQL locales à l'aide de la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-110">Data Factory service supports connecting to on-premises MySQL sources using the Data Management Gateway.</span></span> <span data-ttu-id="b5b6e-111">Consultez l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) pour en savoir plus sur la passerelle de gestion des données et obtenir des instructions détaillées sur la configuration de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="b5b6e-112">Une passerelle est requise même si la base de données MySQL est hébergée sur une machine virtuelle Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-112">Gateway is required even if the MySQL database is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="b5b6e-113">Vous pouvez installer la passerelle sur la même machine virtuelle que le magasin de données, ou sur une autre machine virtuelle pourvu que la passerelle puisse se connecter à la base de données.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-113">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="b5b6e-114">Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="b5b6e-115">Versions prises en charge et installation</span><span class="sxs-lookup"><span data-stu-id="b5b6e-115">Supported versions and installation</span></span>
<span data-ttu-id="b5b6e-116">Pour que la passerelle de gestion des données puisse se connecter à la base de données MySQL, vous devez installer le [connecteur MySQL/Net pour Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 ou ultérieure) sur le même système que la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-116">For Data Management Gateway to connect to the MySQL Database, you need to install the [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 or above) on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="b5b6e-117">MySQL version 5.1 et ultérieures est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-117">MySQL version 5.1 and above is supported.</span></span>

> [!TIP]
> <span data-ttu-id="b5b6e-118">Si vous rencontrez l’erreur « Échec de l'authentification, car le site distant a fermé le flux de transport. », envisagez de mettre à niveau le connecteur MySQL/Net vers une version supérieure.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-118">If you hit error on "Authentication failed because the remote party has closed the transport stream.", consider to upgrade the MySQL Connector/Net to higher version.</span></span>

## <a name="getting-started"></a><span data-ttu-id="b5b6e-119">Prise en main</span><span class="sxs-lookup"><span data-stu-id="b5b6e-119">Getting started</span></span>
<span data-ttu-id="b5b6e-120">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données Cassandra local à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-120">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="b5b6e-121">Le moyen le plus simple de créer un pipeline consiste à utiliser **l’Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-121">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="b5b6e-122">Consultez la page [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant Copier des données.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="b5b6e-123">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-123">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="b5b6e-124">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="b5b6e-125">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="b5b6e-125">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="b5b6e-126">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-126">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="b5b6e-127">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-127">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="b5b6e-128">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="b5b6e-129">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-129">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="b5b6e-130">Lorsque vous utilisez des outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory au format JSON.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="b5b6e-131">Pour consulter un exemple contenant des définitions JSON pour les entités Data Factory utilisées pour copier des données d’un magasin de données MySQL local, consultez la section [Exemple JSON : copier des données depuis un système MySQL vers Azure Blob](#json-example-copy-data-from-mysql-to-azure-blob) de cet article.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-131">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL to Azure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="b5b6e-132">Les sections suivantes contiennent des informations détaillées sur les propriétés JSON utilisées pour définir les entités Data Factory propres à un magasin de données MySQL :</span><span class="sxs-lookup"><span data-stu-id="b5b6e-132">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a MySQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="b5b6e-133">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="b5b6e-133">Linked service properties</span></span>
<span data-ttu-id="b5b6e-134">Le tableau suivant fournit la description des éléments JSON spécifiques au service lié MySQL.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-134">The following table provides description for JSON elements specific to MySQL linked service.</span></span>

| <span data-ttu-id="b5b6e-135">Propriété</span><span class="sxs-lookup"><span data-stu-id="b5b6e-135">Property</span></span> | <span data-ttu-id="b5b6e-136">Description</span><span class="sxs-lookup"><span data-stu-id="b5b6e-136">Description</span></span> | <span data-ttu-id="b5b6e-137">Requis</span><span class="sxs-lookup"><span data-stu-id="b5b6e-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b5b6e-138">type</span><span class="sxs-lookup"><span data-stu-id="b5b6e-138">type</span></span> |<span data-ttu-id="b5b6e-139">Le type de propriété doit être défini sur : **OnPremisesMySql**</span><span class="sxs-lookup"><span data-stu-id="b5b6e-139">The type property must be set to: **OnPremisesMySql**</span></span> |<span data-ttu-id="b5b6e-140">Oui</span><span class="sxs-lookup"><span data-stu-id="b5b6e-140">Yes</span></span> |
| <span data-ttu-id="b5b6e-141">server</span><span class="sxs-lookup"><span data-stu-id="b5b6e-141">server</span></span> |<span data-ttu-id="b5b6e-142">Nom du serveur MySQL.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-142">Name of the MySQL server.</span></span> |<span data-ttu-id="b5b6e-143">Oui</span><span class="sxs-lookup"><span data-stu-id="b5b6e-143">Yes</span></span> |
| <span data-ttu-id="b5b6e-144">database</span><span class="sxs-lookup"><span data-stu-id="b5b6e-144">database</span></span> |<span data-ttu-id="b5b6e-145">Nom de la base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-145">Name of the MySQL database.</span></span> |<span data-ttu-id="b5b6e-146">Oui</span><span class="sxs-lookup"><span data-stu-id="b5b6e-146">Yes</span></span> |
| <span data-ttu-id="b5b6e-147">schema</span><span class="sxs-lookup"><span data-stu-id="b5b6e-147">schema</span></span> |<span data-ttu-id="b5b6e-148">Nom du schéma dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-148">Name of the schema in the database.</span></span> |<span data-ttu-id="b5b6e-149">Non</span><span class="sxs-lookup"><span data-stu-id="b5b6e-149">No</span></span> |
| <span data-ttu-id="b5b6e-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="b5b6e-150">authenticationType</span></span> |<span data-ttu-id="b5b6e-151">Type d'authentification utilisé pour se connecter à la base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-151">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="b5b6e-152">Les valeurs possibles sont les suivantes : `Basic`.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-152">Possible values are: `Basic`.</span></span> |<span data-ttu-id="b5b6e-153">Oui</span><span class="sxs-lookup"><span data-stu-id="b5b6e-153">Yes</span></span> |
| <span data-ttu-id="b5b6e-154">username</span><span class="sxs-lookup"><span data-stu-id="b5b6e-154">username</span></span> |<span data-ttu-id="b5b6e-155">Spécifiez le nom d’utilisateur associé à la connexion à la base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-155">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="b5b6e-156">Oui</span><span class="sxs-lookup"><span data-stu-id="b5b6e-156">Yes</span></span> |
| <span data-ttu-id="b5b6e-157">password</span><span class="sxs-lookup"><span data-stu-id="b5b6e-157">password</span></span> |<span data-ttu-id="b5b6e-158">Spécifiez le mot de passe du compte d’utilisateur que vous avez indiqué.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-158">Specify password for the user account you specified.</span></span> |<span data-ttu-id="b5b6e-159">Oui</span><span class="sxs-lookup"><span data-stu-id="b5b6e-159">Yes</span></span> |
| <span data-ttu-id="b5b6e-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="b5b6e-160">gatewayName</span></span> |<span data-ttu-id="b5b6e-161">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter à la base de données MySQL locale.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-161">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="b5b6e-162">Oui</span><span class="sxs-lookup"><span data-stu-id="b5b6e-162">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="b5b6e-163">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="b5b6e-163">Dataset properties</span></span>
<span data-ttu-id="b5b6e-164">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="b5b6e-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="b5b6e-165">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="b5b6e-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="b5b6e-166">La section **typeProperties** est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-166">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="b5b6e-167">La section typeProperties pour le jeu de données de type **RelationalTable** (qui inclut le jeu de données MySQL) a les propriétés suivantes.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-167">The typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has the following properties</span></span>

| <span data-ttu-id="b5b6e-168">Propriété</span><span class="sxs-lookup"><span data-stu-id="b5b6e-168">Property</span></span> | <span data-ttu-id="b5b6e-169">Description</span><span class="sxs-lookup"><span data-stu-id="b5b6e-169">Description</span></span> | <span data-ttu-id="b5b6e-170">Requis</span><span class="sxs-lookup"><span data-stu-id="b5b6e-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b5b6e-171">TableName</span><span class="sxs-lookup"><span data-stu-id="b5b6e-171">tableName</span></span> |<span data-ttu-id="b5b6e-172">Nom de la table dans l'instance de base de données MySQL à laquelle le service lié fait référence.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-172">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="b5b6e-173">Non (si la **requête** de **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="b5b6e-173">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="b5b6e-174">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="b5b6e-174">Copy activity properties</span></span>
<span data-ttu-id="b5b6e-175">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="b5b6e-175">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="b5b6e-176">Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-176">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="b5b6e-177">En revanche, les propriétés disponibles dans la section **typeProperties** de l’activité varient pour chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-177">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="b5b6e-178">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-178">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="b5b6e-179">Lorsque la source de l’activité de copie est de type **RelationalSource** (ce qui inclut MySQL), les propriétés suivantes sont disponibles dans la section typeProperties :</span><span class="sxs-lookup"><span data-stu-id="b5b6e-179">When source in copy activity is of type **RelationalSource** (which includes MySQL), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="b5b6e-180">Propriété</span><span class="sxs-lookup"><span data-stu-id="b5b6e-180">Property</span></span> | <span data-ttu-id="b5b6e-181">Description</span><span class="sxs-lookup"><span data-stu-id="b5b6e-181">Description</span></span> | <span data-ttu-id="b5b6e-182">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="b5b6e-182">Allowed values</span></span> | <span data-ttu-id="b5b6e-183">Requis</span><span class="sxs-lookup"><span data-stu-id="b5b6e-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b5b6e-184">query</span><span class="sxs-lookup"><span data-stu-id="b5b6e-184">query</span></span> |<span data-ttu-id="b5b6e-185">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-185">Use the custom query to read data.</span></span> |<span data-ttu-id="b5b6e-186">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-186">SQL query string.</span></span> <span data-ttu-id="b5b6e-187">Par exemple : select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-187">For example: select * from MyTable.</span></span> |<span data-ttu-id="b5b6e-188">Non (si **tableName** de **dataset** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="b5b6e-188">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-mysql-to-azure-blob"></a><span data-ttu-id="b5b6e-189">Exemple JSON : copier des données depuis un système MySQL vers Azure Blob</span><span class="sxs-lookup"><span data-stu-id="b5b6e-189">JSON example: Copy data from MySQL to Azure Blob</span></span>
<span data-ttu-id="b5b6e-190">Cet exemple présente des exemples de définition JSON, que vous pouvez utiliser pour créer un pipeline à l’aide du [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), de [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [d’Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b5b6e-190">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="b5b6e-191">Il indique comment copier des données à partir d’une base de données MySQL locale vers un système de Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-191">It shows how to copy data from an on-premises MySQL database to an Azure Blob Storage.</span></span> <span data-ttu-id="b5b6e-192">Toutefois, les données peuvent être copiées vers l’un des récepteurs indiqués [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) , via l’activité de copie d’Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-192">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b5b6e-193">Cet exemple fournit des extraits de code JSON.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-193">This sample provides JSON snippets.</span></span> <span data-ttu-id="b5b6e-194">Il n’inclut pas d’instructions détaillées pour la création de la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-194">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="b5b6e-195">Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="b5b6e-195">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="b5b6e-196">L’exemple contient les entités de fabrique de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="b5b6e-196">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="b5b6e-197">Un service lié de type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b5b6e-197">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="b5b6e-198">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b5b6e-198">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="b5b6e-199">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b5b6e-199">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="b5b6e-200">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b5b6e-200">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="b5b6e-201">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="b5b6e-201">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="b5b6e-202">L’exemple copie toutes les heures les données de résultat d’une requête de base de données MySQL dans un objet blob.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-202">The sample copies data from a query result in MySQL database to a blob hourly.</span></span> <span data-ttu-id="b5b6e-203">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-203">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="b5b6e-204">Dans un premier temps, configurez la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-204">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="b5b6e-205">Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="b5b6e-205">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="b5b6e-206">**Service lié MySQL :**</span><span class="sxs-lookup"><span data-stu-id="b5b6e-206">**MySQL linked service:**</span></span>

```JSON
    {
      "name": "OnPremMySqlLinkedService",
      "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
          "server": "<server name>",
          "database": "<database name>",
          "schema": "<schema name>",
          "authenticationType": "<authentication type>",
          "userName": "<user name>",
          "password": "<password>",
          "gatewayName": "<gateway>"
        }
      }
    }
```

<span data-ttu-id="b5b6e-207">**Service lié Azure Storage :**</span><span class="sxs-lookup"><span data-stu-id="b5b6e-207">**Azure Storage linked service:**</span></span>

```JSON
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

<span data-ttu-id="b5b6e-208">**Jeu de données d’entrée MySQL :**</span><span class="sxs-lookup"><span data-stu-id="b5b6e-208">**MySQL input dataset:**</span></span>

<span data-ttu-id="b5b6e-209">L'exemple suppose que vous avez créé une table « MyTable » dans MySQL et qu'elle contient une colonne appelée « timestampcolumn » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-209">The sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="b5b6e-210">La définition de « external » : « true » sur informe le service Data Factory qu’il s’agit d’un jeu de données qui est externe à la Data Factory et non produit par une activité dans la Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-210">Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
    {
        "name": "MySqlDataSet",
        "properties": {
            "published": false,
            "type": "RelationalTable",
            "linkedServiceName": "OnPremMySqlLinkedService",
            "typeProperties": {},
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

<span data-ttu-id="b5b6e-211">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="b5b6e-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="b5b6e-212">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="b5b6e-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="b5b6e-213">Le chemin d’accès du dossier pour l’objet blob est évalué dynamiquement en fonction de l’heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="b5b6e-214">Le chemin d'accès du dossier utilise l'année, le mois, le jour et l'heure de l'heure de début.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
    {
        "name": "AzureBlobMySqlDataSet",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "mycontainer/mysql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="b5b6e-215">**Pipeline avec activité de copie :**</span><span class="sxs-lookup"><span data-stu-id="b5b6e-215">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="b5b6e-216">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-216">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="b5b6e-217">Dans la définition du pipeline JSON, le type **source** est défini sur **RelationalSource** et le type **sink** est défini sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-217">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="b5b6e-218">La requête SQL spécifiée pour la propriété **query** sélectionne les données de la dernière heure à copier.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```JSON
    {
        "name": "CopyMySqlToBlob",
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
                            "name": "MySqlDataSet"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobMySqlDataSet"
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
                    "name": "MySqlToBlob"
                }
            ],
            "start": "2014-06-01T18:00:00Z",
            "end": "2014-06-01T19:00:00Z"
        }
    }
```


### <a name="type-mapping-for-mysql"></a><span data-ttu-id="b5b6e-219">Mappage de type pour MySQL</span><span class="sxs-lookup"><span data-stu-id="b5b6e-219">Type mapping for MySQL</span></span>
<span data-ttu-id="b5b6e-220">Comme mentionné dans l’article consacré aux [activités de déplacement de données](data-factory-data-movement-activities.md) , l’activité de copie convertit automatiquement des types source en types récepteur à l’aide de l’approche en deux étapes suivante :</span><span class="sxs-lookup"><span data-stu-id="b5b6e-220">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="b5b6e-221">Conversion de types natifs source en types .NET</span><span class="sxs-lookup"><span data-stu-id="b5b6e-221">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="b5b6e-222">Conversion de types .NET en types récepteur natifs</span><span class="sxs-lookup"><span data-stu-id="b5b6e-222">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="b5b6e-223">Lors du déplacement de données vers MySQL, les mappages suivants sont utilisés pour passer des types MySQL aux types .NET.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-223">When moving data to MySQL, the following mappings are used from MySQL types to .NET types.</span></span>

| <span data-ttu-id="b5b6e-224">Type de base de données MySQL</span><span class="sxs-lookup"><span data-stu-id="b5b6e-224">MySQL Database type</span></span> | <span data-ttu-id="b5b6e-225">Type de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="b5b6e-225">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="b5b6e-226">bigint non signé</span><span class="sxs-lookup"><span data-stu-id="b5b6e-226">bigint unsigned</span></span> |<span data-ttu-id="b5b6e-227">Décimal</span><span class="sxs-lookup"><span data-stu-id="b5b6e-227">Decimal</span></span> |
| <span data-ttu-id="b5b6e-228">bigint</span><span class="sxs-lookup"><span data-stu-id="b5b6e-228">bigint</span></span> |<span data-ttu-id="b5b6e-229">Int64</span><span class="sxs-lookup"><span data-stu-id="b5b6e-229">Int64</span></span> |
| <span data-ttu-id="b5b6e-230">bit</span><span class="sxs-lookup"><span data-stu-id="b5b6e-230">bit</span></span> |<span data-ttu-id="b5b6e-231">Décimal</span><span class="sxs-lookup"><span data-stu-id="b5b6e-231">Decimal</span></span> |
| <span data-ttu-id="b5b6e-232">objet blob</span><span class="sxs-lookup"><span data-stu-id="b5b6e-232">blob</span></span> |<span data-ttu-id="b5b6e-233">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b5b6e-233">Byte[]</span></span> |
| <span data-ttu-id="b5b6e-234">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="b5b6e-234">bool</span></span> |<span data-ttu-id="b5b6e-235">Boolean</span><span class="sxs-lookup"><span data-stu-id="b5b6e-235">Boolean</span></span> |
| <span data-ttu-id="b5b6e-236">char</span><span class="sxs-lookup"><span data-stu-id="b5b6e-236">char</span></span> |<span data-ttu-id="b5b6e-237">String</span><span class="sxs-lookup"><span data-stu-id="b5b6e-237">String</span></span> |
| <span data-ttu-id="b5b6e-238">date</span><span class="sxs-lookup"><span data-stu-id="b5b6e-238">date</span></span> |<span data-ttu-id="b5b6e-239">Datetime</span><span class="sxs-lookup"><span data-stu-id="b5b6e-239">Datetime</span></span> |
| <span data-ttu-id="b5b6e-240">Datetime</span><span class="sxs-lookup"><span data-stu-id="b5b6e-240">datetime</span></span> |<span data-ttu-id="b5b6e-241">Datetime</span><span class="sxs-lookup"><span data-stu-id="b5b6e-241">Datetime</span></span> |
| <span data-ttu-id="b5b6e-242">Décimal</span><span class="sxs-lookup"><span data-stu-id="b5b6e-242">decimal</span></span> |<span data-ttu-id="b5b6e-243">Décimal</span><span class="sxs-lookup"><span data-stu-id="b5b6e-243">Decimal</span></span> |
| <span data-ttu-id="b5b6e-244">double précision</span><span class="sxs-lookup"><span data-stu-id="b5b6e-244">double precision</span></span> |<span data-ttu-id="b5b6e-245">Double</span><span class="sxs-lookup"><span data-stu-id="b5b6e-245">Double</span></span> |
| <span data-ttu-id="b5b6e-246">Double</span><span class="sxs-lookup"><span data-stu-id="b5b6e-246">double</span></span> |<span data-ttu-id="b5b6e-247">Double</span><span class="sxs-lookup"><span data-stu-id="b5b6e-247">Double</span></span> |
| <span data-ttu-id="b5b6e-248">enum</span><span class="sxs-lookup"><span data-stu-id="b5b6e-248">enum</span></span> |<span data-ttu-id="b5b6e-249">String</span><span class="sxs-lookup"><span data-stu-id="b5b6e-249">String</span></span> |
| <span data-ttu-id="b5b6e-250">float</span><span class="sxs-lookup"><span data-stu-id="b5b6e-250">float</span></span> |<span data-ttu-id="b5b6e-251">Single</span><span class="sxs-lookup"><span data-stu-id="b5b6e-251">Single</span></span> |
| <span data-ttu-id="b5b6e-252">int non signé</span><span class="sxs-lookup"><span data-stu-id="b5b6e-252">int unsigned</span></span> |<span data-ttu-id="b5b6e-253">Int64</span><span class="sxs-lookup"><span data-stu-id="b5b6e-253">Int64</span></span> |
| <span data-ttu-id="b5b6e-254">int</span><span class="sxs-lookup"><span data-stu-id="b5b6e-254">int</span></span> |<span data-ttu-id="b5b6e-255">Int32</span><span class="sxs-lookup"><span data-stu-id="b5b6e-255">Int32</span></span> |
| <span data-ttu-id="b5b6e-256">entier non signé</span><span class="sxs-lookup"><span data-stu-id="b5b6e-256">integer unsigned</span></span> |<span data-ttu-id="b5b6e-257">Int64</span><span class="sxs-lookup"><span data-stu-id="b5b6e-257">Int64</span></span> |
| <span data-ttu-id="b5b6e-258">integer</span><span class="sxs-lookup"><span data-stu-id="b5b6e-258">integer</span></span> |<span data-ttu-id="b5b6e-259">Int32</span><span class="sxs-lookup"><span data-stu-id="b5b6e-259">Int32</span></span> |
| <span data-ttu-id="b5b6e-260">long varbinary</span><span class="sxs-lookup"><span data-stu-id="b5b6e-260">long varbinary</span></span> |<span data-ttu-id="b5b6e-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b5b6e-261">Byte[]</span></span> |
| <span data-ttu-id="b5b6e-262">long varchar</span><span class="sxs-lookup"><span data-stu-id="b5b6e-262">long varchar</span></span> |<span data-ttu-id="b5b6e-263">String</span><span class="sxs-lookup"><span data-stu-id="b5b6e-263">String</span></span> |
| <span data-ttu-id="b5b6e-264">longblob</span><span class="sxs-lookup"><span data-stu-id="b5b6e-264">longblob</span></span> |<span data-ttu-id="b5b6e-265">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b5b6e-265">Byte[]</span></span> |
| <span data-ttu-id="b5b6e-266">longtext</span><span class="sxs-lookup"><span data-stu-id="b5b6e-266">longtext</span></span> |<span data-ttu-id="b5b6e-267">String</span><span class="sxs-lookup"><span data-stu-id="b5b6e-267">String</span></span> |
| <span data-ttu-id="b5b6e-268">mediumblob</span><span class="sxs-lookup"><span data-stu-id="b5b6e-268">mediumblob</span></span> |<span data-ttu-id="b5b6e-269">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b5b6e-269">Byte[]</span></span> |
| <span data-ttu-id="b5b6e-270">mediumint non signé</span><span class="sxs-lookup"><span data-stu-id="b5b6e-270">mediumint unsigned</span></span> |<span data-ttu-id="b5b6e-271">Int64</span><span class="sxs-lookup"><span data-stu-id="b5b6e-271">Int64</span></span> |
| <span data-ttu-id="b5b6e-272">mediumint</span><span class="sxs-lookup"><span data-stu-id="b5b6e-272">mediumint</span></span> |<span data-ttu-id="b5b6e-273">Int32</span><span class="sxs-lookup"><span data-stu-id="b5b6e-273">Int32</span></span> |
| <span data-ttu-id="b5b6e-274">mediumtext</span><span class="sxs-lookup"><span data-stu-id="b5b6e-274">mediumtext</span></span> |<span data-ttu-id="b5b6e-275">String</span><span class="sxs-lookup"><span data-stu-id="b5b6e-275">String</span></span> |
| <span data-ttu-id="b5b6e-276">numérique</span><span class="sxs-lookup"><span data-stu-id="b5b6e-276">numeric</span></span> |<span data-ttu-id="b5b6e-277">Décimal</span><span class="sxs-lookup"><span data-stu-id="b5b6e-277">Decimal</span></span> |
| <span data-ttu-id="b5b6e-278">real</span><span class="sxs-lookup"><span data-stu-id="b5b6e-278">real</span></span> |<span data-ttu-id="b5b6e-279">Double</span><span class="sxs-lookup"><span data-stu-id="b5b6e-279">Double</span></span> |
| <span data-ttu-id="b5b6e-280">set</span><span class="sxs-lookup"><span data-stu-id="b5b6e-280">set</span></span> |<span data-ttu-id="b5b6e-281">String</span><span class="sxs-lookup"><span data-stu-id="b5b6e-281">String</span></span> |
| <span data-ttu-id="b5b6e-282">smallint non signé</span><span class="sxs-lookup"><span data-stu-id="b5b6e-282">smallint unsigned</span></span> |<span data-ttu-id="b5b6e-283">Int32</span><span class="sxs-lookup"><span data-stu-id="b5b6e-283">Int32</span></span> |
| <span data-ttu-id="b5b6e-284">smallint</span><span class="sxs-lookup"><span data-stu-id="b5b6e-284">smallint</span></span> |<span data-ttu-id="b5b6e-285">Int16</span><span class="sxs-lookup"><span data-stu-id="b5b6e-285">Int16</span></span> |
| <span data-ttu-id="b5b6e-286">texte</span><span class="sxs-lookup"><span data-stu-id="b5b6e-286">text</span></span> |<span data-ttu-id="b5b6e-287">String</span><span class="sxs-lookup"><span data-stu-id="b5b6e-287">String</span></span> |
| <span data-ttu-id="b5b6e-288">time</span><span class="sxs-lookup"><span data-stu-id="b5b6e-288">time</span></span> |<span data-ttu-id="b5b6e-289">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="b5b6e-289">TimeSpan</span></span> |
| <span data-ttu-id="b5b6e-290">timestamp</span><span class="sxs-lookup"><span data-stu-id="b5b6e-290">timestamp</span></span> |<span data-ttu-id="b5b6e-291">Datetime</span><span class="sxs-lookup"><span data-stu-id="b5b6e-291">Datetime</span></span> |
| <span data-ttu-id="b5b6e-292">tinyblob</span><span class="sxs-lookup"><span data-stu-id="b5b6e-292">tinyblob</span></span> |<span data-ttu-id="b5b6e-293">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b5b6e-293">Byte[]</span></span> |
| <span data-ttu-id="b5b6e-294">tinyint non signé</span><span class="sxs-lookup"><span data-stu-id="b5b6e-294">tinyint unsigned</span></span> |<span data-ttu-id="b5b6e-295">Int16</span><span class="sxs-lookup"><span data-stu-id="b5b6e-295">Int16</span></span> |
| <span data-ttu-id="b5b6e-296">tinyint</span><span class="sxs-lookup"><span data-stu-id="b5b6e-296">tinyint</span></span> |<span data-ttu-id="b5b6e-297">Int16</span><span class="sxs-lookup"><span data-stu-id="b5b6e-297">Int16</span></span> |
| <span data-ttu-id="b5b6e-298">tinytext</span><span class="sxs-lookup"><span data-stu-id="b5b6e-298">tinytext</span></span> |<span data-ttu-id="b5b6e-299">String</span><span class="sxs-lookup"><span data-stu-id="b5b6e-299">String</span></span> |
| <span data-ttu-id="b5b6e-300">varchar</span><span class="sxs-lookup"><span data-stu-id="b5b6e-300">varchar</span></span> |<span data-ttu-id="b5b6e-301">String</span><span class="sxs-lookup"><span data-stu-id="b5b6e-301">String</span></span> |
| <span data-ttu-id="b5b6e-302">year</span><span class="sxs-lookup"><span data-stu-id="b5b6e-302">year</span></span> |<span data-ttu-id="b5b6e-303">int</span><span class="sxs-lookup"><span data-stu-id="b5b6e-303">Int</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="b5b6e-304">Mapper les colonnes source aux colonnes du récepteur</span><span class="sxs-lookup"><span data-stu-id="b5b6e-304">Map source to sink columns</span></span>
<span data-ttu-id="b5b6e-305">Pour en savoir plus sur le mappage de colonnes du jeu de données source à des colonnes du jeu de données récepteur, voir [Mappage des colonnes d’un jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="b5b6e-305">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="b5b6e-306">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="b5b6e-306">Repeatable read from relational sources</span></span>
<span data-ttu-id="b5b6e-307">Lorsque vous copiez des données à partir de magasins de données relationnels, gardez à l’esprit la répétabilité de l’opération, afin d’éviter des résultats imprévus.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-307">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="b5b6e-308">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-308">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="b5b6e-309">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-309">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="b5b6e-310">Lorsqu’une tranche est réexécutée d’une manière ou d’une autre, vous devez vous assurer que les mêmes données sont lues et ce, quel que soit le nombre d’exécutions de la tranche.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-310">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="b5b6e-311">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="b5b6e-311">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="b5b6e-312">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="b5b6e-312">Performance and Tuning</span></span>
<span data-ttu-id="b5b6e-313">Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="b5b6e-313">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
