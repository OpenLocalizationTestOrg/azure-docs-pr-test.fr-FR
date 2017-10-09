---
title: "aaaMove des données à partir de la force de vente à l’aide de Data Factory | Documents Microsoft"
description: "En savoir plus sur la façon de toomove les données à partir de la force de vente à l’aide d’Azure Data Factory."
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
ms.openlocfilehash: c1bde2a333f5a3c0a995eb8c13ecf585132888b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a><span data-ttu-id="78c00-103">Déplacer des données depuis Salesforce à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="78c00-103">Move data from Salesforce by using Azure Data Factory</span></span>
<span data-ttu-id="78c00-104">Cet article décrit comment vous pouvez utiliser l’activité de copie dans un Azure data factory toocopy données Salesforce tooany magasin de données qui est répertorié sous la colonne de récepteur hello Bonjour [prise en charge des sources et récepteurs](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="78c00-104">This article outlines how you can use Copy Activity in an Azure data factory toocopy data from Salesforce tooany data store that is listed under hello Sink column in hello [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="78c00-105">Cet article s’appuie sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie et de combinaisons de magasin de données pris en charge.</span><span class="sxs-lookup"><span data-stu-id="78c00-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

<span data-ttu-id="78c00-106">Azure Data Factory prend actuellement en charge uniquement le déplacement des données à partir de Salesforce trop[prise en charge des magasins de données récepteur](data-factory-data-movement-activities.md#supported-data-stores-and-formats), mais ne prend pas en charge le déplacement des données d’autres tooSalesforce de magasins de données.</span><span class="sxs-lookup"><span data-stu-id="78c00-106">Azure Data Factory currently supports only moving data from Salesforce too[supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but does not support moving data from other data stores tooSalesforce.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="78c00-107">Versions prises en charge</span><span class="sxs-lookup"><span data-stu-id="78c00-107">Supported versions</span></span>
<span data-ttu-id="78c00-108">Ce connecteur prend en charge hello suivant des éditions de Salesforce : Developer Edition, Professional Edition, Enterprise Edition ou illimité Edition.</span><span class="sxs-lookup"><span data-stu-id="78c00-108">This connector supports hello following editions of Salesforce: Developer Edition, Professional Edition, Enterprise Edition, or Unlimited Edition.</span></span> <span data-ttu-id="78c00-109">Et il prend en charge la copie de production Salesforce, bac à sable (sandbox) et domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="78c00-109">And it supports copying from Salesforce production, sandbox and custom domain.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78c00-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="78c00-110">Prerequisites</span></span>
* <span data-ttu-id="78c00-111">L’autorisation d’API doit être activée.</span><span class="sxs-lookup"><span data-stu-id="78c00-111">API permission must be enabled.</span></span> <span data-ttu-id="78c00-112">Consultez l’article [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span><span class="sxs-lookup"><span data-stu-id="78c00-112">See [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span></span>
* <span data-ttu-id="78c00-113">toocopy des données à partir des magasins de données Salesforce tooon local, vous devez disposer au moins données Management Gateway 2.0 est installé dans votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="78c00-113">toocopy data from Salesforce tooon-premises data stores, you must have at least Data Management Gateway 2.0 installed in your on-premises environment.</span></span>

## <a name="salesforce-request-limits"></a><span data-ttu-id="78c00-114">Limites des requêtes Salesforce</span><span class="sxs-lookup"><span data-stu-id="78c00-114">Salesforce request limits</span></span>
<span data-ttu-id="78c00-115">Salesforce prend en charge un nombre limité de requêtes d’API totales et de requêtes d’API simultanées.</span><span class="sxs-lookup"><span data-stu-id="78c00-115">Salesforce has limits for both total API requests and concurrent API requests.</span></span> <span data-ttu-id="78c00-116">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="78c00-116">Note hello following points:</span></span>

- <span data-ttu-id="78c00-117">Si le nombre de hello de demandes simultanées dépasse la limite de hello, la limitation se produit et vous verrez des échecs aléatoires.</span><span class="sxs-lookup"><span data-stu-id="78c00-117">If hello number of concurrent requests exceeds hello limit, throttling occurs and you will see random failures.</span></span>
- <span data-ttu-id="78c00-118">Si le nombre total de hello de demandes dépasse la limite de hello, hello compte Salesforce sera bloqué pour 24 heures.</span><span class="sxs-lookup"><span data-stu-id="78c00-118">If hello total number of requests exceeds hello limit, hello Salesforce account will be blocked for 24 hours.</span></span>

<span data-ttu-id="78c00-119">Vous pouvez aussi recevoir l’erreur de « REQUEST_LIMIT_EXCEEDED » hello dans les deux scénarios.</span><span class="sxs-lookup"><span data-stu-id="78c00-119">You might also receive hello “REQUEST_LIMIT_EXCEEDED“ error in both scenarios.</span></span> <span data-ttu-id="78c00-120">Consultez la section hello « API limites des demandes » hello [limites de développeur Salesforce](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="78c00-120">See hello "API Request Limits" section in hello [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article for details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="78c00-121">Prise en main</span><span class="sxs-lookup"><span data-stu-id="78c00-121">Getting started</span></span>
<span data-ttu-id="78c00-122">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données de Salesforce en utilisant différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="78c00-122">You can create a pipeline with a copy activity that moves data from Salesforce by using different tools/APIs.</span></span>

<span data-ttu-id="78c00-123">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="78c00-123">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="78c00-124">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="78c00-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="78c00-125">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="78c00-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="78c00-126">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="78c00-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="78c00-127">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="78c00-127">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="78c00-128">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="78c00-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="78c00-129">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="78c00-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="78c00-130">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="78c00-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="78c00-131">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="78c00-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="78c00-132">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="78c00-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="78c00-133">Pour voir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont utilisés toocopy des données à partir de Salesforce, [exemple de JSON : copier des données à partir de Salesforce tooAzure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="78c00-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from Salesforce, see [JSON example: Copy data from Salesforce tooAzure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="78c00-134">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifique tooSalesforce :</span><span class="sxs-lookup"><span data-stu-id="78c00-134">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooSalesforce:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="78c00-135">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="78c00-135">Linked service properties</span></span>
<span data-ttu-id="78c00-136">Hello tableau suivant fournit des descriptions pour les éléments JSON toohello spécifique au service lié de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="78c00-136">hello following table provides descriptions for JSON elements that are specific toohello Salesforce linked service.</span></span>

| <span data-ttu-id="78c00-137">Propriété</span><span class="sxs-lookup"><span data-stu-id="78c00-137">Property</span></span> | <span data-ttu-id="78c00-138">Description</span><span class="sxs-lookup"><span data-stu-id="78c00-138">Description</span></span> | <span data-ttu-id="78c00-139">Requis</span><span class="sxs-lookup"><span data-stu-id="78c00-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="78c00-140">type</span><span class="sxs-lookup"><span data-stu-id="78c00-140">type</span></span> |<span data-ttu-id="78c00-141">propriété de type Hello doit indiquer : **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="78c00-141">hello type property must be set to: **Salesforce**.</span></span> |<span data-ttu-id="78c00-142">Oui</span><span class="sxs-lookup"><span data-stu-id="78c00-142">Yes</span></span> |
| <span data-ttu-id="78c00-143">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="78c00-143">environmentUrl</span></span> | <span data-ttu-id="78c00-144">Spécifier l’instance d’URL de la force de vente hello.</span><span class="sxs-lookup"><span data-stu-id="78c00-144">Specify hello URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="78c00-145">- L’URL par défaut est « https://login.salesforce.com ».</span><span class="sxs-lookup"><span data-stu-id="78c00-145">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="78c00-146">-toocopy des données à partir de bac à sable, spécifiez « https://test.salesforce.com ».</span><span class="sxs-lookup"><span data-stu-id="78c00-146">- toocopy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="78c00-147">-toocopy des données à partir d’un domaine personnalisé, spécifiez, par exemple, « https://[domain].my.salesforce.com ».</span><span class="sxs-lookup"><span data-stu-id="78c00-147">- toocopy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="78c00-148">Non</span><span class="sxs-lookup"><span data-stu-id="78c00-148">No</span></span> |
| <span data-ttu-id="78c00-149">username</span><span class="sxs-lookup"><span data-stu-id="78c00-149">username</span></span> |<span data-ttu-id="78c00-150">Spécifiez un nom d’utilisateur pour le compte d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="78c00-150">Specify a user name for hello user account.</span></span> |<span data-ttu-id="78c00-151">Oui</span><span class="sxs-lookup"><span data-stu-id="78c00-151">Yes</span></span> |
| <span data-ttu-id="78c00-152">password</span><span class="sxs-lookup"><span data-stu-id="78c00-152">password</span></span> |<span data-ttu-id="78c00-153">Spécifiez un mot de passe pour le compte d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="78c00-153">Specify a password for hello user account.</span></span> |<span data-ttu-id="78c00-154">Oui</span><span class="sxs-lookup"><span data-stu-id="78c00-154">Yes</span></span> |
| <span data-ttu-id="78c00-155">securityToken</span><span class="sxs-lookup"><span data-stu-id="78c00-155">securityToken</span></span> |<span data-ttu-id="78c00-156">Spécifier un jeton de sécurité pour le compte d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="78c00-156">Specify a security token for hello user account.</span></span> <span data-ttu-id="78c00-157">Consultez [obtenir jeton de sécurité](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) pour obtenir des instructions sur la façon de tooreset/obtenir un jeton de sécurité.</span><span class="sxs-lookup"><span data-stu-id="78c00-157">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get a security token.</span></span> <span data-ttu-id="78c00-158">toolearn sur les jetons de sécurité en général, consultez [API de sécurité et hello](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="78c00-158">toolearn about security tokens in general, see [Security and hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="78c00-159">Oui</span><span class="sxs-lookup"><span data-stu-id="78c00-159">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="78c00-160">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="78c00-160">Dataset properties</span></span>
<span data-ttu-id="78c00-161">Pour obtenir une liste complète des sections et les propriétés qui sont disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="78c00-161">For a full list of sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="78c00-162">Les sections comme la structure, la disponibilité et la stratégie d’un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="78c00-162">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, and so on).</span></span>

<span data-ttu-id="78c00-163">Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="78c00-163">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="78c00-164">Hello typeProperties section pour un jeu de données de type de hello **RelationalTable** a hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="78c00-164">hello typeProperties section for a dataset of hello type **RelationalTable** has hello following properties:</span></span>

| <span data-ttu-id="78c00-165">Propriété</span><span class="sxs-lookup"><span data-stu-id="78c00-165">Property</span></span> | <span data-ttu-id="78c00-166">Description</span><span class="sxs-lookup"><span data-stu-id="78c00-166">Description</span></span> | <span data-ttu-id="78c00-167">Requis</span><span class="sxs-lookup"><span data-stu-id="78c00-167">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="78c00-168">TableName</span><span class="sxs-lookup"><span data-stu-id="78c00-168">tableName</span></span> |<span data-ttu-id="78c00-169">Nom de table hello dans Salesforce.</span><span class="sxs-lookup"><span data-stu-id="78c00-169">Name of hello table in Salesforce.</span></span> |<span data-ttu-id="78c00-170">Non (si une **requête** de type **RelationalSource** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="78c00-170">No (if a **query** of **RelationalSource** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="78c00-171">Hello « __c » partie hello nom de l’API est nécessaire pour tout objet personnalisé.</span><span class="sxs-lookup"><span data-stu-id="78c00-171">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Connexion Salesforce - Data Factory - Nom de l’API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a><span data-ttu-id="78c00-173">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="78c00-173">Copy activity properties</span></span>
<span data-ttu-id="78c00-174">Pour obtenir une liste complète des sections et des propriétés qui sont disponibles pour la définition d’activités, consultez hello [création de pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="78c00-174">For a full list of sections and properties that are available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="78c00-175">Les propriétés telles que le nom, la description, les tables d’entrée et de sortie, les différentes stratégies, etc. sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="78c00-175">Properties like name, description, input and output tables, and various policies are available for all types of activities.</span></span>

<span data-ttu-id="78c00-176">propriétés de Hello qui sont disponibles dans hello section typeProperties d’activité hello sur hello autre part, varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="78c00-176">hello properties that are available in hello typeProperties section of hello activity, on hello other hand, vary with each activity type.</span></span> <span data-ttu-id="78c00-177">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="78c00-177">For Copy Activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="78c00-178">Dans l’activité de copie, lors de la source de hello est de type de hello **RelationalSource** (qui inclut Salesforce), hello propriétés suivantes est disponible dans la section de typeProperties :</span><span class="sxs-lookup"><span data-stu-id="78c00-178">In copy activity, when hello source is of hello type **RelationalSource** (which includes Salesforce), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="78c00-179">Propriété</span><span class="sxs-lookup"><span data-stu-id="78c00-179">Property</span></span> | <span data-ttu-id="78c00-180">Description</span><span class="sxs-lookup"><span data-stu-id="78c00-180">Description</span></span> | <span data-ttu-id="78c00-181">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="78c00-181">Allowed values</span></span> | <span data-ttu-id="78c00-182">Requis</span><span class="sxs-lookup"><span data-stu-id="78c00-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="78c00-183">query</span><span class="sxs-lookup"><span data-stu-id="78c00-183">query</span></span> |<span data-ttu-id="78c00-184">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="78c00-184">Use hello custom query tooread data.</span></span> |<span data-ttu-id="78c00-185">Une requête SQL-92 ou une requête [SOQL (Salesforce Object Query Language)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm).</span><span class="sxs-lookup"><span data-stu-id="78c00-185">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="78c00-186">Par exemple : `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="78c00-186">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="78c00-187">Non (si hello **tableName** Hello **dataset** est spécifié)</span><span class="sxs-lookup"><span data-stu-id="78c00-187">No (if hello **tableName** of hello **dataset** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="78c00-188">Hello « __c » partie hello nom de l’API est nécessaire pour tout objet personnalisé.</span><span class="sxs-lookup"><span data-stu-id="78c00-188">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Connexion Salesforce - Data Factory - Nom de l’API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a><span data-ttu-id="78c00-190">Conseils pour les requêtes</span><span class="sxs-lookup"><span data-stu-id="78c00-190">Query tips</span></span>
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a><span data-ttu-id="78c00-191">Récupération de données à l’aide de la clause where sur la colonne DateTime</span><span class="sxs-lookup"><span data-stu-id="78c00-191">Retrieving data using where clause on DateTime column</span></span>
<span data-ttu-id="78c00-192">Lorsque spécifiez hello SOQL ou SQL requête, prêtez attention toohello différence de format de date/heure.</span><span class="sxs-lookup"><span data-stu-id="78c00-192">When specify hello SOQL or SQL query, pay attention toohello DateTime format difference.</span></span> <span data-ttu-id="78c00-193">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="78c00-193">For example:</span></span>

* <span data-ttu-id="78c00-194">**Exemple SOQL** : `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="78c00-194">**SOQL sample**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span></span>
* <span data-ttu-id="78c00-195">**Exemple SQL** :</span><span class="sxs-lookup"><span data-stu-id="78c00-195">**SQL sample**:</span></span>
    * <span data-ttu-id="78c00-196">**À l’aide de la requête de hello toospecify l’Assistant copie :**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="78c00-196">**Using copy wizard toospecify hello query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span></span>
    * <span data-ttu-id="78c00-197">**L’utilisation de JSON modification toospecify hello requête (séquence d’échappement de char correctement) :**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="78c00-197">**Using JSON editing toospecify hello query (escape char properly):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span></span>

### <a name="retrieving-data-from-salesforce-report"></a><span data-ttu-id="78c00-198">Récupération de données à partir d’un rapport Salesforce</span><span class="sxs-lookup"><span data-stu-id="78c00-198">Retrieving data from Salesforce Report</span></span>
<span data-ttu-id="78c00-199">Vous pouvez récupérer des données à partir de rapports Salesforce en spécifiant la requête en tant que `{call "<report name>"}`, par exemple.</span><span class="sxs-lookup"><span data-stu-id="78c00-199">You can retrieve data from Salesforce reports by specifying query as `{call "<report name>"}`,for example,.</span></span> <span data-ttu-id="78c00-200">`"query": "{call \"TestReport\"}"`.</span><span class="sxs-lookup"><span data-stu-id="78c00-200">`"query": "{call \"TestReport\"}"`.</span></span>

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a><span data-ttu-id="78c00-201">Récupération d’enregistrements supprimés dans la Corbeille Salesforce</span><span class="sxs-lookup"><span data-stu-id="78c00-201">Retrieving deleted records from Salesforce Recycle Bin</span></span>
<span data-ttu-id="78c00-202">tooquery des enregistrements de hello logicielle supprimé à partir de la Corbeille de Salesforce, vous pouvez spécifier **« IsDeleted = 1 »** dans votre requête.</span><span class="sxs-lookup"><span data-stu-id="78c00-202">tooquery hello soft deleted records from Salesforce Recycle Bin, you can specify **"IsDeleted = 1"** in your query.</span></span> <span data-ttu-id="78c00-203">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="78c00-203">For example,</span></span>

* <span data-ttu-id="78c00-204">tooquery uniquement les enregistrements supprimé de hello, spécifiez « sélectionner * à partir de MyTable__c **où IsDeleted = 1**»</span><span class="sxs-lookup"><span data-stu-id="78c00-204">tooquery only hello deleted records, specify "select * from MyTable__c **where IsDeleted= 1**"</span></span>
* <span data-ttu-id="78c00-205">tooquery tous hello enregistrements notamment hello existant et hello supprimé, spécifiez « sélectionner * à partir de MyTable__c **où IsDeleted = 0 ou IsDeleted = 1**»</span><span class="sxs-lookup"><span data-stu-id="78c00-205">tooquery all hello records including hello existing and hello deleted, specify "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span></span>

## <a name="json-example-copy-data-from-salesforce-tooazure-blob"></a><span data-ttu-id="78c00-206">Exemple de JSON : copier des données à partir de Salesforce tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="78c00-206">JSON example: Copy data from Salesforce tooAzure Blob</span></span>
<span data-ttu-id="78c00-207">Hello exemple suivant fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de hello [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="78c00-207">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="78c00-208">Elles montrent comment toocopy des données à partir de Salesforce tooAzure stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="78c00-208">They show how toocopy data from Salesforce tooAzure Blob Storage.</span></span> <span data-ttu-id="78c00-209">Toutefois, les données peuvent être copié tooany de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="78c00-209">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="78c00-210">Voici les artefacts de Data Factory hello que vous devez le scénario de toocreate tooimplement hello.</span><span class="sxs-lookup"><span data-stu-id="78c00-210">Here are hello Data Factory artifacts that you'll need toocreate tooimplement hello scenario.</span></span> <span data-ttu-id="78c00-211">les sections Hello qui suivent hello liste fournissent des détails sur ces étapes.</span><span class="sxs-lookup"><span data-stu-id="78c00-211">hello sections that follow hello list provide details about these steps.</span></span>

* <span data-ttu-id="78c00-212">Un service lié de type de hello [Salesforce](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="78c00-212">A linked service of hello type [Salesforce](#linked-service-properties)</span></span>
* <span data-ttu-id="78c00-213">Un service lié de type de hello [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="78c00-213">A linked service of hello type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="78c00-214">Une entrée [dataset](data-factory-create-datasets.md) de type de hello [RelationalTable](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="78c00-214">An input [dataset](data-factory-create-datasets.md) of hello type [RelationalTable](#dataset-properties)</span></span>
* <span data-ttu-id="78c00-215">Une sortie [dataset](data-factory-create-datasets.md) de type de hello [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="78c00-215">An output [dataset](data-factory-create-datasets.md) of hello type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="78c00-216">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [RelationalSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="78c00-216">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="78c00-217">**Service lié Salesforce**</span><span class="sxs-lookup"><span data-stu-id="78c00-217">**Salesforce linked service**</span></span>

<span data-ttu-id="78c00-218">Cet exemple utilise hello **Salesforce** service lié.</span><span class="sxs-lookup"><span data-stu-id="78c00-218">This example uses hello **Salesforce** linked service.</span></span> <span data-ttu-id="78c00-219">Consultez hello [service lié de Salesforce](#linked-service-properties) section pour les propriétés hello sont pris en charge par ce service lié.</span><span class="sxs-lookup"><span data-stu-id="78c00-219">See hello [Salesforce linked service](#linked-service-properties) section for hello properties that are supported by this linked service.</span></span>  <span data-ttu-id="78c00-220">Consultez [obtenir jeton de sécurité](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) pour obtenir des instructions sur la façon dont tooreset/get hello le jeton de sécurité.</span><span class="sxs-lookup"><span data-stu-id="78c00-220">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get hello security token.</span></span>

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
<span data-ttu-id="78c00-221">**Service lié Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="78c00-221">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="78c00-222">**Jeu de données d’entrée Salesforce**</span><span class="sxs-lookup"><span data-stu-id="78c00-222">**Salesforce input dataset**</span></span>

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

<span data-ttu-id="78c00-223">Paramètre **externe** trop**true** informe le service de fabrique de données hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="78c00-223">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78c00-224">Hello « __c » partie hello nom de l’API est nécessaire pour tout objet personnalisé.</span><span class="sxs-lookup"><span data-stu-id="78c00-224">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Connexion Salesforce - Data Factory - Nom de l’API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

<span data-ttu-id="78c00-226">**Jeu de données de sortie d’objet Blob Azure**</span><span class="sxs-lookup"><span data-stu-id="78c00-226">**Azure blob output dataset**</span></span>

<span data-ttu-id="78c00-227">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="78c00-227">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

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

<span data-ttu-id="78c00-228">**Pipeline avec activité de copie**</span><span class="sxs-lookup"><span data-stu-id="78c00-228">**Pipeline with Copy Activity**</span></span>

<span data-ttu-id="78c00-229">pipeline Hello contient l’activité de copie, qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="78c00-229">hello pipeline contains Copy Activity, which is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="78c00-230">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**RelationalSource**et hello **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="78c00-230">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource**, and hello **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="78c00-231">Consultez [RelationalSource les propriétés de type](#copy-activity-properties) pour la liste des propriétés qui sont prises en charge par hello RelationalSource hello.</span><span class="sxs-lookup"><span data-stu-id="78c00-231">See [RelationalSource type properties](#copy-activity-properties) for hello list of properties that are supported by hello RelationalSource.</span></span>

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
            "description": "Copy from Salesforce tooan Azure blob",
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
> <span data-ttu-id="78c00-232">Hello « __c » partie hello nom de l’API est nécessaire pour tout objet personnalisé.</span><span class="sxs-lookup"><span data-stu-id="78c00-232">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Connexion Salesforce - Data Factory - Nom de l’API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a><span data-ttu-id="78c00-234">Mappage de type pour Salesforce</span><span class="sxs-lookup"><span data-stu-id="78c00-234">Type mapping for Salesforce</span></span>
| <span data-ttu-id="78c00-235">Type Salesforce</span><span class="sxs-lookup"><span data-stu-id="78c00-235">Salesforce type</span></span> | <span data-ttu-id="78c00-236">Type basé sur .NET</span><span class="sxs-lookup"><span data-stu-id="78c00-236">.NET-based type</span></span> |
| --- | --- |
| <span data-ttu-id="78c00-237">Numérotation automatique</span><span class="sxs-lookup"><span data-stu-id="78c00-237">Auto Number</span></span> |<span data-ttu-id="78c00-238">String</span><span class="sxs-lookup"><span data-stu-id="78c00-238">String</span></span> |
| <span data-ttu-id="78c00-239">Case à cocher</span><span class="sxs-lookup"><span data-stu-id="78c00-239">Checkbox</span></span> |<span data-ttu-id="78c00-240">Boolean</span><span class="sxs-lookup"><span data-stu-id="78c00-240">Boolean</span></span> |
| <span data-ttu-id="78c00-241">Devise</span><span class="sxs-lookup"><span data-stu-id="78c00-241">Currency</span></span> |<span data-ttu-id="78c00-242">Double</span><span class="sxs-lookup"><span data-stu-id="78c00-242">Double</span></span> |
| <span data-ttu-id="78c00-243">Date</span><span class="sxs-lookup"><span data-stu-id="78c00-243">Date</span></span> |<span data-ttu-id="78c00-244">DateTime</span><span class="sxs-lookup"><span data-stu-id="78c00-244">DateTime</span></span> |
| <span data-ttu-id="78c00-245">Date/Heure</span><span class="sxs-lookup"><span data-stu-id="78c00-245">Date/Time</span></span> |<span data-ttu-id="78c00-246">DateTime</span><span class="sxs-lookup"><span data-stu-id="78c00-246">DateTime</span></span> |
| <span data-ttu-id="78c00-247">Email</span><span class="sxs-lookup"><span data-stu-id="78c00-247">Email</span></span> |<span data-ttu-id="78c00-248">String</span><span class="sxs-lookup"><span data-stu-id="78c00-248">String</span></span> |
| <span data-ttu-id="78c00-249">ID</span><span class="sxs-lookup"><span data-stu-id="78c00-249">Id</span></span> |<span data-ttu-id="78c00-250">String</span><span class="sxs-lookup"><span data-stu-id="78c00-250">String</span></span> |
| <span data-ttu-id="78c00-251">Relation de recherche</span><span class="sxs-lookup"><span data-stu-id="78c00-251">Lookup Relationship</span></span> |<span data-ttu-id="78c00-252">String</span><span class="sxs-lookup"><span data-stu-id="78c00-252">String</span></span> |
| <span data-ttu-id="78c00-253">Liste déroulante à sélection multiple</span><span class="sxs-lookup"><span data-stu-id="78c00-253">Multi-Select Picklist</span></span> |<span data-ttu-id="78c00-254">String</span><span class="sxs-lookup"><span data-stu-id="78c00-254">String</span></span> |
| <span data-ttu-id="78c00-255">Number</span><span class="sxs-lookup"><span data-stu-id="78c00-255">Number</span></span> |<span data-ttu-id="78c00-256">Double</span><span class="sxs-lookup"><span data-stu-id="78c00-256">Double</span></span> |
| <span data-ttu-id="78c00-257">Pourcentage</span><span class="sxs-lookup"><span data-stu-id="78c00-257">Percent</span></span> |<span data-ttu-id="78c00-258">Double</span><span class="sxs-lookup"><span data-stu-id="78c00-258">Double</span></span> |
| <span data-ttu-id="78c00-259">Téléphone</span><span class="sxs-lookup"><span data-stu-id="78c00-259">Phone</span></span> |<span data-ttu-id="78c00-260">String</span><span class="sxs-lookup"><span data-stu-id="78c00-260">String</span></span> |
| <span data-ttu-id="78c00-261">Liste déroulante</span><span class="sxs-lookup"><span data-stu-id="78c00-261">Picklist</span></span> |<span data-ttu-id="78c00-262">String</span><span class="sxs-lookup"><span data-stu-id="78c00-262">String</span></span> |
| <span data-ttu-id="78c00-263">Texte</span><span class="sxs-lookup"><span data-stu-id="78c00-263">Text</span></span> |<span data-ttu-id="78c00-264">String</span><span class="sxs-lookup"><span data-stu-id="78c00-264">String</span></span> |
| <span data-ttu-id="78c00-265">Zone de texte</span><span class="sxs-lookup"><span data-stu-id="78c00-265">Text Area</span></span> |<span data-ttu-id="78c00-266">String</span><span class="sxs-lookup"><span data-stu-id="78c00-266">String</span></span> |
| <span data-ttu-id="78c00-267">Zone de texte (long)</span><span class="sxs-lookup"><span data-stu-id="78c00-267">Text Area (Long)</span></span> |<span data-ttu-id="78c00-268">String</span><span class="sxs-lookup"><span data-stu-id="78c00-268">String</span></span> |
| <span data-ttu-id="78c00-269">Zone de texte (enrichi)</span><span class="sxs-lookup"><span data-stu-id="78c00-269">Text Area (Rich)</span></span> |<span data-ttu-id="78c00-270">String</span><span class="sxs-lookup"><span data-stu-id="78c00-270">String</span></span> |
| <span data-ttu-id="78c00-271">Texte (chiffré)</span><span class="sxs-lookup"><span data-stu-id="78c00-271">Text (Encrypted)</span></span> |<span data-ttu-id="78c00-272">String</span><span class="sxs-lookup"><span data-stu-id="78c00-272">String</span></span> |
| <span data-ttu-id="78c00-273">URL</span><span class="sxs-lookup"><span data-stu-id="78c00-273">URL</span></span> |<span data-ttu-id="78c00-274">String</span><span class="sxs-lookup"><span data-stu-id="78c00-274">String</span></span> |

> [!NOTE]
> <span data-ttu-id="78c00-275">colonnes de toomap de toocolumns du jeu de données source à partir du jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="78c00-275">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a><span data-ttu-id="78c00-276">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="78c00-276">Performance and tuning</span></span>
<span data-ttu-id="78c00-277">Consultez hello [l’activité de copie guide des performances et paramétrage](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="78c00-277">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
