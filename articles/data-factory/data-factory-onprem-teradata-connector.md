---
title: "Déplacer des données depuis Teradata à l’aide d’Azure Data Factory | Microsoft Docs"
description: "En savoir plus sur le connecteur Teradata pour le service Data Factory qui vous permet de déplacer des données depuis une base de données Teradata"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 98eb76d8-5f3d-4667-b76e-e59ed3eea3ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 01edb32cd9e20d4199feac5b98a73aa06b74fec2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="86c8b-103">Déplacer des données depuis Teradata à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="86c8b-103">Move data from Teradata using Azure Data Factory</span></span>
<span data-ttu-id="86c8b-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour déplacer des données à partir d’une base de données Teradata locale.</span><span class="sxs-lookup"><span data-stu-id="86c8b-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Teradata database.</span></span> <span data-ttu-id="86c8b-105">Il s’appuie sur l’article [Activités de déplacement des données](data-factory-data-movement-activities.md), qui présente une vue d’ensemble du déplacement de données avec l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="86c8b-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="86c8b-106">Vous pouvez copier et coller les données d’un magasin de données Teradata local vers tout magasin de données récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="86c8b-106">You can copy data from an on-premises Teradata data store to any supported sink data store.</span></span> <span data-ttu-id="86c8b-107">Consultez la table [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) pour obtenir la liste des magasins de données pris en charge en tant que récepteurs par l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="86c8b-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="86c8b-108">Actuellement, Data Factory prend uniquement en charge le déplacement de données d’un magasin de données Teradata vers d’autres magasins de données, mais non l’inverse.</span><span class="sxs-lookup"><span data-stu-id="86c8b-108">Data factory currently supports only moving data from a Teradata data store to other data stores, but not for moving data from other data stores to a Teradata data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="86c8b-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="86c8b-109">Prerequisites</span></span>
<span data-ttu-id="86c8b-110">Data Factory prend en charge la connexion à des sources Teradata locales via la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="86c8b-110">Data factory supports connecting to on-premises Teradata sources via the Data Management Gateway.</span></span> <span data-ttu-id="86c8b-111">Consultez l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) pour en savoir plus sur la passerelle de gestion des données et obtenir des instructions détaillées sur la configuration de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="86c8b-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="86c8b-112">Une passerelle est requise même si la base de données  Teradata est hébergée sur une machine virtuelle Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="86c8b-112">Gateway is required even if the Teradata is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="86c8b-113">Vous pouvez installer la passerelle sur la même machine virtuelle IaaS que le magasin de données, ou sur une autre machine virtuelle pourvu que la passerelle puisse se connecter à la base de données.</span><span class="sxs-lookup"><span data-stu-id="86c8b-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="86c8b-114">Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.</span><span class="sxs-lookup"><span data-stu-id="86c8b-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="86c8b-115">Versions prises en charge et installation</span><span class="sxs-lookup"><span data-stu-id="86c8b-115">Supported versions and installation</span></span>
<span data-ttu-id="86c8b-116">Pour que la passerelle de gestion des données puisse se connecter à la base de données Teradata, vous devez installer le [fournisseur de données .NET pour Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 ou ultérieure sur le même système que la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="86c8b-116">For Data Management Gateway to connect to the Teradata Database, you need to install the [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="86c8b-117">Teradata version 12 et ultérieures est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="86c8b-117">Teradata version 12 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="86c8b-118">Prise en main</span><span class="sxs-lookup"><span data-stu-id="86c8b-118">Getting started</span></span>
<span data-ttu-id="86c8b-119">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données Cassandra local à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="86c8b-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="86c8b-120">Le moyen le plus simple de créer un pipeline consiste à utiliser **l’Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="86c8b-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="86c8b-121">Consultez la page [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant Copier des données.</span><span class="sxs-lookup"><span data-stu-id="86c8b-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="86c8b-122">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="86c8b-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="86c8b-123">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="86c8b-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="86c8b-124">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="86c8b-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="86c8b-125">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="86c8b-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="86c8b-126">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="86c8b-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="86c8b-127">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="86c8b-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="86c8b-128">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="86c8b-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="86c8b-129">Lorsque vous utilisez des outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory au format JSON.</span><span class="sxs-lookup"><span data-stu-id="86c8b-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="86c8b-130">Pour consulter un exemple contenant des définitions JSON pour les entités Data Factory utilisées pour copier des données d’un magasin de données Teradata local, consultez la section [Exemple JSON : copier des données depuis un système Teradata vers Azure Blob](#json-example-copy-data-from-teradata-to-azure-blob) de cet article.</span><span class="sxs-lookup"><span data-stu-id="86c8b-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata to Azure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="86c8b-131">Les sections suivantes contiennent des informations détaillées sur les propriétés JSON utilisées pour définir les entités Data Factory propres à un magasin de données Teradata :</span><span class="sxs-lookup"><span data-stu-id="86c8b-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Teradata data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="86c8b-132">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="86c8b-132">Linked service properties</span></span>
<span data-ttu-id="86c8b-133">Le tableau suivant fournit la description des éléments JSON spécifiques au service lié Teradata.</span><span class="sxs-lookup"><span data-stu-id="86c8b-133">The following table provides description for JSON elements specific to Teradata linked service.</span></span>

| <span data-ttu-id="86c8b-134">Propriété</span><span class="sxs-lookup"><span data-stu-id="86c8b-134">Property</span></span> | <span data-ttu-id="86c8b-135">Description</span><span class="sxs-lookup"><span data-stu-id="86c8b-135">Description</span></span> | <span data-ttu-id="86c8b-136">Requis</span><span class="sxs-lookup"><span data-stu-id="86c8b-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="86c8b-137">type</span><span class="sxs-lookup"><span data-stu-id="86c8b-137">type</span></span> |<span data-ttu-id="86c8b-138">Le type de propriété doit être défini sur : **OnPremisesTeradata**</span><span class="sxs-lookup"><span data-stu-id="86c8b-138">The type property must be set to: **OnPremisesTeradata**</span></span> |<span data-ttu-id="86c8b-139">Oui</span><span class="sxs-lookup"><span data-stu-id="86c8b-139">Yes</span></span> |
| <span data-ttu-id="86c8b-140">server</span><span class="sxs-lookup"><span data-stu-id="86c8b-140">server</span></span> |<span data-ttu-id="86c8b-141">Nom du serveur Teradata.</span><span class="sxs-lookup"><span data-stu-id="86c8b-141">Name of the Teradata server.</span></span> |<span data-ttu-id="86c8b-142">Oui</span><span class="sxs-lookup"><span data-stu-id="86c8b-142">Yes</span></span> |
| <span data-ttu-id="86c8b-143">authenticationType</span><span class="sxs-lookup"><span data-stu-id="86c8b-143">authenticationType</span></span> |<span data-ttu-id="86c8b-144">Type d'authentification utilisé pour se connecter à la base de données Teradata.</span><span class="sxs-lookup"><span data-stu-id="86c8b-144">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="86c8b-145">Les valeurs possibles sont : Anonyme, De base et Windows.</span><span class="sxs-lookup"><span data-stu-id="86c8b-145">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="86c8b-146">Oui</span><span class="sxs-lookup"><span data-stu-id="86c8b-146">Yes</span></span> |
| <span data-ttu-id="86c8b-147">username</span><span class="sxs-lookup"><span data-stu-id="86c8b-147">username</span></span> |<span data-ttu-id="86c8b-148">Spécifiez le nom d'utilisateur si vous utilisez l'authentification de base ou Windows.</span><span class="sxs-lookup"><span data-stu-id="86c8b-148">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="86c8b-149">Non</span><span class="sxs-lookup"><span data-stu-id="86c8b-149">No</span></span> |
| <span data-ttu-id="86c8b-150">password</span><span class="sxs-lookup"><span data-stu-id="86c8b-150">password</span></span> |<span data-ttu-id="86c8b-151">Spécifiez le mot de passe du compte d’utilisateur que vous avez spécifié pour le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="86c8b-151">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="86c8b-152">Non</span><span class="sxs-lookup"><span data-stu-id="86c8b-152">No</span></span> |
| <span data-ttu-id="86c8b-153">gatewayName</span><span class="sxs-lookup"><span data-stu-id="86c8b-153">gatewayName</span></span> |<span data-ttu-id="86c8b-154">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter à la base de données Teradata locale.</span><span class="sxs-lookup"><span data-stu-id="86c8b-154">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="86c8b-155">Oui</span><span class="sxs-lookup"><span data-stu-id="86c8b-155">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="86c8b-156">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="86c8b-156">Dataset properties</span></span>
<span data-ttu-id="86c8b-157">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="86c8b-157">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="86c8b-158">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="86c8b-158">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="86c8b-159">La section **typeProperties** est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="86c8b-159">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="86c8b-160">Il n’existe actuellement aucune propriété type prise en charge pour le jeu de données Teradata.</span><span class="sxs-lookup"><span data-stu-id="86c8b-160">Currently, there are no type properties supported for the Teradata dataset.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="86c8b-161">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="86c8b-161">Copy activity properties</span></span>
<span data-ttu-id="86c8b-162">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="86c8b-162">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="86c8b-163">Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités.</span><span class="sxs-lookup"><span data-stu-id="86c8b-163">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="86c8b-164">En revanche, les propriétés disponibles dans la section typeProperties de l’activité varient pour chaque type d'activité.</span><span class="sxs-lookup"><span data-stu-id="86c8b-164">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="86c8b-165">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="86c8b-165">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="86c8b-166">Lorsque la source est de type **RelationalSource** (ce qui comprend Teradata), les propriétés suivantes sont disponibles dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="86c8b-166">When the source is of type **RelationalSource** (which includes Teradata), the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="86c8b-167">Propriété</span><span class="sxs-lookup"><span data-stu-id="86c8b-167">Property</span></span> | <span data-ttu-id="86c8b-168">Description</span><span class="sxs-lookup"><span data-stu-id="86c8b-168">Description</span></span> | <span data-ttu-id="86c8b-169">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="86c8b-169">Allowed values</span></span> | <span data-ttu-id="86c8b-170">Requis</span><span class="sxs-lookup"><span data-stu-id="86c8b-170">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="86c8b-171">query</span><span class="sxs-lookup"><span data-stu-id="86c8b-171">query</span></span> |<span data-ttu-id="86c8b-172">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="86c8b-172">Use the custom query to read data.</span></span> |<span data-ttu-id="86c8b-173">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="86c8b-173">SQL query string.</span></span> <span data-ttu-id="86c8b-174">Par exemple : select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="86c8b-174">For example: select * from MyTable.</span></span> |<span data-ttu-id="86c8b-175">Oui</span><span class="sxs-lookup"><span data-stu-id="86c8b-175">Yes</span></span> |

### <a name="json-example-copy-data-from-teradata-to-azure-blob"></a><span data-ttu-id="86c8b-176">Exemple JSON : copier des données depuis un système Teradata vers Azure Blob</span><span class="sxs-lookup"><span data-stu-id="86c8b-176">JSON example: Copy data from Teradata to Azure Blob</span></span>
<span data-ttu-id="86c8b-177">L’exemple suivant présente des exemples de définitions de JSON que vous pouvez utiliser pour créer un pipeline à l’aide du [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), de [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [d’Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="86c8b-177">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="86c8b-178">Ils indiquent comment copier des données depuis Teradata vers Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="86c8b-178">They show how to copy data from Teradata to Azure Blob Storage.</span></span> <span data-ttu-id="86c8b-179">Toutefois, les données peuvent être copiées vers l’un des récepteurs indiqués [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) , via l’activité de copie d’Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="86c8b-179">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="86c8b-180">L’exemple contient les entités de fabrique de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="86c8b-180">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="86c8b-181">Un service lié de type [OnPremisesTeradata](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="86c8b-181">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span></span>
2. <span data-ttu-id="86c8b-182">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="86c8b-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="86c8b-183">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="86c8b-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="86c8b-184">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="86c8b-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="86c8b-185">Le [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [RelationalSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="86c8b-185">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="86c8b-186">L'exemple copie toutes les heures les données de résultat d’une requête de base de données Teradata vers un objet blob.</span><span class="sxs-lookup"><span data-stu-id="86c8b-186">The sample copies data from a query result in Teradata database to a blob every hour.</span></span> <span data-ttu-id="86c8b-187">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="86c8b-187">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="86c8b-188">Dans un premier temps, configurez la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="86c8b-188">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="86c8b-189">Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="86c8b-189">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="86c8b-190">**Service lié Teradata :**</span><span class="sxs-lookup"><span data-stu-id="86c8b-190">**Teradata linked service:**</span></span>

```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="86c8b-191">**Service lié Azure Blob Storage :**</span><span class="sxs-lookup"><span data-stu-id="86c8b-191">**Azure Blob storage linked service:**</span></span>

```json
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

<span data-ttu-id="86c8b-192">**Jeu de données d’entrée Teradata :**</span><span class="sxs-lookup"><span data-stu-id="86c8b-192">**Teradata input dataset:**</span></span>

<span data-ttu-id="86c8b-193">L'exemple suppose que vous avez créé une table « MyTable » dans Teradata et qu'elle contient une colonne appelée « timestamp » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="86c8b-193">The sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="86c8b-194">La définition de « external » : true sur informe le service Data Factory qu’il s’agit d’un jeu de données qui est externe à la Data Factory et non produit par une activité dans la Data Factory.</span><span class="sxs-lookup"><span data-stu-id="86c8b-194">Setting “external”: true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "TeradataDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {
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

<span data-ttu-id="86c8b-195">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="86c8b-195">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="86c8b-196">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="86c8b-196">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="86c8b-197">Le chemin d’accès du dossier pour l’objet blob est évalué dynamiquement en fonction de l’heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="86c8b-197">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="86c8b-198">Le chemin d'accès du dossier utilise l'année, le mois, le jour et l'heure de l'heure de début.</span><span class="sxs-lookup"><span data-stu-id="86c8b-198">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobTeradataDataSet",
    "properties": {
        "published": false,
        "location": {
            "type": "AzureBlobLocation",
            "folderPath": "mycontainer/teradata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            ],
            "linkedServiceName": "AzureStorageLinkedService"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="86c8b-199">**Pipeline avec activité de copie :**</span><span class="sxs-lookup"><span data-stu-id="86c8b-199">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="86c8b-200">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d’entrée et de sortie et planifiée pour s’exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="86c8b-200">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="86c8b-201">Dans la définition du pipeline JSON, le type **source** est défini sur **RelationalSource** et le type **sink** est défini sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="86c8b-201">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="86c8b-202">La requête SQL spécifiée pour la propriété **query** sélectionne les données de la dernière heure à copier.</span><span class="sxs-lookup"><span data-stu-id="86c8b-202">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "TeradataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobTeradataDataSet"
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
                "name": "TeradataToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z",
        "isPaused": false
    }
}
```
## <a name="type-mapping-for-teradata"></a><span data-ttu-id="86c8b-203">Mappage de type pour Teradata</span><span class="sxs-lookup"><span data-stu-id="86c8b-203">Type mapping for Teradata</span></span>
<span data-ttu-id="86c8b-204">Comme mentionné dans l’article consacré aux [activités de déplacement des données](data-factory-data-movement-activities.md) , l’activité de copie convertit automatiquement des types source en types récepteur à l’aide de l’approche en 2 étapes suivante :</span><span class="sxs-lookup"><span data-stu-id="86c8b-204">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="86c8b-205">Conversion de types natifs source en types .NET</span><span class="sxs-lookup"><span data-stu-id="86c8b-205">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="86c8b-206">Conversion de types .NET en types récepteur natifs</span><span class="sxs-lookup"><span data-stu-id="86c8b-206">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="86c8b-207">Lors du déplacement de données vers Teradata, les mappages suivants sont utilisés pour passer du type Teradata au type .NET.</span><span class="sxs-lookup"><span data-stu-id="86c8b-207">When moving data to Teradata, the following mappings are used from Teradata type to .NET type.</span></span>

| <span data-ttu-id="86c8b-208">Type de base de données Teradata</span><span class="sxs-lookup"><span data-stu-id="86c8b-208">Teradata Database type</span></span> | <span data-ttu-id="86c8b-209">Type de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="86c8b-209">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="86c8b-210">Char</span><span class="sxs-lookup"><span data-stu-id="86c8b-210">Char</span></span> |<span data-ttu-id="86c8b-211">String</span><span class="sxs-lookup"><span data-stu-id="86c8b-211">String</span></span> |
| <span data-ttu-id="86c8b-212">Clob</span><span class="sxs-lookup"><span data-stu-id="86c8b-212">Clob</span></span> |<span data-ttu-id="86c8b-213">String</span><span class="sxs-lookup"><span data-stu-id="86c8b-213">String</span></span> |
| <span data-ttu-id="86c8b-214">Graphic</span><span class="sxs-lookup"><span data-stu-id="86c8b-214">Graphic</span></span> |<span data-ttu-id="86c8b-215">String</span><span class="sxs-lookup"><span data-stu-id="86c8b-215">String</span></span> |
| <span data-ttu-id="86c8b-216">VarChar</span><span class="sxs-lookup"><span data-stu-id="86c8b-216">VarChar</span></span> |<span data-ttu-id="86c8b-217">String</span><span class="sxs-lookup"><span data-stu-id="86c8b-217">String</span></span> |
| <span data-ttu-id="86c8b-218">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="86c8b-218">VarGraphic</span></span> |<span data-ttu-id="86c8b-219">String</span><span class="sxs-lookup"><span data-stu-id="86c8b-219">String</span></span> |
| <span data-ttu-id="86c8b-220">Blob</span><span class="sxs-lookup"><span data-stu-id="86c8b-220">Blob</span></span> |<span data-ttu-id="86c8b-221">Byte[]</span><span class="sxs-lookup"><span data-stu-id="86c8b-221">Byte[]</span></span> |
| <span data-ttu-id="86c8b-222">Byte</span><span class="sxs-lookup"><span data-stu-id="86c8b-222">Byte</span></span> |<span data-ttu-id="86c8b-223">Byte[]</span><span class="sxs-lookup"><span data-stu-id="86c8b-223">Byte[]</span></span> |
| <span data-ttu-id="86c8b-224">VarByte</span><span class="sxs-lookup"><span data-stu-id="86c8b-224">VarByte</span></span> |<span data-ttu-id="86c8b-225">Byte[]</span><span class="sxs-lookup"><span data-stu-id="86c8b-225">Byte[]</span></span> |
| <span data-ttu-id="86c8b-226">BigInt</span><span class="sxs-lookup"><span data-stu-id="86c8b-226">BigInt</span></span> |<span data-ttu-id="86c8b-227">Int64</span><span class="sxs-lookup"><span data-stu-id="86c8b-227">Int64</span></span> |
| <span data-ttu-id="86c8b-228">ByteInt</span><span class="sxs-lookup"><span data-stu-id="86c8b-228">ByteInt</span></span> |<span data-ttu-id="86c8b-229">Int16</span><span class="sxs-lookup"><span data-stu-id="86c8b-229">Int16</span></span> |
| <span data-ttu-id="86c8b-230">Décimal</span><span class="sxs-lookup"><span data-stu-id="86c8b-230">Decimal</span></span> |<span data-ttu-id="86c8b-231">Décimal</span><span class="sxs-lookup"><span data-stu-id="86c8b-231">Decimal</span></span> |
| <span data-ttu-id="86c8b-232">Double</span><span class="sxs-lookup"><span data-stu-id="86c8b-232">Double</span></span> |<span data-ttu-id="86c8b-233">Double</span><span class="sxs-lookup"><span data-stu-id="86c8b-233">Double</span></span> |
| <span data-ttu-id="86c8b-234">Integer</span><span class="sxs-lookup"><span data-stu-id="86c8b-234">Integer</span></span> |<span data-ttu-id="86c8b-235">Int32</span><span class="sxs-lookup"><span data-stu-id="86c8b-235">Int32</span></span> |
| <span data-ttu-id="86c8b-236">Number</span><span class="sxs-lookup"><span data-stu-id="86c8b-236">Number</span></span> |<span data-ttu-id="86c8b-237">Double</span><span class="sxs-lookup"><span data-stu-id="86c8b-237">Double</span></span> |
| <span data-ttu-id="86c8b-238">SmallInt</span><span class="sxs-lookup"><span data-stu-id="86c8b-238">SmallInt</span></span> |<span data-ttu-id="86c8b-239">Int16</span><span class="sxs-lookup"><span data-stu-id="86c8b-239">Int16</span></span> |
| <span data-ttu-id="86c8b-240">Date</span><span class="sxs-lookup"><span data-stu-id="86c8b-240">Date</span></span> |<span data-ttu-id="86c8b-241">DateTime</span><span class="sxs-lookup"><span data-stu-id="86c8b-241">DateTime</span></span> |
| <span data-ttu-id="86c8b-242">Time</span><span class="sxs-lookup"><span data-stu-id="86c8b-242">Time</span></span> |<span data-ttu-id="86c8b-243">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="86c8b-243">TimeSpan</span></span> |
| <span data-ttu-id="86c8b-244">Time With Time Zone</span><span class="sxs-lookup"><span data-stu-id="86c8b-244">Time With Time Zone</span></span> |<span data-ttu-id="86c8b-245">String</span><span class="sxs-lookup"><span data-stu-id="86c8b-245">String</span></span> |
| <span data-ttu-id="86c8b-246">Timestamp</span><span class="sxs-lookup"><span data-stu-id="86c8b-246">Timestamp</span></span> |<span data-ttu-id="86c8b-247">DateTime</span><span class="sxs-lookup"><span data-stu-id="86c8b-247">DateTime</span></span> |
| <span data-ttu-id="86c8b-248">Timestamp With Time Zone</span><span class="sxs-lookup"><span data-stu-id="86c8b-248">Timestamp With Time Zone</span></span> |<span data-ttu-id="86c8b-249">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="86c8b-249">DateTimeOffset</span></span> |
| <span data-ttu-id="86c8b-250">Interval Day</span><span class="sxs-lookup"><span data-stu-id="86c8b-250">Interval Day</span></span> |<span data-ttu-id="86c8b-251">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="86c8b-251">TimeSpan</span></span> |
| <span data-ttu-id="86c8b-252">Interval Day To Hour</span><span class="sxs-lookup"><span data-stu-id="86c8b-252">Interval Day To Hour</span></span> |<span data-ttu-id="86c8b-253">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="86c8b-253">TimeSpan</span></span> |
| <span data-ttu-id="86c8b-254">Interval Day To Minute</span><span class="sxs-lookup"><span data-stu-id="86c8b-254">Interval Day To Minute</span></span> |<span data-ttu-id="86c8b-255">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="86c8b-255">TimeSpan</span></span> |
| <span data-ttu-id="86c8b-256">Interval Day To Second</span><span class="sxs-lookup"><span data-stu-id="86c8b-256">Interval Day To Second</span></span> |<span data-ttu-id="86c8b-257">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="86c8b-257">TimeSpan</span></span> |
| <span data-ttu-id="86c8b-258">Interval Hour</span><span class="sxs-lookup"><span data-stu-id="86c8b-258">Interval Hour</span></span> |<span data-ttu-id="86c8b-259">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="86c8b-259">TimeSpan</span></span> |
| <span data-ttu-id="86c8b-260">Interval Hour To Minute</span><span class="sxs-lookup"><span data-stu-id="86c8b-260">Interval Hour To Minute</span></span> |<span data-ttu-id="86c8b-261">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="86c8b-261">TimeSpan</span></span> |
| <span data-ttu-id="86c8b-262">Interval Hour To Second</span><span class="sxs-lookup"><span data-stu-id="86c8b-262">Interval Hour To Second</span></span> |<span data-ttu-id="86c8b-263">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="86c8b-263">TimeSpan</span></span> |
| <span data-ttu-id="86c8b-264">Interval Minute</span><span class="sxs-lookup"><span data-stu-id="86c8b-264">Interval Minute</span></span> |<span data-ttu-id="86c8b-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="86c8b-265">TimeSpan</span></span> |
| <span data-ttu-id="86c8b-266">Interval Minute To Second</span><span class="sxs-lookup"><span data-stu-id="86c8b-266">Interval Minute To Second</span></span> |<span data-ttu-id="86c8b-267">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="86c8b-267">TimeSpan</span></span> |
| <span data-ttu-id="86c8b-268">Interval Second</span><span class="sxs-lookup"><span data-stu-id="86c8b-268">Interval Second</span></span> |<span data-ttu-id="86c8b-269">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="86c8b-269">TimeSpan</span></span> |
| <span data-ttu-id="86c8b-270">Interval Year</span><span class="sxs-lookup"><span data-stu-id="86c8b-270">Interval Year</span></span> |<span data-ttu-id="86c8b-271">String</span><span class="sxs-lookup"><span data-stu-id="86c8b-271">String</span></span> |
| <span data-ttu-id="86c8b-272">Interval Year To Month</span><span class="sxs-lookup"><span data-stu-id="86c8b-272">Interval Year To Month</span></span> |<span data-ttu-id="86c8b-273">String</span><span class="sxs-lookup"><span data-stu-id="86c8b-273">String</span></span> |
| <span data-ttu-id="86c8b-274">Interval Month</span><span class="sxs-lookup"><span data-stu-id="86c8b-274">Interval Month</span></span> |<span data-ttu-id="86c8b-275">String</span><span class="sxs-lookup"><span data-stu-id="86c8b-275">String</span></span> |
| <span data-ttu-id="86c8b-276">Period(Date)</span><span class="sxs-lookup"><span data-stu-id="86c8b-276">Period(Date)</span></span> |<span data-ttu-id="86c8b-277">String</span><span class="sxs-lookup"><span data-stu-id="86c8b-277">String</span></span> |
| <span data-ttu-id="86c8b-278">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="86c8b-278">Period(Time)</span></span> |<span data-ttu-id="86c8b-279">String</span><span class="sxs-lookup"><span data-stu-id="86c8b-279">String</span></span> |
| <span data-ttu-id="86c8b-280">Period(Time With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="86c8b-280">Period(Time With Time Zone)</span></span> |<span data-ttu-id="86c8b-281">String</span><span class="sxs-lookup"><span data-stu-id="86c8b-281">String</span></span> |
| <span data-ttu-id="86c8b-282">Period(Timestamp)</span><span class="sxs-lookup"><span data-stu-id="86c8b-282">Period(Timestamp)</span></span> |<span data-ttu-id="86c8b-283">String</span><span class="sxs-lookup"><span data-stu-id="86c8b-283">String</span></span> |
| <span data-ttu-id="86c8b-284">Period(Timestamp With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="86c8b-284">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="86c8b-285">String</span><span class="sxs-lookup"><span data-stu-id="86c8b-285">String</span></span> |
| <span data-ttu-id="86c8b-286">Xml</span><span class="sxs-lookup"><span data-stu-id="86c8b-286">Xml</span></span> |<span data-ttu-id="86c8b-287">String</span><span class="sxs-lookup"><span data-stu-id="86c8b-287">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="86c8b-288">Mapper les colonnes source aux colonnes du récepteur</span><span class="sxs-lookup"><span data-stu-id="86c8b-288">Map source to sink columns</span></span>
<span data-ttu-id="86c8b-289">Pour en savoir plus sur le mappage de colonnes du jeu de données source à des colonnes du jeu de données récepteur, voir [Mappage des colonnes d’un jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="86c8b-289">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="86c8b-290">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="86c8b-290">Repeatable read from relational sources</span></span>
<span data-ttu-id="86c8b-291">Lorsque vous copiez des données à partir de magasins de données relationnels, gardez à l’esprit la répétabilité de l’opération, afin d’éviter des résultats imprévus.</span><span class="sxs-lookup"><span data-stu-id="86c8b-291">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="86c8b-292">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="86c8b-292">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="86c8b-293">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="86c8b-293">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="86c8b-294">Lorsqu’une tranche est réexécutée d’une manière ou d’une autre, vous devez vous assurer que les mêmes données sont lues et ce, quel que soit le nombre d’exécutions de la tranche.</span><span class="sxs-lookup"><span data-stu-id="86c8b-294">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="86c8b-295">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="86c8b-295">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="86c8b-296">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="86c8b-296">Performance and Tuning</span></span>
<span data-ttu-id="86c8b-297">Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="86c8b-297">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
