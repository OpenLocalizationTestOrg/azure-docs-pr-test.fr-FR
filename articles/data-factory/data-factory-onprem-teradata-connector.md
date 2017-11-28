---
title: "données aaaMove de Teradata à l’aide d’Azure Data Factory | Documents Microsoft"
description: "En savoir plus sur le connecteur de Teradata pour hello service Data Factory qui vous permet de déplacer des données à partir de la base de données Teradata"
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
ms.openlocfilehash: 79153476157666463b499edaa7585adaf8ad3bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="a14d5-103">Déplacer des données depuis Teradata à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a14d5-103">Move data from Teradata using Azure Data Factory</span></span>
<span data-ttu-id="a14d5-104">Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory à partir d’une base de données Teradata locale.</span><span class="sxs-lookup"><span data-stu-id="a14d5-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Teradata database.</span></span> <span data-ttu-id="a14d5-105">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="a14d5-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="a14d5-106">Vous pouvez copier les données d’une banque de données locale Teradata données magasin tooany pris en charge récepteur.</span><span class="sxs-lookup"><span data-stu-id="a14d5-106">You can copy data from an on-premises Teradata data store tooany supported sink data store.</span></span> <span data-ttu-id="a14d5-107">Pour une liste de données pris en charge des magasins récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="a14d5-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="a14d5-108">Fabrique de données prend en charge uniquement le déplacement tooother les magasins de données du magasin de données à partir de données Teradata, mais ne pas pour déplacer des données d’une autre banque de données Teradata tooa données magasins.</span><span class="sxs-lookup"><span data-stu-id="a14d5-108">Data factory currently supports only moving data from a Teradata data store tooother data stores, but not for moving data from other data stores tooa Teradata data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a14d5-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a14d5-109">Prerequisites</span></span>
<span data-ttu-id="a14d5-110">Fabrique de données prend en charge les sources de Teradata tooon local se connectant via hello passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="a14d5-110">Data factory supports connecting tooon-premises Teradata sources via hello Data Management Gateway.</span></span> <span data-ttu-id="a14d5-111">Consultez [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn l’article sur la passerelle de gestion des données et des instructions détaillées sur la configuration de passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="a14d5-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="a14d5-112">Passerelle est requise même si hello Teradata est hébergé dans une machine virtuelle IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="a14d5-112">Gateway is required even if hello Teradata is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="a14d5-113">Vous pouvez installer la passerelle de hello sur hello même IaaS VM sous forme de données de hello stocker ou sur un ordinateur différent virtuel tant que passerelle de hello peuvent se connecter toohello de base de données.</span><span class="sxs-lookup"><span data-stu-id="a14d5-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="a14d5-114">Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.</span><span class="sxs-lookup"><span data-stu-id="a14d5-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="a14d5-115">Versions prises en charge et installation</span><span class="sxs-lookup"><span data-stu-id="a14d5-115">Supported versions and installation</span></span>
<span data-ttu-id="a14d5-116">Pour toohello tooconnect de passerelle de gestion des données de la base de données Teradata, vous devez tooinstall hello [le fournisseur de données .NET pour Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 ou ci-dessus sur hello le même système que hello passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="a14d5-116">For Data Management Gateway tooconnect toohello Teradata Database, you need tooinstall hello [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="a14d5-117">Teradata version 12 et ultérieures est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="a14d5-117">Teradata version 12 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a14d5-118">Prise en main</span><span class="sxs-lookup"><span data-stu-id="a14d5-118">Getting started</span></span>
<span data-ttu-id="a14d5-119">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données Cassandra local à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="a14d5-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="a14d5-120">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="a14d5-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="a14d5-121">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="a14d5-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="a14d5-122">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="a14d5-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a14d5-123">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="a14d5-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="a14d5-124">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="a14d5-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="a14d5-125">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="a14d5-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="a14d5-126">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="a14d5-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="a14d5-127">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="a14d5-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="a14d5-128">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="a14d5-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="a14d5-129">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="a14d5-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="a14d5-130">Pour voir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données à partir d’une banque de données Teradata locale, [exemple de JSON : copier des données Teradata tooAzure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="a14d5-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata tooAzure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="a14d5-131">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont le magasin de données Teradata utilisé toodefine Data Factory entités tooa spécifique :</span><span class="sxs-lookup"><span data-stu-id="a14d5-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Teradata data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a14d5-132">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="a14d5-132">Linked service properties</span></span>
<span data-ttu-id="a14d5-133">Hello tableau suivant fournit la description du service de tooTeradata spécifique lié éléments JSON.</span><span class="sxs-lookup"><span data-stu-id="a14d5-133">hello following table provides description for JSON elements specific tooTeradata linked service.</span></span>

| <span data-ttu-id="a14d5-134">Propriété</span><span class="sxs-lookup"><span data-stu-id="a14d5-134">Property</span></span> | <span data-ttu-id="a14d5-135">Description</span><span class="sxs-lookup"><span data-stu-id="a14d5-135">Description</span></span> | <span data-ttu-id="a14d5-136">Requis</span><span class="sxs-lookup"><span data-stu-id="a14d5-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a14d5-137">type</span><span class="sxs-lookup"><span data-stu-id="a14d5-137">type</span></span> |<span data-ttu-id="a14d5-138">propriété de type Hello doit indiquer : **OnPremisesTeradata**</span><span class="sxs-lookup"><span data-stu-id="a14d5-138">hello type property must be set to: **OnPremisesTeradata**</span></span> |<span data-ttu-id="a14d5-139">Oui</span><span class="sxs-lookup"><span data-stu-id="a14d5-139">Yes</span></span> |
| <span data-ttu-id="a14d5-140">server</span><span class="sxs-lookup"><span data-stu-id="a14d5-140">server</span></span> |<span data-ttu-id="a14d5-141">Nom du serveur de Teradata hello.</span><span class="sxs-lookup"><span data-stu-id="a14d5-141">Name of hello Teradata server.</span></span> |<span data-ttu-id="a14d5-142">Oui</span><span class="sxs-lookup"><span data-stu-id="a14d5-142">Yes</span></span> |
| <span data-ttu-id="a14d5-143">authenticationType</span><span class="sxs-lookup"><span data-stu-id="a14d5-143">authenticationType</span></span> |<span data-ttu-id="a14d5-144">Type d’authentification utilisé tooconnect toohello base de données Teradata.</span><span class="sxs-lookup"><span data-stu-id="a14d5-144">Type of authentication used tooconnect toohello Teradata database.</span></span> <span data-ttu-id="a14d5-145">Les valeurs possibles sont : Anonyme, De base et Windows.</span><span class="sxs-lookup"><span data-stu-id="a14d5-145">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="a14d5-146">Oui</span><span class="sxs-lookup"><span data-stu-id="a14d5-146">Yes</span></span> |
| <span data-ttu-id="a14d5-147">username</span><span class="sxs-lookup"><span data-stu-id="a14d5-147">username</span></span> |<span data-ttu-id="a14d5-148">Spécifiez le nom d'utilisateur si vous utilisez l'authentification de base ou Windows.</span><span class="sxs-lookup"><span data-stu-id="a14d5-148">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="a14d5-149">Non</span><span class="sxs-lookup"><span data-stu-id="a14d5-149">No</span></span> |
| <span data-ttu-id="a14d5-150">password</span><span class="sxs-lookup"><span data-stu-id="a14d5-150">password</span></span> |<span data-ttu-id="a14d5-151">Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="a14d5-151">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="a14d5-152">Non</span><span class="sxs-lookup"><span data-stu-id="a14d5-152">No</span></span> |
| <span data-ttu-id="a14d5-153">gatewayName</span><span class="sxs-lookup"><span data-stu-id="a14d5-153">gatewayName</span></span> |<span data-ttu-id="a14d5-154">Nom de passerelle hello hello service Data Factory doit utiliser la base de données Teradata tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="a14d5-154">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Teradata database.</span></span> |<span data-ttu-id="a14d5-155">Oui</span><span class="sxs-lookup"><span data-stu-id="a14d5-155">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="a14d5-156">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="a14d5-156">Dataset properties</span></span>
<span data-ttu-id="a14d5-157">Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="a14d5-157">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a14d5-158">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="a14d5-158">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="a14d5-159">Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="a14d5-159">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="a14d5-160">Actuellement, il n’y a aucune propriété de type pris en charge pour le jeu de données Teradata hello.</span><span class="sxs-lookup"><span data-stu-id="a14d5-160">Currently, there are no type properties supported for hello Teradata dataset.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="a14d5-161">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="a14d5-161">Copy activity properties</span></span>
<span data-ttu-id="a14d5-162">Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="a14d5-162">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a14d5-163">Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités.</span><span class="sxs-lookup"><span data-stu-id="a14d5-163">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="a14d5-164">Alors que les propriétés disponibles dans la section typeProperties hello activité hello varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="a14d5-164">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="a14d5-165">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="a14d5-165">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="a14d5-166">Lorsque la source de hello est de type **RelationalSource** (qui inclut Teradata), hello propriétés suivantes est disponible dans **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="a14d5-166">When hello source is of type **RelationalSource** (which includes Teradata), hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="a14d5-167">Propriété</span><span class="sxs-lookup"><span data-stu-id="a14d5-167">Property</span></span> | <span data-ttu-id="a14d5-168">Description</span><span class="sxs-lookup"><span data-stu-id="a14d5-168">Description</span></span> | <span data-ttu-id="a14d5-169">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="a14d5-169">Allowed values</span></span> | <span data-ttu-id="a14d5-170">Requis</span><span class="sxs-lookup"><span data-stu-id="a14d5-170">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a14d5-171">query</span><span class="sxs-lookup"><span data-stu-id="a14d5-171">query</span></span> |<span data-ttu-id="a14d5-172">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="a14d5-172">Use hello custom query tooread data.</span></span> |<span data-ttu-id="a14d5-173">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="a14d5-173">SQL query string.</span></span> <span data-ttu-id="a14d5-174">Par exemple : select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="a14d5-174">For example: select * from MyTable.</span></span> |<span data-ttu-id="a14d5-175">Oui</span><span class="sxs-lookup"><span data-stu-id="a14d5-175">Yes</span></span> |

### <a name="json-example-copy-data-from-teradata-tooazure-blob"></a><span data-ttu-id="a14d5-176">Exemple de JSON : copier des données Teradata tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="a14d5-176">JSON example: Copy data from Teradata tooAzure Blob</span></span>
<span data-ttu-id="a14d5-177">Hello exemple suivant fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a14d5-177">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="a14d5-178">Elles montrent comment toocopy des données à partir de Teradata tooAzure stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="a14d5-178">They show how toocopy data from Teradata tooAzure Blob Storage.</span></span> <span data-ttu-id="a14d5-179">Toutefois, les données peuvent être copié tooany de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a14d5-179">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="a14d5-180">exemple Hello a hello suivant des entités de fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="a14d5-180">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="a14d5-181">Un service lié de type [OnPremisesTeradata](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a14d5-181">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span></span>
2. <span data-ttu-id="a14d5-182">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a14d5-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a14d5-183">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a14d5-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="a14d5-184">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a14d5-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="a14d5-185">Hello [pipeline](data-factory-create-pipelines.md) avec l’activité de copie qui utilise [RelationalSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a14d5-185">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a14d5-186">exemple Hello copie des données à partir d’un résultat de requête dans l’objet blob tooa de base de données Teradata toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="a14d5-186">hello sample copies data from a query result in Teradata database tooa blob every hour.</span></span> <span data-ttu-id="a14d5-187">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="a14d5-187">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="a14d5-188">Dans un premier temps, le programme d’installation passerelle de gestion des données hello.</span><span class="sxs-lookup"><span data-stu-id="a14d5-188">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="a14d5-189">instructions de Hello sont Bonjour [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="a14d5-189">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="a14d5-190">**Service lié Teradata :**</span><span class="sxs-lookup"><span data-stu-id="a14d5-190">**Teradata linked service:**</span></span>

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

<span data-ttu-id="a14d5-191">**Service lié Azure Blob Storage :**</span><span class="sxs-lookup"><span data-stu-id="a14d5-191">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="a14d5-192">**Jeu de données d’entrée Teradata :**</span><span class="sxs-lookup"><span data-stu-id="a14d5-192">**Teradata input dataset:**</span></span>

<span data-ttu-id="a14d5-193">exemple Hello suppose que vous avez créé une table « MyTable » dans Teradata et il contienne une colonne appelée « timestamp » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="a14d5-193">hello sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="a14d5-194">Paramètre « external » : true informe le service de fabrique de données hello cette table hello est la fabrique de données externe toohello et n’est pas générée par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="a14d5-194">Setting “external”: true informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="a14d5-195">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="a14d5-195">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="a14d5-196">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="a14d5-196">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="a14d5-197">chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="a14d5-197">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="a14d5-198">chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="a14d5-198">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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
<span data-ttu-id="a14d5-199">**Pipeline avec activité de copie :**</span><span class="sxs-lookup"><span data-stu-id="a14d5-199">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="a14d5-200">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="a14d5-200">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="a14d5-201">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**RelationalSource** et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="a14d5-201">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="a14d5-202">la requête SQL Hello spécifiée pour hello **requête** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.</span><span class="sxs-lookup"><span data-stu-id="a14d5-202">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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
## <a name="type-mapping-for-teradata"></a><span data-ttu-id="a14d5-203">Mappage de type pour Teradata</span><span class="sxs-lookup"><span data-stu-id="a14d5-203">Type mapping for Teradata</span></span>
<span data-ttu-id="a14d5-204">Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, hello activité de copie effectue les conversions de type automatique à partir de types de sources de toosink types avec hello approche de l’étape 2 :</span><span class="sxs-lookup"><span data-stu-id="a14d5-204">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="a14d5-205">Convertir à partir de la source native types too.NET type</span><span class="sxs-lookup"><span data-stu-id="a14d5-205">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="a14d5-206">Conversion de type de récepteur de toonative de type .NET</span><span class="sxs-lookup"><span data-stu-id="a14d5-206">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="a14d5-207">Lorsque vous déplacez des données tooTeradata, hello mappages suivants sont utilisés à partir du type too.NET de type Teradata.</span><span class="sxs-lookup"><span data-stu-id="a14d5-207">When moving data tooTeradata, hello following mappings are used from Teradata type too.NET type.</span></span>

| <span data-ttu-id="a14d5-208">Type de base de données Teradata</span><span class="sxs-lookup"><span data-stu-id="a14d5-208">Teradata Database type</span></span> | <span data-ttu-id="a14d5-209">Type de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="a14d5-209">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="a14d5-210">Char</span><span class="sxs-lookup"><span data-stu-id="a14d5-210">Char</span></span> |<span data-ttu-id="a14d5-211">String</span><span class="sxs-lookup"><span data-stu-id="a14d5-211">String</span></span> |
| <span data-ttu-id="a14d5-212">Clob</span><span class="sxs-lookup"><span data-stu-id="a14d5-212">Clob</span></span> |<span data-ttu-id="a14d5-213">String</span><span class="sxs-lookup"><span data-stu-id="a14d5-213">String</span></span> |
| <span data-ttu-id="a14d5-214">Graphic</span><span class="sxs-lookup"><span data-stu-id="a14d5-214">Graphic</span></span> |<span data-ttu-id="a14d5-215">String</span><span class="sxs-lookup"><span data-stu-id="a14d5-215">String</span></span> |
| <span data-ttu-id="a14d5-216">VarChar</span><span class="sxs-lookup"><span data-stu-id="a14d5-216">VarChar</span></span> |<span data-ttu-id="a14d5-217">String</span><span class="sxs-lookup"><span data-stu-id="a14d5-217">String</span></span> |
| <span data-ttu-id="a14d5-218">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="a14d5-218">VarGraphic</span></span> |<span data-ttu-id="a14d5-219">String</span><span class="sxs-lookup"><span data-stu-id="a14d5-219">String</span></span> |
| <span data-ttu-id="a14d5-220">Blob</span><span class="sxs-lookup"><span data-stu-id="a14d5-220">Blob</span></span> |<span data-ttu-id="a14d5-221">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a14d5-221">Byte[]</span></span> |
| <span data-ttu-id="a14d5-222">Byte</span><span class="sxs-lookup"><span data-stu-id="a14d5-222">Byte</span></span> |<span data-ttu-id="a14d5-223">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a14d5-223">Byte[]</span></span> |
| <span data-ttu-id="a14d5-224">VarByte</span><span class="sxs-lookup"><span data-stu-id="a14d5-224">VarByte</span></span> |<span data-ttu-id="a14d5-225">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a14d5-225">Byte[]</span></span> |
| <span data-ttu-id="a14d5-226">BigInt</span><span class="sxs-lookup"><span data-stu-id="a14d5-226">BigInt</span></span> |<span data-ttu-id="a14d5-227">Int64</span><span class="sxs-lookup"><span data-stu-id="a14d5-227">Int64</span></span> |
| <span data-ttu-id="a14d5-228">ByteInt</span><span class="sxs-lookup"><span data-stu-id="a14d5-228">ByteInt</span></span> |<span data-ttu-id="a14d5-229">Int16</span><span class="sxs-lookup"><span data-stu-id="a14d5-229">Int16</span></span> |
| <span data-ttu-id="a14d5-230">Décimal</span><span class="sxs-lookup"><span data-stu-id="a14d5-230">Decimal</span></span> |<span data-ttu-id="a14d5-231">Décimal</span><span class="sxs-lookup"><span data-stu-id="a14d5-231">Decimal</span></span> |
| <span data-ttu-id="a14d5-232">Double</span><span class="sxs-lookup"><span data-stu-id="a14d5-232">Double</span></span> |<span data-ttu-id="a14d5-233">Double</span><span class="sxs-lookup"><span data-stu-id="a14d5-233">Double</span></span> |
| <span data-ttu-id="a14d5-234">Integer</span><span class="sxs-lookup"><span data-stu-id="a14d5-234">Integer</span></span> |<span data-ttu-id="a14d5-235">Int32</span><span class="sxs-lookup"><span data-stu-id="a14d5-235">Int32</span></span> |
| <span data-ttu-id="a14d5-236">Number</span><span class="sxs-lookup"><span data-stu-id="a14d5-236">Number</span></span> |<span data-ttu-id="a14d5-237">Double</span><span class="sxs-lookup"><span data-stu-id="a14d5-237">Double</span></span> |
| <span data-ttu-id="a14d5-238">SmallInt</span><span class="sxs-lookup"><span data-stu-id="a14d5-238">SmallInt</span></span> |<span data-ttu-id="a14d5-239">Int16</span><span class="sxs-lookup"><span data-stu-id="a14d5-239">Int16</span></span> |
| <span data-ttu-id="a14d5-240">Date</span><span class="sxs-lookup"><span data-stu-id="a14d5-240">Date</span></span> |<span data-ttu-id="a14d5-241">DateTime</span><span class="sxs-lookup"><span data-stu-id="a14d5-241">DateTime</span></span> |
| <span data-ttu-id="a14d5-242">Time</span><span class="sxs-lookup"><span data-stu-id="a14d5-242">Time</span></span> |<span data-ttu-id="a14d5-243">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a14d5-243">TimeSpan</span></span> |
| <span data-ttu-id="a14d5-244">Time With Time Zone</span><span class="sxs-lookup"><span data-stu-id="a14d5-244">Time With Time Zone</span></span> |<span data-ttu-id="a14d5-245">String</span><span class="sxs-lookup"><span data-stu-id="a14d5-245">String</span></span> |
| <span data-ttu-id="a14d5-246">Timestamp</span><span class="sxs-lookup"><span data-stu-id="a14d5-246">Timestamp</span></span> |<span data-ttu-id="a14d5-247">DateTime</span><span class="sxs-lookup"><span data-stu-id="a14d5-247">DateTime</span></span> |
| <span data-ttu-id="a14d5-248">Timestamp With Time Zone</span><span class="sxs-lookup"><span data-stu-id="a14d5-248">Timestamp With Time Zone</span></span> |<span data-ttu-id="a14d5-249">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="a14d5-249">DateTimeOffset</span></span> |
| <span data-ttu-id="a14d5-250">Interval Day</span><span class="sxs-lookup"><span data-stu-id="a14d5-250">Interval Day</span></span> |<span data-ttu-id="a14d5-251">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a14d5-251">TimeSpan</span></span> |
| <span data-ttu-id="a14d5-252">Intervalle jour tooHour</span><span class="sxs-lookup"><span data-stu-id="a14d5-252">Interval Day tooHour</span></span> |<span data-ttu-id="a14d5-253">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a14d5-253">TimeSpan</span></span> |
| <span data-ttu-id="a14d5-254">Intervalle jour tooMinute</span><span class="sxs-lookup"><span data-stu-id="a14d5-254">Interval Day tooMinute</span></span> |<span data-ttu-id="a14d5-255">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a14d5-255">TimeSpan</span></span> |
| <span data-ttu-id="a14d5-256">Intervalle jour tooSecond</span><span class="sxs-lookup"><span data-stu-id="a14d5-256">Interval Day tooSecond</span></span> |<span data-ttu-id="a14d5-257">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a14d5-257">TimeSpan</span></span> |
| <span data-ttu-id="a14d5-258">Interval Hour</span><span class="sxs-lookup"><span data-stu-id="a14d5-258">Interval Hour</span></span> |<span data-ttu-id="a14d5-259">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a14d5-259">TimeSpan</span></span> |
| <span data-ttu-id="a14d5-260">Intervalle heure tooMinute</span><span class="sxs-lookup"><span data-stu-id="a14d5-260">Interval Hour tooMinute</span></span> |<span data-ttu-id="a14d5-261">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a14d5-261">TimeSpan</span></span> |
| <span data-ttu-id="a14d5-262">Intervalle heure tooSecond</span><span class="sxs-lookup"><span data-stu-id="a14d5-262">Interval Hour tooSecond</span></span> |<span data-ttu-id="a14d5-263">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a14d5-263">TimeSpan</span></span> |
| <span data-ttu-id="a14d5-264">Interval Minute</span><span class="sxs-lookup"><span data-stu-id="a14d5-264">Interval Minute</span></span> |<span data-ttu-id="a14d5-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a14d5-265">TimeSpan</span></span> |
| <span data-ttu-id="a14d5-266">TooSecond minutes d’intervalle</span><span class="sxs-lookup"><span data-stu-id="a14d5-266">Interval Minute tooSecond</span></span> |<span data-ttu-id="a14d5-267">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a14d5-267">TimeSpan</span></span> |
| <span data-ttu-id="a14d5-268">Interval Second</span><span class="sxs-lookup"><span data-stu-id="a14d5-268">Interval Second</span></span> |<span data-ttu-id="a14d5-269">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a14d5-269">TimeSpan</span></span> |
| <span data-ttu-id="a14d5-270">Interval Year</span><span class="sxs-lookup"><span data-stu-id="a14d5-270">Interval Year</span></span> |<span data-ttu-id="a14d5-271">String</span><span class="sxs-lookup"><span data-stu-id="a14d5-271">String</span></span> |
| <span data-ttu-id="a14d5-272">Intervalle année tooMonth</span><span class="sxs-lookup"><span data-stu-id="a14d5-272">Interval Year tooMonth</span></span> |<span data-ttu-id="a14d5-273">String</span><span class="sxs-lookup"><span data-stu-id="a14d5-273">String</span></span> |
| <span data-ttu-id="a14d5-274">Interval Month</span><span class="sxs-lookup"><span data-stu-id="a14d5-274">Interval Month</span></span> |<span data-ttu-id="a14d5-275">String</span><span class="sxs-lookup"><span data-stu-id="a14d5-275">String</span></span> |
| <span data-ttu-id="a14d5-276">Period(Date)</span><span class="sxs-lookup"><span data-stu-id="a14d5-276">Period(Date)</span></span> |<span data-ttu-id="a14d5-277">String</span><span class="sxs-lookup"><span data-stu-id="a14d5-277">String</span></span> |
| <span data-ttu-id="a14d5-278">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="a14d5-278">Period(Time)</span></span> |<span data-ttu-id="a14d5-279">String</span><span class="sxs-lookup"><span data-stu-id="a14d5-279">String</span></span> |
| <span data-ttu-id="a14d5-280">Period(Time With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="a14d5-280">Period(Time With Time Zone)</span></span> |<span data-ttu-id="a14d5-281">String</span><span class="sxs-lookup"><span data-stu-id="a14d5-281">String</span></span> |
| <span data-ttu-id="a14d5-282">Period(Timestamp)</span><span class="sxs-lookup"><span data-stu-id="a14d5-282">Period(Timestamp)</span></span> |<span data-ttu-id="a14d5-283">String</span><span class="sxs-lookup"><span data-stu-id="a14d5-283">String</span></span> |
| <span data-ttu-id="a14d5-284">Period(Timestamp With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="a14d5-284">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="a14d5-285">String</span><span class="sxs-lookup"><span data-stu-id="a14d5-285">String</span></span> |
| <span data-ttu-id="a14d5-286">Xml</span><span class="sxs-lookup"><span data-stu-id="a14d5-286">Xml</span></span> |<span data-ttu-id="a14d5-287">String</span><span class="sxs-lookup"><span data-stu-id="a14d5-287">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="a14d5-288">Mapper les colonnes de source toosink</span><span class="sxs-lookup"><span data-stu-id="a14d5-288">Map source toosink columns</span></span>
<span data-ttu-id="a14d5-289">toolearn sur le mappage des colonnes dans toocolumns du jeu de données source dans le jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="a14d5-289">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="a14d5-290">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="a14d5-290">Repeatable read from relational sources</span></span>
<span data-ttu-id="a14d5-291">Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="a14d5-291">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="a14d5-292">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="a14d5-292">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="a14d5-293">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="a14d5-293">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="a14d5-294">Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée.</span><span class="sxs-lookup"><span data-stu-id="a14d5-294">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="a14d5-295">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="a14d5-295">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="a14d5-296">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="a14d5-296">Performance and Tuning</span></span>
<span data-ttu-id="a14d5-297">Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="a14d5-297">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
