---
title: "aaaMove des données à partir de SAP HANA à l’aide d’Azure Data Factory | Documents Microsoft"
description: "En savoir plus sur la façon de toomove les données à partir de SAP HANA à l’aide d’Azure Data Factory."
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
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 5cefe4c8ed01ea4e86e02496b2f8a9083d0b949c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a><span data-ttu-id="d1040-103">Déplacer des données depuis SAP HANA à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d1040-103">Move data From SAP HANA using Azure Data Factory</span></span>
<span data-ttu-id="d1040-104">Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory à partir d’un ordinateur local SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="d1040-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises SAP HANA.</span></span> <span data-ttu-id="d1040-105">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="d1040-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="d1040-106">Vous pouvez copier les données d’une banque de données locale SAP HANA données magasin tooany pris en charge récepteur.</span><span class="sxs-lookup"><span data-stu-id="d1040-106">You can copy data from an on-premises SAP HANA data store tooany supported sink data store.</span></span> <span data-ttu-id="d1040-107">Pour une liste de données pris en charge des magasins récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="d1040-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="d1040-108">Fabrique de données prend actuellement en charge uniquement le déplacement de banques de données à partir d’un tooother de données SAP HANA, mais pas pour déplacer des données d’autres données de magasins tooan SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="d1040-108">Data factory currently supports only moving data from an SAP HANA tooother data stores, but not for moving data from other data stores tooan SAP HANA.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="d1040-109">Versions prises en charge et installation</span><span class="sxs-lookup"><span data-stu-id="d1040-109">Supported versions and installation</span></span>
<span data-ttu-id="d1040-110">Ce connecteur prend en charge n’importe quelle version de base de données SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="d1040-110">This connector supports any version of SAP HANA database.</span></span> <span data-ttu-id="d1040-111">Il prend en charge la copie de données à partir de modèles d’informations HANA (comme les vues Analyse et Calcul) et les tables Ligne/Colonne à l’aide de requêtes SQL.</span><span class="sxs-lookup"><span data-stu-id="d1040-111">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span></span>

<span data-ttu-id="d1040-112">tooenable hello connectivité toohello instance de SAP HANA, installez hello suivant des composants :</span><span class="sxs-lookup"><span data-stu-id="d1040-112">tooenable hello connectivity toohello SAP HANA instance, install hello following components:</span></span>
- <span data-ttu-id="d1040-113">**Passerelle de gestion des données**: service Data Factory prend en charge la connexion de données locales tooon magasins (y compris SAP HANA) à l’aide d’un composant appelé passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="d1040-113">**Data Management Gateway**: Data Factory service supports connecting tooon-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span></span> <span data-ttu-id="d1040-114">toolearn sur la passerelle de gestion des données et des instructions détaillées pour configurer la passerelle de hello, consultez [magasin de données toocloud du magasin de données de déplacement entre des données locales](data-factory-move-data-between-onprem-and-cloud.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="d1040-114">toolearn about Data Management Gateway and step-by-step instructions for setting up hello gateway, see [Moving data between on-premises data store toocloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="d1040-115">Passerelle est requise même si hello SAP HANA est hébergé dans une machine virtuelle de Azure IaaS (VM).</span><span class="sxs-lookup"><span data-stu-id="d1040-115">Gateway is required even if hello SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="d1040-116">Vous pouvez installer la passerelle de hello sur hello même machine virtuelle en tant que données de hello stocker ou sur un ordinateur différent virtuel tant que passerelle de hello peuvent se connecter toohello de base de données.</span><span class="sxs-lookup"><span data-stu-id="d1040-116">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>
- <span data-ttu-id="d1040-117">**Pilote ODBC de HANA SAP** sur l’ordinateur de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="d1040-117">**SAP HANA ODBC driver** on hello gateway machine.</span></span> <span data-ttu-id="d1040-118">Vous pouvez télécharger le pilote ODBC de HANA SAP de hello de hello [centre de téléchargement de logiciel SAP](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="d1040-118">You can download hello SAP HANA ODBC driver from hello [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="d1040-119">Recherche par mot clé de hello **SAP HANA CLIENT pour Windows**.</span><span class="sxs-lookup"><span data-stu-id="d1040-119">Search with hello keyword **SAP HANA CLIENT for Windows**.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="d1040-120">Prise en main</span><span class="sxs-lookup"><span data-stu-id="d1040-120">Getting started</span></span>
<span data-ttu-id="d1040-121">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données Cassandra local à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="d1040-121">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="d1040-122">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="d1040-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="d1040-123">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="d1040-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="d1040-124">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="d1040-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d1040-125">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="d1040-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="d1040-126">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="d1040-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="d1040-127">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="d1040-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="d1040-128">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="d1040-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="d1040-129">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="d1040-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="d1040-130">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="d1040-130">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="d1040-131">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="d1040-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="d1040-132">Pour voir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données à partir d’un ordinateur local SAP HANA, [exemple de JSON : copier des données à partir de SAP HANA tooAzure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="d1040-132">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA tooAzure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="d1040-133">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont le magasin de données SAP HANA utilisé toodefine Data Factory entités tooan spécifique :</span><span class="sxs-lookup"><span data-stu-id="d1040-133">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooan SAP HANA data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d1040-134">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="d1040-134">Linked service properties</span></span>
<span data-ttu-id="d1040-135">Hello tableau suivant fournit la description pour JSON éléments tooSAP spécifique HANA de service lié.</span><span class="sxs-lookup"><span data-stu-id="d1040-135">hello following table provides description for JSON elements specific tooSAP HANA linked service.</span></span>

<span data-ttu-id="d1040-136">Propriété</span><span class="sxs-lookup"><span data-stu-id="d1040-136">Property</span></span> | <span data-ttu-id="d1040-137">Description</span><span class="sxs-lookup"><span data-stu-id="d1040-137">Description</span></span> | <span data-ttu-id="d1040-138">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="d1040-138">Allowed values</span></span> | <span data-ttu-id="d1040-139">Requis</span><span class="sxs-lookup"><span data-stu-id="d1040-139">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="d1040-140">server</span><span class="sxs-lookup"><span data-stu-id="d1040-140">server</span></span> | <span data-ttu-id="d1040-141">Nom du serveur hello sur quel hello SAP HANA instance réside.</span><span class="sxs-lookup"><span data-stu-id="d1040-141">Name of hello server on which hello SAP HANA instance resides.</span></span> <span data-ttu-id="d1040-142">Si votre serveur utilise un port personnalisé, spécifiez `server:port`.</span><span class="sxs-lookup"><span data-stu-id="d1040-142">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="d1040-143">string</span><span class="sxs-lookup"><span data-stu-id="d1040-143">string</span></span> | <span data-ttu-id="d1040-144">Oui</span><span class="sxs-lookup"><span data-stu-id="d1040-144">Yes</span></span>
<span data-ttu-id="d1040-145">authenticationType</span><span class="sxs-lookup"><span data-stu-id="d1040-145">authenticationType</span></span> | <span data-ttu-id="d1040-146">Type d'authentification.</span><span class="sxs-lookup"><span data-stu-id="d1040-146">Type of authentication.</span></span> | <span data-ttu-id="d1040-147">chaîne.</span><span class="sxs-lookup"><span data-stu-id="d1040-147">string.</span></span> <span data-ttu-id="d1040-148">« Basic » ou « Windows »</span><span class="sxs-lookup"><span data-stu-id="d1040-148">"Basic" or "Windows"</span></span> | <span data-ttu-id="d1040-149">Oui</span><span class="sxs-lookup"><span data-stu-id="d1040-149">Yes</span></span> 
<span data-ttu-id="d1040-150">username</span><span class="sxs-lookup"><span data-stu-id="d1040-150">username</span></span> | <span data-ttu-id="d1040-151">Nom d’utilisateur de hello qui a le serveur d’accès toohello SAP</span><span class="sxs-lookup"><span data-stu-id="d1040-151">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="d1040-152">string</span><span class="sxs-lookup"><span data-stu-id="d1040-152">string</span></span> | <span data-ttu-id="d1040-153">Oui</span><span class="sxs-lookup"><span data-stu-id="d1040-153">Yes</span></span>
<span data-ttu-id="d1040-154">password</span><span class="sxs-lookup"><span data-stu-id="d1040-154">password</span></span> | <span data-ttu-id="d1040-155">Mot de passe utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="d1040-155">Password for hello user.</span></span> | <span data-ttu-id="d1040-156">string</span><span class="sxs-lookup"><span data-stu-id="d1040-156">string</span></span> | <span data-ttu-id="d1040-157">Oui</span><span class="sxs-lookup"><span data-stu-id="d1040-157">Yes</span></span>
<span data-ttu-id="d1040-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d1040-158">gatewayName</span></span> | <span data-ttu-id="d1040-159">Nom de passerelle hello hello service Data Factory doit utiliser l’instance de SAP HANA tooconnect toohello sur site.</span><span class="sxs-lookup"><span data-stu-id="d1040-159">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP HANA instance.</span></span> | <span data-ttu-id="d1040-160">string</span><span class="sxs-lookup"><span data-stu-id="d1040-160">string</span></span> | <span data-ttu-id="d1040-161">Oui</span><span class="sxs-lookup"><span data-stu-id="d1040-161">Yes</span></span>
<span data-ttu-id="d1040-162">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="d1040-162">encryptedCredential</span></span> | <span data-ttu-id="d1040-163">chaîne d’identification de Hello chiffré.</span><span class="sxs-lookup"><span data-stu-id="d1040-163">hello encrypted credential string.</span></span> | <span data-ttu-id="d1040-164">string</span><span class="sxs-lookup"><span data-stu-id="d1040-164">string</span></span> | <span data-ttu-id="d1040-165">Non</span><span class="sxs-lookup"><span data-stu-id="d1040-165">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="d1040-166">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="d1040-166">Dataset properties</span></span>
<span data-ttu-id="d1040-167">Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="d1040-167">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="d1040-168">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="d1040-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="d1040-169">Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="d1040-169">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="d1040-170">Aucune propriété spécifique au type pris en charge pour le dataset de SAP HANA hello de type **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="d1040-170">There are no type-specific properties supported for hello SAP HANA dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="d1040-171">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="d1040-171">Copy activity properties</span></span>
<span data-ttu-id="d1040-172">Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="d1040-172">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="d1040-173">Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="d1040-173">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="d1040-174">Tandis que les propriétés disponibles dans hello **typeProperties** section d’activité hello varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="d1040-174">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="d1040-175">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="d1040-175">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="d1040-176">Lorsque la source de l’activité de copie est de type **RelationalSource** (qui inclut SAP HANA), hello propriétés suivantes est disponible dans la section de typeProperties :</span><span class="sxs-lookup"><span data-stu-id="d1040-176">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="d1040-177">Propriété</span><span class="sxs-lookup"><span data-stu-id="d1040-177">Property</span></span> | <span data-ttu-id="d1040-178">Description</span><span class="sxs-lookup"><span data-stu-id="d1040-178">Description</span></span> | <span data-ttu-id="d1040-179">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="d1040-179">Allowed values</span></span> | <span data-ttu-id="d1040-180">Requis</span><span class="sxs-lookup"><span data-stu-id="d1040-180">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d1040-181">query</span><span class="sxs-lookup"><span data-stu-id="d1040-181">query</span></span> | <span data-ttu-id="d1040-182">Spécifie les hello requête tooread de données SQL à partir de l’instance de SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="d1040-182">Specifies hello SQL query tooread data from hello SAP HANA instance.</span></span> | <span data-ttu-id="d1040-183">Requête SQL.</span><span class="sxs-lookup"><span data-stu-id="d1040-183">SQL query.</span></span> | <span data-ttu-id="d1040-184">Oui</span><span class="sxs-lookup"><span data-stu-id="d1040-184">Yes</span></span> |

## <a name="json-example-copy-data-from-sap-hana-tooazure-blob"></a><span data-ttu-id="d1040-185">Exemple de JSON : copier des données à partir de SAP HANA tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="d1040-185">JSON example: Copy data from SAP HANA tooAzure Blob</span></span>
<span data-ttu-id="d1040-186">Hello exemple suivant fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d1040-186">hello following sample provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="d1040-187">Cet exemple montre comment toocopy des données à partir d’un tooan de SAP HANA local stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d1040-187">This sample shows how toocopy data from an on-premises SAP HANA tooan Azure Blob Storage.</span></span> <span data-ttu-id="d1040-188">Toutefois, les données peuvent être copiées **directement** tooany de récepteurs hello répertoriés [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d1040-188">However, data can be copied **directly** tooany of hello sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="d1040-189">Cet exemple fournit des extraits de code JSON.</span><span class="sxs-lookup"><span data-stu-id="d1040-189">This sample provides JSON snippets.</span></span> <span data-ttu-id="d1040-190">Il n’inclut pas d’instructions détaillées pour créer la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="d1040-190">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="d1040-191">Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="d1040-191">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="d1040-192">exemple Hello a hello suivant des entités de fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="d1040-192">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="d1040-193">Un service lié de type [SapHana](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d1040-193">A linked service of type [SapHana](#linked-service-properties).</span></span>
2. <span data-ttu-id="d1040-194">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d1040-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="d1040-195">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d1040-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="d1040-196">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d1040-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="d1040-197">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [RelationalSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d1040-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="d1040-198">exemple Hello copie toutes les heures des données à partir d’un tooan d’instance SAP HANA blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d1040-198">hello sample copies data from an SAP HANA instance tooan Azure blob hourly.</span></span> <span data-ttu-id="d1040-199">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="d1040-199">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="d1040-200">Dans un premier temps, le programme d’installation passerelle de gestion des données hello.</span><span class="sxs-lookup"><span data-stu-id="d1040-200">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="d1040-201">instructions de Hello sont Bonjour [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="d1040-201">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-hana-linked-service"></a><span data-ttu-id="d1040-202">Service lié SAP HANA</span><span class="sxs-lookup"><span data-stu-id="d1040-202">SAP HANA linked service</span></span>
<span data-ttu-id="d1040-203">Cela liées à des liens de service votre fabrique de données SAP HANA instance toohello.</span><span class="sxs-lookup"><span data-stu-id="d1040-203">This linked service links your SAP HANA instance toohello data factory.</span></span> <span data-ttu-id="d1040-204">propriété de type Hello est définie trop**SapHana**.</span><span class="sxs-lookup"><span data-stu-id="d1040-204">hello type property is set too**SapHana**.</span></span> <span data-ttu-id="d1040-205">section de typeProperties Hello fournit des informations de connexion pour l’instance de SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="d1040-205">hello typeProperties section provides connection information for hello SAP HANA instance.</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties":
    {
        "type": "SapHana",
        "typeProperties":
        {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="d1040-206">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d1040-206">Azure Storage linked service</span></span>
<span data-ttu-id="d1040-207">Cela lié à des liens de service votre fabrique de données toohello compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d1040-207">This linked service links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="d1040-208">propriété de type Hello est définie trop**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="d1040-208">hello type property is set too**AzureStorage**.</span></span> <span data-ttu-id="d1040-209">section de typeProperties Hello fournit des informations de connexion pour hello compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d1040-209">hello typeProperties section provides connection information for hello Azure Storage account.</span></span>

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

### <a name="sap-hana-input-dataset"></a><span data-ttu-id="d1040-210">Jeu de données d’entrée SAP HANA</span><span class="sxs-lookup"><span data-stu-id="d1040-210">SAP HANA input dataset</span></span>

<span data-ttu-id="d1040-211">Ce jeu de données définit un jeu de données SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="d1040-211">This dataset defines hello SAP HANA dataset.</span></span> <span data-ttu-id="d1040-212">Vous définissez type hello du jeu de données de Data Factory hello trop**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="d1040-212">You set hello type of hello Data Factory dataset too**RelationalTable**.</span></span> <span data-ttu-id="d1040-213">Actuellement, vous ne spécifiez pas de propriétés propres à un type pour un jeu de données SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="d1040-213">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span></span> <span data-ttu-id="d1040-214">requête Hello dans la définition de l’activité de copie de hello spécifie quel tooread de données à partir de l’instance de SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="d1040-214">hello query in hello Copy Activity definition specifies what data tooread from hello SAP HANA instance.</span></span> 

<span data-ttu-id="d1040-215">Définition de propriété externe tootrue informe service Data Factory de hello cette table hello est la fabrique de données externe toohello n’est pas générée par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="d1040-215">Setting external property tootrue informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="d1040-216">Propriétés de la fréquence et l’intervalle définit la planification de hello.</span><span class="sxs-lookup"><span data-stu-id="d1040-216">Frequency and interval properties defines hello schedule.</span></span> <span data-ttu-id="d1040-217">Dans ce cas, les données de salutation sont en lecture à partir de l’instance de SAP HANA hello toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="d1040-217">In this case, hello data is read from hello SAP HANA instance hourly.</span></span> 

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="d1040-218">Jeu de données de sortie d’objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="d1040-218">Azure Blob output dataset</span></span>
<span data-ttu-id="d1040-219">Ce jeu de données définit un jeu de données objet Blob Azure hello sortie.</span><span class="sxs-lookup"><span data-stu-id="d1040-219">This dataset defines hello output Azure Blob dataset.</span></span> <span data-ttu-id="d1040-220">propriété de type Hello est définie à tooAzureBlob.</span><span class="sxs-lookup"><span data-stu-id="d1040-220">hello type property is set tooAzureBlob.</span></span> <span data-ttu-id="d1040-221">section de typeProperties Hello fournit où sont stockées les données hello copiées à partir de l’instance de SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="d1040-221">hello typeProperties section provides where hello data copied from hello SAP HANA instance is stored.</span></span> <span data-ttu-id="d1040-222">les données de salutation sont écrit tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="d1040-222">hello data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d1040-223">chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="d1040-223">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="d1040-224">chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="d1040-224">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/saphana/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="d1040-225">Pipeline avec activité de copie</span><span class="sxs-lookup"><span data-stu-id="d1040-225">Pipeline with Copy activity</span></span>

<span data-ttu-id="d1040-226">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="d1040-226">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="d1040-227">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**RelationalSource** (pour une source de SAP HANA) et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d1040-227">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** (for SAP HANA source) and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="d1040-228">la requête SQL Hello spécifiée pour hello **requête** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.</span><span class="sxs-lookup"><span data-stu-id="d1040-228">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<SQL Query for HANA>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapHanaDataset"
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
                "name": "SapHanaToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```


### <a name="type-mapping-for-sap-hana"></a><span data-ttu-id="d1040-229">Mappage de type pour SAP HANA</span><span class="sxs-lookup"><span data-stu-id="d1040-229">Type mapping for SAP HANA</span></span>
<span data-ttu-id="d1040-230">Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, l’activité de copie effectue les conversions de type automatique à partir de types de sources de toosink types avec hello suivant l’approche en deux étapes :</span><span class="sxs-lookup"><span data-stu-id="d1040-230">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="d1040-231">Convertir à partir de la source native types too.NET type</span><span class="sxs-lookup"><span data-stu-id="d1040-231">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="d1040-232">Conversion de type de récepteur de toonative de type .NET</span><span class="sxs-lookup"><span data-stu-id="d1040-232">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="d1040-233">Lors du déplacement des données à partir de SAP HANA, hello suivant les mappages est utilisé à partir de types de too.NET de types de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="d1040-233">When moving data from SAP HANA, hello following mappings are used from SAP HANA types too.NET types.</span></span>

<span data-ttu-id="d1040-234">Type SAP HANA</span><span class="sxs-lookup"><span data-stu-id="d1040-234">SAP HANA Type</span></span> | <span data-ttu-id="d1040-235">Type basé sur .NET</span><span class="sxs-lookup"><span data-stu-id="d1040-235">.NET Based Type</span></span>
------------- | ---------------
<span data-ttu-id="d1040-236">TINYINT</span><span class="sxs-lookup"><span data-stu-id="d1040-236">TINYINT</span></span> | <span data-ttu-id="d1040-237">Byte</span><span class="sxs-lookup"><span data-stu-id="d1040-237">Byte</span></span>
<span data-ttu-id="d1040-238">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="d1040-238">SMALLINT</span></span> | <span data-ttu-id="d1040-239">Int16</span><span class="sxs-lookup"><span data-stu-id="d1040-239">Int16</span></span>
<span data-ttu-id="d1040-240">INT</span><span class="sxs-lookup"><span data-stu-id="d1040-240">INT</span></span> | <span data-ttu-id="d1040-241">Int32</span><span class="sxs-lookup"><span data-stu-id="d1040-241">Int32</span></span>
<span data-ttu-id="d1040-242">BIGINT</span><span class="sxs-lookup"><span data-stu-id="d1040-242">BIGINT</span></span> | <span data-ttu-id="d1040-243">Int64</span><span class="sxs-lookup"><span data-stu-id="d1040-243">Int64</span></span>
<span data-ttu-id="d1040-244">REAL</span><span class="sxs-lookup"><span data-stu-id="d1040-244">REAL</span></span> | <span data-ttu-id="d1040-245">Single</span><span class="sxs-lookup"><span data-stu-id="d1040-245">Single</span></span>
<span data-ttu-id="d1040-246">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="d1040-246">DOUBLE</span></span> | <span data-ttu-id="d1040-247">Single</span><span class="sxs-lookup"><span data-stu-id="d1040-247">Single</span></span>
<span data-ttu-id="d1040-248">DÉCIMAL</span><span class="sxs-lookup"><span data-stu-id="d1040-248">DECIMAL</span></span> | <span data-ttu-id="d1040-249">Décimal</span><span class="sxs-lookup"><span data-stu-id="d1040-249">Decimal</span></span>
<span data-ttu-id="d1040-250">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="d1040-250">BOOLEAN</span></span> | <span data-ttu-id="d1040-251">Byte</span><span class="sxs-lookup"><span data-stu-id="d1040-251">Byte</span></span>
<span data-ttu-id="d1040-252">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="d1040-252">VARCHAR</span></span> | <span data-ttu-id="d1040-253">String</span><span class="sxs-lookup"><span data-stu-id="d1040-253">String</span></span>
<span data-ttu-id="d1040-254">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="d1040-254">NVARCHAR</span></span> | <span data-ttu-id="d1040-255">String</span><span class="sxs-lookup"><span data-stu-id="d1040-255">String</span></span>
<span data-ttu-id="d1040-256">CLOB</span><span class="sxs-lookup"><span data-stu-id="d1040-256">CLOB</span></span> | <span data-ttu-id="d1040-257">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d1040-257">Byte[]</span></span>
<span data-ttu-id="d1040-258">ALPHANUM</span><span class="sxs-lookup"><span data-stu-id="d1040-258">ALPHANUM</span></span> | <span data-ttu-id="d1040-259">String</span><span class="sxs-lookup"><span data-stu-id="d1040-259">String</span></span>
<span data-ttu-id="d1040-260">BLOB</span><span class="sxs-lookup"><span data-stu-id="d1040-260">BLOB</span></span> | <span data-ttu-id="d1040-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d1040-261">Byte[]</span></span>
<span data-ttu-id="d1040-262">DATE</span><span class="sxs-lookup"><span data-stu-id="d1040-262">DATE</span></span> | <span data-ttu-id="d1040-263">DateTime</span><span class="sxs-lookup"><span data-stu-id="d1040-263">DateTime</span></span>
<span data-ttu-id="d1040-264">TEMPS</span><span class="sxs-lookup"><span data-stu-id="d1040-264">TIME</span></span> | <span data-ttu-id="d1040-265">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="d1040-265">TimeSpan</span></span>
<span data-ttu-id="d1040-266">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="d1040-266">TIMESTAMP</span></span> | <span data-ttu-id="d1040-267">DateTime</span><span class="sxs-lookup"><span data-stu-id="d1040-267">DateTime</span></span>
<span data-ttu-id="d1040-268">SECONDDATE</span><span class="sxs-lookup"><span data-stu-id="d1040-268">SECONDDATE</span></span> | <span data-ttu-id="d1040-269">DateTime</span><span class="sxs-lookup"><span data-stu-id="d1040-269">DateTime</span></span>

## <a name="known-limitations"></a><span data-ttu-id="d1040-270">Limites connues</span><span class="sxs-lookup"><span data-stu-id="d1040-270">Known limitations</span></span>
<span data-ttu-id="d1040-271">Il existe quelques limitations connues lors de la copie des données à partir de SAP HANA :</span><span class="sxs-lookup"><span data-stu-id="d1040-271">There are a few known limitations when copying data from SAP HANA:</span></span>

- <span data-ttu-id="d1040-272">Les chaînes NVARCHAR sont tronquées toomaximum la longueur de 4 000 caractères Unicode</span><span class="sxs-lookup"><span data-stu-id="d1040-272">NVARCHAR strings are truncated toomaximum length of 4000 Unicode characters</span></span>
- <span data-ttu-id="d1040-273">SMALLDECIMAL n’est pas pris en charge</span><span class="sxs-lookup"><span data-stu-id="d1040-273">SMALLDECIMAL is not supported</span></span>
- <span data-ttu-id="d1040-274">VARBINARY n’est pas pris en charge</span><span class="sxs-lookup"><span data-stu-id="d1040-274">VARBINARY is not supported</span></span>
- <span data-ttu-id="d1040-275">Les dates valides sont celles comprises entre 1899/12/30 et 9999/12/31</span><span class="sxs-lookup"><span data-stu-id="d1040-275">Valid Dates are between 1899/12/30 and 9999/12/31</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="d1040-276">Mapper les colonnes de source toosink</span><span class="sxs-lookup"><span data-stu-id="d1040-276">Map source toosink columns</span></span>
<span data-ttu-id="d1040-277">toolearn sur le mappage des colonnes dans toocolumns du jeu de données source dans le jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="d1040-277">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="d1040-278">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="d1040-278">Repeatable read from relational sources</span></span>
<span data-ttu-id="d1040-279">Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="d1040-279">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="d1040-280">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="d1040-280">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="d1040-281">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="d1040-281">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="d1040-282">Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée.</span><span class="sxs-lookup"><span data-stu-id="d1040-282">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="d1040-283">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="d1040-283">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="d1040-284">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="d1040-284">Performance and Tuning</span></span>
<span data-ttu-id="d1040-285">Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="d1040-285">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
