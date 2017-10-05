---
title: "Copier des données vers/à partir d’Oracle à l’aide de Data Factory | Microsoft Docs"
description: "Découvrez comment copier des données vers et à partir d’une base de données Oracle locale à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: bb6af719fe6f1a30c5933ce4342a4c0c072f3ff4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a><span data-ttu-id="d9ed9-103">Copier des données vers/à partir d’Oracle en local à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d9ed9-103">Copy data to/from on-premises Oracle using Azure Data Factory</span></span>
<span data-ttu-id="d9ed9-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour déplacer des données vers/à partir d’une base de données Oracle locale.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises Oracle database.</span></span> <span data-ttu-id="d9ed9-105">Il s’appuie sur l’article [Activités de déplacement des données](data-factory-data-movement-activities.md), qui présente une vue d’ensemble du déplacement de données avec l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="d9ed9-106">Scénarios pris en charge</span><span class="sxs-lookup"><span data-stu-id="d9ed9-106">Supported scenarios</span></span>
<span data-ttu-id="d9ed9-107">Vous pouvez copier des données **d’une base de données Oracle** vers les magasins de données suivants :</span><span class="sxs-lookup"><span data-stu-id="d9ed9-107">You can copy data **from an Oracle database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="d9ed9-108">Vous pouvez copier des données des magasins de données suivants **vers une base de données Oracle** :</span><span class="sxs-lookup"><span data-stu-id="d9ed9-108">You can copy data from the following data stores **to an Oracle database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a><span data-ttu-id="d9ed9-109">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="d9ed9-109">Prerequisites</span></span>
<span data-ttu-id="d9ed9-110">Data Factory prend en charge la connexion à des sources Oracle locales à l’aide de la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-110">Data Factory supports connecting to on-premises Oracle sources using the Data Management Gateway.</span></span> <span data-ttu-id="d9ed9-111">Consultez l’article [Passerelle de gestion de données](data-factory-data-management-gateway.md) pour en savoir plus sur la passerelle de gestion des données et l’article [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) pour obtenir des instructions détaillées sur la configuration de la passerelle pour un pipeline de données afin de déplacer des données.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article to learn about Data Management Gateway and [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

<span data-ttu-id="d9ed9-112">Une passerelle est requise même si la base de données Oracle est hébergée sur une machine virtuelle Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-112">Gateway is required even if the Oracle is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="d9ed9-113">Vous pouvez installer la passerelle sur la même machine virtuelle IaaS que le magasin de données, ou sur une autre machine virtuelle pourvu que la passerelle puisse se connecter à la base de données.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="d9ed9-114">Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="d9ed9-115">Versions prises en charge et installation</span><span class="sxs-lookup"><span data-stu-id="d9ed9-115">Supported versions and installation</span></span>
<span data-ttu-id="d9ed9-116">Ce connecteur Oracle prend en charge deux versions de pilotes :</span><span class="sxs-lookup"><span data-stu-id="d9ed9-116">This Oracle connector support two versions of drivers:</span></span>

- <span data-ttu-id="d9ed9-117">**Pilote Microsoft pour Oracle (recommandé)** : à compter de Data Management Gateway version 2.7, un pilote Microsoft pour Oracle est installé automatiquement avec la passerelle : il n’est donc pas nécessaire de gérer le pilote pour établir la connexion à Oracle. Vous pouvez également obtenir de meilleures performances de copie en utilisant ce pilote.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-117">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with the gateway, so you don't need to additionally handle the driver in order to establish connectivity to Oracle, and you can also experience better copy performance using this driver.</span></span> <span data-ttu-id="d9ed9-118">Voici les versions de bases de données Oracle prises en charge :</span><span class="sxs-lookup"><span data-stu-id="d9ed9-118">Below versions of Oracle databases are supported:</span></span>
    - <span data-ttu-id="d9ed9-119">Oracle 12c R1 (12.1)</span><span class="sxs-lookup"><span data-stu-id="d9ed9-119">Oracle 12c R1 (12.1)</span></span>
    - <span data-ttu-id="d9ed9-120">Oracle 11g R1, R2 (11.1, 11.2)</span><span class="sxs-lookup"><span data-stu-id="d9ed9-120">Oracle 11g R1, R2 (11.1, 11.2)</span></span>
    - <span data-ttu-id="d9ed9-121">Oracle 10g R1, R2 (10.1, 10.2)</span><span class="sxs-lookup"><span data-stu-id="d9ed9-121">Oracle 10g R1, R2 (10.1, 10.2)</span></span>
    - <span data-ttu-id="d9ed9-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span><span class="sxs-lookup"><span data-stu-id="d9ed9-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span></span>
    - <span data-ttu-id="d9ed9-123">Oracle 8i R3 (8.1.7)</span><span class="sxs-lookup"><span data-stu-id="d9ed9-123">Oracle 8i R3 (8.1.7)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9ed9-124">Actuellement, le pilote Microsoft pour Oracle prend uniquement en charge la copie de données à partir d’Oracle, mais non l’écriture dans Oracle.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-124">Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing to Oracle.</span></span> <span data-ttu-id="d9ed9-125">Notez également que la fonctionnalité de connexion de test dans l’onglet Data Management Gateway Diagnostics (Diagnostics de passerelle de gestion des données) ne prend pas en charge ce pilote.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-125">And note the test connection capability in Data Management Gateway Diagnostics tab does not support this driver.</span></span> <span data-ttu-id="d9ed9-126">Dans ce cas, vous pouvez valider la connectivité à l’aide de l’assistant de copie.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-126">Alternatively, you can use the copy wizard to validate the connectivity.</span></span>
>

- <span data-ttu-id="d9ed9-127">**Fournisseur de données Oracle pour .NET :** vous pouvez également choisir d’utiliser le fournisseur de données Oracle pour copier des données à partir de ou vers Oracle.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-127">**Oracle Data Provider for .NET:** you can also choose to use Oracle Data Provider to copy data from/to Oracle.</span></span> <span data-ttu-id="d9ed9-128">Ce composant est inclus dans [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-128">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span></span> <span data-ttu-id="d9ed9-129">Installez la version appropriée (32/64 bits) sur l’ordinateur sur lequel la passerelle est installée.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-129">Install the appropriate version (32/64 bit) on the machine where the gateway is installed.</span></span> <span data-ttu-id="d9ed9-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) peut accéder à Oracle Database 10g Release 2 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access to Oracle Database 10g Release 2 or later.</span></span>

    <span data-ttu-id="d9ed9-131">Si vous choisissez « Installation XCopy », suivez les étapes dans le fichier readme.htm.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-131">If you choose “XCopy Installation”, follow steps in the readme.htm.</span></span> <span data-ttu-id="d9ed9-132">Nous vous recommandons de choisir le programme d’installation avec interface utilisateur (et pas le programme d’installation XCopy).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-132">We recommend you choose the installer with UI (non-XCopy one).</span></span>

    <span data-ttu-id="d9ed9-133">Après avoir installé le fournisseur, **redémarrez** le service hôte de la passerelle de gestion des données sur votre ordinateur à l’aide de l’applet Services (ou) du Gestionnaire de configuration de la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-133">After installing the provider, **restart** the Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span></span>  

<span data-ttu-id="d9ed9-134">Si vous utilisez l’Assistant Copie pour créer le pipeline de copie, le type de pilote sera déterminé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-134">If you use copy wizard to author the copy pipeline, the driver type will be auto-determined.</span></span> <span data-ttu-id="d9ed9-135">Le pilote Microsoft est utilisé par défaut, sauf la version de votre passerelle est antérieure à 2.7 ou si vous choisissez Oracle comme récepteur.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-135">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d9ed9-136">Prise en main</span><span class="sxs-lookup"><span data-stu-id="d9ed9-136">Getting started</span></span>
<span data-ttu-id="d9ed9-137">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers/depuis une base de données Oracle locale à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-137">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span></span>

<span data-ttu-id="d9ed9-138">Le moyen le plus simple de créer un pipeline consiste à utiliser **l’Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-138">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="d9ed9-139">Consultez la page [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant Copier des données.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-139">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="d9ed9-140">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-140">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d9ed9-141">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-141">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="d9ed9-142">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="d9ed9-142">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="d9ed9-143">Création d'une **fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-143">Create a **data factory**.</span></span> <span data-ttu-id="d9ed9-144">Une fabrique de données peut contenir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-144">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="d9ed9-145">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-145">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="d9ed9-146">Par exemple, si vous copiez des données d’une base de données Oracle vers Stockage Blob Azure, vous créez deux services liés pour lier votre base de données Oracle et votre compte de stockage Azure à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-146">For example, if you are copying data from an Oralce database to an Azure blob storage, you create two linked services to link your Oracle database and Azure storage account to your data factory.</span></span> <span data-ttu-id="d9ed9-147">Pour les propriétés du service lié qui sont propres à Oracle, consultez la section [Propriétés du service lié](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-147">For linked service properties that are specific to Oracle, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="d9ed9-148">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-148">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="d9ed9-149">Dans l’exemple mentionné à la dernière étape, vous créez un jeu de données pour spécifier la table de votre base de données Oracle qui doit contenir les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-149">In the example mentioned in the last step, you create a dataset to specify the table in your Oracle database that contains the input data.</span></span> <span data-ttu-id="d9ed9-150">Ensuite, vous créez un autre jeu de données pour spécifier le conteneur d’objets blob et le dossier qui contient les données copiées à partir de la base de données Oracle.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-150">And, you create another dataset to specify the blob container and the folder that holds the data copied from the Oracle database.</span></span> <span data-ttu-id="d9ed9-151">Pour plus d’informations sur les propriétés de jeu de données qui sont propres à Oracle, consultez la section [Propriétés du jeu de données](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-151">For dataset properties that are specific to Oracle, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="d9ed9-152">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-152">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="d9ed9-153">Dans l’exemple mentionné plus haut, vous utilisez OracleSource comme source et BlobSink comme récepteur pour l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-153">In the example mentioned earlier, you use OracleSource as a source and BlobSink as a sink for the copy activity.</span></span> <span data-ttu-id="d9ed9-154">De la même façon, si vous copiez des données du Stockage Blob Azure vers une base de données Oracle, vous utilisez BlobSource et OracleSink dans l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-154">Similarly, if you are copying from Azure Blob Storage to Oracle Database, you use BlobSource and OracleSink in the copy activity.</span></span> <span data-ttu-id="d9ed9-155">Pour les propriétés d’activité de copie qui sont spécifiques d’une base de données Oracle, consultez la section [Propriétés de l’activité de copie](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-155">For copy activity properties that are specific to Oracle database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="d9ed9-156">Pour plus d’informations sur l’utilisation d’un magasin de données comme source ou comme récepteur, cliquez sur le lien de la section précédente correspondant à votre magasin de données.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-156">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span> 

<span data-ttu-id="d9ed9-157">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-157">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="d9ed9-158">Lorsque vous utilisez des outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory au format JSON.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-158">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="d9ed9-159">Pour obtenir des exemples comportant des définitions JSON pour les entités Data Factory utilisées pour copier les données vers ou à partir d’une base de données Oracle locale, consultez la section [Exemples JSON](#json-examples-for-copying-data-to-and-from-oracle-database) de cet article.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-159">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises Oracle database, see [JSON examples](#json-examples-for-copying-data-to-and-from-oracle-database) section of this article.</span></span>

<span data-ttu-id="d9ed9-160">Les sections suivantes fournissent des informations sur les propriétés JSON utilisées pour définir les entités Data Factory :</span><span class="sxs-lookup"><span data-stu-id="d9ed9-160">The following sections provide details about JSON properties that are used to define Data Factory entities:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d9ed9-161">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="d9ed9-161">Linked service properties</span></span>
<span data-ttu-id="d9ed9-162">Le tableau suivant fournit la description des éléments JSON spécifiques au service lié Oracle.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-162">The following table provides description for JSON elements specific to Oracle linked service.</span></span>

| <span data-ttu-id="d9ed9-163">Propriété</span><span class="sxs-lookup"><span data-stu-id="d9ed9-163">Property</span></span> | <span data-ttu-id="d9ed9-164">Description</span><span class="sxs-lookup"><span data-stu-id="d9ed9-164">Description</span></span> | <span data-ttu-id="d9ed9-165">Requis</span><span class="sxs-lookup"><span data-stu-id="d9ed9-165">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d9ed9-166">type</span><span class="sxs-lookup"><span data-stu-id="d9ed9-166">type</span></span> |<span data-ttu-id="d9ed9-167">Le type de propriété doit être défini sur : **OnPremisesOracle**</span><span class="sxs-lookup"><span data-stu-id="d9ed9-167">The type property must be set to: **OnPremisesOracle**</span></span> |<span data-ttu-id="d9ed9-168">Oui</span><span class="sxs-lookup"><span data-stu-id="d9ed9-168">Yes</span></span> |
| <span data-ttu-id="d9ed9-169">driverType</span><span class="sxs-lookup"><span data-stu-id="d9ed9-169">driverType</span></span> | <span data-ttu-id="d9ed9-170">Spécifiez le pilote à utiliser pour copier les données à partir de ou vers la base de données Oracle.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-170">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="d9ed9-171">Valeurs autorisées : **Microsoft** ou **ODP** (par défaut).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-171">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="d9ed9-172">Consultez la section [Version prise en charge et installation](#supported-versions-and-installation) sur les détails du pilote.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-172">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="d9ed9-173">Non</span><span class="sxs-lookup"><span data-stu-id="d9ed9-173">No</span></span> |
| <span data-ttu-id="d9ed9-174">connectionString</span><span class="sxs-lookup"><span data-stu-id="d9ed9-174">connectionString</span></span> | <span data-ttu-id="d9ed9-175">Spécifier les informations requises pour la connexion à l’instance de base de données Oracle pour la propriété connectionString.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-175">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="d9ed9-176">Oui</span><span class="sxs-lookup"><span data-stu-id="d9ed9-176">Yes</span></span> |
| <span data-ttu-id="d9ed9-177">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d9ed9-177">gatewayName</span></span> | <span data-ttu-id="d9ed9-178">Nom de la passerelle utilisée pour se connecter au serveur Oracle local</span><span class="sxs-lookup"><span data-stu-id="d9ed9-178">Name of the gateway that that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="d9ed9-179">Oui</span><span class="sxs-lookup"><span data-stu-id="d9ed9-179">Yes</span></span> |

<span data-ttu-id="d9ed9-180">**Exemple : avec le pilote Microsoft**</span><span class="sxs-lookup"><span data-stu-id="d9ed9-180">**Example: using Microsoft driver:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="d9ed9-181">**Exemple : avec le pilote ODP**</span><span class="sxs-lookup"><span data-stu-id="d9ed9-181">**Example: using ODP driver**</span></span>

<span data-ttu-id="d9ed9-182">Accédez à [ce site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) pour connaître les formats autorisés.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-182">Refer to [this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for the allowed formats.</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="d9ed9-183">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="d9ed9-183">Dataset properties</span></span>
<span data-ttu-id="d9ed9-184">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-184">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="d9ed9-185">Les sections telles que la structure, la disponibilité et la stratégie d’un jeu de données JSON sont similaires pour tous les types de jeux de données (Oracle, objet blob Azure, table Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-185">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="d9ed9-186">La section typeProperties est différente pour chaque type de jeu de données et fournit des informations sur l'emplacement des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-186">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="d9ed9-187">La section typeProperties pour le jeu de données de type OracleTable a les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="d9ed9-187">The typeProperties section for the dataset of type OracleTable has the following properties:</span></span>

| <span data-ttu-id="d9ed9-188">Propriété</span><span class="sxs-lookup"><span data-stu-id="d9ed9-188">Property</span></span> | <span data-ttu-id="d9ed9-189">Description</span><span class="sxs-lookup"><span data-stu-id="d9ed9-189">Description</span></span> | <span data-ttu-id="d9ed9-190">Requis</span><span class="sxs-lookup"><span data-stu-id="d9ed9-190">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d9ed9-191">TableName</span><span class="sxs-lookup"><span data-stu-id="d9ed9-191">tableName</span></span> |<span data-ttu-id="d9ed9-192">Nom de la table dans la base de données Oracle à laquelle le service lié fait référence.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-192">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="d9ed9-193">Non (si **oracleReaderQuery** de **OracleSource** est spécifié)</span><span class="sxs-lookup"><span data-stu-id="d9ed9-193">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="d9ed9-194">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="d9ed9-194">Copy activity properties</span></span>
<span data-ttu-id="d9ed9-195">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-195">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="d9ed9-196">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-196">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="d9ed9-197">L'activité de copie accepte uniquement une entrée et produit une seule sortie.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-197">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="d9ed9-198">En revanche, les propriétés disponibles dans la section typeProperties de l’activité varient pour chaque type d'activité.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-198">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="d9ed9-199">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-199">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="oraclesource"></a><span data-ttu-id="d9ed9-200">OracleSource</span><span class="sxs-lookup"><span data-stu-id="d9ed9-200">OracleSource</span></span>
<span data-ttu-id="d9ed9-201">Dans le cas d’une activité de copie, quand la source est de type **OracleSource**, les propriétés suivantes sont disponibles dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="d9ed9-201">In Copy activity, when the source is of type **OracleSource** the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="d9ed9-202">Propriété</span><span class="sxs-lookup"><span data-stu-id="d9ed9-202">Property</span></span> | <span data-ttu-id="d9ed9-203">Description</span><span class="sxs-lookup"><span data-stu-id="d9ed9-203">Description</span></span> | <span data-ttu-id="d9ed9-204">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="d9ed9-204">Allowed values</span></span> | <span data-ttu-id="d9ed9-205">Requis</span><span class="sxs-lookup"><span data-stu-id="d9ed9-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d9ed9-206">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="d9ed9-206">oracleReaderQuery</span></span> |<span data-ttu-id="d9ed9-207">Utilise la requête personnalisée pour lire des données.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-207">Use the custom query to read data.</span></span> |<span data-ttu-id="d9ed9-208">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-208">SQL query string.</span></span> <span data-ttu-id="d9ed9-209">Par exemple : select * from MyTable</span><span class="sxs-lookup"><span data-stu-id="d9ed9-209">For example: select * from MyTable</span></span> <br/><br/><span data-ttu-id="d9ed9-210">Si non spécifié, l’instruction SQL est exécutée : select * from MyTable</span><span class="sxs-lookup"><span data-stu-id="d9ed9-210">If not specified, the SQL statement that is executed: select * from MyTable</span></span> |<span data-ttu-id="d9ed9-211">Non (si **tableName** de **dataset** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="d9ed9-211">No (if **tableName** of **dataset** is specified)</span></span> |

### <a name="oraclesink"></a><span data-ttu-id="d9ed9-212">OracleSink</span><span class="sxs-lookup"><span data-stu-id="d9ed9-212">OracleSink</span></span>
<span data-ttu-id="d9ed9-213">**OracleSink** prend en charge les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="d9ed9-213">**OracleSink** supports the following properties:</span></span>

| <span data-ttu-id="d9ed9-214">Propriété</span><span class="sxs-lookup"><span data-stu-id="d9ed9-214">Property</span></span> | <span data-ttu-id="d9ed9-215">Description</span><span class="sxs-lookup"><span data-stu-id="d9ed9-215">Description</span></span> | <span data-ttu-id="d9ed9-216">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="d9ed9-216">Allowed values</span></span> | <span data-ttu-id="d9ed9-217">Requis</span><span class="sxs-lookup"><span data-stu-id="d9ed9-217">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d9ed9-218">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="d9ed9-218">writeBatchTimeout</span></span> |<span data-ttu-id="d9ed9-219">Temps d’attente pour que l’opération d’insertion de lot soit terminée avant d’expirer.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-219">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="d9ed9-220">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="d9ed9-220">timespan</span></span><br/><br/> <span data-ttu-id="d9ed9-221">Exemple : « 00:30:00 » (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-221">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="d9ed9-222">Non</span><span class="sxs-lookup"><span data-stu-id="d9ed9-222">No</span></span> |
| <span data-ttu-id="d9ed9-223">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="d9ed9-223">writeBatchSize</span></span> |<span data-ttu-id="d9ed9-224">Insère des données dans la table SQL lorsque la taille du tampon atteint writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="d9ed9-224">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="d9ed9-225">Nombre entier (nombre de lignes)</span><span class="sxs-lookup"><span data-stu-id="d9ed9-225">Integer (number of rows)</span></span> |<span data-ttu-id="d9ed9-226">Non (valeur par défaut : 100)</span><span class="sxs-lookup"><span data-stu-id="d9ed9-226">No (default: 100)</span></span> |
| <span data-ttu-id="d9ed9-227">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="d9ed9-227">sqlWriterCleanupScript</span></span> |<span data-ttu-id="d9ed9-228">Spécifiez une requête pour exécuter l’activité de copie afin que les données d’un segment spécifique soient nettoyées.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-228">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="d9ed9-229">Une instruction de requête.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-229">A query statement.</span></span> |<span data-ttu-id="d9ed9-230">Non</span><span class="sxs-lookup"><span data-stu-id="d9ed9-230">No</span></span> |
| <span data-ttu-id="d9ed9-231">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="d9ed9-231">sliceIdentifierColumnName</span></span> |<span data-ttu-id="d9ed9-232">Spécifiez le nom de la colonne que l’activité de copie doit remplir avec l’identificateur de segment généré automatiquement, et qui est utilisée pour nettoyer les données d’un segment spécifique lors de la réexécution.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-232">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="d9ed9-233">Nom d’une colonne avec le type de données binary(32).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-233">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="d9ed9-234">Non</span><span class="sxs-lookup"><span data-stu-id="d9ed9-234">No</span></span> |

## <a name="json-examples-for-copying-data-to-and-from-oracle-database"></a><span data-ttu-id="d9ed9-235">Exemples JSON pour copier des données vers et depuis une base de données Oracle</span><span class="sxs-lookup"><span data-stu-id="d9ed9-235">JSON examples for copying data to and from Oracle database</span></span>
<span data-ttu-id="d9ed9-236">L’exemple suivant présente des exemples de définitions de JSON que vous pouvez utiliser pour créer un pipeline à l’aide du [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), de [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [d’Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-236">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="d9ed9-237">Ils indiquent comment copier des données entre une base de données Oracle et Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-237">They show how to copy data from/to an Oracle database to/from Azure Blob Storage.</span></span> <span data-ttu-id="d9ed9-238">Toutefois, les données peuvent être copiées vers l’un des récepteurs indiqués [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) , via l’activité de copie d’Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-238">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

## <a name="example-copy-data-from-oracle-to-azure-blob"></a><span data-ttu-id="d9ed9-239">Exemple : copie de données d’Oracle vers Azure Blob</span><span class="sxs-lookup"><span data-stu-id="d9ed9-239">Example: Copy data from Oracle to Azure Blob</span></span>

<span data-ttu-id="d9ed9-240">L’exemple contient les entités de fabrique de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="d9ed9-240">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="d9ed9-241">Un service lié de type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-241">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="d9ed9-242">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-242">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="d9ed9-243">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-243">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="d9ed9-244">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-244">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="d9ed9-245">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) comme source et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) comme récepteur.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-245">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="d9ed9-246">L’exemple copie toutes les heures les données d’une table d’une base de données Oracle locale vers un objet blob.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-246">The sample copies data from a table in an on-premises Oracle database to a blob hourly.</span></span> <span data-ttu-id="d9ed9-247">Pour plus d’informations sur les diverses propriétés utilisées dans l’exemple, consultez la documentation dans les sections qui suivent les exemples.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-247">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="d9ed9-248">**Service lié Oracle :**</span><span class="sxs-lookup"><span data-stu-id="d9ed9-248">**Oracle linked service:**</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="d9ed9-249">**Service lié Azure Blob Storage :**</span><span class="sxs-lookup"><span data-stu-id="d9ed9-249">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="d9ed9-250">**Jeu de données d’entrée Oracle :**</span><span class="sxs-lookup"><span data-stu-id="d9ed9-250">**Oracle input dataset:**</span></span>

<span data-ttu-id="d9ed9-251">L'exemple suppose que vous avez créé une table « MyTable » dans Oracle et qu'elle contient une colonne appelée « timestampcolumn » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-251">The sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="d9ed9-252">La définition de « external » : « true» informe le service Data Factory qu’il s’agit d’un jeu de données qui est externe à Data Factory et non produit par une activité dans Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-252">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2014-02-27T12:00:00",
            "frequency": "Hour"
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

<span data-ttu-id="d9ed9-253">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="d9ed9-253">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="d9ed9-254">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-254">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d9ed9-255">Le nom du chemin d'accès et du fichier de dossier pour l'objet blob sont évalués dynamiquement en fonction de l'heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-255">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="d9ed9-256">Le chemin d'accès du dossier utilise l'année, le mois, le jour et l'heure de l'heure de début.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-256">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="d9ed9-257">**Pipeline avec activité de copie :**</span><span class="sxs-lookup"><span data-stu-id="d9ed9-257">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="d9ed9-258">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d’entrée et de sortie et planifiée pour s’exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-258">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="d9ed9-259">Dans la définition du pipeline JSON, le type **source** est défini sur **OracleSource** et le type **sink** est défini sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-259">In the pipeline JSON definition, the **source** type is set to **OracleSource** and **sink** type is set to **BlobSink**.</span></span>  <span data-ttu-id="d9ed9-260">La requête SQL spécifiée pour la propriété **oracleReaderQuery** sélectionne les données de la dernière heure à copier.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-260">The SQL query specified with **oracleReaderQuery** property selects the data in the past hour to copy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "OracletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": " OracleInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "OracleSource",
                        "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

## <a name="example-copy-data-from-azure-blob-to-oracle"></a><span data-ttu-id="d9ed9-261">Exemple : copie de données à partir d’Azure Blob vers Oracle</span><span class="sxs-lookup"><span data-stu-id="d9ed9-261">Example: Copy data from Azure Blob to Oracle</span></span>
<span data-ttu-id="d9ed9-262">Cet exemple indique comment copier des données d’un stockage d’objets blob Azure vers une base de données Oracle locale.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-262">This sample shows how to copy data from an Azure Blob Storage to an on-premises Oracle database.</span></span> <span data-ttu-id="d9ed9-263">Toutefois, vous pouvez copier les données **directement** à partir des sources indiquées [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats), par le biais de l’activité de copie de Microsoft Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-263">However, data can be copied **directly** from any of the sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="d9ed9-264">L’exemple contient les entités de fabrique de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="d9ed9-264">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="d9ed9-265">Un service lié de type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-265">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="d9ed9-266">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-266">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="d9ed9-267">un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-267">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="d9ed9-268">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-268">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="d9ed9-269">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) comme source et [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) comme récepteur.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-269">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="d9ed9-270">L’exemple copie chaque heure les données d’une objet blob vers une table d’une base de données Oracle locale.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-270">The sample copies data from a blob to a table in an on-premises Oracle database every hour.</span></span> <span data-ttu-id="d9ed9-271">Pour plus d’informations sur les diverses propriétés utilisées dans l’exemple, consultez la documentation dans les sections qui suivent les exemples.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-271">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="d9ed9-272">**Service lié Oracle :**</span><span class="sxs-lookup"><span data-stu-id="d9ed9-272">**Oracle linked service:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
            User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="d9ed9-273">**Service lié Azure Blob Storage :**</span><span class="sxs-lookup"><span data-stu-id="d9ed9-273">**Azure Blob storage linked service:**</span></span>
```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="d9ed9-274">**Jeu de données d'entrée d'objet Blob Azure**</span><span class="sxs-lookup"><span data-stu-id="d9ed9-274">**Azure Blob input dataset**</span></span>

<span data-ttu-id="d9ed9-275">Les données sont récupérées à partir d’un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-275">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d9ed9-276">Le nom du chemin d'accès et du fichier de dossier pour l'objet blob sont évalués dynamiquement en fonction de l'heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-276">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="d9ed9-277">Le chemin d’accès du dossier utilise l’année, le mois et le jour de début et le nom de fichier utilise l’heure de début.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-277">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="d9ed9-278">Le paramètre « external » : « true » informe le service Data Factory que cette table est externe à la fabrique de données et n’est pas produite par une activité dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-278">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
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
            "frequency": "Day",
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

<span data-ttu-id="d9ed9-279">**Jeu de données de sortie Oracle :**</span><span class="sxs-lookup"><span data-stu-id="d9ed9-279">**Oracle output dataset:**</span></span>

<span data-ttu-id="d9ed9-280">L’exemple suppose que vous avez créé une table « MyTable » dans Oracle.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-280">The sample assumes you have created a table “MyTable” in Oracle.</span></span> <span data-ttu-id="d9ed9-281">Créez la table dans Oracle avec le même nombre de colonnes que le fichier CSV d’objets blob doit en contenir.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-281">Create the table in Oracle with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="d9ed9-282">De nouvelles lignes sont ajoutées à la table toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-282">New rows are added to the table every hour.</span></span>

```json
{
    "name": "OracleOutput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Day",
            "interval": "1"
        }
    }
}
```

<span data-ttu-id="d9ed9-283">**Pipeline avec activité de copie :**</span><span class="sxs-lookup"><span data-stu-id="d9ed9-283">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="d9ed9-284">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-284">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="d9ed9-285">Dans la définition du pipeline JSON, le type **source** est défini sur **BlobSource** et le type **sink** est défini sur **OracleSink**.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-285">In the pipeline JSON definition, the **source** type is set to **BlobSource** and the **sink** type is set to **OracleSink**.</span></span>  

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-05T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
            {
                "name": "AzureBlobtoOracle",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "OracleOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "OracleSink"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
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


## <a name="troubleshooting-tips"></a><span data-ttu-id="d9ed9-286">Conseils de dépannage</span><span class="sxs-lookup"><span data-stu-id="d9ed9-286">Troubleshooting tips</span></span>
### <a name="problem-1-net-framework-data-provider"></a><span data-ttu-id="d9ed9-287">Problème 1 : Fournisseur de données .NET Framework</span><span class="sxs-lookup"><span data-stu-id="d9ed9-287">Problem 1: .NET Framework Data Provider</span></span>

<span data-ttu-id="d9ed9-288">Le **message d’erreur** suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="d9ed9-288">You see the following **error message**:</span></span>

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable to find the requested .Net Framework Data Provider. It may not be installed”.  

<span data-ttu-id="d9ed9-289">**Causes possibles :**</span><span class="sxs-lookup"><span data-stu-id="d9ed9-289">**Possible causes:**</span></span>

1. <span data-ttu-id="d9ed9-290">Le fournisseur de données .NET Framework pour Oracle n’a pas été installé.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-290">The .NET Framework Data Provider for Oracle was not installed.</span></span>
2. <span data-ttu-id="d9ed9-291">Le fournisseur de données .NET Framework pour Oracle a été installé pour .NET Framework 2.0 et est introuvable dans les dossiers de .NET Framework 4.0.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-291">The .NET Framework Data Provider for Oracle was installed to .NET Framework 2.0 and is not found in the .NET Framework 4.0 folders.</span></span>

<span data-ttu-id="d9ed9-292">**Résolution/solution de contournement :**</span><span class="sxs-lookup"><span data-stu-id="d9ed9-292">**Resolution/Workaround:**</span></span>

1. <span data-ttu-id="d9ed9-293">Si vous n’avez pas installé le fournisseur .NET pour Oracle, [installez-le](http://www.oracle.com/technetwork/topics/dotnet/downloads/) , puis réessayez.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-293">If you haven't installed the .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry the scenario.</span></span>
2. <span data-ttu-id="d9ed9-294">Si vous obtenez le message d’erreur même après l’installation du fournisseur, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d9ed9-294">If you get the error message even after installing the provider, do the following steps:</span></span>
   1. <span data-ttu-id="d9ed9-295">Ouvrez le fichier machine.config de .NET 2.0 à partir du dossier : <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-295">Open machine config of .NET 2.0 from the folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span></span>
   2. <span data-ttu-id="d9ed9-296">Recherchez **Fournisseur de données Oracle pour .NET**, et vous devriez trouver une entrée comme indiqué dans l’exemple suivant sous **system.data** -> **DbProviderFactories** : <add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Fournisseur de données Oracle pour .NET</span><span class="sxs-lookup"><span data-stu-id="d9ed9-296">Search for **Oracle Data Provider for .NET**, and you should be able to find an entry as shown in the following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span></span>" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" /><span data-ttu-id="d9ed9-297">.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-297">”</span></span>
3. <span data-ttu-id="d9ed9-298">Copiez cette entrée dans le fichier machine.config dans le dossier v4.0 suivant : <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, et remplacez la version par 4.xxx.x.x.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-298">Copy this entry to the machine.config file in the following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change the version to 4.xxx.x.x.</span></span>
4. <span data-ttu-id="d9ed9-299">Installez <Chemin d’installation d’ODP.NET>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll dans le Global Assembly Cache (GAC) en exécutant `gacutil /i [provider path]`.## Conseils de dépannage</span><span class="sxs-lookup"><span data-stu-id="d9ed9-299">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into the global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span></span>

### <a name="problem-2-datetime-formatting"></a><span data-ttu-id="d9ed9-300">Problème 2 : Mise en forme de la date et de l’heure</span><span class="sxs-lookup"><span data-stu-id="d9ed9-300">Problem 2: datetime formatting</span></span>

<span data-ttu-id="d9ed9-301">Le **message d’erreur** suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="d9ed9-301">You see the following **error message**:</span></span>

    Message=Operation failed in Oracle Database with the following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

<span data-ttu-id="d9ed9-302">**Résolution/solution de contournement :**</span><span class="sxs-lookup"><span data-stu-id="d9ed9-302">**Resolution/Workaround:**</span></span>

<span data-ttu-id="d9ed9-303">Vous devrez peut-être ajuster la chaîne de requête dans votre activité de copie en fonction de la manière dont les dates sont configurées dans votre base de données Oracle, comme indiqué dans l’exemple suivant (à l’aide de la fonction to_date) :</span><span class="sxs-lookup"><span data-stu-id="d9ed9-303">You may need to adjust the query string in your copy activity based on how dates are configured in your Oracle database, as shown in the following sample (using the to_date function):</span></span>

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a><span data-ttu-id="d9ed9-304">Mappage de type pour Oracle</span><span class="sxs-lookup"><span data-stu-id="d9ed9-304">Type mapping for Oracle</span></span>
<span data-ttu-id="d9ed9-305">Comme mentionné dans l’article consacré aux [activités de déplacement des données](data-factory-data-movement-activities.md) , l’activité de copie convertit automatiquement les types source en types récepteur à l’aide de l’approche en 2 étapes suivante :</span><span class="sxs-lookup"><span data-stu-id="d9ed9-305">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="d9ed9-306">Conversion de types natifs source en types .NET</span><span class="sxs-lookup"><span data-stu-id="d9ed9-306">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="d9ed9-307">Conversion de types .NET en types récepteur natifs</span><span class="sxs-lookup"><span data-stu-id="d9ed9-307">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="d9ed9-308">Lors du déplacement de données à partir d’Oracle, les mappages suivants sont utilisés pour convertir le type de données Oracle en type .NET et vice versa.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-308">When moving data from Oracle, the following mappings are used from Oracle data type to .NET type and vice versa.</span></span>

| <span data-ttu-id="d9ed9-309">Type de données Oracle</span><span class="sxs-lookup"><span data-stu-id="d9ed9-309">Oracle data type</span></span> | <span data-ttu-id="d9ed9-310">Type de données .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-310">.NET Framework data type</span></span> |
| --- | --- |
| <span data-ttu-id="d9ed9-311">BFILE</span><span class="sxs-lookup"><span data-stu-id="d9ed9-311">BFILE</span></span> |<span data-ttu-id="d9ed9-312">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d9ed9-312">Byte[]</span></span> |
| <span data-ttu-id="d9ed9-313">BLOB</span><span class="sxs-lookup"><span data-stu-id="d9ed9-313">BLOB</span></span> |<span data-ttu-id="d9ed9-314">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d9ed9-314">Byte[]</span></span> |
| <span data-ttu-id="d9ed9-315">CHAR</span><span class="sxs-lookup"><span data-stu-id="d9ed9-315">CHAR</span></span> |<span data-ttu-id="d9ed9-316">String</span><span class="sxs-lookup"><span data-stu-id="d9ed9-316">String</span></span> |
| <span data-ttu-id="d9ed9-317">CLOB</span><span class="sxs-lookup"><span data-stu-id="d9ed9-317">CLOB</span></span> |<span data-ttu-id="d9ed9-318">String</span><span class="sxs-lookup"><span data-stu-id="d9ed9-318">String</span></span> |
| <span data-ttu-id="d9ed9-319">DATE</span><span class="sxs-lookup"><span data-stu-id="d9ed9-319">DATE</span></span> |<span data-ttu-id="d9ed9-320">DateTime</span><span class="sxs-lookup"><span data-stu-id="d9ed9-320">DateTime</span></span> |
| <span data-ttu-id="d9ed9-321">FLOAT</span><span class="sxs-lookup"><span data-stu-id="d9ed9-321">FLOAT</span></span> |<span data-ttu-id="d9ed9-322">Décimale, chaîne (si précision > 28)</span><span class="sxs-lookup"><span data-stu-id="d9ed9-322">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="d9ed9-323">INTEGER</span><span class="sxs-lookup"><span data-stu-id="d9ed9-323">INTEGER</span></span> |<span data-ttu-id="d9ed9-324">Décimale, chaîne (si précision > 28)</span><span class="sxs-lookup"><span data-stu-id="d9ed9-324">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="d9ed9-325">INTERVAL YEAR TO MONTH</span><span class="sxs-lookup"><span data-stu-id="d9ed9-325">INTERVAL YEAR TO MONTH</span></span> |<span data-ttu-id="d9ed9-326">Int32</span><span class="sxs-lookup"><span data-stu-id="d9ed9-326">Int32</span></span> |
| <span data-ttu-id="d9ed9-327">INTERVAL DAY TO SECOND</span><span class="sxs-lookup"><span data-stu-id="d9ed9-327">INTERVAL DAY TO SECOND</span></span> |<span data-ttu-id="d9ed9-328">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="d9ed9-328">TimeSpan</span></span> |
| <span data-ttu-id="d9ed9-329">LONG</span><span class="sxs-lookup"><span data-stu-id="d9ed9-329">LONG</span></span> |<span data-ttu-id="d9ed9-330">String</span><span class="sxs-lookup"><span data-stu-id="d9ed9-330">String</span></span> |
| <span data-ttu-id="d9ed9-331">LONG RAW</span><span class="sxs-lookup"><span data-stu-id="d9ed9-331">LONG RAW</span></span> |<span data-ttu-id="d9ed9-332">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d9ed9-332">Byte[]</span></span> |
| <span data-ttu-id="d9ed9-333">NCHAR</span><span class="sxs-lookup"><span data-stu-id="d9ed9-333">NCHAR</span></span> |<span data-ttu-id="d9ed9-334">String</span><span class="sxs-lookup"><span data-stu-id="d9ed9-334">String</span></span> |
| <span data-ttu-id="d9ed9-335">NCLOB</span><span class="sxs-lookup"><span data-stu-id="d9ed9-335">NCLOB</span></span> |<span data-ttu-id="d9ed9-336">String</span><span class="sxs-lookup"><span data-stu-id="d9ed9-336">String</span></span> |
| <span data-ttu-id="d9ed9-337">NUMBER</span><span class="sxs-lookup"><span data-stu-id="d9ed9-337">NUMBER</span></span> |<span data-ttu-id="d9ed9-338">Décimale, chaîne (si précision > 28)</span><span class="sxs-lookup"><span data-stu-id="d9ed9-338">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="d9ed9-339">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="d9ed9-339">NVARCHAR2</span></span> |<span data-ttu-id="d9ed9-340">String</span><span class="sxs-lookup"><span data-stu-id="d9ed9-340">String</span></span> |
| <span data-ttu-id="d9ed9-341">RAW</span><span class="sxs-lookup"><span data-stu-id="d9ed9-341">RAW</span></span> |<span data-ttu-id="d9ed9-342">Byte[]</span><span class="sxs-lookup"><span data-stu-id="d9ed9-342">Byte[]</span></span> |
| <span data-ttu-id="d9ed9-343">ROWID</span><span class="sxs-lookup"><span data-stu-id="d9ed9-343">ROWID</span></span> |<span data-ttu-id="d9ed9-344">String</span><span class="sxs-lookup"><span data-stu-id="d9ed9-344">String</span></span> |
| <span data-ttu-id="d9ed9-345">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="d9ed9-345">TIMESTAMP</span></span> |<span data-ttu-id="d9ed9-346">DateTime</span><span class="sxs-lookup"><span data-stu-id="d9ed9-346">DateTime</span></span> |
| <span data-ttu-id="d9ed9-347">TIMESTAMP WITH LOCAL TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="d9ed9-347">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="d9ed9-348">DateTime</span><span class="sxs-lookup"><span data-stu-id="d9ed9-348">DateTime</span></span> |
| <span data-ttu-id="d9ed9-349">TIMESTAMP WITH TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="d9ed9-349">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="d9ed9-350">DateTime</span><span class="sxs-lookup"><span data-stu-id="d9ed9-350">DateTime</span></span> |
| <span data-ttu-id="d9ed9-351">UNSIGNED INTEGER</span><span class="sxs-lookup"><span data-stu-id="d9ed9-351">UNSIGNED INTEGER</span></span> |<span data-ttu-id="d9ed9-352">NUMBER</span><span class="sxs-lookup"><span data-stu-id="d9ed9-352">Number</span></span> |
| <span data-ttu-id="d9ed9-353">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="d9ed9-353">VARCHAR2</span></span> |<span data-ttu-id="d9ed9-354">String</span><span class="sxs-lookup"><span data-stu-id="d9ed9-354">String</span></span> |
| <span data-ttu-id="d9ed9-355">XML</span><span class="sxs-lookup"><span data-stu-id="d9ed9-355">XML</span></span> |<span data-ttu-id="d9ed9-356">String</span><span class="sxs-lookup"><span data-stu-id="d9ed9-356">String</span></span> |

> [!NOTE]
> <span data-ttu-id="d9ed9-357">Les types de données **INTERVAL YEAR TO MONTH** et **INTERVAL DAY TO SECOND** ne sont pas pris en charge lors de l’utilisation du pilote Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-357">Data type **INTERVAL YEAR TO MONTH** and **INTERVAL DAY TO SECOND** are not supported when using Microsoft driver.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="d9ed9-358">Mapper les colonnes source aux colonnes de récepteur</span><span class="sxs-lookup"><span data-stu-id="d9ed9-358">Map source to sink columns</span></span>
<span data-ttu-id="d9ed9-359">Pour en savoir plus sur le mappage de colonnes du jeu de données source à des colonnes du jeu de données récepteur, voir [Mappage des colonnes d’un jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-359">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="d9ed9-360">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="d9ed9-360">Repeatable read from relational sources</span></span>
<span data-ttu-id="d9ed9-361">Lorsque vous copiez des données à partir de magasins de données relationnels, gardez à l’esprit la répétabilité de l’opération, afin d’éviter des résultats imprévus.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-361">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="d9ed9-362">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-362">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="d9ed9-363">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-363">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="d9ed9-364">Lorsqu’une tranche est réexécutée d’une manière ou d’une autre, vous devez vous assurer que les mêmes données sont lues et ce, quel que soit le nombre d’exécutions de la tranche.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-364">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="d9ed9-365">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="d9ed9-365">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="d9ed9-366">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="d9ed9-366">Performance and Tuning</span></span>
<span data-ttu-id="d9ed9-367">Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="d9ed9-367">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
