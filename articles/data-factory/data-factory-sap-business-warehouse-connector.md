---
title: "Déplacer des données depuis SAP Business Warehouse à l’aide d’Azure Data Factory | Microsoft Docs"
description: "Découvrez comment déplacer des données depuis SAP Business Warehouse à l’aide d’Azure Data Factory."
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
ms.openlocfilehash: 220ccc8b94797880d335385046001c5f3b17c862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a><span data-ttu-id="7e871-103">Déplacer des données depuis SAP Business Warehouse à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7e871-103">Move data From SAP Business Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="7e871-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour déplacer des données à partir d’un système SAP Business Warehouse local.</span><span class="sxs-lookup"><span data-stu-id="7e871-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP Business Warehouse (BW).</span></span> <span data-ttu-id="7e871-105">Il s’appuie sur l’article [Activités de déplacement des données](data-factory-data-movement-activities.md), qui présente une vue d’ensemble du déplacement de données avec l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="7e871-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="7e871-106">Vous pouvez copier et coller les données d’un magasin de données SAP Business Warehouse local dans tout magasin de données récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7e871-106">You can copy data from an on-premises SAP Business Warehouse data store to any supported sink data store.</span></span> <span data-ttu-id="7e871-107">Consultez la table [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) pour obtenir la liste des magasins de données pris en charge en tant que récepteurs par l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="7e871-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="7e871-108">Actuellement, Data Factory prend uniquement en charge le déplacement de données de SAP Business Warehouse vers d’autres magasins de données, mais non l’inverse.</span><span class="sxs-lookup"><span data-stu-id="7e871-108">Data factory currently supports only moving data from an SAP Business Warehouse to other data stores, but not for moving data from other data stores to an SAP Business Warehouse.</span></span> 

## <a name="supported-versions-and-installation"></a><span data-ttu-id="7e871-109">Versions prises en charge et installation</span><span class="sxs-lookup"><span data-stu-id="7e871-109">Supported versions and installation</span></span>
<span data-ttu-id="7e871-110">Ce connecteur prend en charge la version 7.x de SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7e871-110">This connector supports SAP Business Warehouse version 7.x.</span></span> <span data-ttu-id="7e871-111">Il prend en charge la copie de données d’InfoCubes et de QueryCubes (y compris les requêtes BEx) à l’aide de requêtes MDX.</span><span class="sxs-lookup"><span data-stu-id="7e871-111">It supports copying data from InfoCubes and QueryCubes (including BEx queries) using MDX queries.</span></span>

<span data-ttu-id="7e871-112">Pour activer la connectivité à l’instance SAP BW, installez les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="7e871-112">To enable the connectivity to the SAP BW instance, install the following components:</span></span>
- <span data-ttu-id="7e871-113">**Passerelle de gestion des données** : le service Data Factory prend en charge la connexion aux magasins de données locaux (y compris SAP Business Warehouse) à l’aide d’un composant appelé passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="7e871-113">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP Business Warehouse) using a component called Data Management Gateway.</span></span> <span data-ttu-id="7e871-114">Consultez l’article [Déplacement de données d’un magasin de données local vers un magasin de données cloud](data-factory-move-data-between-onprem-and-cloud.md) pour en savoir plus sur la passerelle de gestion des données et obtenir des instructions détaillées sur la configuration de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="7e871-114">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="7e871-115">Une passerelle est requise même si SAP Business Warehouse est hébergé sur une machine virtuelle Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="7e871-115">Gateway is required even if the SAP Business Warehouse is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="7e871-116">Vous pouvez installer la passerelle sur la même machine virtuelle que le magasin de données, ou sur une autre machine virtuelle pourvu que la passerelle puisse se connecter à la base de données.</span><span class="sxs-lookup"><span data-stu-id="7e871-116">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>
- <span data-ttu-id="7e871-117">**Bibliothèque SAP NetWeaver** sur la machine passerelle.</span><span class="sxs-lookup"><span data-stu-id="7e871-117">**SAP NetWeaver library** on the gateway machine.</span></span> <span data-ttu-id="7e871-118">Vous pouvez obtenir la bibliothèque SAP Netweaver auprès de votre administrateur SAP, ou directement depuis le [Centre de téléchargement de logiciel SAP](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="7e871-118">You can get the SAP Netweaver library from your SAP administrator, or directly from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="7e871-119">Recherchez la **Note SAP 1025361** pour obtenir l’emplacement de téléchargement de la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="7e871-119">Search for the **SAP Note #1025361** to get the download location for the most recent version.</span></span> <span data-ttu-id="7e871-120">Assurez-vous que l’architecture de la bibliothèque de SAP NetWeaver (32 bits ou 64 bits) correspond à votre installation de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="7e871-120">Make sure that the architecture for the SAP NetWeaver library (32-bit or 64-bit) matches your gateway installation.</span></span> <span data-ttu-id="7e871-121">Ensuite, installez tous les fichiers inclus dans le Kit de développement logiciel (SDK) RFC de SAP NetWeaver en fonction de la note SAP.</span><span class="sxs-lookup"><span data-stu-id="7e871-121">Then install all files included in the SAP NetWeaver RFC SDK according to the SAP Note.</span></span> <span data-ttu-id="7e871-122">La bibliothèque de SAP NetWeaver est également incluse dans l’installation des outils clients SAP.</span><span class="sxs-lookup"><span data-stu-id="7e871-122">The SAP NetWeaver library is also included in the SAP Client Tools installation.</span></span>

> [!TIP]
> <span data-ttu-id="7e871-123">Placer les DLL extraites du Kit de développement logiciel NetWeaver RFC dans le dossier system32.</span><span class="sxs-lookup"><span data-stu-id="7e871-123">Put the dlls extracted from the NetWeaver RFC SDK into system32 folder.</span></span>

## <a name="getting-started"></a><span data-ttu-id="7e871-124">Prise en main</span><span class="sxs-lookup"><span data-stu-id="7e871-124">Getting started</span></span>
<span data-ttu-id="7e871-125">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données Cassandra local à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="7e871-125">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="7e871-126">Le moyen le plus simple de créer un pipeline consiste à utiliser **l’Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="7e871-126">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="7e871-127">Consultez la page [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant Copier des données.</span><span class="sxs-lookup"><span data-stu-id="7e871-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="7e871-128">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="7e871-128">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="7e871-129">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="7e871-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="7e871-130">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="7e871-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="7e871-131">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="7e871-131">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="7e871-132">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="7e871-132">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="7e871-133">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="7e871-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="7e871-134">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="7e871-134">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="7e871-135">Lorsque vous utilisez des outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory au format JSON.</span><span class="sxs-lookup"><span data-stu-id="7e871-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="7e871-136">Pour consulter un exemple contenant des définitions JSON pour les entités Data Factory utilisées pour copier des données d’un magasin de données SAP Business Warehouse, consultez la section [Exemple JSON : copier des données depuis SAP Business Warehouse vers Azure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) de cet article.</span><span class="sxs-lookup"><span data-stu-id="7e871-136">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP Business Warehouse, see [JSON example: Copy data from SAP Business Warehouse to Azure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="7e871-137">Les sections suivantes contiennent des informations détaillées sur les propriétés JSON utilisées pour définir les entités Data Factory propres à un magasin de données SAP Business Warehouse :</span><span class="sxs-lookup"><span data-stu-id="7e871-137">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP BW data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="7e871-138">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="7e871-138">Linked service properties</span></span>
<span data-ttu-id="7e871-139">Le tableau suivant fournit la description des éléments JSON spécifiques au service lié SAP Business Warehouse (BW).</span><span class="sxs-lookup"><span data-stu-id="7e871-139">The following table provides description for JSON elements specific to SAP Business Warehouse (BW) linked service.</span></span>

<span data-ttu-id="7e871-140">Propriété</span><span class="sxs-lookup"><span data-stu-id="7e871-140">Property</span></span> | <span data-ttu-id="7e871-141">Description</span><span class="sxs-lookup"><span data-stu-id="7e871-141">Description</span></span> | <span data-ttu-id="7e871-142">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="7e871-142">Allowed values</span></span> | <span data-ttu-id="7e871-143">Requis</span><span class="sxs-lookup"><span data-stu-id="7e871-143">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="7e871-144">server</span><span class="sxs-lookup"><span data-stu-id="7e871-144">server</span></span> | <span data-ttu-id="7e871-145">Nom du serveur sur lequel réside l’instance SAP BW.</span><span class="sxs-lookup"><span data-stu-id="7e871-145">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="7e871-146">string</span><span class="sxs-lookup"><span data-stu-id="7e871-146">string</span></span> | <span data-ttu-id="7e871-147">Oui</span><span class="sxs-lookup"><span data-stu-id="7e871-147">Yes</span></span>
<span data-ttu-id="7e871-148">systemNumber</span><span class="sxs-lookup"><span data-stu-id="7e871-148">systemNumber</span></span> | <span data-ttu-id="7e871-149">Numéro de système du système SAP BW.</span><span class="sxs-lookup"><span data-stu-id="7e871-149">System number of the SAP BW system.</span></span> | <span data-ttu-id="7e871-150">Nombre décimal à deux chiffres représenté sous forme de chaîne.</span><span class="sxs-lookup"><span data-stu-id="7e871-150">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="7e871-151">Oui</span><span class="sxs-lookup"><span data-stu-id="7e871-151">Yes</span></span>
<span data-ttu-id="7e871-152">clientId</span><span class="sxs-lookup"><span data-stu-id="7e871-152">clientId</span></span> | <span data-ttu-id="7e871-153">ID client du client dans le système SAP W.</span><span class="sxs-lookup"><span data-stu-id="7e871-153">Client ID of the client in the SAP W system.</span></span> | <span data-ttu-id="7e871-154">Nombre décimal à trois chiffres représenté sous forme de chaîne.</span><span class="sxs-lookup"><span data-stu-id="7e871-154">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="7e871-155">Oui</span><span class="sxs-lookup"><span data-stu-id="7e871-155">Yes</span></span>
<span data-ttu-id="7e871-156">username</span><span class="sxs-lookup"><span data-stu-id="7e871-156">username</span></span> | <span data-ttu-id="7e871-157">Nom de l’utilisateur qui a accès au serveur SAP</span><span class="sxs-lookup"><span data-stu-id="7e871-157">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="7e871-158">string</span><span class="sxs-lookup"><span data-stu-id="7e871-158">string</span></span> | <span data-ttu-id="7e871-159">Oui</span><span class="sxs-lookup"><span data-stu-id="7e871-159">Yes</span></span>
<span data-ttu-id="7e871-160">password</span><span class="sxs-lookup"><span data-stu-id="7e871-160">password</span></span> | <span data-ttu-id="7e871-161">Mot de passe pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7e871-161">Password for the user.</span></span> | <span data-ttu-id="7e871-162">string</span><span class="sxs-lookup"><span data-stu-id="7e871-162">string</span></span> | <span data-ttu-id="7e871-163">Oui</span><span class="sxs-lookup"><span data-stu-id="7e871-163">Yes</span></span>
<span data-ttu-id="7e871-164">gatewayName</span><span class="sxs-lookup"><span data-stu-id="7e871-164">gatewayName</span></span> | <span data-ttu-id="7e871-165">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter à l’instance SAP BW locale.</span><span class="sxs-lookup"><span data-stu-id="7e871-165">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span></span> | <span data-ttu-id="7e871-166">string</span><span class="sxs-lookup"><span data-stu-id="7e871-166">string</span></span> | <span data-ttu-id="7e871-167">Oui</span><span class="sxs-lookup"><span data-stu-id="7e871-167">Yes</span></span>
<span data-ttu-id="7e871-168">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="7e871-168">encryptedCredential</span></span> | <span data-ttu-id="7e871-169">La chaîne d’informations d’identification chiffrée.</span><span class="sxs-lookup"><span data-stu-id="7e871-169">The encrypted credential string.</span></span> | <span data-ttu-id="7e871-170">string</span><span class="sxs-lookup"><span data-stu-id="7e871-170">string</span></span> | <span data-ttu-id="7e871-171">Non</span><span class="sxs-lookup"><span data-stu-id="7e871-171">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="7e871-172">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="7e871-172">Dataset properties</span></span>
<span data-ttu-id="7e871-173">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="7e871-173">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="7e871-174">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="7e871-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="7e871-175">La section **typeProperties** est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="7e871-175">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="7e871-176">Aucune propriété propre à un type n’est prise en charge pour le type de jeu de données SAP BW **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="7e871-176">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="7e871-177">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="7e871-177">Copy activity properties</span></span>
<span data-ttu-id="7e871-178">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="7e871-178">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="7e871-179">Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="7e871-179">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="7e871-180">En revanche, les propriétés disponibles dans la section **typeProperties** de l’activité varient pour chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="7e871-180">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="7e871-181">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="7e871-181">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="7e871-182">Lorsque la source de l’activité de copie est de type **RelationalSource** (qui inclut SAP BW), les propriétés suivantes sont disponibles dans la section typeProperties :</span><span class="sxs-lookup"><span data-stu-id="7e871-182">When source in copy activity is of type **RelationalSource** (which includes SAP BW), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="7e871-183">Propriété</span><span class="sxs-lookup"><span data-stu-id="7e871-183">Property</span></span> | <span data-ttu-id="7e871-184">Description</span><span class="sxs-lookup"><span data-stu-id="7e871-184">Description</span></span> | <span data-ttu-id="7e871-185">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="7e871-185">Allowed values</span></span> | <span data-ttu-id="7e871-186">Requis</span><span class="sxs-lookup"><span data-stu-id="7e871-186">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7e871-187">query</span><span class="sxs-lookup"><span data-stu-id="7e871-187">query</span></span> | <span data-ttu-id="7e871-188">Spécifie la requête MDX pour lire les données de l’instance SAP BW.</span><span class="sxs-lookup"><span data-stu-id="7e871-188">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="7e871-189">Requête MDX.</span><span class="sxs-lookup"><span data-stu-id="7e871-189">MDX query.</span></span> | <span data-ttu-id="7e871-190">Oui</span><span class="sxs-lookup"><span data-stu-id="7e871-190">Yes</span></span> |


## <a name="json-example-copy-data-from-sap-business-warehouse-to-azure-blob"></a><span data-ttu-id="7e871-191">Exemple JSON : copier des données depuis SAP Business Warehouse vers Azure Blob</span><span class="sxs-lookup"><span data-stu-id="7e871-191">JSON example: Copy data from SAP Business Warehouse to Azure Blob</span></span>
<span data-ttu-id="7e871-192">L’exemple suivant présente des exemples de définitions de JSON que vous pouvez utiliser pour créer un pipeline à l’aide du [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), de [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [d’Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7e871-192">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="7e871-193">Cet exemple indique comment copier des données depuis un SAP Business Warehouse local vers un Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7e871-193">This sample shows how to copy data from an on-premises SAP Business Warehouse to an Azure Blob Storage.</span></span> <span data-ttu-id="7e871-194">Toutefois, les données peuvent être copiées **directement** vers l’un des récepteurs indiqués [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) , via l’activité de copie d’Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7e871-194">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="7e871-195">Cet exemple fournit des extraits de code JSON.</span><span class="sxs-lookup"><span data-stu-id="7e871-195">This sample provides JSON snippets.</span></span> <span data-ttu-id="7e871-196">Il n’inclut pas d’instructions détaillées pour la création de la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="7e871-196">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="7e871-197">Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="7e871-197">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="7e871-198">L’exemple contient les entités de fabrique de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="7e871-198">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="7e871-199">Un service lié de type [SapBw](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7e871-199">A linked service of type [SapBw](#linked-service-properties).</span></span>
2. <span data-ttu-id="7e871-200">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7e871-200">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="7e871-201">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7e871-201">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="7e871-202">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7e871-202">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="7e871-203">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [RelationalSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="7e871-203">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="7e871-204">L’exemple copie les données d’une instance SAP Business Warehouse vers un objet blob Azure toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="7e871-204">The sample copies data from an SAP Business Warehouse instance to an Azure blob hourly.</span></span> <span data-ttu-id="7e871-205">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="7e871-205">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="7e871-206">Dans un premier temps, configurez la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="7e871-206">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="7e871-207">Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="7e871-207">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-business-warehouse-linked-service"></a><span data-ttu-id="7e871-208">Service lié SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="7e871-208">SAP Business Warehouse linked service</span></span>
<span data-ttu-id="7e871-209">Ce service lié relie votre instance SAP BW à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="7e871-209">This linked service links your SAP BW instance to the data factory.</span></span> <span data-ttu-id="7e871-210">La propriété du type est définie sur **SapBw**.</span><span class="sxs-lookup"><span data-stu-id="7e871-210">The type property is set to **SapBw**.</span></span> <span data-ttu-id="7e871-211">La section typeProperties fournit des informations de connexion pour l’instance SAP BW.</span><span class="sxs-lookup"><span data-stu-id="7e871-211">The typeProperties section provides connection information for the SAP BW instance.</span></span> 

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="7e871-212">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7e871-212">Azure Storage linked service</span></span>
<span data-ttu-id="7e871-213">Le service lié relie votre compte de stockage Azure à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="7e871-213">This linked service links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="7e871-214">La propriété de type est définie sur **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="7e871-214">The type property is set to **AzureStorage**.</span></span> <span data-ttu-id="7e871-215">La section typeProperties fournit des informations de connexion pour le compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="7e871-215">The typeProperties section provides connection information for the Azure Storage account.</span></span>

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

### <a name="sap-bw-input-dataset"></a><span data-ttu-id="7e871-216">Jeu de données d’entrée SAP BW</span><span class="sxs-lookup"><span data-stu-id="7e871-216">SAP BW input dataset</span></span>
<span data-ttu-id="7e871-217">Ce jeu de données définit le jeu de données SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7e871-217">This dataset defines the SAP Business Warehouse dataset.</span></span> <span data-ttu-id="7e871-218">Vous définissez le type de données du jeu de données Data Factory sur **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="7e871-218">You set the type of the Data Factory dataset to **RelationalTable**.</span></span> <span data-ttu-id="7e871-219">Actuellement, vous ne spécifiez pas de propriétés propres à un type pour un jeu de données SAP BW.</span><span class="sxs-lookup"><span data-stu-id="7e871-219">Currently, you do not specify any type-specific properties for an SAP BW dataset.</span></span> <span data-ttu-id="7e871-220">La requête dans la définition de l’activité de copie spécifie les données à lire à partir de l’instance SAP BW.</span><span class="sxs-lookup"><span data-stu-id="7e871-220">The query in the Copy Activity definition specifies what data to read from the SAP BW instance.</span></span> 

<span data-ttu-id="7e871-221">La définition de la propriété external sur true informe le service Data Factory qu’il s’agit d’une table qui est externe à la fabrique de données et non produite par une activité dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="7e871-221">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="7e871-222">Les propriétés de fréquence et d’intervalle définissent la planification.</span><span class="sxs-lookup"><span data-stu-id="7e871-222">Frequency and interval properties defines the schedule.</span></span> <span data-ttu-id="7e871-223">Dans ce cas, les données sont lues à partir de l’instance SAP BW toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="7e871-223">In this case, the data is read from the SAP BW instance hourly.</span></span> 

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



### <a name="azure-blob-output-dataset"></a><span data-ttu-id="7e871-224">Jeu de données de sortie d’objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="7e871-224">Azure Blob output dataset</span></span>
<span data-ttu-id="7e871-225">Ce jeu de données définit le jeu de données d’objet blob Azure de sortie.</span><span class="sxs-lookup"><span data-stu-id="7e871-225">This dataset defines the output Azure Blob dataset.</span></span> <span data-ttu-id="7e871-226">La propriété du type est définie sur AzureBlob.</span><span class="sxs-lookup"><span data-stu-id="7e871-226">The type property is set to AzureBlob.</span></span> <span data-ttu-id="7e871-227">La section typeProperties indique l’emplacement auquel les données copiées à partir de l’instance SAP BW sont stockées.</span><span class="sxs-lookup"><span data-stu-id="7e871-227">The typeProperties section provides where the data copied from the SAP BW instance is stored.</span></span> <span data-ttu-id="7e871-228">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="7e871-228">The data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="7e871-229">Le chemin d’accès du dossier pour l’objet blob est évalué dynamiquement en fonction de l’heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="7e871-229">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="7e871-230">Le chemin d’accès du dossier utilise l’année, le mois, le jour et l’heure de l’heure de début.</span><span class="sxs-lookup"><span data-stu-id="7e871-230">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="7e871-231">Pipeline avec activité de copie</span><span class="sxs-lookup"><span data-stu-id="7e871-231">Pipeline with Copy activity</span></span>
<span data-ttu-id="7e871-232">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="7e871-232">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="7e871-233">Dans la définition du pipeline JSON, le type **source** est défini sur **RelationalSource** (pour la source SAP BW) et le type **sink** est défini sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="7e871-233">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP BW source) and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="7e871-234">La requête spécifiée pour la propriété **query** sélectionne les données de la dernière heure à copier.</span><span class="sxs-lookup"><span data-stu-id="7e871-234">The query specified for the **query** property selects the data in the past hour to copy.</span></span>

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



### <a name="type-mapping-for-sap-bw"></a><span data-ttu-id="7e871-235">Mappage de type pour SAP BW</span><span class="sxs-lookup"><span data-stu-id="7e871-235">Type mapping for SAP BW</span></span>
<span data-ttu-id="7e871-236">Comme mentionné dans l’article consacré aux [activités de déplacement des données](data-factory-data-movement-activities.md) , l’activité de copie convertit automatiquement des types source en types récepteur à l’aide de l’approche en deux étapes suivante :</span><span class="sxs-lookup"><span data-stu-id="7e871-236">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="7e871-237">Conversion de types natifs source en types .NET</span><span class="sxs-lookup"><span data-stu-id="7e871-237">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="7e871-238">Conversion de types .NET en types récepteur natifs</span><span class="sxs-lookup"><span data-stu-id="7e871-238">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="7e871-239">Lors du déplacement des données à partir de SAP BW, les mappages suivants sont réalisés des types SAP BW vers les types .NET.</span><span class="sxs-lookup"><span data-stu-id="7e871-239">When moving data from SAP BW, the following mappings are used from SAP BW types to .NET types.</span></span>

<span data-ttu-id="7e871-240">Type de données dans le dictionnaire ABAP</span><span class="sxs-lookup"><span data-stu-id="7e871-240">Data type in the ABAP Dictionary</span></span> | <span data-ttu-id="7e871-241">Type de données .Net</span><span class="sxs-lookup"><span data-stu-id="7e871-241">.Net Data Type</span></span>
-------------------------------- | --------------
<span data-ttu-id="7e871-242">ACCP</span><span class="sxs-lookup"><span data-stu-id="7e871-242">ACCP</span></span> |  <span data-ttu-id="7e871-243">int</span><span class="sxs-lookup"><span data-stu-id="7e871-243">Int</span></span>
<span data-ttu-id="7e871-244">CHAR</span><span class="sxs-lookup"><span data-stu-id="7e871-244">CHAR</span></span> | <span data-ttu-id="7e871-245">String</span><span class="sxs-lookup"><span data-stu-id="7e871-245">String</span></span>
<span data-ttu-id="7e871-246">CLNT</span><span class="sxs-lookup"><span data-stu-id="7e871-246">CLNT</span></span> | <span data-ttu-id="7e871-247">String</span><span class="sxs-lookup"><span data-stu-id="7e871-247">String</span></span>
<span data-ttu-id="7e871-248">CURR</span><span class="sxs-lookup"><span data-stu-id="7e871-248">CURR</span></span> | <span data-ttu-id="7e871-249">Décimal</span><span class="sxs-lookup"><span data-stu-id="7e871-249">Decimal</span></span>
<span data-ttu-id="7e871-250">CUKY</span><span class="sxs-lookup"><span data-stu-id="7e871-250">CUKY</span></span> | <span data-ttu-id="7e871-251">String</span><span class="sxs-lookup"><span data-stu-id="7e871-251">String</span></span>
<span data-ttu-id="7e871-252">DEC</span><span class="sxs-lookup"><span data-stu-id="7e871-252">DEC</span></span> | <span data-ttu-id="7e871-253">Décimal</span><span class="sxs-lookup"><span data-stu-id="7e871-253">Decimal</span></span>
<span data-ttu-id="7e871-254">FLTP</span><span class="sxs-lookup"><span data-stu-id="7e871-254">FLTP</span></span> | <span data-ttu-id="7e871-255">Double</span><span class="sxs-lookup"><span data-stu-id="7e871-255">Double</span></span>
<span data-ttu-id="7e871-256">INT1</span><span class="sxs-lookup"><span data-stu-id="7e871-256">INT1</span></span> | <span data-ttu-id="7e871-257">Byte</span><span class="sxs-lookup"><span data-stu-id="7e871-257">Byte</span></span>
<span data-ttu-id="7e871-258">INT2</span><span class="sxs-lookup"><span data-stu-id="7e871-258">INT2</span></span> | <span data-ttu-id="7e871-259">Int16</span><span class="sxs-lookup"><span data-stu-id="7e871-259">Int16</span></span>
<span data-ttu-id="7e871-260">INT4</span><span class="sxs-lookup"><span data-stu-id="7e871-260">INT4</span></span> | <span data-ttu-id="7e871-261">int</span><span class="sxs-lookup"><span data-stu-id="7e871-261">Int</span></span>
<span data-ttu-id="7e871-262">LANG</span><span class="sxs-lookup"><span data-stu-id="7e871-262">LANG</span></span> | <span data-ttu-id="7e871-263">String</span><span class="sxs-lookup"><span data-stu-id="7e871-263">String</span></span>
<span data-ttu-id="7e871-264">LCHR</span><span class="sxs-lookup"><span data-stu-id="7e871-264">LCHR</span></span> | <span data-ttu-id="7e871-265">String</span><span class="sxs-lookup"><span data-stu-id="7e871-265">String</span></span>
<span data-ttu-id="7e871-266">LRAW</span><span class="sxs-lookup"><span data-stu-id="7e871-266">LRAW</span></span> | <span data-ttu-id="7e871-267">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7e871-267">Byte[]</span></span>
<span data-ttu-id="7e871-268">PREC</span><span class="sxs-lookup"><span data-stu-id="7e871-268">PREC</span></span> | <span data-ttu-id="7e871-269">Int16</span><span class="sxs-lookup"><span data-stu-id="7e871-269">Int16</span></span>
<span data-ttu-id="7e871-270">QUAN</span><span class="sxs-lookup"><span data-stu-id="7e871-270">QUAN</span></span> | <span data-ttu-id="7e871-271">Décimal</span><span class="sxs-lookup"><span data-stu-id="7e871-271">Decimal</span></span>
<span data-ttu-id="7e871-272">RAW</span><span class="sxs-lookup"><span data-stu-id="7e871-272">RAW</span></span> | <span data-ttu-id="7e871-273">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7e871-273">Byte[]</span></span>
<span data-ttu-id="7e871-274">RAWSTRING</span><span class="sxs-lookup"><span data-stu-id="7e871-274">RAWSTRING</span></span> | <span data-ttu-id="7e871-275">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7e871-275">Byte[]</span></span>
<span data-ttu-id="7e871-276">STRING</span><span class="sxs-lookup"><span data-stu-id="7e871-276">STRING</span></span> | <span data-ttu-id="7e871-277">String</span><span class="sxs-lookup"><span data-stu-id="7e871-277">String</span></span>
<span data-ttu-id="7e871-278">UNITÉ</span><span class="sxs-lookup"><span data-stu-id="7e871-278">UNIT</span></span> | <span data-ttu-id="7e871-279">String</span><span class="sxs-lookup"><span data-stu-id="7e871-279">String</span></span>
<span data-ttu-id="7e871-280">DATS</span><span class="sxs-lookup"><span data-stu-id="7e871-280">DATS</span></span> | <span data-ttu-id="7e871-281">String</span><span class="sxs-lookup"><span data-stu-id="7e871-281">String</span></span>
<span data-ttu-id="7e871-282">NUMC</span><span class="sxs-lookup"><span data-stu-id="7e871-282">NUMC</span></span> | <span data-ttu-id="7e871-283">String</span><span class="sxs-lookup"><span data-stu-id="7e871-283">String</span></span>
<span data-ttu-id="7e871-284">TIMS</span><span class="sxs-lookup"><span data-stu-id="7e871-284">TIMS</span></span> | <span data-ttu-id="7e871-285">String</span><span class="sxs-lookup"><span data-stu-id="7e871-285">String</span></span>

> [!NOTE]
> <span data-ttu-id="7e871-286">Pour savoir comment mapper des colonnes d’un jeu de données source à des colonnes d’un jeu de données récepteur, voir [Mappage des colonnes d’un jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="7e871-286">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="map-source-to-sink-columns"></a><span data-ttu-id="7e871-287">Mapper les colonnes source aux colonnes du récepteur</span><span class="sxs-lookup"><span data-stu-id="7e871-287">Map source to sink columns</span></span>
<span data-ttu-id="7e871-288">Pour en savoir plus sur le mappage de colonnes du jeu de données source à des colonnes du jeu de données récepteur, voir [Mappage des colonnes d’un jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="7e871-288">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="7e871-289">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="7e871-289">Repeatable read from relational sources</span></span>
<span data-ttu-id="7e871-290">Lorsque vous copiez des données à partir de magasins de données relationnels, gardez à l’esprit la répétabilité de l’opération, afin d’éviter des résultats imprévus.</span><span class="sxs-lookup"><span data-stu-id="7e871-290">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="7e871-291">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="7e871-291">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="7e871-292">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="7e871-292">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="7e871-293">Lorsqu’une tranche est réexécutée d’une manière ou d’une autre, vous devez vous assurer que les mêmes données sont lues et ce, quel que soit le nombre d’exécutions de la tranche.</span><span class="sxs-lookup"><span data-stu-id="7e871-293">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="7e871-294">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="7e871-294">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="7e871-295">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="7e871-295">Performance and Tuning</span></span>
<span data-ttu-id="7e871-296">Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="7e871-296">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
