---
title: "Envoyer des données à l’index de recherche à l’aide de Data Factory | Microsoft Docs"
description: "Découvrez comment envoyer des données à l’index Recherche Azure à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 5c617c7a2f2eb4da2164ce5f802354a64dfd1fa1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="push-data-to-an-azure-search-index-by-using-azure-data-factory"></a><span data-ttu-id="8fe90-103">Envoyer des données à un index Recherche Azure à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="8fe90-103">Push data to an Azure Search index by using Azure Data Factory</span></span>
<span data-ttu-id="8fe90-104">Cet article décrit l’utilisation de l’activité de copie pour envoyer des données d’une banque de données source prise en charge à l’index Recherche Azure.</span><span class="sxs-lookup"><span data-stu-id="8fe90-104">This article describes how to use the Copy Activity to push data from a supported source data store to Azure Search index.</span></span> <span data-ttu-id="8fe90-105">Les magasins de données sources pris en charge sont répertoriés dans la colonne Source du tableau des [sources et récepteurs pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="8fe90-105">Supported source data stores are listed in the Source column of the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="8fe90-106">Cet article s’appuie sur l’article des [activités de déplacement des données](data-factory-data-movement-activities.md) qui présente une vue d’ensemble du déplacement des données avec l’activité de copie et les combinaisons de magasins de données prises en charge.</span><span class="sxs-lookup"><span data-stu-id="8fe90-106">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="8fe90-107">Activation de la connectivité</span><span class="sxs-lookup"><span data-stu-id="8fe90-107">Enabling connectivity</span></span>
<span data-ttu-id="8fe90-108">Pour permettre au service Data Factory de se connecter à un magasin de données local, vous devez installer la passerelle de gestion des données dans votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="8fe90-108">To allow Data Factory service connect to an on-premises data store, you install Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="8fe90-109">Vous pouvez l’installer sur l’ordinateur qui héberge le magasin de données sources ou sur un autre ordinateur afin d’éviter toute mise en concurrence des ressources avec le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="8fe90-109">You can install gateway on the same machine that hosts the source data store or on a separate machine to avoid competing for resources with the data store.</span></span>

<span data-ttu-id="8fe90-110">La passerelle de gestion des données connecte des sources de données locales à des services cloud de manière gérée et sécurisée.</span><span class="sxs-lookup"><span data-stu-id="8fe90-110">Data Management Gateway connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="8fe90-111">Pour plus d’informations sur la passerelle de gestion de données, consultez l’article [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="8fe90-111">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="8fe90-112">Prise en main</span><span class="sxs-lookup"><span data-stu-id="8fe90-112">Getting started</span></span>
<span data-ttu-id="8fe90-113">Vous pouvez créer un pipeline avec une activité de copie qui transmet les données d’une banque de données source à l’index Recherche Azure à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="8fe90-113">You can create a pipeline with a copy activity that pushes data from a source data store to Azure Search index by using different tools/APIs.</span></span>

<span data-ttu-id="8fe90-114">Le moyen le plus simple de créer un pipeline consiste à utiliser **l’Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="8fe90-114">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="8fe90-115">Consultez la page [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant Copier des données.</span><span class="sxs-lookup"><span data-stu-id="8fe90-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="8fe90-116">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="8fe90-116">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="8fe90-117">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="8fe90-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="8fe90-118">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8fe90-118">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="8fe90-119">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="8fe90-119">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="8fe90-120">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="8fe90-120">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="8fe90-121">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="8fe90-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="8fe90-122">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="8fe90-122">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="8fe90-123">Lorsque vous utilisez des outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory au format JSON.</span><span class="sxs-lookup"><span data-stu-id="8fe90-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="8fe90-124">Pour consulter un exemple contenant des définitions JSON pour les entités Data Factory utilisées pour copier des données vers l’index Recherche Azure, consultez la section [Exemple JSON : copier des données depuis un serveur SQL local vers l’index Recherche Azure](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) de cet article.</span><span class="sxs-lookup"><span data-stu-id="8fe90-124">For a sample with JSON definitions for Data Factory entities that are used to copy data to Azure Search index, see [JSON example: Copy data from on-premises SQL Server to Azure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span></span> 

<span data-ttu-id="8fe90-125">Les sections suivantes offrent des informations détaillées sur les propriétés JSON utilisées pour définir les entités Data Factory propres à l’Index Recherche Azure :</span><span class="sxs-lookup"><span data-stu-id="8fe90-125">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Search Index:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="8fe90-126">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="8fe90-126">Linked service properties</span></span>

<span data-ttu-id="8fe90-127">Le tableau suivant décrit les éléments JSON propres au service lié Recherche Azure.</span><span class="sxs-lookup"><span data-stu-id="8fe90-127">The following table provides descriptions for JSON elements that are specific to the Azure Search linked service.</span></span>

| <span data-ttu-id="8fe90-128">Propriété</span><span class="sxs-lookup"><span data-stu-id="8fe90-128">Property</span></span> | <span data-ttu-id="8fe90-129">Description</span><span class="sxs-lookup"><span data-stu-id="8fe90-129">Description</span></span> | <span data-ttu-id="8fe90-130">Requis</span><span class="sxs-lookup"><span data-stu-id="8fe90-130">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="8fe90-131">type</span><span class="sxs-lookup"><span data-stu-id="8fe90-131">type</span></span> | <span data-ttu-id="8fe90-132">La propriété de type doit être définie sur **AzureSearch**.</span><span class="sxs-lookup"><span data-stu-id="8fe90-132">The type property must be set to: **AzureSearch**.</span></span> | <span data-ttu-id="8fe90-133">Oui</span><span class="sxs-lookup"><span data-stu-id="8fe90-133">Yes</span></span> |
| <span data-ttu-id="8fe90-134">URL</span><span class="sxs-lookup"><span data-stu-id="8fe90-134">url</span></span> | <span data-ttu-id="8fe90-135">URL du service Recherche Azure.</span><span class="sxs-lookup"><span data-stu-id="8fe90-135">URL for the Azure Search service.</span></span> | <span data-ttu-id="8fe90-136">Oui</span><span class="sxs-lookup"><span data-stu-id="8fe90-136">Yes</span></span> |
| <span data-ttu-id="8fe90-137">key</span><span class="sxs-lookup"><span data-stu-id="8fe90-137">key</span></span> | <span data-ttu-id="8fe90-138">Clé d’administration du service Recherche Azure.</span><span class="sxs-lookup"><span data-stu-id="8fe90-138">Admin key for the Azure Search service.</span></span> | <span data-ttu-id="8fe90-139">Oui</span><span class="sxs-lookup"><span data-stu-id="8fe90-139">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="8fe90-140">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="8fe90-140">Dataset properties</span></span>

<span data-ttu-id="8fe90-141">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md) .</span><span class="sxs-lookup"><span data-stu-id="8fe90-141">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="8fe90-142">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données.</span><span class="sxs-lookup"><span data-stu-id="8fe90-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span> <span data-ttu-id="8fe90-143">La section **typeProperties** est différente pour chaque type de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="8fe90-143">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="8fe90-144">La section typeProperties d’un jeu de données de type **AzureSearchIndex** comprend les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="8fe90-144">The typeProperties section for a dataset of the type **AzureSearchIndex** has the following properties:</span></span>

| <span data-ttu-id="8fe90-145">Propriété</span><span class="sxs-lookup"><span data-stu-id="8fe90-145">Property</span></span> | <span data-ttu-id="8fe90-146">Description</span><span class="sxs-lookup"><span data-stu-id="8fe90-146">Description</span></span> | <span data-ttu-id="8fe90-147">Requis</span><span class="sxs-lookup"><span data-stu-id="8fe90-147">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="8fe90-148">type</span><span class="sxs-lookup"><span data-stu-id="8fe90-148">type</span></span> | <span data-ttu-id="8fe90-149">La propriété de type doit être définie sur **AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="8fe90-149">The type property must be set to **AzureSearchIndex**.</span></span>| <span data-ttu-id="8fe90-150">Oui</span><span class="sxs-lookup"><span data-stu-id="8fe90-150">Yes</span></span> |
| <span data-ttu-id="8fe90-151">indexName</span><span class="sxs-lookup"><span data-stu-id="8fe90-151">indexName</span></span> | <span data-ttu-id="8fe90-152">Nom de l’index Recherche Azure.</span><span class="sxs-lookup"><span data-stu-id="8fe90-152">Name of the Azure Search index.</span></span> <span data-ttu-id="8fe90-153">Data Factory ne crée pas l’index.</span><span class="sxs-lookup"><span data-stu-id="8fe90-153">Data Factory does not create the index.</span></span> <span data-ttu-id="8fe90-154">L’index doit exister dans Recherche Azure.</span><span class="sxs-lookup"><span data-stu-id="8fe90-154">The index must exist in Azure Search.</span></span> | <span data-ttu-id="8fe90-155">Oui</span><span class="sxs-lookup"><span data-stu-id="8fe90-155">Yes</span></span> |


## <a name="copy-activity-properties"></a><span data-ttu-id="8fe90-156">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="8fe90-156">Copy activity properties</span></span>
<span data-ttu-id="8fe90-157">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="8fe90-157">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="8fe90-158">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d’activité.</span><span class="sxs-lookup"><span data-stu-id="8fe90-158">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span></span> <span data-ttu-id="8fe90-159">En revanche, les propriétés disponibles dans la section typeProperties varient pour chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="8fe90-159">Whereas, properties available in the typeProperties section vary with each activity type.</span></span> <span data-ttu-id="8fe90-160">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="8fe90-160">For Copy Activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="8fe90-161">Pour l’activité de copie, quand la source est de type **AzureSearchIndexSink**, les propriétés suivantes sont disponibles dans la section typeProperties :</span><span class="sxs-lookup"><span data-stu-id="8fe90-161">For Copy Activity, when the sink is of the type **AzureSearchIndexSink**, the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="8fe90-162">Propriété</span><span class="sxs-lookup"><span data-stu-id="8fe90-162">Property</span></span> | <span data-ttu-id="8fe90-163">Description</span><span class="sxs-lookup"><span data-stu-id="8fe90-163">Description</span></span> | <span data-ttu-id="8fe90-164">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="8fe90-164">Allowed values</span></span> | <span data-ttu-id="8fe90-165">Requis</span><span class="sxs-lookup"><span data-stu-id="8fe90-165">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="8fe90-166">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="8fe90-166">WriteBehavior</span></span> | <span data-ttu-id="8fe90-167">Indique s’il convient de procéder à une fusion ou à un remplacement lorsqu’un document existe déjà dans l’index.</span><span class="sxs-lookup"><span data-stu-id="8fe90-167">Specifies whether to merge or replace when a document already exists in the index.</span></span> <span data-ttu-id="8fe90-168">Voir la [propriété WriteBehavior](#writebehavior-property).</span><span class="sxs-lookup"><span data-stu-id="8fe90-168">See the [WriteBehavior property](#writebehavior-property).</span></span>| <span data-ttu-id="8fe90-169">Merge (par défaut)</span><span class="sxs-lookup"><span data-stu-id="8fe90-169">Merge (default)</span></span><br/><span data-ttu-id="8fe90-170">Télécharger</span><span class="sxs-lookup"><span data-stu-id="8fe90-170">Upload</span></span>| <span data-ttu-id="8fe90-171">Non</span><span class="sxs-lookup"><span data-stu-id="8fe90-171">No</span></span> |
| <span data-ttu-id="8fe90-172">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="8fe90-172">WriteBatchSize</span></span> | <span data-ttu-id="8fe90-173">Charge des données dans l’index Recherche Azure lorsque la taille du tampon atteint writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="8fe90-173">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="8fe90-174">Pour plus d’informations, voir la [propriété WriteBatchSize](#writebatchsize-property).</span><span class="sxs-lookup"><span data-stu-id="8fe90-174">See the [WriteBatchSize property](#writebatchsize-property) for details.</span></span> | <span data-ttu-id="8fe90-175">1 à 1 000.</span><span class="sxs-lookup"><span data-stu-id="8fe90-175">1 to 1,000.</span></span> <span data-ttu-id="8fe90-176">Valeur par défaut : 1 000.</span><span class="sxs-lookup"><span data-stu-id="8fe90-176">Default value is 1000.</span></span> | <span data-ttu-id="8fe90-177">Non</span><span class="sxs-lookup"><span data-stu-id="8fe90-177">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="8fe90-178">Propriété WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="8fe90-178">WriteBehavior property</span></span>
<span data-ttu-id="8fe90-179">AzureSearchSink effectue une opération d’upsert lors de l’écriture des données.</span><span class="sxs-lookup"><span data-stu-id="8fe90-179">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="8fe90-180">En d’autres termes, lorsque vous écrivez un document, si la clé du document existe déjà dans l’index Recherche Azure, Recherche Azure met à jour le document existant au lieu de lever une exception de conflit.</span><span class="sxs-lookup"><span data-stu-id="8fe90-180">In other words, when writing a document, if the document key already exists in the Azure Search index, Azure Search updates the existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="8fe90-181">AzureSearchSink fournit les deux comportements upsert suivants (en utilisant le Kit de développement logiciel (SDK) AzureSearch) :</span><span class="sxs-lookup"><span data-stu-id="8fe90-181">The AzureSearchSink provides the following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="8fe90-182">**Fusion** : combine toutes les colonnes du nouveau document avec celles du document existant.</span><span class="sxs-lookup"><span data-stu-id="8fe90-182">**Merge**: combine all the columns in the new document with the existing one.</span></span> <span data-ttu-id="8fe90-183">Pour les colonnes ayant une valeur Null dans le nouveau document, la valeur de celles du document existant est conservée.</span><span class="sxs-lookup"><span data-stu-id="8fe90-183">For columns with null value in the new document, the value in the existing one is preserved.</span></span>
- <span data-ttu-id="8fe90-184">**Chargement** : le nouveau document remplace l’ancien.</span><span class="sxs-lookup"><span data-stu-id="8fe90-184">**Upload**: The new document replaces the existing one.</span></span> <span data-ttu-id="8fe90-185">Pour les colonnes qui ne sont pas spécifiées dans le nouveau document, la valeur est définie sur Null qu’il existe ou non une valeur autre que Null dans le document existant.</span><span class="sxs-lookup"><span data-stu-id="8fe90-185">For columns not specified in the new document, the value is set to null whether there is a non-null value in the existing document or not.</span></span>

<span data-ttu-id="8fe90-186">**Fusion** est le comportement par défaut.</span><span class="sxs-lookup"><span data-stu-id="8fe90-186">The default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="8fe90-187">Propriété WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="8fe90-187">WriteBatchSize Property</span></span>
<span data-ttu-id="8fe90-188">Le service Recherche Azure prend en charge l’écriture de documents sous forme d’un lot.</span><span class="sxs-lookup"><span data-stu-id="8fe90-188">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="8fe90-189">Un lot peut contenir 1 à 1 000 actions.</span><span class="sxs-lookup"><span data-stu-id="8fe90-189">A batch can contain 1 to 1,000 Actions.</span></span> <span data-ttu-id="8fe90-190">Une action gère un document pour effectuer l’opération de chargement/fusion.</span><span class="sxs-lookup"><span data-stu-id="8fe90-190">An action handles one document to perform the upload/merge operation.</span></span>

### <a name="data-type-support"></a><span data-ttu-id="8fe90-191">Prise en charge des types de données</span><span class="sxs-lookup"><span data-stu-id="8fe90-191">Data type support</span></span>
<span data-ttu-id="8fe90-192">Le tableau suivant indique si un type de données Recherche Azure est pris en charge ou non.</span><span class="sxs-lookup"><span data-stu-id="8fe90-192">The following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="8fe90-193">Type de données Recherche Azure</span><span class="sxs-lookup"><span data-stu-id="8fe90-193">Azure Search data type</span></span> | <span data-ttu-id="8fe90-194">Pris en charge dans le récepteur de l’index Recherche Azure</span><span class="sxs-lookup"><span data-stu-id="8fe90-194">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="8fe90-195">String</span><span class="sxs-lookup"><span data-stu-id="8fe90-195">String</span></span> | <span data-ttu-id="8fe90-196">O</span><span class="sxs-lookup"><span data-stu-id="8fe90-196">Y</span></span> |
| <span data-ttu-id="8fe90-197">Int32</span><span class="sxs-lookup"><span data-stu-id="8fe90-197">Int32</span></span> | <span data-ttu-id="8fe90-198">O</span><span class="sxs-lookup"><span data-stu-id="8fe90-198">Y</span></span> |
| <span data-ttu-id="8fe90-199">Int64</span><span class="sxs-lookup"><span data-stu-id="8fe90-199">Int64</span></span> | <span data-ttu-id="8fe90-200">O</span><span class="sxs-lookup"><span data-stu-id="8fe90-200">Y</span></span> |
| <span data-ttu-id="8fe90-201">Double</span><span class="sxs-lookup"><span data-stu-id="8fe90-201">Double</span></span> | <span data-ttu-id="8fe90-202">O</span><span class="sxs-lookup"><span data-stu-id="8fe90-202">Y</span></span> |
| <span data-ttu-id="8fe90-203">Booléen</span><span class="sxs-lookup"><span data-stu-id="8fe90-203">Boolean</span></span> | <span data-ttu-id="8fe90-204">O</span><span class="sxs-lookup"><span data-stu-id="8fe90-204">Y</span></span> |
| <span data-ttu-id="8fe90-205">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="8fe90-205">DataTimeOffset</span></span> | <span data-ttu-id="8fe90-206">O</span><span class="sxs-lookup"><span data-stu-id="8fe90-206">Y</span></span> |
| <span data-ttu-id="8fe90-207">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="8fe90-207">String Array</span></span> | <span data-ttu-id="8fe90-208">N</span><span class="sxs-lookup"><span data-stu-id="8fe90-208">N</span></span> |
| <span data-ttu-id="8fe90-209">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="8fe90-209">GeographyPoint</span></span> | <span data-ttu-id="8fe90-210">N</span><span class="sxs-lookup"><span data-stu-id="8fe90-210">N</span></span> |

## <a name="json-example-copy-data-from-on-premises-sql-server-to-azure-search-index"></a><span data-ttu-id="8fe90-211">Exemple JSON : copier des données depuis un serveur SQL Server local vers un index Recherche Azure</span><span class="sxs-lookup"><span data-stu-id="8fe90-211">JSON example: Copy data from on-premises SQL Server to Azure Search index</span></span>

<span data-ttu-id="8fe90-212">L’exemple suivant montre :</span><span class="sxs-lookup"><span data-stu-id="8fe90-212">The following sample shows:</span></span>

1.  <span data-ttu-id="8fe90-213">Un service lié de type [AzureSearch](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8fe90-213">A linked service of type [AzureSearch](#linked-service-properties).</span></span>
2.  <span data-ttu-id="8fe90-214">Service lié de type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8fe90-214">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span></span>
3.  <span data-ttu-id="8fe90-215">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8fe90-215">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
4.  <span data-ttu-id="8fe90-216">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureSearchIndex](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8fe90-216">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span></span>
4.  <span data-ttu-id="8fe90-217">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) et [AzureSearchIndexSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8fe90-217">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span></span>

<span data-ttu-id="8fe90-218">L’exemple copie toutes les heures les données de série chronologique d’une base de données SQL Server locale vers un index Recherche Azure.</span><span class="sxs-lookup"><span data-stu-id="8fe90-218">The sample copies time-series data from an on-premises SQL Server database to an Azure Search index hourly.</span></span> <span data-ttu-id="8fe90-219">Les propriétés JSON utilisées dans cet exemple sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="8fe90-219">The JSON properties used in this sample are described in sections following the samples.</span></span>

<span data-ttu-id="8fe90-220">Dans un premier temps, configurez la passerelle de gestion des données sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="8fe90-220">As a first step, setup the data management gateway on your on-premises machine.</span></span> <span data-ttu-id="8fe90-221">Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="8fe90-221">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="8fe90-222">**Service lié Recherche Azure :**</span><span class="sxs-lookup"><span data-stu-id="8fe90-222">**Azure Search linked service:**</span></span>

```JSON
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="8fe90-223">**Service SQL Server lié**</span><span class="sxs-lookup"><span data-stu-id="8fe90-223">**SQL Server linked service**</span></span>

```JSON
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```

<span data-ttu-id="8fe90-224">**Jeu de données d’entrée de SQL Server**</span><span class="sxs-lookup"><span data-stu-id="8fe90-224">**SQL Server input dataset**</span></span>

<span data-ttu-id="8fe90-225">L’exemple suppose que vous avez créé une table « MyTable » dans SQL Server et qu’elle contient une colonne appelée « timestampcolumn » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="8fe90-225">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="8fe90-226">Vous pouvez interroger plusieurs tables au sein d’une même base de données en utilisant un jeu de données unique, mais une seule table doit être utilisée pour la propriété typeProperty tableName du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="8fe90-226">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="8fe90-227">La définition de external sur true informe le service Data Factory que le jeu de données est externe à la Data Factory et non produite par une activité dans la Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8fe90-227">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "SqlServerDataset",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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

<span data-ttu-id="8fe90-228">**Jeu de données de sortie Recherche Azure :**</span><span class="sxs-lookup"><span data-stu-id="8fe90-228">**Azure Search output dataset:**</span></span>

<span data-ttu-id="8fe90-229">L’exemple copie des données vers un index Recherche Azure nommé **produits**.</span><span class="sxs-lookup"><span data-stu-id="8fe90-229">The sample copies data to an Azure Search index named **products**.</span></span> <span data-ttu-id="8fe90-230">Data Factory ne crée pas l’index.</span><span class="sxs-lookup"><span data-stu-id="8fe90-230">Data Factory does not create the index.</span></span> <span data-ttu-id="8fe90-231">Pour tester l’exemple, créez un index portant ce nom.</span><span class="sxs-lookup"><span data-stu-id="8fe90-231">To test the sample, create an index with this name.</span></span> <span data-ttu-id="8fe90-232">Créez l’index Recherche Azure avec le même nombre de colonnes que dans le jeu de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="8fe90-232">Create the Azure Search index with the same number of columns as in the input dataset.</span></span> <span data-ttu-id="8fe90-233">De nouvelles entrées sont ajoutées toutes les heures à l’index Recherche Azure.</span><span class="sxs-lookup"><span data-stu-id="8fe90-233">New entries are added to the Azure Search index every hour.</span></span>

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

<span data-ttu-id="8fe90-234">**Activité de copie dans un pipeline avec une source SQL et un récepteur de l’index Recherche Azure :**</span><span class="sxs-lookup"><span data-stu-id="8fe90-234">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span></span>

<span data-ttu-id="8fe90-235">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="8fe90-235">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="8fe90-236">Dans la définition JSON du pipeline, le type **source** est défini sur **SqlSource** et le type **sink** est défini sur **AzureSearchIndexSink**.</span><span class="sxs-lookup"><span data-stu-id="8fe90-236">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **AzureSearchIndexSink**.</span></span> <span data-ttu-id="8fe90-237">La requête SQL spécifiée pour la propriété **SqlReaderQuery** sélectionne les données de la dernière heure à copier.</span><span class="sxs-lookup"><span data-stu-id="8fe90-237">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "AzureSearchIndexSink"
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

<span data-ttu-id="8fe90-238">Si vous copiez des données d’un magasin de données cloud vers Recherche Azure, la propriété `executionLocation` est requise.</span><span class="sxs-lookup"><span data-stu-id="8fe90-238">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="8fe90-239">À titre d’exemple, l’extrait de code JSON suivant montre la modification nécessaire dans `typeProperties` pour l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="8fe90-239">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="8fe90-240">Consultez la section [Copier des données entre des banques de données cloud](data-factory-data-movement-activities.md#global) pour plus d’informations et les valeurs prises en charge.</span><span class="sxs-lookup"><span data-stu-id="8fe90-240">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a><span data-ttu-id="8fe90-241">Copier à partir d’une source cloud</span><span class="sxs-lookup"><span data-stu-id="8fe90-241">Copy from a cloud source</span></span>
<span data-ttu-id="8fe90-242">Si vous copiez des données d’un magasin de données cloud vers Recherche Azure, la propriété `executionLocation` est requise.</span><span class="sxs-lookup"><span data-stu-id="8fe90-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="8fe90-243">À titre d’exemple, l’extrait de code JSON suivant montre la modification nécessaire dans `typeProperties` pour l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="8fe90-243">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="8fe90-244">Consultez la section [Copier des données entre des banques de données cloud](data-factory-data-movement-activities.md#global) pour plus d’informations et les valeurs prises en charge.</span><span class="sxs-lookup"><span data-stu-id="8fe90-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

<span data-ttu-id="8fe90-245">Vous pouvez également mapper les colonnes du jeu de données source aux colonnes du jeu de données récepteur dans la définition de l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="8fe90-245">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="8fe90-246">Pour plus d’informations, consultez [Mappage de colonnes de jeux de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="8fe90-246">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="8fe90-247">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="8fe90-247">Performance and tuning</span></span>  
<span data-ttu-id="8fe90-248">Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) et les différentes manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="8fe90-248">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fe90-249">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8fe90-249">Next steps</span></span>
<span data-ttu-id="8fe90-250">Consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="8fe90-250">See the following articles:</span></span>

* <span data-ttu-id="8fe90-251">[Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec Activité de copie.</span><span class="sxs-lookup"><span data-stu-id="8fe90-251">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
