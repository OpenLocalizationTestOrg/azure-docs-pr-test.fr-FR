---
title: "données aaaMove MongoDB à l’aide de la fabrique de données | Documents Microsoft"
description: "Découvrez comment toomove données MongoDB de base de données à l’aide d’Azure Data Factory."
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
ms.openlocfilehash: 154e85712f27b978976c7499c43dde9429f124c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a><span data-ttu-id="141ee-103">Déplacer des données depuis MongoDB à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="141ee-103">Move data From MongoDB using Azure Data Factory</span></span>
<span data-ttu-id="141ee-104">Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory à partir d’une base de données locale MongoDB.</span><span class="sxs-lookup"><span data-stu-id="141ee-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises MongoDB database.</span></span> <span data-ttu-id="141ee-105">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="141ee-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="141ee-106">Vous pouvez copier les données d’une banque de données locale MongoDB données magasin tooany pris en charge récepteur.</span><span class="sxs-lookup"><span data-stu-id="141ee-106">You can copy data from an on-premises MongoDB data store tooany supported sink data store.</span></span> <span data-ttu-id="141ee-107">Pour une liste de données pris en charge des magasins récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="141ee-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="141ee-108">Fabrique de données prend en charge uniquement le déplacement tooother les magasins de données du magasin de données à partir de données MongoDB, mais ne pas pour déplacer des données d’une autre banque de données MongoDB des tooan de magasins de données.</span><span class="sxs-lookup"><span data-stu-id="141ee-108">Data factory currently supports only moving data from a MongoDB data store tooother data stores, but not for moving data from other data stores tooan MongoDB datastore.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="141ee-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="141ee-109">Prerequisites</span></span>
<span data-ttu-id="141ee-110">Pour hello Azure Data Factory service toobe tooconnect en mesure de tooyour MongoDB base de données locale, vous devez installer hello suivant des composants :</span><span class="sxs-lookup"><span data-stu-id="141ee-110">For hello Azure Data Factory service toobe able tooconnect tooyour on-premises MongoDB database, you must install hello following components:</span></span>

- <span data-ttu-id="141ee-111">Versions MongoDB prises en charge : 2.4, 2.6, 3.0 et 3.2.</span><span class="sxs-lookup"><span data-stu-id="141ee-111">Supported MongoDB versions are:  2.4, 2.6, 3.0, and 3.2.</span></span>
- <span data-ttu-id="141ee-112">Passerelle de gestion des données sur hello même machine cette base de données hôtes hello ou sur un tooavoid machine distincte en concurrence pour les ressources de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="141ee-112">Data Management Gateway on hello same machine that hosts hello database or on a separate machine tooavoid competing for resources with hello database.</span></span> <span data-ttu-id="141ee-113">Passerelle de gestion des données est un logiciel qui se connecte des services de toocloud de sources de données sur site de manière sécurisée et gérée.</span><span class="sxs-lookup"><span data-stu-id="141ee-113">Data Management Gateway is a software that connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="141ee-114">Consultez l’article [Passerelle de gestion des données](data-factory-data-management-gateway.md) pour obtenir des informations détaillées sur la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="141ee-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="141ee-115">Consultez [déplacer des données locales toocloud](data-factory-move-data-between-onprem-and-cloud.md) article pour obtenir des instructions sur la configuration de passerelle de hello données toomove de pipeline de données.</span><span class="sxs-lookup"><span data-stu-id="141ee-115">See [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

    <span data-ttu-id="141ee-116">Lorsque vous installez la passerelle de hello, il installe automatiquement un tooMongoDB tooconnect du pilote utilisé Microsoft MongoDB ODBC.</span><span class="sxs-lookup"><span data-stu-id="141ee-116">When you install hello gateway, it automatically installs a Microsoft MongoDB ODBC driver used tooconnect tooMongoDB.</span></span>

    > [!NOTE]
    > <span data-ttu-id="141ee-117">Vous devez toouse hello passerelle tooconnect tooMongoDB même s’il est hébergé dans les machines virtuelles Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="141ee-117">You need toouse hello gateway tooconnect tooMongoDB even if it is hosted in Azure IaaS VMs.</span></span> <span data-ttu-id="141ee-118">Si vous essayez d’instance de tooan tooconnect de MongoDB hébergé dans le cloud, vous pouvez également installer une instance de passerelle hello Bonjour IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="141ee-118">If you are trying tooconnect tooan instance of MongoDB hosted in cloud, you can also install hello gateway instance in hello IaaS VM.</span></span>

## <a name="getting-started"></a><span data-ttu-id="141ee-119">Prise en main</span><span class="sxs-lookup"><span data-stu-id="141ee-119">Getting started</span></span>
<span data-ttu-id="141ee-120">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données MongoDB local à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="141ee-120">You can create a pipeline with a copy activity that moves data from an on-premises MongoDB data store by using different tools/APIs.</span></span>

<span data-ttu-id="141ee-121">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="141ee-121">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="141ee-122">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="141ee-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="141ee-123">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="141ee-123">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="141ee-124">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="141ee-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="141ee-125">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="141ee-125">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="141ee-126">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="141ee-126">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="141ee-127">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="141ee-127">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="141ee-128">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="141ee-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="141ee-129">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="141ee-129">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="141ee-130">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="141ee-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="141ee-131">Pour voir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont des données à partir d’une banque de données locale MongoDB toocopy utilisés, [exemple de JSON : copier des données à partir de MongoDB tooAzure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="141ee-131">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises MongoDB data store, see [JSON example: Copy data from MongoDB tooAzure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="141ee-132">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifiques tooMongoDB source :</span><span class="sxs-lookup"><span data-stu-id="141ee-132">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooMongoDB source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="141ee-133">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="141ee-133">Linked service properties</span></span>
<span data-ttu-id="141ee-134">Hello tableau suivant fournit la description pour les éléments JSON spécifiques trop**OnPremisesMongoDB** service lié.</span><span class="sxs-lookup"><span data-stu-id="141ee-134">hello following table provides description for JSON elements specific too**OnPremisesMongoDB** linked service.</span></span>

| <span data-ttu-id="141ee-135">Propriété</span><span class="sxs-lookup"><span data-stu-id="141ee-135">Property</span></span> | <span data-ttu-id="141ee-136">Description</span><span class="sxs-lookup"><span data-stu-id="141ee-136">Description</span></span> | <span data-ttu-id="141ee-137">Requis</span><span class="sxs-lookup"><span data-stu-id="141ee-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="141ee-138">type</span><span class="sxs-lookup"><span data-stu-id="141ee-138">type</span></span> |<span data-ttu-id="141ee-139">propriété de type Hello doit indiquer : **OnPremisesMongoDb**</span><span class="sxs-lookup"><span data-stu-id="141ee-139">hello type property must be set to: **OnPremisesMongoDb**</span></span> |<span data-ttu-id="141ee-140">Oui</span><span class="sxs-lookup"><span data-stu-id="141ee-140">Yes</span></span> |
| <span data-ttu-id="141ee-141">server</span><span class="sxs-lookup"><span data-stu-id="141ee-141">server</span></span> |<span data-ttu-id="141ee-142">Nom hôte ou adresse IP du serveur de MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="141ee-142">IP address or host name of hello MongoDB server.</span></span> |<span data-ttu-id="141ee-143">Oui</span><span class="sxs-lookup"><span data-stu-id="141ee-143">Yes</span></span> |
| <span data-ttu-id="141ee-144">port</span><span class="sxs-lookup"><span data-stu-id="141ee-144">port</span></span> |<span data-ttu-id="141ee-145">Le port TCP qui hello MongoDB serveur utilise toolisten pour les connexions client.</span><span class="sxs-lookup"><span data-stu-id="141ee-145">TCP port that hello MongoDB server uses toolisten for client connections.</span></span> |<span data-ttu-id="141ee-146">Facultatif, valeur par défaut : 27017</span><span class="sxs-lookup"><span data-stu-id="141ee-146">Optional, default value: 27017</span></span> |
| <span data-ttu-id="141ee-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="141ee-147">authenticationType</span></span> |<span data-ttu-id="141ee-148">De base ou anonyme.</span><span class="sxs-lookup"><span data-stu-id="141ee-148">Basic, or Anonymous.</span></span> |<span data-ttu-id="141ee-149">Oui</span><span class="sxs-lookup"><span data-stu-id="141ee-149">Yes</span></span> |
| <span data-ttu-id="141ee-150">username</span><span class="sxs-lookup"><span data-stu-id="141ee-150">username</span></span> |<span data-ttu-id="141ee-151">Tooaccess du compte utilisateur MongoDB.</span><span class="sxs-lookup"><span data-stu-id="141ee-151">User account tooaccess MongoDB.</span></span> |<span data-ttu-id="141ee-152">Oui (si l’authentification de base est utilisée).</span><span class="sxs-lookup"><span data-stu-id="141ee-152">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="141ee-153">password</span><span class="sxs-lookup"><span data-stu-id="141ee-153">password</span></span> |<span data-ttu-id="141ee-154">Mot de passe utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="141ee-154">Password for hello user.</span></span> |<span data-ttu-id="141ee-155">Oui (si l’authentification de base est utilisée).</span><span class="sxs-lookup"><span data-stu-id="141ee-155">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="141ee-156">authSource</span><span class="sxs-lookup"><span data-stu-id="141ee-156">authSource</span></span> |<span data-ttu-id="141ee-157">Nom de la base de données MongoDB hello que vous souhaitez toouse toocheck vos informations d’identification pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="141ee-157">Name of hello MongoDB database that you want toouse toocheck your credentials for authentication.</span></span> |<span data-ttu-id="141ee-158">Facultatif (si l’authentification de base est utilisée).</span><span class="sxs-lookup"><span data-stu-id="141ee-158">Optional (if basic authentication is used).</span></span> <span data-ttu-id="141ee-159">par défaut : utilise le compte d’administrateur hello et de la base de données de hello spécifié à l’aide de la propriété databaseName.</span><span class="sxs-lookup"><span data-stu-id="141ee-159">default: uses hello admin account and hello database specified using databaseName property.</span></span> |
| <span data-ttu-id="141ee-160">databaseName</span><span class="sxs-lookup"><span data-stu-id="141ee-160">databaseName</span></span> |<span data-ttu-id="141ee-161">Nom de la base de données MongoDB hello que vous souhaitez tooaccess.</span><span class="sxs-lookup"><span data-stu-id="141ee-161">Name of hello MongoDB database that you want tooaccess.</span></span> |<span data-ttu-id="141ee-162">Oui</span><span class="sxs-lookup"><span data-stu-id="141ee-162">Yes</span></span> |
| <span data-ttu-id="141ee-163">gatewayName</span><span class="sxs-lookup"><span data-stu-id="141ee-163">gatewayName</span></span> |<span data-ttu-id="141ee-164">Nom de la passerelle hello qui accède au magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="141ee-164">Name of hello gateway that accesses hello data store.</span></span> |<span data-ttu-id="141ee-165">Oui</span><span class="sxs-lookup"><span data-stu-id="141ee-165">Yes</span></span> |
| <span data-ttu-id="141ee-166">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="141ee-166">encryptedCredential</span></span> |<span data-ttu-id="141ee-167">Informations d’identification chiffrées par la passerelle.</span><span class="sxs-lookup"><span data-stu-id="141ee-167">Credential encrypted by gateway.</span></span> |<span data-ttu-id="141ee-168">Facultatif</span><span class="sxs-lookup"><span data-stu-id="141ee-168">Optional</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="141ee-169">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="141ee-169">Dataset properties</span></span>
<span data-ttu-id="141ee-170">Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="141ee-170">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="141ee-171">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="141ee-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="141ee-172">Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="141ee-172">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="141ee-173">jeu de données de type Hello typeProperties section **MongoDbCollection** a hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="141ee-173">hello typeProperties section for dataset of type **MongoDbCollection** has hello following properties:</span></span>

| <span data-ttu-id="141ee-174">Propriété</span><span class="sxs-lookup"><span data-stu-id="141ee-174">Property</span></span> | <span data-ttu-id="141ee-175">Description</span><span class="sxs-lookup"><span data-stu-id="141ee-175">Description</span></span> | <span data-ttu-id="141ee-176">Requis</span><span class="sxs-lookup"><span data-stu-id="141ee-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="141ee-177">collectionName</span><span class="sxs-lookup"><span data-stu-id="141ee-177">collectionName</span></span> |<span data-ttu-id="141ee-178">Nom de collection hello dans la base de données MongoDB.</span><span class="sxs-lookup"><span data-stu-id="141ee-178">Name of hello collection in MongoDB database.</span></span> |<span data-ttu-id="141ee-179">Oui</span><span class="sxs-lookup"><span data-stu-id="141ee-179">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="141ee-180">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="141ee-180">Copy activity properties</span></span>
<span data-ttu-id="141ee-181">Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="141ee-181">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="141ee-182">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="141ee-182">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="141ee-183">Propriétés disponibles dans hello **typeProperties** section de l’activité de hello sur hello autre part varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="141ee-183">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="141ee-184">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="141ee-184">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="141ee-185">Lorsque la source de hello est de type **MongoDbSource** hello propriétés suivantes est disponible dans la section de typeProperties :</span><span class="sxs-lookup"><span data-stu-id="141ee-185">When hello source is of type **MongoDbSource** hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="141ee-186">Propriété</span><span class="sxs-lookup"><span data-stu-id="141ee-186">Property</span></span> | <span data-ttu-id="141ee-187">Description</span><span class="sxs-lookup"><span data-stu-id="141ee-187">Description</span></span> | <span data-ttu-id="141ee-188">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="141ee-188">Allowed values</span></span> | <span data-ttu-id="141ee-189">Requis</span><span class="sxs-lookup"><span data-stu-id="141ee-189">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="141ee-190">query</span><span class="sxs-lookup"><span data-stu-id="141ee-190">query</span></span> |<span data-ttu-id="141ee-191">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="141ee-191">Use hello custom query tooread data.</span></span> |<span data-ttu-id="141ee-192">Chaîne de requête SQL-92.</span><span class="sxs-lookup"><span data-stu-id="141ee-192">SQL-92 query string.</span></span> <span data-ttu-id="141ee-193">Par exemple : select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="141ee-193">For example: select * from MyTable.</span></span> |<span data-ttu-id="141ee-194">Non (si **collectionName** du **jeu de données** est spécifié)</span><span class="sxs-lookup"><span data-stu-id="141ee-194">No (if **collectionName** of **dataset** is specified)</span></span> |



## <a name="json-example-copy-data-from-mongodb-tooazure-blob"></a><span data-ttu-id="141ee-195">Exemple de JSON : copier des données à partir de MongoDB tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="141ee-195">JSON example: Copy data from MongoDB tooAzure Blob</span></span>
<span data-ttu-id="141ee-196">Cet exemple fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="141ee-196">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="141ee-197">Il montre comment toocopy des données à partir d’un tooan de MongoDB local stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="141ee-197">It shows how toocopy data from an on-premises MongoDB tooan Azure Blob Storage.</span></span> <span data-ttu-id="141ee-198">Toutefois, les données peuvent être copié tooany de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="141ee-198">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="141ee-199">exemple Hello a hello suivant des entités de fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="141ee-199">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="141ee-200">Un service lié de type [OnPremisesMongoDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="141ee-200">A linked service of type [OnPremisesMongoDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="141ee-201">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="141ee-201">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="141ee-202">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [MongoDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="141ee-202">An input [dataset](data-factory-create-datasets.md) of type [MongoDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="141ee-203">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="141ee-203">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="141ee-204">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [MongoDbSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="141ee-204">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [MongoDbSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="141ee-205">exemple Hello copie des données à partir d’un résultat de requête dans l’objet blob tooa de base de données MongoDB toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="141ee-205">hello sample copies data from a query result in MongoDB database tooa blob every hour.</span></span> <span data-ttu-id="141ee-206">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="141ee-206">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="141ee-207">Dans un premier temps, le programme d’installation passerelle de gestion des données hello conformément aux instructions hello Bonjour [passerelle de gestion des données](data-factory-data-management-gateway.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="141ee-207">As a first step, setup hello data management gateway as per hello instructions in hello [Data Management Gateway](data-factory-data-management-gateway.md) article.</span></span>

<span data-ttu-id="141ee-208">**Service lié MongoDB :**</span><span class="sxs-lookup"><span data-stu-id="141ee-208">**MongoDB linked service:**</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",  
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

<span data-ttu-id="141ee-209">**Service lié Azure Storage :**</span><span class="sxs-lookup"><span data-stu-id="141ee-209">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="141ee-210">**Jeu de données d’entrée MongoDB :** définissant « external » : « true » informe service Data Factory de hello cette table hello est la fabrique de données externe toohello et n’est pas générée par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="141ee-210">**MongoDB input dataset:** Setting “external”: ”true” informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="141ee-211">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="141ee-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="141ee-212">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="141ee-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="141ee-213">chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="141ee-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="141ee-214">chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="141ee-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="141ee-215">**Activité de copie dans un pipeline avec une source MongoDB et un récepteur d’objets blob :**</span><span class="sxs-lookup"><span data-stu-id="141ee-215">**Copy activity in a pipeline with MongoDB source and Blob sink:**</span></span>

<span data-ttu-id="141ee-216">pipeline de Hello contient une activité de copie qui est hello toouse configuré au-dessus de jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="141ee-216">hello pipeline contains a Copy Activity that is configured toouse hello above input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="141ee-217">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**MongoDbSource** et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="141ee-217">In hello pipeline JSON definition, hello **source** type is set too**MongoDbSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="141ee-218">la requête SQL Hello spécifiée pour hello **requête** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.</span><span class="sxs-lookup"><span data-stu-id="141ee-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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


## <a name="schema-by-data-factory"></a><span data-ttu-id="141ee-219">Schéma par Data Factory</span><span class="sxs-lookup"><span data-stu-id="141ee-219">Schema by Data Factory</span></span>
<span data-ttu-id="141ee-220">Service de fabrique de données Azure déduit le schéma à partir d’une collection de MongoDB en utilisant des documents de hello 100 dernières de collection de hello.</span><span class="sxs-lookup"><span data-stu-id="141ee-220">Azure Data Factory service infers schema from a MongoDB collection by using hello latest 100 documents in hello collection.</span></span> <span data-ttu-id="141ee-221">Si ces 100 documents ne contiennent pas de schéma complet, certaines colonnes peuvent être ignorés pendant l’opération de copie hello.</span><span class="sxs-lookup"><span data-stu-id="141ee-221">If these 100 documents do not contain full schema, some columns may be ignored during hello copy operation.</span></span>

## <a name="type-mapping-for-mongodb"></a><span data-ttu-id="141ee-222">Mappage de type pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="141ee-222">Type mapping for MongoDB</span></span>
<span data-ttu-id="141ee-223">Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, l’activité de copie effectue les conversions de type automatique à partir des types de sources de toosink types avec hello approche de l’étape 2 :</span><span class="sxs-lookup"><span data-stu-id="141ee-223">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="141ee-224">Convertir à partir de la source native types too.NET type</span><span class="sxs-lookup"><span data-stu-id="141ee-224">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="141ee-225">Conversion de type de récepteur de toonative de type .NET</span><span class="sxs-lookup"><span data-stu-id="141ee-225">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="141ee-226">Lorsque vous déplacez hello tooMongoDB de données suivant les mappages sont utilisés à partir des types de too.NET types MongoDB.</span><span class="sxs-lookup"><span data-stu-id="141ee-226">When moving data tooMongoDB hello following mappings are used from MongoDB types too.NET types.</span></span>

| <span data-ttu-id="141ee-227">Type MongoDB</span><span class="sxs-lookup"><span data-stu-id="141ee-227">MongoDB type</span></span> | <span data-ttu-id="141ee-228">Type de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="141ee-228">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="141ee-229">Fichier binaire</span><span class="sxs-lookup"><span data-stu-id="141ee-229">Binary</span></span> |<span data-ttu-id="141ee-230">Byte[]</span><span class="sxs-lookup"><span data-stu-id="141ee-230">Byte[]</span></span> |
| <span data-ttu-id="141ee-231">Boolean</span><span class="sxs-lookup"><span data-stu-id="141ee-231">Boolean</span></span> |<span data-ttu-id="141ee-232">Boolean</span><span class="sxs-lookup"><span data-stu-id="141ee-232">Boolean</span></span> |
| <span data-ttu-id="141ee-233">Date</span><span class="sxs-lookup"><span data-stu-id="141ee-233">Date</span></span> |<span data-ttu-id="141ee-234">DateTime</span><span class="sxs-lookup"><span data-stu-id="141ee-234">DateTime</span></span> |
| <span data-ttu-id="141ee-235">NumberDouble</span><span class="sxs-lookup"><span data-stu-id="141ee-235">NumberDouble</span></span> |<span data-ttu-id="141ee-236">Double</span><span class="sxs-lookup"><span data-stu-id="141ee-236">Double</span></span> |
| <span data-ttu-id="141ee-237">NumberInt</span><span class="sxs-lookup"><span data-stu-id="141ee-237">NumberInt</span></span> |<span data-ttu-id="141ee-238">Int32</span><span class="sxs-lookup"><span data-stu-id="141ee-238">Int32</span></span> |
| <span data-ttu-id="141ee-239">NumberLong</span><span class="sxs-lookup"><span data-stu-id="141ee-239">NumberLong</span></span> |<span data-ttu-id="141ee-240">Int64</span><span class="sxs-lookup"><span data-stu-id="141ee-240">Int64</span></span> |
| <span data-ttu-id="141ee-241">ObjectID</span><span class="sxs-lookup"><span data-stu-id="141ee-241">ObjectID</span></span> |<span data-ttu-id="141ee-242">Chaîne</span><span class="sxs-lookup"><span data-stu-id="141ee-242">String</span></span> |
| <span data-ttu-id="141ee-243">Chaîne</span><span class="sxs-lookup"><span data-stu-id="141ee-243">String</span></span> |<span data-ttu-id="141ee-244">Chaîne</span><span class="sxs-lookup"><span data-stu-id="141ee-244">String</span></span> |
| <span data-ttu-id="141ee-245">UUID</span><span class="sxs-lookup"><span data-stu-id="141ee-245">UUID</span></span> |<span data-ttu-id="141ee-246">Guid</span><span class="sxs-lookup"><span data-stu-id="141ee-246">Guid</span></span> |
| <span data-ttu-id="141ee-247">Object</span><span class="sxs-lookup"><span data-stu-id="141ee-247">Object</span></span> |<span data-ttu-id="141ee-248">Renormalisé dans des colonnes aplaties avec « _ » comme séparateur imbriqué</span><span class="sxs-lookup"><span data-stu-id="141ee-248">Renormalized into flatten columns with “_” as nested separator</span></span> |

> [!NOTE]
> <span data-ttu-id="141ee-249">toolearn sur la prise en charge des tableaux à l’aide de tables virtuelles, consultez trop[prend en charge pour les types complexes à l’aide de tables virtuelles](#support-for-complex-types-using-virtual-tables) section ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="141ee-249">toolearn about support for arrays using virtual tables, refer too[Support for complex types using virtual tables](#support-for-complex-types-using-virtual-tables) section below.</span></span>

<span data-ttu-id="141ee-250">Actuellement, hello les types de données MongoDB suivants n’est pas prises en charge : DBPointer, JavaScript, Max/Min de clé, une Expression régulière, symbole, Timestamp, non défini</span><span class="sxs-lookup"><span data-stu-id="141ee-250">Currently, hello following MongoDB data types are not supported: DBPointer, JavaScript, Max/Min key, Regular Expression, Symbol, Timestamp, Undefined</span></span>

## <a name="support-for-complex-types-using-virtual-tables"></a><span data-ttu-id="141ee-251">Prise en charge des types complexes à l’aide de tables virtuelles</span><span class="sxs-lookup"><span data-stu-id="141ee-251">Support for complex types using virtual tables</span></span>
<span data-ttu-id="141ee-252">Azure Data Factory utilise une intégrés ODBC driver tooconnect tooand copier les données de votre base de données MongoDB.</span><span class="sxs-lookup"><span data-stu-id="141ee-252">Azure Data Factory uses a built-in ODBC driver tooconnect tooand copy data from your MongoDB database.</span></span> <span data-ttu-id="141ee-253">Pour les types complexes tels que les objets ou les tableaux avec des types différents dans les documents de hello, pilote de hello normalise nouveau des données dans des tables virtuelles correspondants.</span><span class="sxs-lookup"><span data-stu-id="141ee-253">For complex types such as arrays or objects with different types across hello documents, hello driver re-normalizes data into corresponding virtual tables.</span></span> <span data-ttu-id="141ee-254">Plus précisément, si une table contient des colonnes de ce type, les pilotes hello génère hello tables virtuelles suivantes :</span><span class="sxs-lookup"><span data-stu-id="141ee-254">Specifically, if a table contains such columns, hello driver generates hello following virtual tables:</span></span>

* <span data-ttu-id="141ee-255">A **table de base**, lequel contient hello les mêmes données que la table réelle de hello sauf pour les colonnes de type complexe hello.</span><span class="sxs-lookup"><span data-stu-id="141ee-255">A **base table**, which contains hello same data as hello real table except for hello complex type columns.</span></span> <span data-ttu-id="141ee-256">table de base Hello utilise hello même nom en tant que table réelle hello qu’elle représente.</span><span class="sxs-lookup"><span data-stu-id="141ee-256">hello base table uses hello same name as hello real table that it represents.</span></span>
* <span data-ttu-id="141ee-257">A **table virtuelle** pour chaque colonne de type complexe, qui étend les données de salutation imbriquée.</span><span class="sxs-lookup"><span data-stu-id="141ee-257">A **virtual table** for each complex type column, which expands hello nested data.</span></span> <span data-ttu-id="141ee-258">les tables virtuelles Hello sont nommées à l’aide du nom de hello de table réelle de hello, un séparateur « _ » et un nom de hello du tableau de hello ou un objet.</span><span class="sxs-lookup"><span data-stu-id="141ee-258">hello virtual tables are named using hello name of hello real table, a separator “_” and hello name of hello array or object.</span></span>

<span data-ttu-id="141ee-259">Tables virtuelles font référence à des données de toohello dans la table réelle de hello, l’activation tooaccess de pilote hello hello données dénormalisées.</span><span class="sxs-lookup"><span data-stu-id="141ee-259">Virtual tables refer toohello data in hello real table, enabling hello driver tooaccess hello denormalized data.</span></span> <span data-ttu-id="141ee-260">Consultez la section Exemple ci-dessous pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="141ee-260">See Example section below details.</span></span> <span data-ttu-id="141ee-261">Vous pouvez accéder à contenu hello des tableaux de MongoDB en interrogeant et en joignant les tables virtuelles hello.</span><span class="sxs-lookup"><span data-stu-id="141ee-261">You can access hello content of MongoDB arrays by querying and joining hello virtual tables.</span></span>

<span data-ttu-id="141ee-262">Vous pouvez utiliser hello [Assistant copie de](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively vue hello la liste des tables de base de données MongoDB, y compris les tables virtuelles hello et afficher un aperçu des données hello à l’intérieur.</span><span class="sxs-lookup"><span data-stu-id="141ee-262">You can use hello [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively view hello list of tables in MongoDB database including hello virtual tables, and preview hello data inside.</span></span> <span data-ttu-id="141ee-263">Vous pouvez également créer une requête dans l’Assistant copie de hello et toosee hello résultat de la validation.</span><span class="sxs-lookup"><span data-stu-id="141ee-263">You can also construct a query in hello Copy Wizard and validate toosee hello result.</span></span>

### <a name="example"></a><span data-ttu-id="141ee-264">Exemple</span><span class="sxs-lookup"><span data-stu-id="141ee-264">Example</span></span>
<span data-ttu-id="141ee-265">Par exemple, « ExampleTable » ci-dessous est une table MongoDB qui dispose d’une colonne avec un tableau d’objets dans chaque cellule (Factures) et d’une colonne avec un tableau de types scalaires (Évaluations).</span><span class="sxs-lookup"><span data-stu-id="141ee-265">For example, “ExampleTable” below is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.</span></span>

| <span data-ttu-id="141ee-266">_id</span><span class="sxs-lookup"><span data-stu-id="141ee-266">_id</span></span> | <span data-ttu-id="141ee-267">Nom du client</span><span class="sxs-lookup"><span data-stu-id="141ee-267">Customer Name</span></span> | <span data-ttu-id="141ee-268">Factures</span><span class="sxs-lookup"><span data-stu-id="141ee-268">Invoices</span></span> | <span data-ttu-id="141ee-269">Niveau de service</span><span class="sxs-lookup"><span data-stu-id="141ee-269">Service Level</span></span> | <span data-ttu-id="141ee-270">Évaluations</span><span class="sxs-lookup"><span data-stu-id="141ee-270">Ratings</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="141ee-271">1111</span><span class="sxs-lookup"><span data-stu-id="141ee-271">1111</span></span> |<span data-ttu-id="141ee-272">ABC</span><span class="sxs-lookup"><span data-stu-id="141ee-272">ABC</span></span> |<span data-ttu-id="141ee-273">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span><span class="sxs-lookup"><span data-stu-id="141ee-273">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span></span> |<span data-ttu-id="141ee-274">Silver</span><span class="sxs-lookup"><span data-stu-id="141ee-274">Silver</span></span> |<span data-ttu-id="141ee-275">[5,6]</span><span class="sxs-lookup"><span data-stu-id="141ee-275">[5,6]</span></span> |
| <span data-ttu-id="141ee-276">2222</span><span class="sxs-lookup"><span data-stu-id="141ee-276">2222</span></span> |<span data-ttu-id="141ee-277">XYZ</span><span class="sxs-lookup"><span data-stu-id="141ee-277">XYZ</span></span> |<span data-ttu-id="141ee-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span><span class="sxs-lookup"><span data-stu-id="141ee-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span></span> |<span data-ttu-id="141ee-279">Gold</span><span class="sxs-lookup"><span data-stu-id="141ee-279">Gold</span></span> |<span data-ttu-id="141ee-280">[1,2]</span><span class="sxs-lookup"><span data-stu-id="141ee-280">[1,2]</span></span> |

<span data-ttu-id="141ee-281">pilote de Hello génèrent plusieurs tables virtuelles toorepresent ce tableau.</span><span class="sxs-lookup"><span data-stu-id="141ee-281">hello driver would generate multiple virtual tables toorepresent this single table.</span></span> <span data-ttu-id="141ee-282">Hello première virtuel table est hello base nommé « ExampleTable », illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="141ee-282">hello first virtual table is hello base table named “ExampleTable”, shown below.</span></span> <span data-ttu-id="141ee-283">table de base Hello contient toutes les données de hello de table d’origine de hello, mais les données hello depuis des tableaux de hello a été omises sont développées dans les tables virtuelles hello.</span><span class="sxs-lookup"><span data-stu-id="141ee-283">hello base table contains all hello data of hello original table, but hello data from hello arrays has been omitted and is expanded in hello virtual tables.</span></span>

| <span data-ttu-id="141ee-284">_id</span><span class="sxs-lookup"><span data-stu-id="141ee-284">_id</span></span> | <span data-ttu-id="141ee-285">Nom du client</span><span class="sxs-lookup"><span data-stu-id="141ee-285">Customer Name</span></span> | <span data-ttu-id="141ee-286">Niveau de service</span><span class="sxs-lookup"><span data-stu-id="141ee-286">Service Level</span></span> |
| --- | --- | --- |
| <span data-ttu-id="141ee-287">1111</span><span class="sxs-lookup"><span data-stu-id="141ee-287">1111</span></span> |<span data-ttu-id="141ee-288">ABC</span><span class="sxs-lookup"><span data-stu-id="141ee-288">ABC</span></span> |<span data-ttu-id="141ee-289">Silver</span><span class="sxs-lookup"><span data-stu-id="141ee-289">Silver</span></span> |
| <span data-ttu-id="141ee-290">2222</span><span class="sxs-lookup"><span data-stu-id="141ee-290">2222</span></span> |<span data-ttu-id="141ee-291">XYZ</span><span class="sxs-lookup"><span data-stu-id="141ee-291">XYZ</span></span> |<span data-ttu-id="141ee-292">Gold</span><span class="sxs-lookup"><span data-stu-id="141ee-292">Gold</span></span> |

<span data-ttu-id="141ee-293">Hello tableaux suivants indiquent hello tables virtuelles qui représentent les tableaux d’origine de hello dans l’exemple de hello.</span><span class="sxs-lookup"><span data-stu-id="141ee-293">hello following tables show hello virtual tables that represent hello original arrays in hello example.</span></span> <span data-ttu-id="141ee-294">Ces tables contiennent les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="141ee-294">These tables contain hello following:</span></span>

* <span data-ttu-id="141ee-295">Une référence arrière toohello d’origine une colonne clé primaire toohello ligne correspondante du tableau d’origine de hello (via la colonne de _id hello)</span><span class="sxs-lookup"><span data-stu-id="141ee-295">A reference back toohello original primary key column corresponding toohello row of hello original array (via hello _id column)</span></span>
* <span data-ttu-id="141ee-296">Une indication de position hello de données hello dans le tableau d’origine de hello</span><span class="sxs-lookup"><span data-stu-id="141ee-296">An indication of hello position of hello data within hello original array</span></span>
* <span data-ttu-id="141ee-297">Hello développé des données pour chaque élément dans le tableau de hello</span><span class="sxs-lookup"><span data-stu-id="141ee-297">hello expanded data for each element within hello array</span></span>

<span data-ttu-id="141ee-298">Table « ExampleTable_Invoices » :</span><span class="sxs-lookup"><span data-stu-id="141ee-298">Table “ExampleTable_Invoices”:</span></span>

| <span data-ttu-id="141ee-299">_id</span><span class="sxs-lookup"><span data-stu-id="141ee-299">_id</span></span> | <span data-ttu-id="141ee-300">ExampleTable_Invoices_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="141ee-300">ExampleTable_Invoices_dim1_idx</span></span> | <span data-ttu-id="141ee-301">invoice_id</span><span class="sxs-lookup"><span data-stu-id="141ee-301">invoice_id</span></span> | <span data-ttu-id="141ee-302">item</span><span class="sxs-lookup"><span data-stu-id="141ee-302">item</span></span> | <span data-ttu-id="141ee-303">price</span><span class="sxs-lookup"><span data-stu-id="141ee-303">price</span></span> | <span data-ttu-id="141ee-304">Remise</span><span class="sxs-lookup"><span data-stu-id="141ee-304">Discount</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="141ee-305">1111</span><span class="sxs-lookup"><span data-stu-id="141ee-305">1111</span></span> |<span data-ttu-id="141ee-306">0</span><span class="sxs-lookup"><span data-stu-id="141ee-306">0</span></span> |<span data-ttu-id="141ee-307">123</span><span class="sxs-lookup"><span data-stu-id="141ee-307">123</span></span> |<span data-ttu-id="141ee-308">grille-pain</span><span class="sxs-lookup"><span data-stu-id="141ee-308">toaster</span></span> |<span data-ttu-id="141ee-309">456</span><span class="sxs-lookup"><span data-stu-id="141ee-309">456</span></span> |<span data-ttu-id="141ee-310">0.2</span><span class="sxs-lookup"><span data-stu-id="141ee-310">0.2</span></span> |
| <span data-ttu-id="141ee-311">1111</span><span class="sxs-lookup"><span data-stu-id="141ee-311">1111</span></span> |<span data-ttu-id="141ee-312">1</span><span class="sxs-lookup"><span data-stu-id="141ee-312">1</span></span> |<span data-ttu-id="141ee-313">124</span><span class="sxs-lookup"><span data-stu-id="141ee-313">124</span></span> |<span data-ttu-id="141ee-314">four</span><span class="sxs-lookup"><span data-stu-id="141ee-314">oven</span></span> |<span data-ttu-id="141ee-315">1235</span><span class="sxs-lookup"><span data-stu-id="141ee-315">1235</span></span> |<span data-ttu-id="141ee-316">0.2</span><span class="sxs-lookup"><span data-stu-id="141ee-316">0.2</span></span> |
| <span data-ttu-id="141ee-317">2222</span><span class="sxs-lookup"><span data-stu-id="141ee-317">2222</span></span> |<span data-ttu-id="141ee-318">0</span><span class="sxs-lookup"><span data-stu-id="141ee-318">0</span></span> |<span data-ttu-id="141ee-319">135</span><span class="sxs-lookup"><span data-stu-id="141ee-319">135</span></span> |<span data-ttu-id="141ee-320">réfrigérateur</span><span class="sxs-lookup"><span data-stu-id="141ee-320">fridge</span></span> |<span data-ttu-id="141ee-321">12543</span><span class="sxs-lookup"><span data-stu-id="141ee-321">12543</span></span> |<span data-ttu-id="141ee-322">0.0</span><span class="sxs-lookup"><span data-stu-id="141ee-322">0.0</span></span> |

<span data-ttu-id="141ee-323">Table « ExampleTable_Ratings » :</span><span class="sxs-lookup"><span data-stu-id="141ee-323">Table “ExampleTable_Ratings”:</span></span>

| <span data-ttu-id="141ee-324">_id</span><span class="sxs-lookup"><span data-stu-id="141ee-324">_id</span></span> | <span data-ttu-id="141ee-325">ExampleTable_Ratings_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="141ee-325">ExampleTable_Ratings_dim1_idx</span></span> | <span data-ttu-id="141ee-326">ExampleTable_Ratings</span><span class="sxs-lookup"><span data-stu-id="141ee-326">ExampleTable_Ratings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="141ee-327">1111</span><span class="sxs-lookup"><span data-stu-id="141ee-327">1111</span></span> |<span data-ttu-id="141ee-328">0</span><span class="sxs-lookup"><span data-stu-id="141ee-328">0</span></span> |<span data-ttu-id="141ee-329">5</span><span class="sxs-lookup"><span data-stu-id="141ee-329">5</span></span> |
| <span data-ttu-id="141ee-330">1111</span><span class="sxs-lookup"><span data-stu-id="141ee-330">1111</span></span> |<span data-ttu-id="141ee-331">1</span><span class="sxs-lookup"><span data-stu-id="141ee-331">1</span></span> |<span data-ttu-id="141ee-332">6</span><span class="sxs-lookup"><span data-stu-id="141ee-332">6</span></span> |
| <span data-ttu-id="141ee-333">2222</span><span class="sxs-lookup"><span data-stu-id="141ee-333">2222</span></span> |<span data-ttu-id="141ee-334">0</span><span class="sxs-lookup"><span data-stu-id="141ee-334">0</span></span> |<span data-ttu-id="141ee-335">1</span><span class="sxs-lookup"><span data-stu-id="141ee-335">1</span></span> |
| <span data-ttu-id="141ee-336">2222</span><span class="sxs-lookup"><span data-stu-id="141ee-336">2222</span></span> |<span data-ttu-id="141ee-337">1</span><span class="sxs-lookup"><span data-stu-id="141ee-337">1</span></span> |<span data-ttu-id="141ee-338">2</span><span class="sxs-lookup"><span data-stu-id="141ee-338">2</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="141ee-339">Mapper les colonnes de source toosink</span><span class="sxs-lookup"><span data-stu-id="141ee-339">Map source toosink columns</span></span>
<span data-ttu-id="141ee-340">toolearn sur le mappage des colonnes dans toocolumns du jeu de données source dans le jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="141ee-340">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="141ee-341">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="141ee-341">Repeatable read from relational sources</span></span>
<span data-ttu-id="141ee-342">Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="141ee-342">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="141ee-343">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="141ee-343">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="141ee-344">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="141ee-344">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="141ee-345">Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée.</span><span class="sxs-lookup"><span data-stu-id="141ee-345">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="141ee-346">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="141ee-346">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="141ee-347">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="141ee-347">Performance and Tuning</span></span>
<span data-ttu-id="141ee-348">Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="141ee-348">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="141ee-349">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="141ee-349">Next Steps</span></span>
<span data-ttu-id="141ee-350">Consultez [déplacement des données entre locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) article pour obtenir des instructions pour la création d’un pipeline de données qui déplace la banque de données Azure tooan du magasin de données à partir de des données locales.</span><span class="sxs-lookup"><span data-stu-id="141ee-350">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions for creating a data pipeline that moves data from an on-premises data store tooan Azure data store.</span></span>
