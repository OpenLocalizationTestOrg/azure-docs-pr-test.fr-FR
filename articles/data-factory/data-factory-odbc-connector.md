---
title: "aaaMove des données à partir de magasins de données ODBC | Documents Microsoft"
description: "En savoir plus sur le stockage des données toomove à partir de données ODBC à l’aide d’Azure Data Factory."
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
ms.openlocfilehash: bf96e71da449313b6144bb194205c572d2ca2030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="1bcff-103">Transfert de données à partir de magasins de données ODBC à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1bcff-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="1bcff-104">Cet article explique comment stocker des toouse hello activité de copie de données Azure Data Factory toomove une locale, les données ODBC.</span><span class="sxs-lookup"><span data-stu-id="1bcff-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises ODBC data store.</span></span> <span data-ttu-id="1bcff-105">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="1bcff-106">Vous pouvez copier des données à partir d’une banque de données de récepteur ODBC données magasin tooany pris en charge.</span><span class="sxs-lookup"><span data-stu-id="1bcff-106">You can copy data from an ODBC data store tooany supported sink data store.</span></span> <span data-ttu-id="1bcff-107">Pour une liste de données pris en charge des magasins récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="1bcff-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="1bcff-108">Fabrique de données prend en charge uniquement le déplacement tooother les magasins de données du magasin de données à partir de des données ODBC, mais ne pas pour déplacer des données d’une autre banque de données ODBC tooan données magasins.</span><span class="sxs-lookup"><span data-stu-id="1bcff-108">Data factory currently supports only moving data from an ODBC data store tooother data stores, but not for moving data from other data stores tooan ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="1bcff-109">Activation de la connectivité</span><span class="sxs-lookup"><span data-stu-id="1bcff-109">Enabling connectivity</span></span>
<span data-ttu-id="1bcff-110">Service de fabrique de données prend en charge des sources de ODBC tooon local qui se connecte à l’aide de la passerelle de gestion des données de hello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-110">Data Factory service supports connecting tooon-premises ODBC sources using hello Data Management Gateway.</span></span> <span data-ttu-id="1bcff-111">Consultez [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn l’article sur la passerelle de gestion des données et des instructions détaillées sur la configuration de passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="1bcff-112">Utiliser le magasin de données ODBC hello passerelle tooconnect tooan même s’il est hébergé dans une machine virtuelle IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="1bcff-112">Use hello gateway tooconnect tooan ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="1bcff-113">Vous pouvez installer la passerelle de hello sur hello même local de l’ordinateur ou hello Azure VM comme magasin de données ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-113">You can install hello gateway on hello same on-premises machine or hello Azure VM as hello ODBC data store.</span></span> <span data-ttu-id="1bcff-114">Toutefois, nous vous recommandons d’installer hello passerelle sur un ordinateur distinct/Azure IaaS VM tooavoid les conflits de ressources et pour de meilleures performances.</span><span class="sxs-lookup"><span data-stu-id="1bcff-114">However, we recommend that you install hello gateway on a separate machine/Azure IaaS VM tooavoid resource contention and for better performance.</span></span> <span data-ttu-id="1bcff-115">Lorsque vous installez la passerelle de hello sur un ordinateur distinct, machine de hello doit être machine hello tooaccess en mesure de magasin de données ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-115">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello machine with hello ODBC data store.</span></span>

<span data-ttu-id="1bcff-116">Outre hello passerelle de gestion des données, vous devez également pilote ODBC de hello tooinstall de banque de données hello sur l’ordinateur de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-116">Apart from hello Data Management Gateway, you also need tooinstall hello ODBC driver for hello data store on hello gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="1bcff-117">Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.</span><span class="sxs-lookup"><span data-stu-id="1bcff-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="1bcff-118">Prise en main</span><span class="sxs-lookup"><span data-stu-id="1bcff-118">Getting started</span></span>
<span data-ttu-id="1bcff-119">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’un magasin de données ODBC local à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="1bcff-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="1bcff-120">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="1bcff-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="1bcff-121">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="1bcff-122">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="1bcff-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="1bcff-123">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="1bcff-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="1bcff-124">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="1bcff-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="1bcff-125">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="1bcff-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="1bcff-126">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="1bcff-127">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="1bcff-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="1bcff-128">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="1bcff-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="1bcff-129">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="1bcff-130">Pour obtenir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données à partir d’une banque de données ODBC, consultez [exemple de JSON : tooAzure Blob de magasin de données de copie à partir de données ODBC](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="1bcff-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an ODBC data store, see [JSON example: Copy data from ODBC data store tooAzure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="1bcff-131">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont le magasin de données utilisé toodefine Data Factory entités tooODBC spécifique :</span><span class="sxs-lookup"><span data-stu-id="1bcff-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="1bcff-132">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="1bcff-132">Linked service properties</span></span>
<span data-ttu-id="1bcff-133">Hello tableau suivant fournit la description du service de tooODBC spécifique lié éléments JSON.</span><span class="sxs-lookup"><span data-stu-id="1bcff-133">hello following table provides description for JSON elements specific tooODBC linked service.</span></span>

| <span data-ttu-id="1bcff-134">Propriété</span><span class="sxs-lookup"><span data-stu-id="1bcff-134">Property</span></span> | <span data-ttu-id="1bcff-135">Description</span><span class="sxs-lookup"><span data-stu-id="1bcff-135">Description</span></span> | <span data-ttu-id="1bcff-136">Requis</span><span class="sxs-lookup"><span data-stu-id="1bcff-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1bcff-137">type</span><span class="sxs-lookup"><span data-stu-id="1bcff-137">type</span></span> |<span data-ttu-id="1bcff-138">propriété de type Hello doit indiquer : **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="1bcff-138">hello type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="1bcff-139">Oui</span><span class="sxs-lookup"><span data-stu-id="1bcff-139">Yes</span></span> |
| <span data-ttu-id="1bcff-140">connectionString</span><span class="sxs-lookup"><span data-stu-id="1bcff-140">connectionString</span></span> |<span data-ttu-id="1bcff-141">partie des informations d’identification de l’accès non Hello de chaîne de connexion hello et éventuellement un chiffrées d’informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="1bcff-141">hello non-access credential portion of hello connection string and an optional encrypted credential.</span></span> <span data-ttu-id="1bcff-142">Consultez les exemples dans les sections suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-142">See examples in hello following sections.</span></span> |<span data-ttu-id="1bcff-143">Oui</span><span class="sxs-lookup"><span data-stu-id="1bcff-143">Yes</span></span> |
| <span data-ttu-id="1bcff-144">credential</span><span class="sxs-lookup"><span data-stu-id="1bcff-144">credential</span></span> |<span data-ttu-id="1bcff-145">Hello accès informations d’identification la partie de chaîne de connexion hello spécifié au format de la valeur de propriété spécifiques au pilote.</span><span class="sxs-lookup"><span data-stu-id="1bcff-145">hello access credential portion of hello connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="1bcff-146">Exemple : « Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>; ».</span><span class="sxs-lookup"><span data-stu-id="1bcff-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="1bcff-147">Non</span><span class="sxs-lookup"><span data-stu-id="1bcff-147">No</span></span> |
| <span data-ttu-id="1bcff-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1bcff-148">authenticationType</span></span> |<span data-ttu-id="1bcff-149">Type d’authentification utilisé le magasin de données ODBC tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-149">Type of authentication used tooconnect toohello ODBC data store.</span></span> <span data-ttu-id="1bcff-150">Les valeurs possibles sont : Anonyme et De base.</span><span class="sxs-lookup"><span data-stu-id="1bcff-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="1bcff-151">Oui</span><span class="sxs-lookup"><span data-stu-id="1bcff-151">Yes</span></span> |
| <span data-ttu-id="1bcff-152">username</span><span class="sxs-lookup"><span data-stu-id="1bcff-152">username</span></span> |<span data-ttu-id="1bcff-153">Spécifiez le nom d’utilisateur si vous utilisez l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="1bcff-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="1bcff-154">Non</span><span class="sxs-lookup"><span data-stu-id="1bcff-154">No</span></span> |
| <span data-ttu-id="1bcff-155">password</span><span class="sxs-lookup"><span data-stu-id="1bcff-155">password</span></span> |<span data-ttu-id="1bcff-156">Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-156">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="1bcff-157">Non</span><span class="sxs-lookup"><span data-stu-id="1bcff-157">No</span></span> |
| <span data-ttu-id="1bcff-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1bcff-158">gatewayName</span></span> |<span data-ttu-id="1bcff-159">Nom de passerelle hello hello service Data Factory doit utiliser le magasin de données ODBC tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-159">Name of hello gateway that hello Data Factory service should use tooconnect toohello ODBC data store.</span></span> |<span data-ttu-id="1bcff-160">Oui</span><span class="sxs-lookup"><span data-stu-id="1bcff-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="1bcff-161">Utilisation de l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="1bcff-161">Using Basic authentication</span></span>

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
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="1bcff-162">Utilisation de l’authentification de base avec des informations d’identification chiffrées</span><span class="sxs-lookup"><span data-stu-id="1bcff-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="1bcff-163">Vous pouvez chiffrer les informations d’identification hello à l’aide de hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) applet de commande (1.0 version d’Azure PowerShell) ou [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 version ou antérieure de hello Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="1bcff-163">You can encrypt hello credentials using hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of hello Azure PowerShell).</span></span>  

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

### <a name="using-anonymous-authentication"></a><span data-ttu-id="1bcff-164">Utilisation de l’authentification anonyme</span><span class="sxs-lookup"><span data-stu-id="1bcff-164">Using Anonymous authentication</span></span>

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


## <a name="dataset-properties"></a><span data-ttu-id="1bcff-165">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="1bcff-165">Dataset properties</span></span>
<span data-ttu-id="1bcff-166">Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="1bcff-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="1bcff-167">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="1bcff-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="1bcff-168">Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="1bcff-169">jeu de données de type Hello typeProperties section **RelationalTable** (qui comprend de jeu de données ODBC) a hello propriétés suivantes</span><span class="sxs-lookup"><span data-stu-id="1bcff-169">hello typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has hello following properties</span></span>

| <span data-ttu-id="1bcff-170">Propriété</span><span class="sxs-lookup"><span data-stu-id="1bcff-170">Property</span></span> | <span data-ttu-id="1bcff-171">Description</span><span class="sxs-lookup"><span data-stu-id="1bcff-171">Description</span></span> | <span data-ttu-id="1bcff-172">Requis</span><span class="sxs-lookup"><span data-stu-id="1bcff-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1bcff-173">TableName</span><span class="sxs-lookup"><span data-stu-id="1bcff-173">tableName</span></span> |<span data-ttu-id="1bcff-174">Nom de table hello dans le magasin de données ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-174">Name of hello table in hello ODBC data store.</span></span> |<span data-ttu-id="1bcff-175">Oui</span><span class="sxs-lookup"><span data-stu-id="1bcff-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="1bcff-176">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="1bcff-176">Copy activity properties</span></span>
<span data-ttu-id="1bcff-177">Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="1bcff-177">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="1bcff-178">Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités.</span><span class="sxs-lookup"><span data-stu-id="1bcff-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="1bcff-179">Propriétés disponibles dans hello **typeProperties** section de l’activité de hello sur hello autre part varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="1bcff-179">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="1bcff-180">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-180">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="1bcff-181">Dans l’activité de copie, lors de la source est de type **RelationalSource** (qui inclut ODBC), hello propriétés suivantes est disponible dans la section de typeProperties :</span><span class="sxs-lookup"><span data-stu-id="1bcff-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="1bcff-182">Propriété</span><span class="sxs-lookup"><span data-stu-id="1bcff-182">Property</span></span> | <span data-ttu-id="1bcff-183">Description</span><span class="sxs-lookup"><span data-stu-id="1bcff-183">Description</span></span> | <span data-ttu-id="1bcff-184">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="1bcff-184">Allowed values</span></span> | <span data-ttu-id="1bcff-185">Requis</span><span class="sxs-lookup"><span data-stu-id="1bcff-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1bcff-186">query</span><span class="sxs-lookup"><span data-stu-id="1bcff-186">query</span></span> |<span data-ttu-id="1bcff-187">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="1bcff-187">Use hello custom query tooread data.</span></span> |<span data-ttu-id="1bcff-188">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="1bcff-188">SQL query string.</span></span> <span data-ttu-id="1bcff-189">Par exemple : select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="1bcff-189">For example: select * from MyTable.</span></span> |<span data-ttu-id="1bcff-190">Oui</span><span class="sxs-lookup"><span data-stu-id="1bcff-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-tooazure-blob"></a><span data-ttu-id="1bcff-191">Exemple de JSON : tooAzure Blob de magasin de données de copie à partir de données ODBC</span><span class="sxs-lookup"><span data-stu-id="1bcff-191">JSON example: Copy data from ODBC data store tooAzure Blob</span></span>
<span data-ttu-id="1bcff-192">Cet exemple fournit les définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1bcff-192">This example provides JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="1bcff-193">Il montre comment la source de données de toocopy à partir d’une application ODBC tooan stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="1bcff-193">It shows how toocopy data from an ODBC source tooan Azure Blob Storage.</span></span> <span data-ttu-id="1bcff-194">Toutefois, les données peuvent être copié tooany de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1bcff-194">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="1bcff-195">exemple Hello a hello suivant des entités de fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="1bcff-195">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="1bcff-196">Un service lié de type [OnPremisesOdbc](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1bcff-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="1bcff-197">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1bcff-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="1bcff-198">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1bcff-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="1bcff-199">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1bcff-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="1bcff-200">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [RelationalSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1bcff-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="1bcff-201">exemple Hello copie des données à partir d’un résultat de requête dans un blob de tooa de magasin de données ODBC toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="1bcff-201">hello sample copies data from a query result in an ODBC data store tooa blob every hour.</span></span> <span data-ttu-id="1bcff-202">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-202">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="1bcff-203">Dans un premier temps, configurer la passerelle de gestion des données hello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-203">As a first step, set up hello data management gateway.</span></span> <span data-ttu-id="1bcff-204">instructions de Hello sont Bonjour [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="1bcff-204">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="1bcff-205">**Service lié de ODBC** cet exemple utilise hello l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="1bcff-205">**ODBC linked service** This example uses hello Basic authentication.</span></span> <span data-ttu-id="1bcff-206">Consultez la section [Service lié ODBC](#linked-service-properties) pour connaître les différents types d’authentification que vous pouvez utiliser.</span><span class="sxs-lookup"><span data-stu-id="1bcff-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="1bcff-207">**Service lié Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="1bcff-207">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="1bcff-208">**Jeu de données d’entrée ODBC**</span><span class="sxs-lookup"><span data-stu-id="1bcff-208">**ODBC input dataset**</span></span>

<span data-ttu-id="1bcff-209">exemple Hello suppose que vous avez créé une table « MaTable » dans une base de données ODBC et qu’il contient une colonne appelée « timestampcolumn » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="1bcff-209">hello sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="1bcff-210">Paramètre « external » : « true » informe service Data Factory de hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-210">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="1bcff-211">**Jeu de données de sortie d’objet Blob Azure**</span><span class="sxs-lookup"><span data-stu-id="1bcff-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="1bcff-212">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="1bcff-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="1bcff-213">chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="1bcff-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="1bcff-214">chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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


<span data-ttu-id="1bcff-215">**Activité de copie dans un pipeline, avec une source ODBC (RelationalSource) et un récepteur blob (BlobSink)**</span><span class="sxs-lookup"><span data-stu-id="1bcff-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="1bcff-216">pipeline de Hello contient une activité de copie qui est configuré toouse ces jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="1bcff-216">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="1bcff-217">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**RelationalSource** et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="1bcff-217">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="1bcff-218">la requête SQL Hello spécifiée pour hello **requête** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.</span><span class="sxs-lookup"><span data-stu-id="1bcff-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="1bcff-219">Mappage de type pour ODBC</span><span class="sxs-lookup"><span data-stu-id="1bcff-219">Type mapping for ODBC</span></span>
<span data-ttu-id="1bcff-220">Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, l’activité de copie effectue les conversions de type automatique à partir de types de sources de toosink types avec hello suivant l’approche en deux étapes :</span><span class="sxs-lookup"><span data-stu-id="1bcff-220">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="1bcff-221">Convertir à partir de la source native types too.NET type</span><span class="sxs-lookup"><span data-stu-id="1bcff-221">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="1bcff-222">Conversion de type de récepteur de toonative de type .NET</span><span class="sxs-lookup"><span data-stu-id="1bcff-222">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="1bcff-223">Lors du déplacement des données à partir de magasins de données ODBC, types de données ODBC sont mappés too.NET types comme indiqué dans hello [les mappages de types de données ODBC](https://msdn.microsoft.com/library/cc668763.aspx) rubrique.</span><span class="sxs-lookup"><span data-stu-id="1bcff-223">When moving data from ODBC data stores, ODBC data types are mapped too.NET types as mentioned in hello [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="1bcff-224">Mapper les colonnes de source toosink</span><span class="sxs-lookup"><span data-stu-id="1bcff-224">Map source toosink columns</span></span>
<span data-ttu-id="1bcff-225">toolearn sur le mappage des colonnes dans toocolumns du jeu de données source dans le jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="1bcff-225">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="1bcff-226">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="1bcff-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="1bcff-227">Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="1bcff-227">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="1bcff-228">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="1bcff-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="1bcff-229">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="1bcff-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="1bcff-230">Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée.</span><span class="sxs-lookup"><span data-stu-id="1bcff-230">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="1bcff-231">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="1bcff-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="1bcff-232">Magasin GE Historian</span><span class="sxs-lookup"><span data-stu-id="1bcff-232">GE Historian store</span></span>
<span data-ttu-id="1bcff-233">Vous créez un toolink de service ODBC lié un [GE Proficy historien (désormais GE historien)](http://www.geautomation.com/products/proficy-historian) tooan service Azure data factory du magasin de données comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1bcff-233">You create an ODBC linked service toolink a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store tooan Azure data factory as shown in hello following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of hello GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="1bcff-234">Installer la passerelle de gestion des données sur une machine locale et inscrire la passerelle de hello via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-234">Install Data Management Gateway on an on-premises machine and register hello gateway with hello portal.</span></span> <span data-ttu-id="1bcff-235">passerelle Hello installé sur votre ordinateur local utilise le pilote ODBC de hello pour GE historien tooconnect toohello magasin de données GE historien.</span><span class="sxs-lookup"><span data-stu-id="1bcff-235">hello gateway installed on your on-premises computer uses hello ODBC driver for GE Historian tooconnect toohello GE Historian data store.</span></span> <span data-ttu-id="1bcff-236">Par conséquent, installez les pilotes hello s’il n’est pas déjà installé sur l’ordinateur de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-236">Therefore, install hello driver if it is not already installed on hello gateway machine.</span></span> <span data-ttu-id="1bcff-237">Consultez la section [Activation de la connectivité](#enabling-connectivity) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="1bcff-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="1bcff-238">Avant d’utiliser hello GE historien stocker dans une solution de fabrique de données, vérifiez si la passerelle de hello peut se connecter toohello magasin de données à l’aide des instructions dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="1bcff-238">Before you use hello GE Historian store in a Data Factory solution, verify whether hello gateway can connect toohello data store using instructions in hello next section.</span></span>

<span data-ttu-id="1bcff-239">Article de hello en lecture à partir du début de hello pour obtenir une présentation détaillée de l’utilisation de données ODBC stocke en tant que magasins de données source dans une opération de copie.</span><span class="sxs-lookup"><span data-stu-id="1bcff-239">Read hello article from hello beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="1bcff-240">Résoudre les problèmes de connectivité</span><span class="sxs-lookup"><span data-stu-id="1bcff-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="1bcff-241">tootroubleshoot des problèmes de connexion, utilisez hello **Diagnostics** onglet de **Gestionnaire de Configuration de passerelle de gestion de données**.</span><span class="sxs-lookup"><span data-stu-id="1bcff-241">tootroubleshoot connection issues, use hello **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="1bcff-242">Lancez le **Gestionnaire de configuration de la passerelle de gestion des données**.</span><span class="sxs-lookup"><span data-stu-id="1bcff-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="1bcff-243">Vous pouvez exécuter « C:\Program Files\Microsoft données Gestion Gateway\1.0\Shared\ConfigManager.exe « directement (ou) recherche pour **passerelle** toofind un lien trop**passerelle de gestion des données Microsoft** application, comme illustré dans hello suivant l’image.</span><span class="sxs-lookup"><span data-stu-id="1bcff-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** toofind a link too**Microsoft Data Management Gateway** application as shown in hello following image.</span></span>

    ![Rechercher la passerelle](./media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="1bcff-245">Commutateur toohello **Diagnostics** onglet.</span><span class="sxs-lookup"><span data-stu-id="1bcff-245">Switch toohello **Diagnostics** tab.</span></span>

    ![Diagnostics de la passerelle](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="1bcff-247">Sélectionnez hello **type** de stocker des données (lié de service).</span><span class="sxs-lookup"><span data-stu-id="1bcff-247">Select hello **type** of data store (linked service).</span></span>
4. <span data-ttu-id="1bcff-248">Spécifiez **authentification** et entrez **informations d’identification** (ou) entrez **chaîne de connexion** qui est le magasin de données toohello tooconnect utilisé.</span><span class="sxs-lookup"><span data-stu-id="1bcff-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used tooconnect toohello data store.</span></span>
5. <span data-ttu-id="1bcff-249">Cliquez sur **tester la connexion** magasin de données toohello tootest hello connexion.</span><span class="sxs-lookup"><span data-stu-id="1bcff-249">Click **Test connection** tootest hello connection toohello data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="1bcff-250">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="1bcff-250">Performance and Tuning</span></span>
<span data-ttu-id="1bcff-251">Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="1bcff-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
