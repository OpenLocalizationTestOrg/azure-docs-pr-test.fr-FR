---
title: "Copier des données vers et depuis Azure Data Lake Store | Microsoft Docs"
description: "Découvrez comment copier des données depuis et vers Data Lake Store à l’aide d’Azure Data Factory"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 11629fbc83f0554e2097eb4322701654c0bc2028
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="copy-data-to-and-from-data-lake-store-by-using-data-factory"></a><span data-ttu-id="3ca83-103">Copier des données depuis et vers Data Lake Store à l’aide de Data Factory</span><span class="sxs-lookup"><span data-stu-id="3ca83-103">Copy data to and from Data Lake Store by using Data Factory</span></span>
<span data-ttu-id="3ca83-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour déplacer des données vers ou à partir d’Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3ca83-104">This article explains how to use Copy Activity in Azure Data Factory to move data to and from Azure Data Lake Store.</span></span> <span data-ttu-id="3ca83-105">Il s’appuie sur l’article [Activités de déplacement des données](data-factory-data-movement-activities.md), une vue d’ensemble du déplacement de données avec l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="3ca83-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, an overview of data movement with Copy Activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="3ca83-106">Scénarios pris en charge</span><span class="sxs-lookup"><span data-stu-id="3ca83-106">Supported scenarios</span></span>
<span data-ttu-id="3ca83-107">Vous pouvez copier les données **à partir d’Azure Data Lake Store** dans les magasins de données suivants :</span><span class="sxs-lookup"><span data-stu-id="3ca83-107">You can copy data **from Azure Data Lake Store** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="3ca83-108">Vous pouvez copier les données des magasins de données suivants **dans Azure Data Lake Store** :</span><span class="sxs-lookup"><span data-stu-id="3ca83-108">You can copy data from the following data stores **to Azure Data Lake Store**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="3ca83-109">Créez un compte Data Lake Store avant de créer un pipeline avec activité de copie.</span><span class="sxs-lookup"><span data-stu-id="3ca83-109">Create a Data Lake Store account before creating a pipeline with Copy Activity.</span></span> <span data-ttu-id="3ca83-110">Pour plus d’informations, consultez [Prise en main d’Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3ca83-110">For more information, see [Get started with Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="3ca83-111">Types d’authentification pris en charge</span><span class="sxs-lookup"><span data-stu-id="3ca83-111">Supported authentication types</span></span>
<span data-ttu-id="3ca83-112">Le connecteur Data Lake Store prend en charge les types d’authentification suivants :</span><span class="sxs-lookup"><span data-stu-id="3ca83-112">The Data Lake Store connector supports these authentication types:</span></span>
* <span data-ttu-id="3ca83-113">Authentification d’un principal du service</span><span class="sxs-lookup"><span data-stu-id="3ca83-113">Service principal authentication</span></span>
* <span data-ttu-id="3ca83-114">Utilisation de l’authentification des informations d’identification utilisateur (OAuth)</span><span class="sxs-lookup"><span data-stu-id="3ca83-114">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="3ca83-115">Nous vous recommandons d’utiliser l’authentification de principal du service, en particulier pour une copie planifiée des données.</span><span class="sxs-lookup"><span data-stu-id="3ca83-115">We recommend that you use service principal authentication, especially for a scheduled data copy.</span></span> <span data-ttu-id="3ca83-116">Un comportement d’expiration de jeton peut se produire avec l’authentification par informations d’identification utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3ca83-116">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="3ca83-117">Pour les détails de configuration, consultez la section [Propriétés du service lié](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3ca83-117">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>

## <a name="get-started"></a><span data-ttu-id="3ca83-118">Prise en main</span><span class="sxs-lookup"><span data-stu-id="3ca83-118">Get started</span></span>
<span data-ttu-id="3ca83-119">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers ou à partir d’Azure Data Lake Store à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="3ca83-119">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span></span>

<span data-ttu-id="3ca83-120">Le moyen le plus simple de créer un pipeline pour copier des données consiste à utiliser **l’Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="3ca83-120">The easiest way to create a pipeline to copy data is to use the **Copy Wizard**.</span></span> <span data-ttu-id="3ca83-121">Consultez la page [Didacticiel : Créer un pipeline à l’aide de l’Assistant de copie](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant Copier.</span><span class="sxs-lookup"><span data-stu-id="3ca83-121">For a tutorial on creating a pipeline by using the Copy Wizard, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="3ca83-122">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="3ca83-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="3ca83-123">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="3ca83-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="3ca83-124">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="3ca83-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="3ca83-125">Création d'une **fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="3ca83-125">Create a **data factory**.</span></span> <span data-ttu-id="3ca83-126">Une fabrique de données peut contenir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="3ca83-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="3ca83-127">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="3ca83-127">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="3ca83-128">Par exemple, si vous copiez des données d’un stockage Blob Azure dans Azure Data Lake Store, vous créez deux services liés pour lier votre compte de stockage Azure et Azure Data Lake Store à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="3ca83-128">For example, if you are copying data from an Azure blob storage to an Azure Data Lake Store, you create two linked services to link your Azure storage account and Azure Data Lake store to your data factory.</span></span> <span data-ttu-id="3ca83-129">Pour plus d’informations sur les propriétés de service lié qui sont spécifiques à Azure Data Lake Store, consultez la section [Propriétés du service lié](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3ca83-129">For linked service properties that are specific to Azure Data Lake Store, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="3ca83-130">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="3ca83-130">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="3ca83-131">Dans l’exemple mentionné à la dernière étape, vous créez un jeu de données pour spécifier le conteneur d’objets blob et le dossier qui contient les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="3ca83-131">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="3ca83-132">Ensuite, vous créez un autre jeu de données pour spécifier le chemin du dossier/fichier dans l’instance de Data Lake Store qui contient les données copiées à partir du stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="3ca83-132">And, you create another dataset to specify the folder and file path in the Data Lake store that holds the data copied from the blob storage.</span></span> <span data-ttu-id="3ca83-133">Pour plus d’informations sur les propriétés de jeu de données qui sont spécifiques à Azure Data Lake Store, consultez la section [Propriétés du jeu de données](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3ca83-133">For dataset properties that are specific to Azure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="3ca83-134">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="3ca83-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="3ca83-135">Dans l’exemple mentionné plus haut, vous utilisez BlobSource comme source et AzureDataLakeStoreSink comme récepteur pour l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="3ca83-135">In the example mentioned earlier, you use BlobSource as a source and AzureDataLakeStoreSink as a sink for the copy activity.</span></span> <span data-ttu-id="3ca83-136">De la même façon, si vous copiez des données d’Azure Data Lake Store vers le stockage Blob Azure, vous utilisez AzureDataLakeStoreSource et BlobSink dans l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="3ca83-136">Similarly, if you are copying from Azure Data Lake Store to Azure Blob Storage, you use AzureDataLakeStoreSource  and BlobSink in the copy activity.</span></span> <span data-ttu-id="3ca83-137">Pour plus d’informations sur les propriétés de l’activité de copie qui sont spécifiques à Azure Data Lake Store, consultez la section [Propriétés de l’activité de copie](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="3ca83-137">For copy activity properties that are specific to Azure Data Lake Store, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="3ca83-138">Pour plus d’informations sur l’utilisation d’un magasin de données en tant que source ou que récepteur, cliquez sur le lien correspondant à votre magasin de données dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="3ca83-138">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>  

<span data-ttu-id="3ca83-139">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="3ca83-139">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="3ca83-140">Lorsque vous utilisez les outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory à l’aide du format JSON.</span><span class="sxs-lookup"><span data-stu-id="3ca83-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="3ca83-141">Pour obtenir des exemples comportant des définitions JSON pour les entités Data Factory utilisées pour copier les données vers ou à partir d’Azure Data Lake Store, consultez la section [Exemples JSON](#json-examples-for-copying-data-to-and-from-data-lake-store) de cet article.</span><span class="sxs-lookup"><span data-stu-id="3ca83-141">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples-for-copying-data-to-and-from-data-lake-store) section of this article.</span></span>

<span data-ttu-id="3ca83-142">Les sections suivantes offrent des informations détaillées sur les propriétés JSON utilisées pour définir les entités Data Factory propres à Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3ca83-142">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Data Lake Store.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="3ca83-143">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="3ca83-143">Linked service properties</span></span>
<span data-ttu-id="3ca83-144">Un service lié lie un magasin de données à une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="3ca83-144">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="3ca83-145">Pour lier votre magasin de données Data Lake Store à votre fabrique de données, vous devez créer un service lié de type **AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="3ca83-145">You create a linked service of type **AzureDataLakeStore** to link your Data Lake Store data to your data factory.</span></span> <span data-ttu-id="3ca83-146">Le tableau suivant décrit les éléments JSON spécifiques pour des services Data Lake Store liés.</span><span class="sxs-lookup"><span data-stu-id="3ca83-146">The following table describes JSON elements specific to Data Lake Store linked services.</span></span> <span data-ttu-id="3ca83-147">Vous pouvez choisir entre une authentification par principal de service et par informations d’identification utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3ca83-147">You can choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="3ca83-148">Propriété</span><span class="sxs-lookup"><span data-stu-id="3ca83-148">Property</span></span> | <span data-ttu-id="3ca83-149">Description</span><span class="sxs-lookup"><span data-stu-id="3ca83-149">Description</span></span> | <span data-ttu-id="3ca83-150">Requis</span><span class="sxs-lookup"><span data-stu-id="3ca83-150">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3ca83-151">**type**</span><span class="sxs-lookup"><span data-stu-id="3ca83-151">**type**</span></span> | <span data-ttu-id="3ca83-152">La propriété type doit être définie sur : **AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="3ca83-152">The type property must be set to **AzureDataLakeStore**.</span></span> | <span data-ttu-id="3ca83-153">Oui</span><span class="sxs-lookup"><span data-stu-id="3ca83-153">Yes</span></span> |
| <span data-ttu-id="3ca83-154">**dataLakeStoreUri**</span><span class="sxs-lookup"><span data-stu-id="3ca83-154">**dataLakeStoreUri**</span></span> | <span data-ttu-id="3ca83-155">Informations à propos du compte Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3ca83-155">Information about the Azure Data Lake Store account.</span></span> <span data-ttu-id="3ca83-156">Cette information prend un des formats suivants : `https://[accountname].azuredatalakestore.net/webhdfs/v1` ou `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="3ca83-156">This information takes one of the following formats: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="3ca83-157">Oui</span><span class="sxs-lookup"><span data-stu-id="3ca83-157">Yes</span></span> |
| <span data-ttu-id="3ca83-158">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="3ca83-158">**subscriptionId**</span></span> | <span data-ttu-id="3ca83-159">ID d’abonnement Azure auquel appartient le compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3ca83-159">Azure subscription ID to which the Data Lake Store account belongs.</span></span> | <span data-ttu-id="3ca83-160">Requis pour le récepteur</span><span class="sxs-lookup"><span data-stu-id="3ca83-160">Required for sink</span></span> |
| <span data-ttu-id="3ca83-161">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="3ca83-161">**resourceGroupName**</span></span> | <span data-ttu-id="3ca83-162">Nom du groupe de ressources Azure auquel appartient le compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3ca83-162">Azure resource group name to which the Data Lake Store account belongs.</span></span> | <span data-ttu-id="3ca83-163">Requis pour le récepteur</span><span class="sxs-lookup"><span data-stu-id="3ca83-163">Required for sink</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="3ca83-164">Authentification d’un principal du service (recommandée)</span><span class="sxs-lookup"><span data-stu-id="3ca83-164">Service principal authentication (recommended)</span></span>
<span data-ttu-id="3ca83-165">Pour utiliser l’authentification d’un principal du service, inscrivez une entité d’application dans Azure Active Directory (Azure AD) et lui accorder l’accès à Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3ca83-165">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to Data Lake Store.</span></span> <span data-ttu-id="3ca83-166">Consultez la page [Authentification de service à service](../data-lake-store/data-lake-store-authenticate-using-active-directory.md) pour des instructions détaillées.</span><span class="sxs-lookup"><span data-stu-id="3ca83-166">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="3ca83-167">Prenez note des valeurs suivantes, qui vous permettent de définir le service lié :</span><span class="sxs-lookup"><span data-stu-id="3ca83-167">Make note of the following values, which you use to define the linked service:</span></span>
* <span data-ttu-id="3ca83-168">ID de l'application</span><span class="sxs-lookup"><span data-stu-id="3ca83-168">Application ID</span></span>
* <span data-ttu-id="3ca83-169">Clé de l'application</span><span class="sxs-lookup"><span data-stu-id="3ca83-169">Application key</span></span> 
* <span data-ttu-id="3ca83-170">ID client</span><span class="sxs-lookup"><span data-stu-id="3ca83-170">Tenant ID</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3ca83-171">Si vous utilisez l’Assistant Copie dans le cadre de la création de pipelines de données, veillez à accorder au principal du service au minimum le rôle **Lecteur** dans Access Control (gestion des accès et identités) pour le compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3ca83-171">If you are using the Copy Wizard to author data pipelines, make sure that you grant the service principal at least a **Reader** role in access control (identity and access management) for the Data Lake Store account.</span></span> <span data-ttu-id="3ca83-172">En outre, accordez au moins au principal du service l’autorisation **lecture + exécution** sur la racine de Data Lake Store (« / ») et ses enfants.</span><span class="sxs-lookup"><span data-stu-id="3ca83-172">Also, grant the service principal at least **Read + Execute** permission to your Data Lake Store root ("/") and its children.</span></span> <span data-ttu-id="3ca83-173">Sinon, le message « Les informations d’identification fournies ne sont pas valides » peut s’afficher.</span><span class="sxs-lookup"><span data-stu-id="3ca83-173">Otherwise you might see the message "The credentials provided are invalid."</span></span><br/><br/>
<span data-ttu-id="3ca83-174">Une fois que vous créez ou mettez à jour un principal de service dans Azure AD, il peut falloir quelques minutes avant que les modifications entrent en vigueur.</span><span class="sxs-lookup"><span data-stu-id="3ca83-174">After you create or update a service principal in Azure AD, it can take a few minutes for the changes to take effect.</span></span> <span data-ttu-id="3ca83-175">Vérifiez la configuration des ACL du principal de service et de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3ca83-175">Check the service principal and Data Lake Store access control list (ACL) configurations.</span></span> <span data-ttu-id="3ca83-176">Si vous voyez toujours le message « Les informations d’identification fournies ne sont pas valides », attendez un moment et réessayez.</span><span class="sxs-lookup"><span data-stu-id="3ca83-176">If you still see the message "The credentials provided are invalid," wait a while and try again.</span></span>

<span data-ttu-id="3ca83-177">Utilisez l’authentification par principal de service en spécifiant les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="3ca83-177">Use service principal authentication by specifying the following properties:</span></span>

| <span data-ttu-id="3ca83-178">Propriété</span><span class="sxs-lookup"><span data-stu-id="3ca83-178">Property</span></span> | <span data-ttu-id="3ca83-179">Description</span><span class="sxs-lookup"><span data-stu-id="3ca83-179">Description</span></span> | <span data-ttu-id="3ca83-180">Requis</span><span class="sxs-lookup"><span data-stu-id="3ca83-180">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3ca83-181">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="3ca83-181">**servicePrincipalId**</span></span> | <span data-ttu-id="3ca83-182">Spécifiez l’ID client de l’application.</span><span class="sxs-lookup"><span data-stu-id="3ca83-182">Specify the application's client ID.</span></span> | <span data-ttu-id="3ca83-183">Oui</span><span class="sxs-lookup"><span data-stu-id="3ca83-183">Yes</span></span> |
| <span data-ttu-id="3ca83-184">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="3ca83-184">**servicePrincipalKey**</span></span> | <span data-ttu-id="3ca83-185">Spécifiez la clé de l’application.</span><span class="sxs-lookup"><span data-stu-id="3ca83-185">Specify the application's key.</span></span> | <span data-ttu-id="3ca83-186">Oui</span><span class="sxs-lookup"><span data-stu-id="3ca83-186">Yes</span></span> |
| <span data-ttu-id="3ca83-187">**client**</span><span class="sxs-lookup"><span data-stu-id="3ca83-187">**tenant**</span></span> | <span data-ttu-id="3ca83-188">Spécifiez les informations de locataire (nom de domaine ou ID de locataire) dans lesquels se trouve votre application.</span><span class="sxs-lookup"><span data-stu-id="3ca83-188">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="3ca83-189">Vous pouvez le récupérer en pointant la souris dans le coin supérieur droit du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3ca83-189">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span></span> | <span data-ttu-id="3ca83-190">Oui</span><span class="sxs-lookup"><span data-stu-id="3ca83-190">Yes</span></span> |

<span data-ttu-id="3ca83-191">**Exemple : authentification du principal de service**</span><span class="sxs-lookup"><span data-stu-id="3ca83-191">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="3ca83-192">Authentification des informations d’identification utilisateur</span><span class="sxs-lookup"><span data-stu-id="3ca83-192">User credential authentication</span></span>
<span data-ttu-id="3ca83-193">Vous pouvez également utiliser l’authentification des informations d’identification utilisateur pour la copie vers ou à partir de Data Lake Store en spécifiant les propriétés ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3ca83-193">Alternatively, you can use user credential authentication to copy from or to Data Lake Store by specifying the following properties:</span></span>

| <span data-ttu-id="3ca83-194">Propriété</span><span class="sxs-lookup"><span data-stu-id="3ca83-194">Property</span></span> | <span data-ttu-id="3ca83-195">Description</span><span class="sxs-lookup"><span data-stu-id="3ca83-195">Description</span></span> | <span data-ttu-id="3ca83-196">Requis</span><span class="sxs-lookup"><span data-stu-id="3ca83-196">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3ca83-197">**authorization**</span><span class="sxs-lookup"><span data-stu-id="3ca83-197">**authorization**</span></span> | <span data-ttu-id="3ca83-198">Cliquez sur le bouton **Autoriser** dans Data Factory Editor et saisissez vos informations d’identification, ce qui affecte l’URL d’autorisation générée automatiquement à cette propriété.</span><span class="sxs-lookup"><span data-stu-id="3ca83-198">Click the **Authorize** button in the Data Factory Editor and enter your credential that assigns the autogenerated authorization URL to this property.</span></span> | <span data-ttu-id="3ca83-199">Oui</span><span class="sxs-lookup"><span data-stu-id="3ca83-199">Yes</span></span> |
| <span data-ttu-id="3ca83-200">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="3ca83-200">**sessionId**</span></span> | <span data-ttu-id="3ca83-201">ID de session OAuth issu de la session d’autorisation OAuth.</span><span class="sxs-lookup"><span data-stu-id="3ca83-201">OAuth session ID from the OAuth authorization session.</span></span> <span data-ttu-id="3ca83-202">Chaque ID de session est unique et ne peut être utilisé qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="3ca83-202">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="3ca83-203">Ce paramètre est généré automatiquement lorsque vous utilisez Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="3ca83-203">This setting is automatically generated when you use the Data Factory Editor.</span></span> | <span data-ttu-id="3ca83-204">Oui</span><span class="sxs-lookup"><span data-stu-id="3ca83-204">Yes</span></span> |

<span data-ttu-id="3ca83-205">**Exemple : authentification des informations d’identification utilisateur**</span><span class="sxs-lookup"><span data-stu-id="3ca83-205">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="3ca83-206">Expiration du jeton</span><span class="sxs-lookup"><span data-stu-id="3ca83-206">Token expiration</span></span>
<span data-ttu-id="3ca83-207">Le code d’autorisation que vous générez à l’aide du bouton **Autoriser** expire au bout d’un certain temps.</span><span class="sxs-lookup"><span data-stu-id="3ca83-207">The authorization code that you generate by using the **Authorize** button expires after a certain amount of time.</span></span> <span data-ttu-id="3ca83-208">Le message suivant signifie que le jeton d’authentification a expiré :</span><span class="sxs-lookup"><span data-stu-id="3ca83-208">The following message means that the authentication token has expired:</span></span>

<span data-ttu-id="3ca83-209">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span><span class="sxs-lookup"><span data-stu-id="3ca83-209">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="3ca83-210">AADSTS70008: The provided access grant is expired or revoked.</span><span class="sxs-lookup"><span data-stu-id="3ca83-210">AADSTS70008: The provided access grant is expired or revoked.</span></span> <span data-ttu-id="3ca83-211">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span><span class="sxs-lookup"><span data-stu-id="3ca83-211">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span></span>

<span data-ttu-id="3ca83-212">Le tableau suivant présente les délais d’expiration associés aux différents types de comptes d’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="3ca83-212">The following table shows the expiration times of different types of user accounts:</span></span>


| <span data-ttu-id="3ca83-213">Type d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="3ca83-213">User type</span></span> | <span data-ttu-id="3ca83-214">Expire après</span><span class="sxs-lookup"><span data-stu-id="3ca83-214">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="3ca83-215">Comptes d’utilisateurs *non* gérés par Azure Active Directory (par exemple @hotmail.com ou @live.com)</span><span class="sxs-lookup"><span data-stu-id="3ca83-215">User accounts *not* managed by Azure Active Directory (for example, @hotmail.com or @live.com)</span></span> |<span data-ttu-id="3ca83-216">12 heures</span><span class="sxs-lookup"><span data-stu-id="3ca83-216">12 hours</span></span> |
| <span data-ttu-id="3ca83-217">Comptes d’utilisateurs gérés par Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3ca83-217">Users accounts managed by Azure Active Directory</span></span> |<span data-ttu-id="3ca83-218">14 jours après la dernière exécution de tranche de données</span><span class="sxs-lookup"><span data-stu-id="3ca83-218">14 days after the last slice run</span></span> <br/><br/><span data-ttu-id="3ca83-219">90 jours, si une tranche basée sur un service lié OAuth est exécutée au moins une fois tous les 14 jours</span><span class="sxs-lookup"><span data-stu-id="3ca83-219">90 days, if a slice based on an OAuth-based linked service runs at least once every 14 days</span></span> |

<span data-ttu-id="3ca83-220">Si vous modifiez votre mot de passe avant cette date d’expiration du jeton, le jeton expirera immédiatement.</span><span class="sxs-lookup"><span data-stu-id="3ca83-220">If you change your password before the token expiration time, the token expires immediately.</span></span> <span data-ttu-id="3ca83-221">Vous verrez le message mentionné précédemment dans cette section.</span><span class="sxs-lookup"><span data-stu-id="3ca83-221">You will see the message mentioned earlier in this section.</span></span>

<span data-ttu-id="3ca83-222">Vous pouvez autoriser à nouveau le compte à l’aide du bouton **Autoriser** à l’expiration du jeton, puis redéployer le service lié.</span><span class="sxs-lookup"><span data-stu-id="3ca83-222">You can reauthorize the account by using the **Authorize** button when the token expires to redeploy the linked service.</span></span> <span data-ttu-id="3ca83-223">Vous pouvez également générer des valeurs pour les propriétés **sessionId** et **authorization** à l’aide du code suivant :</span><span class="sxs-lookup"><span data-stu-id="3ca83-223">You can also generate values for the **sessionId** and **authorization** properties programmatically by using the following code:</span></span>


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
<span data-ttu-id="3ca83-224">Pour plus d’informations sur les classes Data Factory utilisées dans le code, consultez les rubriques [AzureDataLakeStoreLinkedService, classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService, classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx) et [AuthorizationSessionGetResponse, classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx).</span><span class="sxs-lookup"><span data-stu-id="3ca83-224">For details about the Data Factory classes used in the code, see the [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics.</span></span> <span data-ttu-id="3ca83-225">Ajoutez une référence à la version `2.9.10826.1824` de `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` pour la classe `WindowsFormsWebAuthenticationDialog` utilisée dans le code.</span><span class="sxs-lookup"><span data-stu-id="3ca83-225">Add a reference to version `2.9.10826.1824` of `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` for the `WindowsFormsWebAuthenticationDialog` class used in the code.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="3ca83-226">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="3ca83-226">Dataset properties</span></span>
<span data-ttu-id="3ca83-227">Pour spécifier un jeu de données afin de représenter les données d’entrée dans un Data Lake Store, vous devez définir la propriété **type** du jeu de données sur **AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="3ca83-227">To specify a dataset to represent input data in a Data Lake Store, you set the **type** property of the dataset to **AzureDataLakeStore**.</span></span> <span data-ttu-id="3ca83-228">Définissez la propriété **linkedServiceName** du jeu de données sur le nom du service lié Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3ca83-228">Set the **linkedServiceName** property of the dataset to the name of the Data Lake Store linked service.</span></span> <span data-ttu-id="3ca83-229">Pour obtenir une liste complète des sections et propriétés JSON disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="3ca83-229">For a full list of JSON sections and properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="3ca83-230">Les sections d’un jeu de données en JSON, comme la **structure**, la **disponibilité** et la **stratégie** sont similaires pour tous les types de jeux de données (par exemple, Azure SQL Database, Azure Blob et Azure Table).</span><span class="sxs-lookup"><span data-stu-id="3ca83-230">Sections of a dataset in JSON, such as **structure**, **availability**, and **policy**, are similar for all dataset types (Azure SQL database, Azure blob, and Azure table, for example).</span></span> <span data-ttu-id="3ca83-231">La section **typeProperties** est différente pour chaque type de jeu de données et fournit des informations notamment sur l'emplacement et le format des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="3ca83-231">The **typeProperties** section is different for each type of dataset and provides information such as location and format of the data in the data store.</span></span> 

<span data-ttu-id="3ca83-232">La section **typeProperties** correspondant au jeu de données de type **AzureDataLakeStore** contient les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="3ca83-232">The **typeProperties** section for a dataset of type **AzureDataLakeStore** contains the following properties:</span></span>

| <span data-ttu-id="3ca83-233">Propriété</span><span class="sxs-lookup"><span data-stu-id="3ca83-233">Property</span></span> | <span data-ttu-id="3ca83-234">Description</span><span class="sxs-lookup"><span data-stu-id="3ca83-234">Description</span></span> | <span data-ttu-id="3ca83-235">Requis</span><span class="sxs-lookup"><span data-stu-id="3ca83-235">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3ca83-236">**folderPath**</span><span class="sxs-lookup"><span data-stu-id="3ca83-236">**folderPath**</span></span> |<span data-ttu-id="3ca83-237">Chemin d’accès au conteneur et au dossier dans Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3ca83-237">Path to the container and folder in Data Lake Store.</span></span> |<span data-ttu-id="3ca83-238">Oui</span><span class="sxs-lookup"><span data-stu-id="3ca83-238">Yes</span></span> |
| <span data-ttu-id="3ca83-239">**fileName**</span><span class="sxs-lookup"><span data-stu-id="3ca83-239">**fileName**</span></span> |<span data-ttu-id="3ca83-240">Le nom du fichier dans Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3ca83-240">Name of the file in Azure Data Lake Store.</span></span> <span data-ttu-id="3ca83-241">La propriété **fileName** est facultative et sensible à la casse.</span><span class="sxs-lookup"><span data-stu-id="3ca83-241">The **fileName** property is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="3ca83-242">Si vous spécifiez **fileName**, l’activité (y compris la copie) fonctionne sur le fichier spécifique.</span><span class="sxs-lookup"><span data-stu-id="3ca83-242">If you specify **fileName**, the activity (including Copy) works on the specific file.</span></span><br/><br/><span data-ttu-id="3ca83-243">Lorsque **fileName** n’est pas spécifié, la copie inclut tous les fichiers dans le paramètre **folderPath** du jeu de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="3ca83-243">When **fileName** is not specified, Copy includes all files in **folderPath** in the input dataset.</span></span><br/><br/><span data-ttu-id="3ca83-244">Lorsque **fileName** n'est pas spécifié pour un jeu de données de sortie et que **preserveHierarchy** n’est pas spécifié dans le récepteur d’activité, le nom du fichier généré a le format Data._Guid_.txt\`.</span><span class="sxs-lookup"><span data-stu-id="3ca83-244">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file is in the format Data._Guid_.txt\`.</span></span> <span data-ttu-id="3ca83-245">Par exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span><span class="sxs-lookup"><span data-stu-id="3ca83-245">For example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span></span> |<span data-ttu-id="3ca83-246">Non</span><span class="sxs-lookup"><span data-stu-id="3ca83-246">No</span></span> |
| <span data-ttu-id="3ca83-247">**partitionedBy**</span><span class="sxs-lookup"><span data-stu-id="3ca83-247">**partitionedBy**</span></span> |<span data-ttu-id="3ca83-248">La propriété **partitionedBy** est facultative.</span><span class="sxs-lookup"><span data-stu-id="3ca83-248">The **partitionedBy** property is optional.</span></span> <span data-ttu-id="3ca83-249">Vous pouvez l'utiliser pour spécifier un chemin dynamique et le nom de fichier pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="3ca83-249">You can use it to specify a dynamic path and file name for time-series data.</span></span> <span data-ttu-id="3ca83-250">Par exemple, **folderPath** peut être paramétré pour toutes les heures de données.</span><span class="sxs-lookup"><span data-stu-id="3ca83-250">For example, **folderPath** can be parameterized for every hour of data.</span></span> <span data-ttu-id="3ca83-251">Consultez [La propriété partitionedBy](#using-partitionedby-property) pour obtenir plus d’informations et des exemples.</span><span class="sxs-lookup"><span data-stu-id="3ca83-251">For details and examples, see [The partitionedBy property](#using-partitionedby-property).</span></span> |<span data-ttu-id="3ca83-252">Non</span><span class="sxs-lookup"><span data-stu-id="3ca83-252">No</span></span> |
| <span data-ttu-id="3ca83-253">**format**</span><span class="sxs-lookup"><span data-stu-id="3ca83-253">**format**</span></span> | <span data-ttu-id="3ca83-254">Les types de formats suivants sont pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** et **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="3ca83-254">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span></span> <span data-ttu-id="3ca83-255">Définissez la propriété **type** située sous **Format** sur l’une de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="3ca83-255">Set the **type** property under **format** to one of these values.</span></span> <span data-ttu-id="3ca83-256">Pour en savoir plus, voir les sections [Format Text](data-factory-supported-file-and-compression-formats.md#text-format), [Format JSON](data-factory-supported-file-and-compression-formats.md#json-format), [Format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [Format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format) dans l’article [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="3ca83-256">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections in the [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span> <br><br> <span data-ttu-id="3ca83-257">Si vous souhaitez copier des fichiers en l’état entre des magasins de fichiers (copie binaire), ignorez la section `format` dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="3ca83-257">If you want to copy files "as-is" between file-based stores (binary copy), skip the `format` section in both input and output dataset definitions.</span></span> |<span data-ttu-id="3ca83-258">Non</span><span class="sxs-lookup"><span data-stu-id="3ca83-258">No</span></span> |
| <span data-ttu-id="3ca83-259">**compression**</span><span class="sxs-lookup"><span data-stu-id="3ca83-259">**compression**</span></span> | <span data-ttu-id="3ca83-260">Spécifiez le type et le niveau de compression pour les données.</span><span class="sxs-lookup"><span data-stu-id="3ca83-260">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="3ca83-261">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="3ca83-261">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="3ca83-262">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="3ca83-262">Supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="3ca83-263">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="3ca83-263">For more information, see [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="3ca83-264">Non</span><span class="sxs-lookup"><span data-stu-id="3ca83-264">No</span></span> |

### <a name="the-partitionedby-property"></a><span data-ttu-id="3ca83-265">La propriété partitionedBy</span><span class="sxs-lookup"><span data-stu-id="3ca83-265">The partitionedBy property</span></span>
<span data-ttu-id="3ca83-266">Vous pouvez spécifier des propriétés **folderPath** et un **fileName** dynamiques pour les données de série chronologique avec la propriété **partitionedBy**, les fonctions Data Factory et les variables système.</span><span class="sxs-lookup"><span data-stu-id="3ca83-266">You can specify dynamic **folderPath** and **fileName** properties for time-series data with the **partitionedBy** property, Data Factory functions, and system variables.</span></span> <span data-ttu-id="3ca83-267">Pour plus de détails, consultez l’article [Azure Data Factory - Variables système et fonctions](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="3ca83-267">For details, see the [Azure Data Factory - functions and system variables](data-factory-functions-variables.md) article.</span></span>


<span data-ttu-id="3ca83-268">Dans l’exemple suivant, `{Slice}` est remplacé par la valeur de la variable système Data Factory `SliceStart` au format spécifié (`yyyyMMddHH`).</span><span class="sxs-lookup"><span data-stu-id="3ca83-268">In the following example, `{Slice}` is replaced with the value of the Data Factory system variable `SliceStart` in the format specified (`yyyyMMddHH`).</span></span> <span data-ttu-id="3ca83-269">Le nom `SliceStart` fait référence à l’heure de début de la tranche.</span><span class="sxs-lookup"><span data-stu-id="3ca83-269">The name `SliceStart` refers to the start time of the slice.</span></span> <span data-ttu-id="3ca83-270">La propriété `folderPath` est différente pour chaque secteur, comme dans `wikidatagateway/wikisampledataout/2014100103` ou `wikidatagateway/wikisampledataout/2014100104`.</span><span class="sxs-lookup"><span data-stu-id="3ca83-270">The `folderPath` property is different for each slice, as in `wikidatagateway/wikisampledataout/2014100103` or `wikidatagateway/wikisampledataout/2014100104`.</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="3ca83-271">Dans l’exemple suivant, l’année, le mois, le jour et l’heure de `SliceStart` sont extraits dans des variables distinctes qui sont utilisées par les propriétés `folderPath` et `fileName` :</span><span class="sxs-lookup"><span data-stu-id="3ca83-271">In the following example, the year, month, day, and time of `SliceStart` are extracted into separate variables that are used by the `folderPath` and `fileName` properties:</span></span>
```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="3ca83-272">Consultez les articles [Jeux de données dans Azure Data Factory](data-factory-create-datasets.md) et [Planification et exécution dans Data Factory](data-factory-scheduling-and-execution.md) pour mieux comprendre les jeux de données de série chronologique, la planification et les segments.</span><span class="sxs-lookup"><span data-stu-id="3ca83-272">For more details on time-series datasets, scheduling, and slices, see the [Datasets in Azure Data Factory](data-factory-create-datasets.md) and [Data Factory scheduling and execution](data-factory-scheduling-and-execution.md) articles.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="3ca83-273">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="3ca83-273">Copy activity properties</span></span>
<span data-ttu-id="3ca83-274">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="3ca83-274">For a full list of sections and properties available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="3ca83-275">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="3ca83-275">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="3ca83-276">Les propriétés disponibles dans la section **typeProperties** d’une activité varient pour chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="3ca83-276">The properties available in the **typeProperties** section of an activity vary with each activity type.</span></span> <span data-ttu-id="3ca83-277">Pour une activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="3ca83-277">For a copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="3ca83-278">**AzureDataLakeStoreSource** prend en charge les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="3ca83-278">**AzureDataLakeStoreSource** supports the following property in the **typeProperties** section:</span></span>

| <span data-ttu-id="3ca83-279">Propriété</span><span class="sxs-lookup"><span data-stu-id="3ca83-279">Property</span></span> | <span data-ttu-id="3ca83-280">Description</span><span class="sxs-lookup"><span data-stu-id="3ca83-280">Description</span></span> | <span data-ttu-id="3ca83-281">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="3ca83-281">Allowed values</span></span> | <span data-ttu-id="3ca83-282">Requis</span><span class="sxs-lookup"><span data-stu-id="3ca83-282">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3ca83-283">**recursive**</span><span class="sxs-lookup"><span data-stu-id="3ca83-283">**recursive**</span></span> |<span data-ttu-id="3ca83-284">Indique si les données sont lues de manière récursive à partir des sous-dossiers ou uniquement du dossier spécifié.</span><span class="sxs-lookup"><span data-stu-id="3ca83-284">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="3ca83-285">True (valeur par défaut), False</span><span class="sxs-lookup"><span data-stu-id="3ca83-285">True (default value), False</span></span> |<span data-ttu-id="3ca83-286">Non</span><span class="sxs-lookup"><span data-stu-id="3ca83-286">No</span></span> |


<span data-ttu-id="3ca83-287">**AzureDataLakeStoreSink** prend en charge les propriétés suivantes dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="3ca83-287">**AzureDataLakeStoreSink** supports the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="3ca83-288">Propriété</span><span class="sxs-lookup"><span data-stu-id="3ca83-288">Property</span></span> | <span data-ttu-id="3ca83-289">Description</span><span class="sxs-lookup"><span data-stu-id="3ca83-289">Description</span></span> | <span data-ttu-id="3ca83-290">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="3ca83-290">Allowed values</span></span> | <span data-ttu-id="3ca83-291">Requis</span><span class="sxs-lookup"><span data-stu-id="3ca83-291">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3ca83-292">**copyBehavior**</span><span class="sxs-lookup"><span data-stu-id="3ca83-292">**copyBehavior**</span></span> |<span data-ttu-id="3ca83-293">Spécifie le comportement de copie.</span><span class="sxs-lookup"><span data-stu-id="3ca83-293">Specifies the copy behavior.</span></span> |<span data-ttu-id="3ca83-294"><b>PreserveHierarchy</b> : conserve la hiérarchie des fichiers dans le dossier cible.</span><span class="sxs-lookup"><span data-stu-id="3ca83-294"><b>PreserveHierarchy</b>: Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="3ca83-295">Le chemin d’accès relatif du fichier source vers le dossier source est identique au chemin d’accès relatif du fichier cible vers le dossier cible.</span><span class="sxs-lookup"><span data-stu-id="3ca83-295">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="3ca83-296"><b>FlattenHierarchy</b>: tous les fichiers du dossier source sont créés dans le premier niveau du dossier cible.</span><span class="sxs-lookup"><span data-stu-id="3ca83-296"><b>FlattenHierarchy</b>: All files from the source folder are created in the first level of the target folder.</span></span> <span data-ttu-id="3ca83-297">Les fichiers cibles sont créés avec un nom généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="3ca83-297">The target files are created with autogenerated names.</span></span><br/><br/><span data-ttu-id="3ca83-298"><b>MergeFiles</b> : fusionne tous les fichiers du dossier source dans un même fichier.</span><span class="sxs-lookup"><span data-stu-id="3ca83-298"><b>MergeFiles</b>: Merges all files from the source folder to one file.</span></span> <span data-ttu-id="3ca83-299">Si le nom d’objet blob ou de fichier est spécifié, le nom de fichier fusionné est le nom spécifié.</span><span class="sxs-lookup"><span data-stu-id="3ca83-299">If the file or blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="3ca83-300">Dans le cas contraire, le nom de fichier est généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="3ca83-300">Otherwise, the file name is autogenerated.</span></span> |<span data-ttu-id="3ca83-301">Non</span><span class="sxs-lookup"><span data-stu-id="3ca83-301">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="3ca83-302">exemples de valeurs recursive et copyBehavior</span><span class="sxs-lookup"><span data-stu-id="3ca83-302">recursive and copyBehavior examples</span></span>
<span data-ttu-id="3ca83-303">Cette section décrit le comportement résultant de l’opération de copie pour différentes combinaisons de valeurs recursive et copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="3ca83-303">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="3ca83-304">recursive</span><span class="sxs-lookup"><span data-stu-id="3ca83-304">recursive</span></span> | <span data-ttu-id="3ca83-305">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="3ca83-305">copyBehavior</span></span> | <span data-ttu-id="3ca83-306">Comportement résultant</span><span class="sxs-lookup"><span data-stu-id="3ca83-306">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3ca83-307">true</span><span class="sxs-lookup"><span data-stu-id="3ca83-307">true</span></span> |<span data-ttu-id="3ca83-308">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="3ca83-308">preserveHierarchy</span></span> |<span data-ttu-id="3ca83-309">Pour un dossier source nommé Dossier1 et structuré comme suit : </span><span class="sxs-lookup"><span data-stu-id="3ca83-309">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="3ca83-310">Dossier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-310">Folder1</span></span><br/><span data-ttu-id="3ca83-311">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="3ca83-312">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="3ca83-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="3ca83-313">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="3ca83-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="3ca83-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="3ca83-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="3ca83-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="3ca83-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="3ca83-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="3ca83-317">le dossier cible nommé Dossier1 est créé et structuré de la même manière que la source</span><span class="sxs-lookup"><span data-stu-id="3ca83-317">the target folder Folder1 is created with the same structure as the source</span></span><br/><br/><span data-ttu-id="3ca83-318">Dossier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-318">Folder1</span></span><br/><span data-ttu-id="3ca83-319">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="3ca83-320">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="3ca83-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="3ca83-321">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="3ca83-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="3ca83-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="3ca83-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="3ca83-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="3ca83-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier5.</span><span class="sxs-lookup"><span data-stu-id="3ca83-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="3ca83-325">true</span><span class="sxs-lookup"><span data-stu-id="3ca83-325">true</span></span> |<span data-ttu-id="3ca83-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="3ca83-326">flattenHierarchy</span></span> |<span data-ttu-id="3ca83-327">Pour un dossier source nommé Dossier1 et structuré comme suit : </span><span class="sxs-lookup"><span data-stu-id="3ca83-327">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="3ca83-328">Dossier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-328">Folder1</span></span><br/><span data-ttu-id="3ca83-329">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="3ca83-330">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="3ca83-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="3ca83-331">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="3ca83-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="3ca83-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="3ca83-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="3ca83-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="3ca83-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="3ca83-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="3ca83-335">le dossier cible Dossier1 est créé et structuré comme suit :</span><span class="sxs-lookup"><span data-stu-id="3ca83-335">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="3ca83-336">Dossier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-336">Folder1</span></span><br/><span data-ttu-id="3ca83-337">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="3ca83-338">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier2</span><span class="sxs-lookup"><span data-stu-id="3ca83-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="3ca83-339">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier3</span><span class="sxs-lookup"><span data-stu-id="3ca83-339">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="3ca83-340">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier4</span><span class="sxs-lookup"><span data-stu-id="3ca83-340">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="3ca83-341">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier5</span><span class="sxs-lookup"><span data-stu-id="3ca83-341">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="3ca83-342">true</span><span class="sxs-lookup"><span data-stu-id="3ca83-342">true</span></span> |<span data-ttu-id="3ca83-343">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="3ca83-343">mergeFiles</span></span> |<span data-ttu-id="3ca83-344">Pour un dossier source nommé Dossier1 et structuré comme suit : </span><span class="sxs-lookup"><span data-stu-id="3ca83-344">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="3ca83-345">Dossier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-345">Folder1</span></span><br/><span data-ttu-id="3ca83-346">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="3ca83-347">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="3ca83-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="3ca83-348">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="3ca83-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="3ca83-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="3ca83-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="3ca83-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="3ca83-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="3ca83-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="3ca83-352">le dossier cible Dossier1 est créé et structuré comme suit :</span><span class="sxs-lookup"><span data-stu-id="3ca83-352">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="3ca83-353">Dossier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-353">Folder1</span></span><br/><span data-ttu-id="3ca83-354">&nbsp;&nbsp;&nbsp;&nbsp;Le contenu de Fichier1 + Fichier2 + Fichier3 + Fichier4 + Fichier5 est fusionné dans un fichier avec le nom de fichier généré automatiquement</span><span class="sxs-lookup"><span data-stu-id="3ca83-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="3ca83-355">false</span><span class="sxs-lookup"><span data-stu-id="3ca83-355">false</span></span> |<span data-ttu-id="3ca83-356">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="3ca83-356">preserveHierarchy</span></span> |<span data-ttu-id="3ca83-357">Pour un dossier source nommé Dossier1 et structuré comme suit : </span><span class="sxs-lookup"><span data-stu-id="3ca83-357">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="3ca83-358">Dossier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-358">Folder1</span></span><br/><span data-ttu-id="3ca83-359">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="3ca83-360">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="3ca83-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="3ca83-361">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="3ca83-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="3ca83-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="3ca83-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="3ca83-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="3ca83-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="3ca83-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="3ca83-365">le dossier cible nommé Dossier1 est créé et structuré comme suit</span><span class="sxs-lookup"><span data-stu-id="3ca83-365">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="3ca83-366">Dossier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-366">Folder1</span></span><br/><span data-ttu-id="3ca83-367">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="3ca83-368">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="3ca83-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="3ca83-369">Sous-dossier1, où Fichier3, Fichier4 et Fichier5 ne sont pas sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="3ca83-369">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="3ca83-370">false</span><span class="sxs-lookup"><span data-stu-id="3ca83-370">false</span></span> |<span data-ttu-id="3ca83-371">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="3ca83-371">flattenHierarchy</span></span> |<span data-ttu-id="3ca83-372">Pour un dossier source nommé Dossier1 et structuré comme suit : </span><span class="sxs-lookup"><span data-stu-id="3ca83-372">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="3ca83-373">Dossier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-373">Folder1</span></span><br/><span data-ttu-id="3ca83-374">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="3ca83-375">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="3ca83-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="3ca83-376">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="3ca83-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="3ca83-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="3ca83-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="3ca83-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="3ca83-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="3ca83-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="3ca83-380">le dossier cible nommé Dossier1 est créé et structuré comme suit</span><span class="sxs-lookup"><span data-stu-id="3ca83-380">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="3ca83-381">Dossier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-381">Folder1</span></span><br/><span data-ttu-id="3ca83-382">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-382">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="3ca83-383">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier2</span><span class="sxs-lookup"><span data-stu-id="3ca83-383">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="3ca83-384">Sous-dossier1, où Fichier3, Fichier4 et Fichier5 ne sont pas sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="3ca83-384">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="3ca83-385">false</span><span class="sxs-lookup"><span data-stu-id="3ca83-385">false</span></span> |<span data-ttu-id="3ca83-386">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="3ca83-386">mergeFiles</span></span> |<span data-ttu-id="3ca83-387">Pour un dossier source nommé Dossier1 et structuré comme suit : </span><span class="sxs-lookup"><span data-stu-id="3ca83-387">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="3ca83-388">Dossier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-388">Folder1</span></span><br/><span data-ttu-id="3ca83-389">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="3ca83-390">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="3ca83-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="3ca83-391">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="3ca83-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="3ca83-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="3ca83-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="3ca83-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="3ca83-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="3ca83-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="3ca83-395">le dossier cible nommé Dossier1 est créé et structuré comme suit</span><span class="sxs-lookup"><span data-stu-id="3ca83-395">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="3ca83-396">Dossier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-396">Folder1</span></span><br/><span data-ttu-id="3ca83-397">&nbsp;&nbsp;&nbsp;&nbsp;Le contenu de Fichier1 + Fichier2 est fusionné dans un fichier avec le nom de fichier généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="3ca83-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="3ca83-398">nom généré automatiquement pour Fichier1</span><span class="sxs-lookup"><span data-stu-id="3ca83-398">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="3ca83-399">Sous-dossier1, où Fichier3, Fichier4 et Fichier5 ne sont pas sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="3ca83-399">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="3ca83-400">Formats de fichier et de compression pris en charge</span><span class="sxs-lookup"><span data-stu-id="3ca83-400">Supported file and compression formats</span></span>
<span data-ttu-id="3ca83-401">Pour plus d’informations, voir [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="3ca83-401">For details, see the [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span>

## <a name="json-examples-for-copying-data-to-and-from-data-lake-store"></a><span data-ttu-id="3ca83-402">Exemples JSON pour copier des données vers et depuisData Lake Store</span><span class="sxs-lookup"><span data-stu-id="3ca83-402">JSON examples for copying data to and from Data Lake Store</span></span>
<span data-ttu-id="3ca83-403">Les exemples suivants fournissent des exemples de définitions JSON.</span><span class="sxs-lookup"><span data-stu-id="3ca83-403">The following examples provide sample JSON definitions.</span></span> <span data-ttu-id="3ca83-404">Vous pouvez utiliser ces exemples de définitions pour créer un pipeline à l’aide du [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), de [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [d’Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3ca83-404">You can use these sample definitions to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="3ca83-405">Les exemples indiquent comment copier des données vers et depuis Data Lake Store et Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="3ca83-405">The examples show how to copy data to and from Data Lake Store and Azure Blob storage.</span></span> <span data-ttu-id="3ca83-406">Toutefois, les données peuvent être copiées _directement_ à partir de n’importe quelle source, vers tout récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3ca83-406">However, data can be copied _directly_ from any of the sources to any of the supported sinks.</span></span> <span data-ttu-id="3ca83-407">Pour plus d’informations, consultez la section « Banques de données et formats pris en charge » de l’article [Déplacer des données à l’aide de l’activité de copie](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="3ca83-407">For more information, see the section "Supported data stores and formats" in the [Move data by using Copy Activity](data-factory-data-movement-activities.md) article.</span></span>  

### <a name="example-copy-data-from-azure-blob-storage-to-azure-data-lake-store"></a><span data-ttu-id="3ca83-408">Exemple : copie de données du stockage Blob Azure vers Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3ca83-408">Example: Copy data from Azure Blob Storage to Azure Data Lake Store</span></span>
<span data-ttu-id="3ca83-409">L’exemple de code dans cette section montre :</span><span class="sxs-lookup"><span data-stu-id="3ca83-409">The example code in this section shows:</span></span>

* <span data-ttu-id="3ca83-410">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3ca83-410">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="3ca83-411">Un service lié de type [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3ca83-411">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="3ca83-412">Un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3ca83-412">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="3ca83-413">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3ca83-413">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="3ca83-414">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) et [AzureDataLakeStoreSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="3ca83-414">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span></span>

<span data-ttu-id="3ca83-415">L’exemple montre la copie des données de série horaire depuis un stockage d’objets blob vers Azure Data Lake Store toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="3ca83-415">The examples show how time-series data from Azure Blob Storage is copied to Data Lake Store every hour.</span></span> 

<span data-ttu-id="3ca83-416">**Service lié Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="3ca83-416">**Azure Storage linked service**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="3ca83-417">**Service lié Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="3ca83-417">**Azure Data Lake Store linked service**</span></span>

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="3ca83-418">Pour les détails de configuration, consultez la section [Propriétés du service lié](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3ca83-418">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="3ca83-419">**Jeu de données d'entrée d'objet Blob Azure**</span><span class="sxs-lookup"><span data-stu-id="3ca83-419">**Azure blob input dataset**</span></span>

<span data-ttu-id="3ca83-420">Dans l’exemple suivant, les données sont récupérées à partir d'un nouvel objet Blob toutes les heures (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="3ca83-420">In the following example, data is picked up from a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="3ca83-421">Le nom du chemin d'accès et du fichier de dossier pour l'objet blob sont évalués dynamiquement en fonction de l'heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="3ca83-421">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="3ca83-422">Le chemin d’accès du dossier utilise l’année, le mois et le jour de début.</span><span class="sxs-lookup"><span data-stu-id="3ca83-422">The folder path uses the year, month, and day portion of the start time.</span></span> <span data-ttu-id="3ca83-423">Le nom de fichier utilise la partie heure de l’heure de début.</span><span class="sxs-lookup"><span data-stu-id="3ca83-423">The file name uses the hour portion of the start time.</span></span> <span data-ttu-id="3ca83-424">Le paramètre `"external": true` informe le service Data Factory que cette table est externe à la Data Factory et non produite par une activité dans la Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3ca83-424">The `"external": true` setting informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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

<span data-ttu-id="3ca83-425">**Jeu de données de sortie Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="3ca83-425">**Azure Data Lake Store output dataset**</span></span>

<span data-ttu-id="3ca83-426">L’exemple suivant copie des données dans un magasin Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3ca83-426">The following example copies data to Data Lake Store.</span></span> <span data-ttu-id="3ca83-427">De nouvelles données sont copiées dans Data Lake Store toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="3ca83-427">New data is copied to Data Lake Store every hour.</span></span>

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


<span data-ttu-id="3ca83-428">**Activité de copie dans un pipeline avec une source Blob et un récepteur Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="3ca83-428">**Copy activity in a pipeline with a blob source and a Data Lake Store sink**</span></span>

<span data-ttu-id="3ca83-429">Dans l’exemple suivant, le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="3ca83-429">In the following example, the pipeline contains a copy activity that is configured to use the input and output datasets.</span></span> <span data-ttu-id="3ca83-430">L’activité de copie est planifiée pour s’exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="3ca83-430">The copy activity is scheduled to run every hour.</span></span> <span data-ttu-id="3ca83-431">Dans la définition JSON du pipeline, le type `source` est défini sur `BlobSource` et le type `sink` est défini sur `AzureDataLakeStoreSink`.</span><span class="sxs-lookup"><span data-stu-id="3ca83-431">In the pipeline JSON definition, the `source` type is set to `BlobSource`, and the `sink` type is set to `AzureDataLakeStoreSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
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

### <a name="example-copy-data-from-azure-data-lake-store-to-an-azure-blob"></a><span data-ttu-id="3ca83-432">Exemple : copie de données d’Azure Data Lake Store vers un objet blob Azure</span><span class="sxs-lookup"><span data-stu-id="3ca83-432">Example: Copy data from Azure Data Lake Store to an Azure blob</span></span>
<span data-ttu-id="3ca83-433">L’exemple de code dans cette section montre :</span><span class="sxs-lookup"><span data-stu-id="3ca83-433">The example code in this section shows:</span></span>

* <span data-ttu-id="3ca83-434">Un service lié de type [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3ca83-434">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="3ca83-435">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3ca83-435">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="3ca83-436">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3ca83-436">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="3ca83-437">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3ca83-437">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="3ca83-438">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [AzureDataLakeStoreSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="3ca83-438">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="3ca83-439">Le code copie des données appartenant à une série horaire depuis un magasin Data Lake vers un objet blob Azure toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="3ca83-439">The code copies time-series data from Data Lake Store to an Azure blob every hour.</span></span> 

<span data-ttu-id="3ca83-440">**Service lié Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="3ca83-440">**Azure Data Lake Store linked service**</span></span>

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="3ca83-441">Pour les détails de configuration, consultez la section [Propriétés du service lié](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3ca83-441">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="3ca83-442">**Service lié Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="3ca83-442">**Azure Storage linked service**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="3ca83-443">**Jeu de données Azure Data Lake de sortie**</span><span class="sxs-lookup"><span data-stu-id="3ca83-443">**Azure Data Lake input dataset**</span></span>

<span data-ttu-id="3ca83-444">Dans cet exemple, la définition de `"external"` sur `true` informe le service Data Factory qu’il s’agit d’un jeu de données qui est externe à la Data Factory et non produit par une activité dans la Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3ca83-444">In this example, setting `"external"` to `true` informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
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
        "external": true,
        "availability": {
            "frequency": "Hour",
              "interval": 1
        },
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
<span data-ttu-id="3ca83-445">**Jeu de données de sortie d’objet Blob Azure**</span><span class="sxs-lookup"><span data-stu-id="3ca83-445">**Azure blob output dataset**</span></span>

<span data-ttu-id="3ca83-446">Dans l’exemple suivant, les données sont écrites dans un nouvel objet Blob toutes les heures (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="3ca83-446">In the following example, data is written to a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="3ca83-447">Le chemin d’accès du dossier pour l’objet blob est évalué dynamiquement en fonction de l’heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="3ca83-447">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="3ca83-448">Le chemin d’accès du dossier utilise l’année, le mois, le jour et la partie heure de l’heure de début.</span><span class="sxs-lookup"><span data-stu-id="3ca83-448">The folder path uses the year, month, day, and hours portion of the start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="3ca83-449">**Activité de copie dans un pipeline avec une source Azure Data Lake Store et un récepteur Blob**</span><span class="sxs-lookup"><span data-stu-id="3ca83-449">**A copy activity in a pipeline with an Azure Data Lake Store source and a blob sink**</span></span>

<span data-ttu-id="3ca83-450">Dans l’exemple suivant, le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="3ca83-450">In the following example, the pipeline contains a copy activity that is configured to use the input and output datasets.</span></span> <span data-ttu-id="3ca83-451">L’activité de copie est planifiée pour s’exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="3ca83-451">The copy activity is scheduled to run every hour.</span></span> <span data-ttu-id="3ca83-452">Dans la définition JSON du pipeline, le type `source` est défini sur `AzureDataLakeStoreSource` et le type `sink` est défini sur `BlobSink`.</span><span class="sxs-lookup"><span data-stu-id="3ca83-452">In the pipeline JSON definition, the `source` type is set to `AzureDataLakeStoreSource`, and the `sink` type is set to `BlobSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
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

<span data-ttu-id="3ca83-453">Dans la définition d’activité de copie, vous pouvez également mapper des colonnes du jeu de données source aux colonnes du jeu de données récepteur.</span><span class="sxs-lookup"><span data-stu-id="3ca83-453">In the copy activity definition, you can also map columns from the source dataset to columns in the sink dataset.</span></span> <span data-ttu-id="3ca83-454">Pour plus d’informations, consultez [Mappage de colonnes de jeux de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="3ca83-454">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="3ca83-455">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="3ca83-455">Performance and tuning</span></span>
<span data-ttu-id="3ca83-456">Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) et les manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="3ca83-456">To learn about the factors that affect Copy Activity performance and how to optimize it, see the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) article.</span></span>
