---
title: "aaaMove des données à partir de SAP Business Warehouse à l’aide d’Azure Data Factory | Documents Microsoft"
description: "En savoir plus sur la façon de toomove les données à partir de SAP Business Warehouse à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 85df16f4759a846f578cad301e3cf918179143d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a><span data-ttu-id="2a7fb-103">Déplacer des données depuis SAP Business Warehouse à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="2a7fb-103">Move data From SAP Business Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="2a7fb-104">Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory dans un local SAP Business Warehouse (BW).</span><span class="sxs-lookup"><span data-stu-id="2a7fb-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises SAP Business Warehouse (BW).</span></span> <span data-ttu-id="2a7fb-105">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="2a7fb-106">Vous pouvez copier les données d’une banque de données locale SAP Business Warehouse données magasin tooany pris en charge récepteur.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-106">You can copy data from an on-premises SAP Business Warehouse data store tooany supported sink data store.</span></span> <span data-ttu-id="2a7fb-107">Pour une liste de données pris en charge des magasins récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="2a7fb-108">Fabrique de données prend actuellement en charge uniquement le déplacement de données à partir d’un tooother de données SAP Business Warehouse stocke, mais pas pour déplacer des données d’autres données de magasins tooan SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-108">Data factory currently supports only moving data from an SAP Business Warehouse tooother data stores, but not for moving data from other data stores tooan SAP Business Warehouse.</span></span> 

## <a name="supported-versions-and-installation"></a><span data-ttu-id="2a7fb-109">Versions prises en charge et installation</span><span class="sxs-lookup"><span data-stu-id="2a7fb-109">Supported versions and installation</span></span>
<span data-ttu-id="2a7fb-110">Ce connecteur prend en charge la version 7.x de SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-110">This connector supports SAP Business Warehouse version 7.x.</span></span> <span data-ttu-id="2a7fb-111">Il prend en charge la copie de données d’InfoCubes et de QueryCubes (y compris les requêtes BEx) à l’aide de requêtes MDX.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-111">It supports copying data from InfoCubes and QueryCubes (including BEx queries) using MDX queries.</span></span>

<span data-ttu-id="2a7fb-112">tooenable hello connectivité toohello instance de SAP BW, installez hello suivant des composants :</span><span class="sxs-lookup"><span data-stu-id="2a7fb-112">tooenable hello connectivity toohello SAP BW instance, install hello following components:</span></span>
- <span data-ttu-id="2a7fb-113">**Passerelle de gestion des données**: service Data Factory prend en charge la connexion de données locales tooon magasins (y compris SAP Business Warehouse) à l’aide d’un composant appelé passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-113">**Data Management Gateway**: Data Factory service supports connecting tooon-premises data stores (including SAP Business Warehouse) using a component called Data Management Gateway.</span></span> <span data-ttu-id="2a7fb-114">toolearn sur la passerelle de gestion des données et des instructions détaillées pour configurer la passerelle de hello, consultez [magasin de données toocloud du magasin de données de déplacement entre des données locales](data-factory-move-data-between-onprem-and-cloud.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-114">toolearn about Data Management Gateway and step-by-step instructions for setting up hello gateway, see [Moving data between on-premises data store toocloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="2a7fb-115">Passerelle est requise même si hello SAP Business Warehouse est hébergé dans une machine virtuelle de Azure IaaS (VM).</span><span class="sxs-lookup"><span data-stu-id="2a7fb-115">Gateway is required even if hello SAP Business Warehouse is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="2a7fb-116">Vous pouvez installer la passerelle de hello sur hello même machine virtuelle en tant que données de hello stocker ou sur un ordinateur différent virtuel tant que passerelle de hello peuvent se connecter toohello de base de données.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-116">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>
- <span data-ttu-id="2a7fb-117">**Bibliothèque de SAP NetWeaver** sur l’ordinateur de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-117">**SAP NetWeaver library** on hello gateway machine.</span></span> <span data-ttu-id="2a7fb-118">Vous pouvez obtenir la bibliothèque de SAP Netweaver hello auprès de votre administrateur SAP ou directement à partir de hello [centre de téléchargement de logiciel SAP](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="2a7fb-118">You can get hello SAP Netweaver library from your SAP administrator, or directly from hello [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="2a7fb-119">Recherchez hello **SAP Remarque #1025361** emplacement de téléchargement tooget hello pour la version la plus récente hello.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-119">Search for hello **SAP Note #1025361** tooget hello download location for hello most recent version.</span></span> <span data-ttu-id="2a7fb-120">Assurez-vous qu’architecture hello pour la bibliothèque de SAP NetWeaver hello (32 bits ou 64 bits) correspond à votre installation de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-120">Make sure that hello architecture for hello SAP NetWeaver library (32-bit or 64-bit) matches your gateway installation.</span></span> <span data-ttu-id="2a7fb-121">Ensuite, installez tous les fichiers inclus dans toohello en fonction du Kit de développement logiciel SAP NetWeaver RFC hello la Note SAP.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-121">Then install all files included in hello SAP NetWeaver RFC SDK according toohello SAP Note.</span></span> <span data-ttu-id="2a7fb-122">bibliothèque de SAP NetWeaver Hello est également inclus dans hello l’installation des outils du Client SAP.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-122">hello SAP NetWeaver library is also included in hello SAP Client Tools installation.</span></span>

> [!TIP]
> <span data-ttu-id="2a7fb-123">Placez les DLL hello extraites hello SDK de RFC NetWeaver dans le dossier system32.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-123">Put hello dlls extracted from hello NetWeaver RFC SDK into system32 folder.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2a7fb-124">Prise en main</span><span class="sxs-lookup"><span data-stu-id="2a7fb-124">Getting started</span></span>
<span data-ttu-id="2a7fb-125">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données Cassandra local à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-125">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="2a7fb-126">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-126">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="2a7fb-127">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="2a7fb-128">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-128">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="2a7fb-129">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="2a7fb-130">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="2a7fb-130">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="2a7fb-131">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-131">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="2a7fb-132">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="2a7fb-133">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="2a7fb-134">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-134">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="2a7fb-135">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="2a7fb-136">Pour voir un exemple avec des définitions pour les entités de fabrique de données qui sont utilisées toocopy des données à partir d’un local SAP Business Warehouse JSON, [exemple de JSON : copier des données à partir de SAP Business Warehouse tooAzure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-136">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises SAP Business Warehouse, see [JSON example: Copy data from SAP Business Warehouse tooAzure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="2a7fb-137">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont le magasin de données SAP BW utilisé toodefine Data Factory entités tooan spécifique :</span><span class="sxs-lookup"><span data-stu-id="2a7fb-137">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooan SAP BW data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="2a7fb-138">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="2a7fb-138">Linked service properties</span></span>
<span data-ttu-id="2a7fb-139">Hello tableau suivant fournit la description pour JSON éléments tooSAP spécifique Business Warehouse (BW) lié service.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-139">hello following table provides description for JSON elements specific tooSAP Business Warehouse (BW) linked service.</span></span>

<span data-ttu-id="2a7fb-140">Propriété</span><span class="sxs-lookup"><span data-stu-id="2a7fb-140">Property</span></span> | <span data-ttu-id="2a7fb-141">Description</span><span class="sxs-lookup"><span data-stu-id="2a7fb-141">Description</span></span> | <span data-ttu-id="2a7fb-142">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="2a7fb-142">Allowed values</span></span> | <span data-ttu-id="2a7fb-143">Requis</span><span class="sxs-lookup"><span data-stu-id="2a7fb-143">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="2a7fb-144">server</span><span class="sxs-lookup"><span data-stu-id="2a7fb-144">server</span></span> | <span data-ttu-id="2a7fb-145">Nom du serveur hello sur quel hello SAP BW instance réside.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-145">Name of hello server on which hello SAP BW instance resides.</span></span> | <span data-ttu-id="2a7fb-146">string</span><span class="sxs-lookup"><span data-stu-id="2a7fb-146">string</span></span> | <span data-ttu-id="2a7fb-147">Oui</span><span class="sxs-lookup"><span data-stu-id="2a7fb-147">Yes</span></span>
<span data-ttu-id="2a7fb-148">systemNumber</span><span class="sxs-lookup"><span data-stu-id="2a7fb-148">systemNumber</span></span> | <span data-ttu-id="2a7fb-149">Numéro de système de hello système SAP BW.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-149">System number of hello SAP BW system.</span></span> | <span data-ttu-id="2a7fb-150">Nombre décimal à deux chiffres représenté sous forme de chaîne.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-150">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="2a7fb-151">Oui</span><span class="sxs-lookup"><span data-stu-id="2a7fb-151">Yes</span></span>
<span data-ttu-id="2a7fb-152">clientId</span><span class="sxs-lookup"><span data-stu-id="2a7fb-152">clientId</span></span> | <span data-ttu-id="2a7fb-153">ID client du client hello Bonjour système SAP W.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-153">Client ID of hello client in hello SAP W system.</span></span> | <span data-ttu-id="2a7fb-154">Nombre décimal à trois chiffres représenté sous forme de chaîne.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-154">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="2a7fb-155">Oui</span><span class="sxs-lookup"><span data-stu-id="2a7fb-155">Yes</span></span>
<span data-ttu-id="2a7fb-156">username</span><span class="sxs-lookup"><span data-stu-id="2a7fb-156">username</span></span> | <span data-ttu-id="2a7fb-157">Nom d’utilisateur de hello qui a le serveur d’accès toohello SAP</span><span class="sxs-lookup"><span data-stu-id="2a7fb-157">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="2a7fb-158">string</span><span class="sxs-lookup"><span data-stu-id="2a7fb-158">string</span></span> | <span data-ttu-id="2a7fb-159">Oui</span><span class="sxs-lookup"><span data-stu-id="2a7fb-159">Yes</span></span>
<span data-ttu-id="2a7fb-160">password</span><span class="sxs-lookup"><span data-stu-id="2a7fb-160">password</span></span> | <span data-ttu-id="2a7fb-161">Mot de passe utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-161">Password for hello user.</span></span> | <span data-ttu-id="2a7fb-162">string</span><span class="sxs-lookup"><span data-stu-id="2a7fb-162">string</span></span> | <span data-ttu-id="2a7fb-163">Oui</span><span class="sxs-lookup"><span data-stu-id="2a7fb-163">Yes</span></span>
<span data-ttu-id="2a7fb-164">gatewayName</span><span class="sxs-lookup"><span data-stu-id="2a7fb-164">gatewayName</span></span> | <span data-ttu-id="2a7fb-165">Nom de passerelle hello hello service Data Factory doit utiliser l’instance de SAP BW tooconnect toohello sur site.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-165">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP BW instance.</span></span> | <span data-ttu-id="2a7fb-166">string</span><span class="sxs-lookup"><span data-stu-id="2a7fb-166">string</span></span> | <span data-ttu-id="2a7fb-167">Oui</span><span class="sxs-lookup"><span data-stu-id="2a7fb-167">Yes</span></span>
<span data-ttu-id="2a7fb-168">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="2a7fb-168">encryptedCredential</span></span> | <span data-ttu-id="2a7fb-169">chaîne d’identification de Hello chiffré.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-169">hello encrypted credential string.</span></span> | <span data-ttu-id="2a7fb-170">string</span><span class="sxs-lookup"><span data-stu-id="2a7fb-170">string</span></span> | <span data-ttu-id="2a7fb-171">Non</span><span class="sxs-lookup"><span data-stu-id="2a7fb-171">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="2a7fb-172">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="2a7fb-172">Dataset properties</span></span>
<span data-ttu-id="2a7fb-173">Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-173">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="2a7fb-174">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="2a7fb-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="2a7fb-175">Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-175">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="2a7fb-176">Aucune propriété spécifique au type pris en charge pour le jeu de données hello SAP BW de type **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-176">There are no type-specific properties supported for hello SAP BW dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="2a7fb-177">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="2a7fb-177">Copy activity properties</span></span>
<span data-ttu-id="2a7fb-178">Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-178">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2a7fb-179">Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-179">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="2a7fb-180">Tandis que les propriétés disponibles dans hello **typeProperties** section d’activité hello varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-180">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="2a7fb-181">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-181">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="2a7fb-182">Lorsque la source de l’activité de copie est de type **RelationalSource** (qui inclut SAP BW), hello propriétés suivantes est disponible dans la section de typeProperties :</span><span class="sxs-lookup"><span data-stu-id="2a7fb-182">When source in copy activity is of type **RelationalSource** (which includes SAP BW), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="2a7fb-183">Propriété</span><span class="sxs-lookup"><span data-stu-id="2a7fb-183">Property</span></span> | <span data-ttu-id="2a7fb-184">Description</span><span class="sxs-lookup"><span data-stu-id="2a7fb-184">Description</span></span> | <span data-ttu-id="2a7fb-185">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="2a7fb-185">Allowed values</span></span> | <span data-ttu-id="2a7fb-186">Requis</span><span class="sxs-lookup"><span data-stu-id="2a7fb-186">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2a7fb-187">query</span><span class="sxs-lookup"><span data-stu-id="2a7fb-187">query</span></span> | <span data-ttu-id="2a7fb-188">Spécifie les données de tooread requête hello MDX à partir de l’instance de SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-188">Specifies hello MDX query tooread data from hello SAP BW instance.</span></span> | <span data-ttu-id="2a7fb-189">Requête MDX.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-189">MDX query.</span></span> | <span data-ttu-id="2a7fb-190">Oui</span><span class="sxs-lookup"><span data-stu-id="2a7fb-190">Yes</span></span> |


## <a name="json-example-copy-data-from-sap-business-warehouse-tooazure-blob"></a><span data-ttu-id="2a7fb-191">Exemple de JSON : copier des données à partir de SAP Business Warehouse tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="2a7fb-191">JSON example: Copy data from SAP Business Warehouse tooAzure Blob</span></span>
<span data-ttu-id="2a7fb-192">Hello exemple suivant fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2a7fb-192">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="2a7fb-193">Cet exemple montre comment toocopy des données à partir d’un tooan de SAP Business Warehouse locale stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-193">This sample shows how toocopy data from an on-premises SAP Business Warehouse tooan Azure Blob Storage.</span></span> <span data-ttu-id="2a7fb-194">Toutefois, les données peuvent être copiées **directement** tooany de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-194">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="2a7fb-195">Cet exemple fournit des extraits de code JSON.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-195">This sample provides JSON snippets.</span></span> <span data-ttu-id="2a7fb-196">Il n’inclut pas d’instructions détaillées pour créer la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-196">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="2a7fb-197">Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="2a7fb-197">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="2a7fb-198">exemple Hello a hello suivant des entités de fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="2a7fb-198">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="2a7fb-199">Un service lié de type [SapBw](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2a7fb-199">A linked service of type [SapBw](#linked-service-properties).</span></span>
2. <span data-ttu-id="2a7fb-200">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2a7fb-200">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="2a7fb-201">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2a7fb-201">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="2a7fb-202">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2a7fb-202">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="2a7fb-203">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [RelationalSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="2a7fb-203">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="2a7fb-204">exemple Hello copie toutes les heures des données à partir d’un tooan d’instance SAP Business Warehouse blob Azure.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-204">hello sample copies data from an SAP Business Warehouse instance tooan Azure blob hourly.</span></span> <span data-ttu-id="2a7fb-205">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-205">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="2a7fb-206">Dans un premier temps, le programme d’installation passerelle de gestion des données hello.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-206">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="2a7fb-207">instructions de Hello sont Bonjour [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-207">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-business-warehouse-linked-service"></a><span data-ttu-id="2a7fb-208">Service lié SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="2a7fb-208">SAP Business Warehouse linked service</span></span>
<span data-ttu-id="2a7fb-209">Cela lié à des liens de service votre fabrique de données toohello instance SAP BW.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-209">This linked service links your SAP BW instance toohello data factory.</span></span> <span data-ttu-id="2a7fb-210">propriété de type Hello est définie trop**SapBw**.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-210">hello type property is set too**SapBw**.</span></span> <span data-ttu-id="2a7fb-211">section de typeProperties Hello fournit des informations de connexion pour l’instance de SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-211">hello typeProperties section provides connection information for hello SAP BW instance.</span></span> 

```json
{
    "name": "SapBwLinkedService",
    "properties":
    {
        "type": "SapBw",
        "typeProperties":
        {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="2a7fb-212">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="2a7fb-212">Azure Storage linked service</span></span>
<span data-ttu-id="2a7fb-213">Cela lié à des liens de service votre fabrique de données toohello compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-213">This linked service links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="2a7fb-214">propriété de type Hello est définie trop**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-214">hello type property is set too**AzureStorage**.</span></span> <span data-ttu-id="2a7fb-215">section de typeProperties Hello fournit des informations de connexion pour hello compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-215">hello typeProperties section provides connection information for hello Azure Storage account.</span></span>

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

### <a name="sap-bw-input-dataset"></a><span data-ttu-id="2a7fb-216">Jeu de données d’entrée SAP BW</span><span class="sxs-lookup"><span data-stu-id="2a7fb-216">SAP BW input dataset</span></span>
<span data-ttu-id="2a7fb-217">Ce jeu de données définit un jeu de données SAP Business Warehouse hello.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-217">This dataset defines hello SAP Business Warehouse dataset.</span></span> <span data-ttu-id="2a7fb-218">Vous définissez type hello du jeu de données de Data Factory hello trop**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-218">You set hello type of hello Data Factory dataset too**RelationalTable**.</span></span> <span data-ttu-id="2a7fb-219">Actuellement, vous ne spécifiez pas de propriétés propres à un type pour un jeu de données SAP BW.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-219">Currently, you do not specify any type-specific properties for an SAP BW dataset.</span></span> <span data-ttu-id="2a7fb-220">requête Hello dans la définition de l’activité de copie de hello spécifie quel tooread de données à partir de l’instance de SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-220">hello query in hello Copy Activity definition specifies what data tooread from hello SAP BW instance.</span></span> 

<span data-ttu-id="2a7fb-221">Définition de propriété externe tootrue informe service Data Factory de hello cette table hello est la fabrique de données externe toohello n’est pas générée par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-221">Setting external property tootrue informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="2a7fb-222">Propriétés de la fréquence et l’intervalle définit la planification de hello.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-222">Frequency and interval properties defines hello schedule.</span></span> <span data-ttu-id="2a7fb-223">Dans ce cas, les données de salutation sont en lecture à partir de l’instance de SAP BW hello toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-223">In this case, hello data is read from hello SAP BW instance hourly.</span></span> 

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```



### <a name="azure-blob-output-dataset"></a><span data-ttu-id="2a7fb-224">Jeu de données de sortie d’objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="2a7fb-224">Azure Blob output dataset</span></span>
<span data-ttu-id="2a7fb-225">Ce jeu de données définit un jeu de données objet Blob Azure hello sortie.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-225">This dataset defines hello output Azure Blob dataset.</span></span> <span data-ttu-id="2a7fb-226">propriété de type Hello est définie à tooAzureBlob.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-226">hello type property is set tooAzureBlob.</span></span> <span data-ttu-id="2a7fb-227">section de typeProperties Hello fournit où sont stockées les données hello copiées à partir de l’instance de SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-227">hello typeProperties section provides where hello data copied from hello SAP BW instance is stored.</span></span> <span data-ttu-id="2a7fb-228">les données de salutation sont écrit tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="2a7fb-228">hello data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="2a7fb-229">chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-229">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="2a7fb-230">chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-230">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sapbw/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="2a7fb-231">Pipeline avec activité de copie</span><span class="sxs-lookup"><span data-stu-id="2a7fb-231">Pipeline with Copy activity</span></span>
<span data-ttu-id="2a7fb-232">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-232">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="2a7fb-233">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**RelationalSource** (pour la source SAP BW) et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-233">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** (for SAP BW source) and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="2a7fb-234">requête Hello spécifié pour hello **requête** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-234">hello query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<MDX query for SAP BW>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapBwDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
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
                "name": "SapBwToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```



### <a name="type-mapping-for-sap-bw"></a><span data-ttu-id="2a7fb-235">Mappage de type pour SAP BW</span><span class="sxs-lookup"><span data-stu-id="2a7fb-235">Type mapping for SAP BW</span></span>
<span data-ttu-id="2a7fb-236">Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, l’activité de copie effectue les conversions de type automatique à partir de types de sources de toosink types avec hello suivant l’approche en deux étapes :</span><span class="sxs-lookup"><span data-stu-id="2a7fb-236">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="2a7fb-237">Convertir à partir de la source native types too.NET type</span><span class="sxs-lookup"><span data-stu-id="2a7fb-237">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="2a7fb-238">Conversion de type de récepteur de toonative de type .NET</span><span class="sxs-lookup"><span data-stu-id="2a7fb-238">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="2a7fb-239">Lors du déplacement des données à partir de SAP BW, hello suivant les mappages est utilisé à partir de types de too.NET de types de SAP BW.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-239">When moving data from SAP BW, hello following mappings are used from SAP BW types too.NET types.</span></span>

<span data-ttu-id="2a7fb-240">Type de données Bonjour ABAP dictionnaire</span><span class="sxs-lookup"><span data-stu-id="2a7fb-240">Data type in hello ABAP Dictionary</span></span> | <span data-ttu-id="2a7fb-241">Type de données .Net</span><span class="sxs-lookup"><span data-stu-id="2a7fb-241">.Net Data Type</span></span>
-------------------------------- | --------------
<span data-ttu-id="2a7fb-242">ACCP</span><span class="sxs-lookup"><span data-stu-id="2a7fb-242">ACCP</span></span> |  <span data-ttu-id="2a7fb-243">int</span><span class="sxs-lookup"><span data-stu-id="2a7fb-243">Int</span></span>
<span data-ttu-id="2a7fb-244">CHAR</span><span class="sxs-lookup"><span data-stu-id="2a7fb-244">CHAR</span></span> | <span data-ttu-id="2a7fb-245">String</span><span class="sxs-lookup"><span data-stu-id="2a7fb-245">String</span></span>
<span data-ttu-id="2a7fb-246">CLNT</span><span class="sxs-lookup"><span data-stu-id="2a7fb-246">CLNT</span></span> | <span data-ttu-id="2a7fb-247">String</span><span class="sxs-lookup"><span data-stu-id="2a7fb-247">String</span></span>
<span data-ttu-id="2a7fb-248">CURR</span><span class="sxs-lookup"><span data-stu-id="2a7fb-248">CURR</span></span> | <span data-ttu-id="2a7fb-249">Décimal</span><span class="sxs-lookup"><span data-stu-id="2a7fb-249">Decimal</span></span>
<span data-ttu-id="2a7fb-250">CUKY</span><span class="sxs-lookup"><span data-stu-id="2a7fb-250">CUKY</span></span> | <span data-ttu-id="2a7fb-251">String</span><span class="sxs-lookup"><span data-stu-id="2a7fb-251">String</span></span>
<span data-ttu-id="2a7fb-252">DEC</span><span class="sxs-lookup"><span data-stu-id="2a7fb-252">DEC</span></span> | <span data-ttu-id="2a7fb-253">Décimal</span><span class="sxs-lookup"><span data-stu-id="2a7fb-253">Decimal</span></span>
<span data-ttu-id="2a7fb-254">FLTP</span><span class="sxs-lookup"><span data-stu-id="2a7fb-254">FLTP</span></span> | <span data-ttu-id="2a7fb-255">Double</span><span class="sxs-lookup"><span data-stu-id="2a7fb-255">Double</span></span>
<span data-ttu-id="2a7fb-256">INT1</span><span class="sxs-lookup"><span data-stu-id="2a7fb-256">INT1</span></span> | <span data-ttu-id="2a7fb-257">Byte</span><span class="sxs-lookup"><span data-stu-id="2a7fb-257">Byte</span></span>
<span data-ttu-id="2a7fb-258">INT2</span><span class="sxs-lookup"><span data-stu-id="2a7fb-258">INT2</span></span> | <span data-ttu-id="2a7fb-259">Int16</span><span class="sxs-lookup"><span data-stu-id="2a7fb-259">Int16</span></span>
<span data-ttu-id="2a7fb-260">INT4</span><span class="sxs-lookup"><span data-stu-id="2a7fb-260">INT4</span></span> | <span data-ttu-id="2a7fb-261">int</span><span class="sxs-lookup"><span data-stu-id="2a7fb-261">Int</span></span>
<span data-ttu-id="2a7fb-262">LANG</span><span class="sxs-lookup"><span data-stu-id="2a7fb-262">LANG</span></span> | <span data-ttu-id="2a7fb-263">String</span><span class="sxs-lookup"><span data-stu-id="2a7fb-263">String</span></span>
<span data-ttu-id="2a7fb-264">LCHR</span><span class="sxs-lookup"><span data-stu-id="2a7fb-264">LCHR</span></span> | <span data-ttu-id="2a7fb-265">String</span><span class="sxs-lookup"><span data-stu-id="2a7fb-265">String</span></span>
<span data-ttu-id="2a7fb-266">LRAW</span><span class="sxs-lookup"><span data-stu-id="2a7fb-266">LRAW</span></span> | <span data-ttu-id="2a7fb-267">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2a7fb-267">Byte[]</span></span>
<span data-ttu-id="2a7fb-268">PREC</span><span class="sxs-lookup"><span data-stu-id="2a7fb-268">PREC</span></span> | <span data-ttu-id="2a7fb-269">Int16</span><span class="sxs-lookup"><span data-stu-id="2a7fb-269">Int16</span></span>
<span data-ttu-id="2a7fb-270">QUAN</span><span class="sxs-lookup"><span data-stu-id="2a7fb-270">QUAN</span></span> | <span data-ttu-id="2a7fb-271">Décimal</span><span class="sxs-lookup"><span data-stu-id="2a7fb-271">Decimal</span></span>
<span data-ttu-id="2a7fb-272">RAW</span><span class="sxs-lookup"><span data-stu-id="2a7fb-272">RAW</span></span> | <span data-ttu-id="2a7fb-273">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2a7fb-273">Byte[]</span></span>
<span data-ttu-id="2a7fb-274">RAWSTRING</span><span class="sxs-lookup"><span data-stu-id="2a7fb-274">RAWSTRING</span></span> | <span data-ttu-id="2a7fb-275">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2a7fb-275">Byte[]</span></span>
<span data-ttu-id="2a7fb-276">STRING</span><span class="sxs-lookup"><span data-stu-id="2a7fb-276">STRING</span></span> | <span data-ttu-id="2a7fb-277">String</span><span class="sxs-lookup"><span data-stu-id="2a7fb-277">String</span></span>
<span data-ttu-id="2a7fb-278">UNITÉ</span><span class="sxs-lookup"><span data-stu-id="2a7fb-278">UNIT</span></span> | <span data-ttu-id="2a7fb-279">String</span><span class="sxs-lookup"><span data-stu-id="2a7fb-279">String</span></span>
<span data-ttu-id="2a7fb-280">DATS</span><span class="sxs-lookup"><span data-stu-id="2a7fb-280">DATS</span></span> | <span data-ttu-id="2a7fb-281">String</span><span class="sxs-lookup"><span data-stu-id="2a7fb-281">String</span></span>
<span data-ttu-id="2a7fb-282">NUMC</span><span class="sxs-lookup"><span data-stu-id="2a7fb-282">NUMC</span></span> | <span data-ttu-id="2a7fb-283">String</span><span class="sxs-lookup"><span data-stu-id="2a7fb-283">String</span></span>
<span data-ttu-id="2a7fb-284">TIMS</span><span class="sxs-lookup"><span data-stu-id="2a7fb-284">TIMS</span></span> | <span data-ttu-id="2a7fb-285">String</span><span class="sxs-lookup"><span data-stu-id="2a7fb-285">String</span></span>

> [!NOTE]
> <span data-ttu-id="2a7fb-286">colonnes de toomap de toocolumns du jeu de données source à partir du jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="2a7fb-286">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="map-source-toosink-columns"></a><span data-ttu-id="2a7fb-287">Mapper les colonnes de source toosink</span><span class="sxs-lookup"><span data-stu-id="2a7fb-287">Map source toosink columns</span></span>
<span data-ttu-id="2a7fb-288">toolearn sur le mappage des colonnes dans toocolumns du jeu de données source dans le jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="2a7fb-288">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="2a7fb-289">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="2a7fb-289">Repeatable read from relational sources</span></span>
<span data-ttu-id="2a7fb-290">Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-290">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="2a7fb-291">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-291">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="2a7fb-292">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-292">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="2a7fb-293">Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-293">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="2a7fb-294">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="2a7fb-294">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="2a7fb-295">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="2a7fb-295">Performance and Tuning</span></span>
<span data-ttu-id="2a7fb-296">Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="2a7fb-296">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
