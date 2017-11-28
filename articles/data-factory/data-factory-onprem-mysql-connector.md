---
title: "aaaMove des données de MySQL à l’aide d’Azure Data Factory | Documents Microsoft"
description: "Découvrez comment toomove les données de MySQL de base de données à l’aide d’Azure Data Factory."
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
ms.openlocfilehash: 3ffe969e42ce1a54b265c4739df43fdc594ea891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="5df76-103">Déplacer des données depuis MySQL à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="5df76-103">Move data From MySQL using Azure Data Factory</span></span>
<span data-ttu-id="5df76-104">Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory à partir d’une base de données MySQL locale.</span><span class="sxs-lookup"><span data-stu-id="5df76-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises MySQL database.</span></span> <span data-ttu-id="5df76-105">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="5df76-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="5df76-106">Vous pouvez copier les données d’une banque de données locale MySQL tooany pris en charge données magasin récepteur.</span><span class="sxs-lookup"><span data-stu-id="5df76-106">You can copy data from an on-premises MySQL data store tooany supported sink data store.</span></span> <span data-ttu-id="5df76-107">Pour une liste de données pris en charge des magasins récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="5df76-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="5df76-108">Fabrique de données prend en charge uniquement le déplacement tooother les magasins de données du magasin de données à partir de données MySQL, mais ne pas pour déplacer des données d’une autre banque de données MySQL tooan données magasins.</span><span class="sxs-lookup"><span data-stu-id="5df76-108">Data factory currently supports only moving data from a MySQL data store tooother data stores, but not for moving data from other data stores tooan MySQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5df76-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5df76-109">Prerequisites</span></span>
<span data-ttu-id="5df76-110">Service de fabrique de données prend en charge des sources de MySQL tooon local qui se connecte à l’aide de la passerelle de gestion des données de hello.</span><span class="sxs-lookup"><span data-stu-id="5df76-110">Data Factory service supports connecting tooon-premises MySQL sources using hello Data Management Gateway.</span></span> <span data-ttu-id="5df76-111">Consultez [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn l’article sur la passerelle de gestion des données et des instructions détaillées sur la configuration de passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="5df76-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="5df76-112">Passerelle est requise même si la base de données MySQL hello est hébergé dans une machine virtuelle de Azure IaaS (VM).</span><span class="sxs-lookup"><span data-stu-id="5df76-112">Gateway is required even if hello MySQL database is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="5df76-113">Vous pouvez installer la passerelle de hello sur hello même machine virtuelle en tant que données de hello stocker ou sur un ordinateur différent virtuel tant que passerelle de hello peuvent se connecter toohello de base de données.</span><span class="sxs-lookup"><span data-stu-id="5df76-113">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="5df76-114">Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.</span><span class="sxs-lookup"><span data-stu-id="5df76-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="5df76-115">Versions prises en charge et installation</span><span class="sxs-lookup"><span data-stu-id="5df76-115">Supported versions and installation</span></span>
<span data-ttu-id="5df76-116">Pour toohello tooconnect de passerelle de gestion des données de la base de données MySQL, vous devez tooinstall hello [Connector/Net MySQL pour Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 ou version ultérieure) sur hello même système que hello passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="5df76-116">For Data Management Gateway tooconnect toohello MySQL Database, you need tooinstall hello [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 or above) on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="5df76-117">MySQL version 5.1 et ultérieures est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="5df76-117">MySQL version 5.1 and above is supported.</span></span>

> [!TIP]
> <span data-ttu-id="5df76-118">Si vous rencontrez l’erreur « Échec de l’authentification, car la partie distante de hello a fermé hello flux de transport. », envisagez de tooupgrade hello version toohigher de Connector/Net MySQL.</span><span class="sxs-lookup"><span data-stu-id="5df76-118">If you hit error on "Authentication failed because hello remote party has closed hello transport stream.", consider tooupgrade hello MySQL Connector/Net toohigher version.</span></span>

## <a name="getting-started"></a><span data-ttu-id="5df76-119">Prise en main</span><span class="sxs-lookup"><span data-stu-id="5df76-119">Getting started</span></span>
<span data-ttu-id="5df76-120">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données Cassandra local à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="5df76-120">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="5df76-121">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="5df76-121">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="5df76-122">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="5df76-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="5df76-123">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="5df76-123">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="5df76-124">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="5df76-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="5df76-125">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="5df76-125">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="5df76-126">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="5df76-126">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="5df76-127">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="5df76-127">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="5df76-128">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="5df76-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="5df76-129">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="5df76-129">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="5df76-130">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="5df76-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="5df76-131">Pour voir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont utilisés toocopy des données à partir d’une banque de données MySQL locale, [exemple de JSON : copier des données de MySQL tooAzure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="5df76-131">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL tooAzure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="5df76-132">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont le magasin de données MySQL utilisés toodefine Data Factory entités tooa spécifique :</span><span class="sxs-lookup"><span data-stu-id="5df76-132">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa MySQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="5df76-133">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="5df76-133">Linked service properties</span></span>
<span data-ttu-id="5df76-134">Hello tableau suivant fournit la description du service de tooMySQL spécifique lié éléments JSON.</span><span class="sxs-lookup"><span data-stu-id="5df76-134">hello following table provides description for JSON elements specific tooMySQL linked service.</span></span>

| <span data-ttu-id="5df76-135">Propriété</span><span class="sxs-lookup"><span data-stu-id="5df76-135">Property</span></span> | <span data-ttu-id="5df76-136">Description</span><span class="sxs-lookup"><span data-stu-id="5df76-136">Description</span></span> | <span data-ttu-id="5df76-137">Requis</span><span class="sxs-lookup"><span data-stu-id="5df76-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5df76-138">type</span><span class="sxs-lookup"><span data-stu-id="5df76-138">type</span></span> |<span data-ttu-id="5df76-139">propriété de type Hello doit indiquer : **OnPremisesMySql**</span><span class="sxs-lookup"><span data-stu-id="5df76-139">hello type property must be set to: **OnPremisesMySql**</span></span> |<span data-ttu-id="5df76-140">Oui</span><span class="sxs-lookup"><span data-stu-id="5df76-140">Yes</span></span> |
| <span data-ttu-id="5df76-141">server</span><span class="sxs-lookup"><span data-stu-id="5df76-141">server</span></span> |<span data-ttu-id="5df76-142">Nom du serveur de MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="5df76-142">Name of hello MySQL server.</span></span> |<span data-ttu-id="5df76-143">Oui</span><span class="sxs-lookup"><span data-stu-id="5df76-143">Yes</span></span> |
| <span data-ttu-id="5df76-144">database</span><span class="sxs-lookup"><span data-stu-id="5df76-144">database</span></span> |<span data-ttu-id="5df76-145">Nom de la base de données MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="5df76-145">Name of hello MySQL database.</span></span> |<span data-ttu-id="5df76-146">Oui</span><span class="sxs-lookup"><span data-stu-id="5df76-146">Yes</span></span> |
| <span data-ttu-id="5df76-147">schema</span><span class="sxs-lookup"><span data-stu-id="5df76-147">schema</span></span> |<span data-ttu-id="5df76-148">Nom de schéma hello hello de base de données.</span><span class="sxs-lookup"><span data-stu-id="5df76-148">Name of hello schema in hello database.</span></span> |<span data-ttu-id="5df76-149">Non</span><span class="sxs-lookup"><span data-stu-id="5df76-149">No</span></span> |
| <span data-ttu-id="5df76-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="5df76-150">authenticationType</span></span> |<span data-ttu-id="5df76-151">Type d’authentification utilisé tooconnect toohello base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="5df76-151">Type of authentication used tooconnect toohello MySQL database.</span></span> <span data-ttu-id="5df76-152">Les valeurs possibles sont les suivantes : `Basic`.</span><span class="sxs-lookup"><span data-stu-id="5df76-152">Possible values are: `Basic`.</span></span> |<span data-ttu-id="5df76-153">Oui</span><span class="sxs-lookup"><span data-stu-id="5df76-153">Yes</span></span> |
| <span data-ttu-id="5df76-154">username</span><span class="sxs-lookup"><span data-stu-id="5df76-154">username</span></span> |<span data-ttu-id="5df76-155">Spécifiez la base de données utilisateur nom tooconnect toohello MySQL.</span><span class="sxs-lookup"><span data-stu-id="5df76-155">Specify user name tooconnect toohello MySQL database.</span></span> |<span data-ttu-id="5df76-156">Oui</span><span class="sxs-lookup"><span data-stu-id="5df76-156">Yes</span></span> |
| <span data-ttu-id="5df76-157">password</span><span class="sxs-lookup"><span data-stu-id="5df76-157">password</span></span> |<span data-ttu-id="5df76-158">Spécifiez le mot de passe de compte d’utilisateur hello spécifié.</span><span class="sxs-lookup"><span data-stu-id="5df76-158">Specify password for hello user account you specified.</span></span> |<span data-ttu-id="5df76-159">Oui</span><span class="sxs-lookup"><span data-stu-id="5df76-159">Yes</span></span> |
| <span data-ttu-id="5df76-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="5df76-160">gatewayName</span></span> |<span data-ttu-id="5df76-161">Nom de passerelle hello hello service Data Factory doit utiliser la base de données MySQL tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="5df76-161">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises MySQL database.</span></span> |<span data-ttu-id="5df76-162">Oui</span><span class="sxs-lookup"><span data-stu-id="5df76-162">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="5df76-163">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="5df76-163">Dataset properties</span></span>
<span data-ttu-id="5df76-164">Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="5df76-164">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="5df76-165">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="5df76-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="5df76-166">Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="5df76-166">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="5df76-167">jeu de données de type Hello typeProperties section **RelationalTable** (qui comprend de jeu de données MySQL) a hello propriétés suivantes</span><span class="sxs-lookup"><span data-stu-id="5df76-167">hello typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has hello following properties</span></span>

| <span data-ttu-id="5df76-168">Propriété</span><span class="sxs-lookup"><span data-stu-id="5df76-168">Property</span></span> | <span data-ttu-id="5df76-169">Description</span><span class="sxs-lookup"><span data-stu-id="5df76-169">Description</span></span> | <span data-ttu-id="5df76-170">Requis</span><span class="sxs-lookup"><span data-stu-id="5df76-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5df76-171">TableName</span><span class="sxs-lookup"><span data-stu-id="5df76-171">tableName</span></span> |<span data-ttu-id="5df76-172">Nom de table hello Bonjour instance de base de données MySQL service lié fait référence à.</span><span class="sxs-lookup"><span data-stu-id="5df76-172">Name of hello table in hello MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="5df76-173">Non (si la **requête** de **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="5df76-173">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="5df76-174">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="5df76-174">Copy activity properties</span></span>
<span data-ttu-id="5df76-175">Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="5df76-175">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="5df76-176">Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="5df76-176">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="5df76-177">Tandis que les propriétés disponibles dans hello **typeProperties** section d’activité hello varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="5df76-177">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="5df76-178">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="5df76-178">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="5df76-179">Lorsque la source de l’activité de copie est de type **RelationalSource** (qui inclut MySQL), hello propriétés suivantes est disponible dans la section de typeProperties :</span><span class="sxs-lookup"><span data-stu-id="5df76-179">When source in copy activity is of type **RelationalSource** (which includes MySQL), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="5df76-180">Propriété</span><span class="sxs-lookup"><span data-stu-id="5df76-180">Property</span></span> | <span data-ttu-id="5df76-181">Description</span><span class="sxs-lookup"><span data-stu-id="5df76-181">Description</span></span> | <span data-ttu-id="5df76-182">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="5df76-182">Allowed values</span></span> | <span data-ttu-id="5df76-183">Requis</span><span class="sxs-lookup"><span data-stu-id="5df76-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5df76-184">query</span><span class="sxs-lookup"><span data-stu-id="5df76-184">query</span></span> |<span data-ttu-id="5df76-185">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="5df76-185">Use hello custom query tooread data.</span></span> |<span data-ttu-id="5df76-186">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="5df76-186">SQL query string.</span></span> <span data-ttu-id="5df76-187">Par exemple : select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="5df76-187">For example: select * from MyTable.</span></span> |<span data-ttu-id="5df76-188">Non (si **tableName** de **dataset** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="5df76-188">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-mysql-tooazure-blob"></a><span data-ttu-id="5df76-189">Exemple de JSON : copier des données de MySQL tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="5df76-189">JSON example: Copy data from MySQL tooAzure Blob</span></span>
<span data-ttu-id="5df76-190">Cet exemple fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5df76-190">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="5df76-191">Elle indique la base de données toocopy à partir d’un MySQL locale tooan stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="5df76-191">It shows how toocopy data from an on-premises MySQL database tooan Azure Blob Storage.</span></span> <span data-ttu-id="5df76-192">Toutefois, les données peuvent être copié tooany de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5df76-192">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5df76-193">Cet exemple fournit des extraits de code JSON.</span><span class="sxs-lookup"><span data-stu-id="5df76-193">This sample provides JSON snippets.</span></span> <span data-ttu-id="5df76-194">Il n’inclut pas d’instructions détaillées pour créer la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="5df76-194">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="5df76-195">Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="5df76-195">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="5df76-196">exemple Hello a hello suivant des entités de fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="5df76-196">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="5df76-197">Un service lié de type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5df76-197">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="5df76-198">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5df76-198">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="5df76-199">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5df76-199">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="5df76-200">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5df76-200">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="5df76-201">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="5df76-201">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="5df76-202">exemple Hello copie toutes les heures des données à partir d’un résultat de requête dans l’objet blob tooa de base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="5df76-202">hello sample copies data from a query result in MySQL database tooa blob hourly.</span></span> <span data-ttu-id="5df76-203">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="5df76-203">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="5df76-204">Dans un premier temps, le programme d’installation passerelle de gestion des données hello.</span><span class="sxs-lookup"><span data-stu-id="5df76-204">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="5df76-205">instructions de Hello sont Bonjour [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="5df76-205">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="5df76-206">**Service lié MySQL :**</span><span class="sxs-lookup"><span data-stu-id="5df76-206">**MySQL linked service:**</span></span>

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

<span data-ttu-id="5df76-207">**Service lié Azure Storage :**</span><span class="sxs-lookup"><span data-stu-id="5df76-207">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="5df76-208">**Jeu de données d’entrée MySQL :**</span><span class="sxs-lookup"><span data-stu-id="5df76-208">**MySQL input dataset:**</span></span>

<span data-ttu-id="5df76-209">exemple Hello suppose que vous avez créé une table « MyTable » dans MySQL et il contienne une colonne appelée « timestampcolumn » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="5df76-209">hello sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="5df76-210">Paramètre « external » : « true » informe service Data Factory de hello cette table hello est la fabrique de données externe toohello et n’est pas générée par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="5df76-210">Setting “external”: ”true” informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="5df76-211">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="5df76-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="5df76-212">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="5df76-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="5df76-213">chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="5df76-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="5df76-214">chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="5df76-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="5df76-215">**Pipeline avec activité de copie :**</span><span class="sxs-lookup"><span data-stu-id="5df76-215">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="5df76-216">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="5df76-216">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="5df76-217">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**RelationalSource** et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="5df76-217">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="5df76-218">la requête SQL Hello spécifiée pour hello **requête** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.</span><span class="sxs-lookup"><span data-stu-id="5df76-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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


### <a name="type-mapping-for-mysql"></a><span data-ttu-id="5df76-219">Mappage de type pour MySQL</span><span class="sxs-lookup"><span data-stu-id="5df76-219">Type mapping for MySQL</span></span>
<span data-ttu-id="5df76-220">Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, l’activité de copie effectue les conversions de type automatique à partir de types de sources de toosink types avec hello suivant l’approche en deux étapes :</span><span class="sxs-lookup"><span data-stu-id="5df76-220">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="5df76-221">Convertir à partir de la source native types too.NET type</span><span class="sxs-lookup"><span data-stu-id="5df76-221">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="5df76-222">Conversion de type de récepteur de toonative de type .NET</span><span class="sxs-lookup"><span data-stu-id="5df76-222">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="5df76-223">Lorsque vous déplacez des données tooMySQL, hello mappages suivants sont utilisés à partir des types de too.NET de types de MySQL.</span><span class="sxs-lookup"><span data-stu-id="5df76-223">When moving data tooMySQL, hello following mappings are used from MySQL types too.NET types.</span></span>

| <span data-ttu-id="5df76-224">Type de base de données MySQL</span><span class="sxs-lookup"><span data-stu-id="5df76-224">MySQL Database type</span></span> | <span data-ttu-id="5df76-225">Type de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="5df76-225">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="5df76-226">bigint non signé</span><span class="sxs-lookup"><span data-stu-id="5df76-226">bigint unsigned</span></span> |<span data-ttu-id="5df76-227">Décimal</span><span class="sxs-lookup"><span data-stu-id="5df76-227">Decimal</span></span> |
| <span data-ttu-id="5df76-228">bigint</span><span class="sxs-lookup"><span data-stu-id="5df76-228">bigint</span></span> |<span data-ttu-id="5df76-229">Int64</span><span class="sxs-lookup"><span data-stu-id="5df76-229">Int64</span></span> |
| <span data-ttu-id="5df76-230">bit</span><span class="sxs-lookup"><span data-stu-id="5df76-230">bit</span></span> |<span data-ttu-id="5df76-231">Décimal</span><span class="sxs-lookup"><span data-stu-id="5df76-231">Decimal</span></span> |
| <span data-ttu-id="5df76-232">objet blob</span><span class="sxs-lookup"><span data-stu-id="5df76-232">blob</span></span> |<span data-ttu-id="5df76-233">Byte[]</span><span class="sxs-lookup"><span data-stu-id="5df76-233">Byte[]</span></span> |
| <span data-ttu-id="5df76-234">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="5df76-234">bool</span></span> |<span data-ttu-id="5df76-235">Boolean</span><span class="sxs-lookup"><span data-stu-id="5df76-235">Boolean</span></span> |
| <span data-ttu-id="5df76-236">char</span><span class="sxs-lookup"><span data-stu-id="5df76-236">char</span></span> |<span data-ttu-id="5df76-237">String</span><span class="sxs-lookup"><span data-stu-id="5df76-237">String</span></span> |
| <span data-ttu-id="5df76-238">date</span><span class="sxs-lookup"><span data-stu-id="5df76-238">date</span></span> |<span data-ttu-id="5df76-239">Datetime</span><span class="sxs-lookup"><span data-stu-id="5df76-239">Datetime</span></span> |
| <span data-ttu-id="5df76-240">Datetime</span><span class="sxs-lookup"><span data-stu-id="5df76-240">datetime</span></span> |<span data-ttu-id="5df76-241">Datetime</span><span class="sxs-lookup"><span data-stu-id="5df76-241">Datetime</span></span> |
| <span data-ttu-id="5df76-242">Décimal</span><span class="sxs-lookup"><span data-stu-id="5df76-242">decimal</span></span> |<span data-ttu-id="5df76-243">Décimal</span><span class="sxs-lookup"><span data-stu-id="5df76-243">Decimal</span></span> |
| <span data-ttu-id="5df76-244">double précision</span><span class="sxs-lookup"><span data-stu-id="5df76-244">double precision</span></span> |<span data-ttu-id="5df76-245">Double</span><span class="sxs-lookup"><span data-stu-id="5df76-245">Double</span></span> |
| <span data-ttu-id="5df76-246">Double</span><span class="sxs-lookup"><span data-stu-id="5df76-246">double</span></span> |<span data-ttu-id="5df76-247">Double</span><span class="sxs-lookup"><span data-stu-id="5df76-247">Double</span></span> |
| <span data-ttu-id="5df76-248">enum</span><span class="sxs-lookup"><span data-stu-id="5df76-248">enum</span></span> |<span data-ttu-id="5df76-249">String</span><span class="sxs-lookup"><span data-stu-id="5df76-249">String</span></span> |
| <span data-ttu-id="5df76-250">float</span><span class="sxs-lookup"><span data-stu-id="5df76-250">float</span></span> |<span data-ttu-id="5df76-251">Single</span><span class="sxs-lookup"><span data-stu-id="5df76-251">Single</span></span> |
| <span data-ttu-id="5df76-252">int non signé</span><span class="sxs-lookup"><span data-stu-id="5df76-252">int unsigned</span></span> |<span data-ttu-id="5df76-253">Int64</span><span class="sxs-lookup"><span data-stu-id="5df76-253">Int64</span></span> |
| <span data-ttu-id="5df76-254">int</span><span class="sxs-lookup"><span data-stu-id="5df76-254">int</span></span> |<span data-ttu-id="5df76-255">Int32</span><span class="sxs-lookup"><span data-stu-id="5df76-255">Int32</span></span> |
| <span data-ttu-id="5df76-256">entier non signé</span><span class="sxs-lookup"><span data-stu-id="5df76-256">integer unsigned</span></span> |<span data-ttu-id="5df76-257">Int64</span><span class="sxs-lookup"><span data-stu-id="5df76-257">Int64</span></span> |
| <span data-ttu-id="5df76-258">integer</span><span class="sxs-lookup"><span data-stu-id="5df76-258">integer</span></span> |<span data-ttu-id="5df76-259">Int32</span><span class="sxs-lookup"><span data-stu-id="5df76-259">Int32</span></span> |
| <span data-ttu-id="5df76-260">long varbinary</span><span class="sxs-lookup"><span data-stu-id="5df76-260">long varbinary</span></span> |<span data-ttu-id="5df76-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="5df76-261">Byte[]</span></span> |
| <span data-ttu-id="5df76-262">long varchar</span><span class="sxs-lookup"><span data-stu-id="5df76-262">long varchar</span></span> |<span data-ttu-id="5df76-263">String</span><span class="sxs-lookup"><span data-stu-id="5df76-263">String</span></span> |
| <span data-ttu-id="5df76-264">longblob</span><span class="sxs-lookup"><span data-stu-id="5df76-264">longblob</span></span> |<span data-ttu-id="5df76-265">Byte[]</span><span class="sxs-lookup"><span data-stu-id="5df76-265">Byte[]</span></span> |
| <span data-ttu-id="5df76-266">longtext</span><span class="sxs-lookup"><span data-stu-id="5df76-266">longtext</span></span> |<span data-ttu-id="5df76-267">String</span><span class="sxs-lookup"><span data-stu-id="5df76-267">String</span></span> |
| <span data-ttu-id="5df76-268">mediumblob</span><span class="sxs-lookup"><span data-stu-id="5df76-268">mediumblob</span></span> |<span data-ttu-id="5df76-269">Byte[]</span><span class="sxs-lookup"><span data-stu-id="5df76-269">Byte[]</span></span> |
| <span data-ttu-id="5df76-270">mediumint non signé</span><span class="sxs-lookup"><span data-stu-id="5df76-270">mediumint unsigned</span></span> |<span data-ttu-id="5df76-271">Int64</span><span class="sxs-lookup"><span data-stu-id="5df76-271">Int64</span></span> |
| <span data-ttu-id="5df76-272">mediumint</span><span class="sxs-lookup"><span data-stu-id="5df76-272">mediumint</span></span> |<span data-ttu-id="5df76-273">Int32</span><span class="sxs-lookup"><span data-stu-id="5df76-273">Int32</span></span> |
| <span data-ttu-id="5df76-274">mediumtext</span><span class="sxs-lookup"><span data-stu-id="5df76-274">mediumtext</span></span> |<span data-ttu-id="5df76-275">String</span><span class="sxs-lookup"><span data-stu-id="5df76-275">String</span></span> |
| <span data-ttu-id="5df76-276">numérique</span><span class="sxs-lookup"><span data-stu-id="5df76-276">numeric</span></span> |<span data-ttu-id="5df76-277">Décimal</span><span class="sxs-lookup"><span data-stu-id="5df76-277">Decimal</span></span> |
| <span data-ttu-id="5df76-278">real</span><span class="sxs-lookup"><span data-stu-id="5df76-278">real</span></span> |<span data-ttu-id="5df76-279">Double</span><span class="sxs-lookup"><span data-stu-id="5df76-279">Double</span></span> |
| <span data-ttu-id="5df76-280">set</span><span class="sxs-lookup"><span data-stu-id="5df76-280">set</span></span> |<span data-ttu-id="5df76-281">String</span><span class="sxs-lookup"><span data-stu-id="5df76-281">String</span></span> |
| <span data-ttu-id="5df76-282">smallint non signé</span><span class="sxs-lookup"><span data-stu-id="5df76-282">smallint unsigned</span></span> |<span data-ttu-id="5df76-283">Int32</span><span class="sxs-lookup"><span data-stu-id="5df76-283">Int32</span></span> |
| <span data-ttu-id="5df76-284">smallint</span><span class="sxs-lookup"><span data-stu-id="5df76-284">smallint</span></span> |<span data-ttu-id="5df76-285">Int16</span><span class="sxs-lookup"><span data-stu-id="5df76-285">Int16</span></span> |
| <span data-ttu-id="5df76-286">texte</span><span class="sxs-lookup"><span data-stu-id="5df76-286">text</span></span> |<span data-ttu-id="5df76-287">String</span><span class="sxs-lookup"><span data-stu-id="5df76-287">String</span></span> |
| <span data-ttu-id="5df76-288">time</span><span class="sxs-lookup"><span data-stu-id="5df76-288">time</span></span> |<span data-ttu-id="5df76-289">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="5df76-289">TimeSpan</span></span> |
| <span data-ttu-id="5df76-290">timestamp</span><span class="sxs-lookup"><span data-stu-id="5df76-290">timestamp</span></span> |<span data-ttu-id="5df76-291">Datetime</span><span class="sxs-lookup"><span data-stu-id="5df76-291">Datetime</span></span> |
| <span data-ttu-id="5df76-292">tinyblob</span><span class="sxs-lookup"><span data-stu-id="5df76-292">tinyblob</span></span> |<span data-ttu-id="5df76-293">Byte[]</span><span class="sxs-lookup"><span data-stu-id="5df76-293">Byte[]</span></span> |
| <span data-ttu-id="5df76-294">tinyint non signé</span><span class="sxs-lookup"><span data-stu-id="5df76-294">tinyint unsigned</span></span> |<span data-ttu-id="5df76-295">Int16</span><span class="sxs-lookup"><span data-stu-id="5df76-295">Int16</span></span> |
| <span data-ttu-id="5df76-296">tinyint</span><span class="sxs-lookup"><span data-stu-id="5df76-296">tinyint</span></span> |<span data-ttu-id="5df76-297">Int16</span><span class="sxs-lookup"><span data-stu-id="5df76-297">Int16</span></span> |
| <span data-ttu-id="5df76-298">tinytext</span><span class="sxs-lookup"><span data-stu-id="5df76-298">tinytext</span></span> |<span data-ttu-id="5df76-299">String</span><span class="sxs-lookup"><span data-stu-id="5df76-299">String</span></span> |
| <span data-ttu-id="5df76-300">varchar</span><span class="sxs-lookup"><span data-stu-id="5df76-300">varchar</span></span> |<span data-ttu-id="5df76-301">String</span><span class="sxs-lookup"><span data-stu-id="5df76-301">String</span></span> |
| <span data-ttu-id="5df76-302">year</span><span class="sxs-lookup"><span data-stu-id="5df76-302">year</span></span> |<span data-ttu-id="5df76-303">Int</span><span class="sxs-lookup"><span data-stu-id="5df76-303">Int</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="5df76-304">Mapper les colonnes de source toosink</span><span class="sxs-lookup"><span data-stu-id="5df76-304">Map source toosink columns</span></span>
<span data-ttu-id="5df76-305">toolearn sur le mappage des colonnes dans toocolumns du jeu de données source dans le jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="5df76-305">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="5df76-306">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="5df76-306">Repeatable read from relational sources</span></span>
<span data-ttu-id="5df76-307">Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="5df76-307">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="5df76-308">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="5df76-308">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="5df76-309">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="5df76-309">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="5df76-310">Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée.</span><span class="sxs-lookup"><span data-stu-id="5df76-310">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="5df76-311">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="5df76-311">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="5df76-312">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="5df76-312">Performance and Tuning</span></span>
<span data-ttu-id="5df76-313">Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="5df76-313">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
