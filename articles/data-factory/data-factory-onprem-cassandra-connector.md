---
title: "données aaaMove Cassandra à l’aide de la fabrique de données | Documents Microsoft"
description: "Découvrez comment toomove des données à partir d’un Cassandra local de base de données à l’aide d’Azure Data Factory."
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
ms.openlocfilehash: 0e265d3a8439d0a2cb2a5c32e5ea8348a1617621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a><span data-ttu-id="2b728-103">Déplacer des données depuis une base de données Cassandra locale à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="2b728-103">Move data from an on-premises Cassandra database using Azure Data Factory</span></span>
<span data-ttu-id="2b728-104">Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory à partir d’une base de données locale Cassandra.</span><span class="sxs-lookup"><span data-stu-id="2b728-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Cassandra database.</span></span> <span data-ttu-id="2b728-105">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="2b728-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="2b728-106">Vous pouvez copier les données d’une banque de données locale Cassandra données magasin tooany pris en charge récepteur.</span><span class="sxs-lookup"><span data-stu-id="2b728-106">You can copy data from an on-premises Cassandra data store tooany supported sink data store.</span></span> <span data-ttu-id="2b728-107">Pour une liste de données pris en charge des magasins récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="2b728-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="2b728-108">Fabrique de données prend en charge uniquement le déplacement tooother les magasins de données du magasin de données à partir de données Cassandra, mais ne pas pour déplacer des données d’une autre banque de données Cassandra tooa données magasins.</span><span class="sxs-lookup"><span data-stu-id="2b728-108">Data factory currently supports only moving data from a Cassandra data store tooother data stores, but not for moving data from other data stores tooa Cassandra data store.</span></span> 

## <a name="supported-versions"></a><span data-ttu-id="2b728-109">Versions prises en charge</span><span class="sxs-lookup"><span data-stu-id="2b728-109">Supported versions</span></span>
<span data-ttu-id="2b728-110">connecteur de Cassandra Hello prend en charge hello versions de Cassandra suivantes : 2.X.</span><span class="sxs-lookup"><span data-stu-id="2b728-110">hello Cassandra connector supports hello following versions of Cassandra: 2.X.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b728-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2b728-111">Prerequisites</span></span>
<span data-ttu-id="2b728-112">Pour hello Azure Data Factory service toobe tooconnect en mesure de tooyour Cassandra base de données locale, vous devez installer une passerelle de gestion des données sur hello même cette base de données hello hôtes de l’ordinateur ou sur un tooavoid machine distincte qui entrent en concurrence pour les ressources par hello base de données.</span><span class="sxs-lookup"><span data-stu-id="2b728-112">For hello Azure Data Factory service toobe able tooconnect tooyour on-premises Cassandra database, you must install a Data Management Gateway on hello same machine that hosts hello database or on a separate machine tooavoid competing for resources with hello database.</span></span> <span data-ttu-id="2b728-113">Passerelle de gestion des données est un composant qui établit des services de toocloud de sources de données sur site de manière sécurisée et gérée.</span><span class="sxs-lookup"><span data-stu-id="2b728-113">Data Management Gateway is a component that connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="2b728-114">Consultez l’article [Passerelle de gestion des données](data-factory-data-management-gateway.md) pour obtenir des informations détaillées sur la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="2b728-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="2b728-115">Consultez [déplacer des données locales toocloud](data-factory-move-data-between-onprem-and-cloud.md) article pour obtenir des instructions sur la configuration de passerelle de hello données toomove de pipeline de données.</span><span class="sxs-lookup"><span data-stu-id="2b728-115">See [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

<span data-ttu-id="2b728-116">Vous devez utiliser la base de données hello passerelle tooconnect tooa Cassandra même si la base de données hello est hébergé dans le cloud de hello, par exemple, sur une machine virtuelle IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="2b728-116">You must use hello gateway tooconnect tooa Cassandra database even if hello database is hosted in hello cloud, for example, on an Azure IaaS VM.</span></span> <span data-ttu-id="2b728-117">Y avoir de passerelle de hello sur hello même machine virtuelle de cette base de données hôtes hello ou sur un ordinateur distinct virtuel tant que passerelle de hello peuvent se connecter toohello de base de données.</span><span class="sxs-lookup"><span data-stu-id="2b728-117">Y You can have hello gateway on hello same VM that hosts hello database or on a separate VM as long as hello gateway can connect toohello database.</span></span>  

<span data-ttu-id="2b728-118">Lorsque vous installez la passerelle de hello, il installe automatiquement une base de données ODBC de Microsoft Cassandra pilote utilisé tooconnect tooCassandra.</span><span class="sxs-lookup"><span data-stu-id="2b728-118">When you install hello gateway, it automatically installs a Microsoft Cassandra ODBC driver used tooconnect tooCassandra database.</span></span> <span data-ttu-id="2b728-119">Par conséquent, vous n’avez pas besoin toomanually installer un pilote sur l’ordinateur de passerelle hello lors de la copie des données à partir de la base de données Cassandra hello.</span><span class="sxs-lookup"><span data-stu-id="2b728-119">Therefore, you don't need toomanually install any driver on hello gateway machine when copying data from hello Cassandra database.</span></span> 

> [!NOTE]
> <span data-ttu-id="2b728-120">Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.</span><span class="sxs-lookup"><span data-stu-id="2b728-120">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2b728-121">Prise en main</span><span class="sxs-lookup"><span data-stu-id="2b728-121">Getting started</span></span>
<span data-ttu-id="2b728-122">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données Cassandra local à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="2b728-122">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="2b728-123">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="2b728-123">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="2b728-124">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="2b728-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="2b728-125">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="2b728-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="2b728-126">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="2b728-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="2b728-127">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="2b728-127">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="2b728-128">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="2b728-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="2b728-129">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="2b728-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="2b728-130">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="2b728-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="2b728-131">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="2b728-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="2b728-132">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="2b728-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="2b728-133">Pour voir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont utilisés toocopy des données à partir d’une banque de données locale Cassandra, [exemple de JSON : copier des données à partir de Cassandra tooAzure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="2b728-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Cassandra data store, see [JSON example: Copy data from Cassandra tooAzure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="2b728-134">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont le magasin de données Cassandra utilisé toodefine Data Factory entités tooa spécifique :</span><span class="sxs-lookup"><span data-stu-id="2b728-134">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Cassandra data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="2b728-135">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="2b728-135">Linked service properties</span></span>
<span data-ttu-id="2b728-136">Hello tableau suivant fournit la description du service de tooCassandra spécifique lié éléments JSON.</span><span class="sxs-lookup"><span data-stu-id="2b728-136">hello following table provides description for JSON elements specific tooCassandra linked service.</span></span>

| <span data-ttu-id="2b728-137">Propriété</span><span class="sxs-lookup"><span data-stu-id="2b728-137">Property</span></span> | <span data-ttu-id="2b728-138">Description</span><span class="sxs-lookup"><span data-stu-id="2b728-138">Description</span></span> | <span data-ttu-id="2b728-139">Requis</span><span class="sxs-lookup"><span data-stu-id="2b728-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2b728-140">type</span><span class="sxs-lookup"><span data-stu-id="2b728-140">type</span></span> |<span data-ttu-id="2b728-141">propriété de type Hello doit indiquer : **OnPremisesCassandra**</span><span class="sxs-lookup"><span data-stu-id="2b728-141">hello type property must be set to: **OnPremisesCassandra**</span></span> |<span data-ttu-id="2b728-142">Oui</span><span class="sxs-lookup"><span data-stu-id="2b728-142">Yes</span></span> |
| <span data-ttu-id="2b728-143">host</span><span class="sxs-lookup"><span data-stu-id="2b728-143">host</span></span> |<span data-ttu-id="2b728-144">Une ou plusieurs adresses IP ou noms d’hôte de serveurs Cassandra.</span><span class="sxs-lookup"><span data-stu-id="2b728-144">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="2b728-145">Spécifiez une liste séparée par des virgules des adresses IP ou hôte noms tooconnect tooall serveurs simultanément.</span><span class="sxs-lookup"><span data-stu-id="2b728-145">Specify a comma-separated list of IP addresses or host names tooconnect tooall servers concurrently.</span></span> |<span data-ttu-id="2b728-146">Oui</span><span class="sxs-lookup"><span data-stu-id="2b728-146">Yes</span></span> |
| <span data-ttu-id="2b728-147">port</span><span class="sxs-lookup"><span data-stu-id="2b728-147">port</span></span> |<span data-ttu-id="2b728-148">Hello le port TCP qui hello du serveur de Cassandra utilise toolisten pour les connexions client.</span><span class="sxs-lookup"><span data-stu-id="2b728-148">hello TCP port that hello Cassandra server uses toolisten for client connections.</span></span> |<span data-ttu-id="2b728-149">Non, valeur par défaut : 9042</span><span class="sxs-lookup"><span data-stu-id="2b728-149">No, default value: 9042</span></span> |
| <span data-ttu-id="2b728-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="2b728-150">authenticationType</span></span> |<span data-ttu-id="2b728-151">Basique ou anonyme</span><span class="sxs-lookup"><span data-stu-id="2b728-151">Basic, or Anonymous</span></span> |<span data-ttu-id="2b728-152">Oui</span><span class="sxs-lookup"><span data-stu-id="2b728-152">Yes</span></span> |
| <span data-ttu-id="2b728-153">username</span><span class="sxs-lookup"><span data-stu-id="2b728-153">username</span></span> |<span data-ttu-id="2b728-154">Spécifiez le nom d’utilisateur pour le compte d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="2b728-154">Specify user name for hello user account.</span></span> |<span data-ttu-id="2b728-155">Oui, si authenticationType a la valeur tooBasic.</span><span class="sxs-lookup"><span data-stu-id="2b728-155">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="2b728-156">password</span><span class="sxs-lookup"><span data-stu-id="2b728-156">password</span></span> |<span data-ttu-id="2b728-157">Spécifiez le mot de passe de compte d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="2b728-157">Specify password for hello user account.</span></span> |<span data-ttu-id="2b728-158">Oui, si authenticationType a la valeur tooBasic.</span><span class="sxs-lookup"><span data-stu-id="2b728-158">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="2b728-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="2b728-159">gatewayName</span></span> |<span data-ttu-id="2b728-160">nom Hello de passerelle hello est utilisé tooconnect toohello Cassandra base de données locale.</span><span class="sxs-lookup"><span data-stu-id="2b728-160">hello name of hello gateway that is used tooconnect toohello on-premises Cassandra database.</span></span> |<span data-ttu-id="2b728-161">Oui</span><span class="sxs-lookup"><span data-stu-id="2b728-161">Yes</span></span> |
| <span data-ttu-id="2b728-162">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="2b728-162">encryptedCredential</span></span> |<span data-ttu-id="2b728-163">Informations d’identification chiffrées par la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="2b728-163">Credential encrypted by hello gateway.</span></span> |<span data-ttu-id="2b728-164">Non</span><span class="sxs-lookup"><span data-stu-id="2b728-164">No</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="2b728-165">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="2b728-165">Dataset properties</span></span>
<span data-ttu-id="2b728-166">Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="2b728-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="2b728-167">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="2b728-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="2b728-168">Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="2b728-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="2b728-169">jeu de données de type Hello typeProperties section **CassandraTable** a les propriétés suivantes de hello</span><span class="sxs-lookup"><span data-stu-id="2b728-169">hello typeProperties section for dataset of type **CassandraTable** has hello following properties</span></span>

| <span data-ttu-id="2b728-170">Propriété</span><span class="sxs-lookup"><span data-stu-id="2b728-170">Property</span></span> | <span data-ttu-id="2b728-171">Description</span><span class="sxs-lookup"><span data-stu-id="2b728-171">Description</span></span> | <span data-ttu-id="2b728-172">Requis</span><span class="sxs-lookup"><span data-stu-id="2b728-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2b728-173">espace de clé</span><span class="sxs-lookup"><span data-stu-id="2b728-173">keyspace</span></span> |<span data-ttu-id="2b728-174">Nom de l’espace de clés hello ou un schéma de base de données Cassandra.</span><span class="sxs-lookup"><span data-stu-id="2b728-174">Name of hello keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="2b728-175">Oui (si la **requête** pour **CassandraSource** n’est pas définie).</span><span class="sxs-lookup"><span data-stu-id="2b728-175">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="2b728-176">TableName</span><span class="sxs-lookup"><span data-stu-id="2b728-176">tableName</span></span> |<span data-ttu-id="2b728-177">Nom de table hello Cassandra de base de données.</span><span class="sxs-lookup"><span data-stu-id="2b728-177">Name of hello table in Cassandra database.</span></span> |<span data-ttu-id="2b728-178">Oui (si la **requête** pour **CassandraSource** n’est pas définie).</span><span class="sxs-lookup"><span data-stu-id="2b728-178">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="2b728-179">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="2b728-179">Copy activity properties</span></span>
<span data-ttu-id="2b728-180">Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="2b728-180">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2b728-181">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="2b728-181">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="2b728-182">Alors que les propriétés disponibles dans la section typeProperties hello activité hello varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="2b728-182">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="2b728-183">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="2b728-183">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="2b728-184">Lorsque la source est de type **CassandraSource**, hello propriétés suivantes est disponible dans la section de typeProperties :</span><span class="sxs-lookup"><span data-stu-id="2b728-184">When source is of type **CassandraSource**, hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="2b728-185">Propriété</span><span class="sxs-lookup"><span data-stu-id="2b728-185">Property</span></span> | <span data-ttu-id="2b728-186">Description</span><span class="sxs-lookup"><span data-stu-id="2b728-186">Description</span></span> | <span data-ttu-id="2b728-187">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="2b728-187">Allowed values</span></span> | <span data-ttu-id="2b728-188">Requis</span><span class="sxs-lookup"><span data-stu-id="2b728-188">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2b728-189">query</span><span class="sxs-lookup"><span data-stu-id="2b728-189">query</span></span> |<span data-ttu-id="2b728-190">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="2b728-190">Use hello custom query tooread data.</span></span> |<span data-ttu-id="2b728-191">Requête SQL-92 ou requête CQL.</span><span class="sxs-lookup"><span data-stu-id="2b728-191">SQL-92 query or CQL query.</span></span> <span data-ttu-id="2b728-192">Reportez-vous à [référence CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="2b728-192">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="2b728-193">Lorsque vous utilisez la requête SQL, spécifiez **nom d’espace de clés name.table** toorepresent hello tableau tooquery.</span><span class="sxs-lookup"><span data-stu-id="2b728-193">When using SQL query, specify **keyspace name.table name** toorepresent hello table you want tooquery.</span></span> |<span data-ttu-id="2b728-194">Non (si tableName et keyspace sur le jeu de données sont définis).</span><span class="sxs-lookup"><span data-stu-id="2b728-194">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="2b728-195">Niveau de cohérence</span><span class="sxs-lookup"><span data-stu-id="2b728-195">consistencyLevel</span></span> |<span data-ttu-id="2b728-196">niveau de cohérence Hello Spécifie le nombre de réplicas doit répondre de requête de lecture tooa avant de retourner l’application data toohello client.</span><span class="sxs-lookup"><span data-stu-id="2b728-196">hello consistency level specifies how many replicas must respond tooa read request before returning data toohello client application.</span></span> <span data-ttu-id="2b728-197">Les vérifications Cassandra hello un nombre spécifié de réplicas pour la requête de lecture hello toosatisfy de données.</span><span class="sxs-lookup"><span data-stu-id="2b728-197">Cassandra checks hello specified number of replicas for data toosatisfy hello read request.</span></span> |<span data-ttu-id="2b728-198">UN, DEUX, TROIS, QUORUM, TOUT, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="2b728-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="2b728-199">Reportez-vous à [Configuring data consistency (Configuration de la cohérence des données)](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="2b728-199">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="2b728-200">Non.</span><span class="sxs-lookup"><span data-stu-id="2b728-200">No.</span></span> <span data-ttu-id="2b728-201">La valeur par défaut est UN.</span><span class="sxs-lookup"><span data-stu-id="2b728-201">Default value is ONE.</span></span> |

## <a name="json-example-copy-data-from-cassandra-tooazure-blob"></a><span data-ttu-id="2b728-202">Exemple de JSON : copier des données à partir de Cassandra tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="2b728-202">JSON example: Copy data from Cassandra tooAzure Blob</span></span>
<span data-ttu-id="2b728-203">Cet exemple fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2b728-203">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="2b728-204">Elle indique la base de données toocopy à partir d’un Cassandra local tooan stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="2b728-204">It shows how toocopy data from an on-premises Cassandra database tooan Azure Blob Storage.</span></span> <span data-ttu-id="2b728-205">Toutefois, les données peuvent être copié tooany de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2b728-205">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b728-206">Cet exemple fournit des extraits de code JSON.</span><span class="sxs-lookup"><span data-stu-id="2b728-206">This sample provides JSON snippets.</span></span> <span data-ttu-id="2b728-207">Il n’inclut pas d’instructions détaillées pour créer la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="2b728-207">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="2b728-208">Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="2b728-208">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="2b728-209">exemple Hello a hello suivant des entités de fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="2b728-209">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="2b728-210">Un service lié de type [OnPremisesCassandra](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2b728-210">A linked service of type [OnPremisesCassandra](#linked-service-properties).</span></span>
* <span data-ttu-id="2b728-211">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2b728-211">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="2b728-212">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [CassandraTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2b728-212">An input [dataset](data-factory-create-datasets.md) of type [CassandraTable](#dataset-properties).</span></span>
* <span data-ttu-id="2b728-213">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2b728-213">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="2b728-214">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [CassandraSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="2b728-214">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [CassandraSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="2b728-215">**Service lié Cassandra :**</span><span class="sxs-lookup"><span data-stu-id="2b728-215">**Cassandra linked service:**</span></span>

<span data-ttu-id="2b728-216">Cet exemple utilise hello **Cassandra** service lié.</span><span class="sxs-lookup"><span data-stu-id="2b728-216">This example uses hello **Cassandra** linked service.</span></span> <span data-ttu-id="2b728-217">Consultez [Cassandra de service lié](#linked-service-properties) section pour les propriétés hello pris en charge par ce service lié.</span><span class="sxs-lookup"><span data-stu-id="2b728-217">See [Cassandra linked service](#linked-service-properties) section for hello properties supported by this linked service.</span></span>  

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

<span data-ttu-id="2b728-218">**Service lié Azure Storage :**</span><span class="sxs-lookup"><span data-stu-id="2b728-218">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="2b728-219">**Jeu de données d’entrée Cassandra :**</span><span class="sxs-lookup"><span data-stu-id="2b728-219">**Cassandra input dataset:**</span></span>

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

<span data-ttu-id="2b728-220">Paramètre **externe** trop**true** informe le service de fabrique de données hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="2b728-220">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="2b728-221">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="2b728-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="2b728-222">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="2b728-222">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

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

<span data-ttu-id="2b728-223">**Activité de copie dans un pipeline avec une source Cassandra et un récepteur blob :**</span><span class="sxs-lookup"><span data-stu-id="2b728-223">**Copy activity in a pipeline with Cassandra source and Blob sink:**</span></span>

<span data-ttu-id="2b728-224">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="2b728-224">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="2b728-225">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**CassandraSource** et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="2b728-225">In hello pipeline JSON definition, hello **source** type is set too**CassandraSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="2b728-226">Consultez [RelationalSource les propriétés de type](#copy-activity-properties) pour la liste des propriétés prises en charge par hello RelationalSource hello.</span><span class="sxs-lookup"><span data-stu-id="2b728-226">See [RelationalSource type properties](#copy-activity-properties) for hello list of properties supported by hello RelationalSource.</span></span>

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
            "description": "Copy from Cassandra tooan Azure blob",
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

### <a name="type-mapping-for-cassandra"></a><span data-ttu-id="2b728-227">Mappage de type pour Cassandra</span><span class="sxs-lookup"><span data-stu-id="2b728-227">Type mapping for Cassandra</span></span>
| <span data-ttu-id="2b728-228">Type Cassandra</span><span class="sxs-lookup"><span data-stu-id="2b728-228">Cassandra Type</span></span> | <span data-ttu-id="2b728-229">Type basé sur .Net</span><span class="sxs-lookup"><span data-stu-id="2b728-229">.Net Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="2b728-230">ASCII</span><span class="sxs-lookup"><span data-stu-id="2b728-230">ASCII</span></span> |<span data-ttu-id="2b728-231">String</span><span class="sxs-lookup"><span data-stu-id="2b728-231">String</span></span> |
| <span data-ttu-id="2b728-232">BIGINT</span><span class="sxs-lookup"><span data-stu-id="2b728-232">BIGINT</span></span> |<span data-ttu-id="2b728-233">Int64</span><span class="sxs-lookup"><span data-stu-id="2b728-233">Int64</span></span> |
| <span data-ttu-id="2b728-234">BLOB</span><span class="sxs-lookup"><span data-stu-id="2b728-234">BLOB</span></span> |<span data-ttu-id="2b728-235">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2b728-235">Byte[]</span></span> |
| <span data-ttu-id="2b728-236">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="2b728-236">BOOLEAN</span></span> |<span data-ttu-id="2b728-237">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="2b728-237">Boolean</span></span> |
| <span data-ttu-id="2b728-238">DÉCIMAL</span><span class="sxs-lookup"><span data-stu-id="2b728-238">DECIMAL</span></span> |<span data-ttu-id="2b728-239">DÉCIMAL</span><span class="sxs-lookup"><span data-stu-id="2b728-239">Decimal</span></span> |
| <span data-ttu-id="2b728-240">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="2b728-240">DOUBLE</span></span> |<span data-ttu-id="2b728-241">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="2b728-241">Double</span></span> |
| <span data-ttu-id="2b728-242">FLOAT</span><span class="sxs-lookup"><span data-stu-id="2b728-242">FLOAT</span></span> |<span data-ttu-id="2b728-243">Single</span><span class="sxs-lookup"><span data-stu-id="2b728-243">Single</span></span> |
| <span data-ttu-id="2b728-244">INET</span><span class="sxs-lookup"><span data-stu-id="2b728-244">INET</span></span> |<span data-ttu-id="2b728-245">String</span><span class="sxs-lookup"><span data-stu-id="2b728-245">String</span></span> |
| <span data-ttu-id="2b728-246">INT</span><span class="sxs-lookup"><span data-stu-id="2b728-246">INT</span></span> |<span data-ttu-id="2b728-247">Int32</span><span class="sxs-lookup"><span data-stu-id="2b728-247">Int32</span></span> |
| <span data-ttu-id="2b728-248">TEXTE</span><span class="sxs-lookup"><span data-stu-id="2b728-248">TEXT</span></span> |<span data-ttu-id="2b728-249">String</span><span class="sxs-lookup"><span data-stu-id="2b728-249">String</span></span> |
| <span data-ttu-id="2b728-250">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="2b728-250">TIMESTAMP</span></span> |<span data-ttu-id="2b728-251">DateTime</span><span class="sxs-lookup"><span data-stu-id="2b728-251">DateTime</span></span> |
| <span data-ttu-id="2b728-252">TIMEUUID</span><span class="sxs-lookup"><span data-stu-id="2b728-252">TIMEUUID</span></span> |<span data-ttu-id="2b728-253">Guid</span><span class="sxs-lookup"><span data-stu-id="2b728-253">Guid</span></span> |
| <span data-ttu-id="2b728-254">UUID</span><span class="sxs-lookup"><span data-stu-id="2b728-254">UUID</span></span> |<span data-ttu-id="2b728-255">Guid</span><span class="sxs-lookup"><span data-stu-id="2b728-255">Guid</span></span> |
| <span data-ttu-id="2b728-256">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="2b728-256">VARCHAR</span></span> |<span data-ttu-id="2b728-257">String</span><span class="sxs-lookup"><span data-stu-id="2b728-257">String</span></span> |
| <span data-ttu-id="2b728-258">VARINT</span><span class="sxs-lookup"><span data-stu-id="2b728-258">VARINT</span></span> |<span data-ttu-id="2b728-259">Décimal</span><span class="sxs-lookup"><span data-stu-id="2b728-259">Decimal</span></span> |

> [!NOTE]
> <span data-ttu-id="2b728-260">Pour la collection de types (carte, ensemble, liste, etc.), consultez trop[travailler avec les types de collection Cassandra à l’aide de la table virtuelle](#work-with-collections-using-virtual-table) section.</span><span class="sxs-lookup"><span data-stu-id="2b728-260">For collection types (map, set, list, etc.), refer too[Work with Cassandra collection types using virtual table](#work-with-collections-using-virtual-table) section.</span></span>
>
> <span data-ttu-id="2b728-261">Les types définis par l’utilisateur ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="2b728-261">User-defined types are not supported.</span></span>
>
> <span data-ttu-id="2b728-262">longueur de Hello de longueurs de colonne binaire et de la colonne de chaîne ne peut pas être supérieure à 4000.</span><span class="sxs-lookup"><span data-stu-id="2b728-262">hello length of Binary Column and String Column lengths cannot be greater than 4000.</span></span>
>
>

## <a name="work-with-collections-using-virtual-table"></a><span data-ttu-id="2b728-263">Travailler avec des collections à l’aide d’une table virtuelle</span><span class="sxs-lookup"><span data-stu-id="2b728-263">Work with collections using virtual table</span></span>
<span data-ttu-id="2b728-264">Azure Data Factory utilise une intégrés ODBC driver tooconnect tooand copier les données de votre base de données Cassandra.</span><span class="sxs-lookup"><span data-stu-id="2b728-264">Azure Data Factory uses a built-in ODBC driver tooconnect tooand copy data from your Cassandra database.</span></span> <span data-ttu-id="2b728-265">Pour les types de collection, y compris la carte, ensemble et liste, les pilotes hello renormalise les données hello dans les tables virtuelles correspondants.</span><span class="sxs-lookup"><span data-stu-id="2b728-265">For collection types including map, set and list, hello driver renormalizes hello data into corresponding virtual tables.</span></span> <span data-ttu-id="2b728-266">Plus précisément, si une table contient des colonnes de la collection, pilote de hello génère hello tables virtuelles suivantes :</span><span class="sxs-lookup"><span data-stu-id="2b728-266">Specifically, if a table contains any collection columns, hello driver generates hello following virtual tables:</span></span>

* <span data-ttu-id="2b728-267">A **table de base**, lequel contient hello les mêmes données que la table réelle de hello sauf pour les colonnes de regroupement hello.</span><span class="sxs-lookup"><span data-stu-id="2b728-267">A **base table**, which contains hello same data as hello real table except for hello collection columns.</span></span> <span data-ttu-id="2b728-268">table de base Hello utilise hello même nom en tant que table réelle hello qu’elle représente.</span><span class="sxs-lookup"><span data-stu-id="2b728-268">hello base table uses hello same name as hello real table that it represents.</span></span>
* <span data-ttu-id="2b728-269">A **table virtuelle** pour chaque colonne de la collection, qui étend les données de salutation imbriquée.</span><span class="sxs-lookup"><span data-stu-id="2b728-269">A **virtual table** for each collection column, which expands hello nested data.</span></span> <span data-ttu-id="2b728-270">tables virtuelles Hello qui représentent des collections sont nommées à l’aide du nom hello de table réelle hello, un séparateur «*vt*» et le nom hello de colonne de hello.</span><span class="sxs-lookup"><span data-stu-id="2b728-270">hello virtual tables that represent collections are named using hello name of hello real table, a separator “*vt*” and hello name of hello column.</span></span>

<span data-ttu-id="2b728-271">Tables virtuelles font référence à des données de toohello dans la table réelle de hello, l’activation tooaccess de pilote hello hello données dénormalisées.</span><span class="sxs-lookup"><span data-stu-id="2b728-271">Virtual tables refer toohello data in hello real table, enabling hello driver tooaccess hello denormalized data.</span></span> <span data-ttu-id="2b728-272">Consultez la section Exemple pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="2b728-272">See Example section for details.</span></span> <span data-ttu-id="2b728-273">Vous pouvez accéder à contenu hello des collections de Cassandra en interrogeant et en joignant les tables virtuelles hello.</span><span class="sxs-lookup"><span data-stu-id="2b728-273">You can access hello content of Cassandra collections by querying and joining hello virtual tables.</span></span>

<span data-ttu-id="2b728-274">Vous pouvez utiliser hello [Assistant copie de](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively vue hello la liste des tables de base de données Cassandra, y compris les tables virtuelles hello et afficher un aperçu des données hello à l’intérieur.</span><span class="sxs-lookup"><span data-stu-id="2b728-274">You can use hello [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively view hello list of tables in Cassandra database including hello virtual tables, and preview hello data inside.</span></span> <span data-ttu-id="2b728-275">Vous pouvez également créer une requête dans l’Assistant copie de hello et toosee hello résultat de la validation.</span><span class="sxs-lookup"><span data-stu-id="2b728-275">You can also construct a query in hello Copy Wizard and validate toosee hello result.</span></span>

### <a name="example"></a><span data-ttu-id="2b728-276">Exemple</span><span class="sxs-lookup"><span data-stu-id="2b728-276">Example</span></span>
<span data-ttu-id="2b728-277">Par exemple, hello suivant « ExampleTable » est une table de base de données Cassandra qui contient une colonne clé primaire d’entiers nommés « pk_int », une colonne de texte nommé value, une colonne de liste, une colonne de table et une colonne de jeu (nommé « StringSet »).</span><span class="sxs-lookup"><span data-stu-id="2b728-277">For example, hello following “ExampleTable” is a Cassandra database table that contains an integer primary key column named “pk_int”, a text column named value, a list column, a map column, and a set column (named “StringSet”).</span></span>

| <span data-ttu-id="2b728-278">pk_int</span><span class="sxs-lookup"><span data-stu-id="2b728-278">pk_int</span></span> | <span data-ttu-id="2b728-279">Valeur</span><span class="sxs-lookup"><span data-stu-id="2b728-279">Value</span></span> | <span data-ttu-id="2b728-280">Énumérer</span><span class="sxs-lookup"><span data-stu-id="2b728-280">List</span></span> | <span data-ttu-id="2b728-281">Mappage</span><span class="sxs-lookup"><span data-stu-id="2b728-281">Map</span></span> | <span data-ttu-id="2b728-282">StringSet</span><span class="sxs-lookup"><span data-stu-id="2b728-282">StringSet</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="2b728-283">1</span><span class="sxs-lookup"><span data-stu-id="2b728-283">1</span></span> |<span data-ttu-id="2b728-284">« exemple de valeur 1 »</span><span class="sxs-lookup"><span data-stu-id="2b728-284">"sample value 1"</span></span> |<span data-ttu-id="2b728-285">[« 1 », « 2 », « 3 »]</span><span class="sxs-lookup"><span data-stu-id="2b728-285">["1", "2", "3"]</span></span> |<span data-ttu-id="2b728-286">{« S1 » : « a », « S2 » : « b »}</span><span class="sxs-lookup"><span data-stu-id="2b728-286">{"S1": "a", "S2": "b"}</span></span> |<span data-ttu-id="2b728-287">{« A », « B », « C »}</span><span class="sxs-lookup"><span data-stu-id="2b728-287">{"A", "B", "C"}</span></span> |
| <span data-ttu-id="2b728-288">3</span><span class="sxs-lookup"><span data-stu-id="2b728-288">3</span></span> |<span data-ttu-id="2b728-289">« exemple de valeur 3 »</span><span class="sxs-lookup"><span data-stu-id="2b728-289">"sample value 3"</span></span> |<span data-ttu-id="2b728-290">[« 100 », « 101 », « 102 », « 105 »]</span><span class="sxs-lookup"><span data-stu-id="2b728-290">["100", "101", "102", "105"]</span></span> |<span data-ttu-id="2b728-291">{« S1 » : « t »}</span><span class="sxs-lookup"><span data-stu-id="2b728-291">{"S1": "t"}</span></span> |<span data-ttu-id="2b728-292">{« A », « E »}</span><span class="sxs-lookup"><span data-stu-id="2b728-292">{"A", "E"}</span></span> |

<span data-ttu-id="2b728-293">pilote de Hello génèrent plusieurs tables virtuelles toorepresent ce tableau.</span><span class="sxs-lookup"><span data-stu-id="2b728-293">hello driver would generate multiple virtual tables toorepresent this single table.</span></span> <span data-ttu-id="2b728-294">Hello colonnes clés étrangères dans les tables virtuelles hello référencer des colonnes de clé primaire hello dans la table réelle de hello et indiquer quels réel table ligne hello table virtuelle ligne correspond à.</span><span class="sxs-lookup"><span data-stu-id="2b728-294">hello foreign key columns in hello virtual tables reference hello primary key columns in hello real table, and indicate which real table row hello virtual table row corresponds to.</span></span>

<span data-ttu-id="2b728-295">table virtuelle de Hello première est la table de base hello nommé « ExampleTable » est indiqué dans hello tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="2b728-295">hello first virtual table is hello base table named “ExampleTable” is shown in hello following table.</span></span> <span data-ttu-id="2b728-296">table de base Hello contient hello mêmes données que la table de base de données d’origine hello à l’exception des collections de hello, qui sont omis dans cette table et développés dans d’autres tables virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2b728-296">hello base table contains hello same data as hello original database table except for hello collections, which are omitted from this table and expanded in other virtual tables.</span></span>

| <span data-ttu-id="2b728-297">pk_int</span><span class="sxs-lookup"><span data-stu-id="2b728-297">pk_int</span></span> | <span data-ttu-id="2b728-298">Valeur</span><span class="sxs-lookup"><span data-stu-id="2b728-298">Value</span></span> |
| --- | --- |
| <span data-ttu-id="2b728-299">1</span><span class="sxs-lookup"><span data-stu-id="2b728-299">1</span></span> |<span data-ttu-id="2b728-300">« exemple de valeur 1 »</span><span class="sxs-lookup"><span data-stu-id="2b728-300">"sample value 1"</span></span> |
| <span data-ttu-id="2b728-301">3</span><span class="sxs-lookup"><span data-stu-id="2b728-301">3</span></span> |<span data-ttu-id="2b728-302">« exemple de valeur 3 »</span><span class="sxs-lookup"><span data-stu-id="2b728-302">"sample value 3"</span></span> |

<span data-ttu-id="2b728-303">Hello tableaux suivants indiquent les tables virtuelles hello qui renormalize données hello à partir de colonnes de liste, carte et StringSet hello.</span><span class="sxs-lookup"><span data-stu-id="2b728-303">hello following tables show hello virtual tables that renormalize hello data from hello List, Map, and StringSet columns.</span></span> <span data-ttu-id="2b728-304">colonnes de Hello avec des noms qui se terminent par « _index » ou « _clés » indiquent position hello de données hello dans la liste d’origine de hello ou un mappage.</span><span class="sxs-lookup"><span data-stu-id="2b728-304">hello columns with names that end with “_index” or “_key” indicate hello position of hello data within hello original list or map.</span></span> <span data-ttu-id="2b728-305">les colonnes avec des noms qui se terminent par « _value » Hello contiennent des données de hello développé à partir de la collection de hello.</span><span class="sxs-lookup"><span data-stu-id="2b728-305">hello columns with names that end with “_value” contain hello expanded data from hello collection.</span></span>

#### <a name="table-exampletablevtlist"></a><span data-ttu-id="2b728-306">Table « ExampleTable_vt_List » :</span><span class="sxs-lookup"><span data-stu-id="2b728-306">Table “ExampleTable_vt_List”:</span></span>
| <span data-ttu-id="2b728-307">pk_int</span><span class="sxs-lookup"><span data-stu-id="2b728-307">pk_int</span></span> | <span data-ttu-id="2b728-308">List_index</span><span class="sxs-lookup"><span data-stu-id="2b728-308">List_index</span></span> | <span data-ttu-id="2b728-309">List_value</span><span class="sxs-lookup"><span data-stu-id="2b728-309">List_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2b728-310">1</span><span class="sxs-lookup"><span data-stu-id="2b728-310">1</span></span> |<span data-ttu-id="2b728-311">0</span><span class="sxs-lookup"><span data-stu-id="2b728-311">0</span></span> |<span data-ttu-id="2b728-312">1</span><span class="sxs-lookup"><span data-stu-id="2b728-312">1</span></span> |
| <span data-ttu-id="2b728-313">1</span><span class="sxs-lookup"><span data-stu-id="2b728-313">1</span></span> |<span data-ttu-id="2b728-314">1</span><span class="sxs-lookup"><span data-stu-id="2b728-314">1</span></span> |<span data-ttu-id="2b728-315">2</span><span class="sxs-lookup"><span data-stu-id="2b728-315">2</span></span> |
| <span data-ttu-id="2b728-316">1</span><span class="sxs-lookup"><span data-stu-id="2b728-316">1</span></span> |<span data-ttu-id="2b728-317">2</span><span class="sxs-lookup"><span data-stu-id="2b728-317">2</span></span> |<span data-ttu-id="2b728-318">3</span><span class="sxs-lookup"><span data-stu-id="2b728-318">3</span></span> |
| <span data-ttu-id="2b728-319">3</span><span class="sxs-lookup"><span data-stu-id="2b728-319">3</span></span> |<span data-ttu-id="2b728-320">0</span><span class="sxs-lookup"><span data-stu-id="2b728-320">0</span></span> |<span data-ttu-id="2b728-321">100</span><span class="sxs-lookup"><span data-stu-id="2b728-321">100</span></span> |
| <span data-ttu-id="2b728-322">3</span><span class="sxs-lookup"><span data-stu-id="2b728-322">3</span></span> |<span data-ttu-id="2b728-323">1</span><span class="sxs-lookup"><span data-stu-id="2b728-323">1</span></span> |<span data-ttu-id="2b728-324">101</span><span class="sxs-lookup"><span data-stu-id="2b728-324">101</span></span> |
| <span data-ttu-id="2b728-325">3</span><span class="sxs-lookup"><span data-stu-id="2b728-325">3</span></span> |<span data-ttu-id="2b728-326">2</span><span class="sxs-lookup"><span data-stu-id="2b728-326">2</span></span> |<span data-ttu-id="2b728-327">102</span><span class="sxs-lookup"><span data-stu-id="2b728-327">102</span></span> |
| <span data-ttu-id="2b728-328">3</span><span class="sxs-lookup"><span data-stu-id="2b728-328">3</span></span> |<span data-ttu-id="2b728-329">3</span><span class="sxs-lookup"><span data-stu-id="2b728-329">3</span></span> |<span data-ttu-id="2b728-330">103</span><span class="sxs-lookup"><span data-stu-id="2b728-330">103</span></span> |

#### <a name="table-exampletablevtmap"></a><span data-ttu-id="2b728-331">Table « ExampleTable_vt_List » :</span><span class="sxs-lookup"><span data-stu-id="2b728-331">Table “ExampleTable_vt_Map”:</span></span>
| <span data-ttu-id="2b728-332">pk_int</span><span class="sxs-lookup"><span data-stu-id="2b728-332">pk_int</span></span> | <span data-ttu-id="2b728-333">Map_key</span><span class="sxs-lookup"><span data-stu-id="2b728-333">Map_key</span></span> | <span data-ttu-id="2b728-334">Map_value</span><span class="sxs-lookup"><span data-stu-id="2b728-334">Map_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2b728-335">1</span><span class="sxs-lookup"><span data-stu-id="2b728-335">1</span></span> |<span data-ttu-id="2b728-336">S1</span><span class="sxs-lookup"><span data-stu-id="2b728-336">S1</span></span> |<span data-ttu-id="2b728-337">Un </span><span class="sxs-lookup"><span data-stu-id="2b728-337">A</span></span> |
| <span data-ttu-id="2b728-338">1</span><span class="sxs-lookup"><span data-stu-id="2b728-338">1</span></span> |<span data-ttu-id="2b728-339">S2</span><span class="sxs-lookup"><span data-stu-id="2b728-339">S2</span></span> |<span data-ttu-id="2b728-340">b</span><span class="sxs-lookup"><span data-stu-id="2b728-340">b</span></span> |
| <span data-ttu-id="2b728-341">3</span><span class="sxs-lookup"><span data-stu-id="2b728-341">3</span></span> |<span data-ttu-id="2b728-342">S1</span><span class="sxs-lookup"><span data-stu-id="2b728-342">S1</span></span> |<span data-ttu-id="2b728-343">t</span><span class="sxs-lookup"><span data-stu-id="2b728-343">t</span></span> |

#### <a name="table-exampletablevtstringset"></a><span data-ttu-id="2b728-344">Table « ExampleTable_vt_List » :</span><span class="sxs-lookup"><span data-stu-id="2b728-344">Table “ExampleTable_vt_StringSet”:</span></span>
| <span data-ttu-id="2b728-345">pk_int</span><span class="sxs-lookup"><span data-stu-id="2b728-345">pk_int</span></span> | <span data-ttu-id="2b728-346">StringSet_value</span><span class="sxs-lookup"><span data-stu-id="2b728-346">StringSet_value</span></span> |
| --- | --- |
| <span data-ttu-id="2b728-347">1</span><span class="sxs-lookup"><span data-stu-id="2b728-347">1</span></span> |<span data-ttu-id="2b728-348">Un </span><span class="sxs-lookup"><span data-stu-id="2b728-348">A</span></span> |
| <span data-ttu-id="2b728-349">1</span><span class="sxs-lookup"><span data-stu-id="2b728-349">1</span></span> |<span data-ttu-id="2b728-350">b</span><span class="sxs-lookup"><span data-stu-id="2b728-350">B</span></span> |
| <span data-ttu-id="2b728-351">1</span><span class="sxs-lookup"><span data-stu-id="2b728-351">1</span></span> |<span data-ttu-id="2b728-352">C</span><span class="sxs-lookup"><span data-stu-id="2b728-352">C</span></span> |
| <span data-ttu-id="2b728-353">3</span><span class="sxs-lookup"><span data-stu-id="2b728-353">3</span></span> |<span data-ttu-id="2b728-354">Un </span><span class="sxs-lookup"><span data-stu-id="2b728-354">A</span></span> |
| <span data-ttu-id="2b728-355">3</span><span class="sxs-lookup"><span data-stu-id="2b728-355">3</span></span> |<span data-ttu-id="2b728-356">E</span><span class="sxs-lookup"><span data-stu-id="2b728-356">E</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="2b728-357">Mapper les colonnes de source toosink</span><span class="sxs-lookup"><span data-stu-id="2b728-357">Map source toosink columns</span></span>
<span data-ttu-id="2b728-358">toolearn sur le mappage des colonnes dans toocolumns du jeu de données source dans le jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="2b728-358">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="2b728-359">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="2b728-359">Repeatable read from relational sources</span></span>
<span data-ttu-id="2b728-360">Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="2b728-360">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="2b728-361">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="2b728-361">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="2b728-362">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="2b728-362">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="2b728-363">Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée.</span><span class="sxs-lookup"><span data-stu-id="2b728-363">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="2b728-364">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="2b728-364">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="2b728-365">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="2b728-365">Performance and Tuning</span></span>
<span data-ttu-id="2b728-366">Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="2b728-366">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
