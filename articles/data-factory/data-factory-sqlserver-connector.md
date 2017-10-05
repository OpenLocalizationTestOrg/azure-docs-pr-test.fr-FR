---
title: "Déplacer des données vers et à partir de SQL Server | Microsoft Docs"
description: "Apprendre à déplacer des données vers/depuis une base de données SQL Server locale ou une machine virtuelle Azure à l’aide d’Azure Data Factory."
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
ms.openlocfilehash: 9cd2077d897631457925cda5ef5e6df3c0c33177
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="b08ed-103">Déplacement des données vers et depuis SQL Server local ou sur IaaS (Machine virtuelle Azure) à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="b08ed-103">Move data to and from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="b08ed-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour déplacer des données vers/à partir d’une base de données SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="b08ed-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="b08ed-105">Il s’appuie sur l’article [Activités de déplacement des données](data-factory-data-movement-activities.md), qui présente une vue d’ensemble du déplacement de données avec l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="b08ed-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="b08ed-106">Scénarios pris en charge</span><span class="sxs-lookup"><span data-stu-id="b08ed-106">Supported scenarios</span></span>
<span data-ttu-id="b08ed-107">Vous pouvez copier les données **d’une base de données SQL Server** dans les magasins de données suivants :</span><span class="sxs-lookup"><span data-stu-id="b08ed-107">You can copy data **from a SQL Server database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="b08ed-108">Vous pouvez copier les données des magasins de données suivants **dans une base de données SQL Server** :</span><span class="sxs-lookup"><span data-stu-id="b08ed-108">You can copy data from the following data stores **to a SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="b08ed-109">Versions de SQL Server prises en charge</span><span class="sxs-lookup"><span data-stu-id="b08ed-109">Supported SQL Server versions</span></span>
<span data-ttu-id="b08ed-110">Ce connecteur SQL Server prend en charge la copie de données à partir de/vers les versions suivantes d’une instance hébergée en local ou dans Azure IaaS à l’aide de l’authentification SQL et de l’authentification Windows : SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span><span class="sxs-lookup"><span data-stu-id="b08ed-110">This SQL Server connector support copying data from/to the following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="b08ed-111">Activation de la connectivité</span><span class="sxs-lookup"><span data-stu-id="b08ed-111">Enabling connectivity</span></span>
<span data-ttu-id="b08ed-112">Les concepts et les étapes nécessaires pour la connexion avec SQL Server sont hébergés localement ou dans les machines virtuelles Iaas Azure (Infrastructure-as-a-Service) sont les mêmes.</span><span class="sxs-lookup"><span data-stu-id="b08ed-112">The concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are the same.</span></span> <span data-ttu-id="b08ed-113">Dans les deux cas, vous devez utiliser la passerelle de gestion des données de connectivité.</span><span class="sxs-lookup"><span data-stu-id="b08ed-113">In both cases, you need to use Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="b08ed-114">Consultez l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) pour en savoir plus sur la passerelle de gestion des données et obtenir des instructions détaillées sur la configuration de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="b08ed-114">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="b08ed-115">La configuration d’une instance de passerelle est pré requise pour la connexion avec SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b08ed-115">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="b08ed-116">Vous pouvez installer la passerelle sur la même machine locale ou l’instance de machine virtuelle cloud en tant que serveur SQL Server pour de meilleures performances. Nous recommandons de les installer sur des machines séparées ou les machines virtuelles Cloud.</span><span class="sxs-lookup"><span data-stu-id="b08ed-116">While you can install gateway on the same on-premises machine or cloud VM instance as the SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="b08ed-117">Placer la passerelle et SQL Server sur des ordinateurs distincts réduit les conflits de ressources.</span><span class="sxs-lookup"><span data-stu-id="b08ed-117">Having the gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="b08ed-118">Prise en main</span><span class="sxs-lookup"><span data-stu-id="b08ed-118">Getting started</span></span>
<span data-ttu-id="b08ed-119">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers/depuis une base de données SQL Server à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="b08ed-119">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="b08ed-120">Le moyen le plus simple de créer un pipeline consiste à utiliser **l’Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="b08ed-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="b08ed-121">Consultez la page [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant Copier des données.</span><span class="sxs-lookup"><span data-stu-id="b08ed-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="b08ed-122">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="b08ed-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="b08ed-123">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="b08ed-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="b08ed-124">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="b08ed-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="b08ed-125">Création d'une **fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="b08ed-125">Create a **data factory**.</span></span> <span data-ttu-id="b08ed-126">Une fabrique de données peut contenir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="b08ed-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="b08ed-127">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="b08ed-127">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="b08ed-128">Par exemple, si vous copiez des données d’une base de données SQL Server vers un stockage Blob Azure, vous créez deux services liés pour lier votre base de données SQL Server et votre compte de stockage Azure à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="b08ed-128">For example, if you are copying data from a SQL Server database to an Azure blob storage, you create two linked services to link your SQL Server database and Azure storage account to your data factory.</span></span> <span data-ttu-id="b08ed-129">Pour plus d’informations sur les propriétés de service lié qui sont spécifiques à la base de données SQL Server, consultez la section [Propriétés du service lié](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b08ed-129">For linked service properties that are specific to SQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="b08ed-130">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="b08ed-130">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="b08ed-131">Dans l’exemple mentionné à la dernière étape, vous créez un jeu de données pour spécifier la table SQL de votre base de données SQL Server qui doit contenir les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="b08ed-131">In the example mentioned in the last step, you create a dataset to specify the SQL table in your SQL Server database that contains the input data.</span></span> <span data-ttu-id="b08ed-132">Ensuite, vous créez un autre jeu de données pour spécifier le conteneur d’objets blob et le dossier qui contient les données copiées à partir de la base de données SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b08ed-132">And, you create another dataset to specify the blob container and the folder that holds the data copied from the SQL Server database.</span></span> <span data-ttu-id="b08ed-133">Pour plus d’informations sur les propriétés de jeu de données qui sont spécifiques à la base de données SQL Server, consultez la section [Propriétés du jeu de données](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b08ed-133">For dataset properties that are specific to SQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="b08ed-134">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="b08ed-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="b08ed-135">Dans l’exemple mentionné plus haut, vous utilisez SqlSource comme source et BlobSink comme récepteur pour l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="b08ed-135">In the example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for the copy activity.</span></span> <span data-ttu-id="b08ed-136">De la même façon, si vous copiez des données du stockage Blob Azure vers une base de données SQL Server, vous utilisez BlobSource et SqlSink dans l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="b08ed-136">Similarly, if you are copying from Azure Blob Storage to SQL Server Database, you use BlobSource and SqlSink in the copy activity.</span></span> <span data-ttu-id="b08ed-137">Pour plus d’informations sur les propriétés de l’activité de copie qui sont spécifiques à la base de données SQL Server, consultez la section [Propriétés de l’activité de copie](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="b08ed-137">For copy activity properties that are specific to SQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="b08ed-138">Pour plus d’informations sur l’utilisation d’un magasin de données en tant que source ou que récepteur, cliquez sur le lien correspondant à votre magasin de données dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="b08ed-138">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span> 

<span data-ttu-id="b08ed-139">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="b08ed-139">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="b08ed-140">Lorsque vous utilisez des outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory au format JSON.</span><span class="sxs-lookup"><span data-stu-id="b08ed-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="b08ed-141">Pour obtenir des exemples comportant des définitions JSON pour les entités Data Factory utilisées pour copier les données vers ou à partir d’une base de données SQL Server locale, consultez la section [Exemples JSON](#json-examples-for-copying-data-from-and-to-sql-server) de cet article.</span><span class="sxs-lookup"><span data-stu-id="b08ed-141">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="b08ed-142">Les sections suivantes fournissent des informations sur les propriétés JSON utilisées pour définir les entités Data Factory spécifiques à SQL Server :</span><span class="sxs-lookup"><span data-stu-id="b08ed-142">The following sections provide details about JSON properties that are used to define Data Factory entities specific to SQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="b08ed-143">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="b08ed-143">Linked service properties</span></span>
<span data-ttu-id="b08ed-144">Vous créez un service lié de type **OnPremisesSqlServer** pour lier une base de données SQL Server locale à une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="b08ed-144">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="b08ed-145">Le tableau suivant fournit la description des éléments JSON spécifiques au service lié SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="b08ed-145">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="b08ed-146">Le tableau suivant fournit la description des éléments JSON spécifiques au service lié SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b08ed-146">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="b08ed-147">Propriété</span><span class="sxs-lookup"><span data-stu-id="b08ed-147">Property</span></span> | <span data-ttu-id="b08ed-148">Description</span><span class="sxs-lookup"><span data-stu-id="b08ed-148">Description</span></span> | <span data-ttu-id="b08ed-149">Requis</span><span class="sxs-lookup"><span data-stu-id="b08ed-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b08ed-150">type</span><span class="sxs-lookup"><span data-stu-id="b08ed-150">type</span></span> |<span data-ttu-id="b08ed-151">Le type de propriété doit être défini sur **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="b08ed-151">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="b08ed-152">Oui</span><span class="sxs-lookup"><span data-stu-id="b08ed-152">Yes</span></span> |
| <span data-ttu-id="b08ed-153">connectionString</span><span class="sxs-lookup"><span data-stu-id="b08ed-153">connectionString</span></span> |<span data-ttu-id="b08ed-154">Spécifiez les informations connectionString nécessaires pour connecter la base de données SQL Server locale à l’aide de l’authentification SQL ou de l’authentification Windows.</span><span class="sxs-lookup"><span data-stu-id="b08ed-154">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="b08ed-155">Oui</span><span class="sxs-lookup"><span data-stu-id="b08ed-155">Yes</span></span> |
| <span data-ttu-id="b08ed-156">gatewayName</span><span class="sxs-lookup"><span data-stu-id="b08ed-156">gatewayName</span></span> |<span data-ttu-id="b08ed-157">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter à la base de données SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="b08ed-157">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="b08ed-158">Oui</span><span class="sxs-lookup"><span data-stu-id="b08ed-158">Yes</span></span> |
| <span data-ttu-id="b08ed-159">username</span><span class="sxs-lookup"><span data-stu-id="b08ed-159">username</span></span> |<span data-ttu-id="b08ed-160">Spécifiez le nom d’utilisateur si vous utilisez l’authentification Windows.</span><span class="sxs-lookup"><span data-stu-id="b08ed-160">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="b08ed-161">Exemple : **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="b08ed-161">Example: **domainname\\username**.</span></span> |<span data-ttu-id="b08ed-162">Non</span><span class="sxs-lookup"><span data-stu-id="b08ed-162">No</span></span> |
| <span data-ttu-id="b08ed-163">password</span><span class="sxs-lookup"><span data-stu-id="b08ed-163">password</span></span> |<span data-ttu-id="b08ed-164">Spécifiez le mot de passe du compte d’utilisateur que vous avez spécifié pour le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b08ed-164">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="b08ed-165">Non</span><span class="sxs-lookup"><span data-stu-id="b08ed-165">No</span></span> |

<span data-ttu-id="b08ed-166">Vous pouvez chiffrer les informations d’identification à l’aide de l’applet de commande **New-AzureRmDataFactoryEncryptValue** et les utiliser dans la chaîne de connexion comme indiqué dans l’exemple suivant (propriété **EncryptedCredential**) :</span><span class="sxs-lookup"><span data-stu-id="b08ed-166">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="b08ed-167">Exemples</span><span class="sxs-lookup"><span data-stu-id="b08ed-167">Samples</span></span>
<span data-ttu-id="b08ed-168">**JSON pour utilisation de l’authentification SQL**</span><span class="sxs-lookup"><span data-stu-id="b08ed-168">**JSON for using SQL Authentication**</span></span>

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
<span data-ttu-id="b08ed-169">**JSON pour utilisation de l’authentification Windows**</span><span class="sxs-lookup"><span data-stu-id="b08ed-169">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="b08ed-170">La passerelle de gestion des données utilisera l’identité du compte utilisateur spécifié pour se connecter à la base de données SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="b08ed-170">Data Management Gateway will impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> 

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

## <a name="dataset-properties"></a><span data-ttu-id="b08ed-171">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="b08ed-171">Dataset properties</span></span>
<span data-ttu-id="b08ed-172">Dans les exemples, vous avez utilisé un jeu de données de type **SqlServerTable** pour représenter une table dans une base de données SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b08ed-172">In the samples, you have used a dataset of type **SqlServerTable** to represent a table in a SQL Server database.</span></span>  

<span data-ttu-id="b08ed-173">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="b08ed-173">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="b08ed-174">Les sections comme la structure, la disponibilité et la stratégie d’un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Server, objet Blob Azure, table Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="b08ed-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="b08ed-175">La section typeProperties est différente pour chaque type de jeu de données et fournit des informations sur l'emplacement des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="b08ed-175">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="b08ed-176">La section **typeProperties** pour le jeu de données de type **SqlServerTable** a les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="b08ed-176">The **typeProperties** section for the dataset of type **SqlServerTable** has the following properties:</span></span>

| <span data-ttu-id="b08ed-177">Propriété</span><span class="sxs-lookup"><span data-stu-id="b08ed-177">Property</span></span> | <span data-ttu-id="b08ed-178">Description</span><span class="sxs-lookup"><span data-stu-id="b08ed-178">Description</span></span> | <span data-ttu-id="b08ed-179">Requis</span><span class="sxs-lookup"><span data-stu-id="b08ed-179">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b08ed-180">TableName</span><span class="sxs-lookup"><span data-stu-id="b08ed-180">tableName</span></span> |<span data-ttu-id="b08ed-181">Nom de la table ou de la vue dans l’instance de base de données SQL Server à laquelle le service lié fait référence.</span><span class="sxs-lookup"><span data-stu-id="b08ed-181">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="b08ed-182">Oui</span><span class="sxs-lookup"><span data-stu-id="b08ed-182">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="b08ed-183">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="b08ed-183">Copy activity properties</span></span>
<span data-ttu-id="b08ed-184">Si vous déplacez des données à partir d’une base de données SQL Server, vous définissez le type de source dans l’activité de copie sur **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="b08ed-184">If you are moving data from a SQL Server database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="b08ed-185">De même, si vous déplacez des données vers une base de données SQL Server, vous définissez le type de récepteur dans l’activité de copie sur **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="b08ed-185">Similarly, if you are moving data to a SQL Server database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="b08ed-186">Cette section fournit une liste de propriétés prises en charge par SqlSource et SqlSink.</span><span class="sxs-lookup"><span data-stu-id="b08ed-186">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="b08ed-187">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="b08ed-187">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="b08ed-188">Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités.</span><span class="sxs-lookup"><span data-stu-id="b08ed-188">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="b08ed-189">L'activité de copie accepte uniquement une entrée et produit une seule sortie.</span><span class="sxs-lookup"><span data-stu-id="b08ed-189">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="b08ed-190">En revanche, les propriétés disponibles dans la section typeProperties de l’activité varient pour chaque type d'activité.</span><span class="sxs-lookup"><span data-stu-id="b08ed-190">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="b08ed-191">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="b08ed-191">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="b08ed-192">SqlSource</span><span class="sxs-lookup"><span data-stu-id="b08ed-192">SqlSource</span></span>
<span data-ttu-id="b08ed-193">Lorsqu’une source dans une activité de copie est de type **SqlSource**, les propriétés suivantes sont disponibles dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="b08ed-193">When source in a copy activity is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="b08ed-194">Propriété</span><span class="sxs-lookup"><span data-stu-id="b08ed-194">Property</span></span> | <span data-ttu-id="b08ed-195">Description</span><span class="sxs-lookup"><span data-stu-id="b08ed-195">Description</span></span> | <span data-ttu-id="b08ed-196">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="b08ed-196">Allowed values</span></span> | <span data-ttu-id="b08ed-197">Requis</span><span class="sxs-lookup"><span data-stu-id="b08ed-197">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b08ed-198">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="b08ed-198">sqlReaderQuery</span></span> |<span data-ttu-id="b08ed-199">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="b08ed-199">Use the custom query to read data.</span></span> |<span data-ttu-id="b08ed-200">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="b08ed-200">SQL query string.</span></span> <span data-ttu-id="b08ed-201">Par exemple : select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="b08ed-201">For example: select * from MyTable.</span></span> <span data-ttu-id="b08ed-202">Peut faire référence à plusieurs tables de la base de données référencée par le jeu de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="b08ed-202">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="b08ed-203">S’il n’est pas spécifié, l’instruction SQL est exécutée : select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="b08ed-203">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="b08ed-204">Non</span><span class="sxs-lookup"><span data-stu-id="b08ed-204">No</span></span> |
| <span data-ttu-id="b08ed-205">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="b08ed-205">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="b08ed-206">Nom de la procédure stockée qui lit les données de la table source.</span><span class="sxs-lookup"><span data-stu-id="b08ed-206">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="b08ed-207">Nom de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="b08ed-207">Name of the stored procedure.</span></span> <span data-ttu-id="b08ed-208">La dernière instruction SQL doit être une instruction SELECT dans la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="b08ed-208">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="b08ed-209">Non</span><span class="sxs-lookup"><span data-stu-id="b08ed-209">No</span></span> |
| <span data-ttu-id="b08ed-210">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="b08ed-210">storedProcedureParameters</span></span> |<span data-ttu-id="b08ed-211">Paramètres de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="b08ed-211">Parameters for the stored procedure.</span></span> |<span data-ttu-id="b08ed-212">Paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="b08ed-212">Name/value pairs.</span></span> <span data-ttu-id="b08ed-213">Les noms et la casse des paramètres doivent correspondre aux noms et à la casse des paramètres de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="b08ed-213">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="b08ed-214">Non</span><span class="sxs-lookup"><span data-stu-id="b08ed-214">No</span></span> |

<span data-ttu-id="b08ed-215">Si **sqlReaderQuery** est spécifié pour la SqlSource, l'activité de copie exécute cette requête dans la source Azure SQL Database pour obtenir les données.</span><span class="sxs-lookup"><span data-stu-id="b08ed-215">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="b08ed-216">Vous pouvez également spécifier une procédure stockée en indiquant **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si la procédure stockée accepte des paramètres).</span><span class="sxs-lookup"><span data-stu-id="b08ed-216">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="b08ed-217">Si vous ne spécifiez pas sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes définies dans la section structure du code JSON du jeu de données sont utilisées pour créer une requête à exécuter sur Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="b08ed-217">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="b08ed-218">Si la définition du jeu de données ne possède pas de structure, toutes les colonnes de la table sont sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="b08ed-218">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="b08ed-219">Quand vous utilisez **sqlReaderStoredProcedureName**, vous devez toujours spécifier une valeur pour la propriété **tableName** du code JSON du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="b08ed-219">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="b08ed-220">Cependant, il n’existe aucune validation effectuée pour cette table.</span><span class="sxs-lookup"><span data-stu-id="b08ed-220">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="b08ed-221">SqlSink</span><span class="sxs-lookup"><span data-stu-id="b08ed-221">SqlSink</span></span>
<span data-ttu-id="b08ed-222">**SqlSink** prend en charge les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="b08ed-222">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="b08ed-223">Propriété</span><span class="sxs-lookup"><span data-stu-id="b08ed-223">Property</span></span> | <span data-ttu-id="b08ed-224">Description</span><span class="sxs-lookup"><span data-stu-id="b08ed-224">Description</span></span> | <span data-ttu-id="b08ed-225">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="b08ed-225">Allowed values</span></span> | <span data-ttu-id="b08ed-226">Requis</span><span class="sxs-lookup"><span data-stu-id="b08ed-226">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b08ed-227">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="b08ed-227">writeBatchTimeout</span></span> |<span data-ttu-id="b08ed-228">Temps d’attente pour que l’opération d’insertion de lot soit terminée avant d’expirer.</span><span class="sxs-lookup"><span data-stu-id="b08ed-228">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="b08ed-229">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="b08ed-229">timespan</span></span><br/><br/> <span data-ttu-id="b08ed-230">Exemple : « 00:30:00 » (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="b08ed-230">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="b08ed-231">Non</span><span class="sxs-lookup"><span data-stu-id="b08ed-231">No</span></span> |
| <span data-ttu-id="b08ed-232">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="b08ed-232">writeBatchSize</span></span> |<span data-ttu-id="b08ed-233">Insère des données dans la table SQL lorsque la taille du tampon atteint writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="b08ed-233">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="b08ed-234">Nombre entier (nombre de lignes)</span><span class="sxs-lookup"><span data-stu-id="b08ed-234">Integer (number of rows)</span></span> |<span data-ttu-id="b08ed-235">Non (valeur par défaut : 10000)</span><span class="sxs-lookup"><span data-stu-id="b08ed-235">No (default: 10000)</span></span> |
| <span data-ttu-id="b08ed-236">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="b08ed-236">sqlWriterCleanupScript</span></span> |<span data-ttu-id="b08ed-237">Spécifiez une requête pour exécuter l'activité de copie de sorte que les données d'un segment spécifique sont nettoyées.</span><span class="sxs-lookup"><span data-stu-id="b08ed-237">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="b08ed-238">Pour en savoir plus, voir la section [Copie renouvelée](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="b08ed-238">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="b08ed-239">Une instruction de requête.</span><span class="sxs-lookup"><span data-stu-id="b08ed-239">A query statement.</span></span> |<span data-ttu-id="b08ed-240">Non</span><span class="sxs-lookup"><span data-stu-id="b08ed-240">No</span></span> |
| <span data-ttu-id="b08ed-241">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="b08ed-241">sliceIdentifierColumnName</span></span> |<span data-ttu-id="b08ed-242">Spécifiez le nom de la colonne que l’activité de copie doit remplir avec l’identificateur de segment généré automatiquement, et qui est utilisée pour nettoyer les données d’un segment spécifique lors de la réexécution.</span><span class="sxs-lookup"><span data-stu-id="b08ed-242">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="b08ed-243">Pour en savoir plus, voir la section [Copie renouvelée](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="b08ed-243">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="b08ed-244">Nom d’une colonne avec le type de données binary(32).</span><span class="sxs-lookup"><span data-stu-id="b08ed-244">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="b08ed-245">Non</span><span class="sxs-lookup"><span data-stu-id="b08ed-245">No</span></span> |
| <span data-ttu-id="b08ed-246">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="b08ed-246">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="b08ed-247">Nom de la procédure stockée qui met à jour/insère les données dans la table cible.</span><span class="sxs-lookup"><span data-stu-id="b08ed-247">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="b08ed-248">Nom de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="b08ed-248">Name of the stored procedure.</span></span> |<span data-ttu-id="b08ed-249">Non</span><span class="sxs-lookup"><span data-stu-id="b08ed-249">No</span></span> |
| <span data-ttu-id="b08ed-250">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="b08ed-250">storedProcedureParameters</span></span> |<span data-ttu-id="b08ed-251">Paramètres de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="b08ed-251">Parameters for the stored procedure.</span></span> |<span data-ttu-id="b08ed-252">Paires nom/valeur.</span><span class="sxs-lookup"><span data-stu-id="b08ed-252">Name/value pairs.</span></span> <span data-ttu-id="b08ed-253">Les noms et la casse des paramètres doivent correspondre aux noms et à la casse des paramètres de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="b08ed-253">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="b08ed-254">Non</span><span class="sxs-lookup"><span data-stu-id="b08ed-254">No</span></span> |
| <span data-ttu-id="b08ed-255">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="b08ed-255">sqlWriterTableType</span></span> |<span data-ttu-id="b08ed-256">Spécifiez le nom du type de table à utiliser dans la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="b08ed-256">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="b08ed-257">L’activité de copie place les données déplacées disponibles dans une table temporaire avec ce type de table.</span><span class="sxs-lookup"><span data-stu-id="b08ed-257">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="b08ed-258">Le code de procédure stockée peut ensuite fusionner les données copiées avec les données existantes.</span><span class="sxs-lookup"><span data-stu-id="b08ed-258">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="b08ed-259">Nom de type de table.</span><span class="sxs-lookup"><span data-stu-id="b08ed-259">A table type name.</span></span> |<span data-ttu-id="b08ed-260">Non</span><span class="sxs-lookup"><span data-stu-id="b08ed-260">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-to-sql-server"></a><span data-ttu-id="b08ed-261">Exemples JSON pour copier des données vers et depuis SQL Server</span><span class="sxs-lookup"><span data-stu-id="b08ed-261">JSON examples for copying data from and to SQL Server</span></span>
<span data-ttu-id="b08ed-262">Les exemples suivants présentent des exemples de définitions de JSON que vous pouvez utiliser pour créer un pipeline à l’aide [du Portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [de Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [d’Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b08ed-262">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="b08ed-263">Les exemples suivants indiquent comment copier des données vers et depuis SQL Server et un système Blob Storage Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b08ed-263">The following samples show how to copy data to and from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="b08ed-264">Toutefois, les données peuvent être copiées **directement** vers l’un des récepteurs indiqués [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) , via l’activité de copie de Microsoft Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b08ed-264">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-to-azure-blob"></a><span data-ttu-id="b08ed-265">Exemple : copie de données à partir de SQL Server vers un objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="b08ed-265">Example: Copy data from SQL Server to Azure Blob</span></span>
<span data-ttu-id="b08ed-266">L’exemple suivant montre :</span><span class="sxs-lookup"><span data-stu-id="b08ed-266">The following sample shows:</span></span>

1. <span data-ttu-id="b08ed-267">Service lié de type [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b08ed-267">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="b08ed-268">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b08ed-268">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="b08ed-269">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [SqlServerTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b08ed-269">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="b08ed-270">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b08ed-270">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="b08ed-271">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [SqlSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="b08ed-271">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="b08ed-272">L’exemple copie des données appartenant à une série horaire depuis une table SQL Server vers un objet blob Azure toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="b08ed-272">The sample copies time-series data from a SQL Server table to an Azure blob every hour.</span></span> <span data-ttu-id="b08ed-273">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="b08ed-273">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="b08ed-274">Dans un premier temps, configurez la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="b08ed-274">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="b08ed-275">Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="b08ed-275">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="b08ed-276">**Service SQL Server lié**</span><span class="sxs-lookup"><span data-stu-id="b08ed-276">**SQL Server linked service**</span></span>
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
<span data-ttu-id="b08ed-277">**Service lié Azure Blob Storage**</span><span class="sxs-lookup"><span data-stu-id="b08ed-277">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="b08ed-278">**Jeu de données d’entrée de SQL Server**</span><span class="sxs-lookup"><span data-stu-id="b08ed-278">**SQL Server input dataset**</span></span>

<span data-ttu-id="b08ed-279">L’exemple suppose que vous avez créé une table « MyTable » dans SQL Server et qu’elle contient une colonne appelée « timestampcolumn » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="b08ed-279">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="b08ed-280">Vous pouvez interroger plusieurs tables au sein d’une même base de données en utilisant un jeu de données unique, mais une seule table doit être utilisée pour la propriété typeProperty tableName du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="b08ed-280">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="b08ed-281">La définition de external sur true informe le service Data Factory que le jeu de données est externe à la Data Factory et non produite par une activité dans la Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b08ed-281">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="b08ed-282">**Jeu de données de sortie Azure Blob**</span><span class="sxs-lookup"><span data-stu-id="b08ed-282">**Azure Blob output dataset**</span></span>

<span data-ttu-id="b08ed-283">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="b08ed-283">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="b08ed-284">Le chemin d’accès du dossier pour l’objet blob est évalué dynamiquement en fonction de l’heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="b08ed-284">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="b08ed-285">Le chemin d’accès du dossier utilise l’année, le mois, le jour et l’heure de l’heure de début.</span><span class="sxs-lookup"><span data-stu-id="b08ed-285">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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
<span data-ttu-id="b08ed-286">**Pipeline avec activité de copie**</span><span class="sxs-lookup"><span data-stu-id="b08ed-286">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="b08ed-287">Le pipeline contient une activité de copie qui est configurée pour utiliser ces jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="b08ed-287">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="b08ed-288">Dans la définition du pipeline JSON, le type **source** est défini sur **SqlSource** et le type **sink** est défini sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="b08ed-288">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="b08ed-289">La requête SQL spécifiée pour la propriété **SqlReaderQuery** sélectionne les données de la dernière heure à copier.</span><span class="sxs-lookup"><span data-stu-id="b08ed-289">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
<span data-ttu-id="b08ed-290">Dans cet exemple, **sqlReaderQuery** est spécifié pour SqlSource.</span><span class="sxs-lookup"><span data-stu-id="b08ed-290">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="b08ed-291">L'activité de copie exécute cette requête dans la source de base de données SQL server pour obtenir les données.</span><span class="sxs-lookup"><span data-stu-id="b08ed-291">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="b08ed-292">Vous pouvez également spécifier une procédure stockée en indiquant **sqlReaderStoredProcedureName** et **storedProcedureParameters** (si la procédure stockée accepte des paramètres).</span><span class="sxs-lookup"><span data-stu-id="b08ed-292">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="b08ed-293">sqlReaderQuery peut faire référence à plusieurs tables de la base de données référencée par le jeu de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="b08ed-293">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="b08ed-294">Cela n’est pas limité à la seule table définie en tant que typeProperty tableName du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="b08ed-294">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="b08ed-295">Si vous ne spécifiez pas sqlReaderQuery ou sqlReaderStoredProcedureName, les colonnes définies dans la section Structure sont utilisées pour sélectionner une requête à exécuter dans l'Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="b08ed-295">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="b08ed-296">Si la définition du jeu de données ne possède pas de structure, toutes les colonnes de la table sont sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="b08ed-296">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="b08ed-297">Consultez la section [Sql Source](#sqlsource) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) pour obtenir la liste des propriétés prises en charge par SqlSource et BlobSink.</span><span class="sxs-lookup"><span data-stu-id="b08ed-297">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-to-sql-server"></a><span data-ttu-id="b08ed-298">Exemple : copie de données à partir d’un objet Blob Azure vers SQL Server</span><span class="sxs-lookup"><span data-stu-id="b08ed-298">Example: Copy data from Azure Blob to SQL Server</span></span>
<span data-ttu-id="b08ed-299">L’exemple suivant montre :</span><span class="sxs-lookup"><span data-stu-id="b08ed-299">The following sample shows:</span></span>

1. <span data-ttu-id="b08ed-300">un service lié de type [OnPremisesSqlServer](#linked-service-properties);</span><span class="sxs-lookup"><span data-stu-id="b08ed-300">The linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="b08ed-301">un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) ;</span><span class="sxs-lookup"><span data-stu-id="b08ed-301">The linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="b08ed-302">un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b08ed-302">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="b08ed-303">un [jeu de données](data-factory-create-datasets.md) de sortie de type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties) ;</span><span class="sxs-lookup"><span data-stu-id="b08ed-303">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="b08ed-304">un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) et [SqlSink](#sql-server-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="b08ed-304">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="b08ed-305">L'exemple copie des données de série horaire à partir d'un objet Blob Azure vers une table dans une base de données SQL Azure, toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="b08ed-305">The sample copies time-series data from an Azure blob to a SQL Server table every hour.</span></span> <span data-ttu-id="b08ed-306">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="b08ed-306">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="b08ed-307">**Service SQL Server lié**</span><span class="sxs-lookup"><span data-stu-id="b08ed-307">**SQL Server linked service**</span></span>

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
<span data-ttu-id="b08ed-308">**Service lié Azure Blob Storage**</span><span class="sxs-lookup"><span data-stu-id="b08ed-308">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="b08ed-309">**Jeu de données d'entrée d'objet Blob Azure**</span><span class="sxs-lookup"><span data-stu-id="b08ed-309">**Azure Blob input dataset**</span></span>

<span data-ttu-id="b08ed-310">Les données sont récupérées à partir d’un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="b08ed-310">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="b08ed-311">Le nom du chemin d'accès et du fichier de dossier pour l'objet blob sont évalués dynamiquement en fonction de l'heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="b08ed-311">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="b08ed-312">Le chemin d’accès du dossier utilise l’année, le mois et le jour de l’heure de début et le nom de fichier utilise la partie heure de l’heure de début.</span><span class="sxs-lookup"><span data-stu-id="b08ed-312">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="b08ed-313">Le paramètre « external » : « true » informe le service Data Factory que ce jeu de données est externe à la Data Factory et non produit par une activité dans la Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b08ed-313">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="b08ed-314">**Jeu de données de sortie de SQL Server**</span><span class="sxs-lookup"><span data-stu-id="b08ed-314">**SQL Server output dataset**</span></span>

<span data-ttu-id="b08ed-315">L’exemple copie les données dans une table nommée « MyTable » dans SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b08ed-315">The sample copies data to a table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="b08ed-316">Créez la table dans SQL Server avec le même nombre de colonnes que le fichier CSV d’objets Blob doit contenir.</span><span class="sxs-lookup"><span data-stu-id="b08ed-316">Create the table in SQL Server with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="b08ed-317">De nouvelles lignes sont ajoutées à la table toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="b08ed-317">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="b08ed-318">**Pipeline avec activité de copie**</span><span class="sxs-lookup"><span data-stu-id="b08ed-318">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="b08ed-319">Le pipeline contient une activité de copie qui est configurée pour utiliser ces jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="b08ed-319">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="b08ed-320">Dans la définition du pipeline JSON, le type **source** est défini sur **BlobSource** et le type **sink** est défini sur **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="b08ed-320">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

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

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="b08ed-321">Résolution des problèmes de connexion</span><span class="sxs-lookup"><span data-stu-id="b08ed-321">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="b08ed-322">Configurez votre serveur SQL Server pour qu’il accepte les connexions à distance.</span><span class="sxs-lookup"><span data-stu-id="b08ed-322">Configure your SQL Server to accept remote connections.</span></span> <span data-ttu-id="b08ed-323">Démarrez **SQL Server Management Studio**, cliquez avec le bouton droit de la souris sur **Serveur**, puis cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="b08ed-323">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="b08ed-324">Sélectionnez **Connexions** dans la liste, puis cochez **Autoriser les accès distants à ce serveur**.</span><span class="sxs-lookup"><span data-stu-id="b08ed-324">Select **Connections** from the list and check **Allow remote connections to the server**.</span></span>

    ![Activation des connexions à distance](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="b08ed-326">Vous trouverez la procédure détaillée à la page [Configurer l’option de configuration du serveur remote access](https://msdn.microsoft.com/library/ms191464.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b08ed-326">See [Configure the remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="b08ed-327">Lancez le **Gestionnaire de configuration SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="b08ed-327">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="b08ed-328">Développez **Configuration du réseau SQL Server** pour l’instance souhaitée, puis sélectionnez **Protocoles pour MSSQLSERVER**.</span><span class="sxs-lookup"><span data-stu-id="b08ed-328">Expand **SQL Server Network Configuration** for the instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="b08ed-329">Les protocoles doivent s’afficher dans le volet droit.</span><span class="sxs-lookup"><span data-stu-id="b08ed-329">You should see protocols in the right-pane.</span></span> <span data-ttu-id="b08ed-330">Activez TCP/IP en cliquant avec le bouton droit sur **TCP/IP** et en cliquant sur **Activer**.</span><span class="sxs-lookup"><span data-stu-id="b08ed-330">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![Activation de TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="b08ed-332">Consultez la page [Activer ou désactiver un protocole réseau de serveur](https://msdn.microsoft.com/library/ms191294.aspx) pour obtenir des détails et découvrir d’autres façons d’activer le protocole TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="b08ed-332">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="b08ed-333">Dans la même fenêtre, double-cliquez sur **TCP/IP** pour lancer la fenêtre des **propriétés de TCP/IP**.</span><span class="sxs-lookup"><span data-stu-id="b08ed-333">In the same window, double-click **TCP/IP** to launch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="b08ed-334">Allez sous l’onglet **Adresses IP** .</span><span class="sxs-lookup"><span data-stu-id="b08ed-334">Switch to the **IP Addresses** tab.</span></span> <span data-ttu-id="b08ed-335">Faites défiler l’écran vers le bas jusqu’à la section **IPAll** .</span><span class="sxs-lookup"><span data-stu-id="b08ed-335">Scroll down to see **IPAll** section.</span></span> <span data-ttu-id="b08ed-336">Notez le **Port TCP** (le port par défaut est le **1433**).</span><span class="sxs-lookup"><span data-stu-id="b08ed-336">Note down the **TCP Port **(default is **1433**).</span></span>
5. <span data-ttu-id="b08ed-337">Créez une **règle de Pare-feu Windows** sur l’ordinateur pour autoriser le trafic à entrer par ce port.</span><span class="sxs-lookup"><span data-stu-id="b08ed-337">Create a **rule for the Windows Firewall** on the machine to allow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="b08ed-338">**Vérifiez la connexion**: servez-vous de SQL Server Management Studio sur un autre ordinateur pour vous connecter à SQL Server en utilisant un nom qualifié complet.</span><span class="sxs-lookup"><span data-stu-id="b08ed-338">**Verify connection**: To connect to the SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="b08ed-339">Par exemple : « <machine><domain>.corp<company>.com, 1433 ».</span><span class="sxs-lookup"><span data-stu-id="b08ed-339">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="b08ed-340">Pour plus d’informations, consultez [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="b08ed-340">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="b08ed-341">Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.</span><span class="sxs-lookup"><span data-stu-id="b08ed-341">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="b08ed-342">Colonnes d’identité dans la base de données cible</span><span class="sxs-lookup"><span data-stu-id="b08ed-342">Identity columns in the target database</span></span>
<span data-ttu-id="b08ed-343">Cette section fournit un exemple qui copie des données d’une table source sans colonne d’identité vers une table de destination avec une colonne d’identité.</span><span class="sxs-lookup"><span data-stu-id="b08ed-343">This section provides an example that copies data from a source table with no identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="b08ed-344">**Table source :**</span><span class="sxs-lookup"><span data-stu-id="b08ed-344">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="b08ed-345">**Table de destination :**</span><span class="sxs-lookup"><span data-stu-id="b08ed-345">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="b08ed-346">Notez que la table cible possède une colonne d’identité.</span><span class="sxs-lookup"><span data-stu-id="b08ed-346">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="b08ed-347">**Définition du jeu de données JSON source**</span><span class="sxs-lookup"><span data-stu-id="b08ed-347">**Source dataset JSON definition**</span></span>

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
<span data-ttu-id="b08ed-348">**Définition de jeu de données JSON de destination**</span><span class="sxs-lookup"><span data-stu-id="b08ed-348">**Destination dataset JSON definition**</span></span>

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

<span data-ttu-id="b08ed-349">Notez que vos tables source et cible ont des schémas différents (la cible possède une colonne supplémentaire avec identité).</span><span class="sxs-lookup"><span data-stu-id="b08ed-349">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="b08ed-350">Dans ce scénario, vous devez spécifier la propriété **structure** dans la définition du jeu de données cible, qui n’inclut pas la colonne d’identité.</span><span class="sxs-lookup"><span data-stu-id="b08ed-350">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="b08ed-351">Appel d’une procédure stockée pour un récepteur SQL</span><span class="sxs-lookup"><span data-stu-id="b08ed-351">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="b08ed-352">L’article [Appeler une procédure stockée pour un récepteur SQL dans l’activité de copie](data-factory-invoke-stored-procedure-from-copy-activity.md) illustre l’appel d’une procédure stockée à partir d’un récepteur SQL dans l’activité de copie d’un pipeline.</span><span class="sxs-lookup"><span data-stu-id="b08ed-352">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="b08ed-353">Mappage de type pour SQL Server</span><span class="sxs-lookup"><span data-stu-id="b08ed-353">Type mapping for SQL server</span></span>
<span data-ttu-id="b08ed-354">Comme mentionné dans l’article consacré aux [activités de déplacement des données](data-factory-data-movement-activities.md) , l’activité de copie convertit automatiquement des types source en types récepteur à l’aide de l’approche en 2 étapes suivante :</span><span class="sxs-lookup"><span data-stu-id="b08ed-354">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="b08ed-355">Conversion de types natifs source en types .NET</span><span class="sxs-lookup"><span data-stu-id="b08ed-355">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="b08ed-356">Conversion de types .NET en types récepteur natifs</span><span class="sxs-lookup"><span data-stu-id="b08ed-356">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="b08ed-357">Lors du déplacement de données vers et à partir de SQL Server, les mappages suivants sont utilisés à partir du type SQL vers le type .NET et vice versa.</span><span class="sxs-lookup"><span data-stu-id="b08ed-357">When moving data to & from SQL server, the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="b08ed-358">Le mappage est identique au mappage du type de données SQL Server pour ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="b08ed-358">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="b08ed-359">Type de moteur de base de données SQL Server</span><span class="sxs-lookup"><span data-stu-id="b08ed-359">SQL Server Database Engine type</span></span> | <span data-ttu-id="b08ed-360">Type de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="b08ed-360">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="b08ed-361">bigint</span><span class="sxs-lookup"><span data-stu-id="b08ed-361">bigint</span></span> |<span data-ttu-id="b08ed-362">Int64</span><span class="sxs-lookup"><span data-stu-id="b08ed-362">Int64</span></span> |
| <span data-ttu-id="b08ed-363">binaire</span><span class="sxs-lookup"><span data-stu-id="b08ed-363">binary</span></span> |<span data-ttu-id="b08ed-364">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b08ed-364">Byte[]</span></span> |
| <span data-ttu-id="b08ed-365">bit</span><span class="sxs-lookup"><span data-stu-id="b08ed-365">bit</span></span> |<span data-ttu-id="b08ed-366">Boolean</span><span class="sxs-lookup"><span data-stu-id="b08ed-366">Boolean</span></span> |
| <span data-ttu-id="b08ed-367">char</span><span class="sxs-lookup"><span data-stu-id="b08ed-367">char</span></span> |<span data-ttu-id="b08ed-368">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="b08ed-368">String, Char[]</span></span> |
| <span data-ttu-id="b08ed-369">date</span><span class="sxs-lookup"><span data-stu-id="b08ed-369">date</span></span> |<span data-ttu-id="b08ed-370">DateTime</span><span class="sxs-lookup"><span data-stu-id="b08ed-370">DateTime</span></span> |
| <span data-ttu-id="b08ed-371">DateTime</span><span class="sxs-lookup"><span data-stu-id="b08ed-371">Datetime</span></span> |<span data-ttu-id="b08ed-372">DateTime</span><span class="sxs-lookup"><span data-stu-id="b08ed-372">DateTime</span></span> |
| <span data-ttu-id="b08ed-373">datetime2</span><span class="sxs-lookup"><span data-stu-id="b08ed-373">datetime2</span></span> |<span data-ttu-id="b08ed-374">DateTime</span><span class="sxs-lookup"><span data-stu-id="b08ed-374">DateTime</span></span> |
| <span data-ttu-id="b08ed-375">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="b08ed-375">Datetimeoffset</span></span> |<span data-ttu-id="b08ed-376">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="b08ed-376">DateTimeOffset</span></span> |
| <span data-ttu-id="b08ed-377">Décimal</span><span class="sxs-lookup"><span data-stu-id="b08ed-377">Decimal</span></span> |<span data-ttu-id="b08ed-378">Décimal</span><span class="sxs-lookup"><span data-stu-id="b08ed-378">Decimal</span></span> |
| <span data-ttu-id="b08ed-379">Attribut FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="b08ed-379">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="b08ed-380">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b08ed-380">Byte[]</span></span> |
| <span data-ttu-id="b08ed-381">Float</span><span class="sxs-lookup"><span data-stu-id="b08ed-381">Float</span></span> |<span data-ttu-id="b08ed-382">Double</span><span class="sxs-lookup"><span data-stu-id="b08ed-382">Double</span></span> |
| <span data-ttu-id="b08ed-383">image</span><span class="sxs-lookup"><span data-stu-id="b08ed-383">image</span></span> |<span data-ttu-id="b08ed-384">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b08ed-384">Byte[]</span></span> |
| <span data-ttu-id="b08ed-385">int</span><span class="sxs-lookup"><span data-stu-id="b08ed-385">int</span></span> |<span data-ttu-id="b08ed-386">Int32</span><span class="sxs-lookup"><span data-stu-id="b08ed-386">Int32</span></span> |
| <span data-ttu-id="b08ed-387">money</span><span class="sxs-lookup"><span data-stu-id="b08ed-387">money</span></span> |<span data-ttu-id="b08ed-388">Décimal</span><span class="sxs-lookup"><span data-stu-id="b08ed-388">Decimal</span></span> |
| <span data-ttu-id="b08ed-389">nchar</span><span class="sxs-lookup"><span data-stu-id="b08ed-389">nchar</span></span> |<span data-ttu-id="b08ed-390">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="b08ed-390">String, Char[]</span></span> |
| <span data-ttu-id="b08ed-391">ntext</span><span class="sxs-lookup"><span data-stu-id="b08ed-391">ntext</span></span> |<span data-ttu-id="b08ed-392">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="b08ed-392">String, Char[]</span></span> |
| <span data-ttu-id="b08ed-393">numérique</span><span class="sxs-lookup"><span data-stu-id="b08ed-393">numeric</span></span> |<span data-ttu-id="b08ed-394">Décimal</span><span class="sxs-lookup"><span data-stu-id="b08ed-394">Decimal</span></span> |
| <span data-ttu-id="b08ed-395">nvarchar</span><span class="sxs-lookup"><span data-stu-id="b08ed-395">nvarchar</span></span> |<span data-ttu-id="b08ed-396">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="b08ed-396">String, Char[]</span></span> |
| <span data-ttu-id="b08ed-397">real</span><span class="sxs-lookup"><span data-stu-id="b08ed-397">real</span></span> |<span data-ttu-id="b08ed-398">Single</span><span class="sxs-lookup"><span data-stu-id="b08ed-398">Single</span></span> |
| <span data-ttu-id="b08ed-399">rowversion</span><span class="sxs-lookup"><span data-stu-id="b08ed-399">rowversion</span></span> |<span data-ttu-id="b08ed-400">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b08ed-400">Byte[]</span></span> |
| <span data-ttu-id="b08ed-401">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="b08ed-401">smalldatetime</span></span> |<span data-ttu-id="b08ed-402">DateTime</span><span class="sxs-lookup"><span data-stu-id="b08ed-402">DateTime</span></span> |
| <span data-ttu-id="b08ed-403">smallint</span><span class="sxs-lookup"><span data-stu-id="b08ed-403">smallint</span></span> |<span data-ttu-id="b08ed-404">Int16</span><span class="sxs-lookup"><span data-stu-id="b08ed-404">Int16</span></span> |
| <span data-ttu-id="b08ed-405">smallmoney</span><span class="sxs-lookup"><span data-stu-id="b08ed-405">smallmoney</span></span> |<span data-ttu-id="b08ed-406">Décimal</span><span class="sxs-lookup"><span data-stu-id="b08ed-406">Decimal</span></span> |
| <span data-ttu-id="b08ed-407">sql_variant</span><span class="sxs-lookup"><span data-stu-id="b08ed-407">sql_variant</span></span> |<span data-ttu-id="b08ed-408">Objet *</span><span class="sxs-lookup"><span data-stu-id="b08ed-408">Object *</span></span> |
| <span data-ttu-id="b08ed-409">texte</span><span class="sxs-lookup"><span data-stu-id="b08ed-409">text</span></span> |<span data-ttu-id="b08ed-410">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="b08ed-410">String, Char[]</span></span> |
| <span data-ttu-id="b08ed-411">time</span><span class="sxs-lookup"><span data-stu-id="b08ed-411">time</span></span> |<span data-ttu-id="b08ed-412">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="b08ed-412">TimeSpan</span></span> |
| <span data-ttu-id="b08ed-413">timestamp</span><span class="sxs-lookup"><span data-stu-id="b08ed-413">timestamp</span></span> |<span data-ttu-id="b08ed-414">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b08ed-414">Byte[]</span></span> |
| <span data-ttu-id="b08ed-415">tinyint</span><span class="sxs-lookup"><span data-stu-id="b08ed-415">tinyint</span></span> |<span data-ttu-id="b08ed-416">Byte</span><span class="sxs-lookup"><span data-stu-id="b08ed-416">Byte</span></span> |
| <span data-ttu-id="b08ed-417">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="b08ed-417">uniqueidentifier</span></span> |<span data-ttu-id="b08ed-418">Guid</span><span class="sxs-lookup"><span data-stu-id="b08ed-418">Guid</span></span> |
| <span data-ttu-id="b08ed-419">varbinary</span><span class="sxs-lookup"><span data-stu-id="b08ed-419">varbinary</span></span> |<span data-ttu-id="b08ed-420">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b08ed-420">Byte[]</span></span> |
| <span data-ttu-id="b08ed-421">varchar</span><span class="sxs-lookup"><span data-stu-id="b08ed-421">varchar</span></span> |<span data-ttu-id="b08ed-422">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="b08ed-422">String, Char[]</span></span> |
| <span data-ttu-id="b08ed-423">xml</span><span class="sxs-lookup"><span data-stu-id="b08ed-423">xml</span></span> |<span data-ttu-id="b08ed-424">xml</span><span class="sxs-lookup"><span data-stu-id="b08ed-424">Xml</span></span> |

## <a name="mapping-source-to-sink-columns"></a><span data-ttu-id="b08ed-425">Mappage des colonnes source aux colonnes du récepteur</span><span class="sxs-lookup"><span data-stu-id="b08ed-425">Mapping source to sink columns</span></span>
<span data-ttu-id="b08ed-426">Pour savoir comment mapper des colonnes d’un jeu de données source à des colonnes d’un jeu de données récepteur, voir [Mappage des colonnes d’un jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="b08ed-426">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="b08ed-427">Copie renouvelée</span><span class="sxs-lookup"><span data-stu-id="b08ed-427">Repeatable copy</span></span>
<span data-ttu-id="b08ed-428">Lors de la copie de données sur une base de données SQL Server, l’activité de copie ajoute des données à la table de récepteur par défaut.</span><span class="sxs-lookup"><span data-stu-id="b08ed-428">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="b08ed-429">Pour effectuer une opération UPSERT à la place, consultez l’article [Écriture renouvelée sur SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink).</span><span class="sxs-lookup"><span data-stu-id="b08ed-429">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="b08ed-430">Lorsque vous copiez des données à partir de magasins de données relationnels, gardez à l’esprit la répétabilité de l’opération, afin d’éviter des résultats imprévus.</span><span class="sxs-lookup"><span data-stu-id="b08ed-430">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="b08ed-431">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="b08ed-431">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="b08ed-432">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="b08ed-432">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="b08ed-433">Lorsqu’une tranche est réexécutée d’une manière ou d’une autre, vous devez vous assurer que les mêmes données sont lues et ce, quel que soit le nombre d’exécutions de la tranche.</span><span class="sxs-lookup"><span data-stu-id="b08ed-433">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="b08ed-434">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="b08ed-434">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="b08ed-435">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="b08ed-435">Performance and Tuning</span></span>
<span data-ttu-id="b08ed-436">Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="b08ed-436">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
