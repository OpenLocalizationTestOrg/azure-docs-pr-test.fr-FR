---
title: "Déplacer des données depuis Salesforce à l’aide de Data Factory | Microsoft Docs"
description: "Découvrez comment déplacer des données depuis Salesforce à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 9390b992bce2dede750c3fc55b7783a6b0db678f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a><span data-ttu-id="98a5f-103">Déplacer des données depuis Salesforce à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="98a5f-103">Move data from Salesforce by using Azure Data Factory</span></span>
<span data-ttu-id="98a5f-104">Cet article décrit la façon dont vous pouvez utiliser l’activité de copie dans Azure Data Factory pour copier des données depuis Salesforce vers n’importe quel magasin de données répertorié dans la colonne du récepteur du tableau [Sources et récepteurs pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) .</span><span class="sxs-lookup"><span data-stu-id="98a5f-104">This article outlines how you can use Copy Activity in an Azure data factory to copy data from Salesforce to any data store that is listed under the Sink column in the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="98a5f-105">Cet article s’appuie sur l’article des [activités de déplacement des données](data-factory-data-movement-activities.md) qui présente une vue d’ensemble du déplacement des données avec l’activité de copie et les combinaisons de magasins de données prises en charge.</span><span class="sxs-lookup"><span data-stu-id="98a5f-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

<span data-ttu-id="98a5f-106">Pour l’instant, Data Factory permet uniquement de déplacer des données de Salesforce vers des [magasins récepteurs pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats), mais il ne prend pas en charge le déplacement des données à partir d’autres magasins de données vers Salesforce.</span><span class="sxs-lookup"><span data-stu-id="98a5f-106">Azure Data Factory currently supports only moving data from Salesforce to [supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but does not support moving data from other data stores to Salesforce.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="98a5f-107">Versions prises en charge</span><span class="sxs-lookup"><span data-stu-id="98a5f-107">Supported versions</span></span>
<span data-ttu-id="98a5f-108">Ce connecteur prend en charge les éditions suivantes de Salesforce : Developer Edition, Professional Edition, Enterprise Edition et Unlimited Edition.</span><span class="sxs-lookup"><span data-stu-id="98a5f-108">This connector supports the following editions of Salesforce: Developer Edition, Professional Edition, Enterprise Edition, or Unlimited Edition.</span></span> <span data-ttu-id="98a5f-109">Et il prend en charge la copie de production Salesforce, bac à sable (sandbox) et domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="98a5f-109">And it supports copying from Salesforce production, sandbox and custom domain.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98a5f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="98a5f-110">Prerequisites</span></span>
* <span data-ttu-id="98a5f-111">L’autorisation d’API doit être activée.</span><span class="sxs-lookup"><span data-stu-id="98a5f-111">API permission must be enabled.</span></span> <span data-ttu-id="98a5f-112">Consultez l’article [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span><span class="sxs-lookup"><span data-stu-id="98a5f-112">See [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span></span>
* <span data-ttu-id="98a5f-113">Pour copier des données depuis Salesforce vers des magasins de données locaux, la passerelle de gestion des données version 2.0 doit être au moins installée dans votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="98a5f-113">To copy data from Salesforce to on-premises data stores, you must have at least Data Management Gateway 2.0 installed in your on-premises environment.</span></span>

## <a name="salesforce-request-limits"></a><span data-ttu-id="98a5f-114">Limites des requêtes Salesforce</span><span class="sxs-lookup"><span data-stu-id="98a5f-114">Salesforce request limits</span></span>
<span data-ttu-id="98a5f-115">Salesforce prend en charge un nombre limité de requêtes d’API totales et de requêtes d’API simultanées.</span><span class="sxs-lookup"><span data-stu-id="98a5f-115">Salesforce has limits for both total API requests and concurrent API requests.</span></span> <span data-ttu-id="98a5f-116">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="98a5f-116">Note the following points:</span></span>

- <span data-ttu-id="98a5f-117">Si le nombre de requêtes simultanées dépasse la limite autorisée, les nouvelles requêtes seront bloquées avec un risque de défaillances aléatoires.</span><span class="sxs-lookup"><span data-stu-id="98a5f-117">If the number of concurrent requests exceeds the limit, throttling occurs and you will see random failures.</span></span>
- <span data-ttu-id="98a5f-118">Si le nombre total de requêtes dépasse la limite autorisée, le compte Salesforce sera bloqué pendant 24 heures.</span><span class="sxs-lookup"><span data-stu-id="98a5f-118">If the total number of requests exceeds the limit, the Salesforce account will be blocked for 24 hours.</span></span>

<span data-ttu-id="98a5f-119">Vous pouvez également recevoir l’erreur « REQUEST_LIMIT_EXCEEDED » dans les deux scénarios.</span><span class="sxs-lookup"><span data-stu-id="98a5f-119">You might also receive the “REQUEST_LIMIT_EXCEEDED“ error in both scenarios.</span></span> <span data-ttu-id="98a5f-120">Pour plus de détails, consultez la section « API Request Limits » (Limites de requête d’API) du document [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) (Limites des développeurs Salesforce).</span><span class="sxs-lookup"><span data-stu-id="98a5f-120">See the "API Request Limits" section in the [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article for details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="98a5f-121">Prise en main</span><span class="sxs-lookup"><span data-stu-id="98a5f-121">Getting started</span></span>
<span data-ttu-id="98a5f-122">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données de Salesforce en utilisant différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="98a5f-122">You can create a pipeline with a copy activity that moves data from Salesforce by using different tools/APIs.</span></span>

<span data-ttu-id="98a5f-123">Le moyen le plus simple de créer un pipeline consiste à utiliser **l’Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="98a5f-123">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="98a5f-124">Consultez la page [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant Copier des données.</span><span class="sxs-lookup"><span data-stu-id="98a5f-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="98a5f-125">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="98a5f-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="98a5f-126">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="98a5f-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="98a5f-127">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="98a5f-127">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="98a5f-128">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="98a5f-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="98a5f-129">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="98a5f-129">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="98a5f-130">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="98a5f-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="98a5f-131">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="98a5f-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="98a5f-132">Lorsque vous utilisez des outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory au format JSON.</span><span class="sxs-lookup"><span data-stu-id="98a5f-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="98a5f-133">Pour consulter un exemple contenant des définitions JSON des entités Data Factory utilisées pour copier des données de Salesforce, consultez la section [Exemple JSON : copier des données de Salesforce vers Blob Azure](#json-example-copy-data-from-salesforce-to-azure-blob) de cet article.</span><span class="sxs-lookup"><span data-stu-id="98a5f-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from Salesforce, see [JSON example: Copy data from Salesforce to Azure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="98a5f-134">Les sections suivantes fournissent des informations sur les propriétés JSON utilisées pour définir les entités Data Factory spécifiques à Salesforce :</span><span class="sxs-lookup"><span data-stu-id="98a5f-134">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Salesforce:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="98a5f-135">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="98a5f-135">Linked service properties</span></span>
<span data-ttu-id="98a5f-136">Le tableau suivant décrit les éléments JSON spécifiques au service lié Salesforce.</span><span class="sxs-lookup"><span data-stu-id="98a5f-136">The following table provides descriptions for JSON elements that are specific to the Salesforce linked service.</span></span>

| <span data-ttu-id="98a5f-137">Propriété</span><span class="sxs-lookup"><span data-stu-id="98a5f-137">Property</span></span> | <span data-ttu-id="98a5f-138">Description</span><span class="sxs-lookup"><span data-stu-id="98a5f-138">Description</span></span> | <span data-ttu-id="98a5f-139">Requis</span><span class="sxs-lookup"><span data-stu-id="98a5f-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98a5f-140">type</span><span class="sxs-lookup"><span data-stu-id="98a5f-140">type</span></span> |<span data-ttu-id="98a5f-141">La propriété de type doit être définie sur **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="98a5f-141">The type property must be set to: **Salesforce**.</span></span> |<span data-ttu-id="98a5f-142">Oui</span><span class="sxs-lookup"><span data-stu-id="98a5f-142">Yes</span></span> |
| <span data-ttu-id="98a5f-143">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="98a5f-143">environmentUrl</span></span> | <span data-ttu-id="98a5f-144">Spécifiez l’URL de l’instance Salesforce.</span><span class="sxs-lookup"><span data-stu-id="98a5f-144">Specify the URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="98a5f-145">- L’URL par défaut est « https://login.salesforce.com ».</span><span class="sxs-lookup"><span data-stu-id="98a5f-145">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="98a5f-146">- Pour copier des données à partir du bac à sable (sandbox), spécifiez « https://test.salesforce.com ».</span><span class="sxs-lookup"><span data-stu-id="98a5f-146">- To copy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="98a5f-147">- Pour copier des données du domaine personnalisé, spécifiez, par exemple : « https://[domain].my.salesforce.com ».</span><span class="sxs-lookup"><span data-stu-id="98a5f-147">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="98a5f-148">Non</span><span class="sxs-lookup"><span data-stu-id="98a5f-148">No</span></span> |
| <span data-ttu-id="98a5f-149">username</span><span class="sxs-lookup"><span data-stu-id="98a5f-149">username</span></span> |<span data-ttu-id="98a5f-150">Spécifiez un nom d’utilisateur pour le compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="98a5f-150">Specify a user name for the user account.</span></span> |<span data-ttu-id="98a5f-151">Oui</span><span class="sxs-lookup"><span data-stu-id="98a5f-151">Yes</span></span> |
| <span data-ttu-id="98a5f-152">password</span><span class="sxs-lookup"><span data-stu-id="98a5f-152">password</span></span> |<span data-ttu-id="98a5f-153">Spécifiez le mot de passe du compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="98a5f-153">Specify a password for the user account.</span></span> |<span data-ttu-id="98a5f-154">Oui</span><span class="sxs-lookup"><span data-stu-id="98a5f-154">Yes</span></span> |
| <span data-ttu-id="98a5f-155">securityToken</span><span class="sxs-lookup"><span data-stu-id="98a5f-155">securityToken</span></span> |<span data-ttu-id="98a5f-156">Spécifiez le jeton de sécurité du compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="98a5f-156">Specify a security token for the user account.</span></span> <span data-ttu-id="98a5f-157">Consultez l’article [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) (Obtenir un jeton de sécurité) pour obtenir des instructions sur la réinitialisation et l’obtention d’un jeton de sécurité.</span><span class="sxs-lookup"><span data-stu-id="98a5f-157">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span></span> <span data-ttu-id="98a5f-158">Pour en savoir plus sur les jetons de sécurité, consultez l’article [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm)(Sécurité et API).</span><span class="sxs-lookup"><span data-stu-id="98a5f-158">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="98a5f-159">Oui</span><span class="sxs-lookup"><span data-stu-id="98a5f-159">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="98a5f-160">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="98a5f-160">Dataset properties</span></span>
<span data-ttu-id="98a5f-161">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md) .</span><span class="sxs-lookup"><span data-stu-id="98a5f-161">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="98a5f-162">Les sections comme la structure, la disponibilité et la stratégie d’un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="98a5f-162">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, and so on).</span></span>

<span data-ttu-id="98a5f-163">La section **typeProperties** est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="98a5f-163">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="98a5f-164">La section typeProperties pour le jeu de données de type **RelationalTable** comprend les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="98a5f-164">The typeProperties section for a dataset of the type **RelationalTable** has the following properties:</span></span>

| <span data-ttu-id="98a5f-165">Propriété</span><span class="sxs-lookup"><span data-stu-id="98a5f-165">Property</span></span> | <span data-ttu-id="98a5f-166">Description</span><span class="sxs-lookup"><span data-stu-id="98a5f-166">Description</span></span> | <span data-ttu-id="98a5f-167">Requis</span><span class="sxs-lookup"><span data-stu-id="98a5f-167">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98a5f-168">TableName</span><span class="sxs-lookup"><span data-stu-id="98a5f-168">tableName</span></span> |<span data-ttu-id="98a5f-169">Nom de la table dans Salesforce.</span><span class="sxs-lookup"><span data-stu-id="98a5f-169">Name of the table in Salesforce.</span></span> |<span data-ttu-id="98a5f-170">Non (si une **requête** de type **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="98a5f-170">No (if a **query** of **RelationalSource** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="98a5f-171">La partie « __c » du nom de l’API est requise pour tout objet personnalisé.</span><span class="sxs-lookup"><span data-stu-id="98a5f-171">The "__c" part of the API Name is needed for any custom object.</span></span>

![Connexion Salesforce - Data Factory - Nom de l’API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a><span data-ttu-id="98a5f-173">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="98a5f-173">Copy activity properties</span></span>
<span data-ttu-id="98a5f-174">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="98a5f-174">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="98a5f-175">Les propriétés telles que le nom, la description, les tables d’entrée et de sortie, les différentes stratégies, etc. sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="98a5f-175">Properties like name, description, input and output tables, and various policies are available for all types of activities.</span></span>

<span data-ttu-id="98a5f-176">En revanche, les propriétés qui sont disponibles dans la section typeProperties de l’activité varient pour chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="98a5f-176">The properties that are available in the typeProperties section of the activity, on the other hand, vary with each activity type.</span></span> <span data-ttu-id="98a5f-177">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="98a5f-177">For Copy Activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="98a5f-178">Dans l’activité de copie, lorsque la source est de type **RelationalSource** (qui inclut Salesforce), les propriétés suivantes sont disponibles dans la section typeProperties :</span><span class="sxs-lookup"><span data-stu-id="98a5f-178">In copy activity, when the source is of the type **RelationalSource** (which includes Salesforce), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="98a5f-179">Propriété</span><span class="sxs-lookup"><span data-stu-id="98a5f-179">Property</span></span> | <span data-ttu-id="98a5f-180">Description</span><span class="sxs-lookup"><span data-stu-id="98a5f-180">Description</span></span> | <span data-ttu-id="98a5f-181">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="98a5f-181">Allowed values</span></span> | <span data-ttu-id="98a5f-182">Requis</span><span class="sxs-lookup"><span data-stu-id="98a5f-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98a5f-183">query</span><span class="sxs-lookup"><span data-stu-id="98a5f-183">query</span></span> |<span data-ttu-id="98a5f-184">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="98a5f-184">Use the custom query to read data.</span></span> |<span data-ttu-id="98a5f-185">Une requête SQL-92 ou une requête [SOQL (Salesforce Object Query Language)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm).</span><span class="sxs-lookup"><span data-stu-id="98a5f-185">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="98a5f-186">Par exemple : `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="98a5f-186">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="98a5f-187">Non (si l’attribut **tableName** de l’élément **dataset** est spécifié)</span><span class="sxs-lookup"><span data-stu-id="98a5f-187">No (if the **tableName** of the **dataset** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="98a5f-188">La partie « __c » du nom de l’API est requise pour tout objet personnalisé.</span><span class="sxs-lookup"><span data-stu-id="98a5f-188">The "__c" part of the API Name is needed for any custom object.</span></span>

![Connexion Salesforce - Data Factory - Nom de l’API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a><span data-ttu-id="98a5f-190">Conseils pour les requêtes</span><span class="sxs-lookup"><span data-stu-id="98a5f-190">Query tips</span></span>
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a><span data-ttu-id="98a5f-191">Récupération de données à l’aide de la clause where sur la colonne DateTime</span><span class="sxs-lookup"><span data-stu-id="98a5f-191">Retrieving data using where clause on DateTime column</span></span>
<span data-ttu-id="98a5f-192">Lorsque vous spécifiez une requête SOQL ou SQL, faites attention à la différence de format DateTime.</span><span class="sxs-lookup"><span data-stu-id="98a5f-192">When specify the SOQL or SQL query, pay attention to the DateTime format difference.</span></span> <span data-ttu-id="98a5f-193">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="98a5f-193">For example:</span></span>

* <span data-ttu-id="98a5f-194">**Exemple SOQL** : `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="98a5f-194">**SOQL sample**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span></span>
* <span data-ttu-id="98a5f-195">**Exemple SQL** :</span><span class="sxs-lookup"><span data-stu-id="98a5f-195">**SQL sample**:</span></span>
    * <span data-ttu-id="98a5f-196">**Utilisation de l’Assistant de copie pour spécifier la requête :**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="98a5f-196">**Using copy wizard to specify the query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span></span>
    * <span data-ttu-id="98a5f-197">**Utilisation de la modification JSON pour spécifier la requête (caractère d’échappement correct) :**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="98a5f-197">**Using JSON editing to specify the query (escape char properly):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span></span>

### <a name="retrieving-data-from-salesforce-report"></a><span data-ttu-id="98a5f-198">Récupération de données à partir d’un rapport Salesforce</span><span class="sxs-lookup"><span data-stu-id="98a5f-198">Retrieving data from Salesforce Report</span></span>
<span data-ttu-id="98a5f-199">Vous pouvez récupérer des données à partir de rapports Salesforce en spécifiant la requête en tant que `{call "<report name>"}`, par exemple.</span><span class="sxs-lookup"><span data-stu-id="98a5f-199">You can retrieve data from Salesforce reports by specifying query as `{call "<report name>"}`,for example,.</span></span> <span data-ttu-id="98a5f-200">`"query": "{call \"TestReport\"}"`.</span><span class="sxs-lookup"><span data-stu-id="98a5f-200">`"query": "{call \"TestReport\"}"`.</span></span>

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a><span data-ttu-id="98a5f-201">Récupération d’enregistrements supprimés dans la Corbeille Salesforce</span><span class="sxs-lookup"><span data-stu-id="98a5f-201">Retrieving deleted records from Salesforce Recycle Bin</span></span>
<span data-ttu-id="98a5f-202">Pour interroger les enregistrements supprimés de manière réversible dans la Corbeille Salesforce, vous pouvez spécifier **« IsDeleted = 1 »** dans votre requête.</span><span class="sxs-lookup"><span data-stu-id="98a5f-202">To query the soft deleted records from Salesforce Recycle Bin, you can specify **"IsDeleted = 1"** in your query.</span></span> <span data-ttu-id="98a5f-203">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="98a5f-203">For example,</span></span>

* <span data-ttu-id="98a5f-204">Pour interroger uniquement les enregistrements supprimés, spécifiez « select * from MyTable__c **where IsDeleted= 1** »</span><span class="sxs-lookup"><span data-stu-id="98a5f-204">To query only the deleted records, specify "select * from MyTable__c **where IsDeleted= 1**"</span></span>
* <span data-ttu-id="98a5f-205">Pour interroger tous les enregistrements, notamment ceux existants et supprimés, spécifiez « select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1** »</span><span class="sxs-lookup"><span data-stu-id="98a5f-205">To query all the records including the existing and the deleted, specify "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span></span>

## <a name="json-example-copy-data-from-salesforce-to-azure-blob"></a><span data-ttu-id="98a5f-206">Exemple JSON : copie de données de Salesforce vers Azure Blob</span><span class="sxs-lookup"><span data-stu-id="98a5f-206">JSON example: Copy data from Salesforce to Azure Blob</span></span>
<span data-ttu-id="98a5f-207">L’exemple suivant présente des exemples de définitions de JSON que vous pouvez utiliser pour créer un pipeline à l’aide du [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), de [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [d’Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="98a5f-207">The following example provides sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="98a5f-208">Ils indiquent comment copier des données depuis Salesforce vers Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="98a5f-208">They show how to copy data from Salesforce to Azure Blob Storage.</span></span> <span data-ttu-id="98a5f-209">Toutefois, les données peuvent être copiées vers l’un des récepteurs indiqués [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) , via l’activité de copie d’Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="98a5f-209">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="98a5f-210">Voici les artefacts Data Factory dont vous aurez besoin pour implémenter le scénario.</span><span class="sxs-lookup"><span data-stu-id="98a5f-210">Here are the Data Factory artifacts that you'll need to create to implement the scenario.</span></span> <span data-ttu-id="98a5f-211">Les sections qui suivent la liste fournissent des informations supplémentaires sur ces étapes.</span><span class="sxs-lookup"><span data-stu-id="98a5f-211">The sections that follow the list provide details about these steps.</span></span>

* <span data-ttu-id="98a5f-212">Un service lié de type [Salesforce](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="98a5f-212">A linked service of the type [Salesforce](#linked-service-properties)</span></span>
* <span data-ttu-id="98a5f-213">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="98a5f-213">A linked service of the type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="98a5f-214">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="98a5f-214">An input [dataset](data-factory-create-datasets.md) of the type [RelationalTable](#dataset-properties)</span></span>
* <span data-ttu-id="98a5f-215">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="98a5f-215">An output [dataset](data-factory-create-datasets.md) of the type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="98a5f-216">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [RelationalSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="98a5f-216">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="98a5f-217">**Service lié Salesforce**</span><span class="sxs-lookup"><span data-stu-id="98a5f-217">**Salesforce linked service**</span></span>

<span data-ttu-id="98a5f-218">Cet exemple utilise le service lié **Salesforce** .</span><span class="sxs-lookup"><span data-stu-id="98a5f-218">This example uses the **Salesforce** linked service.</span></span> <span data-ttu-id="98a5f-219">Consultez la section [Service lié Salesforce](#linked-service-properties) pour connaître les propriétés prises en charge par ce service lié.</span><span class="sxs-lookup"><span data-stu-id="98a5f-219">See the [Salesforce linked service](#linked-service-properties) section for the properties that are supported by this linked service.</span></span>  <span data-ttu-id="98a5f-220">Consultez l’article [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) (Obtenir un jeton de sécurité) pour obtenir des instructions sur la réinitialisation et l’obtention du jeton de sécurité.</span><span class="sxs-lookup"><span data-stu-id="98a5f-220">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get the security token.</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```
<span data-ttu-id="98a5f-221">**Service lié Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="98a5f-221">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="98a5f-222">**Jeu de données d’entrée Salesforce**</span><span class="sxs-lookup"><span data-stu-id="98a5f-222">**Salesforce input dataset**</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"  
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

<span data-ttu-id="98a5f-223">La définition de **external** sur **true** informe le service Data Factory qu’il s’agit d’un jeu de données qui est externe à la Data Factory et non produit par une activité dans la Data Factory.</span><span class="sxs-lookup"><span data-stu-id="98a5f-223">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98a5f-224">La partie « __c » du nom de l’API est requise pour tout objet personnalisé.</span><span class="sxs-lookup"><span data-stu-id="98a5f-224">The "__c" part of the API Name is needed for any custom object.</span></span>

![Connexion Salesforce - Data Factory - Nom de l’API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

<span data-ttu-id="98a5f-226">**Jeu de données de sortie d’objet Blob Azure**</span><span class="sxs-lookup"><span data-stu-id="98a5f-226">**Azure blob output dataset**</span></span>

<span data-ttu-id="98a5f-227">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="98a5f-227">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/alltypes_c"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="98a5f-228">**Pipeline avec activité de copie**</span><span class="sxs-lookup"><span data-stu-id="98a5f-228">**Pipeline with Copy Activity**</span></span>

<span data-ttu-id="98a5f-229">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d’entrée et de sortie, et qui est planifiée pour s’exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="98a5f-229">The pipeline contains Copy Activity, which is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="98a5f-230">Dans la définition du pipeline JSON, le type **source** est défini sur **RelationalSource** et le type **sink** est défini sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="98a5f-230">In the pipeline JSON definition, the **source** type is set to **RelationalSource**, and the **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="98a5f-231">Pour obtenir la liste des propriétés prises en charge par RelationalSource, voir [Propriétés de type RelationalSource](#copy-activity-properties) .</span><span class="sxs-lookup"><span data-stu-id="98a5f-231">See [RelationalSource type properties](#copy-activity-properties) for the list of properties that are supported by the RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce to an Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"                
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
> [!IMPORTANT]
> <span data-ttu-id="98a5f-232">La partie « __c » du nom de l’API est requise pour tout objet personnalisé.</span><span class="sxs-lookup"><span data-stu-id="98a5f-232">The "__c" part of the API Name is needed for any custom object.</span></span>

![Connexion Salesforce - Data Factory - Nom de l’API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a><span data-ttu-id="98a5f-234">Mappage de type pour Salesforce</span><span class="sxs-lookup"><span data-stu-id="98a5f-234">Type mapping for Salesforce</span></span>
| <span data-ttu-id="98a5f-235">Type Salesforce</span><span class="sxs-lookup"><span data-stu-id="98a5f-235">Salesforce type</span></span> | <span data-ttu-id="98a5f-236">Type basé sur .NET</span><span class="sxs-lookup"><span data-stu-id="98a5f-236">.NET-based type</span></span> |
| --- | --- |
| <span data-ttu-id="98a5f-237">Numérotation automatique</span><span class="sxs-lookup"><span data-stu-id="98a5f-237">Auto Number</span></span> |<span data-ttu-id="98a5f-238">String</span><span class="sxs-lookup"><span data-stu-id="98a5f-238">String</span></span> |
| <span data-ttu-id="98a5f-239">Case à cocher</span><span class="sxs-lookup"><span data-stu-id="98a5f-239">Checkbox</span></span> |<span data-ttu-id="98a5f-240">Boolean</span><span class="sxs-lookup"><span data-stu-id="98a5f-240">Boolean</span></span> |
| <span data-ttu-id="98a5f-241">Devise</span><span class="sxs-lookup"><span data-stu-id="98a5f-241">Currency</span></span> |<span data-ttu-id="98a5f-242">Double</span><span class="sxs-lookup"><span data-stu-id="98a5f-242">Double</span></span> |
| <span data-ttu-id="98a5f-243">Date</span><span class="sxs-lookup"><span data-stu-id="98a5f-243">Date</span></span> |<span data-ttu-id="98a5f-244">DateTime</span><span class="sxs-lookup"><span data-stu-id="98a5f-244">DateTime</span></span> |
| <span data-ttu-id="98a5f-245">Date/Heure</span><span class="sxs-lookup"><span data-stu-id="98a5f-245">Date/Time</span></span> |<span data-ttu-id="98a5f-246">DateTime</span><span class="sxs-lookup"><span data-stu-id="98a5f-246">DateTime</span></span> |
| <span data-ttu-id="98a5f-247">Email</span><span class="sxs-lookup"><span data-stu-id="98a5f-247">Email</span></span> |<span data-ttu-id="98a5f-248">String</span><span class="sxs-lookup"><span data-stu-id="98a5f-248">String</span></span> |
| <span data-ttu-id="98a5f-249">ID</span><span class="sxs-lookup"><span data-stu-id="98a5f-249">Id</span></span> |<span data-ttu-id="98a5f-250">String</span><span class="sxs-lookup"><span data-stu-id="98a5f-250">String</span></span> |
| <span data-ttu-id="98a5f-251">Relation de recherche</span><span class="sxs-lookup"><span data-stu-id="98a5f-251">Lookup Relationship</span></span> |<span data-ttu-id="98a5f-252">String</span><span class="sxs-lookup"><span data-stu-id="98a5f-252">String</span></span> |
| <span data-ttu-id="98a5f-253">Liste déroulante à sélection multiple</span><span class="sxs-lookup"><span data-stu-id="98a5f-253">Multi-Select Picklist</span></span> |<span data-ttu-id="98a5f-254">String</span><span class="sxs-lookup"><span data-stu-id="98a5f-254">String</span></span> |
| <span data-ttu-id="98a5f-255">Number</span><span class="sxs-lookup"><span data-stu-id="98a5f-255">Number</span></span> |<span data-ttu-id="98a5f-256">Double</span><span class="sxs-lookup"><span data-stu-id="98a5f-256">Double</span></span> |
| <span data-ttu-id="98a5f-257">Pourcentage</span><span class="sxs-lookup"><span data-stu-id="98a5f-257">Percent</span></span> |<span data-ttu-id="98a5f-258">Double</span><span class="sxs-lookup"><span data-stu-id="98a5f-258">Double</span></span> |
| <span data-ttu-id="98a5f-259">Téléphone</span><span class="sxs-lookup"><span data-stu-id="98a5f-259">Phone</span></span> |<span data-ttu-id="98a5f-260">String</span><span class="sxs-lookup"><span data-stu-id="98a5f-260">String</span></span> |
| <span data-ttu-id="98a5f-261">Liste déroulante</span><span class="sxs-lookup"><span data-stu-id="98a5f-261">Picklist</span></span> |<span data-ttu-id="98a5f-262">String</span><span class="sxs-lookup"><span data-stu-id="98a5f-262">String</span></span> |
| <span data-ttu-id="98a5f-263">Texte</span><span class="sxs-lookup"><span data-stu-id="98a5f-263">Text</span></span> |<span data-ttu-id="98a5f-264">String</span><span class="sxs-lookup"><span data-stu-id="98a5f-264">String</span></span> |
| <span data-ttu-id="98a5f-265">Zone de texte</span><span class="sxs-lookup"><span data-stu-id="98a5f-265">Text Area</span></span> |<span data-ttu-id="98a5f-266">String</span><span class="sxs-lookup"><span data-stu-id="98a5f-266">String</span></span> |
| <span data-ttu-id="98a5f-267">Zone de texte (long)</span><span class="sxs-lookup"><span data-stu-id="98a5f-267">Text Area (Long)</span></span> |<span data-ttu-id="98a5f-268">String</span><span class="sxs-lookup"><span data-stu-id="98a5f-268">String</span></span> |
| <span data-ttu-id="98a5f-269">Zone de texte (enrichi)</span><span class="sxs-lookup"><span data-stu-id="98a5f-269">Text Area (Rich)</span></span> |<span data-ttu-id="98a5f-270">String</span><span class="sxs-lookup"><span data-stu-id="98a5f-270">String</span></span> |
| <span data-ttu-id="98a5f-271">Texte (chiffré)</span><span class="sxs-lookup"><span data-stu-id="98a5f-271">Text (Encrypted)</span></span> |<span data-ttu-id="98a5f-272">String</span><span class="sxs-lookup"><span data-stu-id="98a5f-272">String</span></span> |
| <span data-ttu-id="98a5f-273">URL</span><span class="sxs-lookup"><span data-stu-id="98a5f-273">URL</span></span> |<span data-ttu-id="98a5f-274">String</span><span class="sxs-lookup"><span data-stu-id="98a5f-274">String</span></span> |

> [!NOTE]
> <span data-ttu-id="98a5f-275">Pour savoir comment mapper des colonnes d’un jeu de données source à des colonnes d’un jeu de données récepteur, voir [Mappage des colonnes d’un jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="98a5f-275">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a><span data-ttu-id="98a5f-276">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="98a5f-276">Performance and tuning</span></span>
<span data-ttu-id="98a5f-277">Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="98a5f-277">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
