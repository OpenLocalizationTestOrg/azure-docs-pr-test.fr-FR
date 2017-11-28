---
title: "tooand de données aaaMove à partir de SQL Server | Documents Microsoft"
description: "Obtenir des informations sur comment les données de toomove vers/à partir de SQL Server de base de données qui est local ou dans une machine virtuelle de Azure à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="6ea38-103">Déplacer les données tooand à partir de SQL Server sur site ou sur IaaS (machine virtuelle Azure) à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="6ea38-103">Move data tooand from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="6ea38-104">Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory vers/à partir d’une base de données SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="6ea38-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="6ea38-105">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="6ea38-106">Scénarios pris en charge</span><span class="sxs-lookup"><span data-stu-id="6ea38-106">Supported scenarios</span></span>
<span data-ttu-id="6ea38-107">Vous pouvez copier des données **à partir d’une base de données SQL Server** toohello suivant des magasins de données :</span><span class="sxs-lookup"><span data-stu-id="6ea38-107">You can copy data **from a SQL Server database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="6ea38-108">Vous pouvez copier des données à partir de hello suivant des magasins de données **base de données SQL Server tooa**:</span><span class="sxs-lookup"><span data-stu-id="6ea38-108">You can copy data from hello following data stores **tooa SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="6ea38-109">Versions de SQL Server prises en charge</span><span class="sxs-lookup"><span data-stu-id="6ea38-109">Supported SQL Server versions</span></span>
<span data-ttu-id="6ea38-110">Cette prise en charge du connecteur SQL Server copie des données à partir de / toohello suivant les versions de l’instance hébergée localement ou IaaS Azure à l’aide de l’authentification SQL et l’authentification Windows : SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span><span class="sxs-lookup"><span data-stu-id="6ea38-110">This SQL Server connector support copying data from/toohello following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="6ea38-111">Activation de la connectivité</span><span class="sxs-lookup"><span data-stu-id="6ea38-111">Enabling connectivity</span></span>
<span data-ttu-id="6ea38-112">concepts de Hello et les étapes nécessaires pour la connexion avec SQL Server hébergé localement ou dans Azure IaaS (Infrastructure-as-a-Service) VMs sont hello même.</span><span class="sxs-lookup"><span data-stu-id="6ea38-112">hello concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are hello same.</span></span> <span data-ttu-id="6ea38-113">Dans les deux cas, vous devez toouse passerelle de gestion des données pour la connectivité.</span><span class="sxs-lookup"><span data-stu-id="6ea38-113">In both cases, you need toouse Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="6ea38-114">Consultez [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn l’article sur la passerelle de gestion des données et des instructions détaillées sur la configuration de passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-114">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="6ea38-115">La configuration d’une instance de passerelle est pré requise pour la connexion avec SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6ea38-115">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="6ea38-116">Pendant que vous pouvez installer la passerelle sur hello même local instance de machine virtuelle d’ordinateur ou le cloud comme hello SQL Server pour de meilleures performances, nous vous recommandons de les installer sur des ordinateurs distincts.</span><span class="sxs-lookup"><span data-stu-id="6ea38-116">While you can install gateway on hello same on-premises machine or cloud VM instance as hello SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="6ea38-117">Passerelle de hello et SQL Server sur des ordinateurs distincts réduit la contention des ressources.</span><span class="sxs-lookup"><span data-stu-id="6ea38-117">Having hello gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="6ea38-118">Prise en main</span><span class="sxs-lookup"><span data-stu-id="6ea38-118">Getting started</span></span>
<span data-ttu-id="6ea38-119">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers/depuis une base de données SQL Server à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="6ea38-119">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="6ea38-120">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="6ea38-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="6ea38-121">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="6ea38-122">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="6ea38-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="6ea38-123">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="6ea38-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="6ea38-124">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="6ea38-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="6ea38-125">Création d'une **fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="6ea38-125">Create a **data factory**.</span></span> <span data-ttu-id="6ea38-126">Une fabrique de données peut contenir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="6ea38-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="6ea38-127">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="6ea38-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="6ea38-128">Par exemple, si vous copiez des données à partir d’un tooan de base de données SQL Server stockage d’objets blob Azure, vous créez deux services liés toolink votre base de données SQL Server et de la fabrique de données de stockage Azure compte tooyour.</span><span class="sxs-lookup"><span data-stu-id="6ea38-128">For example, if you are copying data from a SQL Server database tooan Azure blob storage, you create two linked services toolink your SQL Server database and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="6ea38-129">Pour les propriétés de service lié qui sont la base de données du serveur tooSQL spécifiques, consultez [lié des propriétés du service](#linked-service-properties) section.</span><span class="sxs-lookup"><span data-stu-id="6ea38-129">For linked service properties that are specific tooSQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="6ea38-130">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="6ea38-131">Dans l’exemple hello mentionné dans la dernière étape de hello, vous créez une table de dataset toospecify hello SQL dans votre base de données SQL Server qui contient les données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-131">In hello example mentioned in hello last step, you create a dataset toospecify hello SQL table in your SQL Server database that contains hello input data.</span></span> <span data-ttu-id="6ea38-132">Vous créez un autre conteneur d’objets blob dataset toospecify hello et dossier hello qui contient les données de salutation provenant de hello de base de données SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6ea38-132">And, you create another dataset toospecify hello blob container and hello folder that holds hello data copied from hello SQL Server database.</span></span> <span data-ttu-id="6ea38-133">Pour les propriétés du dataset qui sont la base de données du serveur tooSQL spécifiques, consultez [propriétés du dataset](#dataset-properties) section.</span><span class="sxs-lookup"><span data-stu-id="6ea38-133">For dataset properties that are specific tooSQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="6ea38-134">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="6ea38-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="6ea38-135">Dans l’exemple hello mentionné précédemment, vous utilisez SqlSource en tant que source et BlobSink comme un récepteur pour l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-135">In hello example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for hello copy activity.</span></span> <span data-ttu-id="6ea38-136">De même, si vous copiez à partir du stockage d’objets Blob Azure tooSQL serveur de base de données, vous utilisez BlobSource et SqlSink dans l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-136">Similarly, if you are copying from Azure Blob Storage tooSQL Server Database, you use BlobSource and SqlSink in hello copy activity.</span></span> <span data-ttu-id="6ea38-137">Pour les propriétés d’activité de copie sont tooSQL spécifique de base de données de serveur, consultez [copier les propriétés de l’activité](#copy-activity-properties) section.</span><span class="sxs-lookup"><span data-stu-id="6ea38-137">For copy activity properties that are specific tooSQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="6ea38-138">Pour plus d’informations sur comment toouse du magasin de données source ou un récepteur, cliquez sur le lien hello dans la section précédente de hello pour votre magasin de données.</span><span class="sxs-lookup"><span data-stu-id="6ea38-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span> 

<span data-ttu-id="6ea38-139">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="6ea38-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="6ea38-140">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="6ea38-141">Pour obtenir des exemples avec des définitions de JSON pour les entités de fabrique de données qui sont utilisés toocopy des données vers/à partir d’une base de données locale SQL Server, consultez [exemples JSON](#json-examples-for-copying-data-from-and-to-sql-server) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="6ea38-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="6ea38-142">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifique tooSQL Server :</span><span class="sxs-lookup"><span data-stu-id="6ea38-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooSQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="6ea38-143">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="6ea38-143">Linked service properties</span></span>
<span data-ttu-id="6ea38-144">Vous créez un service lié de type **OnPremisesSqlServer** toolink une fabrique de données de tooa de base de données locale SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6ea38-144">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="6ea38-145">Hello tableau suivant fournit la description du service de SQL Server lié JSON éléments tooon local spécifique.</span><span class="sxs-lookup"><span data-stu-id="6ea38-145">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="6ea38-146">Hello tableau suivant fournit la description pour JSON éléments tooSQL spécifique service du serveur lié.</span><span class="sxs-lookup"><span data-stu-id="6ea38-146">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="6ea38-147">Propriété</span><span class="sxs-lookup"><span data-stu-id="6ea38-147">Property</span></span> | <span data-ttu-id="6ea38-148">Description</span><span class="sxs-lookup"><span data-stu-id="6ea38-148">Description</span></span> | <span data-ttu-id="6ea38-149">Requis</span><span class="sxs-lookup"><span data-stu-id="6ea38-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ea38-150">type</span><span class="sxs-lookup"><span data-stu-id="6ea38-150">type</span></span> |<span data-ttu-id="6ea38-151">propriété de type Hello doit indiquer : **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="6ea38-151">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="6ea38-152">Oui</span><span class="sxs-lookup"><span data-stu-id="6ea38-152">Yes</span></span> |
| <span data-ttu-id="6ea38-153">connectionString</span><span class="sxs-lookup"><span data-stu-id="6ea38-153">connectionString</span></span> |<span data-ttu-id="6ea38-154">Spécifiez les informations connectionString nécessaires de base de données SQL Server tooconnect toohello local à l’aide de l’authentification Windows ou authentification SQL.</span><span class="sxs-lookup"><span data-stu-id="6ea38-154">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="6ea38-155">Oui</span><span class="sxs-lookup"><span data-stu-id="6ea38-155">Yes</span></span> |
| <span data-ttu-id="6ea38-156">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6ea38-156">gatewayName</span></span> |<span data-ttu-id="6ea38-157">Nom de passerelle hello hello service Data Factory doit utiliser la base de données SQL Server tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="6ea38-157">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="6ea38-158">Oui</span><span class="sxs-lookup"><span data-stu-id="6ea38-158">Yes</span></span> |
| <span data-ttu-id="6ea38-159">username</span><span class="sxs-lookup"><span data-stu-id="6ea38-159">username</span></span> |<span data-ttu-id="6ea38-160">Spécifiez le nom d’utilisateur si vous utilisez l’authentification Windows.</span><span class="sxs-lookup"><span data-stu-id="6ea38-160">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="6ea38-161">Exemple : **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="6ea38-161">Example: **domainname\\username**.</span></span> |<span data-ttu-id="6ea38-162">Non</span><span class="sxs-lookup"><span data-stu-id="6ea38-162">No</span></span> |
| <span data-ttu-id="6ea38-163">password</span><span class="sxs-lookup"><span data-stu-id="6ea38-163">password</span></span> |<span data-ttu-id="6ea38-164">Spécifiez le mot de passe de compte d’utilisateur hello que vous avez spécifié pour le nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-164">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="6ea38-165">Non</span><span class="sxs-lookup"><span data-stu-id="6ea38-165">No</span></span> |

<span data-ttu-id="6ea38-166">Vous pouvez chiffrer les informations d’identification à l’aide de hello **New-AzureRmDataFactoryEncryptValue** applet de commande et les utiliser dans la chaîne de connexion hello comme indiqué dans hello exemple suivant (**EncryptedCredential** propriété) :</span><span class="sxs-lookup"><span data-stu-id="6ea38-166">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="6ea38-167">Exemples</span><span class="sxs-lookup"><span data-stu-id="6ea38-167">Samples</span></span>
<span data-ttu-id="6ea38-168">**JSON pour utilisation de l’authentification SQL**</span><span class="sxs-lookup"><span data-stu-id="6ea38-168">**JSON for using SQL Authentication**</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
<span data-ttu-id="6ea38-169">**JSON pour utilisation de l’authentification Windows**</span><span class="sxs-lookup"><span data-stu-id="6ea38-169">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="6ea38-170">Passerelle de gestion des données emprunte l’identité hello spécifié compte tooconnect toohello local SQL Server base de données utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6ea38-170">Data Management Gateway will impersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="6ea38-171">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="6ea38-171">Dataset properties</span></span>
<span data-ttu-id="6ea38-172">Dans les exemples de hello, vous avez utilisé un jeu de données de type **SqlServerTable** toorepresent une table dans une base de données SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6ea38-172">In hello samples, you have used a dataset of type **SqlServerTable** toorepresent a table in a SQL Server database.</span></span>  

<span data-ttu-id="6ea38-173">Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="6ea38-173">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="6ea38-174">Les sections comme la structure, la disponibilité et la stratégie d’un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Server, objet Blob Azure, table Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="6ea38-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="6ea38-175">section de typeProperties Hello est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-175">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="6ea38-176">Hello **typeProperties** section hello le jeu de données de type **SqlServerTable** a hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="6ea38-176">hello **typeProperties** section for hello dataset of type **SqlServerTable** has hello following properties:</span></span>

| <span data-ttu-id="6ea38-177">Propriété</span><span class="sxs-lookup"><span data-stu-id="6ea38-177">Property</span></span> | <span data-ttu-id="6ea38-178">Description</span><span class="sxs-lookup"><span data-stu-id="6ea38-178">Description</span></span> | <span data-ttu-id="6ea38-179">Requis</span><span class="sxs-lookup"><span data-stu-id="6ea38-179">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ea38-180">TableName</span><span class="sxs-lookup"><span data-stu-id="6ea38-180">tableName</span></span> |<span data-ttu-id="6ea38-181">Nom de la table de hello ou la vue d’instance de base de données SQL Server hello service lié fait référence à.</span><span class="sxs-lookup"><span data-stu-id="6ea38-181">Name of hello table or view in hello SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="6ea38-182">Oui</span><span class="sxs-lookup"><span data-stu-id="6ea38-182">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="6ea38-183">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="6ea38-183">Copy activity properties</span></span>
<span data-ttu-id="6ea38-184">Si vous déplacez des données à partir d’une base de données SQL Server, vous définissez type de source de hello dans l’activité de copie hello trop**SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="6ea38-184">If you are moving data from a SQL Server database, you set hello source type in hello copy activity too**SqlSource**.</span></span> <span data-ttu-id="6ea38-185">De même, si vous déplacez une base de données tooa SQL Server, vous définir le type de récepteur hello dans l’activité de copie hello trop**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="6ea38-185">Similarly, if you are moving data tooa SQL Server database, you set hello sink type in hello copy activity too**SqlSink**.</span></span> <span data-ttu-id="6ea38-186">Cette section fournit une liste de propriétés prises en charge par SqlSource et SqlSink.</span><span class="sxs-lookup"><span data-stu-id="6ea38-186">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="6ea38-187">Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="6ea38-187">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6ea38-188">Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités.</span><span class="sxs-lookup"><span data-stu-id="6ea38-188">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="6ea38-189">Hello activité de copie accepte uniquement une entrée et produit qu’une seule sortie.</span><span class="sxs-lookup"><span data-stu-id="6ea38-189">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="6ea38-190">Alors que les propriétés disponibles dans la section typeProperties hello activité hello varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="6ea38-190">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="6ea38-191">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-191">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="6ea38-192">SqlSource</span><span class="sxs-lookup"><span data-stu-id="6ea38-192">SqlSource</span></span>
<span data-ttu-id="6ea38-193">Lorsque la source dans une activité de copie est de type **SqlSource**, hello propriétés suivantes est disponible dans **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="6ea38-193">When source in a copy activity is of type **SqlSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="6ea38-194">Propriété</span><span class="sxs-lookup"><span data-stu-id="6ea38-194">Property</span></span> | <span data-ttu-id="6ea38-195">Description</span><span class="sxs-lookup"><span data-stu-id="6ea38-195">Description</span></span> | <span data-ttu-id="6ea38-196">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="6ea38-196">Allowed values</span></span> | <span data-ttu-id="6ea38-197">Requis</span><span class="sxs-lookup"><span data-stu-id="6ea38-197">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6ea38-198">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="6ea38-198">sqlReaderQuery</span></span> |<span data-ttu-id="6ea38-199">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="6ea38-199">Use hello custom query tooread data.</span></span> |<span data-ttu-id="6ea38-200">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="6ea38-200">SQL query string.</span></span> <span data-ttu-id="6ea38-201">Par exemple : select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="6ea38-201">For example: select * from MyTable.</span></span> <span data-ttu-id="6ea38-202">Peut faire référence à plusieurs tables de base de données hello référencé par le jeu de données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-202">May reference multiple tables from hello database referenced by hello input dataset.</span></span> <span data-ttu-id="6ea38-203">Si non spécifié, hello instruction SQL exécutée : select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="6ea38-203">If not specified, hello SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="6ea38-204">Non</span><span class="sxs-lookup"><span data-stu-id="6ea38-204">No</span></span> |
| <span data-ttu-id="6ea38-205">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="6ea38-205">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="6ea38-206">Nom de hello procédure stockée qui lit les données à partir de la table de source de hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-206">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="6ea38-207">Nom de hello procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="6ea38-207">Name of hello stored procedure.</span></span> <span data-ttu-id="6ea38-208">instruction SQL de la dernière Hello doit être une instruction SELECT dans la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-208">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="6ea38-209">Non</span><span class="sxs-lookup"><span data-stu-id="6ea38-209">No</span></span> |
| <span data-ttu-id="6ea38-210">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="6ea38-210">storedProcedureParameters</span></span> |<span data-ttu-id="6ea38-211">Pourquoi les paramètres de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="6ea38-211">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="6ea38-212">Paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="6ea38-212">Name/value pairs.</span></span> <span data-ttu-id="6ea38-213">Noms et la casse des paramètres doivent correspondre à des noms de hello et la casse des paramètres de la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-213">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="6ea38-214">Non</span><span class="sxs-lookup"><span data-stu-id="6ea38-214">No</span></span> |

<span data-ttu-id="6ea38-215">Si hello **sqlReaderQuery** est spécifié pour hello SqlSource, hello activité de copie s’exécute cette requête sur des données hello tooget hello base de données SQL Server source.</span><span class="sxs-lookup"><span data-stu-id="6ea38-215">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span>

<span data-ttu-id="6ea38-216">Ou bien, vous pouvez spécifier une procédure stockée en spécifiant hello **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si hello une procédure stockée accepte des paramètres).</span><span class="sxs-lookup"><span data-stu-id="6ea38-216">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="6ea38-217">Si vous ne spécifiez pas de sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes de hello définis dans la section de structure hello sont utilisée toobuild un toorun requête select sur hello de base de données SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6ea38-217">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="6ea38-218">Si la définition de dataset hello n’a pas de structure de hello, toutes les colonnes sont sélectionnées à partir de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-218">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="6ea38-219">Lorsque vous utilisez **sqlReaderStoredProcedureName**, vous devez toujours toospecify une valeur pour hello **tableName** propriété dans le dataset hello JSON.</span><span class="sxs-lookup"><span data-stu-id="6ea38-219">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="6ea38-220">Cependant, il n’existe aucune validation effectuée pour cette table.</span><span class="sxs-lookup"><span data-stu-id="6ea38-220">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="6ea38-221">SqlSink</span><span class="sxs-lookup"><span data-stu-id="6ea38-221">SqlSink</span></span>
<span data-ttu-id="6ea38-222">**SqlSink** prend en charge hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="6ea38-222">**SqlSink** supports hello following properties:</span></span>

| <span data-ttu-id="6ea38-223">Propriété</span><span class="sxs-lookup"><span data-stu-id="6ea38-223">Property</span></span> | <span data-ttu-id="6ea38-224">Description</span><span class="sxs-lookup"><span data-stu-id="6ea38-224">Description</span></span> | <span data-ttu-id="6ea38-225">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="6ea38-225">Allowed values</span></span> | <span data-ttu-id="6ea38-226">Requis</span><span class="sxs-lookup"><span data-stu-id="6ea38-226">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6ea38-227">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="6ea38-227">writeBatchTimeout</span></span> |<span data-ttu-id="6ea38-228">Temps d’attente pour hello lot insert opération toocomplete avant d’expirer.</span><span class="sxs-lookup"><span data-stu-id="6ea38-228">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="6ea38-229">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="6ea38-229">timespan</span></span><br/><br/> <span data-ttu-id="6ea38-230">Exemple : « 00:30:00 » (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="6ea38-230">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="6ea38-231">Non</span><span class="sxs-lookup"><span data-stu-id="6ea38-231">No</span></span> |
| <span data-ttu-id="6ea38-232">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="6ea38-232">writeBatchSize</span></span> |<span data-ttu-id="6ea38-233">Insère des données dans une table SQL de hello lorsque la taille de mémoire tampon de hello atteint la valeur writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="6ea38-233">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="6ea38-234">Nombre entier (nombre de lignes)</span><span class="sxs-lookup"><span data-stu-id="6ea38-234">Integer (number of rows)</span></span> |<span data-ttu-id="6ea38-235">Non (valeur par défaut : 10000)</span><span class="sxs-lookup"><span data-stu-id="6ea38-235">No (default: 10000)</span></span> |
| <span data-ttu-id="6ea38-236">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="6ea38-236">sqlWriterCleanupScript</span></span> |<span data-ttu-id="6ea38-237">Spécifier la requête pour l’activité de copie tooexecute telles que les données d’un secteur spécifique sont nettoyées.</span><span class="sxs-lookup"><span data-stu-id="6ea38-237">Specify query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="6ea38-238">Pour en savoir plus, voir la section [Copie renouvelée](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="6ea38-238">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="6ea38-239">Une instruction de requête.</span><span class="sxs-lookup"><span data-stu-id="6ea38-239">A query statement.</span></span> |<span data-ttu-id="6ea38-240">Non</span><span class="sxs-lookup"><span data-stu-id="6ea38-240">No</span></span> |
| <span data-ttu-id="6ea38-241">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="6ea38-241">sliceIdentifierColumnName</span></span> |<span data-ttu-id="6ea38-242">Spécifiez nom de colonne pour l’activité de copie toofill avec l’identificateur de secteur généré automatiquement, qui est utilisé tooclean des données d’un secteur spécifique quand réexécutée.</span><span class="sxs-lookup"><span data-stu-id="6ea38-242">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="6ea38-243">Pour en savoir plus, voir la section [Copie renouvelée](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="6ea38-243">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="6ea38-244">Nom d’une colonne avec le type de données binary(32).</span><span class="sxs-lookup"><span data-stu-id="6ea38-244">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="6ea38-245">Non</span><span class="sxs-lookup"><span data-stu-id="6ea38-245">No</span></span> |
| <span data-ttu-id="6ea38-246">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="6ea38-246">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="6ea38-247">Nom de hello procédure stockée que les données upserts (mises à jour/insertion) dans la table cible hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-247">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="6ea38-248">Nom de hello procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="6ea38-248">Name of hello stored procedure.</span></span> |<span data-ttu-id="6ea38-249">Non</span><span class="sxs-lookup"><span data-stu-id="6ea38-249">No</span></span> |
| <span data-ttu-id="6ea38-250">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="6ea38-250">storedProcedureParameters</span></span> |<span data-ttu-id="6ea38-251">Pourquoi les paramètres de procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="6ea38-251">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="6ea38-252">Paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="6ea38-252">Name/value pairs.</span></span> <span data-ttu-id="6ea38-253">Noms et la casse des paramètres doivent correspondre à des noms de hello et la casse des paramètres de la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-253">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="6ea38-254">Non</span><span class="sxs-lookup"><span data-stu-id="6ea38-254">No</span></span> |
| <span data-ttu-id="6ea38-255">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="6ea38-255">sqlWriterTableType</span></span> |<span data-ttu-id="6ea38-256">Spécifiez toobe de nom de type de table utilisée dans la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-256">Specify table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="6ea38-257">Activité de copie rend les données de hello déplacées disponibles dans une table temporaire avec ce type de table.</span><span class="sxs-lookup"><span data-stu-id="6ea38-257">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="6ea38-258">Code de procédure stockée puis de fusionner des données hello copiées avec les données existantes.</span><span class="sxs-lookup"><span data-stu-id="6ea38-258">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="6ea38-259">Nom de type de table.</span><span class="sxs-lookup"><span data-stu-id="6ea38-259">A table type name.</span></span> |<span data-ttu-id="6ea38-260">Non</span><span class="sxs-lookup"><span data-stu-id="6ea38-260">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a><span data-ttu-id="6ea38-261">Exemples JSON pour copier des données à partir d’et tooSQL Server</span><span class="sxs-lookup"><span data-stu-id="6ea38-261">JSON examples for copying data from and tooSQL Server</span></span>
<span data-ttu-id="6ea38-262">Hello exemples suivants proposent des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6ea38-262">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="6ea38-263">Hello suivant exemples indiquent comment tooand de données toocopy à partir de SQL Server et le stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="6ea38-263">hello following samples show how toocopy data tooand from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="6ea38-264">Toutefois, les données peuvent être copiées **directement** de n’importe quelle tooany de sources de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6ea38-264">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a><span data-ttu-id="6ea38-265">Exemple : Copier des données à partir de SQL Server tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="6ea38-265">Example: Copy data from SQL Server tooAzure Blob</span></span>
<span data-ttu-id="6ea38-266">Hello ci-dessous illustre d’exemple :</span><span class="sxs-lookup"><span data-stu-id="6ea38-266">hello following sample shows:</span></span>

1. <span data-ttu-id="6ea38-267">Service lié de type [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6ea38-267">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="6ea38-268">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6ea38-268">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="6ea38-269">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [SqlServerTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6ea38-269">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="6ea38-270">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6ea38-270">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="6ea38-271">Hello [pipeline](data-factory-create-pipelines.md) avec l’activité de copie qui utilise [SqlSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="6ea38-271">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="6ea38-272">exemple Hello copie des données de série chronologique à partir d’un tooan de table SQL Server Azure blob toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="6ea38-272">hello sample copies time-series data from a SQL Server table tooan Azure blob every hour.</span></span> <span data-ttu-id="6ea38-273">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-273">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="6ea38-274">Dans un premier temps, le programme d’installation passerelle de gestion des données hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-274">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="6ea38-275">instructions de Hello sont Bonjour [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="6ea38-275">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="6ea38-276">**Service SQL Server lié**</span><span class="sxs-lookup"><span data-stu-id="6ea38-276">**SQL Server linked service**</span></span>
```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="6ea38-277">**Service lié Azure Blob Storage**</span><span class="sxs-lookup"><span data-stu-id="6ea38-277">**Azure Blob storage linked service**</span></span>

```json
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
<span data-ttu-id="6ea38-278">**Jeu de données d’entrée de SQL Server**</span><span class="sxs-lookup"><span data-stu-id="6ea38-278">**SQL Server input dataset**</span></span>

<span data-ttu-id="6ea38-279">exemple Hello suppose que vous avez créé une table « MyTable » dans SQL Server et il contienne une colonne appelée « timestampcolumn » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="6ea38-279">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="6ea38-280">Vous pouvez interroger sur plusieurs tables en hello même à l’aide d’un dataset unique, mais une seule table de base de données doit être utilisé pour typeProperty de tableName hello du groupe de données.</span><span class="sxs-lookup"><span data-stu-id="6ea38-280">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="6ea38-281">Paramètre « external » : « true » informe service Data Factory ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-281">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "SqlServerInput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
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
<span data-ttu-id="6ea38-282">**Jeu de données de sortie d’objet Blob Azure**</span><span class="sxs-lookup"><span data-stu-id="6ea38-282">**Azure Blob output dataset**</span></span>

<span data-ttu-id="6ea38-283">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="6ea38-283">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6ea38-284">chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="6ea38-284">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="6ea38-285">chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-285">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
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
<span data-ttu-id="6ea38-286">**Pipeline avec activité de copie**</span><span class="sxs-lookup"><span data-stu-id="6ea38-286">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="6ea38-287">pipeline de Hello contient une activité de copie qui est configuré toouse ces jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="6ea38-287">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="6ea38-288">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**SqlSource** et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="6ea38-288">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="6ea38-289">la requête SQL Hello spécifiée pour hello **SqlReaderQuery** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.</span><span class="sxs-lookup"><span data-stu-id="6ea38-289">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
<span data-ttu-id="6ea38-290">Dans cet exemple, **sqlReaderQuery** est spécifié pour hello SqlSource.</span><span class="sxs-lookup"><span data-stu-id="6ea38-290">In this example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="6ea38-291">Hello activité de copie s’exécute cette requête par rapport aux données de base de données SQL Server source tooget hello de hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-291">hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span> <span data-ttu-id="6ea38-292">Ou bien, vous pouvez spécifier une procédure stockée en spécifiant hello **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si hello une procédure stockée accepte des paramètres).</span><span class="sxs-lookup"><span data-stu-id="6ea38-292">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span> <span data-ttu-id="6ea38-293">Hello sqlReaderQuery permettre faire référence à plusieurs tables de base de données hello référencé par le jeu de données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-293">hello sqlReaderQuery can reference multiple tables within hello database referenced by hello input dataset.</span></span> <span data-ttu-id="6ea38-294">Il n’est pas limité tooonly hello tableau comme hello typeProperty de tableName du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="6ea38-294">It is not limited tooonly hello table set as hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="6ea38-295">Si vous ne spécifiez pas sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes de hello définis dans la section de structure hello sont utilisée toobuild un toorun requête select sur hello de base de données SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6ea38-295">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="6ea38-296">Si la définition de dataset hello n’a pas de structure de hello, toutes les colonnes sont sélectionnées à partir de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-296">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="6ea38-297">Consultez hello [Sql Source](#sqlsource) section et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) pour la liste de propriétés prises en charge par SqlSource et BlobSink hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-297">See hello [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-toosql-server"></a><span data-ttu-id="6ea38-298">Exemple : Copier des données d’objets Blob Azure tooSQL Server</span><span class="sxs-lookup"><span data-stu-id="6ea38-298">Example: Copy data from Azure Blob tooSQL Server</span></span>
<span data-ttu-id="6ea38-299">Hello ci-dessous illustre d’exemple :</span><span class="sxs-lookup"><span data-stu-id="6ea38-299">hello following sample shows:</span></span>

1. <span data-ttu-id="6ea38-300">Hello liés de service de type [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6ea38-300">hello linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="6ea38-301">Hello liés de service de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6ea38-301">hello linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="6ea38-302">Un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6ea38-302">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="6ea38-303">un [jeu de données](data-factory-create-datasets.md) de sortie de type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties) ;</span><span class="sxs-lookup"><span data-stu-id="6ea38-303">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="6ea38-304">Hello [pipeline](data-factory-create-pipelines.md) avec l’activité de copie qui utilise [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) et [SqlSink](#sql-server-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="6ea38-304">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="6ea38-305">exemple Hello copie les données de séries chronologiques à partir d’une table de SQL Server tooa objets blob Azure toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="6ea38-305">hello sample copies time-series data from an Azure blob tooa SQL Server table every hour.</span></span> <span data-ttu-id="6ea38-306">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-306">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="6ea38-307">**Service SQL Server lié**</span><span class="sxs-lookup"><span data-stu-id="6ea38-307">**SQL Server linked service**</span></span>

```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="6ea38-308">**Service lié Azure Blob Storage**</span><span class="sxs-lookup"><span data-stu-id="6ea38-308">**Azure Blob storage linked service**</span></span>

```json
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
<span data-ttu-id="6ea38-309">**Jeu de données d'entrée d'objet Blob Azure**</span><span class="sxs-lookup"><span data-stu-id="6ea38-309">**Azure Blob input dataset**</span></span>

<span data-ttu-id="6ea38-310">Les données sont récupérées à partir d'un nouvel objet Blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="6ea38-310">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6ea38-311">nom de chemin d’accès et de dossier pour l’objet blob de hello Hello sont dynamiquement évaluées en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="6ea38-311">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="6ea38-312">chemin d’accès du dossier Hello utilise la partie jour de l’heure de début hello, mois et année et nom de fichier partie d’heure hello de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-312">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="6ea38-313">« external » : « true » paramètre informe le service de fabrique de données de hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-313">“external”: “true” setting informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
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
<span data-ttu-id="6ea38-314">**Jeu de données de sortie de SQL Server**</span><span class="sxs-lookup"><span data-stu-id="6ea38-314">**SQL Server output dataset**</span></span>

<span data-ttu-id="6ea38-315">exemple Hello copie table tooa de données nommé « MyTable » dans SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6ea38-315">hello sample copies data tooa table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="6ea38-316">Créer la table de hello dans SQL Server avec hello même nombre de colonnes comme vous le souhaitez toocontain de fichier CSV d’objets Blob hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-316">Create hello table in SQL Server with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="6ea38-317">Nouvelles lignes sont ajoutées à la table de toohello toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="6ea38-317">New rows are added toohello table every hour.</span></span>

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="6ea38-318">**Pipeline avec activité de copie**</span><span class="sxs-lookup"><span data-stu-id="6ea38-318">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="6ea38-319">pipeline de Hello contient une activité de copie qui est configuré toouse ces jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="6ea38-319">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="6ea38-320">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**BlobSource** et **récepteur** type est défini trop**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="6ea38-320">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": " SqlServerOutput "
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="6ea38-321">Résolution des problèmes de connexion</span><span class="sxs-lookup"><span data-stu-id="6ea38-321">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="6ea38-322">Configurez vos connexions à distance de SQL Server tooaccept.</span><span class="sxs-lookup"><span data-stu-id="6ea38-322">Configure your SQL Server tooaccept remote connections.</span></span> <span data-ttu-id="6ea38-323">Démarrez **SQL Server Management Studio**, cliquez avec le bouton droit de la souris sur **Serveur**, puis cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="6ea38-323">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="6ea38-324">Sélectionnez **connexions** à partir de la liste de hello et vérification **server de toohello autoriser les connexions à distance**.</span><span class="sxs-lookup"><span data-stu-id="6ea38-324">Select **Connections** from hello list and check **Allow remote connections toohello server**.</span></span>

    ![Activation des connexions à distance](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="6ea38-326">Consultez [configurer hello remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) pour obtenir des instructions détaillées.</span><span class="sxs-lookup"><span data-stu-id="6ea38-326">See [Configure hello remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="6ea38-327">Lancez le **Gestionnaire de configuration SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="6ea38-327">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="6ea38-328">Développez **Configuration du réseau SQL Server** pour hello instance vous souhaitez, puis sélectionnez **protocoles pour MSSQLSERVER**.</span><span class="sxs-lookup"><span data-stu-id="6ea38-328">Expand **SQL Server Network Configuration** for hello instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="6ea38-329">Vous devez voir des protocoles dans le volet droit hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-329">You should see protocols in hello right-pane.</span></span> <span data-ttu-id="6ea38-330">Activez TCP/IP en cliquant avec le bouton droit sur **TCP/IP** et en cliquant sur **Activer**.</span><span class="sxs-lookup"><span data-stu-id="6ea38-330">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![Activation de TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="6ea38-332">Consultez la page [Activer ou désactiver un protocole réseau de serveur](https://msdn.microsoft.com/library/ms191294.aspx) pour obtenir des détails et découvrir d’autres façons d’activer le protocole TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="6ea38-332">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="6ea38-333">Dans la même fenêtre de hello, double-cliquez sur **TCP/IP** toolaunch **propriétés TCP/IP** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="6ea38-333">In hello same window, double-click **TCP/IP** toolaunch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="6ea38-334">Commutateur toohello **des adresses IP** onglet. Faites défiler vers le bas toosee **IPAll** section.</span><span class="sxs-lookup"><span data-stu-id="6ea38-334">Switch toohello **IP Addresses** tab. Scroll down toosee **IPAll** section.</span></span> <span data-ttu-id="6ea38-335">Notez les hello ** le Port TCP ** (valeur par défaut est **1433**).</span><span class="sxs-lookup"><span data-stu-id="6ea38-335">Note down hello **TCP Port **(default is **1433**).</span></span>
5. <span data-ttu-id="6ea38-336">Créer un **règle pour le pare-feu Windows de hello** hello machine tooallow du trafic entrant via ce port.</span><span class="sxs-lookup"><span data-stu-id="6ea38-336">Create a **rule for hello Windows Firewall** on hello machine tooallow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="6ea38-337">**Vérifiez la connexion**: tooconnect toohello SQL Server à l’aide du nom qualifié complet, utilisez SQL Server Management Studio à partir d’un autre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="6ea38-337">**Verify connection**: tooconnect toohello SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="6ea38-338">Par exemple : « <machine><domain>.corp<company>.com, 1433 ».</span><span class="sxs-lookup"><span data-stu-id="6ea38-338">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="6ea38-339">Consultez [déplacement des données entre des sources locales et cloud hello avec la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="6ea38-339">See [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="6ea38-340">Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.</span><span class="sxs-lookup"><span data-stu-id="6ea38-340">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-hello-target-database"></a><span data-ttu-id="6ea38-341">Colonnes d’identité dans la base de données cible hello</span><span class="sxs-lookup"><span data-stu-id="6ea38-341">Identity columns in hello target database</span></span>
<span data-ttu-id="6ea38-342">Cette section fournit un exemple qui copie les données d’une table source avec aucune table de destination tooa colonne identité avec une colonne d’identité.</span><span class="sxs-lookup"><span data-stu-id="6ea38-342">This section provides an example that copies data from a source table with no identity column tooa destination table with an identity column.</span></span>

<span data-ttu-id="6ea38-343">**Table source :**</span><span class="sxs-lookup"><span data-stu-id="6ea38-343">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="6ea38-344">**Table de destination :**</span><span class="sxs-lookup"><span data-stu-id="6ea38-344">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="6ea38-345">Notez que la table cible hello possède une colonne d’identité.</span><span class="sxs-lookup"><span data-stu-id="6ea38-345">Notice that hello target table has an identity column.</span></span>

<span data-ttu-id="6ea38-346">**Définition du jeu de données JSON source**</span><span class="sxs-lookup"><span data-stu-id="6ea38-346">**Source dataset JSON definition**</span></span>

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="6ea38-347">**Définition de jeu de données JSON de destination**</span><span class="sxs-lookup"><span data-stu-id="6ea38-347">**Destination dataset JSON definition**</span></span>

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

<span data-ttu-id="6ea38-348">Notez que vos tables source et cible ont des schémas différents (la cible possède une colonne supplémentaire avec identité).</span><span class="sxs-lookup"><span data-stu-id="6ea38-348">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="6ea38-349">Dans ce scénario, vous devez toospecify **structure** propriété dans la définition du dataset cible hello, qui n’inclut pas colonne d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="6ea38-349">In this scenario, you need toospecify **structure** property in hello target dataset definition, which doesn’t include hello identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="6ea38-350">Appel d’une procédure stockée pour un récepteur SQL</span><span class="sxs-lookup"><span data-stu-id="6ea38-350">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="6ea38-351">L’article [Appeler une procédure stockée pour un récepteur SQL dans l’activité de copie](data-factory-invoke-stored-procedure-from-copy-activity.md) illustre l’appel d’une procédure stockée à partir d’un récepteur SQL dans l’activité de copie d’un pipeline.</span><span class="sxs-lookup"><span data-stu-id="6ea38-351">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="6ea38-352">Mappage de type pour SQL Server</span><span class="sxs-lookup"><span data-stu-id="6ea38-352">Type mapping for SQL server</span></span>
<span data-ttu-id="6ea38-353">Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, hello activité de copie effectue les conversions de type automatique à partir de types de sources de toosink types avec hello approche de l’étape 2 :</span><span class="sxs-lookup"><span data-stu-id="6ea38-353">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="6ea38-354">Convertir à partir de la source native types too.NET type</span><span class="sxs-lookup"><span data-stu-id="6ea38-354">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="6ea38-355">Conversion de type de récepteur de toonative de type .NET</span><span class="sxs-lookup"><span data-stu-id="6ea38-355">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="6ea38-356">Lorsque le déplacement des données trop & à partir de SQL server, hello mappages suivants sont utilisés à partir du type too.NET de type SQL et vice versa.</span><span class="sxs-lookup"><span data-stu-id="6ea38-356">When moving data too& from SQL server, hello following mappings are used from SQL type too.NET type and vice versa.</span></span>

<span data-ttu-id="6ea38-357">mappage de Hello est identique à celui hello mappage des types de données SQL Server pour ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="6ea38-357">hello mapping is same as hello SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="6ea38-358">Type de moteur de base de données SQL Server</span><span class="sxs-lookup"><span data-stu-id="6ea38-358">SQL Server Database Engine type</span></span> | <span data-ttu-id="6ea38-359">Type de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="6ea38-359">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="6ea38-360">bigint</span><span class="sxs-lookup"><span data-stu-id="6ea38-360">bigint</span></span> |<span data-ttu-id="6ea38-361">Int64</span><span class="sxs-lookup"><span data-stu-id="6ea38-361">Int64</span></span> |
| <span data-ttu-id="6ea38-362">binaire</span><span class="sxs-lookup"><span data-stu-id="6ea38-362">binary</span></span> |<span data-ttu-id="6ea38-363">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6ea38-363">Byte[]</span></span> |
| <span data-ttu-id="6ea38-364">bit</span><span class="sxs-lookup"><span data-stu-id="6ea38-364">bit</span></span> |<span data-ttu-id="6ea38-365">Boolean</span><span class="sxs-lookup"><span data-stu-id="6ea38-365">Boolean</span></span> |
| <span data-ttu-id="6ea38-366">char</span><span class="sxs-lookup"><span data-stu-id="6ea38-366">char</span></span> |<span data-ttu-id="6ea38-367">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="6ea38-367">String, Char[]</span></span> |
| <span data-ttu-id="6ea38-368">date</span><span class="sxs-lookup"><span data-stu-id="6ea38-368">date</span></span> |<span data-ttu-id="6ea38-369">DateTime</span><span class="sxs-lookup"><span data-stu-id="6ea38-369">DateTime</span></span> |
| <span data-ttu-id="6ea38-370">DateTime</span><span class="sxs-lookup"><span data-stu-id="6ea38-370">Datetime</span></span> |<span data-ttu-id="6ea38-371">DateTime</span><span class="sxs-lookup"><span data-stu-id="6ea38-371">DateTime</span></span> |
| <span data-ttu-id="6ea38-372">datetime2</span><span class="sxs-lookup"><span data-stu-id="6ea38-372">datetime2</span></span> |<span data-ttu-id="6ea38-373">DateTime</span><span class="sxs-lookup"><span data-stu-id="6ea38-373">DateTime</span></span> |
| <span data-ttu-id="6ea38-374">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="6ea38-374">Datetimeoffset</span></span> |<span data-ttu-id="6ea38-375">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="6ea38-375">DateTimeOffset</span></span> |
| <span data-ttu-id="6ea38-376">Décimal</span><span class="sxs-lookup"><span data-stu-id="6ea38-376">Decimal</span></span> |<span data-ttu-id="6ea38-377">Décimal</span><span class="sxs-lookup"><span data-stu-id="6ea38-377">Decimal</span></span> |
| <span data-ttu-id="6ea38-378">Attribut FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="6ea38-378">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="6ea38-379">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6ea38-379">Byte[]</span></span> |
| <span data-ttu-id="6ea38-380">Float</span><span class="sxs-lookup"><span data-stu-id="6ea38-380">Float</span></span> |<span data-ttu-id="6ea38-381">Double</span><span class="sxs-lookup"><span data-stu-id="6ea38-381">Double</span></span> |
| <span data-ttu-id="6ea38-382">image</span><span class="sxs-lookup"><span data-stu-id="6ea38-382">image</span></span> |<span data-ttu-id="6ea38-383">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6ea38-383">Byte[]</span></span> |
| <span data-ttu-id="6ea38-384">int</span><span class="sxs-lookup"><span data-stu-id="6ea38-384">int</span></span> |<span data-ttu-id="6ea38-385">Int32</span><span class="sxs-lookup"><span data-stu-id="6ea38-385">Int32</span></span> |
| <span data-ttu-id="6ea38-386">money</span><span class="sxs-lookup"><span data-stu-id="6ea38-386">money</span></span> |<span data-ttu-id="6ea38-387">Décimal</span><span class="sxs-lookup"><span data-stu-id="6ea38-387">Decimal</span></span> |
| <span data-ttu-id="6ea38-388">nchar</span><span class="sxs-lookup"><span data-stu-id="6ea38-388">nchar</span></span> |<span data-ttu-id="6ea38-389">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="6ea38-389">String, Char[]</span></span> |
| <span data-ttu-id="6ea38-390">ntext</span><span class="sxs-lookup"><span data-stu-id="6ea38-390">ntext</span></span> |<span data-ttu-id="6ea38-391">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="6ea38-391">String, Char[]</span></span> |
| <span data-ttu-id="6ea38-392">numérique</span><span class="sxs-lookup"><span data-stu-id="6ea38-392">numeric</span></span> |<span data-ttu-id="6ea38-393">Décimal</span><span class="sxs-lookup"><span data-stu-id="6ea38-393">Decimal</span></span> |
| <span data-ttu-id="6ea38-394">nvarchar</span><span class="sxs-lookup"><span data-stu-id="6ea38-394">nvarchar</span></span> |<span data-ttu-id="6ea38-395">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="6ea38-395">String, Char[]</span></span> |
| <span data-ttu-id="6ea38-396">real</span><span class="sxs-lookup"><span data-stu-id="6ea38-396">real</span></span> |<span data-ttu-id="6ea38-397">Single</span><span class="sxs-lookup"><span data-stu-id="6ea38-397">Single</span></span> |
| <span data-ttu-id="6ea38-398">rowversion</span><span class="sxs-lookup"><span data-stu-id="6ea38-398">rowversion</span></span> |<span data-ttu-id="6ea38-399">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6ea38-399">Byte[]</span></span> |
| <span data-ttu-id="6ea38-400">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="6ea38-400">smalldatetime</span></span> |<span data-ttu-id="6ea38-401">DateTime</span><span class="sxs-lookup"><span data-stu-id="6ea38-401">DateTime</span></span> |
| <span data-ttu-id="6ea38-402">smallint</span><span class="sxs-lookup"><span data-stu-id="6ea38-402">smallint</span></span> |<span data-ttu-id="6ea38-403">Int16</span><span class="sxs-lookup"><span data-stu-id="6ea38-403">Int16</span></span> |
| <span data-ttu-id="6ea38-404">smallmoney</span><span class="sxs-lookup"><span data-stu-id="6ea38-404">smallmoney</span></span> |<span data-ttu-id="6ea38-405">Décimal</span><span class="sxs-lookup"><span data-stu-id="6ea38-405">Decimal</span></span> |
| <span data-ttu-id="6ea38-406">sql_variant</span><span class="sxs-lookup"><span data-stu-id="6ea38-406">sql_variant</span></span> |<span data-ttu-id="6ea38-407">Objet *</span><span class="sxs-lookup"><span data-stu-id="6ea38-407">Object *</span></span> |
| <span data-ttu-id="6ea38-408">texte</span><span class="sxs-lookup"><span data-stu-id="6ea38-408">text</span></span> |<span data-ttu-id="6ea38-409">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="6ea38-409">String, Char[]</span></span> |
| <span data-ttu-id="6ea38-410">time</span><span class="sxs-lookup"><span data-stu-id="6ea38-410">time</span></span> |<span data-ttu-id="6ea38-411">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="6ea38-411">TimeSpan</span></span> |
| <span data-ttu-id="6ea38-412">timestamp</span><span class="sxs-lookup"><span data-stu-id="6ea38-412">timestamp</span></span> |<span data-ttu-id="6ea38-413">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6ea38-413">Byte[]</span></span> |
| <span data-ttu-id="6ea38-414">tinyint</span><span class="sxs-lookup"><span data-stu-id="6ea38-414">tinyint</span></span> |<span data-ttu-id="6ea38-415">Byte</span><span class="sxs-lookup"><span data-stu-id="6ea38-415">Byte</span></span> |
| <span data-ttu-id="6ea38-416">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="6ea38-416">uniqueidentifier</span></span> |<span data-ttu-id="6ea38-417">Guid</span><span class="sxs-lookup"><span data-stu-id="6ea38-417">Guid</span></span> |
| <span data-ttu-id="6ea38-418">varbinary</span><span class="sxs-lookup"><span data-stu-id="6ea38-418">varbinary</span></span> |<span data-ttu-id="6ea38-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6ea38-419">Byte[]</span></span> |
| <span data-ttu-id="6ea38-420">varchar</span><span class="sxs-lookup"><span data-stu-id="6ea38-420">varchar</span></span> |<span data-ttu-id="6ea38-421">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="6ea38-421">String, Char[]</span></span> |
| <span data-ttu-id="6ea38-422">xml</span><span class="sxs-lookup"><span data-stu-id="6ea38-422">xml</span></span> |<span data-ttu-id="6ea38-423">xml</span><span class="sxs-lookup"><span data-stu-id="6ea38-423">Xml</span></span> |

## <a name="mapping-source-toosink-columns"></a><span data-ttu-id="6ea38-424">Mappage des colonnes toosink source</span><span class="sxs-lookup"><span data-stu-id="6ea38-424">Mapping source toosink columns</span></span>
<span data-ttu-id="6ea38-425">colonnes de toomap de toocolumns du jeu de données source à partir du jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="6ea38-425">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="6ea38-426">Copie renouvelée</span><span class="sxs-lookup"><span data-stu-id="6ea38-426">Repeatable copy</span></span>
<span data-ttu-id="6ea38-427">Lors de la copie des données tooSQL serveur de base de données, l’activité de copie hello ajoute la table de données toohello récepteur par défaut.</span><span class="sxs-lookup"><span data-stu-id="6ea38-427">When copying data tooSQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="6ea38-428">tooperform UPSERT au lieu de cela, consultez [écriture Repeatable tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) l’article.</span><span class="sxs-lookup"><span data-stu-id="6ea38-428">tooperform an UPSERT instead,  See [Repeatable write tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="6ea38-429">Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="6ea38-429">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="6ea38-430">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="6ea38-430">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="6ea38-431">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="6ea38-431">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="6ea38-432">Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée.</span><span class="sxs-lookup"><span data-stu-id="6ea38-432">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="6ea38-433">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="6ea38-433">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="6ea38-434">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="6ea38-434">Performance and Tuning</span></span>
<span data-ttu-id="6ea38-435">Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="6ea38-435">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
