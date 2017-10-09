---
title: "aaaMove données PostgreSQL à partir de l’aide d’Azure Data Factory | Documents Microsoft"
description: "En savoir plus sur la façon de toomove les données à partir de la base de données PostgreSQL à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 888d9ebc-2500-4071-b6d1-0f6bd1b5997c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: ea384f4e06f7d7bedae2949e4ea727c8f8806614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a><span data-ttu-id="fee73-103">Déplacer des données depuis PostgreSQL à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="fee73-103">Move data from PostgreSQL using Azure Data Factory</span></span>
<span data-ttu-id="fee73-104">Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory à partir d’une base de données PostgreSQL locale.</span><span class="sxs-lookup"><span data-stu-id="fee73-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises PostgreSQL database.</span></span> <span data-ttu-id="fee73-105">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="fee73-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="fee73-106">Vous pouvez copier les données d’une banque de données locale PostgreSQL tooany pris en charge données magasin récepteur.</span><span class="sxs-lookup"><span data-stu-id="fee73-106">You can copy data from an on-premises PostgreSQL data store tooany supported sink data store.</span></span> <span data-ttu-id="fee73-107">Pour obtenir la liste des magasins de données pris en charge en tant que les récepteurs par l’activité de copie hello, consultez [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="fee73-107">For a list of data stores supported as sinks by hello copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="fee73-108">Fabrique de données actuellement prend en charge le déplacement de données à partir d’un PostgreSQL de base de données tooother des magasins de données, mais pas pour le déplacement des données à partir d’autres données stocke tooan base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="fee73-108">Data factory currently supports moving data from a PostgreSQL database tooother data stores, but not for moving data from other data stores tooan PostgreSQL database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fee73-109">configuration requise</span><span class="sxs-lookup"><span data-stu-id="fee73-109">prerequisites</span></span>

<span data-ttu-id="fee73-110">Service de fabrique de données prend en charge des sources de PostgreSQL tooon local qui se connecte à l’aide de la passerelle de gestion des données de hello.</span><span class="sxs-lookup"><span data-stu-id="fee73-110">Data Factory service supports connecting tooon-premises PostgreSQL sources using hello Data Management Gateway.</span></span> <span data-ttu-id="fee73-111">Consultez [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn l’article sur la passerelle de gestion des données et des instructions détaillées sur la configuration de passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="fee73-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="fee73-112">Passerelle est requise même si la base de données PostgreSQL hello est hébergé dans une machine virtuelle IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="fee73-112">Gateway is required even if hello PostgreSQL database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="fee73-113">Vous pouvez installer la passerelle sur hello même IaaS VM sous forme de données de hello stocker ou sur un ordinateur différent virtuel tant que passerelle de hello peuvent se connecter toohello de base de données.</span><span class="sxs-lookup"><span data-stu-id="fee73-113">You can install gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="fee73-114">Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.</span><span class="sxs-lookup"><span data-stu-id="fee73-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="fee73-115">Versions prises en charge et installation</span><span class="sxs-lookup"><span data-stu-id="fee73-115">Supported versions and installation</span></span>
<span data-ttu-id="fee73-116">Pour toohello tooconnect de passerelle de gestion des données de la base de données PostgreSQL, installez hello [Ngpsql du fournisseur de données pour PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 ou ci-dessus sur hello le même système que hello passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="fee73-116">For Data Management Gateway tooconnect toohello PostgreSQL Database, install hello [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="fee73-117">PostgreSQL version 7.4 et ultérieures est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="fee73-117">PostgreSQL version 7.4 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="fee73-118">Prise en main</span><span class="sxs-lookup"><span data-stu-id="fee73-118">Getting started</span></span>
<span data-ttu-id="fee73-119">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données PostgreSQL local à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="fee73-119">You can create a pipeline with a copy activity that moves data from an on-premises PostgreSQL data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="fee73-120">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="fee73-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="fee73-121">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="fee73-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="fee73-122">Vous pouvez également utiliser hello suivant outils toocreate un pipeline :</span><span class="sxs-lookup"><span data-stu-id="fee73-122">You can also use hello following tools toocreate a pipeline:</span></span> 
    - <span data-ttu-id="fee73-123">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="fee73-123">Azure portal</span></span>
    - <span data-ttu-id="fee73-124">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fee73-124">Visual Studio</span></span>
    - <span data-ttu-id="fee73-125">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fee73-125">Azure PowerShell</span></span>
    - <span data-ttu-id="fee73-126">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fee73-126">Azure Resource Manager template</span></span>
    - <span data-ttu-id="fee73-127">API .NET</span><span class="sxs-lookup"><span data-stu-id="fee73-127">.NET API</span></span>
    - <span data-ttu-id="fee73-128">API REST</span><span class="sxs-lookup"><span data-stu-id="fee73-128">REST API</span></span>

     <span data-ttu-id="fee73-129">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="fee73-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="fee73-130">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="fee73-130">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="fee73-131">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="fee73-131">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="fee73-132">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="fee73-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="fee73-133">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="fee73-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="fee73-134">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="fee73-134">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="fee73-135">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="fee73-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="fee73-136">Pour voir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données à partir d’une banque de données PostgreSQL locale, [exemple de JSON : copier des données PostgreSQL tooAzure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="fee73-136">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises PostgreSQL data store, see [JSON example: Copy data from PostgreSQL tooAzure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="fee73-137">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont le magasin de données PostgreSQL toodefine utilisé Data Factory entités tooa spécifique :</span><span class="sxs-lookup"><span data-stu-id="fee73-137">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa PostgreSQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="fee73-138">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="fee73-138">Linked service properties</span></span>
<span data-ttu-id="fee73-139">Hello tableau suivant fournit la description du service de tooPostgreSQL spécifique lié éléments JSON.</span><span class="sxs-lookup"><span data-stu-id="fee73-139">hello following table provides description for JSON elements specific tooPostgreSQL linked service.</span></span>

| <span data-ttu-id="fee73-140">Propriété</span><span class="sxs-lookup"><span data-stu-id="fee73-140">Property</span></span> | <span data-ttu-id="fee73-141">Description</span><span class="sxs-lookup"><span data-stu-id="fee73-141">Description</span></span> | <span data-ttu-id="fee73-142">Requis</span><span class="sxs-lookup"><span data-stu-id="fee73-142">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fee73-143">type</span><span class="sxs-lookup"><span data-stu-id="fee73-143">type</span></span> |<span data-ttu-id="fee73-144">propriété de type Hello doit indiquer : **OnPremisesPostgreSql**</span><span class="sxs-lookup"><span data-stu-id="fee73-144">hello type property must be set to: **OnPremisesPostgreSql**</span></span> |<span data-ttu-id="fee73-145">Oui</span><span class="sxs-lookup"><span data-stu-id="fee73-145">Yes</span></span> |
| <span data-ttu-id="fee73-146">server</span><span class="sxs-lookup"><span data-stu-id="fee73-146">server</span></span> |<span data-ttu-id="fee73-147">Nom du serveur de PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="fee73-147">Name of hello PostgreSQL server.</span></span> |<span data-ttu-id="fee73-148">Oui</span><span class="sxs-lookup"><span data-stu-id="fee73-148">Yes</span></span> |
| <span data-ttu-id="fee73-149">database</span><span class="sxs-lookup"><span data-stu-id="fee73-149">database</span></span> |<span data-ttu-id="fee73-150">Nom de la base de données PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="fee73-150">Name of hello PostgreSQL database.</span></span> |<span data-ttu-id="fee73-151">Oui</span><span class="sxs-lookup"><span data-stu-id="fee73-151">Yes</span></span> |
| <span data-ttu-id="fee73-152">schema</span><span class="sxs-lookup"><span data-stu-id="fee73-152">schema</span></span> |<span data-ttu-id="fee73-153">Nom de schéma hello hello de base de données.</span><span class="sxs-lookup"><span data-stu-id="fee73-153">Name of hello schema in hello database.</span></span> <span data-ttu-id="fee73-154">nom du schéma Hello respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="fee73-154">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="fee73-155">Non</span><span class="sxs-lookup"><span data-stu-id="fee73-155">No</span></span> |
| <span data-ttu-id="fee73-156">authenticationType</span><span class="sxs-lookup"><span data-stu-id="fee73-156">authenticationType</span></span> |<span data-ttu-id="fee73-157">Type d’authentification utilisé tooconnect toohello base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="fee73-157">Type of authentication used tooconnect toohello PostgreSQL database.</span></span> <span data-ttu-id="fee73-158">Les valeurs possibles sont : Anonyme, De base et Windows.</span><span class="sxs-lookup"><span data-stu-id="fee73-158">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="fee73-159">Oui</span><span class="sxs-lookup"><span data-stu-id="fee73-159">Yes</span></span> |
| <span data-ttu-id="fee73-160">username</span><span class="sxs-lookup"><span data-stu-id="fee73-160">username</span></span> |<span data-ttu-id="fee73-161">Spécifiez le nom d'utilisateur si vous utilisez l'authentification de base ou Windows.</span><span class="sxs-lookup"><span data-stu-id="fee73-161">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="fee73-162">Non</span><span class="sxs-lookup"><span data-stu-id="fee73-162">No</span></span> |
| <span data-ttu-id="fee73-163">password</span><span class="sxs-lookup"><span data-stu-id="fee73-163">password</span></span> |<span data-ttu-id="fee73-164">Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="fee73-164">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="fee73-165">Non</span><span class="sxs-lookup"><span data-stu-id="fee73-165">No</span></span> |
| <span data-ttu-id="fee73-166">gatewayName</span><span class="sxs-lookup"><span data-stu-id="fee73-166">gatewayName</span></span> |<span data-ttu-id="fee73-167">Nom de passerelle hello hello service Data Factory doit utiliser la base de données PostgreSQL tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="fee73-167">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises PostgreSQL database.</span></span> |<span data-ttu-id="fee73-168">Oui</span><span class="sxs-lookup"><span data-stu-id="fee73-168">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="fee73-169">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="fee73-169">Dataset properties</span></span>
<span data-ttu-id="fee73-170">Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="fee73-170">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="fee73-171">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données.</span><span class="sxs-lookup"><span data-stu-id="fee73-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="fee73-172">section de typeProperties Hello est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="fee73-172">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="fee73-173">jeu de données de type Hello typeProperties section **RelationalTable** (qui comprend de jeu de données PostgreSQL) a hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="fee73-173">hello typeProperties section for dataset of type **RelationalTable** (which includes PostgreSQL dataset) has hello following properties:</span></span>

| <span data-ttu-id="fee73-174">Propriété</span><span class="sxs-lookup"><span data-stu-id="fee73-174">Property</span></span> | <span data-ttu-id="fee73-175">Description</span><span class="sxs-lookup"><span data-stu-id="fee73-175">Description</span></span> | <span data-ttu-id="fee73-176">Requis</span><span class="sxs-lookup"><span data-stu-id="fee73-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fee73-177">TableName</span><span class="sxs-lookup"><span data-stu-id="fee73-177">tableName</span></span> |<span data-ttu-id="fee73-178">Nom de table hello Bonjour instance de base de données PostgreSQL service lié fait référence à.</span><span class="sxs-lookup"><span data-stu-id="fee73-178">Name of hello table in hello PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="fee73-179">Hello tableName respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="fee73-179">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="fee73-180">Non (si la **requête** de **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="fee73-180">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="fee73-181">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="fee73-181">Copy activity properties</span></span>
<span data-ttu-id="fee73-182">Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="fee73-182">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="fee73-183">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="fee73-183">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="fee73-184">Alors que les propriétés disponibles dans la section typeProperties hello activité hello varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="fee73-184">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="fee73-185">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="fee73-185">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="fee73-186">Lorsque la source est de type **RelationalSource** (qui inclut PostgreSQL), hello propriétés suivantes est disponible dans la section de typeProperties :</span><span class="sxs-lookup"><span data-stu-id="fee73-186">When source is of type **RelationalSource** (which includes PostgreSQL), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="fee73-187">Propriété</span><span class="sxs-lookup"><span data-stu-id="fee73-187">Property</span></span> | <span data-ttu-id="fee73-188">Description</span><span class="sxs-lookup"><span data-stu-id="fee73-188">Description</span></span> | <span data-ttu-id="fee73-189">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="fee73-189">Allowed values</span></span> | <span data-ttu-id="fee73-190">Requis</span><span class="sxs-lookup"><span data-stu-id="fee73-190">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fee73-191">query</span><span class="sxs-lookup"><span data-stu-id="fee73-191">query</span></span> |<span data-ttu-id="fee73-192">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="fee73-192">Use hello custom query tooread data.</span></span> |<span data-ttu-id="fee73-193">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="fee73-193">SQL query string.</span></span> <span data-ttu-id="fee73-194">Par exemple : "query": "select * from \"MySchema\".\"MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="fee73-194">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="fee73-195">Non (si **tableName** de **dataset** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="fee73-195">No (if **tableName** of **dataset** is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="fee73-196">Les noms de schéma et de table respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="fee73-196">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="fee73-197">Placez-les dans `""` (guillemets doubles) dans la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="fee73-197">Enclose them in `""` (double quotes) in hello query.</span></span>  

<span data-ttu-id="fee73-198">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="fee73-198">**Example:**</span></span>

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-tooazure-blob"></a><span data-ttu-id="fee73-199">Exemple de JSON : copier des données PostgreSQL tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="fee73-199">JSON example: Copy data from PostgreSQL tooAzure Blob</span></span>
<span data-ttu-id="fee73-200">Cet exemple fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fee73-200">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="fee73-201">Ils montrent la base de données PostgreSQL toocopy tooAzure stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="fee73-201">They show how toocopy data from PostgreSQL database tooAzure Blob Storage.</span></span> <span data-ttu-id="fee73-202">Toutefois, les données peuvent être copié tooany de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="fee73-202">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="fee73-203">Cet exemple fournit des extraits de code JSON.</span><span class="sxs-lookup"><span data-stu-id="fee73-203">This sample provides JSON snippets.</span></span> <span data-ttu-id="fee73-204">Il n’inclut pas d’instructions détaillées pour créer la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="fee73-204">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="fee73-205">Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="fee73-205">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="fee73-206">exemple Hello a hello suivant des entités de fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="fee73-206">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="fee73-207">Un service lié de type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fee73-207">A linked service of type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="fee73-208">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fee73-208">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="fee73-209">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fee73-209">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="fee73-210">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fee73-210">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="fee73-211">Hello [pipeline](data-factory-create-pipelines.md) avec l’activité de copie qui utilise [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="fee73-211">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="fee73-212">exemple Hello copie des données à partir d’un résultat de requête dans l’objet blob tooa de base de données PostgreSQL toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="fee73-212">hello sample copies data from a query result in PostgreSQL database tooa blob every hour.</span></span> <span data-ttu-id="fee73-213">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="fee73-213">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="fee73-214">Dans un premier temps, le programme d’installation passerelle de gestion des données hello.</span><span class="sxs-lookup"><span data-stu-id="fee73-214">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="fee73-215">instructions de Hello sont Bonjour [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="fee73-215">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="fee73-216">**Service lié PostgreSQL :**</span><span class="sxs-lookup"><span data-stu-id="fee73-216">**PostgreSQL linked service:**</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
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
<span data-ttu-id="fee73-217">**Service lié Azure Blob Storage :**</span><span class="sxs-lookup"><span data-stu-id="fee73-217">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
    }
    }
}
```
<span data-ttu-id="fee73-218">**Jeu de données d’entrée PostgreSQL :**</span><span class="sxs-lookup"><span data-stu-id="fee73-218">**PostgreSQL input dataset:**</span></span>

<span data-ttu-id="fee73-219">exemple Hello suppose que vous avez créé une table « MyTable » dans PostgreSQL et il contienne une colonne appelée « timestamp » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="fee73-219">hello sample assumes you have created a table “MyTable” in PostgreSQL and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="fee73-220">Paramètre `"external": true` informe le service de fabrique de données hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="fee73-220">Setting `"external": true` informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
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

<span data-ttu-id="fee73-221">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="fee73-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="fee73-222">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="fee73-222">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="fee73-223">nom de chemin d’accès et de dossier pour l’objet blob de hello Hello sont dynamiquement évaluées en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="fee73-223">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="fee73-224">chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="fee73-224">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobPostgreSqlDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/postgresql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="fee73-225">**Pipeline avec activité de copie :**</span><span class="sxs-lookup"><span data-stu-id="fee73-225">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="fee73-226">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="fee73-226">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="fee73-227">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**RelationalSource** et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="fee73-227">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="fee73-228">la requête SQL Hello spécifiée pour hello **requête** propriété sélectionne des données de hello à partir de la table de public.usstates hello dans la base de données PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="fee73-228">hello SQL query specified for hello **query** property selects hello data from hello public.usstates table in hello PostgreSQL database.</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"public\".\"usstates\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "PostgreSqlDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobPostgreSqlDataSet"
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
                "name": "PostgreSqlToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
## <a name="type-mapping-for-postgresql"></a><span data-ttu-id="fee73-229">Mappage de type pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="fee73-229">Type mapping for PostgreSQL</span></span>
<span data-ttu-id="fee73-230">Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) activité de copie de l’article effectue des conversions de type automatique à partir de types de sources de toosink types avec hello approche de l’étape 2 :</span><span class="sxs-lookup"><span data-stu-id="fee73-230">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="fee73-231">Convertir à partir de la source native types too.NET type</span><span class="sxs-lookup"><span data-stu-id="fee73-231">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="fee73-232">Conversion de type de récepteur de toonative de type .NET</span><span class="sxs-lookup"><span data-stu-id="fee73-232">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="fee73-233">Lors du déplacement des données tooPostgreSQL, hello mappages suivants sont utilisés à partir de too.NET de type PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="fee73-233">When moving data tooPostgreSQL, hello following mappings are used from PostgreSQL type too.NET type.</span></span>

| <span data-ttu-id="fee73-234">Type de base de données PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="fee73-234">PostgreSQL Database type</span></span> | <span data-ttu-id="fee73-235">Alias PostgresSQL</span><span class="sxs-lookup"><span data-stu-id="fee73-235">PostgresSQL aliases</span></span> | <span data-ttu-id="fee73-236">Type de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="fee73-236">.NET Framework type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fee73-237">abstime</span><span class="sxs-lookup"><span data-stu-id="fee73-237">abstime</span></span> | |<span data-ttu-id="fee73-238">Datetime</span><span class="sxs-lookup"><span data-stu-id="fee73-238">Datetime</span></span> | &nbsp;
| <span data-ttu-id="fee73-239">bigint</span><span class="sxs-lookup"><span data-stu-id="fee73-239">bigint</span></span> |<span data-ttu-id="fee73-240">int8</span><span class="sxs-lookup"><span data-stu-id="fee73-240">int8</span></span> |<span data-ttu-id="fee73-241">Int64</span><span class="sxs-lookup"><span data-stu-id="fee73-241">Int64</span></span> |
| <span data-ttu-id="fee73-242">bigserial</span><span class="sxs-lookup"><span data-stu-id="fee73-242">bigserial</span></span> |<span data-ttu-id="fee73-243">serial8</span><span class="sxs-lookup"><span data-stu-id="fee73-243">serial8</span></span> |<span data-ttu-id="fee73-244">Int64</span><span class="sxs-lookup"><span data-stu-id="fee73-244">Int64</span></span> |
| <span data-ttu-id="fee73-245">bit [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="fee73-245">bit [ (n) ]</span></span> | |<span data-ttu-id="fee73-246">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="fee73-246">Byte[], String</span></span> | &nbsp;
| <span data-ttu-id="fee73-247">bit varying [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="fee73-247">bit varying [ (n) ]</span></span> |<span data-ttu-id="fee73-248">varbit</span><span class="sxs-lookup"><span data-stu-id="fee73-248">varbit</span></span> |<span data-ttu-id="fee73-249">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="fee73-249">Byte[], String</span></span> |
| <span data-ttu-id="fee73-250">booléenne</span><span class="sxs-lookup"><span data-stu-id="fee73-250">boolean</span></span> |<span data-ttu-id="fee73-251">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="fee73-251">bool</span></span> |<span data-ttu-id="fee73-252">booléenne</span><span class="sxs-lookup"><span data-stu-id="fee73-252">Boolean</span></span> |
| <span data-ttu-id="fee73-253">box</span><span class="sxs-lookup"><span data-stu-id="fee73-253">box</span></span> | |<span data-ttu-id="fee73-254">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="fee73-254">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="fee73-255">bytea</span><span class="sxs-lookup"><span data-stu-id="fee73-255">bytea</span></span> | |<span data-ttu-id="fee73-256">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="fee73-256">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="fee73-257">character [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="fee73-257">character [ (n) ]</span></span> |<span data-ttu-id="fee73-258">char [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="fee73-258">char [ (n) ]</span></span> |<span data-ttu-id="fee73-259">String</span><span class="sxs-lookup"><span data-stu-id="fee73-259">String</span></span> |
| <span data-ttu-id="fee73-260">character varying [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="fee73-260">character varying [ (n) ]</span></span> |<span data-ttu-id="fee73-261">varchar [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="fee73-261">varchar [ (n) ]</span></span> |<span data-ttu-id="fee73-262">String</span><span class="sxs-lookup"><span data-stu-id="fee73-262">String</span></span> |
| <span data-ttu-id="fee73-263">cid</span><span class="sxs-lookup"><span data-stu-id="fee73-263">cid</span></span> | |<span data-ttu-id="fee73-264">String</span><span class="sxs-lookup"><span data-stu-id="fee73-264">String</span></span> |&nbsp;
| <span data-ttu-id="fee73-265">cidr</span><span class="sxs-lookup"><span data-stu-id="fee73-265">cidr</span></span> | |<span data-ttu-id="fee73-266">String</span><span class="sxs-lookup"><span data-stu-id="fee73-266">String</span></span> |&nbsp;
| <span data-ttu-id="fee73-267">circle</span><span class="sxs-lookup"><span data-stu-id="fee73-267">circle</span></span> | |<span data-ttu-id="fee73-268">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="fee73-268">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="fee73-269">date</span><span class="sxs-lookup"><span data-stu-id="fee73-269">date</span></span> | |<span data-ttu-id="fee73-270">Datetime</span><span class="sxs-lookup"><span data-stu-id="fee73-270">Datetime</span></span> |&nbsp;
| <span data-ttu-id="fee73-271">daterange</span><span class="sxs-lookup"><span data-stu-id="fee73-271">daterange</span></span> | |<span data-ttu-id="fee73-272">String</span><span class="sxs-lookup"><span data-stu-id="fee73-272">String</span></span> |&nbsp;
| <span data-ttu-id="fee73-273">double précision</span><span class="sxs-lookup"><span data-stu-id="fee73-273">double precision</span></span> |<span data-ttu-id="fee73-274">float8</span><span class="sxs-lookup"><span data-stu-id="fee73-274">float8</span></span> |<span data-ttu-id="fee73-275">Double</span><span class="sxs-lookup"><span data-stu-id="fee73-275">Double</span></span> |
| <span data-ttu-id="fee73-276">inet</span><span class="sxs-lookup"><span data-stu-id="fee73-276">inet</span></span> | |<span data-ttu-id="fee73-277">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="fee73-277">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="fee73-278">intarry</span><span class="sxs-lookup"><span data-stu-id="fee73-278">intarry</span></span> | |<span data-ttu-id="fee73-279">String</span><span class="sxs-lookup"><span data-stu-id="fee73-279">String</span></span> |&nbsp;
| <span data-ttu-id="fee73-280">int4range</span><span class="sxs-lookup"><span data-stu-id="fee73-280">int4range</span></span> | |<span data-ttu-id="fee73-281">String</span><span class="sxs-lookup"><span data-stu-id="fee73-281">String</span></span> |&nbsp;
| <span data-ttu-id="fee73-282">int8range</span><span class="sxs-lookup"><span data-stu-id="fee73-282">int8range</span></span> | |<span data-ttu-id="fee73-283">String</span><span class="sxs-lookup"><span data-stu-id="fee73-283">String</span></span> |&nbsp;
| <span data-ttu-id="fee73-284">integer</span><span class="sxs-lookup"><span data-stu-id="fee73-284">integer</span></span> |<span data-ttu-id="fee73-285">int, int4</span><span class="sxs-lookup"><span data-stu-id="fee73-285">int, int4</span></span> |<span data-ttu-id="fee73-286">Int32</span><span class="sxs-lookup"><span data-stu-id="fee73-286">Int32</span></span> |
| <span data-ttu-id="fee73-287">interval [ fields ] [ (p) ]</span><span class="sxs-lookup"><span data-stu-id="fee73-287">interval [ fields ] [ (p) ]</span></span> | |<span data-ttu-id="fee73-288">Timespan</span><span class="sxs-lookup"><span data-stu-id="fee73-288">Timespan</span></span> |&nbsp;
| <span data-ttu-id="fee73-289">json</span><span class="sxs-lookup"><span data-stu-id="fee73-289">json</span></span> | |<span data-ttu-id="fee73-290">String</span><span class="sxs-lookup"><span data-stu-id="fee73-290">String</span></span> |&nbsp;
| <span data-ttu-id="fee73-291">jsonb</span><span class="sxs-lookup"><span data-stu-id="fee73-291">jsonb</span></span> | |<span data-ttu-id="fee73-292">Byte[]</span><span class="sxs-lookup"><span data-stu-id="fee73-292">Byte[]</span></span> |&nbsp;
| <span data-ttu-id="fee73-293">line</span><span class="sxs-lookup"><span data-stu-id="fee73-293">line</span></span> | |<span data-ttu-id="fee73-294">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="fee73-294">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="fee73-295">lseg</span><span class="sxs-lookup"><span data-stu-id="fee73-295">lseg</span></span> | |<span data-ttu-id="fee73-296">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="fee73-296">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="fee73-297">macaddr</span><span class="sxs-lookup"><span data-stu-id="fee73-297">macaddr</span></span> | |<span data-ttu-id="fee73-298">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="fee73-298">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="fee73-299">money</span><span class="sxs-lookup"><span data-stu-id="fee73-299">money</span></span> | |<span data-ttu-id="fee73-300">Décimal</span><span class="sxs-lookup"><span data-stu-id="fee73-300">Decimal</span></span> |&nbsp;
| <span data-ttu-id="fee73-301">numeric [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="fee73-301">numeric [ (p, s) ]</span></span> |<span data-ttu-id="fee73-302">decimal [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="fee73-302">decimal [ (p, s) ]</span></span> |<span data-ttu-id="fee73-303">Décimal</span><span class="sxs-lookup"><span data-stu-id="fee73-303">Decimal</span></span> |
| <span data-ttu-id="fee73-304">numrange</span><span class="sxs-lookup"><span data-stu-id="fee73-304">numrange</span></span> | |<span data-ttu-id="fee73-305">String</span><span class="sxs-lookup"><span data-stu-id="fee73-305">String</span></span> |&nbsp;
| <span data-ttu-id="fee73-306">oid</span><span class="sxs-lookup"><span data-stu-id="fee73-306">oid</span></span> | |<span data-ttu-id="fee73-307">Int32</span><span class="sxs-lookup"><span data-stu-id="fee73-307">Int32</span></span> |&nbsp;
| <span data-ttu-id="fee73-308">path</span><span class="sxs-lookup"><span data-stu-id="fee73-308">path</span></span> | |<span data-ttu-id="fee73-309">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="fee73-309">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="fee73-310">pg_lsn</span><span class="sxs-lookup"><span data-stu-id="fee73-310">pg_lsn</span></span> | |<span data-ttu-id="fee73-311">Int64</span><span class="sxs-lookup"><span data-stu-id="fee73-311">Int64</span></span> |&nbsp;
| <span data-ttu-id="fee73-312">point</span><span class="sxs-lookup"><span data-stu-id="fee73-312">point</span></span> | |<span data-ttu-id="fee73-313">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="fee73-313">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="fee73-314">polygon</span><span class="sxs-lookup"><span data-stu-id="fee73-314">polygon</span></span> | |<span data-ttu-id="fee73-315">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="fee73-315">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="fee73-316">real</span><span class="sxs-lookup"><span data-stu-id="fee73-316">real</span></span> |<span data-ttu-id="fee73-317">float4</span><span class="sxs-lookup"><span data-stu-id="fee73-317">float4</span></span> |<span data-ttu-id="fee73-318">Single</span><span class="sxs-lookup"><span data-stu-id="fee73-318">Single</span></span> |
| <span data-ttu-id="fee73-319">smallint</span><span class="sxs-lookup"><span data-stu-id="fee73-319">smallint</span></span> |<span data-ttu-id="fee73-320">int2</span><span class="sxs-lookup"><span data-stu-id="fee73-320">int2</span></span> |<span data-ttu-id="fee73-321">Int16</span><span class="sxs-lookup"><span data-stu-id="fee73-321">Int16</span></span> |
| <span data-ttu-id="fee73-322">smallserial</span><span class="sxs-lookup"><span data-stu-id="fee73-322">smallserial</span></span> |<span data-ttu-id="fee73-323">serial2</span><span class="sxs-lookup"><span data-stu-id="fee73-323">serial2</span></span> |<span data-ttu-id="fee73-324">Int16</span><span class="sxs-lookup"><span data-stu-id="fee73-324">Int16</span></span> |
| <span data-ttu-id="fee73-325">serial</span><span class="sxs-lookup"><span data-stu-id="fee73-325">serial</span></span> |<span data-ttu-id="fee73-326">serial4</span><span class="sxs-lookup"><span data-stu-id="fee73-326">serial4</span></span> |<span data-ttu-id="fee73-327">Int32</span><span class="sxs-lookup"><span data-stu-id="fee73-327">Int32</span></span> |
| <span data-ttu-id="fee73-328">texte</span><span class="sxs-lookup"><span data-stu-id="fee73-328">text</span></span> | |<span data-ttu-id="fee73-329">String</span><span class="sxs-lookup"><span data-stu-id="fee73-329">String</span></span> |&nbsp;

## <a name="map-source-toosink-columns"></a><span data-ttu-id="fee73-330">Mapper les colonnes de source toosink</span><span class="sxs-lookup"><span data-stu-id="fee73-330">Map source toosink columns</span></span>
<span data-ttu-id="fee73-331">toolearn sur le mappage des colonnes dans toocolumns du jeu de données source dans le jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="fee73-331">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="fee73-332">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="fee73-332">Repeatable read from relational sources</span></span>
<span data-ttu-id="fee73-333">Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="fee73-333">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="fee73-334">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="fee73-334">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="fee73-335">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="fee73-335">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="fee73-336">Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée.</span><span class="sxs-lookup"><span data-stu-id="fee73-336">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="fee73-337">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="fee73-337">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="fee73-338">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="fee73-338">Performance and Tuning</span></span>
<span data-ttu-id="fee73-339">Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="fee73-339">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
