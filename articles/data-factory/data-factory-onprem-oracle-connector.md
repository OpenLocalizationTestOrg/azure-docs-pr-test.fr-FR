---
title: "les données d’aaaCopy vers/à partir d’Oracle à l’aide de la fabrique de données | Documents Microsoft"
description: "Découvrez comment toocopy des données vers/à partir d’une base de données Oracle qui est local à l’aide d’Azure Data Factory."
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
ms.openlocfilehash: adb6d5fbe38e18791616ac77e8179970bbea37fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a><span data-ttu-id="69994-103">Copier des données vers/à partir d’Oracle en local à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="69994-103">Copy data to/from on-premises Oracle using Azure Data Factory</span></span>
<span data-ttu-id="69994-104">Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory vers/à partir d’une base de données Oracle locale.</span><span class="sxs-lookup"><span data-stu-id="69994-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from an on-premises Oracle database.</span></span> <span data-ttu-id="69994-105">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="69994-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="69994-106">Scénarios pris en charge</span><span class="sxs-lookup"><span data-stu-id="69994-106">Supported scenarios</span></span>
<span data-ttu-id="69994-107">Vous pouvez copier des données **à partir d’une base de données Oracle** toohello suivant des magasins de données :</span><span class="sxs-lookup"><span data-stu-id="69994-107">You can copy data **from an Oracle database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="69994-108">Vous pouvez copier des données à partir de hello suivant des magasins de données **base de données Oracle tooan**:</span><span class="sxs-lookup"><span data-stu-id="69994-108">You can copy data from hello following data stores **tooan Oracle database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a><span data-ttu-id="69994-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="69994-109">Prerequisites</span></span>
<span data-ttu-id="69994-110">Fabrique de données prend en charge des sources de Oracle tooon local qui se connecte à l’aide de la passerelle de gestion des données de hello.</span><span class="sxs-lookup"><span data-stu-id="69994-110">Data Factory supports connecting tooon-premises Oracle sources using hello Data Management Gateway.</span></span> <span data-ttu-id="69994-111">Consultez [passerelle de gestion des données](data-factory-data-management-gateway.md) toolearn l’article sur la passerelle de gestion des données et [déplacer des données locales toocloud](data-factory-move-data-between-onprem-and-cloud.md) article pour obtenir des instructions sur la configuration de passerelle de hello un pipeline de données toomove des données.</span><span class="sxs-lookup"><span data-stu-id="69994-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article toolearn about Data Management Gateway and [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

<span data-ttu-id="69994-112">Passerelle est requise même si Oracle hello est hébergé dans une machine virtuelle IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="69994-112">Gateway is required even if hello Oracle is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="69994-113">Vous pouvez installer la passerelle de hello sur hello même IaaS VM sous forme de données de hello stocker ou sur un ordinateur différent virtuel tant que passerelle de hello peuvent se connecter toohello de base de données.</span><span class="sxs-lookup"><span data-stu-id="69994-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="69994-114">Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.</span><span class="sxs-lookup"><span data-stu-id="69994-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="69994-115">Versions prises en charge et installation</span><span class="sxs-lookup"><span data-stu-id="69994-115">Supported versions and installation</span></span>
<span data-ttu-id="69994-116">Ce connecteur Oracle prend en charge deux versions de pilotes :</span><span class="sxs-lookup"><span data-stu-id="69994-116">This Oracle connector support two versions of drivers:</span></span>

- <span data-ttu-id="69994-117">**Pilote Microsoft pour Oracle (recommandé)**: à partir de la passerelle de gestion des données de la version 2.7, un pilote Microsoft pour Oracle est installé automatiquement en même temps que la passerelle de hello, par conséquent, vous n’avez pas besoin handle tooadditionally pilote hello tooestablish connectivité tooOracle et vous pouvez également bénéficier de meilleures performances de copie à l’aide de ce pilote.</span><span class="sxs-lookup"><span data-stu-id="69994-117">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with hello gateway, so you don't need tooadditionally handle hello driver in order tooestablish connectivity tooOracle, and you can also experience better copy performance using this driver.</span></span> <span data-ttu-id="69994-118">Voici les versions de bases de données Oracle prises en charge :</span><span class="sxs-lookup"><span data-stu-id="69994-118">Below versions of Oracle databases are supported:</span></span>
    - <span data-ttu-id="69994-119">Oracle 12c R1 (12.1)</span><span class="sxs-lookup"><span data-stu-id="69994-119">Oracle 12c R1 (12.1)</span></span>
    - <span data-ttu-id="69994-120">Oracle 11g R1, R2 (11.1, 11.2)</span><span class="sxs-lookup"><span data-stu-id="69994-120">Oracle 11g R1, R2 (11.1, 11.2)</span></span>
    - <span data-ttu-id="69994-121">Oracle 10g R1, R2 (10.1, 10.2)</span><span class="sxs-lookup"><span data-stu-id="69994-121">Oracle 10g R1, R2 (10.1, 10.2)</span></span>
    - <span data-ttu-id="69994-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span><span class="sxs-lookup"><span data-stu-id="69994-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span></span>
    - <span data-ttu-id="69994-123">Oracle 8i R3 (8.1.7)</span><span class="sxs-lookup"><span data-stu-id="69994-123">Oracle 8i R3 (8.1.7)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="69994-124">Pilote Microsoft pour Oracle seulement prend en charge copie de données à partir d’Oracle, mais n’écrit ne pas tooOracle.</span><span class="sxs-lookup"><span data-stu-id="69994-124">Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing tooOracle.</span></span> <span data-ttu-id="69994-125">Et la fonctionnalité de connexion de test de hello Remarque dans l’onglet Diagnostics de passerelle de gestion de données ne prend pas en charge ce pilote.</span><span class="sxs-lookup"><span data-stu-id="69994-125">And note hello test connection capability in Data Management Gateway Diagnostics tab does not support this driver.</span></span> <span data-ttu-id="69994-126">Vous pouvez également utiliser connectivité de hello copie Assistant toovalidate hello.</span><span class="sxs-lookup"><span data-stu-id="69994-126">Alternatively, you can use hello copy wizard toovalidate hello connectivity.</span></span>
>

- <span data-ttu-id="69994-127">**Le fournisseur de données Oracle pour .NET :** vous pouvez également choisir les données de toocopy toouse fournisseur de données Oracle à partir de / tooOracle.</span><span class="sxs-lookup"><span data-stu-id="69994-127">**Oracle Data Provider for .NET:** you can also choose toouse Oracle Data Provider toocopy data from/tooOracle.</span></span> <span data-ttu-id="69994-128">Ce composant est inclus dans [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span><span class="sxs-lookup"><span data-stu-id="69994-128">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span></span> <span data-ttu-id="69994-129">Installer la version appropriée de hello (32/64 bits) sur l’ordinateur hello où hello gateway est installé.</span><span class="sxs-lookup"><span data-stu-id="69994-129">Install hello appropriate version (32/64 bit) on hello machine where hello gateway is installed.</span></span> <span data-ttu-id="69994-130">[Fournisseur de données Oracle .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) accessible tooOracle 10 g version 2 ou version ultérieure de la base de données.</span><span class="sxs-lookup"><span data-stu-id="69994-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access tooOracle Database 10g Release 2 or later.</span></span>

    <span data-ttu-id="69994-131">Si vous choisissez « Installation XCopy », suivez les étapes de hello readme.htm.</span><span class="sxs-lookup"><span data-stu-id="69994-131">If you choose “XCopy Installation”, follow steps in hello readme.htm.</span></span> <span data-ttu-id="69994-132">Nous vous recommandons de que choisir de programme d’installation de hello avec une interface utilisateur (non-XCopy une).</span><span class="sxs-lookup"><span data-stu-id="69994-132">We recommend you choose hello installer with UI (non-XCopy one).</span></span>

    <span data-ttu-id="69994-133">Après avoir installé le fournisseur de hello, **redémarrer** hello service hôte de passerelle de gestion des données sur votre ordinateur à l’aide des Services applet (ou) Gestionnaire de Configuration de passerelle de gestion de données.</span><span class="sxs-lookup"><span data-stu-id="69994-133">After installing hello provider, **restart** hello Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span></span>  

<span data-ttu-id="69994-134">Si vous utilisez le pipeline de copie copie Assistant tooauthor hello, hello pilote sera déterminé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="69994-134">If you use copy wizard tooauthor hello copy pipeline, hello driver type will be auto-determined.</span></span> <span data-ttu-id="69994-135">Le pilote Microsoft est utilisé par défaut, sauf la version de votre passerelle est antérieure à 2.7 ou si vous choisissez Oracle comme récepteur.</span><span class="sxs-lookup"><span data-stu-id="69994-135">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span></span>

## <a name="getting-started"></a><span data-ttu-id="69994-136">Prise en main</span><span class="sxs-lookup"><span data-stu-id="69994-136">Getting started</span></span>
<span data-ttu-id="69994-137">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers/depuis une base de données Oracle locale à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="69994-137">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span></span>

<span data-ttu-id="69994-138">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="69994-138">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="69994-139">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="69994-139">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="69994-140">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="69994-140">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="69994-141">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="69994-141">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="69994-142">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="69994-142">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="69994-143">Création d'une **fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="69994-143">Create a **data factory**.</span></span> <span data-ttu-id="69994-144">Une fabrique de données peut contenir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="69994-144">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="69994-145">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="69994-145">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="69994-146">Par exemple, si vous copiez des données à partir d’un tooan de base de données Oralce stockage d’objets blob Azure, vous créez deux services liés toolink votre base de données Oracle et de la fabrique de données de stockage Azure compte tooyour.</span><span class="sxs-lookup"><span data-stu-id="69994-146">For example, if you are copying data from an Oralce database tooan Azure blob storage, you create two linked services toolink your Oracle database and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="69994-147">Pour les propriétés de service lié sont tooOracle spécifique, consultez [lié des propriétés du service](#linked-service-properties) section.</span><span class="sxs-lookup"><span data-stu-id="69994-147">For linked service properties that are specific tooOracle, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="69994-148">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="69994-148">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="69994-149">Dans l’exemple hello mentionné dans la dernière étape de hello, vous créer une table de hello toospecify jeu de données dans votre base de données Oracle qui contient les données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="69994-149">In hello example mentioned in hello last step, you create a dataset toospecify hello table in your Oracle database that contains hello input data.</span></span> <span data-ttu-id="69994-150">Vous créez un autre conteneur d’objets blob dataset toospecify hello et dossier hello qui contient les données de salutation provenant de base de données Oracle hello.</span><span class="sxs-lookup"><span data-stu-id="69994-150">And, you create another dataset toospecify hello blob container and hello folder that holds hello data copied from hello Oracle database.</span></span> <span data-ttu-id="69994-151">Pour les propriétés du dataset qui sont tooOracle spécifique, consultez [propriétés du dataset](#dataset-properties) section.</span><span class="sxs-lookup"><span data-stu-id="69994-151">For dataset properties that are specific tooOracle, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="69994-152">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="69994-152">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="69994-153">Dans l’exemple hello mentionné précédemment, vous utilisez OracleSource en tant que source et BlobSink comme un récepteur pour l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="69994-153">In hello example mentioned earlier, you use OracleSource as a source and BlobSink as a sink for hello copy activity.</span></span> <span data-ttu-id="69994-154">De même, si vous copiez à partir du stockage d’objets Blob Azure tooOracle de base de données, vous utilisez BlobSource et OracleSink dans l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="69994-154">Similarly, if you are copying from Azure Blob Storage tooOracle Database, you use BlobSource and OracleSink in hello copy activity.</span></span> <span data-ttu-id="69994-155">Pour les propriétés d’activité de copie sont tooOracle spécifique de base de données, consultez [copier les propriétés de l’activité](#copy-activity-properties) section.</span><span class="sxs-lookup"><span data-stu-id="69994-155">For copy activity properties that are specific tooOracle database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="69994-156">Pour plus d’informations sur comment toouse du magasin de données source ou un récepteur, cliquez sur le lien hello dans la section précédente de hello pour votre magasin de données.</span><span class="sxs-lookup"><span data-stu-id="69994-156">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span> 

<span data-ttu-id="69994-157">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="69994-157">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="69994-158">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="69994-158">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="69994-159">Pour plus d’exemples de définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données vers/à partir d’une base de données Oracle locale, consultez [exemples JSON](#json-examples-for-copying-data-to-and-from-oracle-database) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="69994-159">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an on-premises Oracle database, see [JSON examples](#json-examples-for-copying-data-to-and-from-oracle-database) section of this article.</span></span>

<span data-ttu-id="69994-160">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont des entités de fabrique de données toodefine utilisé :</span><span class="sxs-lookup"><span data-stu-id="69994-160">hello following sections provide details about JSON properties that are used toodefine Data Factory entities:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="69994-161">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="69994-161">Linked service properties</span></span>
<span data-ttu-id="69994-162">Hello tableau suivant fournit la description du service de tooOracle spécifique lié éléments JSON.</span><span class="sxs-lookup"><span data-stu-id="69994-162">hello following table provides description for JSON elements specific tooOracle linked service.</span></span>

| <span data-ttu-id="69994-163">Propriété</span><span class="sxs-lookup"><span data-stu-id="69994-163">Property</span></span> | <span data-ttu-id="69994-164">Description</span><span class="sxs-lookup"><span data-stu-id="69994-164">Description</span></span> | <span data-ttu-id="69994-165">Requis</span><span class="sxs-lookup"><span data-stu-id="69994-165">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="69994-166">type</span><span class="sxs-lookup"><span data-stu-id="69994-166">type</span></span> |<span data-ttu-id="69994-167">propriété de type Hello doit indiquer : **OnPremisesOracle**</span><span class="sxs-lookup"><span data-stu-id="69994-167">hello type property must be set to: **OnPremisesOracle**</span></span> |<span data-ttu-id="69994-168">Oui</span><span class="sxs-lookup"><span data-stu-id="69994-168">Yes</span></span> |
| <span data-ttu-id="69994-169">driverType</span><span class="sxs-lookup"><span data-stu-id="69994-169">driverType</span></span> | <span data-ttu-id="69994-170">Spécifier les données de toocopy toouse pilote à partir de / tooOracle de base de données.</span><span class="sxs-lookup"><span data-stu-id="69994-170">Specify which driver toouse toocopy data from/tooOracle Database.</span></span> <span data-ttu-id="69994-171">Valeurs autorisées : **Microsoft** ou **ODP** (par défaut).</span><span class="sxs-lookup"><span data-stu-id="69994-171">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="69994-172">Consultez la section [Version prise en charge et installation](#supported-versions-and-installation) sur les détails du pilote.</span><span class="sxs-lookup"><span data-stu-id="69994-172">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="69994-173">Non</span><span class="sxs-lookup"><span data-stu-id="69994-173">No</span></span> |
| <span data-ttu-id="69994-174">connectionString</span><span class="sxs-lookup"><span data-stu-id="69994-174">connectionString</span></span> | <span data-ttu-id="69994-175">Spécifiez les informations nécessaires d’instance de base de données Oracle tooconnect toohello pour la propriété connectionString de hello.</span><span class="sxs-lookup"><span data-stu-id="69994-175">Specify information needed tooconnect toohello Oracle Database instance for hello connectionString property.</span></span> | <span data-ttu-id="69994-176">Oui</span><span class="sxs-lookup"><span data-stu-id="69994-176">Yes</span></span> |
| <span data-ttu-id="69994-177">gatewayName</span><span class="sxs-lookup"><span data-stu-id="69994-177">gatewayName</span></span> | <span data-ttu-id="69994-178">Nom de la passerelle hello qui est utilisé tooconnect toohello serveur Oracle locale</span><span class="sxs-lookup"><span data-stu-id="69994-178">Name of hello gateway that that is used tooconnect toohello on-premises Oracle server</span></span> |<span data-ttu-id="69994-179">Oui</span><span class="sxs-lookup"><span data-stu-id="69994-179">Yes</span></span> |

<span data-ttu-id="69994-180">**Exemple : avec le pilote Microsoft**</span><span class="sxs-lookup"><span data-stu-id="69994-180">**Example: using Microsoft driver:**</span></span>
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

<span data-ttu-id="69994-181">**Exemple : avec le pilote ODP**</span><span class="sxs-lookup"><span data-stu-id="69994-181">**Example: using ODP driver**</span></span>

<span data-ttu-id="69994-182">Consultez trop[ce site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) pour hello formats autorisé.</span><span class="sxs-lookup"><span data-stu-id="69994-182">Refer too[this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for hello allowed formats.</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="69994-183">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="69994-183">Dataset properties</span></span>
<span data-ttu-id="69994-184">Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="69994-184">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="69994-185">Les sections telles que la structure, la disponibilité et la stratégie d’un jeu de données JSON sont similaires pour tous les types de jeux de données (Oracle, objet blob Azure, table Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="69994-185">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="69994-186">section de typeProperties Hello est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="69994-186">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="69994-187">section de typeProperties Hello pour hello le jeu de données de type OracleTable a hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="69994-187">hello typeProperties section for hello dataset of type OracleTable has hello following properties:</span></span>

| <span data-ttu-id="69994-188">Propriété</span><span class="sxs-lookup"><span data-stu-id="69994-188">Property</span></span> | <span data-ttu-id="69994-189">Description</span><span class="sxs-lookup"><span data-stu-id="69994-189">Description</span></span> | <span data-ttu-id="69994-190">Requis</span><span class="sxs-lookup"><span data-stu-id="69994-190">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="69994-191">TableName</span><span class="sxs-lookup"><span data-stu-id="69994-191">tableName</span></span> |<span data-ttu-id="69994-192">Nom de table hello Bonjour base de données Oracle hello service lié fait référence à.</span><span class="sxs-lookup"><span data-stu-id="69994-192">Name of hello table in hello Oracle Database that hello linked service refers to.</span></span> |<span data-ttu-id="69994-193">Non (si **oracleReaderQuery** de **OracleSource** est spécifié)</span><span class="sxs-lookup"><span data-stu-id="69994-193">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="69994-194">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="69994-194">Copy activity properties</span></span>
<span data-ttu-id="69994-195">Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="69994-195">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="69994-196">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="69994-196">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="69994-197">Hello activité de copie accepte uniquement une entrée et produit qu’une seule sortie.</span><span class="sxs-lookup"><span data-stu-id="69994-197">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="69994-198">Alors que les propriétés disponibles dans la section typeProperties hello activité hello varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="69994-198">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="69994-199">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="69994-199">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="oraclesource"></a><span data-ttu-id="69994-200">OracleSource</span><span class="sxs-lookup"><span data-stu-id="69994-200">OracleSource</span></span>
<span data-ttu-id="69994-201">Dans l’activité de copie, lors de la source de hello est de type **OracleSource** hello propriétés suivantes est disponible dans **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="69994-201">In Copy activity, when hello source is of type **OracleSource** hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="69994-202">Propriété</span><span class="sxs-lookup"><span data-stu-id="69994-202">Property</span></span> | <span data-ttu-id="69994-203">Description</span><span class="sxs-lookup"><span data-stu-id="69994-203">Description</span></span> | <span data-ttu-id="69994-204">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="69994-204">Allowed values</span></span> | <span data-ttu-id="69994-205">Requis</span><span class="sxs-lookup"><span data-stu-id="69994-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="69994-206">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="69994-206">oracleReaderQuery</span></span> |<span data-ttu-id="69994-207">Utiliser des données tooread hello requête personnalisée.</span><span class="sxs-lookup"><span data-stu-id="69994-207">Use hello custom query tooread data.</span></span> |<span data-ttu-id="69994-208">Chaîne de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="69994-208">SQL query string.</span></span> <span data-ttu-id="69994-209">Par exemple : select * from MyTable</span><span class="sxs-lookup"><span data-stu-id="69994-209">For example: select * from MyTable</span></span> <br/><br/><span data-ttu-id="69994-210">Si non spécifié, hello instruction SQL exécutée : sélectionnez * dans MaTable</span><span class="sxs-lookup"><span data-stu-id="69994-210">If not specified, hello SQL statement that is executed: select * from MyTable</span></span> |<span data-ttu-id="69994-211">Non (si **tableName** de **dataset** est spécifiée)</span><span class="sxs-lookup"><span data-stu-id="69994-211">No (if **tableName** of **dataset** is specified)</span></span> |

### <a name="oraclesink"></a><span data-ttu-id="69994-212">OracleSink</span><span class="sxs-lookup"><span data-stu-id="69994-212">OracleSink</span></span>
<span data-ttu-id="69994-213">**OracleSink** prend en charge hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="69994-213">**OracleSink** supports hello following properties:</span></span>

| <span data-ttu-id="69994-214">Propriété</span><span class="sxs-lookup"><span data-stu-id="69994-214">Property</span></span> | <span data-ttu-id="69994-215">Description</span><span class="sxs-lookup"><span data-stu-id="69994-215">Description</span></span> | <span data-ttu-id="69994-216">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="69994-216">Allowed values</span></span> | <span data-ttu-id="69994-217">Requis</span><span class="sxs-lookup"><span data-stu-id="69994-217">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="69994-218">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="69994-218">writeBatchTimeout</span></span> |<span data-ttu-id="69994-219">Temps d’attente pour hello lot insert opération toocomplete avant d’expirer.</span><span class="sxs-lookup"><span data-stu-id="69994-219">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="69994-220">intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="69994-220">timespan</span></span><br/><br/> <span data-ttu-id="69994-221">Exemple : « 00:30:00 » (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="69994-221">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="69994-222">Non</span><span class="sxs-lookup"><span data-stu-id="69994-222">No</span></span> |
| <span data-ttu-id="69994-223">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="69994-223">writeBatchSize</span></span> |<span data-ttu-id="69994-224">Insère des données dans une table SQL de hello lorsque la taille de mémoire tampon de hello atteint la valeur writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="69994-224">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="69994-225">Nombre entier (nombre de lignes)</span><span class="sxs-lookup"><span data-stu-id="69994-225">Integer (number of rows)</span></span> |<span data-ttu-id="69994-226">Non (valeur par défaut : 100)</span><span class="sxs-lookup"><span data-stu-id="69994-226">No (default: 100)</span></span> |
| <span data-ttu-id="69994-227">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="69994-227">sqlWriterCleanupScript</span></span> |<span data-ttu-id="69994-228">Spécifier une requête pour l’activité de copie tooexecute telles que les données d’un secteur spécifique sont nettoyées.</span><span class="sxs-lookup"><span data-stu-id="69994-228">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="69994-229">Une instruction de requête.</span><span class="sxs-lookup"><span data-stu-id="69994-229">A query statement.</span></span> |<span data-ttu-id="69994-230">Non</span><span class="sxs-lookup"><span data-stu-id="69994-230">No</span></span> |
| <span data-ttu-id="69994-231">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="69994-231">sliceIdentifierColumnName</span></span> |<span data-ttu-id="69994-232">Spécifiez nom de colonne pour l’activité de copie toofill avec l’identificateur de secteur généré automatiquement, qui est utilisé tooclean des données d’un secteur spécifique quand réexécutée.</span><span class="sxs-lookup"><span data-stu-id="69994-232">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="69994-233">Nom d’une colonne avec le type de données binary(32).</span><span class="sxs-lookup"><span data-stu-id="69994-233">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="69994-234">Non</span><span class="sxs-lookup"><span data-stu-id="69994-234">No</span></span> |

## <a name="json-examples-for-copying-data-tooand-from-oracle-database"></a><span data-ttu-id="69994-235">Exemples JSON pour la copie des données tooand à partir de la base de données Oracle</span><span class="sxs-lookup"><span data-stu-id="69994-235">JSON examples for copying data tooand from Oracle database</span></span>
<span data-ttu-id="69994-236">Hello exemple suivant fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="69994-236">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="69994-237">Elles montrent comment toocopy des données à partir de / tooan Oracle database vers/depuis le stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="69994-237">They show how toocopy data from/tooan Oracle database to/from Azure Blob Storage.</span></span> <span data-ttu-id="69994-238">Toutefois, les données peuvent être copié tooany de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="69994-238">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

## <a name="example-copy-data-from-oracle-tooazure-blob"></a><span data-ttu-id="69994-239">Exemple : Copier des données à partir d’Oracle tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="69994-239">Example: Copy data from Oracle tooAzure Blob</span></span>

<span data-ttu-id="69994-240">exemple Hello a hello suivant des entités de fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="69994-240">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="69994-241">Un service lié de type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="69994-241">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="69994-242">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="69994-242">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="69994-243">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="69994-243">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="69994-244">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="69994-244">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="69994-245">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) comme source et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) comme récepteur.</span><span class="sxs-lookup"><span data-stu-id="69994-245">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="69994-246">exemple Hello copie toutes les heures des données à partir d’une table dans un blob de tooa de base de données Oracle locale.</span><span class="sxs-lookup"><span data-stu-id="69994-246">hello sample copies data from a table in an on-premises Oracle database tooa blob hourly.</span></span> <span data-ttu-id="69994-247">Pour plus d’informations sur les diverses propriétés utilisées dans l’exemple hello, consultez la documentation dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="69994-247">For more information on various properties used in hello sample, see documentation in sections following hello samples.</span></span>

<span data-ttu-id="69994-248">**Service lié Oracle :**</span><span class="sxs-lookup"><span data-stu-id="69994-248">**Oracle linked service:**</span></span>

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

<span data-ttu-id="69994-249">**Service lié Azure Blob Storage :**</span><span class="sxs-lookup"><span data-stu-id="69994-249">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="69994-250">**Jeu de données d’entrée Oracle :**</span><span class="sxs-lookup"><span data-stu-id="69994-250">**Oracle input dataset:**</span></span>

<span data-ttu-id="69994-251">exemple Hello suppose que vous avez créé une table « MyTable » dans Oracle, et il contienne une colonne appelée « timestampcolumn » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="69994-251">hello sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="69994-252">Paramètre « external » : « true » informe service Data Factory de hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="69994-252">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="69994-253">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="69994-253">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="69994-254">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="69994-254">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="69994-255">nom de chemin d’accès et de dossier pour l’objet blob de hello Hello sont dynamiquement évaluées en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="69994-255">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="69994-256">chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="69994-256">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="69994-257">**Pipeline avec activité de copie :**</span><span class="sxs-lookup"><span data-stu-id="69994-257">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="69994-258">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="69994-258">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="69994-259">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**OracleSource** et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="69994-259">In hello pipeline JSON definition, hello **source** type is set too**OracleSource** and **sink** type is set too**BlobSink**.</span></span>  <span data-ttu-id="69994-260">spécifié avec la requête SQL Hello **oracleReaderQuery** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.</span><span class="sxs-lookup"><span data-stu-id="69994-260">hello SQL query specified with **oracleReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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

## <a name="example-copy-data-from-azure-blob-toooracle"></a><span data-ttu-id="69994-261">Exemple : Copier des données d’objets Blob Azure tooOracle</span><span class="sxs-lookup"><span data-stu-id="69994-261">Example: Copy data from Azure Blob tooOracle</span></span>
<span data-ttu-id="69994-262">Cet exemple montre comment toocopy les données à partir d’un tooan de stockage d’objets Blob Azure en local de la base de données Oracle.</span><span class="sxs-lookup"><span data-stu-id="69994-262">This sample shows how toocopy data from an Azure Blob Storage tooan on-premises Oracle database.</span></span> <span data-ttu-id="69994-263">Toutefois, les données peuvent être copiées **directement** à partir des sources de hello indiqués [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="69994-263">However, data can be copied **directly** from any of hello sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="69994-264">exemple Hello a hello suivant des entités de fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="69994-264">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="69994-265">Un service lié de type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="69994-265">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="69994-266">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="69994-266">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="69994-267">un [jeu de données](data-factory-create-datasets.md) d'entrée de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="69994-267">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="69994-268">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="69994-268">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="69994-269">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) comme source et [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) comme récepteur.</span><span class="sxs-lookup"><span data-stu-id="69994-269">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="69994-270">exemple Hello copie des données à partir d’une table de tooa d’objets blob dans une base de données Oracle locale toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="69994-270">hello sample copies data from a blob tooa table in an on-premises Oracle database every hour.</span></span> <span data-ttu-id="69994-271">Pour plus d’informations sur les diverses propriétés utilisées dans l’exemple hello, consultez la documentation dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="69994-271">For more information on various properties used in hello sample, see documentation in sections following hello samples.</span></span>

<span data-ttu-id="69994-272">**Service lié Oracle :**</span><span class="sxs-lookup"><span data-stu-id="69994-272">**Oracle linked service:**</span></span>
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

<span data-ttu-id="69994-273">**Service lié Azure Blob Storage :**</span><span class="sxs-lookup"><span data-stu-id="69994-273">**Azure Blob storage linked service:**</span></span>
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

<span data-ttu-id="69994-274">**Jeu de données d'entrée d'objet Blob Azure**</span><span class="sxs-lookup"><span data-stu-id="69994-274">**Azure Blob input dataset**</span></span>

<span data-ttu-id="69994-275">Les données sont récupérées à partir d'un nouvel objet Blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="69994-275">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="69994-276">nom de chemin d’accès et de dossier pour l’objet blob de hello Hello sont dynamiquement évaluées en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="69994-276">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="69994-277">chemin d’accès du dossier Hello utilise la partie jour de l’heure de début hello, mois et année et nom de fichier partie d’heure hello de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="69994-277">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="69994-278">« external » : « true » paramètre informe le service Data Factory de hello que cette table est la fabrique de données externe toohello et qu’il n’est pas générée par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="69994-278">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="69994-279">**Jeu de données de sortie Oracle :**</span><span class="sxs-lookup"><span data-stu-id="69994-279">**Oracle output dataset:**</span></span>

<span data-ttu-id="69994-280">exemple Hello suppose que vous avez créé une table « MaTable » dans Oracle.</span><span class="sxs-lookup"><span data-stu-id="69994-280">hello sample assumes you have created a table “MyTable” in Oracle.</span></span> <span data-ttu-id="69994-281">Créer la table de hello dans Oracle avec hello même nombre de colonnes comme vous le souhaitez toocontain de fichier CSV d’objets Blob hello.</span><span class="sxs-lookup"><span data-stu-id="69994-281">Create hello table in Oracle with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="69994-282">Nouvelles lignes sont ajoutées à la table de toohello toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="69994-282">New rows are added toohello table every hour.</span></span>

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

<span data-ttu-id="69994-283">**Pipeline avec activité de copie :**</span><span class="sxs-lookup"><span data-stu-id="69994-283">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="69994-284">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="69994-284">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="69994-285">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**BlobSource** et hello **récepteur** type est défini trop**OracleSink**.</span><span class="sxs-lookup"><span data-stu-id="69994-285">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and hello **sink** type is set too**OracleSink**.</span></span>  

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


## <a name="troubleshooting-tips"></a><span data-ttu-id="69994-286">Conseils de dépannage</span><span class="sxs-lookup"><span data-stu-id="69994-286">Troubleshooting tips</span></span>
### <a name="problem-1-net-framework-data-provider"></a><span data-ttu-id="69994-287">Problème 1 : Fournisseur de données .NET Framework</span><span class="sxs-lookup"><span data-stu-id="69994-287">Problem 1: .NET Framework Data Provider</span></span>

<span data-ttu-id="69994-288">Hello suivante **message d’erreur**:</span><span class="sxs-lookup"><span data-stu-id="69994-288">You see hello following **error message**:</span></span>

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable toofind hello requested .Net Framework Data Provider. It may not be installed”.  

<span data-ttu-id="69994-289">**Causes possibles :**</span><span class="sxs-lookup"><span data-stu-id="69994-289">**Possible causes:**</span></span>

1. <span data-ttu-id="69994-290">Hello, fournisseur de données .NET Framework pour Oracle n’a pas été installé.</span><span class="sxs-lookup"><span data-stu-id="69994-290">hello .NET Framework Data Provider for Oracle was not installed.</span></span>
2. <span data-ttu-id="69994-291">Hello, fournisseur de données .NET Framework pour Oracle a été installé too.NET Framework 2.0 et est introuvable dans les dossiers hello .NET Framework 4.0.</span><span class="sxs-lookup"><span data-stu-id="69994-291">hello .NET Framework Data Provider for Oracle was installed too.NET Framework 2.0 and is not found in hello .NET Framework 4.0 folders.</span></span>

<span data-ttu-id="69994-292">**Résolution/solution de contournement :**</span><span class="sxs-lookup"><span data-stu-id="69994-292">**Resolution/Workaround:**</span></span>

1. <span data-ttu-id="69994-293">Si vous n’avez pas installé hello fournisseur .NET pour Oracle, [installer](http://www.oracle.com/technetwork/topics/dotnet/downloads/) et recommencez le scénario de hello.</span><span class="sxs-lookup"><span data-stu-id="69994-293">If you haven't installed hello .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry hello scenario.</span></span>
2. <span data-ttu-id="69994-294">Si vous obtenez un message d’erreur hello même après l’installation du fournisseur de hello, procédez comme hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="69994-294">If you get hello error message even after installing hello provider, do hello following steps:</span></span>
   1. <span data-ttu-id="69994-295">Ouvrir la configuration de la machine de .NET 2.0 à partir du dossier hello : <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span><span class="sxs-lookup"><span data-stu-id="69994-295">Open machine config of .NET 2.0 from hello folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span></span>
   2. <span data-ttu-id="69994-296">Recherchez **le fournisseur de données Oracle pour .NET**, et vous devez être en mesure de toofind une entrée comme indiqué dans hello suivant l’exemple sous **system.data** -> **DbProviderFactories**: «<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Du fournisseur de données oracle pour .NET</span><span class="sxs-lookup"><span data-stu-id="69994-296">Search for **Oracle Data Provider for .NET**, and you should be able toofind an entry as shown in hello following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span></span>" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" /><span data-ttu-id="69994-297">.</span><span class="sxs-lookup"><span data-stu-id="69994-297">”</span></span>
3. <span data-ttu-id="69994-298">Copiez ce fichier machine.config de toohello entrée Bonjour suivant v4.0 dossier : <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config et modification hello version too4.xxx.x.x.</span><span class="sxs-lookup"><span data-stu-id="69994-298">Copy this entry toohello machine.config file in hello following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change hello version too4.xxx.x.x.</span></span>
4. <span data-ttu-id="69994-299">Installez « < chemin d’accès ODP.NET installé > \11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll » dans hello global assembly cache (GAC) en exécutant `gacutil /i [provider path]`. ## des conseils de dépannage</span><span class="sxs-lookup"><span data-stu-id="69994-299">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into hello global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span></span>

### <a name="problem-2-datetime-formatting"></a><span data-ttu-id="69994-300">Problème 2 : Mise en forme de la date et de l’heure</span><span class="sxs-lookup"><span data-stu-id="69994-300">Problem 2: datetime formatting</span></span>

<span data-ttu-id="69994-301">Hello suivante **message d’erreur**:</span><span class="sxs-lookup"><span data-stu-id="69994-301">You see hello following **error message**:</span></span>

    Message=Operation failed in Oracle Database with hello following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

<span data-ttu-id="69994-302">**Résolution/solution de contournement :**</span><span class="sxs-lookup"><span data-stu-id="69994-302">**Resolution/Workaround:**</span></span>

<span data-ttu-id="69994-303">Vous devrez peut-être la chaîne de requête tooadjust hello dans votre activité de copie basée sur la façon dont les dates sont configurés dans votre base de données Oracle, comme indiqué dans les éléments suivants de hello exemple (à l’aide de la fonction to_date hello) :</span><span class="sxs-lookup"><span data-stu-id="69994-303">You may need tooadjust hello query string in your copy activity based on how dates are configured in your Oracle database, as shown in hello following sample (using hello to_date function):</span></span>

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a><span data-ttu-id="69994-304">Mappage de type pour Oracle</span><span class="sxs-lookup"><span data-stu-id="69994-304">Type mapping for Oracle</span></span>
<span data-ttu-id="69994-305">Comme mentionné dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) activité de copie de l’article effectue des conversions de type automatique à partir de types de sources de toosink types avec hello approche de l’étape 2 :</span><span class="sxs-lookup"><span data-stu-id="69994-305">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="69994-306">Convertir à partir de la source native types too.NET type</span><span class="sxs-lookup"><span data-stu-id="69994-306">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="69994-307">Conversion de type de récepteur de toonative de type .NET</span><span class="sxs-lookup"><span data-stu-id="69994-307">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="69994-308">Lors du déplacement des données à partir d’Oracle, hello suivant les mappages est utilisé à partir du type too.NET de type de données Oracle et vice versa.</span><span class="sxs-lookup"><span data-stu-id="69994-308">When moving data from Oracle, hello following mappings are used from Oracle data type too.NET type and vice versa.</span></span>

| <span data-ttu-id="69994-309">Type de données Oracle</span><span class="sxs-lookup"><span data-stu-id="69994-309">Oracle data type</span></span> | <span data-ttu-id="69994-310">Type de données .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="69994-310">.NET Framework data type</span></span> |
| --- | --- |
| <span data-ttu-id="69994-311">BFILE</span><span class="sxs-lookup"><span data-stu-id="69994-311">BFILE</span></span> |<span data-ttu-id="69994-312">Byte[]</span><span class="sxs-lookup"><span data-stu-id="69994-312">Byte[]</span></span> |
| <span data-ttu-id="69994-313">BLOB</span><span class="sxs-lookup"><span data-stu-id="69994-313">BLOB</span></span> |<span data-ttu-id="69994-314">Byte[]</span><span class="sxs-lookup"><span data-stu-id="69994-314">Byte[]</span></span> |
| <span data-ttu-id="69994-315">CHAR</span><span class="sxs-lookup"><span data-stu-id="69994-315">CHAR</span></span> |<span data-ttu-id="69994-316">String</span><span class="sxs-lookup"><span data-stu-id="69994-316">String</span></span> |
| <span data-ttu-id="69994-317">CLOB</span><span class="sxs-lookup"><span data-stu-id="69994-317">CLOB</span></span> |<span data-ttu-id="69994-318">String</span><span class="sxs-lookup"><span data-stu-id="69994-318">String</span></span> |
| <span data-ttu-id="69994-319">DATE</span><span class="sxs-lookup"><span data-stu-id="69994-319">DATE</span></span> |<span data-ttu-id="69994-320">DateTime</span><span class="sxs-lookup"><span data-stu-id="69994-320">DateTime</span></span> |
| <span data-ttu-id="69994-321">FLOAT</span><span class="sxs-lookup"><span data-stu-id="69994-321">FLOAT</span></span> |<span data-ttu-id="69994-322">Décimale, chaîne (si précision > 28)</span><span class="sxs-lookup"><span data-stu-id="69994-322">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="69994-323">INTEGER</span><span class="sxs-lookup"><span data-stu-id="69994-323">INTEGER</span></span> |<span data-ttu-id="69994-324">Décimale, chaîne (si précision > 28)</span><span class="sxs-lookup"><span data-stu-id="69994-324">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="69994-325">INTERVALLE année tooMONTH</span><span class="sxs-lookup"><span data-stu-id="69994-325">INTERVAL YEAR tooMONTH</span></span> |<span data-ttu-id="69994-326">Int32</span><span class="sxs-lookup"><span data-stu-id="69994-326">Int32</span></span> |
| <span data-ttu-id="69994-327">INTERVALLE jour tooSECOND</span><span class="sxs-lookup"><span data-stu-id="69994-327">INTERVAL DAY tooSECOND</span></span> |<span data-ttu-id="69994-328">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="69994-328">TimeSpan</span></span> |
| <span data-ttu-id="69994-329">LONG</span><span class="sxs-lookup"><span data-stu-id="69994-329">LONG</span></span> |<span data-ttu-id="69994-330">String</span><span class="sxs-lookup"><span data-stu-id="69994-330">String</span></span> |
| <span data-ttu-id="69994-331">LONG RAW</span><span class="sxs-lookup"><span data-stu-id="69994-331">LONG RAW</span></span> |<span data-ttu-id="69994-332">Byte[]</span><span class="sxs-lookup"><span data-stu-id="69994-332">Byte[]</span></span> |
| <span data-ttu-id="69994-333">NCHAR</span><span class="sxs-lookup"><span data-stu-id="69994-333">NCHAR</span></span> |<span data-ttu-id="69994-334">String</span><span class="sxs-lookup"><span data-stu-id="69994-334">String</span></span> |
| <span data-ttu-id="69994-335">NCLOB</span><span class="sxs-lookup"><span data-stu-id="69994-335">NCLOB</span></span> |<span data-ttu-id="69994-336">String</span><span class="sxs-lookup"><span data-stu-id="69994-336">String</span></span> |
| <span data-ttu-id="69994-337">NUMBER</span><span class="sxs-lookup"><span data-stu-id="69994-337">NUMBER</span></span> |<span data-ttu-id="69994-338">Décimale, chaîne (si précision > 28)</span><span class="sxs-lookup"><span data-stu-id="69994-338">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="69994-339">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="69994-339">NVARCHAR2</span></span> |<span data-ttu-id="69994-340">String</span><span class="sxs-lookup"><span data-stu-id="69994-340">String</span></span> |
| <span data-ttu-id="69994-341">RAW</span><span class="sxs-lookup"><span data-stu-id="69994-341">RAW</span></span> |<span data-ttu-id="69994-342">Byte[]</span><span class="sxs-lookup"><span data-stu-id="69994-342">Byte[]</span></span> |
| <span data-ttu-id="69994-343">ROWID</span><span class="sxs-lookup"><span data-stu-id="69994-343">ROWID</span></span> |<span data-ttu-id="69994-344">String</span><span class="sxs-lookup"><span data-stu-id="69994-344">String</span></span> |
| <span data-ttu-id="69994-345">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="69994-345">TIMESTAMP</span></span> |<span data-ttu-id="69994-346">DateTime</span><span class="sxs-lookup"><span data-stu-id="69994-346">DateTime</span></span> |
| <span data-ttu-id="69994-347">TIMESTAMP WITH LOCAL TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="69994-347">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="69994-348">DateTime</span><span class="sxs-lookup"><span data-stu-id="69994-348">DateTime</span></span> |
| <span data-ttu-id="69994-349">TIMESTAMP WITH TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="69994-349">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="69994-350">DateTime</span><span class="sxs-lookup"><span data-stu-id="69994-350">DateTime</span></span> |
| <span data-ttu-id="69994-351">UNSIGNED INTEGER</span><span class="sxs-lookup"><span data-stu-id="69994-351">UNSIGNED INTEGER</span></span> |<span data-ttu-id="69994-352">NUMBER</span><span class="sxs-lookup"><span data-stu-id="69994-352">Number</span></span> |
| <span data-ttu-id="69994-353">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="69994-353">VARCHAR2</span></span> |<span data-ttu-id="69994-354">String</span><span class="sxs-lookup"><span data-stu-id="69994-354">String</span></span> |
| <span data-ttu-id="69994-355">XML</span><span class="sxs-lookup"><span data-stu-id="69994-355">XML</span></span> |<span data-ttu-id="69994-356">String</span><span class="sxs-lookup"><span data-stu-id="69994-356">String</span></span> |

> [!NOTE]
> <span data-ttu-id="69994-357">Type de données **intervalle année tooMONTH** et **INTERVAL DAY tooSECOND** ne sont pas pris en charge lors de l’utilisation du pilote Microsoft.</span><span class="sxs-lookup"><span data-stu-id="69994-357">Data type **INTERVAL YEAR tooMONTH** and **INTERVAL DAY tooSECOND** are not supported when using Microsoft driver.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="69994-358">Mapper les colonnes de source toosink</span><span class="sxs-lookup"><span data-stu-id="69994-358">Map source toosink columns</span></span>
<span data-ttu-id="69994-359">toolearn sur le mappage des colonnes dans toocolumns du jeu de données source dans le jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="69994-359">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="69994-360">Lecture renouvelée de sources relationnelles</span><span class="sxs-lookup"><span data-stu-id="69994-360">Repeatable read from relational sources</span></span>
<span data-ttu-id="69994-361">Lors de la copie des données à partir de banques de données relationnelles, conserver la répétabilité dans l’esprit tooavoid des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="69994-361">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="69994-362">Dans Azure Data Factory, vous pouvez réexécuter une tranche manuellement.</span><span class="sxs-lookup"><span data-stu-id="69994-362">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="69994-363">Vous pouvez également configurer une stratégie de nouvelles tentatives pour un jeu de données, afin qu’une tranche soit réexécutée en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="69994-363">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="69994-364">Lorsqu’une tranche est exécuté à nouveau dans les deux cas, vous devez toomake vraiment qui hello des mêmes données n’est en lecture aucune question comment plusieurs fois une tranche est exécutée.</span><span class="sxs-lookup"><span data-stu-id="69994-364">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="69994-365">Voir [Lecture renouvelée de sources relationnelles](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="69994-365">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="69994-366">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="69994-366">Performance and Tuning</span></span>
<span data-ttu-id="69994-367">Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="69994-367">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
