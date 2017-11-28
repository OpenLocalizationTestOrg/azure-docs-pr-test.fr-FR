---
title: "Déplacer des données à partir de magasins de données ODBC | Microsoft Docs"
description: "Apprenez à transférer des données à partir de magasins de données ODBC à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 269d9802ca4a6a16dbf9021929fe21104cb431f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="6c216-103">Transfert de données à partir de magasins de données ODBC à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="6c216-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="6c216-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour déplacer des données à partir d’un magasin de données ODBC local.</span><span class="sxs-lookup"><span data-stu-id="6c216-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises ODBC data store.</span></span> <span data-ttu-id="6c216-105">Il s’appuie sur cet article, relatif aux [activités de déplacement de données](data-factory-data-movement-activities.md), qui présente une vue d’ensemble du déplacement de données avec l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="6c216-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="6c216-106">Vous pouvez copier et coller les données d’un magasin de données ODBC dans tout magasin de données récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="6c216-106">You can copy data from an ODBC data store to any supported sink data store.</span></span> <span data-ttu-id="6c216-107">Consultez la table [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) pour obtenir la liste des magasins de données pris en charge en tant que récepteurs par l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="6c216-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="6c216-108">Actuellement, Data Factory prend uniquement en charge le déplacement de données d’un magasin de données ODBC vers d’autres magasins de données, mais non l’inverse.</span><span class="sxs-lookup"><span data-stu-id="6c216-108">Data factory currently supports only moving data from an ODBC data store to other data stores, but not for moving data from other data stores to an ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="6c216-109">Activation de la connectivité</span><span class="sxs-lookup"><span data-stu-id="6c216-109">Enabling connectivity</span></span>
<span data-ttu-id="6c216-110">Le service Data Factory prend en charge la connexion à des sources ODBC locales à l’aide de la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="6c216-110">Data Factory service supports connecting to on-premises ODBC sources using the Data Management Gateway.</span></span> <span data-ttu-id="6c216-111">Consultez l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) pour en savoir plus sur la passerelle de gestion des données et obtenir des instructions détaillées sur la configuration de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="6c216-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="6c216-112">Utilisez la passerelle pour vous connecter à un magasin de données ODBC même si elle est hébergée sur une machine virtuelle IaaS Azure.</span><span class="sxs-lookup"><span data-stu-id="6c216-112">Use the gateway to connect to an ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="6c216-113">Vous pouvez installer la passerelle sur le même ordinateur local ou la machine virtuelle Azure comme magasin de données ODBC.</span><span class="sxs-lookup"><span data-stu-id="6c216-113">You can install the gateway on the same on-premises machine or the Azure VM as the ODBC data store.</span></span> <span data-ttu-id="6c216-114">Toutefois, nous vous recommandons d’installer la passerelle sur un ordinateur/une machine virtuelle IaaS Azure distinct(e) afin d’éviter les conflits de ressources, ainsi que pour obtenir de meilleures performances.</span><span class="sxs-lookup"><span data-stu-id="6c216-114">However, we recommend that you install the gateway on a separate machine/Azure IaaS VM to avoid resource contention and for better performance.</span></span> <span data-ttu-id="6c216-115">Lorsque vous installez la passerelle sur un ordinateur distinct, l’ordinateur doit être en mesure d’accéder à l’ordinateur sur lequel réside le magasin de données ODBC.</span><span class="sxs-lookup"><span data-stu-id="6c216-115">When you install the gateway on a separate machine, the machine should be able to access the machine with the ODBC data store.</span></span>

<span data-ttu-id="6c216-116">En dehors de la passerelle de gestion des données, vous devez également installer le pilote ODBC pour le magasin de données de l’ordinateur de passerelle.</span><span class="sxs-lookup"><span data-stu-id="6c216-116">Apart from the Data Management Gateway, you also need to install the ODBC driver for the data store on the gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="6c216-117">Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.</span><span class="sxs-lookup"><span data-stu-id="6c216-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="6c216-118">Prise en main</span><span class="sxs-lookup"><span data-stu-id="6c216-118">Getting started</span></span>
<span data-ttu-id="6c216-119">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données ODBC local à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="6c216-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="6c216-120">Le moyen le plus simple de créer un pipeline consiste à utiliser **l’Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="6c216-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="6c216-121">Consultez la page [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant Copier des données.</span><span class="sxs-lookup"><span data-stu-id="6c216-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="6c216-122">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="6c216-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="6c216-123">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="6c216-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="6c216-124">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="6c216-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="6c216-125">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="6c216-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="6c216-126">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="6c216-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="6c216-127">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="6c216-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="6c216-128">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="6c216-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="6c216-129">Lorsque vous utilisez des outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory à l’aide du format JSON.</span><span class="sxs-lookup"><span data-stu-id="6c216-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="6c216-130">Pour consulter un exemple contenant des définitions JSON pour les entités Data Factory utilisées pour copier des données d’un magasin de données ODBC, consultez la section [Exemple JSON : copier des données depuis un magasin de données ODBC vers Blob Azure](#json-example-copy-data-from-odbc-data-store-to-azure-blob) de cet article.</span><span class="sxs-lookup"><span data-stu-id="6c216-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an ODBC data store, see [JSON example: Copy data from ODBC data store to Azure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="6c216-131">Les sections suivantes contiennent des informations détaillées sur les propriétés JSON utilisées pour définir les entités Data Factory propres au magasin de données ODBC :</span><span class="sxs-lookup"><span data-stu-id="6c216-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to ODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="6c216-132">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="6c216-132">Linked service properties</span></span>
<span data-ttu-id="6c216-133">Le tableau suivant fournit la description des éléments JSON spécifiques au service lié ODBC.</span><span class="sxs-lookup"><span data-stu-id="6c216-133">The following table provides description for JSON elements specific to ODBC linked service.</span></span>

| <span data-ttu-id="6c216-134">Propriété</span><span class="sxs-lookup"><span data-stu-id="6c216-134">Property</span></span> | <span data-ttu-id="6c216-135">Description</span><span class="sxs-lookup"><span data-stu-id="6c216-135">Description</span></span> | <span data-ttu-id="6c216-136">Requis</span><span class="sxs-lookup"><span data-stu-id="6c216-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c216-137">type</span><span class="sxs-lookup"><span data-stu-id="6c216-137">type</span></span> |<span data-ttu-id="6c216-138">Le type de propriété doit être défini sur : **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="6c216-138">The type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="6c216-139">Oui</span><span class="sxs-lookup"><span data-stu-id="6c216-139">Yes</span></span> |
| <span data-ttu-id="6c216-140">connectionString</span><span class="sxs-lookup"><span data-stu-id="6c216-140">connectionString</span></span> |<span data-ttu-id="6c216-141">Partie de la chaîne de connexion ne contenant pas les informations d’accès, avec des informations d’identification chiffrées facultatives.</span><span class="sxs-lookup"><span data-stu-id="6c216-141">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="6c216-142">Consultez les exemples dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="6c216-142">See examples in the following sections.</span></span> |<span data-ttu-id="6c216-143">Oui</span><span class="sxs-lookup"><span data-stu-id="6c216-143">Yes</span></span> |
| <span data-ttu-id="6c216-144">credential</span><span class="sxs-lookup"><span data-stu-id="6c216-144">credential</span></span> |<span data-ttu-id="6c216-145">Partie de la chaîne de connexion contenant les informations d’accès, spécifiée dans un format de valeurs de propriété spécifique au pilote.</span><span class="sxs-lookup"><span data-stu-id="6c216-145">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="6c216-146">Exemple : « Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>; ».</span><span class="sxs-lookup"><span data-stu-id="6c216-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="6c216-147">Non</span><span class="sxs-lookup"><span data-stu-id="6c216-147">No</span></span> |
| <span data-ttu-id="6c216-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6c216-148">authenticationType</span></span> |<span data-ttu-id="6c216-149">Type d’authentification utilisé pour se connecter au magasin de données ODBC.</span><span class="sxs-lookup"><span data-stu-id="6c216-149">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="6c216-150">Les valeurs possibles sont : Anonyme et De base.</span><span class="sxs-lookup"><span data-stu-id="6c216-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="6c216-151">Oui</span><span class="sxs-lookup"><span data-stu-id="6c216-151">Yes</span></span> |
| <span data-ttu-id="6c216-152">username</span><span class="sxs-lookup"><span data-stu-id="6c216-152">username</span></span> |<span data-ttu-id="6c216-153">Spécifiez le nom d’utilisateur si vous utilisez l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="6c216-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="6c216-154">Non</span><span class="sxs-lookup"><span data-stu-id="6c216-154">No</span></span> |
| <span data-ttu-id="6c216-155">password</span><span class="sxs-lookup"><span data-stu-id="6c216-155">password</span></span> |<span data-ttu-id="6c216-156">Spécifiez le mot de passe du compte d’utilisateur que vous avez spécifié pour le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6c216-156">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="6c216-157">Non</span><span class="sxs-lookup"><span data-stu-id="6c216-157">No</span></span> |
| <span data-ttu-id="6c216-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6c216-158">gatewayName</span></span> |<span data-ttu-id="6c216-159">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter au magasin de données ODBC.</span><span class="sxs-lookup"><span data-stu-id="6c216-159">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="6c216-160">Oui</span><span class="sxs-lookup"><span data-stu-id="6c216-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="6c216-161">Utilisation de l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="6c216-161">Using Basic authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="6c216-162">Utilisation de l’authentification de base avec des informations d’identification chiffrées</span><span class="sxs-lookup"><span data-stu-id="6c216-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="6c216-163">Vous pouvez chiffrer les informations d’identification à l’aide de l’applet de commande [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (version 1.0 d’Azure PowerShell) ou [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (version 0.9 ou antérieure d’Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="6c216-163">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="6c216-164">Utilisation de l’authentification anonyme</span><span class="sxs-lookup"><span data-stu-id="6c216-164">Using Anonymous authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a><span data-ttu-id="6c216-165">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="6c216-165">Dataset properties</span></span>
<span data-ttu-id="6c216-166">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="6c216-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="6c216-167">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="6c216-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="6c216-168">La section **typeProperties** est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="6c216-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="6c216-169">La section typeProperties du jeu de données de type **RelationalTable** (qui inclut le jeu de données ODBC) présente les propriétés suivantes</span><span class="sxs-lookup"><span data-stu-id="6c216-169">The typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has the following properties</span></span>

| <span data-ttu-id="6c216-170">Propriété</span><span class="sxs-lookup"><span data-stu-id="6c216-170">Property</span></span> | <span data-ttu-id="6c216-171">Description</span><span class="sxs-lookup"><span data-stu-id="6c216-171">Description</span></span> | <span data-ttu-id="6c216-172">Requis</span><span class="sxs-lookup"><span data-stu-id="6c216-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c216-173">TableName</span><span class="sxs-lookup"><span data-stu-id="6c216-173">tableName</span></span> |<span data-ttu-id="6c216-174">Nom de la table dans le magasin de données ODBC.</span><span class="sxs-lookup"><span data-stu-id="6c216-174">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="6c216-175">Oui</span><span class="sxs-lookup"><span data-stu-id="6c216-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="6c216-176">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="6c216-176">Copy activity properties</span></span>
<span data-ttu-id="6c216-177">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="6c216-177">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6c216-178">Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités.</span><span class="sxs-lookup"><span data-stu-id="6c216-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="6c216-179">En revanche, les propriétés disponibles dans la section **typeProperties** de l'activité varient pour chaque type d'activité.</span><span class="sxs-lookup"><span data-stu-id="6c216-179">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="6c216-180">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="6c216-180">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="6c216-181">Dans l’activité de copie, quand la source est de type **RelationalSource** (ce qui inclut ODBC), les propriétés suivantes sont disponibles dans la section typeProperties :</span><span class="sxs-lookup"><span data-stu-id="6c216-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="6c216-182">Propriété</span><span class="sxs-lookup"><span data-stu-id="6c216-182">Property</span></span> | <span data-ttu-id="6c216-183">Description</span><span class="sxs-lookup"><span data-stu-id="6c216-183">Description</span></span> | <span data-ttu-id="6c216-184">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="6c216-184">Allowed values</span></span> | <span data-ttu-id="6c216-185">Requis</span><span class="sxs-lookup"><span data-stu-id="6c216-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6c216-186">query</span><span class="sxs-lookup"><span data-stu-id="6c216-186">query</span></span> |<span data-ttu-id="6c216-187">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="6c216-187">Use the custom query to read data.</span></span> |<span data-ttu-id="6c216-188">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="6c216-188">SQL query string.</span></span> <span data-ttu-id="6c216-189">Par exemple : select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="6c216-189">For example: select * from MyTable.</span></span> |<span data-ttu-id="6c216-190">Oui</span><span class="sxs-lookup"><span data-stu-id="6c216-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-to-azure-blob"></a><span data-ttu-id="6c216-191">Exemple JSON : copier des données depuis un magasin de données ODBC vers Blob Azure</span><span class="sxs-lookup"><span data-stu-id="6c216-191">JSON example: Copy data from ODBC data store to Azure Blob</span></span>
<span data-ttu-id="6c216-192">Cet exemple présente des définitions JSON que vous pouvez utiliser pour créer un pipeline à l’aide du [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), de [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [d’Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6c216-192">This example provides JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="6c216-193">Il indique comment copier des données depuis une source ODBC vers un système de stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="6c216-193">It shows how to copy data from an ODBC source to an Azure Blob Storage.</span></span> <span data-ttu-id="6c216-194">Toutefois, les données peuvent être copiées vers l’un des récepteurs indiqués [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) , via l’activité de copie d’Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6c216-194">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="6c216-195">L’exemple contient les entités de fabrique de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="6c216-195">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="6c216-196">Un service lié de type [OnPremisesOdbc](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6c216-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="6c216-197">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6c216-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="6c216-198">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6c216-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="6c216-199">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6c216-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="6c216-200">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [RelationalSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="6c216-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="6c216-201">L’exemple copie toutes les heures les données de résultat d’une requête d’un magasin de données ODBC en local vers un objet blob.</span><span class="sxs-lookup"><span data-stu-id="6c216-201">The sample copies data from a query result in an ODBC data store to a blob every hour.</span></span> <span data-ttu-id="6c216-202">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="6c216-202">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="6c216-203">Dans un premier temps, configurez la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="6c216-203">As a first step, set up the data management gateway.</span></span> <span data-ttu-id="6c216-204">Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="6c216-204">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="6c216-205">**Service lié de HDFS** : cet exemple utilise l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="6c216-205">**ODBC linked service** This example uses the Basic authentication.</span></span> <span data-ttu-id="6c216-206">Consultez la section [Service lié ODBC](#linked-service-properties) pour connaître les différents types d’authentification que vous pouvez utiliser.</span><span class="sxs-lookup"><span data-stu-id="6c216-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="6c216-207">**Service lié Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="6c216-207">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="6c216-208">**Jeu de données d’entrée ODBC**</span><span class="sxs-lookup"><span data-stu-id="6c216-208">**ODBC input dataset**</span></span>

<span data-ttu-id="6c216-209">L’exemple suppose que vous avez créé une table « MyTable » dans une base de données ODBC et qu’elle contient une colonne appelée « timestampcolumn » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="6c216-209">The sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="6c216-210">La définition de « external » : « true» informe le service Data Factory qu’il s’agit d’un jeu de données qui est externe à Data Factory et non produit par une activité dans Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6c216-210">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
        "typeProperties": {},
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

<span data-ttu-id="6c216-211">**Jeu de données de sortie Azure Blob**</span><span class="sxs-lookup"><span data-stu-id="6c216-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="6c216-212">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="6c216-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6c216-213">Le chemin d’accès du dossier pour l’objet blob est évalué dynamiquement en fonction de l’heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="6c216-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="6c216-214">Le chemin d'accès du dossier utilise l'année, le mois, le jour et l'heure de l'heure de début.</span><span class="sxs-lookup"><span data-stu-id="6c216-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


<span data-ttu-id="6c216-215">**Activité de copie dans un pipeline, avec une source ODBC (RelationalSource) et un récepteur blob (BlobSink)**</span><span class="sxs-lookup"><span data-stu-id="6c216-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="6c216-216">Le pipeline contient une activité de copie qui est configurée pour utiliser ces jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="6c216-216">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="6c216-217">Dans la définition du pipeline JSON, le type **source** est défini sur **RelationalSource** et le type **sink** est défini sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="6c216-217">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="6c216-218">La requête SQL spécifiée pour la propriété **query** sélectionne les données de la dernière heure à copier.</span><span class="sxs-lookup"><span data-stu-id="6c216-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
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
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="6c216-219">Mappage de type pour ODBC</span><span class="sxs-lookup"><span data-stu-id="6c216-219">Type mapping for ODBC</span></span>
<span data-ttu-id="6c216-220">Comme mentionné dans l’article consacré aux [activités de déplacement de données](data-factory-data-movement-activities.md) , l’activité de copie convertit automatiquement des types source en types récepteur à l’aide de l’approche en deux étapes suivante :</span><span class="sxs-lookup"><span data-stu-id="6c216-220">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="6c216-221">Conversion de types natifs source en types .NET</span><span class="sxs-lookup"><span data-stu-id="6c216-221">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="6c216-222">Conversion à partir du type .NET en type de récepteur natif</span><span class="sxs-lookup"><span data-stu-id="6c216-222">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="6c216-223">Lors du déplacement de données à partir de magasins de données ODBC, les types de données ODBC sont mappés aux types .NET, comme indiqué dans la rubrique [Mappages de types de données ODBC](https://msdn.microsoft.com/library/cc668763.aspx) .</span><span class="sxs-lookup"><span data-stu-id="6c216-223">When moving data from ODBC data stores, ODBC data types are mapped to .NET types as mentioned in the [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="6c216-224">Mapper les colonnes source aux colonnes du récepteur</span><span class="sxs-lookup"><span data-stu-id="6c216-224">Map source to sink columns</span></span>
<span data-ttu-id="6c216-225">Pour en savoir plus sur le mappage de colonnes du jeu de données source à des colonnes du jeu de données récepteur, voir [Mappage des colonnes d’un jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="6c216-225">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="6c216-226">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="6c216-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="6c216-227">Lorsque vous copiez des données à partir de magasins de données relationnels, gardez à l’esprit la répétabilité de l’opération, afin d’éviter des résultats imprévus.</span><span class="sxs-lookup"><span data-stu-id="6c216-227">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="6c216-228">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="6c216-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="6c216-229">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="6c216-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="6c216-230">Lorsqu’une tranche est réexécutée d’une manière ou d’une autre, vous devez vous assurer que les mêmes données sont lues et ce, quel que soit le nombre d’exécutions de la tranche.</span><span class="sxs-lookup"><span data-stu-id="6c216-230">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="6c216-231">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="6c216-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="6c216-232">Magasin GE Historian</span><span class="sxs-lookup"><span data-stu-id="6c216-232">GE Historian store</span></span>
<span data-ttu-id="6c216-233">Vous créez un service lié ODBC pour lier un magasin de données [GE Proficy Historian (désormais GE Historian)](http://www.geautomation.com/products/proficy-historian) à une fabrique de données Azure comme l’indique l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6c216-233">You create an ODBC linked service to link a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store to an Azure data factory as shown in the following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of the GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="6c216-234">Installez la passerelle de gestion des données sur un ordinateur local et enregistrez la passerelle auprès du portail.</span><span class="sxs-lookup"><span data-stu-id="6c216-234">Install Data Management Gateway on an on-premises machine and register the gateway with the portal.</span></span> <span data-ttu-id="6c216-235">La passerelle installée sur votre ordinateur local utilise le pilote ODBC pour GE Historian afin de se connecter au magasin de données GE Historian.</span><span class="sxs-lookup"><span data-stu-id="6c216-235">The gateway installed on your on-premises computer uses the ODBC driver for GE Historian to connect to the GE Historian data store.</span></span> <span data-ttu-id="6c216-236">Par conséquent, installez le pilote s’il n’est pas déjà installé sur l’ordinateur passerelle.</span><span class="sxs-lookup"><span data-stu-id="6c216-236">Therefore, install the driver if it is not already installed on the gateway machine.</span></span> <span data-ttu-id="6c216-237">Consultez la section [Activation de la connectivité](#enabling-connectivity) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="6c216-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="6c216-238">Avant d'utiliser le magasin GE Historian dans une solution Data Factory, vérifiez que la passerelle peut se connecter au magasin de données en suivant les instructions de la section suivante.</span><span class="sxs-lookup"><span data-stu-id="6c216-238">Before you use the GE Historian store in a Data Factory solution, verify whether the gateway can connect to the data store using instructions in the next section.</span></span>

<span data-ttu-id="6c216-239">Lisez l'article depuis le début pour une présentation détaillée de l'utilisation de magasins de données ODBC en tant que magasins de données sources dans une opération de copie.</span><span class="sxs-lookup"><span data-stu-id="6c216-239">Read the article from the beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="6c216-240">Résoudre les problèmes de connectivité</span><span class="sxs-lookup"><span data-stu-id="6c216-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="6c216-241">Pour résoudre les problèmes de connexion, utilisez l’onglet **Diagnostics** du **Gestionnaire de configuration de la passerelle de gestion des données**.</span><span class="sxs-lookup"><span data-stu-id="6c216-241">To troubleshoot connection issues, use the **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="6c216-242">Lancez le **Gestionnaire de configuration de la passerelle de gestion des données**.</span><span class="sxs-lookup"><span data-stu-id="6c216-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="6c216-243">Vous pouvez exécuter directement « C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe » (ou) rechercher **Passerelle** pour trouver un lien vers l’application **Passerelle de gestion des données de Microsoft**, comme l’illustre l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="6c216-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** to find a link to **Microsoft Data Management Gateway** application as shown in the following image.</span></span>

    ![Rechercher la passerelle](./media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="6c216-245">Basculez vers l’onglet **Diagnostics** .</span><span class="sxs-lookup"><span data-stu-id="6c216-245">Switch to the **Diagnostics** tab.</span></span>

    ![Diagnostics de la passerelle](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="6c216-247">Sélectionnez le **type** de magasin de données (service lié).</span><span class="sxs-lookup"><span data-stu-id="6c216-247">Select the **type** of data store (linked service).</span></span>
4. <span data-ttu-id="6c216-248">Spécifiez **l’authentification** et entrez les **informations d’identification** (ou) entrez la **chaîne de connexion** utilisée pour vous connecter au magasin de données.</span><span class="sxs-lookup"><span data-stu-id="6c216-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used to connect to the data store.</span></span>
5. <span data-ttu-id="6c216-249">Cliquez sur **Tester la connexion** pour tester la connexion au magasin de données.</span><span class="sxs-lookup"><span data-stu-id="6c216-249">Click **Test connection** to test the connection to the data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="6c216-250">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="6c216-250">Performance and Tuning</span></span>
<span data-ttu-id="6c216-251">Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="6c216-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
