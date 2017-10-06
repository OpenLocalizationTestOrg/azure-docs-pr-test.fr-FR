---
title: "aaaMove des données à partir de Sybase à l’aide d’Azure Data Factory | Documents Microsoft"
description: "En savoir plus sur la façon de toomove les données à partir de la base de données Sybase à l’aide d’Azure Data Factory."
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
ms.openlocfilehash: ad003ec502028d56db9570fe08af329eb5b71817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a><span data-ttu-id="06071-103">Déplacer des données depuis Sybase à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="06071-103">Move data from Sybase using Azure Data Factory</span></span>
<span data-ttu-id="06071-104">Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory à partir d’une base de données Sybase locale.</span><span class="sxs-lookup"><span data-stu-id="06071-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Sybase database.</span></span> <span data-ttu-id="06071-105">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="06071-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="06071-106">Vous pouvez copier les données d’une banque de données locale Sybase tooany pris en charge données magasin récepteur.</span><span class="sxs-lookup"><span data-stu-id="06071-106">You can copy data from an on-premises Sybase data store tooany supported sink data store.</span></span> <span data-ttu-id="06071-107">Pour une liste de données pris en charge des magasins récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="06071-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="06071-108">Fabrique de données prend en charge uniquement le déplacement tooother les magasins de données du magasin de données à partir de données Sybase, mais ne pas pour déplacer des données d’une autre banque de données Sybase tooa données magasins.</span><span class="sxs-lookup"><span data-stu-id="06071-108">Data factory currently supports only moving data from a Sybase data store tooother data stores, but not for moving data from other data stores tooa Sybase data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="06071-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="06071-109">Prerequisites</span></span>
<span data-ttu-id="06071-110">Service de fabrique de données prend en charge des sources de Sybase tooon local qui se connecte à l’aide de la passerelle de gestion des données de hello.</span><span class="sxs-lookup"><span data-stu-id="06071-110">Data Factory service supports connecting tooon-premises Sybase sources using hello Data Management Gateway.</span></span> <span data-ttu-id="06071-111">Consultez [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn l’article sur la passerelle de gestion des données et des instructions détaillées sur la configuration de passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="06071-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="06071-112">Passerelle est requise même si la base de données Sybase hello est hébergé dans une machine virtuelle IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="06071-112">Gateway is required even if hello Sybase database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="06071-113">Vous pouvez installer la passerelle de hello sur hello même IaaS VM sous forme de données de hello stocker ou sur un ordinateur différent virtuel tant que passerelle de hello peuvent se connecter toohello de base de données.</span><span class="sxs-lookup"><span data-stu-id="06071-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="06071-114">Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.</span><span class="sxs-lookup"><span data-stu-id="06071-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="06071-115">Versions prises en charge et installation</span><span class="sxs-lookup"><span data-stu-id="06071-115">Supported versions and installation</span></span>
<span data-ttu-id="06071-116">Pour toohello tooconnect de passerelle de gestion des données de la base de données Sybase, vous devez tooinstall hello [fournisseur de données pour Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 ou ci-dessus sur hello le même système que hello passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="06071-116">For Data Management Gateway tooconnect toohello Sybase Database, you need tooinstall hello [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="06071-117">Sybase (version 16 et ultérieures) est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="06071-117">Sybase version 16 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="06071-118">Prise en main</span><span class="sxs-lookup"><span data-stu-id="06071-118">Getting started</span></span>
<span data-ttu-id="06071-119">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données Cassandra local à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="06071-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="06071-120">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="06071-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="06071-121">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="06071-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="06071-122">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="06071-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="06071-123">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="06071-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="06071-124">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="06071-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="06071-125">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="06071-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="06071-126">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="06071-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="06071-127">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="06071-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="06071-128">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="06071-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="06071-129">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="06071-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="06071-130">Pour voir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données à partir d’une banque de données Sybase locale, [exemple de JSON : copier des données à partir de Sybase tooAzure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="06071-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Sybase data store, see [JSON example: Copy data from Sybase tooAzure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="06071-131">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont le magasin de données Sybase utilisé toodefine Data Factory entités tooa spécifique :</span><span class="sxs-lookup"><span data-stu-id="06071-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Sybase data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="06071-132">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="06071-132">Linked service properties</span></span>
<span data-ttu-id="06071-133">Hello tableau suivant fournit la description du service de tooSybase spécifique lié éléments JSON.</span><span class="sxs-lookup"><span data-stu-id="06071-133">hello following table provides description for JSON elements specific tooSybase linked service.</span></span>

| <span data-ttu-id="06071-134">Propriété</span><span class="sxs-lookup"><span data-stu-id="06071-134">Property</span></span> | <span data-ttu-id="06071-135">Description</span><span class="sxs-lookup"><span data-stu-id="06071-135">Description</span></span> | <span data-ttu-id="06071-136">Requis</span><span class="sxs-lookup"><span data-stu-id="06071-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="06071-137">type</span><span class="sxs-lookup"><span data-stu-id="06071-137">type</span></span> |<span data-ttu-id="06071-138">propriété de type Hello doit indiquer : **OnPremisesSybase**</span><span class="sxs-lookup"><span data-stu-id="06071-138">hello type property must be set to: **OnPremisesSybase**</span></span> |<span data-ttu-id="06071-139">Oui</span><span class="sxs-lookup"><span data-stu-id="06071-139">Yes</span></span> |
| <span data-ttu-id="06071-140">server</span><span class="sxs-lookup"><span data-stu-id="06071-140">server</span></span> |<span data-ttu-id="06071-141">Nom du serveur de Sybase hello.</span><span class="sxs-lookup"><span data-stu-id="06071-141">Name of hello Sybase server.</span></span> |<span data-ttu-id="06071-142">Oui</span><span class="sxs-lookup"><span data-stu-id="06071-142">Yes</span></span> |
| <span data-ttu-id="06071-143">database</span><span class="sxs-lookup"><span data-stu-id="06071-143">database</span></span> |<span data-ttu-id="06071-144">Nom de la base de données Sybase hello.</span><span class="sxs-lookup"><span data-stu-id="06071-144">Name of hello Sybase database.</span></span> |<span data-ttu-id="06071-145">Oui</span><span class="sxs-lookup"><span data-stu-id="06071-145">Yes</span></span> |
| <span data-ttu-id="06071-146">schema</span><span class="sxs-lookup"><span data-stu-id="06071-146">schema</span></span> |<span data-ttu-id="06071-147">Nom de schéma hello hello de base de données.</span><span class="sxs-lookup"><span data-stu-id="06071-147">Name of hello schema in hello database.</span></span> |<span data-ttu-id="06071-148">Non</span><span class="sxs-lookup"><span data-stu-id="06071-148">No</span></span> |
| <span data-ttu-id="06071-149">authenticationType</span><span class="sxs-lookup"><span data-stu-id="06071-149">authenticationType</span></span> |<span data-ttu-id="06071-150">Type d’authentification utilisé tooconnect toohello base de données Sybase.</span><span class="sxs-lookup"><span data-stu-id="06071-150">Type of authentication used tooconnect toohello Sybase database.</span></span> <span data-ttu-id="06071-151">Les valeurs possibles sont : Anonyme, De base et Windows.</span><span class="sxs-lookup"><span data-stu-id="06071-151">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="06071-152">Oui</span><span class="sxs-lookup"><span data-stu-id="06071-152">Yes</span></span> |
| <span data-ttu-id="06071-153">username</span><span class="sxs-lookup"><span data-stu-id="06071-153">username</span></span> |<span data-ttu-id="06071-154">Spécifiez le nom d'utilisateur si vous utilisez l'authentification de base ou Windows.</span><span class="sxs-lookup"><span data-stu-id="06071-154">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="06071-155">Non</span><span class="sxs-lookup"><span data-stu-id="06071-155">No</span></span> |
| <span data-ttu-id="06071-156">password</span><span class="sxs-lookup"><span data-stu-id="06071-156">password</span></span> |<span data-ttu-id="06071-157">Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="06071-157">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="06071-158">Non</span><span class="sxs-lookup"><span data-stu-id="06071-158">No</span></span> |
| <span data-ttu-id="06071-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="06071-159">gatewayName</span></span> |<span data-ttu-id="06071-160">Nom de passerelle hello hello service Data Factory doit utiliser la base de données Sybase tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="06071-160">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Sybase database.</span></span> |<span data-ttu-id="06071-161">Oui</span><span class="sxs-lookup"><span data-stu-id="06071-161">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="06071-162">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="06071-162">Dataset properties</span></span>
<span data-ttu-id="06071-163">Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="06071-163">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="06071-164">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="06071-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="06071-165">section de typeProperties Hello est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="06071-165">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="06071-166">Hello **typeProperties** section pour le jeu de données de type **RelationalTable** (qui comprend de jeu de données Sybase) a hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="06071-166">hello **typeProperties** section for dataset of type **RelationalTable** (which includes Sybase dataset) has hello following properties:</span></span>

| <span data-ttu-id="06071-167">Propriété</span><span class="sxs-lookup"><span data-stu-id="06071-167">Property</span></span> | <span data-ttu-id="06071-168">Description</span><span class="sxs-lookup"><span data-stu-id="06071-168">Description</span></span> | <span data-ttu-id="06071-169">Requis</span><span class="sxs-lookup"><span data-stu-id="06071-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="06071-170">TableName</span><span class="sxs-lookup"><span data-stu-id="06071-170">tableName</span></span> |<span data-ttu-id="06071-171">Nom de table hello Bonjour instance de base de données Sybase service lié fait référence à.</span><span class="sxs-lookup"><span data-stu-id="06071-171">Name of hello table in hello Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="06071-172">Non (si la **requête** de **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="06071-172">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="06071-173">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="06071-173">Copy activity properties</span></span>
<span data-ttu-id="06071-174">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="06071-174">For a full list of sections & properties available for defining activities, see [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="06071-175">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="06071-175">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="06071-176">Alors que les propriétés disponibles dans la section typeProperties hello activité hello varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="06071-176">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="06071-177">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="06071-177">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="06071-178">Lorsque la source de hello est de type **RelationalSource** (qui inclut Sybase), hello propriétés suivantes est disponible dans **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="06071-178">When hello source is of type **RelationalSource** (which includes Sybase), hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="06071-179">Propriété</span><span class="sxs-lookup"><span data-stu-id="06071-179">Property</span></span> | <span data-ttu-id="06071-180">Description</span><span class="sxs-lookup"><span data-stu-id="06071-180">Description</span></span> | <span data-ttu-id="06071-181">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="06071-181">Allowed values</span></span> | <span data-ttu-id="06071-182">Requis</span><span class="sxs-lookup"><span data-stu-id="06071-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="06071-183">query</span><span class="sxs-lookup"><span data-stu-id="06071-183">query</span></span> |<span data-ttu-id="06071-184">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="06071-184">Use hello custom query tooread data.</span></span> |<span data-ttu-id="06071-185">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="06071-185">SQL query string.</span></span> <span data-ttu-id="06071-186">Par exemple : select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="06071-186">For example: select * from MyTable.</span></span> |<span data-ttu-id="06071-187">Non (si **tableName** de **dataset** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="06071-187">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-sybase-tooazure-blob"></a><span data-ttu-id="06071-188">Exemple de JSON : copier des données à partir de Sybase tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="06071-188">JSON example: Copy data from Sybase tooAzure Blob</span></span>
<span data-ttu-id="06071-189">Hello exemple suivant fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="06071-189">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="06071-190">Ils montrent la base de données toocopy à partir de Sybase tooAzure stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="06071-190">They show how toocopy data from Sybase database tooAzure Blob Storage.</span></span> <span data-ttu-id="06071-191">Toutefois, les données peuvent être copié tooany de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="06071-191">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="06071-192">exemple Hello a hello suivant des entités de fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="06071-192">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="06071-193">Un service lié de type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="06071-193">A linked service of type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="06071-194">Un service lié de type [Stockage Azure](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="06071-194">A liked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="06071-195">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="06071-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="06071-196">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="06071-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="06071-197">Hello [pipeline](data-factory-create-pipelines.md) avec l’activité de copie qui utilise [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="06071-197">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="06071-198">exemple Hello copie des données à partir d’un résultat de requête dans l’objet blob tooa de base de données Sybase toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="06071-198">hello sample copies data from a query result in Sybase database tooa blob every hour.</span></span> <span data-ttu-id="06071-199">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="06071-199">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="06071-200">Dans un premier temps, le programme d’installation passerelle de gestion des données hello.</span><span class="sxs-lookup"><span data-stu-id="06071-200">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="06071-201">instructions de Hello sont Bonjour [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="06071-201">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="06071-202">**Service lié Sybase :**</span><span class="sxs-lookup"><span data-stu-id="06071-202">**Sybase linked service:**</span></span>

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

<span data-ttu-id="06071-203">**Service lié Azure Blob Storage :**</span><span class="sxs-lookup"><span data-stu-id="06071-203">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="06071-204">**Jeu de données d’entrée Sybase :**</span><span class="sxs-lookup"><span data-stu-id="06071-204">**Sybase input dataset:**</span></span>

<span data-ttu-id="06071-205">exemple Hello suppose que vous avez créé une table « MyTable » dans Sybase et il contienne une colonne appelée « timestamp » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="06071-205">hello sample assumes you have created a table “MyTable” in Sybase and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="06071-206">Paramètre « external » : true informe le service de fabrique de données hello que ce jeu de données est la fabrique de données externe toohello et qu’il n’est pas généré par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="06071-206">Setting “external”: true informs hello Data Factory service that this dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="06071-207">Notez que hello **type** d’hello service lié est défini sur : **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="06071-207">Notice that hello **type** of hello linked service is set to: **RelationalTable**.</span></span>

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

<span data-ttu-id="06071-208">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="06071-208">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="06071-209">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="06071-209">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="06071-210">chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="06071-210">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="06071-211">chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="06071-211">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="06071-212">**Pipeline avec activité de copie :**</span><span class="sxs-lookup"><span data-stu-id="06071-212">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="06071-213">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="06071-213">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="06071-214">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**RelationalSource** et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="06071-214">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="06071-215">la requête SQL Hello spécifiée pour hello **requête** propriété sélectionne des données de hello de hello DBA. Table Orders dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="06071-215">hello SQL query specified for hello **query** property selects hello data from hello DBA.Orders table in hello database.</span></span>

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

## <a name="type-mapping-for-sybase"></a><span data-ttu-id="06071-216">Mappage de type pour Sybase</span><span class="sxs-lookup"><span data-stu-id="06071-216">Type mapping for Sybase</span></span>
<span data-ttu-id="06071-217">Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, hello activité de copie effectue les conversions de type automatique à partir de types de sources de toosink types avec hello approche de l’étape 2 :</span><span class="sxs-lookup"><span data-stu-id="06071-217">As mentioned in hello [Data Movement Activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="06071-218">Convertir à partir de la source native types too.NET type</span><span class="sxs-lookup"><span data-stu-id="06071-218">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="06071-219">Conversion de type de récepteur de toonative de type .NET</span><span class="sxs-lookup"><span data-stu-id="06071-219">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="06071-220">Sybase prend en charge les types T-SQL et T-SQL.</span><span class="sxs-lookup"><span data-stu-id="06071-220">Sybase supports T-SQL and T-SQL types.</span></span> <span data-ttu-id="06071-221">Pour une table de mappage de type too.NET de types sql, consultez [le connecteur Azure SQL](data-factory-azure-sql-connector.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="06071-221">For a mapping table from sql types too.NET type, see [Azure SQL Connector](data-factory-azure-sql-connector.md) article.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="06071-222">Mapper les colonnes de source toosink</span><span class="sxs-lookup"><span data-stu-id="06071-222">Map source toosink columns</span></span>
<span data-ttu-id="06071-223">toolearn sur le mappage des colonnes dans toocolumns du jeu de données source dans le jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="06071-223">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="06071-224">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="06071-224">Repeatable read from relational sources</span></span>
<span data-ttu-id="06071-225">Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="06071-225">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="06071-226">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="06071-226">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="06071-227">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="06071-227">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="06071-228">Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée.</span><span class="sxs-lookup"><span data-stu-id="06071-228">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="06071-229">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="06071-229">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="06071-230">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="06071-230">Performance and Tuning</span></span>
<span data-ttu-id="06071-231">Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="06071-231">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
