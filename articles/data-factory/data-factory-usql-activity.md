---
title: "Transformer des données à l’aide d’un script U-SQL - Azure | Microsoft Docs"
description: "Découvrez comment traiter ou transformer les données en exécutant des scripts U-SQL sur le service de calcul Azure Data Lake Analytics."
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
ms.openlocfilehash: 49a809af92ed1bc6664fbdd3bf1aabf36afb8180
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a><span data-ttu-id="a6298-103">Transformer des données en exécutant des scripts U-SQL sur Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a6298-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="a6298-104">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="a6298-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="a6298-105">Activité pig</span><span class="sxs-lookup"><span data-stu-id="a6298-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="a6298-106">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="a6298-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="a6298-107">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="a6298-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="a6298-108">Activité Spark</span><span class="sxs-lookup"><span data-stu-id="a6298-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="a6298-109">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a6298-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="a6298-110">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a6298-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="a6298-111">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="a6298-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="a6298-112">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a6298-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="a6298-113">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="a6298-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="a6298-114">Un pipeline dans une fabrique de données Azure traite les données dans les services de stockage liés à l'aide des services de calcul liés.</span><span class="sxs-lookup"><span data-stu-id="a6298-114">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="a6298-115">Il contient une séquence d'activités dans laquelle chaque activité effectue une opération de traitement spécifique.</span><span class="sxs-lookup"><span data-stu-id="a6298-115">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="a6298-116">Cet article décrit l’**activité U-SQL de Data Lake Analytics** qui exécute un script **U-SQL** sur un service lié de calcul **Azure Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="a6298-116">This article describes the **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span></span> 

> [!NOTE]
> <span data-ttu-id="a6298-117">Créez un compte Azure Data Lake Analytics avant de créer un pipeline avec une activité U-SQL Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="a6298-117">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="a6298-118">Pour plus d’informations sur Azure Data Lake Analytics, consultez [Prise en main d’Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a6298-118">To learn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span>
> 
> <span data-ttu-id="a6298-119">Consultez le [didacticiel Concevez votre premier pipeline](data-factory-build-your-first-pipeline.md) pour connaître les étapes détaillées de création d'une fabrique de données, de services liés, de jeux de données et d'un pipeline.</span><span class="sxs-lookup"><span data-stu-id="a6298-119">Review the [Build your first pipeline tutorial](data-factory-build-your-first-pipeline.md) for detailed steps to create a data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="a6298-120">Utilisez les extraits de code JSON avec Data Factory Editor ou Visual Studio ou Azure PowerShell pour créer les entités Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a6298-120">Use JSON snippets with Data Factory Editor or Visual Studio or Azure PowerShell to create Data Factory entities.</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="a6298-121">Types d’authentification pris en charge</span><span class="sxs-lookup"><span data-stu-id="a6298-121">Supported authentication types</span></span>
<span data-ttu-id="a6298-122">L’activité U-SQL prend en charge les types d’authentification ci-dessous pour Data Lake Analytics :</span><span class="sxs-lookup"><span data-stu-id="a6298-122">U-SQL activity supports below authentication types against Data Lake Analytics:</span></span>
* <span data-ttu-id="a6298-123">Authentification d’un principal du service</span><span class="sxs-lookup"><span data-stu-id="a6298-123">Service principal authentication</span></span>
* <span data-ttu-id="a6298-124">Utilisation de l’authentification des informations d’identification utilisateur (OAuth)</span><span class="sxs-lookup"><span data-stu-id="a6298-124">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="a6298-125">Nous vous recommandons d’utiliser l’authentification de principal du service, en particulier pour une exécution de U-SQL planifiée.</span><span class="sxs-lookup"><span data-stu-id="a6298-125">We recommend that you use service principal authentication, especially for a scheduled U-SQL execution.</span></span> <span data-ttu-id="a6298-126">Un comportement d’expiration de jeton peut se produire avec l’authentification par informations d’identification utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a6298-126">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="a6298-127">Pour les détails de configuration, consultez la section [Propriétés du service lié](#azure-data-lake-analytics-linked-service).</span><span class="sxs-lookup"><span data-stu-id="a6298-127">For configuration details, see the [Linked service properties](#azure-data-lake-analytics-linked-service) section.</span></span>

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="a6298-128">Service lié Analytique Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="a6298-128">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="a6298-129">Vous créez un service lié **Analytique Azure Data Lake** pour lier un service de calcul Analytique Azure Data Lake Analytics à une fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="a6298-129">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory.</span></span> <span data-ttu-id="a6298-130">L’activité U-SQL Analytique Data Lake dans le pipeline fait référence à ce service lié.</span><span class="sxs-lookup"><span data-stu-id="a6298-130">The Data Lake Analytics U-SQL activity in the pipeline refers to this linked service.</span></span> 

<span data-ttu-id="a6298-131">Le tableau suivant décrit les propriétés génériques utilisées dans la définition JSON.</span><span class="sxs-lookup"><span data-stu-id="a6298-131">The following table provides descriptions for the generic properties used in the JSON definition.</span></span> <span data-ttu-id="a6298-132">Vous pouvez ensuite choisir entre une authentification par principal de service et par informations d’identification utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a6298-132">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="a6298-133">Propriété</span><span class="sxs-lookup"><span data-stu-id="a6298-133">Property</span></span> | <span data-ttu-id="a6298-134">Description</span><span class="sxs-lookup"><span data-stu-id="a6298-134">Description</span></span> | <span data-ttu-id="a6298-135">Requis</span><span class="sxs-lookup"><span data-stu-id="a6298-135">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a6298-136">**type**</span><span class="sxs-lookup"><span data-stu-id="a6298-136">**type**</span></span> |<span data-ttu-id="a6298-137">La propriété de type doit être définie sur **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="a6298-137">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="a6298-138">Oui</span><span class="sxs-lookup"><span data-stu-id="a6298-138">Yes</span></span> |
| <span data-ttu-id="a6298-139">**accountName**</span><span class="sxs-lookup"><span data-stu-id="a6298-139">**accountName**</span></span> |<span data-ttu-id="a6298-140">Nom du compte du service Analytique Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a6298-140">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="a6298-141">Oui</span><span class="sxs-lookup"><span data-stu-id="a6298-141">Yes</span></span> |
| <span data-ttu-id="a6298-142">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="a6298-142">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="a6298-143">URI du service Analytique Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a6298-143">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="a6298-144">Non</span><span class="sxs-lookup"><span data-stu-id="a6298-144">No</span></span> |
| <span data-ttu-id="a6298-145">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="a6298-145">**subscriptionId**</span></span> |<span data-ttu-id="a6298-146">ID d’abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="a6298-146">Azure subscription id</span></span> |<span data-ttu-id="a6298-147">Non (si non spécifié, l’abonnement de la fabrique de données est utilisé).</span><span class="sxs-lookup"><span data-stu-id="a6298-147">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="a6298-148">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="a6298-148">**resourceGroupName**</span></span> |<span data-ttu-id="a6298-149">Nom du groupe de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="a6298-149">Azure resource group name</span></span> |<span data-ttu-id="a6298-150">Non (si non spécifié, le groupe de ressources de la fabrique de données est utilisé).</span><span class="sxs-lookup"><span data-stu-id="a6298-150">No (If not specified, resource group of the data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="a6298-151">Authentification d’un principal du service (recommandée)</span><span class="sxs-lookup"><span data-stu-id="a6298-151">Service principal authentication (recommended)</span></span>
<span data-ttu-id="a6298-152">Pour utiliser l’authentification d’un principal du service, inscrivez une entité d’application dans Azure Active Directory (Azure AD) et lui accorder l’accès à Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a6298-152">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to Data Lake Store.</span></span> <span data-ttu-id="a6298-153">Consultez la page [Authentification de service à service](../data-lake-store/data-lake-store-authenticate-using-active-directory.md) pour des instructions détaillées.</span><span class="sxs-lookup"><span data-stu-id="a6298-153">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="a6298-154">Prenez note des valeurs suivantes, qui vous permettent de définir le service lié :</span><span class="sxs-lookup"><span data-stu-id="a6298-154">Make note of the following values, which you use to define the linked service:</span></span>
* <span data-ttu-id="a6298-155">ID de l'application</span><span class="sxs-lookup"><span data-stu-id="a6298-155">Application ID</span></span>
* <span data-ttu-id="a6298-156">Clé de l'application</span><span class="sxs-lookup"><span data-stu-id="a6298-156">Application key</span></span> 
* <span data-ttu-id="a6298-157">ID client</span><span class="sxs-lookup"><span data-stu-id="a6298-157">Tenant ID</span></span>

<span data-ttu-id="a6298-158">Utilisez l’authentification par principal de service en spécifiant les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="a6298-158">Use service principal authentication by specifying the following properties:</span></span>

| <span data-ttu-id="a6298-159">Propriété</span><span class="sxs-lookup"><span data-stu-id="a6298-159">Property</span></span> | <span data-ttu-id="a6298-160">Description</span><span class="sxs-lookup"><span data-stu-id="a6298-160">Description</span></span> | <span data-ttu-id="a6298-161">Requis</span><span class="sxs-lookup"><span data-stu-id="a6298-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a6298-162">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="a6298-162">**servicePrincipalId**</span></span> | <span data-ttu-id="a6298-163">Spécifiez l’ID client de l’application.</span><span class="sxs-lookup"><span data-stu-id="a6298-163">Specify the application's client ID.</span></span> | <span data-ttu-id="a6298-164">Oui</span><span class="sxs-lookup"><span data-stu-id="a6298-164">Yes</span></span> |
| <span data-ttu-id="a6298-165">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="a6298-165">**servicePrincipalKey**</span></span> | <span data-ttu-id="a6298-166">Spécifiez la clé de l’application.</span><span class="sxs-lookup"><span data-stu-id="a6298-166">Specify the application's key.</span></span> | <span data-ttu-id="a6298-167">Oui</span><span class="sxs-lookup"><span data-stu-id="a6298-167">Yes</span></span> |
| <span data-ttu-id="a6298-168">**client**</span><span class="sxs-lookup"><span data-stu-id="a6298-168">**tenant**</span></span> | <span data-ttu-id="a6298-169">Spécifiez les informations de locataire (nom de domaine ou ID de locataire) dans lesquels se trouve votre application.</span><span class="sxs-lookup"><span data-stu-id="a6298-169">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="a6298-170">Vous pouvez le récupérer en pointant la souris dans le coin supérieur droit du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a6298-170">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span></span> | <span data-ttu-id="a6298-171">Oui</span><span class="sxs-lookup"><span data-stu-id="a6298-171">Yes</span></span> |

<span data-ttu-id="a6298-172">**Exemple : authentification du principal de service**</span><span class="sxs-lookup"><span data-stu-id="a6298-172">**Example: Service principal authentication**</span></span>
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

### <a name="user-credential-authentication"></a><span data-ttu-id="a6298-173">Authentification des informations d’identification utilisateur</span><span class="sxs-lookup"><span data-stu-id="a6298-173">User credential authentication</span></span>
<span data-ttu-id="a6298-174">Vous pouvez également utiliser l’authentification par informations d’identification utilisateur pour Data Lake Analytics en spécifiant les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="a6298-174">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying the following properties:</span></span>

| <span data-ttu-id="a6298-175">Propriété</span><span class="sxs-lookup"><span data-stu-id="a6298-175">Property</span></span> | <span data-ttu-id="a6298-176">Description</span><span class="sxs-lookup"><span data-stu-id="a6298-176">Description</span></span> | <span data-ttu-id="a6298-177">Requis</span><span class="sxs-lookup"><span data-stu-id="a6298-177">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a6298-178">**authorization**</span><span class="sxs-lookup"><span data-stu-id="a6298-178">**authorization**</span></span> | <span data-ttu-id="a6298-179">Cliquez sur le bouton **Autoriser** dans Data Factory Editor et saisissez vos informations d’identification, ce qui affecte l’URL d’autorisation générée automatiquement à cette propriété.</span><span class="sxs-lookup"><span data-stu-id="a6298-179">Click the **Authorize** button in the Data Factory Editor and enter your credential that assigns the autogenerated authorization URL to this property.</span></span> | <span data-ttu-id="a6298-180">Oui</span><span class="sxs-lookup"><span data-stu-id="a6298-180">Yes</span></span> |
| <span data-ttu-id="a6298-181">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="a6298-181">**sessionId**</span></span> | <span data-ttu-id="a6298-182">ID de session OAuth issu de la session d’autorisation OAuth.</span><span class="sxs-lookup"><span data-stu-id="a6298-182">OAuth session ID from the OAuth authorization session.</span></span> <span data-ttu-id="a6298-183">Chaque ID de session est unique et ne peut être utilisé qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="a6298-183">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="a6298-184">Ce paramètre est généré automatiquement lorsque vous utilisez Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="a6298-184">This setting is automatically generated when you use the Data Factory Editor.</span></span> | <span data-ttu-id="a6298-185">Oui</span><span class="sxs-lookup"><span data-stu-id="a6298-185">Yes</span></span> |

<span data-ttu-id="a6298-186">**Exemple : authentification des informations d’identification utilisateur**</span><span class="sxs-lookup"><span data-stu-id="a6298-186">**Example: User credential authentication**</span></span>
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

#### <a name="token-expiration"></a><span data-ttu-id="a6298-187">Expiration du jeton</span><span class="sxs-lookup"><span data-stu-id="a6298-187">Token expiration</span></span>
<span data-ttu-id="a6298-188">Le code d’autorisation que vous avez généré à l’aide du bouton **Autoriser** expire au bout d’un certain temps.</span><span class="sxs-lookup"><span data-stu-id="a6298-188">The authorization code you generated by using the **Authorize** button expires after sometime.</span></span> <span data-ttu-id="a6298-189">Consultez le tableau suivant pour connaître les délais d’expiration associés aux différents types de comptes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a6298-189">See the following table for the expiration times for different types of user accounts.</span></span> <span data-ttu-id="a6298-190">Le message d’erreur suivant peut s’afficher à **l’expiration du jeton** d’authentification : Erreur de l’opération d’informations d’identification : invalid_grant - AADSTS70002: Erreur de validation des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="a6298-190">You may see the following error message when the authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="a6298-191">AADSTS70008: The provided access grant is expired or revoked.</span><span class="sxs-lookup"><span data-stu-id="a6298-191">AADSTS70008: The provided access grant is expired or revoked.</span></span> <span data-ttu-id="a6298-192">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z ».</span><span class="sxs-lookup"><span data-stu-id="a6298-192">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="a6298-193">Type d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="a6298-193">User type</span></span> | <span data-ttu-id="a6298-194">Expire après</span><span class="sxs-lookup"><span data-stu-id="a6298-194">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="a6298-195">Comptes d’utilisateurs NON gérés par Azure Active Directory (@hotmail.com, @live.com, etc.)</span><span class="sxs-lookup"><span data-stu-id="a6298-195">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="a6298-196">12 heures</span><span class="sxs-lookup"><span data-stu-id="a6298-196">12 hours</span></span> |
| <span data-ttu-id="a6298-197">Comptes d’utilisateurs gérés par Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="a6298-197">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="a6298-198">14 jours après la dernière exécution de tranche de données.</span><span class="sxs-lookup"><span data-stu-id="a6298-198">14 days after the last slice run.</span></span> <br/><br/><span data-ttu-id="a6298-199">90 jours, si une tranche basée sur un service lié OAuth est exécutée au moins une fois tous les 14 jours.</span><span class="sxs-lookup"><span data-stu-id="a6298-199">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="a6298-200">Pour éviter ou résoudre cette erreur, accordez une nouvelle autorisation à l’aide du bouton **Autoriser** au moment de **l’expiration du jeton**, puis redéployer le service lié.</span><span class="sxs-lookup"><span data-stu-id="a6298-200">To avoid/resolve this error, reauthorize using the **Authorize** button when the **token expires** and redeploy the linked service.</span></span> <span data-ttu-id="a6298-201">Vous pouvez également générer par programmation des valeurs pour les propriétés **sessionId** et **authorization** à l’aide du code suivant :</span><span class="sxs-lookup"><span data-stu-id="a6298-201">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

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

<span data-ttu-id="a6298-202">Pour plus d’informations sur les classes Data Factory utilisées dans le code, consultez les rubriques [AzureDataLakeStoreLinkedService, classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService, classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx) et [AuthorizationSessionGetResponse, classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx).</span><span class="sxs-lookup"><span data-stu-id="a6298-202">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about the Data Factory classes used in the code.</span></span> <span data-ttu-id="a6298-203">Ajoutez une référence à Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll pour la classe WindowsFormsWebAuthenticationDialog.</span><span class="sxs-lookup"><span data-stu-id="a6298-203">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for the WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="a6298-204">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a6298-204">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="a6298-205">L'extrait de code JSON suivant définit un pipeline avec une activité U-SQL Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="a6298-205">The following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="a6298-206">La définition d'activité comporte une référence au service lié Azure Data Lake Analytics créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="a6298-206">The activity definition has a reference to the Azure Data Lake Analytics linked service you created earlier.</span></span>   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline to compute events for en-gb locale and date less than 2012/02/19.",
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

<span data-ttu-id="a6298-207">Le tableau suivant indique les noms et les descriptions des propriétés qui sont spécifiques à cette activité.</span><span class="sxs-lookup"><span data-stu-id="a6298-207">The following table describes names and descriptions of properties that are specific to this activity.</span></span> 

| <span data-ttu-id="a6298-208">Propriété</span><span class="sxs-lookup"><span data-stu-id="a6298-208">Property</span></span> | <span data-ttu-id="a6298-209">Description</span><span class="sxs-lookup"><span data-stu-id="a6298-209">Description</span></span> | <span data-ttu-id="a6298-210">Requis</span><span class="sxs-lookup"><span data-stu-id="a6298-210">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a6298-211">Type</span><span class="sxs-lookup"><span data-stu-id="a6298-211">type</span></span> |<span data-ttu-id="a6298-212">La propriété de type doit être définie sur **DataLakeAnalyticsU-SQL**.</span><span class="sxs-lookup"><span data-stu-id="a6298-212">The type property must be set to **DataLakeAnalyticsU-SQL**.</span></span> |<span data-ttu-id="a6298-213">Oui</span><span class="sxs-lookup"><span data-stu-id="a6298-213">Yes</span></span> |
| <span data-ttu-id="a6298-214">scriptPath</span><span class="sxs-lookup"><span data-stu-id="a6298-214">scriptPath</span></span> |<span data-ttu-id="a6298-215">Chemin d'accès au dossier qui contient le script SQL-U.</span><span class="sxs-lookup"><span data-stu-id="a6298-215">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="a6298-216">Le nom de fichier respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="a6298-216">Name of the file is case-sensitive.</span></span> |<span data-ttu-id="a6298-217">Non (si vous utilisez le script)</span><span class="sxs-lookup"><span data-stu-id="a6298-217">No (if you use script)</span></span> |
| <span data-ttu-id="a6298-218">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="a6298-218">scriptLinkedService</span></span> |<span data-ttu-id="a6298-219">Service lié qui lie le stockage qui contient le script à la fabrique de données</span><span class="sxs-lookup"><span data-stu-id="a6298-219">Linked service that links the storage that contains the script to the data factory</span></span> |<span data-ttu-id="a6298-220">Non (si vous utilisez le script)</span><span class="sxs-lookup"><span data-stu-id="a6298-220">No (if you use script)</span></span> |
| <span data-ttu-id="a6298-221">script</span><span class="sxs-lookup"><span data-stu-id="a6298-221">script</span></span> |<span data-ttu-id="a6298-222">Spécifiez un script en ligne au lieu de spécifier scriptPath et scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="a6298-222">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="a6298-223">Par exemple : `"script": "CREATE DATABASE test"`.</span><span class="sxs-lookup"><span data-stu-id="a6298-223">For example: `"script": "CREATE DATABASE test"`.</span></span> |<span data-ttu-id="a6298-224">Non (si vous utilisez scriptPath et scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="a6298-224">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="a6298-225">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="a6298-225">degreeOfParallelism</span></span> |<span data-ttu-id="a6298-226">Le nombre maximal de nœuds utilisés simultanément pour exécuter le travail.</span><span class="sxs-lookup"><span data-stu-id="a6298-226">The maximum number of nodes simultaneously used to run the job.</span></span> |<span data-ttu-id="a6298-227">Non</span><span class="sxs-lookup"><span data-stu-id="a6298-227">No</span></span> |
| <span data-ttu-id="a6298-228">priority</span><span class="sxs-lookup"><span data-stu-id="a6298-228">priority</span></span> |<span data-ttu-id="a6298-229">Détermine les travaux parmi tous ceux qui sont en file d'attente qui doivent être sélectionnés pour s'exécuter en premier.</span><span class="sxs-lookup"><span data-stu-id="a6298-229">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="a6298-230">Plus le numéro est faible, plus la priorité est élevée.</span><span class="sxs-lookup"><span data-stu-id="a6298-230">The lower the number, the higher the priority.</span></span> |<span data-ttu-id="a6298-231">Non</span><span class="sxs-lookup"><span data-stu-id="a6298-231">No</span></span> |
| <span data-ttu-id="a6298-232">parameters</span><span class="sxs-lookup"><span data-stu-id="a6298-232">parameters</span></span> |<span data-ttu-id="a6298-233">Paramètres du script U-SQL</span><span class="sxs-lookup"><span data-stu-id="a6298-233">Parameters for the U-SQL script</span></span> |<span data-ttu-id="a6298-234">Non</span><span class="sxs-lookup"><span data-stu-id="a6298-234">No</span></span> |
| <span data-ttu-id="a6298-235">runtimeVersion</span><span class="sxs-lookup"><span data-stu-id="a6298-235">runtimeVersion</span></span> | <span data-ttu-id="a6298-236">Version du runtime du moteur U-SQL à utiliser</span><span class="sxs-lookup"><span data-stu-id="a6298-236">Runtime version of the U-SQL engine to use</span></span> | <span data-ttu-id="a6298-237">Non</span><span class="sxs-lookup"><span data-stu-id="a6298-237">No</span></span> | 
| <span data-ttu-id="a6298-238">compilationMode</span><span class="sxs-lookup"><span data-stu-id="a6298-238">compilationMode</span></span> | <p><span data-ttu-id="a6298-239">Mode de compilation d’U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a6298-239">Compilation mode of U-SQL.</span></span> <span data-ttu-id="a6298-240">Doit avoir l’une des valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="a6298-240">Must be one of these values:</span></span></p> <ul><li><span data-ttu-id="a6298-241">**Semantic :** exécuter uniquement les vérifications sémantiques et les contrôles d’intégrité nécessaires.</span><span class="sxs-lookup"><span data-stu-id="a6298-241">**Semantic:** Only perform semantic checks and necessary sanity checks.</span></span></li><li><span data-ttu-id="a6298-242">**Full :** effectuer la compilation complète, y compris la vérification de la syntaxe, l’optimisation, la génération de code, etc.</span><span class="sxs-lookup"><span data-stu-id="a6298-242">**Full:** Perform the full compilation, including syntax check, optimization, code generation, etc.</span></span></li><li><span data-ttu-id="a6298-243">**SingleBox :** effectuer la compilation complète, avec le paramètre TargetType défini sur SingleBox.</span><span class="sxs-lookup"><span data-stu-id="a6298-243">**SingleBox:** Perform the full compilation, with TargetType setting to SingleBox.</span></span></li></ul><p><span data-ttu-id="a6298-244">Si vous ne spécifiez pas de valeur pour cette propriété, le serveur détermine le mode de compilation optimal.</span><span class="sxs-lookup"><span data-stu-id="a6298-244">If you don't specify a value for this property, the server determines the optimal compilation mode.</span></span> </p>| <span data-ttu-id="a6298-245">Non</span><span class="sxs-lookup"><span data-stu-id="a6298-245">No</span></span> | 

<span data-ttu-id="a6298-246">Vous trouverez la définition du script dans la section [Définition du script SearchLogProcessing.txt](#sample-u-sql-script) .</span><span class="sxs-lookup"><span data-stu-id="a6298-246">See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for the script definition.</span></span> 

## <a name="sample-input-and-output-datasets"></a><span data-ttu-id="a6298-247">Exemples de jeux de données d'entrée et de sortie</span><span class="sxs-lookup"><span data-stu-id="a6298-247">Sample input and output datasets</span></span>
### <a name="input-dataset"></a><span data-ttu-id="a6298-248">Jeu de données d'entrée</span><span class="sxs-lookup"><span data-stu-id="a6298-248">Input dataset</span></span>
<span data-ttu-id="a6298-249">Dans cet exemple, les données d'entrée se trouvent dans un magasin Azure Data Lake (fichier SearchLog.tsv dans le dossier datalake/input).</span><span class="sxs-lookup"><span data-stu-id="a6298-249">In this example, the input data resides in an Azure Data Lake Store (SearchLog.tsv file in the datalake/input folder).</span></span> 

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

### <a name="output-dataset"></a><span data-ttu-id="a6298-250">Jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="a6298-250">Output dataset</span></span>
<span data-ttu-id="a6298-251">Dans cet exemple, les données de sortie générées par le script U-SQL sont stockées dans un magasin Azure Data Lake (dossier datalake/output).</span><span class="sxs-lookup"><span data-stu-id="a6298-251">In this example, the output data produced by the U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span></span> 

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

### <a name="sample-data-lake-store-linked-service"></a><span data-ttu-id="a6298-252">Exemple de service lié Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a6298-252">Sample Data Lake Store Linked Service</span></span>
<span data-ttu-id="a6298-253">Voici la définition de l’exemple de service lié Azure Data Lake Store utilisé par les jeux de données d’entrée/de sortie.</span><span class="sxs-lookup"><span data-stu-id="a6298-253">Here is the definition of the sample Azure Data Lake Store linked service used by the input/output datasets.</span></span> 

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

<span data-ttu-id="a6298-254">Consultez l’article [Déplacer des données vers et depuis Azure Data Lake Store](data-factory-azure-datalake-connector.md) pour obtenir une description des propriétés JSON.</span><span class="sxs-lookup"><span data-stu-id="a6298-254">See [Move data to and from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span></span> 

## <a name="sample-u-sql-script"></a><span data-ttu-id="a6298-255">Exemple de script SQL-U</span><span class="sxs-lookup"><span data-stu-id="a6298-255">Sample U-SQL Script</span></span>

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
    TO @out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

<span data-ttu-id="a6298-256">Les valeurs des paramètres **@in** et **@out** dans le script U-SQL sont passées dynamiquement par ADF en utilisant la section « parameters ».</span><span class="sxs-lookup"><span data-stu-id="a6298-256">The values for **@in** and **@out** parameters in the U-SQL script are passed dynamically by ADF using the ‘parameters’ section.</span></span> <span data-ttu-id="a6298-257">Consultez la section « parameters » dans la définition du pipeline.</span><span class="sxs-lookup"><span data-stu-id="a6298-257">See the ‘parameters’ section in the pipeline definition.</span></span>

<span data-ttu-id="a6298-258">Vous pouvez aussi spécifier d’autres propriétés comme degreeOfParallelism et priority dans votre définition de pipeline pour les travaux qui s’exécutent au niveau du service Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="a6298-258">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for the jobs that run on the Azure Data Lake Analytics service.</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="a6298-259">Paramètres dynamiques</span><span class="sxs-lookup"><span data-stu-id="a6298-259">Dynamic parameters</span></span>
<span data-ttu-id="a6298-260">Dans l’exemple de définition de pipeline, des valeurs codées en dur sont affectées aux paramètres de sortie.</span><span class="sxs-lookup"><span data-stu-id="a6298-260">In the sample pipeline definition, in and out parameters are assigned with hard-coded values.</span></span> 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

<span data-ttu-id="a6298-261">Il est possible d’utiliser des paramètres dynamiques à la place.</span><span class="sxs-lookup"><span data-stu-id="a6298-261">It is possible to use dynamic parameters instead.</span></span> <span data-ttu-id="a6298-262">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a6298-262">For example:</span></span> 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

<span data-ttu-id="a6298-263">Dans ce cas, les fichiers d’entrée sont toujours récupérés à partir du dossier /datalake/input et les fichiers de sortie sont générés dans le dossier /datalake/output.</span><span class="sxs-lookup"><span data-stu-id="a6298-263">In this case, input files are still picked up from the /datalake/input folder and output files are generated in the /datalake/output folder.</span></span> <span data-ttu-id="a6298-264">Les noms de fichiers sont dynamiques et basés sur l’heure de début de la tranche horaire.</span><span class="sxs-lookup"><span data-stu-id="a6298-264">The file names are dynamic based on the slice start time.</span></span>  

