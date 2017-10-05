---
title: "Déplacer des données à partir de sources OData | Microsoft Docs"
description: "Apprenez à déplacer des données à partir de sources OData à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: de28fa56-3204-4546-a4df-21a21de43ed7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 624b6c8f317477d83539392c6c2f15c2dc69d401
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a><span data-ttu-id="436d2-103">Déplacer des données depuis une source OData à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="436d2-103">Move data From a OData source using Azure Data Factory</span></span>
<span data-ttu-id="436d2-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour déplacer des données à partir d’une source OData locale.</span><span class="sxs-lookup"><span data-stu-id="436d2-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an OData source.</span></span> <span data-ttu-id="436d2-105">Il s’appuie sur l’article [Activités de déplacement des données](data-factory-data-movement-activities.md), qui présente une vue d’ensemble du déplacement de données avec l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="436d2-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="436d2-106">Vous pouvez copier les données d’une source OData dans tout magasin de données récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="436d2-106">You can copy data from an OData source to any supported sink data store.</span></span> <span data-ttu-id="436d2-107">Consultez la table [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) pour obtenir la liste des magasins de données pris en charge en tant que récepteurs par l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="436d2-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="436d2-108">Actuellement, Data Factory prend uniquement en charge le déplacement de données d’une source OData vers d’autres magasins de données, mais pas l’inverse.</span><span class="sxs-lookup"><span data-stu-id="436d2-108">Data factory currently supports only moving data from an OData source to other data stores, but not for moving data from other data stores to an OData source.</span></span> 

## <a name="supported-versions-and-authentication-types"></a><span data-ttu-id="436d2-109">Versions et types d’authentification pris en charge</span><span class="sxs-lookup"><span data-stu-id="436d2-109">Supported versions and authentication types</span></span>
<span data-ttu-id="436d2-110">Ce connecteur OData prend en charge OData versions 3.0 et 4.0, et vous pouvez copier des données à partir de sources OData cloud et locales.</span><span class="sxs-lookup"><span data-stu-id="436d2-110">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span></span> <span data-ttu-id="436d2-111">Dans le second cas, vous devez installer la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="436d2-111">For the latter, you need to install the Data Management Gateway.</span></span> <span data-ttu-id="436d2-112">Pour plus d’informations sur la passerelle de gestion de données, consultez l’article [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="436d2-112">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

<span data-ttu-id="436d2-113">Les types d’authentification suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="436d2-113">Below authentication types are supported:</span></span>

* <span data-ttu-id="436d2-114">Pour accéder au flux OData **cloud**, vous pouvez utiliser l’authentification OAuth basée sur Azure Active Directory, anonyme ou de base (nom d’utilisateur et mot de passe).</span><span class="sxs-lookup"><span data-stu-id="436d2-114">To access **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span></span>
* <span data-ttu-id="436d2-115">Pour accéder au flux OData **local**, vous pouvez utiliser l’authentification anonyme, de base (nom d’utilisateur et mot de passe) ou Windows.</span><span class="sxs-lookup"><span data-stu-id="436d2-115">To access **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="436d2-116">Prise en main</span><span class="sxs-lookup"><span data-stu-id="436d2-116">Getting started</span></span>
<span data-ttu-id="436d2-117">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’une source OData à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="436d2-117">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span></span>

<span data-ttu-id="436d2-118">Le moyen le plus simple de créer un pipeline consiste à utiliser **l’Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="436d2-118">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="436d2-119">Consultez la page [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant Copier des données.</span><span class="sxs-lookup"><span data-stu-id="436d2-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="436d2-120">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="436d2-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="436d2-121">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="436d2-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="436d2-122">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="436d2-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="436d2-123">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="436d2-123">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="436d2-124">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="436d2-124">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="436d2-125">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="436d2-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="436d2-126">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="436d2-126">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="436d2-127">Lorsque vous utilisez des outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory au format JSON.</span><span class="sxs-lookup"><span data-stu-id="436d2-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="436d2-128">Pour consulter un exemple contenant des définitions JSON pour les entités Data Factory utilisées pour copier des données d’une source OData, consultez la section [Exemple JSON : copier des données depuis une source OData vers Azure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) de cet article.</span><span class="sxs-lookup"><span data-stu-id="436d2-128">For a sample with JSON definitions for Data Factory entities that are used to copy data from an OData source, see [JSON example: Copy data from OData source to Azure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="436d2-129">Les sections suivantes contiennent des informations détaillées sur les propriétés JSON utilisées pour définir les entités Data Factory propres à la source OData :</span><span class="sxs-lookup"><span data-stu-id="436d2-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to OData source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="436d2-130">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="436d2-130">Linked Service properties</span></span>
<span data-ttu-id="436d2-131">Le tableau suivant fournit la description des éléments JSON spécifiques au service lié OData.</span><span class="sxs-lookup"><span data-stu-id="436d2-131">The following table provides description for JSON elements specific to OData linked service.</span></span>

| <span data-ttu-id="436d2-132">Propriété</span><span class="sxs-lookup"><span data-stu-id="436d2-132">Property</span></span> | <span data-ttu-id="436d2-133">Description</span><span class="sxs-lookup"><span data-stu-id="436d2-133">Description</span></span> | <span data-ttu-id="436d2-134">Requis</span><span class="sxs-lookup"><span data-stu-id="436d2-134">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="436d2-135">type</span><span class="sxs-lookup"><span data-stu-id="436d2-135">type</span></span> |<span data-ttu-id="436d2-136">La propriété de type doit être définie sur **OData**</span><span class="sxs-lookup"><span data-stu-id="436d2-136">The type property must be set to: **OData**</span></span> |<span data-ttu-id="436d2-137">Oui</span><span class="sxs-lookup"><span data-stu-id="436d2-137">Yes</span></span> |
| <span data-ttu-id="436d2-138">URL</span><span class="sxs-lookup"><span data-stu-id="436d2-138">url</span></span> |<span data-ttu-id="436d2-139">URL du service OData.</span><span class="sxs-lookup"><span data-stu-id="436d2-139">Url of the OData service.</span></span> |<span data-ttu-id="436d2-140">Oui</span><span class="sxs-lookup"><span data-stu-id="436d2-140">Yes</span></span> |
| <span data-ttu-id="436d2-141">authenticationType</span><span class="sxs-lookup"><span data-stu-id="436d2-141">authenticationType</span></span> |<span data-ttu-id="436d2-142">Type d’authentification utilisé pour se connecter à la source OData.</span><span class="sxs-lookup"><span data-stu-id="436d2-142">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="436d2-143">Pour OData dans le cloud, les valeurs possibles sont Anonyme, De base et OAuth (notez qu’à l’heure actuelle, Azure Data Factory prend en charge uniquement l’authentification OAuth basée sur Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="436d2-143">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="436d2-144">Pour OData en local, les valeurs possibles sont Anonyme, De base et Windows.</span><span class="sxs-lookup"><span data-stu-id="436d2-144">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="436d2-145">Oui</span><span class="sxs-lookup"><span data-stu-id="436d2-145">Yes</span></span> |
| <span data-ttu-id="436d2-146">username</span><span class="sxs-lookup"><span data-stu-id="436d2-146">username</span></span> |<span data-ttu-id="436d2-147">Spécifiez le nom d’utilisateur si vous utilisez l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="436d2-147">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="436d2-148">Oui (uniquement si vous utilisez l’authentification de base)</span><span class="sxs-lookup"><span data-stu-id="436d2-148">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="436d2-149">password</span><span class="sxs-lookup"><span data-stu-id="436d2-149">password</span></span> |<span data-ttu-id="436d2-150">Spécifiez le mot de passe du compte d’utilisateur que vous avez spécifié pour le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="436d2-150">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="436d2-151">Oui (uniquement si vous utilisez l’authentification de base)</span><span class="sxs-lookup"><span data-stu-id="436d2-151">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="436d2-152">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="436d2-152">authorizedCredential</span></span> |<span data-ttu-id="436d2-153">Si vous utilisez OAuth, cliquez sur le bouton **Autoriser** de l’Assistant de copie Data Factory ou de l’éditeur et entrez vos informations d’identification. La valeur de cette propriété sera alors générée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="436d2-153">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="436d2-154">Oui (uniquement si vous utilisez l’authentification OAuth)</span><span class="sxs-lookup"><span data-stu-id="436d2-154">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="436d2-155">gatewayName</span><span class="sxs-lookup"><span data-stu-id="436d2-155">gatewayName</span></span> |<span data-ttu-id="436d2-156">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter au service OData local.</span><span class="sxs-lookup"><span data-stu-id="436d2-156">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="436d2-157">Indiquez uniquement si vous copiez des données à partir de la source OData locale.</span><span class="sxs-lookup"><span data-stu-id="436d2-157">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="436d2-158">Non</span><span class="sxs-lookup"><span data-stu-id="436d2-158">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="436d2-159">Utilisation de l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="436d2-159">Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="436d2-160">Utilisation de l’authentification anonyme</span><span class="sxs-lookup"><span data-stu-id="436d2-160">Using Anonymous authentication</span></span>
```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
        "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="436d2-161">Utilisation de l’authentification Windows pour accéder à la source OData locale</span><span class="sxs-lookup"><span data-stu-id="436d2-161">Using Windows authentication accessing on-premises OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of on-premises OData source e.g. Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="436d2-162">Utilisation de l’authentification OAuth pour accéder à la source OData dans le cloud</span><span class="sxs-lookup"><span data-stu-id="436d2-162">Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source e.g. https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking the Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="436d2-163">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="436d2-163">Dataset properties</span></span>
<span data-ttu-id="436d2-164">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="436d2-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="436d2-165">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="436d2-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="436d2-166">La section **typeProperties** est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="436d2-166">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="436d2-167">La section typeProperties du jeu de données de type **ODataResource** (qui inclut le jeu de données OData) présente les propriétés suivantes</span><span class="sxs-lookup"><span data-stu-id="436d2-167">The typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has the following properties</span></span>

| <span data-ttu-id="436d2-168">Propriété</span><span class="sxs-lookup"><span data-stu-id="436d2-168">Property</span></span> | <span data-ttu-id="436d2-169">Description</span><span class="sxs-lookup"><span data-stu-id="436d2-169">Description</span></span> | <span data-ttu-id="436d2-170">Requis</span><span class="sxs-lookup"><span data-stu-id="436d2-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="436d2-171">chemin d’accès</span><span class="sxs-lookup"><span data-stu-id="436d2-171">path</span></span> |<span data-ttu-id="436d2-172">Chemin d'accès à la ressource OData</span><span class="sxs-lookup"><span data-stu-id="436d2-172">Path to the OData resource</span></span> |<span data-ttu-id="436d2-173">Non</span><span class="sxs-lookup"><span data-stu-id="436d2-173">No</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="436d2-174">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="436d2-174">Copy activity properties</span></span>
<span data-ttu-id="436d2-175">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="436d2-175">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="436d2-176">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="436d2-176">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="436d2-177">En revanche, les propriétés disponibles dans la section typeProperties de l'activité varient pour chaque type d'activité.</span><span class="sxs-lookup"><span data-stu-id="436d2-177">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="436d2-178">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="436d2-178">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="436d2-179">Lorsque la source est de type **RelationalSource** (qui inclut OData), les propriétés suivantes sont disponibles dans la section typeProperties :</span><span class="sxs-lookup"><span data-stu-id="436d2-179">When source is of type **RelationalSource** (which includes OData) the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="436d2-180">Propriété</span><span class="sxs-lookup"><span data-stu-id="436d2-180">Property</span></span> | <span data-ttu-id="436d2-181">Description</span><span class="sxs-lookup"><span data-stu-id="436d2-181">Description</span></span> | <span data-ttu-id="436d2-182">Exemple</span><span class="sxs-lookup"><span data-stu-id="436d2-182">Example</span></span> | <span data-ttu-id="436d2-183">Requis</span><span class="sxs-lookup"><span data-stu-id="436d2-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="436d2-184">query</span><span class="sxs-lookup"><span data-stu-id="436d2-184">query</span></span> |<span data-ttu-id="436d2-185">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="436d2-185">Use the custom query to read data.</span></span> |<span data-ttu-id="436d2-186">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="436d2-186">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="436d2-187">Non</span><span class="sxs-lookup"><span data-stu-id="436d2-187">No</span></span> |

## <a name="type-mapping-for-odata"></a><span data-ttu-id="436d2-188">Mappage de type pour OData</span><span class="sxs-lookup"><span data-stu-id="436d2-188">Type Mapping for OData</span></span>
<span data-ttu-id="436d2-189">Comme mentionné dans l’article consacré aux [activités de déplacement de données](data-factory-data-movement-activities.md) , l’activité de copie convertit automatiquement les types source en types récepteur à l’aide de l’approche en deux étapes suivante.</span><span class="sxs-lookup"><span data-stu-id="436d2-189">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span></span>

1. <span data-ttu-id="436d2-190">Conversion de types natifs source en types .NET</span><span class="sxs-lookup"><span data-stu-id="436d2-190">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="436d2-191">Conversion de types .NET en types récepteur natifs</span><span class="sxs-lookup"><span data-stu-id="436d2-191">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="436d2-192">Lors du déplacement de données à partir d’OData, les mappages suivants sont utilisés entre les types OData et le type .NET.</span><span class="sxs-lookup"><span data-stu-id="436d2-192">When moving data from OData, the following mappings are used from OData types to .NET type.</span></span>

| <span data-ttu-id="436d2-193">Type de données OData</span><span class="sxs-lookup"><span data-stu-id="436d2-193">OData Data Type</span></span> | <span data-ttu-id="436d2-194">Type .NET</span><span class="sxs-lookup"><span data-stu-id="436d2-194">.NET Type</span></span> |
| --- | --- |
| <span data-ttu-id="436d2-195">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="436d2-195">Edm.Binary</span></span> |<span data-ttu-id="436d2-196">Byte[]</span><span class="sxs-lookup"><span data-stu-id="436d2-196">Byte[]</span></span> |
| <span data-ttu-id="436d2-197">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="436d2-197">Edm.Boolean</span></span> |<span data-ttu-id="436d2-198">Bool</span><span class="sxs-lookup"><span data-stu-id="436d2-198">Bool</span></span> |
| <span data-ttu-id="436d2-199">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="436d2-199">Edm.Byte</span></span> |<span data-ttu-id="436d2-200">Byte[]</span><span class="sxs-lookup"><span data-stu-id="436d2-200">Byte[]</span></span> |
| <span data-ttu-id="436d2-201">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="436d2-201">Edm.DateTime</span></span> |<span data-ttu-id="436d2-202">DateTime</span><span class="sxs-lookup"><span data-stu-id="436d2-202">DateTime</span></span> |
| <span data-ttu-id="436d2-203">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="436d2-203">Edm.Decimal</span></span> |<span data-ttu-id="436d2-204">Décimal</span><span class="sxs-lookup"><span data-stu-id="436d2-204">Decimal</span></span> |
| <span data-ttu-id="436d2-205">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="436d2-205">Edm.Double</span></span> |<span data-ttu-id="436d2-206">Double</span><span class="sxs-lookup"><span data-stu-id="436d2-206">Double</span></span> |
| <span data-ttu-id="436d2-207">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="436d2-207">Edm.Single</span></span> |<span data-ttu-id="436d2-208">Single</span><span class="sxs-lookup"><span data-stu-id="436d2-208">Single</span></span> |
| <span data-ttu-id="436d2-209">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="436d2-209">Edm.Guid</span></span> |<span data-ttu-id="436d2-210">Guid</span><span class="sxs-lookup"><span data-stu-id="436d2-210">Guid</span></span> |
| <span data-ttu-id="436d2-211">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="436d2-211">Edm.Int16</span></span> |<span data-ttu-id="436d2-212">Int16</span><span class="sxs-lookup"><span data-stu-id="436d2-212">Int16</span></span> |
| <span data-ttu-id="436d2-213">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="436d2-213">Edm.Int32</span></span> |<span data-ttu-id="436d2-214">Int32</span><span class="sxs-lookup"><span data-stu-id="436d2-214">Int32</span></span> |
| <span data-ttu-id="436d2-215">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="436d2-215">Edm.Int64</span></span> |<span data-ttu-id="436d2-216">Int64</span><span class="sxs-lookup"><span data-stu-id="436d2-216">Int64</span></span> |
| <span data-ttu-id="436d2-217">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="436d2-217">Edm.SByte</span></span> |<span data-ttu-id="436d2-218">Int16</span><span class="sxs-lookup"><span data-stu-id="436d2-218">Int16</span></span> |
| <span data-ttu-id="436d2-219">Edm.String</span><span class="sxs-lookup"><span data-stu-id="436d2-219">Edm.String</span></span> |<span data-ttu-id="436d2-220">String</span><span class="sxs-lookup"><span data-stu-id="436d2-220">String</span></span> |
| <span data-ttu-id="436d2-221">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="436d2-221">Edm.Time</span></span> |<span data-ttu-id="436d2-222">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="436d2-222">TimeSpan</span></span> |
| <span data-ttu-id="436d2-223">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="436d2-223">Edm.DateTimeOffset</span></span> |<span data-ttu-id="436d2-224">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="436d2-224">DateTimeOffset</span></span> |

> [!Note]
> <span data-ttu-id="436d2-225">Les types de données complexes OData, comme Object, ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="436d2-225">OData complex data types e.g. Object are not supported.</span></span>

## <a name="json-example-copy-data-from-odata-source-to-azure-blob"></a><span data-ttu-id="436d2-226">Exemple JSON : copie de données d’une source OData vers Azure Blob</span><span class="sxs-lookup"><span data-stu-id="436d2-226">JSON example: Copy data from OData source to Azure Blob</span></span>
<span data-ttu-id="436d2-227">Cet exemple présente des exemples de définition JSON que vous pouvez utiliser pour créer un pipeline à l’aide du [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), de [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [d’Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="436d2-227">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="436d2-228">Ils indiquent comment copier des données depuis une source OData vers un système Blob Storage Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="436d2-228">They show how to copy data from an OData source to an Azure Blob Storage.</span></span> <span data-ttu-id="436d2-229">Toutefois, les données peuvent être copiées vers l’un des récepteurs indiqués [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) , via l’activité de copie d’Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="436d2-229">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span> <span data-ttu-id="436d2-230">L’exemple contient les entités Data Factory suivantes :</span><span class="sxs-lookup"><span data-stu-id="436d2-230">The sample has the following Data Factory entities:</span></span>

1. <span data-ttu-id="436d2-231">Un service lié de type [OData](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="436d2-231">A linked service of type [OData](#linked-service-properties).</span></span>
2. <span data-ttu-id="436d2-232">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="436d2-232">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="436d2-233">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [ODataResource](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="436d2-233">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span></span>
4. <span data-ttu-id="436d2-234">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="436d2-234">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="436d2-235">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [RelationalSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="436d2-235">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="436d2-236">L'exemple copie toutes les heures les données provenant de l’interrogation d'une source OData vers un objet blob Azure.</span><span class="sxs-lookup"><span data-stu-id="436d2-236">The sample copies data from querying against an OData source to an Azure blob every hour.</span></span> <span data-ttu-id="436d2-237">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="436d2-237">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="436d2-238">**Service lié OData :** cet exemple utilise l’authentification anonyme.</span><span class="sxs-lookup"><span data-stu-id="436d2-238">**OData linked service:** This example uses the Anonymous authentication.</span></span> <span data-ttu-id="436d2-239">Consultez la section [Service lié OData](#linked-service-properties) pour connaître les différents types d’authentification que vous pouvez utiliser.</span><span class="sxs-lookup"><span data-stu-id="436d2-239">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
            }
        }
}
```

<span data-ttu-id="436d2-240">**Service lié Azure Storage :**</span><span class="sxs-lookup"><span data-stu-id="436d2-240">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="436d2-241">**Jeu de données d’entrée OData :**</span><span class="sxs-lookup"><span data-stu-id="436d2-241">**OData input dataset:**</span></span>

<span data-ttu-id="436d2-242">La définition de « external » : « true» informe le service Data Factory qu’il s’agit d’un jeu de données qui est externe à Data Factory et non produit par une activité dans Data Factory.</span><span class="sxs-lookup"><span data-stu-id="436d2-242">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "ODataDataset",
    "properties":
    {
        "type": "ODataResource",
        "typeProperties":
        {
                "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3                
        }
    }
}
```

<span data-ttu-id="436d2-243">La spécification d’un **chemin d’accès** dans la définition du jeu de données est facultative.</span><span class="sxs-lookup"><span data-stu-id="436d2-243">Specifying **path** in the dataset definition is optional.</span></span>

<span data-ttu-id="436d2-244">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="436d2-244">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="436d2-245">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="436d2-245">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="436d2-246">Le chemin d’accès du dossier pour l’objet blob est évalué dynamiquement en fonction de l’heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="436d2-246">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="436d2-247">Le chemin d'accès du dossier utilise l'année, le mois, le jour et l'heure de l'heure de début.</span><span class="sxs-lookup"><span data-stu-id="436d2-247">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobODataDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


<span data-ttu-id="436d2-248">**Activité de copie dans un pipeline avec une source OData et un récepteur d’objets blob :**</span><span class="sxs-lookup"><span data-stu-id="436d2-248">**Copy activity in a pipeline with OData source and Blob sink:**</span></span>

<span data-ttu-id="436d2-249">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="436d2-249">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="436d2-250">Dans la définition du pipeline JSON, le type **source** est défini sur **RelationalSource** et le type **sink** est défini sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="436d2-250">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="436d2-251">La requête SQL spécifiée pour la propriété **query** sélectionne les dernières (nouvelles) données de la source OData.</span><span class="sxs-lookup"><span data-stu-id="436d2-251">The SQL query specified for the **query** property selects the latest (newest) data from the OData source.</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "?$select=Name, Description&$top=5",
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "ODataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobODataDataSet"
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
                "name": "ODataToBlob"
            }
        ],
        "start": "2017-02-01T18:00:00Z",
        "end": "2017-02-03T19:00:00Z"
    }
}
```

<span data-ttu-id="436d2-252">La spécification de la **requête** dans la définition du pipeline est facultative.</span><span class="sxs-lookup"><span data-stu-id="436d2-252">Specifying **query** in the pipeline definition is optional.</span></span> <span data-ttu-id="436d2-253">L’ **URL** que le service Data Factory utilise pour récupérer les données est : URL spécifiée dans le service lié (obligatoire) + chemin d'accès spécifié dans le jeu de données (facultatif) + requête dans le pipeline (facultatif).</span><span class="sxs-lookup"><span data-stu-id="436d2-253">The **URL** that the Data Factory service uses to retrieve data is: URL specified in the linked service (required) + path specified in the dataset (optional) + query in the pipeline (optional).</span></span>


### <a name="type-mapping-for-odata"></a><span data-ttu-id="436d2-254">Mappage de type pour OData</span><span class="sxs-lookup"><span data-stu-id="436d2-254">Type mapping for OData</span></span>
<span data-ttu-id="436d2-255">Comme mentionné dans l’article consacré aux [activités de déplacement des données](data-factory-data-movement-activities.md) , l’activité de copie convertit automatiquement les types source en types récepteur à l’aide de l’approche en 2 étapes suivante :</span><span class="sxs-lookup"><span data-stu-id="436d2-255">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="436d2-256">Conversion de types natifs source en types .NET</span><span class="sxs-lookup"><span data-stu-id="436d2-256">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="436d2-257">Conversion à partir du type .NET en type de récepteur natif</span><span class="sxs-lookup"><span data-stu-id="436d2-257">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="436d2-258">Lorsque que déplacez des données à partir de magasins de données OData, les types de données OData sont mappés aux types .NET.</span><span class="sxs-lookup"><span data-stu-id="436d2-258">When moving data from OData data stores, OData data types are mapped to .NET types.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="436d2-259">Mapper les colonnes source aux colonnes du récepteur</span><span class="sxs-lookup"><span data-stu-id="436d2-259">Map source to sink columns</span></span>
<span data-ttu-id="436d2-260">Pour en savoir plus sur le mappage de colonnes du jeu de données source à des colonnes du jeu de données récepteur, voir [Mappage des colonnes d’un jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="436d2-260">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="436d2-261">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="436d2-261">Repeatable read from relational sources</span></span>
<span data-ttu-id="436d2-262">Lorsque vous copiez des données à partir de magasins de données relationnels, gardez à l’esprit la répétabilité de l’opération, afin d’éviter des résultats imprévus.</span><span class="sxs-lookup"><span data-stu-id="436d2-262">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="436d2-263">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="436d2-263">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="436d2-264">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="436d2-264">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="436d2-265">Lorsqu’une tranche est réexécutée d’une manière ou d’une autre, vous devez vous assurer que les mêmes données sont lues et ce, quel que soit le nombre d’exécutions de la tranche.</span><span class="sxs-lookup"><span data-stu-id="436d2-265">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="436d2-266">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="436d2-266">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="436d2-267">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="436d2-267">Performance and Tuning</span></span>
<span data-ttu-id="436d2-268">Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="436d2-268">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
