---
title: "index de tooSearch aaaPush données à l’aide de Data Factory | Documents Microsoft"
description: "En savoir plus sur la façon de toopush données tooAzure Index de recherche à l’aide d’Azure Data Factory."
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
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a><span data-ttu-id="4a824-103">Push index Azure Search de tooan données à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="4a824-103">Push data tooan Azure Search index by using Azure Data Factory</span></span>
<span data-ttu-id="4a824-104">Cet article décrit comment les données de toopush toouse hello activité de copie à partir des données sources pris en charge stocker les index de recherche tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4a824-104">This article describes how toouse hello Copy Activity toopush data from a supported source data store tooAzure Search index.</span></span> <span data-ttu-id="4a824-105">Magasins de données source pris en charge sont répertoriés dans la colonne de Source de hello Hello [prise en charge des sources et récepteurs](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="4a824-105">Supported source data stores are listed in hello Source column of hello [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="4a824-106">Cet article s’appuie sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie et de combinaisons de magasin de données pris en charge.</span><span class="sxs-lookup"><span data-stu-id="4a824-106">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="4a824-107">Activation de la connectivité</span><span class="sxs-lookup"><span data-stu-id="4a824-107">Enabling connectivity</span></span>
<span data-ttu-id="4a824-108">banque de données locale tooan de connexion de tooallow service Data Factory, vous installez la passerelle de gestion des données dans votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="4a824-108">tooallow Data Factory service connect tooan on-premises data store, you install Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="4a824-109">Vous pouvez installer la passerelle sur hello même ordinateur qui héberge la source de données hello stocker ou sur un tooavoid machine distincte qui entrent en concurrence pour les ressources avec des données hello magasin.</span><span class="sxs-lookup"><span data-stu-id="4a824-109">You can install gateway on hello same machine that hosts hello source data store or on a separate machine tooavoid competing for resources with hello data store.</span></span>

<span data-ttu-id="4a824-110">Passerelle de gestion des données se connecte à des services de toocloud de sources de données sur site de manière sécurisée et gérée.</span><span class="sxs-lookup"><span data-stu-id="4a824-110">Data Management Gateway connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="4a824-111">Pour plus d’informations sur la passerelle de gestion de données, consultez l’article [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="4a824-111">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="4a824-112">Prise en main</span><span class="sxs-lookup"><span data-stu-id="4a824-112">Getting started</span></span>
<span data-ttu-id="4a824-113">Vous pouvez créer un pipeline avec une activité de copie qui envoie des données à partir d’un index de recherche source données magasin tooAzure à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="4a824-113">You can create a pipeline with a copy activity that pushes data from a source data store tooAzure Search index by using different tools/APIs.</span></span>

<span data-ttu-id="4a824-114">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="4a824-114">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="4a824-115">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="4a824-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="4a824-116">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="4a824-116">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="4a824-117">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="4a824-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="4a824-118">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="4a824-118">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="4a824-119">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="4a824-119">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="4a824-120">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="4a824-120">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="4a824-121">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="4a824-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="4a824-122">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="4a824-122">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="4a824-123">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="4a824-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="4a824-124">Pour voir un exemple avec des définitions pour les entités de fabrique de données qui sont des index de recherche tooAzure toocopy utilisé données JSON, [exemple de JSON : copier des données à partir de l’index de recherche local SQL Server tooAzure](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="4a824-124">For a sample with JSON definitions for Data Factory entities that are used toocopy data tooAzure Search index, see [JSON example: Copy data from on-premises SQL Server tooAzure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span></span> 

<span data-ttu-id="4a824-125">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifique tooAzure Index de recherche :</span><span class="sxs-lookup"><span data-stu-id="4a824-125">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Search Index:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="4a824-126">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="4a824-126">Linked service properties</span></span>

<span data-ttu-id="4a824-127">Hello tableau suivant fournit des descriptions pour les éléments JSON toohello spécifique au service Azure Search est lié.</span><span class="sxs-lookup"><span data-stu-id="4a824-127">hello following table provides descriptions for JSON elements that are specific toohello Azure Search linked service.</span></span>

| <span data-ttu-id="4a824-128">Propriété</span><span class="sxs-lookup"><span data-stu-id="4a824-128">Property</span></span> | <span data-ttu-id="4a824-129">Description</span><span class="sxs-lookup"><span data-stu-id="4a824-129">Description</span></span> | <span data-ttu-id="4a824-130">Requis</span><span class="sxs-lookup"><span data-stu-id="4a824-130">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="4a824-131">type</span><span class="sxs-lookup"><span data-stu-id="4a824-131">type</span></span> | <span data-ttu-id="4a824-132">propriété de type Hello doit indiquer : **AzureSearch**.</span><span class="sxs-lookup"><span data-stu-id="4a824-132">hello type property must be set to: **AzureSearch**.</span></span> | <span data-ttu-id="4a824-133">Oui</span><span class="sxs-lookup"><span data-stu-id="4a824-133">Yes</span></span> |
| <span data-ttu-id="4a824-134">url</span><span class="sxs-lookup"><span data-stu-id="4a824-134">url</span></span> | <span data-ttu-id="4a824-135">URL de hello service Azure Search.</span><span class="sxs-lookup"><span data-stu-id="4a824-135">URL for hello Azure Search service.</span></span> | <span data-ttu-id="4a824-136">Oui</span><span class="sxs-lookup"><span data-stu-id="4a824-136">Yes</span></span> |
| <span data-ttu-id="4a824-137">key</span><span class="sxs-lookup"><span data-stu-id="4a824-137">key</span></span> | <span data-ttu-id="4a824-138">Clé d’administration pour hello service Azure Search.</span><span class="sxs-lookup"><span data-stu-id="4a824-138">Admin key for hello Azure Search service.</span></span> | <span data-ttu-id="4a824-139">Oui</span><span class="sxs-lookup"><span data-stu-id="4a824-139">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="4a824-140">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="4a824-140">Dataset properties</span></span>

<span data-ttu-id="4a824-141">Pour obtenir une liste complète des sections et les propriétés qui sont disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="4a824-141">For a full list of sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="4a824-142">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données.</span><span class="sxs-lookup"><span data-stu-id="4a824-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span> <span data-ttu-id="4a824-143">Hello **typeProperties** section est différente pour chaque type de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="4a824-143">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="4a824-144">Hello typeProperties section pour un jeu de données de type de hello **AzureSearchIndex** a hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="4a824-144">hello typeProperties section for a dataset of hello type **AzureSearchIndex** has hello following properties:</span></span>

| <span data-ttu-id="4a824-145">Propriété</span><span class="sxs-lookup"><span data-stu-id="4a824-145">Property</span></span> | <span data-ttu-id="4a824-146">Description</span><span class="sxs-lookup"><span data-stu-id="4a824-146">Description</span></span> | <span data-ttu-id="4a824-147">Requis</span><span class="sxs-lookup"><span data-stu-id="4a824-147">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="4a824-148">type</span><span class="sxs-lookup"><span data-stu-id="4a824-148">type</span></span> | <span data-ttu-id="4a824-149">propriété de type Hello doit être définie trop**AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="4a824-149">hello type property must be set too**AzureSearchIndex**.</span></span>| <span data-ttu-id="4a824-150">Oui</span><span class="sxs-lookup"><span data-stu-id="4a824-150">Yes</span></span> |
| <span data-ttu-id="4a824-151">indexName</span><span class="sxs-lookup"><span data-stu-id="4a824-151">indexName</span></span> | <span data-ttu-id="4a824-152">Nom de l’index de recherche de Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4a824-152">Name of hello Azure Search index.</span></span> <span data-ttu-id="4a824-153">Fabrique de données ne crée pas d’index de hello.</span><span class="sxs-lookup"><span data-stu-id="4a824-153">Data Factory does not create hello index.</span></span> <span data-ttu-id="4a824-154">index de Hello doit exister dans Azure Search.</span><span class="sxs-lookup"><span data-stu-id="4a824-154">hello index must exist in Azure Search.</span></span> | <span data-ttu-id="4a824-155">Oui</span><span class="sxs-lookup"><span data-stu-id="4a824-155">Yes</span></span> |


## <a name="copy-activity-properties"></a><span data-ttu-id="4a824-156">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="4a824-156">Copy activity properties</span></span>
<span data-ttu-id="4a824-157">Pour obtenir une liste complète des sections et des propriétés qui sont disponibles pour la définition d’activités, consultez hello [création de pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="4a824-157">For a full list of sections and properties that are available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="4a824-158">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d’activité.</span><span class="sxs-lookup"><span data-stu-id="4a824-158">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span></span> <span data-ttu-id="4a824-159">Alors que les propriétés disponibles dans la section de typeProperties hello varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="4a824-159">Whereas, properties available in hello typeProperties section vary with each activity type.</span></span> <span data-ttu-id="4a824-160">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="4a824-160">For Copy Activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="4a824-161">Pour l’activité de copie, lorsque le récepteur de hello est de type de hello **AzureSearchIndexSink**, hello propriétés suivantes est disponible dans la section de typeProperties :</span><span class="sxs-lookup"><span data-stu-id="4a824-161">For Copy Activity, when hello sink is of hello type **AzureSearchIndexSink**, hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="4a824-162">Propriété</span><span class="sxs-lookup"><span data-stu-id="4a824-162">Property</span></span> | <span data-ttu-id="4a824-163">Description</span><span class="sxs-lookup"><span data-stu-id="4a824-163">Description</span></span> | <span data-ttu-id="4a824-164">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="4a824-164">Allowed values</span></span> | <span data-ttu-id="4a824-165">Requis</span><span class="sxs-lookup"><span data-stu-id="4a824-165">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="4a824-166">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="4a824-166">WriteBehavior</span></span> | <span data-ttu-id="4a824-167">Spécifie si toomerge ou remplacer un document existe déjà dans l’index de hello.</span><span class="sxs-lookup"><span data-stu-id="4a824-167">Specifies whether toomerge or replace when a document already exists in hello index.</span></span> <span data-ttu-id="4a824-168">Consultez hello [WriteBehavior propriété](#writebehavior-property).</span><span class="sxs-lookup"><span data-stu-id="4a824-168">See hello [WriteBehavior property](#writebehavior-property).</span></span>| <span data-ttu-id="4a824-169">Merge (par défaut)</span><span class="sxs-lookup"><span data-stu-id="4a824-169">Merge (default)</span></span><br/><span data-ttu-id="4a824-170">Télécharger</span><span class="sxs-lookup"><span data-stu-id="4a824-170">Upload</span></span>| <span data-ttu-id="4a824-171">Non</span><span class="sxs-lookup"><span data-stu-id="4a824-171">No</span></span> |
| <span data-ttu-id="4a824-172">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="4a824-172">WriteBatchSize</span></span> | <span data-ttu-id="4a824-173">Télécharge des données dans l’index de recherche de Azure hello lorsque la taille de mémoire tampon de hello atteint la valeur writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="4a824-173">Uploads data into hello Azure Search index when hello buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="4a824-174">Consultez hello [valeur WriteBatchSize propriété](#writebatchsize-property) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="4a824-174">See hello [WriteBatchSize property](#writebatchsize-property) for details.</span></span> | <span data-ttu-id="4a824-175">1 too1, 000.</span><span class="sxs-lookup"><span data-stu-id="4a824-175">1 too1,000.</span></span> <span data-ttu-id="4a824-176">Valeur par défaut : 1 000.</span><span class="sxs-lookup"><span data-stu-id="4a824-176">Default value is 1000.</span></span> | <span data-ttu-id="4a824-177">Non</span><span class="sxs-lookup"><span data-stu-id="4a824-177">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="4a824-178">Propriété WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="4a824-178">WriteBehavior property</span></span>
<span data-ttu-id="4a824-179">AzureSearchSink effectue une opération d’upsert lors de l’écriture des données.</span><span class="sxs-lookup"><span data-stu-id="4a824-179">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="4a824-180">En d’autres termes, lorsque vous écrivez un document, si la clé de document hello existe déjà dans l’index de recherche de Azure hello, Azure Search met à jour les documents existants hello plutôt que de lever une exception de conflit.</span><span class="sxs-lookup"><span data-stu-id="4a824-180">In other words, when writing a document, if hello document key already exists in hello Azure Search index, Azure Search updates hello existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="4a824-181">Hello AzureSearchSink fournit hello suivant deux comportements upsert (en utilisant AzureSearch SDK) :</span><span class="sxs-lookup"><span data-stu-id="4a824-181">hello AzureSearchSink provides hello following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="4a824-182">**Fusion**: associent toutes les colonnes hello dans le nouveau document de hello hello une existante.</span><span class="sxs-lookup"><span data-stu-id="4a824-182">**Merge**: combine all hello columns in hello new document with hello existing one.</span></span> <span data-ttu-id="4a824-183">Pour les colonnes avec la valeur null dans le nouveau document de hello, la valeur de hello Bonjour une existante est conservée.</span><span class="sxs-lookup"><span data-stu-id="4a824-183">For columns with null value in hello new document, hello value in hello existing one is preserved.</span></span>
- <span data-ttu-id="4a824-184">**Télécharger**: remplace de document nouveau hello hello existant.</span><span class="sxs-lookup"><span data-stu-id="4a824-184">**Upload**: hello new document replaces hello existing one.</span></span> <span data-ttu-id="4a824-185">Pour les colonnes non spécifiées dans le nouveau document de hello, hello valeur toonull s’il existe une valeur non null dans un document existant de hello ou non.</span><span class="sxs-lookup"><span data-stu-id="4a824-185">For columns not specified in hello new document, hello value is set toonull whether there is a non-null value in hello existing document or not.</span></span>

<span data-ttu-id="4a824-186">comportement par défaut de Hello est **fusion**.</span><span class="sxs-lookup"><span data-stu-id="4a824-186">hello default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="4a824-187">Propriété WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="4a824-187">WriteBatchSize Property</span></span>
<span data-ttu-id="4a824-188">Le service Recherche Azure prend en charge l’écriture de documents sous forme d’un lot.</span><span class="sxs-lookup"><span data-stu-id="4a824-188">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="4a824-189">Un lot peut contenir 1 too1, 000 Actions.</span><span class="sxs-lookup"><span data-stu-id="4a824-189">A batch can contain 1 too1,000 Actions.</span></span> <span data-ttu-id="4a824-190">Une action gère une opération de téléchargement et de fusion hello tooperform document.</span><span class="sxs-lookup"><span data-stu-id="4a824-190">An action handles one document tooperform hello upload/merge operation.</span></span>

### <a name="data-type-support"></a><span data-ttu-id="4a824-191">Prise en charge des types de données</span><span class="sxs-lookup"><span data-stu-id="4a824-191">Data type support</span></span>
<span data-ttu-id="4a824-192">Hello tableau suivant indique si un type de données Azure Search est pris en charge ou non.</span><span class="sxs-lookup"><span data-stu-id="4a824-192">hello following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="4a824-193">Type de données Recherche Azure</span><span class="sxs-lookup"><span data-stu-id="4a824-193">Azure Search data type</span></span> | <span data-ttu-id="4a824-194">Pris en charge dans le récepteur de l’index Recherche Azure</span><span class="sxs-lookup"><span data-stu-id="4a824-194">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="4a824-195">String</span><span class="sxs-lookup"><span data-stu-id="4a824-195">String</span></span> | <span data-ttu-id="4a824-196">O</span><span class="sxs-lookup"><span data-stu-id="4a824-196">Y</span></span> |
| <span data-ttu-id="4a824-197">Int32</span><span class="sxs-lookup"><span data-stu-id="4a824-197">Int32</span></span> | <span data-ttu-id="4a824-198">O</span><span class="sxs-lookup"><span data-stu-id="4a824-198">Y</span></span> |
| <span data-ttu-id="4a824-199">Int64</span><span class="sxs-lookup"><span data-stu-id="4a824-199">Int64</span></span> | <span data-ttu-id="4a824-200">O</span><span class="sxs-lookup"><span data-stu-id="4a824-200">Y</span></span> |
| <span data-ttu-id="4a824-201">Double</span><span class="sxs-lookup"><span data-stu-id="4a824-201">Double</span></span> | <span data-ttu-id="4a824-202">O</span><span class="sxs-lookup"><span data-stu-id="4a824-202">Y</span></span> |
| <span data-ttu-id="4a824-203">Booléen</span><span class="sxs-lookup"><span data-stu-id="4a824-203">Boolean</span></span> | <span data-ttu-id="4a824-204">O</span><span class="sxs-lookup"><span data-stu-id="4a824-204">Y</span></span> |
| <span data-ttu-id="4a824-205">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="4a824-205">DataTimeOffset</span></span> | <span data-ttu-id="4a824-206">O</span><span class="sxs-lookup"><span data-stu-id="4a824-206">Y</span></span> |
| <span data-ttu-id="4a824-207">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="4a824-207">String Array</span></span> | <span data-ttu-id="4a824-208">N</span><span class="sxs-lookup"><span data-stu-id="4a824-208">N</span></span> |
| <span data-ttu-id="4a824-209">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="4a824-209">GeographyPoint</span></span> | <span data-ttu-id="4a824-210">N</span><span class="sxs-lookup"><span data-stu-id="4a824-210">N</span></span> |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a><span data-ttu-id="4a824-211">Exemple de JSON : copier des données à partir de l’index de recherche tooAzure local SQL Server</span><span class="sxs-lookup"><span data-stu-id="4a824-211">JSON example: Copy data from on-premises SQL Server tooAzure Search index</span></span>

<span data-ttu-id="4a824-212">Hello ci-dessous illustre d’exemple :</span><span class="sxs-lookup"><span data-stu-id="4a824-212">hello following sample shows:</span></span>

1.  <span data-ttu-id="4a824-213">Un service lié de type [AzureSearch](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4a824-213">A linked service of type [AzureSearch](#linked-service-properties).</span></span>
2.  <span data-ttu-id="4a824-214">Service lié de type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4a824-214">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span></span>
3.  <span data-ttu-id="4a824-215">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4a824-215">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
4.  <span data-ttu-id="4a824-216">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureSearchIndex](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4a824-216">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span></span>
4.  <span data-ttu-id="4a824-217">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) et [AzureSearchIndexSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="4a824-217">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span></span>

<span data-ttu-id="4a824-218">exemple Hello copie toutes les heures des données de séries chronologiques à partir d’un index Azure Search tooan de base de données de SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="4a824-218">hello sample copies time-series data from an on-premises SQL Server database tooan Azure Search index hourly.</span></span> <span data-ttu-id="4a824-219">les propriétés JSON Hello utilisées dans cet exemple sont décrites dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="4a824-219">hello JSON properties used in this sample are described in sections following hello samples.</span></span>

<span data-ttu-id="4a824-220">Dans un premier temps, le programme d’installation passerelle de gestion des données hello sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="4a824-220">As a first step, setup hello data management gateway on your on-premises machine.</span></span> <span data-ttu-id="4a824-221">instructions de Hello sont Bonjour [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="4a824-221">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="4a824-222">**Service lié Recherche Azure :**</span><span class="sxs-lookup"><span data-stu-id="4a824-222">**Azure Search linked service:**</span></span>

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

<span data-ttu-id="4a824-223">**Service SQL Server lié**</span><span class="sxs-lookup"><span data-stu-id="4a824-223">**SQL Server linked service**</span></span>

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

<span data-ttu-id="4a824-224">**Jeu de données d’entrée de SQL Server**</span><span class="sxs-lookup"><span data-stu-id="4a824-224">**SQL Server input dataset**</span></span>

<span data-ttu-id="4a824-225">exemple Hello suppose que vous avez créé une table « MyTable » dans SQL Server et il contienne une colonne appelée « timestampcolumn » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="4a824-225">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="4a824-226">Vous pouvez interroger sur plusieurs tables en hello même à l’aide d’un dataset unique, mais une seule table de base de données doit être utilisé pour typeProperty de tableName hello du groupe de données.</span><span class="sxs-lookup"><span data-stu-id="4a824-226">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="4a824-227">Paramètre « external » : « true » informe service Data Factory ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="4a824-227">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="4a824-228">**Jeu de données de sortie Recherche Azure :**</span><span class="sxs-lookup"><span data-stu-id="4a824-228">**Azure Search output dataset:**</span></span>

<span data-ttu-id="4a824-229">Hello exemple copies données tooan Azure Search index nommé **produits**.</span><span class="sxs-lookup"><span data-stu-id="4a824-229">hello sample copies data tooan Azure Search index named **products**.</span></span> <span data-ttu-id="4a824-230">Fabrique de données ne crée pas d’index de hello.</span><span class="sxs-lookup"><span data-stu-id="4a824-230">Data Factory does not create hello index.</span></span> <span data-ttu-id="4a824-231">tootest hello exemple, créer un index portant ce nom.</span><span class="sxs-lookup"><span data-stu-id="4a824-231">tootest hello sample, create an index with this name.</span></span> <span data-ttu-id="4a824-232">Créez l’index de recherche de Azure hello hello même nombre de colonnes dans le jeu de données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="4a824-232">Create hello Azure Search index with hello same number of columns as in hello input dataset.</span></span> <span data-ttu-id="4a824-233">Nouvelles entrées sont ajoutées à index Azure Search de toohello toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="4a824-233">New entries are added toohello Azure Search index every hour.</span></span>

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

<span data-ttu-id="4a824-234">**Activité de copie dans un pipeline avec une source SQL et un récepteur de l’index Recherche Azure :**</span><span class="sxs-lookup"><span data-stu-id="4a824-234">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span></span>

<span data-ttu-id="4a824-235">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="4a824-235">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="4a824-236">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**SqlSource** et **récepteur** type est défini trop**AzureSearchIndexSink**.</span><span class="sxs-lookup"><span data-stu-id="4a824-236">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**AzureSearchIndexSink**.</span></span> <span data-ttu-id="4a824-237">la requête SQL Hello spécifiée pour hello **SqlReaderQuery** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.</span><span class="sxs-lookup"><span data-stu-id="4a824-237">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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

<span data-ttu-id="4a824-238">Si vous copiez des données d’un magasin de données cloud vers Recherche Azure, la propriété `executionLocation` est requise.</span><span class="sxs-lookup"><span data-stu-id="4a824-238">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="4a824-239">Hello extrait de code JSON suivant montre les changements de hello requis dans l’activité de copie `typeProperties` comme exemple.</span><span class="sxs-lookup"><span data-stu-id="4a824-239">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="4a824-240">Consultez la section [Copier des données entre des banques de données cloud](data-factory-data-movement-activities.md#global) pour plus d’informations et les valeurs prises en charge.</span><span class="sxs-lookup"><span data-stu-id="4a824-240">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

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


## <a name="copy-from-a-cloud-source"></a><span data-ttu-id="4a824-241">Copier à partir d’une source cloud</span><span class="sxs-lookup"><span data-stu-id="4a824-241">Copy from a cloud source</span></span>
<span data-ttu-id="4a824-242">Si vous copiez des données d’un magasin de données cloud vers Recherche Azure, la propriété `executionLocation` est requise.</span><span class="sxs-lookup"><span data-stu-id="4a824-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="4a824-243">Hello extrait de code JSON suivant montre les changements de hello requis dans l’activité de copie `typeProperties` comme exemple.</span><span class="sxs-lookup"><span data-stu-id="4a824-243">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="4a824-244">Consultez la section [Copier des données entre des banques de données cloud](data-factory-data-movement-activities.md#global) pour plus d’informations et les valeurs prises en charge.</span><span class="sxs-lookup"><span data-stu-id="4a824-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

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

<span data-ttu-id="4a824-245">Vous pouvez également mapper des colonnes à partir de toocolumns du jeu de données source à partir de récepteur de jeu de données dans la définition d’activité de copie de hello.</span><span class="sxs-lookup"><span data-stu-id="4a824-245">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="4a824-246">Pour plus d’informations, consultez [Mappage de colonnes de jeux de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="4a824-246">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="4a824-247">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="4a824-247">Performance and tuning</span></span>  
<span data-ttu-id="4a824-248">Consultez hello [l’activité de copie guide des performances et paramétrage](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs impact sur les performances de transfert de données (activité de copie) et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="4a824-248">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a824-249">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4a824-249">Next steps</span></span>
<span data-ttu-id="4a824-250">Consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="4a824-250">See hello following articles:</span></span>

* <span data-ttu-id="4a824-251">[Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec Activité de copie.</span><span class="sxs-lookup"><span data-stu-id="4a824-251">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
