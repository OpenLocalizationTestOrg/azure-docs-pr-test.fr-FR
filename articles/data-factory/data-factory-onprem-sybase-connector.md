---
title: "Déplacer des données depuis Sybase à l’aide d’Azure Data Factory | Microsoft Docs"
description: "Découvrez comment déplacer des données depuis une base de données Sybase à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: b379ee10-0ff5-4974-8c87-c95f82f1c5c6
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 617e604b220b8bc1c452e67da83f733448e16c0b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a><span data-ttu-id="e6cb8-103">Déplacer des données depuis Sybase à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e6cb8-103">Move data from Sybase using Azure Data Factory</span></span>
<span data-ttu-id="e6cb8-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour déplacer des données à partir d’une base de données Sybase locale.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Sybase database.</span></span> <span data-ttu-id="e6cb8-105">Il s’appuie sur cet article, relatif aux [activités de déplacement de données](data-factory-data-movement-activities.md), qui présente une vue d’ensemble du déplacement de données avec l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="e6cb8-106">Vous pouvez copier et coller les données d’un magasin de données Sybase local dans tout magasin de données récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-106">You can copy data from an on-premises Sybase data store to any supported sink data store.</span></span> <span data-ttu-id="e6cb8-107">Consultez la table [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) pour obtenir la liste des magasins de données pris en charge en tant que récepteurs par l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="e6cb8-108">Actuellement, Data Factory prend uniquement en charge le déplacement de données d’un magasin de données Sybase vers d’autres magasins de données, mais non l’inverse.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-108">Data factory currently supports only moving data from a Sybase data store to other data stores, but not for moving data from other data stores to a Sybase data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e6cb8-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e6cb8-109">Prerequisites</span></span>
<span data-ttu-id="e6cb8-110">Le service Data Factory prend en charge la connexion à des sources Sybase locales à l'aide de la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-110">Data Factory service supports connecting to on-premises Sybase sources using the Data Management Gateway.</span></span> <span data-ttu-id="e6cb8-111">Consultez l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) pour en savoir plus sur la passerelle de gestion des données et obtenir des instructions détaillées sur la configuration de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="e6cb8-112">Une passerelle est requise même si la base de données Sybase est hébergée sur une machine virtuelle Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-112">Gateway is required even if the Sybase database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="e6cb8-113">Vous pouvez installer la passerelle sur la même machine virtuelle IaaS que le magasin de données, ou sur une autre machine virtuelle pourvu que la passerelle puisse se connecter à la base de données.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="e6cb8-114">Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="e6cb8-115">Versions prises en charge et installation</span><span class="sxs-lookup"><span data-stu-id="e6cb8-115">Supported versions and installation</span></span>
<span data-ttu-id="e6cb8-116">Pour que la passerelle de gestion des données puisse se connecter à la base de données Sybase, vous devez installer la version 16 du [fournisseur de données pour Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) ou une version ultérieure sur le même système que la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-116">For Data Management Gateway to connect to the Sybase Database, you need to install the [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="e6cb8-117">Sybase (version 16 et ultérieures) est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-117">Sybase version 16 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="e6cb8-118">Prise en main</span><span class="sxs-lookup"><span data-stu-id="e6cb8-118">Getting started</span></span>
<span data-ttu-id="e6cb8-119">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données Cassandra local à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="e6cb8-120">Le moyen le plus simple de créer un pipeline consiste à utiliser **l’Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="e6cb8-121">Consultez la page [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant Copier des données.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="e6cb8-122">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="e6cb8-123">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="e6cb8-124">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e6cb8-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="e6cb8-125">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="e6cb8-126">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="e6cb8-127">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="e6cb8-128">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="e6cb8-129">Lorsque vous utilisez des outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory à l’aide du format JSON.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="e6cb8-130">Pour consulter un exemple contenant des définitions JSON pour les entités Data Factory utilisées pour copier des données d’un magasin de données Sybase local, consultez la section [Exemple JSON : copier des données depuis une base de données Sybase vers Azure Blob](#json-example-copy-data-from-sybase-to-azure-blob) de cet article.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Sybase data store, see [JSON example: Copy data from Sybase to Azure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="e6cb8-131">Les sections suivantes contiennent des informations détaillées sur les propriétés JSON utilisées pour définir les entités Data Factory propres à un magasin de données Sybase :</span><span class="sxs-lookup"><span data-stu-id="e6cb8-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Sybase data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="e6cb8-132">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="e6cb8-132">Linked service properties</span></span>
<span data-ttu-id="e6cb8-133">Le tableau suivant fournit la description des éléments JSON spécifiques au service lié Sybase.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-133">The following table provides description for JSON elements specific to Sybase linked service.</span></span>

| <span data-ttu-id="e6cb8-134">Propriété</span><span class="sxs-lookup"><span data-stu-id="e6cb8-134">Property</span></span> | <span data-ttu-id="e6cb8-135">Description</span><span class="sxs-lookup"><span data-stu-id="e6cb8-135">Description</span></span> | <span data-ttu-id="e6cb8-136">Requis</span><span class="sxs-lookup"><span data-stu-id="e6cb8-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e6cb8-137">type</span><span class="sxs-lookup"><span data-stu-id="e6cb8-137">type</span></span> |<span data-ttu-id="e6cb8-138">Le type de propriété doit être défini sur : **OnPremisesSybase**</span><span class="sxs-lookup"><span data-stu-id="e6cb8-138">The type property must be set to: **OnPremisesSybase**</span></span> |<span data-ttu-id="e6cb8-139">Oui</span><span class="sxs-lookup"><span data-stu-id="e6cb8-139">Yes</span></span> |
| <span data-ttu-id="e6cb8-140">server</span><span class="sxs-lookup"><span data-stu-id="e6cb8-140">server</span></span> |<span data-ttu-id="e6cb8-141">Nom du serveur Sybase.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-141">Name of the Sybase server.</span></span> |<span data-ttu-id="e6cb8-142">Oui</span><span class="sxs-lookup"><span data-stu-id="e6cb8-142">Yes</span></span> |
| <span data-ttu-id="e6cb8-143">database</span><span class="sxs-lookup"><span data-stu-id="e6cb8-143">database</span></span> |<span data-ttu-id="e6cb8-144">Nom de la base de données Sybase.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-144">Name of the Sybase database.</span></span> |<span data-ttu-id="e6cb8-145">Oui</span><span class="sxs-lookup"><span data-stu-id="e6cb8-145">Yes</span></span> |
| <span data-ttu-id="e6cb8-146">schema</span><span class="sxs-lookup"><span data-stu-id="e6cb8-146">schema</span></span> |<span data-ttu-id="e6cb8-147">Nom du schéma dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-147">Name of the schema in the database.</span></span> |<span data-ttu-id="e6cb8-148">Non</span><span class="sxs-lookup"><span data-stu-id="e6cb8-148">No</span></span> |
| <span data-ttu-id="e6cb8-149">authenticationType</span><span class="sxs-lookup"><span data-stu-id="e6cb8-149">authenticationType</span></span> |<span data-ttu-id="e6cb8-150">Type d'authentification utilisé pour se connecter à la base de données Sybase.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-150">Type of authentication used to connect to the Sybase database.</span></span> <span data-ttu-id="e6cb8-151">Les valeurs possibles sont : Anonyme, De base et Windows.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-151">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="e6cb8-152">Oui</span><span class="sxs-lookup"><span data-stu-id="e6cb8-152">Yes</span></span> |
| <span data-ttu-id="e6cb8-153">username</span><span class="sxs-lookup"><span data-stu-id="e6cb8-153">username</span></span> |<span data-ttu-id="e6cb8-154">Spécifiez le nom d'utilisateur si vous utilisez l'authentification de base ou Windows.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-154">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="e6cb8-155">Non</span><span class="sxs-lookup"><span data-stu-id="e6cb8-155">No</span></span> |
| <span data-ttu-id="e6cb8-156">password</span><span class="sxs-lookup"><span data-stu-id="e6cb8-156">password</span></span> |<span data-ttu-id="e6cb8-157">Spécifiez le mot de passe du compte d’utilisateur que vous avez spécifié pour le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-157">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="e6cb8-158">Non</span><span class="sxs-lookup"><span data-stu-id="e6cb8-158">No</span></span> |
| <span data-ttu-id="e6cb8-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e6cb8-159">gatewayName</span></span> |<span data-ttu-id="e6cb8-160">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter à la base de données Sybase locale.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-160">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span></span> |<span data-ttu-id="e6cb8-161">Oui</span><span class="sxs-lookup"><span data-stu-id="e6cb8-161">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="e6cb8-162">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="e6cb8-162">Dataset properties</span></span>
<span data-ttu-id="e6cb8-163">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="e6cb8-163">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="e6cb8-164">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="e6cb8-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="e6cb8-165">La section typeProperties est différente pour chaque type de jeu de données et fournit des informations sur l'emplacement des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-165">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="e6cb8-166">La section **typeProperties** pour le jeu de données de type **RelationalTable** (qui inclut le jeu de données Sybase) a les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="e6cb8-166">The **typeProperties** section for dataset of type **RelationalTable** (which includes Sybase dataset) has the following properties:</span></span>

| <span data-ttu-id="e6cb8-167">Propriété</span><span class="sxs-lookup"><span data-stu-id="e6cb8-167">Property</span></span> | <span data-ttu-id="e6cb8-168">Description</span><span class="sxs-lookup"><span data-stu-id="e6cb8-168">Description</span></span> | <span data-ttu-id="e6cb8-169">Requis</span><span class="sxs-lookup"><span data-stu-id="e6cb8-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e6cb8-170">TableName</span><span class="sxs-lookup"><span data-stu-id="e6cb8-170">tableName</span></span> |<span data-ttu-id="e6cb8-171">Nom de la table dans l'instance de base de données Sybase à laquelle le service lié fait référence.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-171">Name of the table in the Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="e6cb8-172">Non (si la **requête** de **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="e6cb8-172">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="e6cb8-173">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="e6cb8-173">Copy activity properties</span></span>
<span data-ttu-id="e6cb8-174">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="e6cb8-174">For a full list of sections & properties available for defining activities, see [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="e6cb8-175">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-175">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="e6cb8-176">En revanche, les propriétés disponibles dans la section typeProperties de l’activité varient pour chaque type d'activité.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-176">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="e6cb8-177">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-177">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="e6cb8-178">Lorsque la source est de type **RelationalSource** (qui inclut Sybase), les propriétés suivantes sont disponibles dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="e6cb8-178">When the source is of type **RelationalSource** (which includes Sybase), the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="e6cb8-179">Propriété</span><span class="sxs-lookup"><span data-stu-id="e6cb8-179">Property</span></span> | <span data-ttu-id="e6cb8-180">Description</span><span class="sxs-lookup"><span data-stu-id="e6cb8-180">Description</span></span> | <span data-ttu-id="e6cb8-181">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="e6cb8-181">Allowed values</span></span> | <span data-ttu-id="e6cb8-182">Requis</span><span class="sxs-lookup"><span data-stu-id="e6cb8-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e6cb8-183">query</span><span class="sxs-lookup"><span data-stu-id="e6cb8-183">query</span></span> |<span data-ttu-id="e6cb8-184">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-184">Use the custom query to read data.</span></span> |<span data-ttu-id="e6cb8-185">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-185">SQL query string.</span></span> <span data-ttu-id="e6cb8-186">Par exemple : select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-186">For example: select * from MyTable.</span></span> |<span data-ttu-id="e6cb8-187">Non (si **tableName** de **dataset** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="e6cb8-187">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-sybase-to-azure-blob"></a><span data-ttu-id="e6cb8-188">Exemple JSON : copier des données depuis une base de données Sybase vers Azure Blob</span><span class="sxs-lookup"><span data-stu-id="e6cb8-188">JSON example: Copy data from Sybase to Azure Blob</span></span>
<span data-ttu-id="e6cb8-189">L’exemple suivant présente des exemples de définitions de JSON que vous pouvez utiliser pour créer un pipeline à l’aide du [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), de [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [d’Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e6cb8-189">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="e6cb8-190">Ils indiquent comment copier des données depuis une base de données Sybase vers Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-190">They show how to copy data from Sybase database to Azure Blob Storage.</span></span> <span data-ttu-id="e6cb8-191">Toutefois, les données peuvent être copiées vers l’un des récepteurs indiqués [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) , via l’activité de copie d’Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-191">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="e6cb8-192">L’exemple contient les entités de fabrique de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="e6cb8-192">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="e6cb8-193">Un service lié de type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e6cb8-193">A linked service of type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="e6cb8-194">Un service lié de type [Stockage Azure](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e6cb8-194">A liked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="e6cb8-195">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e6cb8-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="e6cb8-196">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e6cb8-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="e6cb8-197">Le [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="e6cb8-197">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="e6cb8-198">L'exemple copie toutes les heures les données de résultat d’une requête de base de données Sybase vers un objet blob.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-198">The sample copies data from a query result in Sybase database to a blob every hour.</span></span> <span data-ttu-id="e6cb8-199">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-199">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="e6cb8-200">Dans un premier temps, configurez la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-200">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="e6cb8-201">Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="e6cb8-201">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="e6cb8-202">**Service lié Sybase :**</span><span class="sxs-lookup"><span data-stu-id="e6cb8-202">**Sybase linked service:**</span></span>

```JSON
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="e6cb8-203">**Service lié Azure Blob Storage :**</span><span class="sxs-lookup"><span data-stu-id="e6cb8-203">**Azure Blob storage linked service:**</span></span>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

<span data-ttu-id="e6cb8-204">**Jeu de données d’entrée Sybase :**</span><span class="sxs-lookup"><span data-stu-id="e6cb8-204">**Sybase input dataset:**</span></span>

<span data-ttu-id="e6cb8-205">L'exemple suppose que vous avez créé une table « MyTable » dans Sybase et qu'elle contient une colonne appelée « timestamp » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-205">The sample assumes you have created a table “MyTable” in Sybase and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="e6cb8-206">La définition de external sur true informe le service Data Factory que le jeu de données est externe à la Data Factory et non produite par une activité dans la Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-206">Setting “external”: true informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="e6cb8-207">Notez que le **type** du service lié est défini sur **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-207">Notice that the **type** of the linked service is set to: **RelationalTable**.</span></span>

```JSON
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
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

<span data-ttu-id="e6cb8-208">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="e6cb8-208">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="e6cb8-209">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="e6cb8-209">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="e6cb8-210">Le chemin d’accès du dossier pour l’objet blob est évalué dynamiquement en fonction de l’heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-210">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="e6cb8-211">Le chemin d'accès du dossier utilise l'année, le mois, le jour et l'heure de l'heure de début.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-211">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
    "name": "AzureBlobSybaseDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sybase/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="e6cb8-212">**Pipeline avec activité de copie :**</span><span class="sxs-lookup"><span data-stu-id="e6cb8-212">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="e6cb8-213">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d’entrée et de sortie et planifiée pour s’exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-213">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="e6cb8-214">Dans la définition du pipeline JSON, le type **source** est défini sur **RelationalSource** et le type **sink** est défini sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-214">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="e6cb8-215">La requête SQL spécifiée pour la propriété **query** sélectionne les données de la table DBA.Orders dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-215">The SQL query specified for the **query** property selects the data from the DBA.Orders table in the database.</span></span>

```JSON
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from DBA.Orders"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "SybaseDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobSybaseDataSet"
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
                "name": "SybaseToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-sybase"></a><span data-ttu-id="e6cb8-216">Mappage de type pour Sybase</span><span class="sxs-lookup"><span data-stu-id="e6cb8-216">Type mapping for Sybase</span></span>
<span data-ttu-id="e6cb8-217">Comme mentionné dans l’article consacré aux [activités de déplacement des données](data-factory-data-movement-activities.md) , l’activité de copie convertit automatiquement les types source en types récepteur à l’aide de l’approche en 2 étapes suivante :</span><span class="sxs-lookup"><span data-stu-id="e6cb8-217">As mentioned in the [Data Movement Activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="e6cb8-218">Conversion de types natifs source en types .NET</span><span class="sxs-lookup"><span data-stu-id="e6cb8-218">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="e6cb8-219">Conversion de types .NET en types récepteur natifs</span><span class="sxs-lookup"><span data-stu-id="e6cb8-219">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="e6cb8-220">Sybase prend en charge les types T-SQL et T-SQL.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-220">Sybase supports T-SQL and T-SQL types.</span></span> <span data-ttu-id="e6cb8-221">Pour une table de mappage de types SQL en un type .NET, consultez l’article [Connecteur Azure SQL](data-factory-azure-sql-connector.md) .</span><span class="sxs-lookup"><span data-stu-id="e6cb8-221">For a mapping table from sql types to .NET type, see [Azure SQL Connector](data-factory-azure-sql-connector.md) article.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="e6cb8-222">Mapper les colonnes source aux colonnes du récepteur</span><span class="sxs-lookup"><span data-stu-id="e6cb8-222">Map source to sink columns</span></span>
<span data-ttu-id="e6cb8-223">Pour en savoir plus sur le mappage de colonnes du jeu de données source à des colonnes du jeu de données récepteur, voir [Mappage des colonnes d’un jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="e6cb8-223">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="e6cb8-224">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="e6cb8-224">Repeatable read from relational sources</span></span>
<span data-ttu-id="e6cb8-225">Lorsque vous copiez des données à partir de magasins de données relationnels, gardez à l’esprit la répétabilité de l’opération, afin d’éviter des résultats imprévus.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-225">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="e6cb8-226">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-226">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="e6cb8-227">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-227">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="e6cb8-228">Lorsqu’une tranche est réexécutée d’une manière ou d’une autre, vous devez vous assurer que les mêmes données sont lues et ce, quel que soit le nombre d’exécutions de la tranche.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-228">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="e6cb8-229">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="e6cb8-229">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="e6cb8-230">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="e6cb8-230">Performance and Tuning</span></span>
<span data-ttu-id="e6cb8-231">Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="e6cb8-231">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
