---
title: "données aaaTransform à l’aide du script U-SQL - Azure | Documents Microsoft"
description: "Découvrez comment tooprocess ou transformation des données en exécutant des scripts U-SQL sur Azure données Lake Analytique service de calcul."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: spelluru
ms.openlocfilehash: 51fdb40334d0c131720f65c3a96b4c5045a98b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a><span data-ttu-id="1f8f2-103">Transformer des données en exécutant des scripts U-SQL sur Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1f8f2-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="1f8f2-104">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="1f8f2-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="1f8f2-105">Activité pig</span><span class="sxs-lookup"><span data-stu-id="1f8f2-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="1f8f2-106">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="1f8f2-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="1f8f2-107">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="1f8f2-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="1f8f2-108">Activité Spark</span><span class="sxs-lookup"><span data-stu-id="1f8f2-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="1f8f2-109">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1f8f2-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="1f8f2-110">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1f8f2-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="1f8f2-111">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="1f8f2-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="1f8f2-112">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1f8f2-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="1f8f2-113">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="1f8f2-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="1f8f2-114">Un pipeline dans une fabrique de données Azure traite les données dans les services de stockage liés à l'aide des services de calcul liés.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-114">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="1f8f2-115">Il contient une séquence d'activités dans laquelle chaque activité effectue une opération de traitement spécifique.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-115">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="1f8f2-116">Cet article décrit hello **données Lake Analytique U-SQL activité** qui exécute un **U-SQL** de script sur un **Analytique de LAC de données Azure** service lié de calcul.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-116">This article describes hello **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span></span> 

> [!NOTE]
> <span data-ttu-id="1f8f2-117">Créez un compte Azure Data Lake Analytics avant de créer un pipeline avec une activité U-SQL Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-117">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="1f8f2-118">toolearn sur Analytique de LAC de données Azure, consultez [prise en main Azure données Lake Analytique](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1f8f2-118">toolearn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span>
> 
> <span data-ttu-id="1f8f2-119">Hello de révision [créer votre premier didacticiel de pipeline](data-factory-build-your-first-pipeline.md) pour obtenir des instructions détaillées toocreate une fabrique de données, lié à un pipeline, jeux de données et services.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-119">Review hello [Build your first pipeline tutorial](data-factory-build-your-first-pipeline.md) for detailed steps toocreate a data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="1f8f2-120">Utiliser des extraits de code JSON avec l’éditeur Data Factory ou entités de fabrique de données toocreate Visual Studio ou Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-120">Use JSON snippets with Data Factory Editor or Visual Studio or Azure PowerShell toocreate Data Factory entities.</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="1f8f2-121">Types d’authentification pris en charge</span><span class="sxs-lookup"><span data-stu-id="1f8f2-121">Supported authentication types</span></span>
<span data-ttu-id="1f8f2-122">L’activité U-SQL prend en charge les types d’authentification ci-dessous pour Data Lake Analytics :</span><span class="sxs-lookup"><span data-stu-id="1f8f2-122">U-SQL activity supports below authentication types against Data Lake Analytics:</span></span>
* <span data-ttu-id="1f8f2-123">Authentification d’un principal du service</span><span class="sxs-lookup"><span data-stu-id="1f8f2-123">Service principal authentication</span></span>
* <span data-ttu-id="1f8f2-124">Utilisation de l’authentification des informations d’identification utilisateur (OAuth)</span><span class="sxs-lookup"><span data-stu-id="1f8f2-124">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="1f8f2-125">Nous vous recommandons d’utiliser l’authentification de principal du service, en particulier pour une exécution de U-SQL planifiée.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-125">We recommend that you use service principal authentication, especially for a scheduled U-SQL execution.</span></span> <span data-ttu-id="1f8f2-126">Un comportement d’expiration de jeton peut se produire avec l’authentification par informations d’identification utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-126">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="1f8f2-127">Pour plus d’informations, consultez hello [lié des propriétés du service](#azure-data-lake-analytics-linked-service) section.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-127">For configuration details, see hello [Linked service properties](#azure-data-lake-analytics-linked-service) section.</span></span>

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="1f8f2-128">Service lié Analytique Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="1f8f2-128">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="1f8f2-129">Vous créez un **Analytique de LAC de données Azure** lié service toolink une Analytique de LAC de données Azure compute service tooan Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-129">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory.</span></span> <span data-ttu-id="1f8f2-130">Hello activité Data Lake Analytique U-SQL dans le pipeline de hello fait référence toothis lié service.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-130">hello Data Lake Analytics U-SQL activity in hello pipeline refers toothis linked service.</span></span> 

<span data-ttu-id="1f8f2-131">Hello tableau suivant fournit des descriptions pour hello propriétés génériques utilisées dans hello définition JSON.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-131">hello following table provides descriptions for hello generic properties used in hello JSON definition.</span></span> <span data-ttu-id="1f8f2-132">Vous pouvez ensuite choisir entre une authentification par principal de service et par informations d’identification utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-132">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="1f8f2-133">Propriété</span><span class="sxs-lookup"><span data-stu-id="1f8f2-133">Property</span></span> | <span data-ttu-id="1f8f2-134">Description</span><span class="sxs-lookup"><span data-stu-id="1f8f2-134">Description</span></span> | <span data-ttu-id="1f8f2-135">Requis</span><span class="sxs-lookup"><span data-stu-id="1f8f2-135">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1f8f2-136">**type**</span><span class="sxs-lookup"><span data-stu-id="1f8f2-136">**type**</span></span> |<span data-ttu-id="1f8f2-137">propriété de type Hello doit indiquer : **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-137">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="1f8f2-138">Oui</span><span class="sxs-lookup"><span data-stu-id="1f8f2-138">Yes</span></span> |
| <span data-ttu-id="1f8f2-139">**accountName**</span><span class="sxs-lookup"><span data-stu-id="1f8f2-139">**accountName**</span></span> |<span data-ttu-id="1f8f2-140">Nom du compte du service Analytique Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-140">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="1f8f2-141">Oui</span><span class="sxs-lookup"><span data-stu-id="1f8f2-141">Yes</span></span> |
| <span data-ttu-id="1f8f2-142">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="1f8f2-142">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="1f8f2-143">URI du service Analytique Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-143">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="1f8f2-144">Non</span><span class="sxs-lookup"><span data-stu-id="1f8f2-144">No</span></span> |
| <span data-ttu-id="1f8f2-145">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="1f8f2-145">**subscriptionId**</span></span> |<span data-ttu-id="1f8f2-146">ID d’abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="1f8f2-146">Azure subscription id</span></span> |<span data-ttu-id="1f8f2-147">Non (si non spécifié, abonnement Hello fabrique de données est utilisée).</span><span class="sxs-lookup"><span data-stu-id="1f8f2-147">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="1f8f2-148">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="1f8f2-148">**resourceGroupName**</span></span> |<span data-ttu-id="1f8f2-149">Nom du groupe de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="1f8f2-149">Azure resource group name</span></span> |<span data-ttu-id="1f8f2-150">Non (si non spécifié, groupe de ressources de hello fabrique de données est utilisée).</span><span class="sxs-lookup"><span data-stu-id="1f8f2-150">No (If not specified, resource group of hello data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="1f8f2-151">Authentification d’un principal du service (recommandée)</span><span class="sxs-lookup"><span data-stu-id="1f8f2-151">Service principal authentication (recommended)</span></span>
<span data-ttu-id="1f8f2-152">authentification principale du service toouse, inscrire une entité de l’application dans Azure Active Directory (Azure AD) et accordez à elle hello accéder à tooData Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-152">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="1f8f2-153">Consultez la page [Authentification de service à service](../data-lake-store/data-lake-store-authenticate-using-active-directory.md) pour des instructions détaillées.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-153">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="1f8f2-154">Prenez note de hello après les valeurs que vous pouvez utiliser toodefine hello de service lié :</span><span class="sxs-lookup"><span data-stu-id="1f8f2-154">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="1f8f2-155">ID de l'application</span><span class="sxs-lookup"><span data-stu-id="1f8f2-155">Application ID</span></span>
* <span data-ttu-id="1f8f2-156">Clé de l'application</span><span class="sxs-lookup"><span data-stu-id="1f8f2-156">Application key</span></span> 
* <span data-ttu-id="1f8f2-157">ID client</span><span class="sxs-lookup"><span data-stu-id="1f8f2-157">Tenant ID</span></span>

<span data-ttu-id="1f8f2-158">Utilisez l’authentification principale du service en spécifiant hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="1f8f2-158">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="1f8f2-159">Propriété</span><span class="sxs-lookup"><span data-stu-id="1f8f2-159">Property</span></span> | <span data-ttu-id="1f8f2-160">Description</span><span class="sxs-lookup"><span data-stu-id="1f8f2-160">Description</span></span> | <span data-ttu-id="1f8f2-161">Requis</span><span class="sxs-lookup"><span data-stu-id="1f8f2-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1f8f2-162">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="1f8f2-162">**servicePrincipalId**</span></span> | <span data-ttu-id="1f8f2-163">Spécifiez l’ID client de. l’application hello</span><span class="sxs-lookup"><span data-stu-id="1f8f2-163">Specify hello application's client ID.</span></span> | <span data-ttu-id="1f8f2-164">Oui</span><span class="sxs-lookup"><span data-stu-id="1f8f2-164">Yes</span></span> |
| <span data-ttu-id="1f8f2-165">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="1f8f2-165">**servicePrincipalKey**</span></span> | <span data-ttu-id="1f8f2-166">Spécifiez la clé de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-166">Specify hello application's key.</span></span> | <span data-ttu-id="1f8f2-167">Oui</span><span class="sxs-lookup"><span data-stu-id="1f8f2-167">Yes</span></span> |
| <span data-ttu-id="1f8f2-168">**client**</span><span class="sxs-lookup"><span data-stu-id="1f8f2-168">**tenant**</span></span> | <span data-ttu-id="1f8f2-169">Spécifiez les informations de locataire hello (ID client ou le nom de domaine) dans lequel réside votre application.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-169">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="1f8f2-170">Vous pouvez le récupérer par pointage de souris hello dans le coin supérieur droit de hello Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-170">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="1f8f2-171">Oui</span><span class="sxs-lookup"><span data-stu-id="1f8f2-171">Yes</span></span> |

<span data-ttu-id="1f8f2-172">**Exemple : authentification du principal de service**</span><span class="sxs-lookup"><span data-stu-id="1f8f2-172">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="1f8f2-173">Authentification des informations d’identification utilisateur</span><span class="sxs-lookup"><span data-stu-id="1f8f2-173">User credential authentication</span></span>
<span data-ttu-id="1f8f2-174">Vous pouvez également utiliser authentification des informations d’identification utilisateur pour l’Analytique lac de données en spécifiant les propriétés suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="1f8f2-174">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying hello following properties:</span></span>

| <span data-ttu-id="1f8f2-175">Propriété</span><span class="sxs-lookup"><span data-stu-id="1f8f2-175">Property</span></span> | <span data-ttu-id="1f8f2-176">Description</span><span class="sxs-lookup"><span data-stu-id="1f8f2-176">Description</span></span> | <span data-ttu-id="1f8f2-177">Requis</span><span class="sxs-lookup"><span data-stu-id="1f8f2-177">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1f8f2-178">**authorization**</span><span class="sxs-lookup"><span data-stu-id="1f8f2-178">**authorization**</span></span> | <span data-ttu-id="1f8f2-179">Cliquez sur hello **Authorize** bouton Bonjour éditeur Data Factory et entrez vos informations d’identification qui affecte le propriété toothis URL hello générées automatiquement d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-179">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="1f8f2-180">Oui</span><span class="sxs-lookup"><span data-stu-id="1f8f2-180">Yes</span></span> |
| <span data-ttu-id="1f8f2-181">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="1f8f2-181">**sessionId**</span></span> | <span data-ttu-id="1f8f2-182">ID de session OAuth à partir de la session de d’autorisation OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-182">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="1f8f2-183">Chaque ID de session est unique et ne peut être utilisé qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-183">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="1f8f2-184">Ce paramètre est automatiquement généré lorsque vous utilisez hello éditeur Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-184">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="1f8f2-185">Oui</span><span class="sxs-lookup"><span data-stu-id="1f8f2-185">Yes</span></span> |

<span data-ttu-id="1f8f2-186">**Exemple : authentification des informations d’identification utilisateur**</span><span class="sxs-lookup"><span data-stu-id="1f8f2-186">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="1f8f2-187">Expiration du jeton</span><span class="sxs-lookup"><span data-stu-id="1f8f2-187">Token expiration</span></span>
<span data-ttu-id="1f8f2-188">Hello code d’autorisation généré à l’aide de hello **Authorize** bouton expire après un certain temps.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-188">hello authorization code you generated by using hello **Authorize** button expires after sometime.</span></span> <span data-ttu-id="1f8f2-189">Consultez hello tableau suivant pour les délais d’expiration de hello pour différents types de comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-189">See hello following table for hello expiration times for different types of user accounts.</span></span> <span data-ttu-id="1f8f2-190">Hello message d’erreur suivant peut s’afficher lorsque hello authentification **expiration du jeton**: erreur de l’opération des informations d’identification : invalid_grant - AADSTS70002 : erreur de validation des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-190">You may see hello following error message when hello authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="1f8f2-191">AADSTS70008 : hello fourni octroi d’accès est expiré ou révoqué.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-191">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="1f8f2-192">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z ».</span><span class="sxs-lookup"><span data-stu-id="1f8f2-192">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="1f8f2-193">Type d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="1f8f2-193">User type</span></span> | <span data-ttu-id="1f8f2-194">Expire après</span><span class="sxs-lookup"><span data-stu-id="1f8f2-194">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="1f8f2-195">Comptes d’utilisateurs NON gérés par Azure Active Directory (@hotmail.com, @live.com, etc.)</span><span class="sxs-lookup"><span data-stu-id="1f8f2-195">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="1f8f2-196">12 heures</span><span class="sxs-lookup"><span data-stu-id="1f8f2-196">12 hours</span></span> |
| <span data-ttu-id="1f8f2-197">Comptes d’utilisateurs gérés par Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="1f8f2-197">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="1f8f2-198">exécution de 14 jours après la dernière tranche de hello.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-198">14 days after hello last slice run.</span></span> <br/><br/><span data-ttu-id="1f8f2-199">90 jours, si une tranche basée sur un service lié OAuth est exécutée au moins une fois tous les 14 jours.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-199">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="1f8f2-200">tooavoid/résoudre cette erreur, autorisez à nouveau à l’aide de hello **Authorize** bouton lorsque hello **expiration du jeton** et redéployez hello lié service.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-200">tooavoid/resolve this error, reauthorize using hello **Authorize** button when hello **token expires** and redeploy hello linked service.</span></span> <span data-ttu-id="1f8f2-201">Vous pouvez également générer par programmation des valeurs pour les propriétés **sessionId** et **authorization** à l’aide du code suivant :</span><span class="sxs-lookup"><span data-stu-id="1f8f2-201">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

<span data-ttu-id="1f8f2-202">Consultez [AzureDataLakeStoreLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), et [AuthorizationSessionGetResponse classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) pour plus d’informations sur les classes de fabrique de données hello utilisées dans le code hello.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-202">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about hello Data Factory classes used in hello code.</span></span> <span data-ttu-id="1f8f2-203">Ajoutez une référence à : Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll pour hello WindowsFormsWebAuthenticationDialog classe.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-203">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for hello WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="1f8f2-204">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1f8f2-204">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="1f8f2-205">Hello suivant extrait de code JSON définit un pipeline avec une activité de données Lake Analytique U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-205">hello following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="1f8f2-206">définition d’activité Hello possède une référence de toohello service Analytique de LAC de données Azure lié vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-206">hello activity definition has a reference toohello Azure Data Lake Analytics linked service you created earlier.</span></span>   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline toocompute events for en-gb locale and date less than 2012/02/19.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00Z",
        "end": "2015-08-08T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="1f8f2-207">Hello tableau suivant décrit les noms et descriptions des propriétés qui sont spécifiques toothis activité.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-207">hello following table describes names and descriptions of properties that are specific toothis activity.</span></span> 

| <span data-ttu-id="1f8f2-208">Propriété</span><span class="sxs-lookup"><span data-stu-id="1f8f2-208">Property</span></span> | <span data-ttu-id="1f8f2-209">Description</span><span class="sxs-lookup"><span data-stu-id="1f8f2-209">Description</span></span> | <span data-ttu-id="1f8f2-210">Requis</span><span class="sxs-lookup"><span data-stu-id="1f8f2-210">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1f8f2-211">type</span><span class="sxs-lookup"><span data-stu-id="1f8f2-211">type</span></span> |<span data-ttu-id="1f8f2-212">propriété de type Hello doit être définie trop**DataLakeAnalyticsU-SQL**.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-212">hello type property must be set too**DataLakeAnalyticsU-SQL**.</span></span> |<span data-ttu-id="1f8f2-213">Oui</span><span class="sxs-lookup"><span data-stu-id="1f8f2-213">Yes</span></span> |
| <span data-ttu-id="1f8f2-214">scriptPath</span><span class="sxs-lookup"><span data-stu-id="1f8f2-214">scriptPath</span></span> |<span data-ttu-id="1f8f2-215">Toofolder de chemin d’accès qui contient le script de hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-215">Path toofolder that contains hello U-SQL script.</span></span> <span data-ttu-id="1f8f2-216">Nom du fichier de hello respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-216">Name of hello file is case-sensitive.</span></span> |<span data-ttu-id="1f8f2-217">Non (si vous utilisez le script)</span><span class="sxs-lookup"><span data-stu-id="1f8f2-217">No (if you use script)</span></span> |
| <span data-ttu-id="1f8f2-218">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="1f8f2-218">scriptLinkedService</span></span> |<span data-ttu-id="1f8f2-219">Service lié qui établit un lien stockage hello qui contient la fabrique de données hello script toohello</span><span class="sxs-lookup"><span data-stu-id="1f8f2-219">Linked service that links hello storage that contains hello script toohello data factory</span></span> |<span data-ttu-id="1f8f2-220">Non (si vous utilisez le script)</span><span class="sxs-lookup"><span data-stu-id="1f8f2-220">No (if you use script)</span></span> |
| <span data-ttu-id="1f8f2-221">script</span><span class="sxs-lookup"><span data-stu-id="1f8f2-221">script</span></span> |<span data-ttu-id="1f8f2-222">Spécifiez un script en ligne au lieu de spécifier scriptPath et scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-222">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="1f8f2-223">Par exemple : `"script": "CREATE DATABASE test"`.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-223">For example: `"script": "CREATE DATABASE test"`.</span></span> |<span data-ttu-id="1f8f2-224">Non (si vous utilisez scriptPath et scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="1f8f2-224">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="1f8f2-225">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="1f8f2-225">degreeOfParallelism</span></span> |<span data-ttu-id="1f8f2-226">nombre maximal de Hello de nœuds utilisés simultanément tâche hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-226">hello maximum number of nodes simultaneously used toorun hello job.</span></span> |<span data-ttu-id="1f8f2-227">Non</span><span class="sxs-lookup"><span data-stu-id="1f8f2-227">No</span></span> |
| <span data-ttu-id="1f8f2-228">priority</span><span class="sxs-lookup"><span data-stu-id="1f8f2-228">priority</span></span> |<span data-ttu-id="1f8f2-229">Détermine les tâches en dehors de tout ce qui sont en attente doivent être sélectionné toorun tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-229">Determines which jobs out of all that are queued should be selected toorun first.</span></span> <span data-ttu-id="1f8f2-230">Hello hello numéro inférieur, une priorité plus élevée hello hello.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-230">hello lower hello number, hello higher hello priority.</span></span> |<span data-ttu-id="1f8f2-231">Non</span><span class="sxs-lookup"><span data-stu-id="1f8f2-231">No</span></span> |
| <span data-ttu-id="1f8f2-232">parameters</span><span class="sxs-lookup"><span data-stu-id="1f8f2-232">parameters</span></span> |<span data-ttu-id="1f8f2-233">Paramètres de script de hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="1f8f2-233">Parameters for hello U-SQL script</span></span> |<span data-ttu-id="1f8f2-234">Non</span><span class="sxs-lookup"><span data-stu-id="1f8f2-234">No</span></span> |
| <span data-ttu-id="1f8f2-235">runtimeVersion</span><span class="sxs-lookup"><span data-stu-id="1f8f2-235">runtimeVersion</span></span> | <span data-ttu-id="1f8f2-236">Version du runtime de toouse de moteur hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="1f8f2-236">Runtime version of hello U-SQL engine toouse</span></span> | <span data-ttu-id="1f8f2-237">Non</span><span class="sxs-lookup"><span data-stu-id="1f8f2-237">No</span></span> | 
| <span data-ttu-id="1f8f2-238">compilationMode</span><span class="sxs-lookup"><span data-stu-id="1f8f2-238">compilationMode</span></span> | <p><span data-ttu-id="1f8f2-239">Mode de compilation d’U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-239">Compilation mode of U-SQL.</span></span> <span data-ttu-id="1f8f2-240">Doit avoir l’une des valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="1f8f2-240">Must be one of these values:</span></span></p> <ul><li><span data-ttu-id="1f8f2-241">**Semantic :** exécuter uniquement les vérifications sémantiques et les contrôles d’intégrité nécessaires.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-241">**Semantic:** Only perform semantic checks and necessary sanity checks.</span></span></li><li><span data-ttu-id="1f8f2-242">**Complète :** effectuer une compilation complète hello, y compris la vérification de la syntaxe, l’optimisation, la génération de code, etc..</span><span class="sxs-lookup"><span data-stu-id="1f8f2-242">**Full:** Perform hello full compilation, including syntax check, optimization, code generation, etc.</span></span></li><li><span data-ttu-id="1f8f2-243">**SingleBox :** effectuer une compilation complète hello, avec tooSingleBox de paramètre TargetType.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-243">**SingleBox:** Perform hello full compilation, with TargetType setting tooSingleBox.</span></span></li></ul><p><span data-ttu-id="1f8f2-244">Si vous ne spécifiez pas une valeur pour cette propriété, serveur de hello détermine le mode de compilation optimal hello.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-244">If you don't specify a value for this property, hello server determines hello optimal compilation mode.</span></span> </p>| <span data-ttu-id="1f8f2-245">Non</span><span class="sxs-lookup"><span data-stu-id="1f8f2-245">No</span></span> | 

<span data-ttu-id="1f8f2-246">Consultez [SearchLogProcessing.txt Script définition](#sample-u-sql-script) pour la définition de script hello.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-246">See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for hello script definition.</span></span> 

## <a name="sample-input-and-output-datasets"></a><span data-ttu-id="1f8f2-247">Exemples de jeux de données d'entrée et de sortie</span><span class="sxs-lookup"><span data-stu-id="1f8f2-247">Sample input and output datasets</span></span>
### <a name="input-dataset"></a><span data-ttu-id="1f8f2-248">Jeu de données d'entrée</span><span class="sxs-lookup"><span data-stu-id="1f8f2-248">Input dataset</span></span>
<span data-ttu-id="1f8f2-249">Dans cet exemple, les données d’entrée hello résident dans un Azure Data Lake Store (fichier SearchLog.tsv dans le dossier de datalake/entrée hello).</span><span class="sxs-lookup"><span data-stu-id="1f8f2-249">In this example, hello input data resides in an Azure Data Lake Store (SearchLog.tsv file in hello datalake/input folder).</span></span> 

```json
{
    "name": "DataLakeTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}    
```

### <a name="output-dataset"></a><span data-ttu-id="1f8f2-250">Jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="1f8f2-250">Output dataset</span></span>
<span data-ttu-id="1f8f2-251">Dans cet exemple, les données de sortie de hello produites par hello script U-SQL sont stockées dans un Azure Data Lake Store (dossier datalake/sortie).</span><span class="sxs-lookup"><span data-stu-id="1f8f2-251">In this example, hello output data produced by hello U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span></span> 

```json
{
    "name": "EventsByRegionTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="sample-data-lake-store-linked-service"></a><span data-ttu-id="1f8f2-252">Exemple de service lié Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1f8f2-252">Sample Data Lake Store Linked Service</span></span>
<span data-ttu-id="1f8f2-253">Voici la définition hello d’exemple hello Qu'azure Data Lake Store lié service utilisé par les jeux de données d’entrée/sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-253">Here is hello definition of hello sample Azure Data Lake Store linked service used by hello input/output datasets.</span></span> 

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
        }
    }
}
```

<span data-ttu-id="1f8f2-254">Consultez [déplacer tooand de données à partir d’Azure Data Lake Store](data-factory-azure-datalake-connector.md) article pour une description des propriétés JSON.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-254">See [Move data tooand from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span></span> 

## <a name="sample-u-sql-script"></a><span data-ttu-id="1f8f2-255">Exemple de script SQL-U</span><span class="sxs-lookup"><span data-stu-id="1f8f2-255">Sample U-SQL Script</span></span>

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    too@out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

<span data-ttu-id="1f8f2-256">Hello pour les valeurs  **@in**  et  **@out**  paramètres dans le script de hello U-SQL sont passés dynamiquement par la définition d’application à l’aide de la section « Paramètres » de hello.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-256">hello values for **@in** and **@out** parameters in hello U-SQL script are passed dynamically by ADF using hello ‘parameters’ section.</span></span> <span data-ttu-id="1f8f2-257">Consultez la section de « paramètres » de hello dans la définition de pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-257">See hello ‘parameters’ section in hello pipeline definition.</span></span>

<span data-ttu-id="1f8f2-258">Vous pouvez spécifier d’autres propriétés comme la priorité et degreeOfParallelism également dans votre définition de pipeline pour les travaux hello qui s’exécutent sur hello service d’Analytique de LAC de données Azure.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-258">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for hello jobs that run on hello Azure Data Lake Analytics service.</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="1f8f2-259">Paramètres dynamiques</span><span class="sxs-lookup"><span data-stu-id="1f8f2-259">Dynamic parameters</span></span>
<span data-ttu-id="1f8f2-260">Dans la définition de pipeline exemple hello et l’extraction sont affectées aux paramètres avec des valeurs codées en dur.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-260">In hello sample pipeline definition, in and out parameters are assigned with hard-coded values.</span></span> 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

<span data-ttu-id="1f8f2-261">Il est possible toouse les paramètres dynamiques à la place.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-261">It is possible toouse dynamic parameters instead.</span></span> <span data-ttu-id="1f8f2-262">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="1f8f2-262">For example:</span></span> 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

<span data-ttu-id="1f8f2-263">Dans ce cas, les fichiers d’entrée sont toujours extraits à partir du dossier /datalake/input hello et les fichiers de sortie sont générés dans le dossier de /datalake/output hello.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-263">In this case, input files are still picked up from hello /datalake/input folder and output files are generated in hello /datalake/output folder.</span></span> <span data-ttu-id="1f8f2-264">les noms de fichiers Hello sont dynamiques en fonction de l’heure de début de tranche hello.</span><span class="sxs-lookup"><span data-stu-id="1f8f2-264">hello file names are dynamic based on hello slice start time.</span></span>  

