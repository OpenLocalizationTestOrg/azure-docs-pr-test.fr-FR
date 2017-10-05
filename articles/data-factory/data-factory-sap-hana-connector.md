---
title: "Déplacer des données depuis SAP HANA à l’aide d’Azure Data Factory | Microsoft Docs"
description: "Découvrez comment déplacer des données depuis SAP HANA à l’aide d’Azure Data Factory."
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
ms.openlocfilehash: 2ab488d82d24999a6231e40cb719715463c51d64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a><span data-ttu-id="851d0-103">Déplacer des données depuis SAP HANA à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="851d0-103">Move data From SAP HANA using Azure Data Factory</span></span>
<span data-ttu-id="851d0-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour déplacer des données à partir d’une base de données SAP HANA locale.</span><span class="sxs-lookup"><span data-stu-id="851d0-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP HANA.</span></span> <span data-ttu-id="851d0-105">Il s’appuie sur l’article [Activités de déplacement des données](data-factory-data-movement-activities.md), qui présente une vue d’ensemble du déplacement de données avec l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="851d0-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="851d0-106">Vous pouvez copier les données d’un magasin de données SAP HANA local dans tout magasin de données récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="851d0-106">You can copy data from an on-premises SAP HANA data store to any supported sink data store.</span></span> <span data-ttu-id="851d0-107">Pour obtenir la liste des magasins de données pris en charge en tant que récepteurs pour l’activité de copie, consultez le tableau [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="851d0-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="851d0-108">Actuellement, Data Factory prend uniquement en charge le déplacement de données de SAP HANA vers d’autres magasins de données, mais pas l’inverse.</span><span class="sxs-lookup"><span data-stu-id="851d0-108">Data factory currently supports only moving data from an SAP HANA to other data stores, but not for moving data from other data stores to an SAP HANA.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="851d0-109">Versions prises en charge et installation</span><span class="sxs-lookup"><span data-stu-id="851d0-109">Supported versions and installation</span></span>
<span data-ttu-id="851d0-110">Ce connecteur prend en charge n’importe quelle version de base de données SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="851d0-110">This connector supports any version of SAP HANA database.</span></span> <span data-ttu-id="851d0-111">Il prend en charge la copie de données à partir de modèles d’informations HANA (comme les vues Analyse et Calcul) et les tables Ligne/Colonne à l’aide de requêtes SQL.</span><span class="sxs-lookup"><span data-stu-id="851d0-111">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span></span>

<span data-ttu-id="851d0-112">Pour activer la connectivité à l’instance SAP HANA, installez les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="851d0-112">To enable the connectivity to the SAP HANA instance, install the following components:</span></span>
- <span data-ttu-id="851d0-113">**Passerelle de gestion des données** : le service de fabrique de données prend en charge la connexion aux magasins de données locaux (y compris SAP HANA) à l’aide d’un composant appelé passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="851d0-113">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span></span> <span data-ttu-id="851d0-114">Consultez l’article [Déplacement de données d’un magasin de données local vers un magasin de données cloud](data-factory-move-data-between-onprem-and-cloud.md) pour en savoir plus sur la passerelle de gestion des données et obtenir des instructions détaillées sur la configuration de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="851d0-114">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="851d0-115">Une passerelle est requise même si SAP HANA est hébergé sur une machine virtuelle Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="851d0-115">Gateway is required even if the SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="851d0-116">Vous pouvez installer la passerelle sur la même machine virtuelle que le magasin de données, ou sur une autre machine virtuelle pourvu que la passerelle puisse se connecter à la base de données.</span><span class="sxs-lookup"><span data-stu-id="851d0-116">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>
- <span data-ttu-id="851d0-117">Le **pilote ODBC SAP HANA** sur la machine passerelle.</span><span class="sxs-lookup"><span data-stu-id="851d0-117">**SAP HANA ODBC driver** on the gateway machine.</span></span> <span data-ttu-id="851d0-118">Vous pouvez télécharger le pilote ODBC SAP HANA à partir du [Centre de téléchargement de logiciels SAP](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="851d0-118">You can download the SAP HANA ODBC driver from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="851d0-119">Faites une recherche avec le mot-clé **SAP HANA CLIENT for Windows**.</span><span class="sxs-lookup"><span data-stu-id="851d0-119">Search with the keyword **SAP HANA CLIENT for Windows**.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="851d0-120">Prise en main</span><span class="sxs-lookup"><span data-stu-id="851d0-120">Getting started</span></span>
<span data-ttu-id="851d0-121">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données Cassandra local à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="851d0-121">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="851d0-122">Le moyen le plus simple de créer un pipeline consiste à utiliser **l’Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="851d0-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="851d0-123">Consultez la page [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant Copier des données.</span><span class="sxs-lookup"><span data-stu-id="851d0-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="851d0-124">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="851d0-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="851d0-125">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="851d0-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="851d0-126">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="851d0-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="851d0-127">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="851d0-127">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="851d0-128">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="851d0-128">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="851d0-129">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="851d0-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="851d0-130">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="851d0-130">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="851d0-131">Lorsque vous utilisez des outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory au format JSON.</span><span class="sxs-lookup"><span data-stu-id="851d0-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="851d0-132">Pour consulter un exemple contenant des définitions JSON pour les entités Data Factory utilisées pour copier des données d’un magasin de données SAP HANA local, consultez la section [Exemple JSON : copier des données depuis une instance SAP HANA vers Azure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) de cet article.</span><span class="sxs-lookup"><span data-stu-id="851d0-132">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA to Azure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="851d0-133">Les sections suivantes contiennent des informations détaillées sur les propriétés JSON utilisées pour définir les entités Data Factory propres à un magasin de données SAP HANA :</span><span class="sxs-lookup"><span data-stu-id="851d0-133">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP HANA data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="851d0-134">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="851d0-134">Linked service properties</span></span>
<span data-ttu-id="851d0-135">Le tableau suivant fournit la description des éléments JSON spécifiques au service lié SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="851d0-135">The following table provides description for JSON elements specific to SAP HANA linked service.</span></span>

<span data-ttu-id="851d0-136">Propriété</span><span class="sxs-lookup"><span data-stu-id="851d0-136">Property</span></span> | <span data-ttu-id="851d0-137">Description</span><span class="sxs-lookup"><span data-stu-id="851d0-137">Description</span></span> | <span data-ttu-id="851d0-138">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="851d0-138">Allowed values</span></span> | <span data-ttu-id="851d0-139">Requis</span><span class="sxs-lookup"><span data-stu-id="851d0-139">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="851d0-140">server</span><span class="sxs-lookup"><span data-stu-id="851d0-140">server</span></span> | <span data-ttu-id="851d0-141">Le nom du serveur sur lequel réside l’instance SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="851d0-141">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="851d0-142">Si votre serveur utilise un port personnalisé, spécifiez `server:port`.</span><span class="sxs-lookup"><span data-stu-id="851d0-142">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="851d0-143">string</span><span class="sxs-lookup"><span data-stu-id="851d0-143">string</span></span> | <span data-ttu-id="851d0-144">Oui</span><span class="sxs-lookup"><span data-stu-id="851d0-144">Yes</span></span>
<span data-ttu-id="851d0-145">authenticationType</span><span class="sxs-lookup"><span data-stu-id="851d0-145">authenticationType</span></span> | <span data-ttu-id="851d0-146">Type d'authentification.</span><span class="sxs-lookup"><span data-stu-id="851d0-146">Type of authentication.</span></span> | <span data-ttu-id="851d0-147">chaîne.</span><span class="sxs-lookup"><span data-stu-id="851d0-147">string.</span></span> <span data-ttu-id="851d0-148">« Basic » ou « Windows »</span><span class="sxs-lookup"><span data-stu-id="851d0-148">"Basic" or "Windows"</span></span> | <span data-ttu-id="851d0-149">Oui</span><span class="sxs-lookup"><span data-stu-id="851d0-149">Yes</span></span> 
<span data-ttu-id="851d0-150">username</span><span class="sxs-lookup"><span data-stu-id="851d0-150">username</span></span> | <span data-ttu-id="851d0-151">Nom de l’utilisateur qui a accès au serveur SAP</span><span class="sxs-lookup"><span data-stu-id="851d0-151">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="851d0-152">string</span><span class="sxs-lookup"><span data-stu-id="851d0-152">string</span></span> | <span data-ttu-id="851d0-153">Oui</span><span class="sxs-lookup"><span data-stu-id="851d0-153">Yes</span></span>
<span data-ttu-id="851d0-154">password</span><span class="sxs-lookup"><span data-stu-id="851d0-154">password</span></span> | <span data-ttu-id="851d0-155">Mot de passe pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="851d0-155">Password for the user.</span></span> | <span data-ttu-id="851d0-156">string</span><span class="sxs-lookup"><span data-stu-id="851d0-156">string</span></span> | <span data-ttu-id="851d0-157">Oui</span><span class="sxs-lookup"><span data-stu-id="851d0-157">Yes</span></span>
<span data-ttu-id="851d0-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="851d0-158">gatewayName</span></span> | <span data-ttu-id="851d0-159">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter à l’instance SAP HANA locale.</span><span class="sxs-lookup"><span data-stu-id="851d0-159">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span></span> | <span data-ttu-id="851d0-160">string</span><span class="sxs-lookup"><span data-stu-id="851d0-160">string</span></span> | <span data-ttu-id="851d0-161">Oui</span><span class="sxs-lookup"><span data-stu-id="851d0-161">Yes</span></span>
<span data-ttu-id="851d0-162">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="851d0-162">encryptedCredential</span></span> | <span data-ttu-id="851d0-163">La chaîne d’informations d’identification chiffrée.</span><span class="sxs-lookup"><span data-stu-id="851d0-163">The encrypted credential string.</span></span> | <span data-ttu-id="851d0-164">string</span><span class="sxs-lookup"><span data-stu-id="851d0-164">string</span></span> | <span data-ttu-id="851d0-165">Non</span><span class="sxs-lookup"><span data-stu-id="851d0-165">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="851d0-166">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="851d0-166">Dataset properties</span></span>
<span data-ttu-id="851d0-167">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="851d0-167">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="851d0-168">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="851d0-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="851d0-169">La section **typeProperties** est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="851d0-169">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="851d0-170">Aucune propriété propre à un type n’est prise en charge pour le type de jeu de données SAP HANA **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="851d0-170">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="851d0-171">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="851d0-171">Copy activity properties</span></span>
<span data-ttu-id="851d0-172">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="851d0-172">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="851d0-173">Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="851d0-173">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="851d0-174">En revanche, les propriétés disponibles dans la section **typeProperties** de l’activité varient pour chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="851d0-174">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="851d0-175">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="851d0-175">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="851d0-176">Lorsque la source de l’activité de copie est de type **RelationalSource** (qui inclut SAP HANA), les propriétés suivantes sont disponibles dans la section typeProperties :</span><span class="sxs-lookup"><span data-stu-id="851d0-176">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="851d0-177">Propriété</span><span class="sxs-lookup"><span data-stu-id="851d0-177">Property</span></span> | <span data-ttu-id="851d0-178">Description</span><span class="sxs-lookup"><span data-stu-id="851d0-178">Description</span></span> | <span data-ttu-id="851d0-179">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="851d0-179">Allowed values</span></span> | <span data-ttu-id="851d0-180">Requis</span><span class="sxs-lookup"><span data-stu-id="851d0-180">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="851d0-181">query</span><span class="sxs-lookup"><span data-stu-id="851d0-181">query</span></span> | <span data-ttu-id="851d0-182">Spécifie la requête SQL pour lire les données de l’instance SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="851d0-182">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="851d0-183">Requête SQL.</span><span class="sxs-lookup"><span data-stu-id="851d0-183">SQL query.</span></span> | <span data-ttu-id="851d0-184">Oui</span><span class="sxs-lookup"><span data-stu-id="851d0-184">Yes</span></span> |

## <a name="json-example-copy-data-from-sap-hana-to-azure-blob"></a><span data-ttu-id="851d0-185">Exemple JSON : copier des données à partir de SAP HANA vers Azure Blob</span><span class="sxs-lookup"><span data-stu-id="851d0-185">JSON example: Copy data from SAP HANA to Azure Blob</span></span>
<span data-ttu-id="851d0-186">L’exemple suivant présente des exemples de définitions de JSON que vous pouvez utiliser pour créer un pipeline à l’aide du [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), de [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [d’Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="851d0-186">The following sample provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="851d0-187">Cet exemple indique comment copier des données depuis SAP HANA vers un système Blob Storage Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="851d0-187">This sample shows how to copy data from an on-premises SAP HANA to an Azure Blob Storage.</span></span> <span data-ttu-id="851d0-188">Toutefois, les données peuvent être copiées **directement** vers l’un des récepteurs répertoriés [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) , via l’activité de copie d’Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="851d0-188">However, data can be copied **directly** to any of the sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="851d0-189">Cet exemple fournit des extraits de code JSON.</span><span class="sxs-lookup"><span data-stu-id="851d0-189">This sample provides JSON snippets.</span></span> <span data-ttu-id="851d0-190">Il n’inclut pas d’instructions détaillées pour la création de la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="851d0-190">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="851d0-191">Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="851d0-191">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="851d0-192">L’exemple contient les entités de fabrique de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="851d0-192">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="851d0-193">Un service lié de type [SapHana](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="851d0-193">A linked service of type [SapHana](#linked-service-properties).</span></span>
2. <span data-ttu-id="851d0-194">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="851d0-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="851d0-195">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="851d0-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="851d0-196">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="851d0-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="851d0-197">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [RelationalSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="851d0-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="851d0-198">L’exemple copie les données d’une instance SAP HANA vers un objet blob Azure toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="851d0-198">The sample copies data from an SAP HANA instance to an Azure blob hourly.</span></span> <span data-ttu-id="851d0-199">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="851d0-199">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="851d0-200">Dans un premier temps, configurez la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="851d0-200">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="851d0-201">Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="851d0-201">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-hana-linked-service"></a><span data-ttu-id="851d0-202">Service lié SAP HANA</span><span class="sxs-lookup"><span data-stu-id="851d0-202">SAP HANA linked service</span></span>
<span data-ttu-id="851d0-203">Ce service lié relie votre instance SAP HANA à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="851d0-203">This linked service links your SAP HANA instance to the data factory.</span></span> <span data-ttu-id="851d0-204">La propriété type est définie sur **SapHana**.</span><span class="sxs-lookup"><span data-stu-id="851d0-204">The type property is set to **SapHana**.</span></span> <span data-ttu-id="851d0-205">La section typeProperties fournit des informations de connexion pour l’instance SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="851d0-205">The typeProperties section provides connection information for the SAP HANA instance.</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="851d0-206">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="851d0-206">Azure Storage linked service</span></span>
<span data-ttu-id="851d0-207">Le service lié relie votre compte de stockage Azure à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="851d0-207">This linked service links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="851d0-208">La propriété de type est définie sur **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="851d0-208">The type property is set to **AzureStorage**.</span></span> <span data-ttu-id="851d0-209">La section typeProperties fournit des informations de connexion pour le compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="851d0-209">The typeProperties section provides connection information for the Azure Storage account.</span></span>

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

### <a name="sap-hana-input-dataset"></a><span data-ttu-id="851d0-210">Jeu de données d’entrée SAP HANA</span><span class="sxs-lookup"><span data-stu-id="851d0-210">SAP HANA input dataset</span></span>

<span data-ttu-id="851d0-211">Ce jeu de données définit le jeu de données SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="851d0-211">This dataset defines the SAP HANA dataset.</span></span> <span data-ttu-id="851d0-212">Vous définissez le type de données du jeu de données Data Factory sur **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="851d0-212">You set the type of the Data Factory dataset to **RelationalTable**.</span></span> <span data-ttu-id="851d0-213">Actuellement, vous ne spécifiez pas de propriétés propres à un type pour un jeu de données SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="851d0-213">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span></span> <span data-ttu-id="851d0-214">La requête dans la définition de l’activité de copie spécifie les données à lire à partir de l’instance SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="851d0-214">The query in the Copy Activity definition specifies what data to read from the SAP HANA instance.</span></span> 

<span data-ttu-id="851d0-215">La définition de la propriété external sur true informe le service Data Factory qu’il s’agit d’un jeu de données qui est externe à la Data Factory et non produit par une activité dans la Data Factory.</span><span class="sxs-lookup"><span data-stu-id="851d0-215">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="851d0-216">Les propriétés de fréquence et d’intervalle définissent la planification.</span><span class="sxs-lookup"><span data-stu-id="851d0-216">Frequency and interval properties defines the schedule.</span></span> <span data-ttu-id="851d0-217">Dans ce cas, les données sont lues à partir de l’instance SAP HANA toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="851d0-217">In this case, the data is read from the SAP HANA instance hourly.</span></span> 

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="851d0-218">Jeu de données de sortie d’objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="851d0-218">Azure Blob output dataset</span></span>
<span data-ttu-id="851d0-219">Ce jeu de données définit le jeu de données d’objet blob Azure de sortie.</span><span class="sxs-lookup"><span data-stu-id="851d0-219">This dataset defines the output Azure Blob dataset.</span></span> <span data-ttu-id="851d0-220">La propriété type est définie sur AzureBlob.</span><span class="sxs-lookup"><span data-stu-id="851d0-220">The type property is set to AzureBlob.</span></span> <span data-ttu-id="851d0-221">La section typeProperties indique l’endroit auquel les données copiées à partir de l’instance SAP HANA sont stockées.</span><span class="sxs-lookup"><span data-stu-id="851d0-221">The typeProperties section provides where the data copied from the SAP HANA instance is stored.</span></span> <span data-ttu-id="851d0-222">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="851d0-222">The data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="851d0-223">Le chemin d’accès du dossier pour l’objet blob est évalué dynamiquement en fonction de l’heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="851d0-223">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="851d0-224">Le chemin d’accès du dossier utilise l’année, le mois, le jour et l’heure de l’heure de début.</span><span class="sxs-lookup"><span data-stu-id="851d0-224">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="851d0-225">Pipeline avec activité de copie</span><span class="sxs-lookup"><span data-stu-id="851d0-225">Pipeline with Copy activity</span></span>

<span data-ttu-id="851d0-226">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="851d0-226">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="851d0-227">Dans la définition du pipeline JSON, le type **source** est défini sur **RelationalSource** (pour la source SAP HANA) et le type **sink** est défini sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="851d0-227">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP HANA source) and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="851d0-228">La requête SQL spécifiée pour la propriété **query** sélectionne les données de la dernière heure à copier.</span><span class="sxs-lookup"><span data-stu-id="851d0-228">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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


### <a name="type-mapping-for-sap-hana"></a><span data-ttu-id="851d0-229">Mappage de type pour SAP HANA</span><span class="sxs-lookup"><span data-stu-id="851d0-229">Type mapping for SAP HANA</span></span>
<span data-ttu-id="851d0-230">Comme mentionné dans l’article consacré aux [activités de déplacement des données](data-factory-data-movement-activities.md) , l’activité de copie convertit automatiquement des types source en types récepteur à l’aide de l’approche en deux étapes suivante :</span><span class="sxs-lookup"><span data-stu-id="851d0-230">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="851d0-231">Conversion de types natifs source en types .NET</span><span class="sxs-lookup"><span data-stu-id="851d0-231">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="851d0-232">Conversion de types .NET en types récepteur natifs</span><span class="sxs-lookup"><span data-stu-id="851d0-232">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="851d0-233">Lors du déplacement des données à partir de SAP HANA, les mappages suivants sont réalisés des types SAP HANA vers les types .NET.</span><span class="sxs-lookup"><span data-stu-id="851d0-233">When moving data from SAP HANA, the following mappings are used from SAP HANA types to .NET types.</span></span>

<span data-ttu-id="851d0-234">Type SAP HANA</span><span class="sxs-lookup"><span data-stu-id="851d0-234">SAP HANA Type</span></span> | <span data-ttu-id="851d0-235">Type basé sur .NET</span><span class="sxs-lookup"><span data-stu-id="851d0-235">.NET Based Type</span></span>
------------- | ---------------
<span data-ttu-id="851d0-236">TINYINT</span><span class="sxs-lookup"><span data-stu-id="851d0-236">TINYINT</span></span> | <span data-ttu-id="851d0-237">Byte</span><span class="sxs-lookup"><span data-stu-id="851d0-237">Byte</span></span>
<span data-ttu-id="851d0-238">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="851d0-238">SMALLINT</span></span> | <span data-ttu-id="851d0-239">Int16</span><span class="sxs-lookup"><span data-stu-id="851d0-239">Int16</span></span>
<span data-ttu-id="851d0-240">INT</span><span class="sxs-lookup"><span data-stu-id="851d0-240">INT</span></span> | <span data-ttu-id="851d0-241">Int32</span><span class="sxs-lookup"><span data-stu-id="851d0-241">Int32</span></span>
<span data-ttu-id="851d0-242">BIGINT</span><span class="sxs-lookup"><span data-stu-id="851d0-242">BIGINT</span></span> | <span data-ttu-id="851d0-243">Int64</span><span class="sxs-lookup"><span data-stu-id="851d0-243">Int64</span></span>
<span data-ttu-id="851d0-244">REAL</span><span class="sxs-lookup"><span data-stu-id="851d0-244">REAL</span></span> | <span data-ttu-id="851d0-245">Single</span><span class="sxs-lookup"><span data-stu-id="851d0-245">Single</span></span>
<span data-ttu-id="851d0-246">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="851d0-246">DOUBLE</span></span> | <span data-ttu-id="851d0-247">Single</span><span class="sxs-lookup"><span data-stu-id="851d0-247">Single</span></span>
<span data-ttu-id="851d0-248">DÉCIMAL</span><span class="sxs-lookup"><span data-stu-id="851d0-248">DECIMAL</span></span> | <span data-ttu-id="851d0-249">Décimal</span><span class="sxs-lookup"><span data-stu-id="851d0-249">Decimal</span></span>
<span data-ttu-id="851d0-250">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="851d0-250">BOOLEAN</span></span> | <span data-ttu-id="851d0-251">Byte</span><span class="sxs-lookup"><span data-stu-id="851d0-251">Byte</span></span>
<span data-ttu-id="851d0-252">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="851d0-252">VARCHAR</span></span> | <span data-ttu-id="851d0-253">String</span><span class="sxs-lookup"><span data-stu-id="851d0-253">String</span></span>
<span data-ttu-id="851d0-254">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="851d0-254">NVARCHAR</span></span> | <span data-ttu-id="851d0-255">String</span><span class="sxs-lookup"><span data-stu-id="851d0-255">String</span></span>
<span data-ttu-id="851d0-256">CLOB</span><span class="sxs-lookup"><span data-stu-id="851d0-256">CLOB</span></span> | <span data-ttu-id="851d0-257">Byte[]</span><span class="sxs-lookup"><span data-stu-id="851d0-257">Byte[]</span></span>
<span data-ttu-id="851d0-258">ALPHANUM</span><span class="sxs-lookup"><span data-stu-id="851d0-258">ALPHANUM</span></span> | <span data-ttu-id="851d0-259">String</span><span class="sxs-lookup"><span data-stu-id="851d0-259">String</span></span>
<span data-ttu-id="851d0-260">BLOB</span><span class="sxs-lookup"><span data-stu-id="851d0-260">BLOB</span></span> | <span data-ttu-id="851d0-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="851d0-261">Byte[]</span></span>
<span data-ttu-id="851d0-262">DATE</span><span class="sxs-lookup"><span data-stu-id="851d0-262">DATE</span></span> | <span data-ttu-id="851d0-263">DateTime</span><span class="sxs-lookup"><span data-stu-id="851d0-263">DateTime</span></span>
<span data-ttu-id="851d0-264">TEMPS</span><span class="sxs-lookup"><span data-stu-id="851d0-264">TIME</span></span> | <span data-ttu-id="851d0-265">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="851d0-265">TimeSpan</span></span>
<span data-ttu-id="851d0-266">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="851d0-266">TIMESTAMP</span></span> | <span data-ttu-id="851d0-267">DateTime</span><span class="sxs-lookup"><span data-stu-id="851d0-267">DateTime</span></span>
<span data-ttu-id="851d0-268">SECONDDATE</span><span class="sxs-lookup"><span data-stu-id="851d0-268">SECONDDATE</span></span> | <span data-ttu-id="851d0-269">DateTime</span><span class="sxs-lookup"><span data-stu-id="851d0-269">DateTime</span></span>

## <a name="known-limitations"></a><span data-ttu-id="851d0-270">Limites connues</span><span class="sxs-lookup"><span data-stu-id="851d0-270">Known limitations</span></span>
<span data-ttu-id="851d0-271">Il existe quelques limitations connues lors de la copie des données à partir de SAP HANA :</span><span class="sxs-lookup"><span data-stu-id="851d0-271">There are a few known limitations when copying data from SAP HANA:</span></span>

- <span data-ttu-id="851d0-272">Les chaînes NVARCHAR sont tronquées à une longueur maximale de 4 000 caractères Unicode</span><span class="sxs-lookup"><span data-stu-id="851d0-272">NVARCHAR strings are truncated to maximum length of 4000 Unicode characters</span></span>
- <span data-ttu-id="851d0-273">SMALLDECIMAL n’est pas pris en charge</span><span class="sxs-lookup"><span data-stu-id="851d0-273">SMALLDECIMAL is not supported</span></span>
- <span data-ttu-id="851d0-274">VARBINARY n’est pas pris en charge</span><span class="sxs-lookup"><span data-stu-id="851d0-274">VARBINARY is not supported</span></span>
- <span data-ttu-id="851d0-275">Les dates valides sont celles comprises entre 1899/12/30 et 9999/12/31</span><span class="sxs-lookup"><span data-stu-id="851d0-275">Valid Dates are between 1899/12/30 and 9999/12/31</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="851d0-276">Mapper les colonnes source aux colonnes de récepteur</span><span class="sxs-lookup"><span data-stu-id="851d0-276">Map source to sink columns</span></span>
<span data-ttu-id="851d0-277">Pour en savoir plus sur le mappage de colonnes du jeu de données source à des colonnes du jeu de données récepteur, voir [Mappage des colonnes d’un jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="851d0-277">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="851d0-278">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="851d0-278">Repeatable read from relational sources</span></span>
<span data-ttu-id="851d0-279">Lorsque vous copiez des données à partir de magasins de données relationnels, gardez à l’esprit la répétabilité de l’opération, afin d’éviter des résultats imprévus.</span><span class="sxs-lookup"><span data-stu-id="851d0-279">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="851d0-280">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="851d0-280">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="851d0-281">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="851d0-281">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="851d0-282">Lorsqu’une tranche est réexécutée d’une manière ou d’une autre, vous devez vous assurer que les mêmes données sont lues et ce, quel que soit le nombre d’exécutions de la tranche.</span><span class="sxs-lookup"><span data-stu-id="851d0-282">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="851d0-283">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="851d0-283">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="851d0-284">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="851d0-284">Performance and Tuning</span></span>
<span data-ttu-id="851d0-285">Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="851d0-285">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
