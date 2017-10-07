---
title: "données aaaCopy vers/depuis un système de fichiers à l’aide d’Azure Data Factory | Documents Microsoft"
description: "Découvrez comment tooand de données toocopy à partir d’un système de fichiers local à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a><span data-ttu-id="f5d43-103">Copier des données tooand à partir d’un système de fichiers local à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f5d43-103">Copy data tooand from an on-premises file system by using Azure Data Factory</span></span>
<span data-ttu-id="f5d43-104">Cet article explique comment toouse hello activité de copie de données de toocopy Azure Data Factory vers/à partir d’un système de fichiers local.</span><span class="sxs-lookup"><span data-stu-id="f5d43-104">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data to/from an on-premises file system.</span></span> <span data-ttu-id="f5d43-105">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="f5d43-106">Scénarios pris en charge</span><span class="sxs-lookup"><span data-stu-id="f5d43-106">Supported scenarios</span></span>
<span data-ttu-id="f5d43-107">Vous pouvez copier des données **à partir d’un système de fichiers local** toohello suivant des magasins de données :</span><span class="sxs-lookup"><span data-stu-id="f5d43-107">You can copy data **from an on-premises file system** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="f5d43-108">Vous pouvez copier des données à partir de hello suivant des magasins de données **tooan local système de fichiers**:</span><span class="sxs-lookup"><span data-stu-id="f5d43-108">You can copy data from hello following data stores **tooan on-premises file system**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="f5d43-109">Activité de copie ne supprime pas le fichier de source de hello lorsqu’elle est correctement copié toohello destination.</span><span class="sxs-lookup"><span data-stu-id="f5d43-109">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="f5d43-110">Si vous avez besoin de fichier de source de hello toodelete après la copie a réussi, créer un fichier de hello toodelete activité personnalisée et utiliser l’activité hello dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-110">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="f5d43-111">Activation de la connectivité</span><span class="sxs-lookup"><span data-stu-id="f5d43-111">Enabling connectivity</span></span>
<span data-ttu-id="f5d43-112">Fabrique de données prend en charge la connexion tooand à partir d’un système de fichiers local via **passerelle de gestion des données**.</span><span class="sxs-lookup"><span data-stu-id="f5d43-112">Data Factory supports connecting tooand from an on-premises file system via **Data Management Gateway**.</span></span> <span data-ttu-id="f5d43-113">Vous devez installer hello passerelle de gestion des données dans votre environnement local pour hello Data Factory service tooconnect tooany locale prise en charge banque de données, y compris le système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="f5d43-113">You must install hello Data Management Gateway in your on-premises environment for hello Data Factory service tooconnect tooany supported on-premises data store including file system.</span></span> <span data-ttu-id="f5d43-114">toolearn sur la passerelle de gestion des données et pour obtenir des instructions sur la configuration de passerelle de hello, consultez [déplacement des données entre des sources locales et cloud hello avec la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="f5d43-114">toolearn about Data Management Gateway and for step-by-step instructions on setting up hello gateway, see [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="f5d43-115">En dehors de la passerelle de gestion des données, aucun autre fichier binaire ne devez tooand de toocommunicate toobe installé à partir d’un système de fichiers local.</span><span class="sxs-lookup"><span data-stu-id="f5d43-115">Apart from Data Management Gateway, no other binary files need toobe installed toocommunicate tooand from an on-premises file system.</span></span> <span data-ttu-id="f5d43-116">Vous devez installer et utiliser hello passerelle de gestion des données, même si le système de fichiers hello est dans une machine virtuelle IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="f5d43-116">You must install and use hello Data Management Gateway even if hello file system is in Azure IaaS VM.</span></span> <span data-ttu-id="f5d43-117">Pour plus d’informations sur la passerelle de hello, consultez [passerelle de gestion des données](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="f5d43-117">For detailed information about hello gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="f5d43-118">toouse un partage de fichiers Linux, installer [Samba](https://www.samba.org/) sur votre serveur Linux et installez passerelle de gestion des données sur un serveur Windows.</span><span class="sxs-lookup"><span data-stu-id="f5d43-118">toouse a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span></span> <span data-ttu-id="f5d43-119">L’installation de la passerelle de gestion des données sur un serveur Linux n'est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="f5d43-119">Installing Data Management Gateway on a Linux server is not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f5d43-120">Prise en main</span><span class="sxs-lookup"><span data-stu-id="f5d43-120">Getting started</span></span>
<span data-ttu-id="f5d43-121">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers/depuis un système de fichiers à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="f5d43-121">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span></span>

<span data-ttu-id="f5d43-122">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="f5d43-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="f5d43-123">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="f5d43-124">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="f5d43-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="f5d43-125">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="f5d43-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="f5d43-126">Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :</span><span class="sxs-lookup"><span data-stu-id="f5d43-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="f5d43-127">Création d'une **fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="f5d43-127">Create a **data factory**.</span></span> <span data-ttu-id="f5d43-128">Une fabrique de données peut contenir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="f5d43-128">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="f5d43-129">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="f5d43-129">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="f5d43-130">Par exemple, si vous copiez des données à partir d’un système de fichiers local tooan Azure blob storage, vous créez deux services liés toolink votre système de fichiers local et la fabrique de données de stockage Azure compte tooyour.</span><span class="sxs-lookup"><span data-stu-id="f5d43-130">For example, if you are copying data from an Azure blob storage tooan on-premises file system, you create two linked services toolink your on-premises file system and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="f5d43-131">Pour les propriétés de service lié qui sont le système de fichiers local tooan spécifiques, consultez [lié des propriétés du service](#linked-service-properties) section.</span><span class="sxs-lookup"><span data-stu-id="f5d43-131">For linked service properties that are specific tooan on-premises file system, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="f5d43-132">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="f5d43-133">Exemple hello mentionné dans la dernière étape de hello, vous permet de créer un conteneur d’objets blob de jeu de données toospecify hello et un dossier qui contient les données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-133">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="f5d43-134">De plus, vous créez un autre jeu de données toospecify hello dossier et le nom (facultatif) dans votre système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="f5d43-134">And, you create another dataset toospecify hello folder and file name (optional) in your file system.</span></span> <span data-ttu-id="f5d43-135">Pour le système de fichiers de propriétés du dataset qui sont spécifiques tooon locaux, consultez [propriétés du dataset](#dataset-properties) section.</span><span class="sxs-lookup"><span data-stu-id="f5d43-135">For dataset properties that are specific tooon-premises file system, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="f5d43-136">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="f5d43-136">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="f5d43-137">Dans l’exemple hello mentionné précédemment, vous utilisez BlobSource en tant que source et FileSystemSink comme un récepteur pour l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-137">In hello example mentioned earlier, you use BlobSource as a source and FileSystemSink as a sink for hello copy activity.</span></span> <span data-ttu-id="f5d43-138">De même, si vous copiez à partir de tooAzure de système de fichiers local stockage d’objets Blob, vous utilisez FileSystemSource et BlobSink dans l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-138">Similarly, if you are copying from on-premises file system tooAzure Blob Storage, you use FileSystemSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="f5d43-139">Pour le système de fichiers de propriétés de l’activité copie tooon-site spécifique, consultez [copier les propriétés de l’activité](#copy-activity-properties) section.</span><span class="sxs-lookup"><span data-stu-id="f5d43-139">For copy activity properties that are specific tooon-premises file system, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="f5d43-140">Pour plus d’informations sur comment toouse du magasin de données source ou un récepteur, cliquez sur le lien hello dans la section précédente de hello pour votre magasin de données.</span><span class="sxs-lookup"><span data-stu-id="f5d43-140">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="f5d43-141">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="f5d43-141">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="f5d43-142">Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-142">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="f5d43-143">Pour plus d’exemples de définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données vers/depuis un système de fichiers, consultez [exemples JSON](#json-examples-for-copying-data-to-and-from-file-system) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="f5d43-143">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from a file system, see [JSON examples](#json-examples-for-copying-data-to-and-from-file-system) section of this article.</span></span>

<span data-ttu-id="f5d43-144">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifiques toofile système :</span><span class="sxs-lookup"><span data-stu-id="f5d43-144">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific toofile system:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="f5d43-145">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="f5d43-145">Linked service properties</span></span>
<span data-ttu-id="f5d43-146">Vous pouvez lier une fabrique de données Azure local fichier système tooan avec hello **serveur de fichiers local** service lié.</span><span class="sxs-lookup"><span data-stu-id="f5d43-146">You can link an on-premises file system tooan Azure data factory with hello **On-Premises File Server** linked service.</span></span> <span data-ttu-id="f5d43-147">Hello tableau suivant fournit des descriptions pour les éléments JSON qui sont spécifique toohello service serveur de fichiers local lié.</span><span class="sxs-lookup"><span data-stu-id="f5d43-147">hello following table provides descriptions for JSON elements that are specific toohello On-Premises File Server linked service.</span></span>

| <span data-ttu-id="f5d43-148">Propriété</span><span class="sxs-lookup"><span data-stu-id="f5d43-148">Property</span></span> | <span data-ttu-id="f5d43-149">Description</span><span class="sxs-lookup"><span data-stu-id="f5d43-149">Description</span></span> | <span data-ttu-id="f5d43-150">Requis</span><span class="sxs-lookup"><span data-stu-id="f5d43-150">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5d43-151">type</span><span class="sxs-lookup"><span data-stu-id="f5d43-151">type</span></span> |<span data-ttu-id="f5d43-152">Assurez-vous que les propriétés de type hello sont définie trop**OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="f5d43-152">Ensure that hello type property is set too**OnPremisesFileServer**.</span></span> |<span data-ttu-id="f5d43-153">Oui</span><span class="sxs-lookup"><span data-stu-id="f5d43-153">Yes</span></span> |
| <span data-ttu-id="f5d43-154">host</span><span class="sxs-lookup"><span data-stu-id="f5d43-154">host</span></span> |<span data-ttu-id="f5d43-155">Spécifie le chemin d’accès racine de hello du dossier hello que vous souhaitez toocopy.</span><span class="sxs-lookup"><span data-stu-id="f5d43-155">Specifies hello root path of hello folder that you want toocopy.</span></span> <span data-ttu-id="f5d43-156">Utilisez le caractère d’échappement de hello ' \ ' pour les caractères spéciaux dans la chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-156">Use hello escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="f5d43-157">Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples.</span><span class="sxs-lookup"><span data-stu-id="f5d43-157">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="f5d43-158">Oui</span><span class="sxs-lookup"><span data-stu-id="f5d43-158">Yes</span></span> |
| <span data-ttu-id="f5d43-159">userId</span><span class="sxs-lookup"><span data-stu-id="f5d43-159">userid</span></span> |<span data-ttu-id="f5d43-160">Spécifiez des ID de hello de serveur d’accès toohello utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-160">Specify hello ID of hello user who has access toohello server.</span></span> |<span data-ttu-id="f5d43-161">Non (si vous choisissez encryptedcredential)</span><span class="sxs-lookup"><span data-stu-id="f5d43-161">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="f5d43-162">password</span><span class="sxs-lookup"><span data-stu-id="f5d43-162">password</span></span> |<span data-ttu-id="f5d43-163">Spécifiez le mot de passe hello pour hello (userid).</span><span class="sxs-lookup"><span data-stu-id="f5d43-163">Specify hello password for hello user (userid).</span></span> |<span data-ttu-id="f5d43-164">Non (si vous choisissez encryptedcredential)</span><span class="sxs-lookup"><span data-stu-id="f5d43-164">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="f5d43-165">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="f5d43-165">encryptedCredential</span></span> |<span data-ttu-id="f5d43-166">Spécifiez les informations d’identification de hello chiffré que vous pouvez obtenir en exécutant l’applet de commande New-AzureRmDataFactoryEncryptValue de hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-166">Specify hello encrypted credentials that you can get by running hello New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="f5d43-167">Non (si vous choisissez toospecify nom d’utilisateur et mot de passe en texte brut)</span><span class="sxs-lookup"><span data-stu-id="f5d43-167">No (if you choose toospecify userid and password in plain text)</span></span> |
| <span data-ttu-id="f5d43-168">gatewayName</span><span class="sxs-lookup"><span data-stu-id="f5d43-168">gatewayName</span></span> |<span data-ttu-id="f5d43-169">Spécifie le nom hello de passerelle hello que Data Factory doit utiliser de serveur de fichiers local tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-169">Specifies hello name of hello gateway that Data Factory should use tooconnect toohello on-premises file server.</span></span> |<span data-ttu-id="f5d43-170">Oui</span><span class="sxs-lookup"><span data-stu-id="f5d43-170">Yes</span></span> |


### <a name="sample-linked-service-and-dataset-definitions"></a><span data-ttu-id="f5d43-171">Exemples de définitions de jeux de données et de service liés</span><span class="sxs-lookup"><span data-stu-id="f5d43-171">Sample linked service and dataset definitions</span></span>
| <span data-ttu-id="f5d43-172">Scénario</span><span class="sxs-lookup"><span data-stu-id="f5d43-172">Scenario</span></span> | <span data-ttu-id="f5d43-173">Hôte dans la définition du service lié</span><span class="sxs-lookup"><span data-stu-id="f5d43-173">Host in linked service definition</span></span> | <span data-ttu-id="f5d43-174">folderPath dans la définition du jeu de données</span><span class="sxs-lookup"><span data-stu-id="f5d43-174">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5d43-175">Dossier local sur l’ordinateur passerelle de gestion des données : </span><span class="sxs-lookup"><span data-stu-id="f5d43-175">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="f5d43-176">Exemples : D:\\\* ou D:\dossier\sous-dossier\\*</span><span class="sxs-lookup"><span data-stu-id="f5d43-176">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="f5d43-177">D:\\\\ (pour la passerelle de gestion des données 2.0 et versions ultérieures)</span><span class="sxs-lookup"><span data-stu-id="f5d43-177">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="f5d43-178">hôte local (pour les versions de la passerelle de gestion des données antérieures à 2.0)</span><span class="sxs-lookup"><span data-stu-id="f5d43-178">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="f5d43-179">.\\\\ ou dossier\\\\sous-dossier (pour la passerelle de gestion des données 2.0 et versions ultérieures)</span><span class="sxs-lookup"><span data-stu-id="f5d43-179">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="f5d43-180">D:\\\\ ou D:\\\\dossier\\\\sous-dossier (pour les versions de la passerelle antérieures à 2.0)</span><span class="sxs-lookup"><span data-stu-id="f5d43-180">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="f5d43-181">Dossier partagé distant : </span><span class="sxs-lookup"><span data-stu-id="f5d43-181">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="f5d43-182">Exemples : \\\\myserver\\share\\\* ou \\\\myserver\\share\\dossier\\sous-dossier\\*</span><span class="sxs-lookup"><span data-stu-id="f5d43-182">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="f5d43-183">\\\\\\\\myserver\\\\share</span><span class="sxs-lookup"><span data-stu-id="f5d43-183">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="f5d43-184">.\\\\ ou dossier\\\\sous-dossier</span><span class="sxs-lookup"><span data-stu-id="f5d43-184">.\\\\ or folder\\\\subfolder</span></span> |


### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="f5d43-185">Exemple : utilisation d’un nom d'utilisateur et d’un mot de passe en texte brut</span><span class="sxs-lookup"><span data-stu-id="f5d43-185">Example: Using username and password in plain text</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a><span data-ttu-id="f5d43-186">Exemple : utilisation de l’élément encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="f5d43-186">Example: Using encryptedcredential</span></span>

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="f5d43-187">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="f5d43-187">Dataset properties</span></span>
<span data-ttu-id="f5d43-188">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="f5d43-188">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="f5d43-189">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données.</span><span class="sxs-lookup"><span data-stu-id="f5d43-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="f5d43-190">section de typeProperties Hello est différente pour chaque type de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="f5d43-190">hello typeProperties section is different for each type of dataset.</span></span> <span data-ttu-id="f5d43-191">Il fournit des informations telles que l’emplacement de hello et le format de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-191">It provides information such as hello location and format of hello data in hello data store.</span></span> <span data-ttu-id="f5d43-192">section hello le jeu de données de type Hello typeProperties **le partage de fichiers** a hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="f5d43-192">hello typeProperties section for hello dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="f5d43-193">Propriété</span><span class="sxs-lookup"><span data-stu-id="f5d43-193">Property</span></span> | <span data-ttu-id="f5d43-194">Description</span><span class="sxs-lookup"><span data-stu-id="f5d43-194">Description</span></span> | <span data-ttu-id="f5d43-195">Requis</span><span class="sxs-lookup"><span data-stu-id="f5d43-195">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5d43-196">folderPath</span><span class="sxs-lookup"><span data-stu-id="f5d43-196">folderPath</span></span> |<span data-ttu-id="f5d43-197">Spécifie le dossier de toohello sous-chemin hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-197">Specifies hello subpath toohello folder.</span></span> <span data-ttu-id="f5d43-198">Utilisez le caractère d’échappement de hello ' \' pour les caractères spéciaux dans la chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-198">Use hello escape character ‘\’ for special characters in hello string.</span></span> <span data-ttu-id="f5d43-199">Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples.</span><span class="sxs-lookup"><span data-stu-id="f5d43-199">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="f5d43-200">Vous pouvez combiner cette propriété avec **partitionBy** toohave chemins d’accès basés sur un secteur de début et date et l’heure de fin.</span><span class="sxs-lookup"><span data-stu-id="f5d43-200">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="f5d43-201">Oui</span><span class="sxs-lookup"><span data-stu-id="f5d43-201">Yes</span></span> |
| <span data-ttu-id="f5d43-202">fileName</span><span class="sxs-lookup"><span data-stu-id="f5d43-202">fileName</span></span> |<span data-ttu-id="f5d43-203">Spécifiez le nom hello du fichier de hello Bonjour **folderPath** si vous souhaitez hello table toorefer tooa fichier spécifique dans le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-203">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="f5d43-204">Si vous ne spécifiez pas de valeur pour cette propriété, la table de hello pointe tooall des fichiers dans le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-204">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="f5d43-205">Lorsque **nom de fichier** n’est pas spécifié pour un dataset de sortie et **preserveHierarchy** n’est pas spécifié dans récepteur d’activité, hello nom hello généré est Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="f5d43-205">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="f5d43-206">`Data.<Guid>.txt` (Exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="f5d43-206">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="f5d43-207">Non</span><span class="sxs-lookup"><span data-stu-id="f5d43-207">No</span></span> |
| <span data-ttu-id="f5d43-208">fileFilter</span><span class="sxs-lookup"><span data-stu-id="f5d43-208">fileFilter</span></span> |<span data-ttu-id="f5d43-209">Spécifier qu'un filtre toobe utilisé tooselect un sous-ensemble de fichiers dans hello folderPath plutôt que tous les fichiers.</span><span class="sxs-lookup"><span data-stu-id="f5d43-209">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="f5d43-210">Les valeurs autorisées sont : `*` (plusieurs caractères) et `?` (caractère unique).</span><span class="sxs-lookup"><span data-stu-id="f5d43-210">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="f5d43-211">Exemple 1 : « fileFilter » : « *.log »</span><span class="sxs-lookup"><span data-stu-id="f5d43-211">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="f5d43-212">Exemple 2 : « fileFilter » : « 2014-1-?.txt »</span><span class="sxs-lookup"><span data-stu-id="f5d43-212">Example 2: "fileFilter": 2014-1-?.txt"</span></span><br/><br/><span data-ttu-id="f5d43-213">Remarque : fileFilter s’applique à un jeu de données FileShare d’entrée.</span><span class="sxs-lookup"><span data-stu-id="f5d43-213">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="f5d43-214">Non</span><span class="sxs-lookup"><span data-stu-id="f5d43-214">No</span></span> |
| <span data-ttu-id="f5d43-215">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="f5d43-215">partitionedBy</span></span> |<span data-ttu-id="f5d43-216">Vous pouvez utiliser partitionedBy toospecify folderPath/nom de fichier dynamique pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="f5d43-216">You can use partitionedBy toospecify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="f5d43-217">Par exemple, folderPath peut être paramétré pour toutes les heures de données.</span><span class="sxs-lookup"><span data-stu-id="f5d43-217">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="f5d43-218">Non</span><span class="sxs-lookup"><span data-stu-id="f5d43-218">No</span></span> |
| <span data-ttu-id="f5d43-219">format</span><span class="sxs-lookup"><span data-stu-id="f5d43-219">format</span></span> | <span data-ttu-id="f5d43-220">Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="f5d43-220">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="f5d43-221">Ensemble hello **type** propriété sous tooone de format de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="f5d43-221">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="f5d43-222">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="f5d43-222">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="f5d43-223">Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="f5d43-223">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="f5d43-224">Non</span><span class="sxs-lookup"><span data-stu-id="f5d43-224">No</span></span> |
| <span data-ttu-id="f5d43-225">compression</span><span class="sxs-lookup"><span data-stu-id="f5d43-225">compression</span></span> | <span data-ttu-id="f5d43-226">Spécifiez le type de hello et le niveau de compression pour les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="f5d43-226">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="f5d43-227">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="f5d43-227">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="f5d43-228">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="f5d43-228">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="f5d43-229">consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="f5d43-229">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="f5d43-230">Non</span><span class="sxs-lookup"><span data-stu-id="f5d43-230">No</span></span> |

> [!NOTE]
> <span data-ttu-id="f5d43-231">Vous ne pouvez pas utiliser fileName et fileFilter simultanément.</span><span class="sxs-lookup"><span data-stu-id="f5d43-231">You cannot use fileName and fileFilter simultaneously.</span></span>

### <a name="using-partitionedby-property"></a><span data-ttu-id="f5d43-232">Utilisation de la propriété partitionedBy</span><span class="sxs-lookup"><span data-stu-id="f5d43-232">Using partitionedBy property</span></span>
<span data-ttu-id="f5d43-233">Comme indiqué dans la section précédente de hello, vous pouvez spécifier un folderPath dynamique et le nom de fichier de données de série chronologique par hello **partitionedBy** propriété, [fonctions de la fabrique de données et les variables système hello](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="f5d43-233">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="f5d43-234">toounderstand plus d’informations sur les jeux de données de série chronologique, en planifiant et secteurs, consultez [création de datasets](data-factory-create-datasets.md), [de planification et de l’exécution](data-factory-scheduling-and-execution.md), et [création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="f5d43-234">toounderstand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="f5d43-235">Exemple 1 :</span><span class="sxs-lookup"><span data-stu-id="f5d43-235">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="f5d43-236">Dans cet exemple, {Slice} est remplacé par la valeur hello hello fabrique de données système variable SliceStart au hello format (AAAAMMJJHH).</span><span class="sxs-lookup"><span data-stu-id="f5d43-236">In this example, {Slice} is replaced with hello value of hello Data Factory system variable SliceStart in hello format (YYYYMMDDHH).</span></span> <span data-ttu-id="f5d43-237">SliceStart fait référence à des temps de toostart de tranche de hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-237">SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="f5d43-238">Hello folderPath est différent pour chaque secteur.</span><span class="sxs-lookup"><span data-stu-id="f5d43-238">hello folderPath is different for each slice.</span></span> <span data-ttu-id="f5d43-239">Par exemple : wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="f5d43-239">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="f5d43-240">Exemple 2 :</span><span class="sxs-lookup"><span data-stu-id="f5d43-240">Sample 2:</span></span>

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

<span data-ttu-id="f5d43-241">Dans cet exemple, année, mois, jour et l’heure de SliceStart sont extraits dans des variables distinctes qui utilisent des propriétés folderPath et fileName de hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-241">In this example, year, month, day, and time of SliceStart are extracted into separate variables that hello folderPath and fileName properties use.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="f5d43-242">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="f5d43-242">Copy activity properties</span></span>
<span data-ttu-id="f5d43-243">Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="f5d43-243">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f5d43-244">Les propriétés comme le nom, la description, les jeux de données d’entrée et de sortie et les stratégies sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="f5d43-244">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="f5d43-245">Tandis que les propriétés disponibles dans hello **typeProperties** section d’activité hello varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="f5d43-245">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span>

<span data-ttu-id="f5d43-246">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-246">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="f5d43-247">Si vous déplacez des données à partir d’un système de fichiers local, vous définissez type de source de hello dans l’activité de copie hello trop**FileSystemSource**.</span><span class="sxs-lookup"><span data-stu-id="f5d43-247">If you are moving data from an on-premises file system, you set hello source type in hello copy activity too**FileSystemSource**.</span></span> <span data-ttu-id="f5d43-248">De même, si vous déplacez des données tooan système de fichiers local, vous définissez le type de récepteur hello dans l’activité de copie hello trop**FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="f5d43-248">Similarly, if you are moving data tooan on-premises file system, you set hello sink type in hello copy activity too**FileSystemSink**.</span></span> <span data-ttu-id="f5d43-249">Cette section fournit une liste de propriétés prises en charge par FileSystemSource et FileSystemSink.</span><span class="sxs-lookup"><span data-stu-id="f5d43-249">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span></span>

<span data-ttu-id="f5d43-250">**FileSystemSource** prend en charge hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="f5d43-250">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="f5d43-251">Propriété</span><span class="sxs-lookup"><span data-stu-id="f5d43-251">Property</span></span> | <span data-ttu-id="f5d43-252">Description</span><span class="sxs-lookup"><span data-stu-id="f5d43-252">Description</span></span> | <span data-ttu-id="f5d43-253">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="f5d43-253">Allowed values</span></span> | <span data-ttu-id="f5d43-254">Requis</span><span class="sxs-lookup"><span data-stu-id="f5d43-254">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f5d43-255">recursive</span><span class="sxs-lookup"><span data-stu-id="f5d43-255">recursive</span></span> |<span data-ttu-id="f5d43-256">Indique si les données de salutation sont lu de manière récursive des sous-dossiers de hello ou uniquement à partir de dossier spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-256">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="f5d43-257">True, False (par défaut)</span><span class="sxs-lookup"><span data-stu-id="f5d43-257">True, False (default)</span></span> |<span data-ttu-id="f5d43-258">Non</span><span class="sxs-lookup"><span data-stu-id="f5d43-258">No</span></span> |

<span data-ttu-id="f5d43-259">**FileSystemSink** prend en charge hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="f5d43-259">**FileSystemSink** supports hello following properties:</span></span>

| <span data-ttu-id="f5d43-260">Propriété</span><span class="sxs-lookup"><span data-stu-id="f5d43-260">Property</span></span> | <span data-ttu-id="f5d43-261">Description</span><span class="sxs-lookup"><span data-stu-id="f5d43-261">Description</span></span> | <span data-ttu-id="f5d43-262">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="f5d43-262">Allowed values</span></span> | <span data-ttu-id="f5d43-263">Requis</span><span class="sxs-lookup"><span data-stu-id="f5d43-263">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f5d43-264">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="f5d43-264">copyBehavior</span></span> |<span data-ttu-id="f5d43-265">Définit le comportement de copie de hello lors de la source de hello est BlobSource ou système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="f5d43-265">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="f5d43-266">**PreserveHierarchy :** conserve la hiérarchie des fichiers dans le dossier cible de hello hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-266">**PreserveHierarchy:** Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="f5d43-267">Autrement dit, chemin d’accès relatif de hello du dossier source de hello source fichier toohello est hello identique au chemin d’accès relatif de hello du dossier cible de hello cible fichier toohello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-267">That is, hello relative path of hello source file toohello source folder is hello same as hello relative path of hello target file toohello target folder.</span></span><br/><br/><span data-ttu-id="f5d43-268">**FlattenHierarchy :** tous les fichiers à partir du dossier source hello sont créés dans hello premier niveau du dossier cible.</span><span class="sxs-lookup"><span data-stu-id="f5d43-268">**FlattenHierarchy:** All files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="f5d43-269">les fichiers cibles Hello sont créés avec un nom généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="f5d43-269">hello target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="f5d43-270">**MergeFiles :** fusionne tous les fichiers à partir de fichiers de tooone du dossier source hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-270">**MergeFiles:** Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="f5d43-271">Si le nom de blob/nom de fichier hello est spécifié, nom de fichier fusionné hello désigne hello spécifié.</span><span class="sxs-lookup"><span data-stu-id="f5d43-271">If hello file name/blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="f5d43-272">Dans le cas contraire, il s’agit d’un nom de fichier généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="f5d43-272">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="f5d43-273">Non</span><span class="sxs-lookup"><span data-stu-id="f5d43-273">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="f5d43-274">exemples de valeurs recursive et copyBehavior</span><span class="sxs-lookup"><span data-stu-id="f5d43-274">recursive and copyBehavior examples</span></span>
<span data-ttu-id="f5d43-275">Cette section décrit le comportement qui en résulte de hello d’opération de copie hello pour différentes combinaisons de valeurs pour les propriétés récursive et copyBehavior hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-275">This section describes hello resulting behavior of hello Copy operation for different combinations of values for hello recursive and copyBehavior properties.</span></span>

| <span data-ttu-id="f5d43-276">valeur recursive</span><span class="sxs-lookup"><span data-stu-id="f5d43-276">recursive value</span></span> | <span data-ttu-id="f5d43-277">valeur copyBehavior</span><span class="sxs-lookup"><span data-stu-id="f5d43-277">copyBehavior value</span></span> | <span data-ttu-id="f5d43-278">Comportement résultant</span><span class="sxs-lookup"><span data-stu-id="f5d43-278">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5d43-279">true</span><span class="sxs-lookup"><span data-stu-id="f5d43-279">true</span></span> |<span data-ttu-id="f5d43-280">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="f5d43-280">preserveHierarchy</span></span> |<span data-ttu-id="f5d43-281">Pour un dossier source Dossier1 avec hello suivant la structure,</span><span class="sxs-lookup"><span data-stu-id="f5d43-281">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="f5d43-282">Dossier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-282">Folder1</span></span><br/><span data-ttu-id="f5d43-283">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="f5d43-284">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="f5d43-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="f5d43-285">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="f5d43-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="f5d43-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="f5d43-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="f5d43-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="f5d43-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="f5d43-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="f5d43-289">dossier cible de Hello Dossier1 est créée avec hello même structure en tant que source de hello :</span><span class="sxs-lookup"><span data-stu-id="f5d43-289">hello target folder Folder1 is created with hello same structure as hello source:</span></span><br/><br/><span data-ttu-id="f5d43-290">Dossier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-290">Folder1</span></span><br/><span data-ttu-id="f5d43-291">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="f5d43-292">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="f5d43-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="f5d43-293">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="f5d43-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="f5d43-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="f5d43-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="f5d43-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="f5d43-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="f5d43-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="f5d43-297">true</span><span class="sxs-lookup"><span data-stu-id="f5d43-297">true</span></span> |<span data-ttu-id="f5d43-298">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="f5d43-298">flattenHierarchy</span></span> |<span data-ttu-id="f5d43-299">Pour un dossier source Dossier1 avec hello suivant la structure,</span><span class="sxs-lookup"><span data-stu-id="f5d43-299">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="f5d43-300">Dossier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-300">Folder1</span></span><br/><span data-ttu-id="f5d43-301">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="f5d43-302">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="f5d43-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="f5d43-303">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="f5d43-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="f5d43-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="f5d43-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="f5d43-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="f5d43-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="f5d43-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="f5d43-307">cible de Hello Dossier1 est créée avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="f5d43-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="f5d43-308">Dossier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-308">Folder1</span></span><br/><span data-ttu-id="f5d43-309">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-309">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="f5d43-310">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier2</span><span class="sxs-lookup"><span data-stu-id="f5d43-310">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="f5d43-311">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier3</span><span class="sxs-lookup"><span data-stu-id="f5d43-311">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="f5d43-312">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier4</span><span class="sxs-lookup"><span data-stu-id="f5d43-312">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="f5d43-313">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier5</span><span class="sxs-lookup"><span data-stu-id="f5d43-313">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="f5d43-314">true</span><span class="sxs-lookup"><span data-stu-id="f5d43-314">true</span></span> |<span data-ttu-id="f5d43-315">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="f5d43-315">mergeFiles</span></span> |<span data-ttu-id="f5d43-316">Pour un dossier source Dossier1 avec hello suivant la structure,</span><span class="sxs-lookup"><span data-stu-id="f5d43-316">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="f5d43-317">Dossier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-317">Folder1</span></span><br/><span data-ttu-id="f5d43-318">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="f5d43-319">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="f5d43-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="f5d43-320">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="f5d43-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="f5d43-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="f5d43-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="f5d43-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="f5d43-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="f5d43-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="f5d43-324">cible de Hello Dossier1 est créée avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="f5d43-324">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="f5d43-325">Dossier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-325">Folder1</span></span><br/><span data-ttu-id="f5d43-326">&nbsp;&nbsp;&nbsp;&nbsp;Le contenu de Fichier1 + Fichier2 + Fichier3 + Fichier4 + Fichier5 est fusionné dans un fichier avec le nom de fichier généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="f5d43-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span></span> |
| <span data-ttu-id="f5d43-327">false</span><span class="sxs-lookup"><span data-stu-id="f5d43-327">false</span></span> |<span data-ttu-id="f5d43-328">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="f5d43-328">preserveHierarchy</span></span> |<span data-ttu-id="f5d43-329">Pour un dossier source Dossier1 avec hello suivant la structure,</span><span class="sxs-lookup"><span data-stu-id="f5d43-329">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="f5d43-330">Dossier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-330">Folder1</span></span><br/><span data-ttu-id="f5d43-331">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="f5d43-332">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="f5d43-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="f5d43-333">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="f5d43-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="f5d43-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="f5d43-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="f5d43-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="f5d43-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="f5d43-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="f5d43-337">dossier cible de Hello Dossier1 est créée avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="f5d43-337">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="f5d43-338">Dossier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-338">Folder1</span></span><br/><span data-ttu-id="f5d43-339">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="f5d43-340">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="f5d43-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="f5d43-341">Sous-dossier1, où Fichier3, Fichier4 et Fichier5 ne sont pas sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="f5d43-341">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="f5d43-342">false</span><span class="sxs-lookup"><span data-stu-id="f5d43-342">false</span></span> |<span data-ttu-id="f5d43-343">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="f5d43-343">flattenHierarchy</span></span> |<span data-ttu-id="f5d43-344">Pour un dossier source Dossier1 avec hello suivant la structure,</span><span class="sxs-lookup"><span data-stu-id="f5d43-344">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="f5d43-345">Dossier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-345">Folder1</span></span><br/><span data-ttu-id="f5d43-346">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="f5d43-347">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="f5d43-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="f5d43-348">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="f5d43-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="f5d43-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="f5d43-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="f5d43-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="f5d43-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="f5d43-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="f5d43-352">dossier cible de Hello Dossier1 est créée avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="f5d43-352">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="f5d43-353">Dossier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-353">Folder1</span></span><br/><span data-ttu-id="f5d43-354">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-354">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="f5d43-355">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier2</span><span class="sxs-lookup"><span data-stu-id="f5d43-355">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><span data-ttu-id="f5d43-356">Sous-dossier1, où Fichier3, Fichier4 et Fichier5 ne sont pas sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="f5d43-356">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="f5d43-357">false</span><span class="sxs-lookup"><span data-stu-id="f5d43-357">false</span></span> |<span data-ttu-id="f5d43-358">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="f5d43-358">mergeFiles</span></span> |<span data-ttu-id="f5d43-359">Pour un dossier source Dossier1 avec hello suivant la structure,</span><span class="sxs-lookup"><span data-stu-id="f5d43-359">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="f5d43-360">Dossier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-360">Folder1</span></span><br/><span data-ttu-id="f5d43-361">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="f5d43-362">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="f5d43-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="f5d43-363">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="f5d43-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="f5d43-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="f5d43-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="f5d43-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="f5d43-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="f5d43-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="f5d43-367">dossier cible de Hello Dossier1 est créée avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="f5d43-367">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="f5d43-368">Dossier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-368">Folder1</span></span><br/><span data-ttu-id="f5d43-369">&nbsp;&nbsp;&nbsp;&nbsp;Le contenu de Fichier1 + Fichier2 est fusionné dans un fichier avec un nom de fichier généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="f5d43-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span></span><br/><span data-ttu-id="f5d43-370">&nbsp;&nbsp;&nbsp;&nbsp;Nom généré automatiquement pour Fichier1</span><span class="sxs-lookup"><span data-stu-id="f5d43-370">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span></span><br/><br/><span data-ttu-id="f5d43-371">Sous-dossier1, où Fichier3, Fichier4 et Fichier5 ne sont pas sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="f5d43-371">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="f5d43-372">Formats de fichier et de compression pris en charge</span><span class="sxs-lookup"><span data-stu-id="f5d43-372">Supported file and compression formats</span></span>
<span data-ttu-id="f5d43-373">Pour plus d’informations, voir [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="f5d43-373">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a><span data-ttu-id="f5d43-374">Exemples JSON pour la copie des données tooand à partir du système de fichiers</span><span class="sxs-lookup"><span data-stu-id="f5d43-374">JSON examples for copying data tooand from file system</span></span>
<span data-ttu-id="f5d43-375">Hello exemples suivants proposent des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de hello [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f5d43-375">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="f5d43-376">Elles montrent comment tooand de données toocopy à partir d’un système de fichiers local et le stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="f5d43-376">They show how toocopy data tooand from an on-premises file system and Azure Blob storage.</span></span> <span data-ttu-id="f5d43-377">Toutefois, vous pouvez copier les données *directement* de n’importe quelle tooany de sources hello de récepteurs hello répertoriés dans [prise en charge des sources et récepteurs](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de l’activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f5d43-377">However, you can copy data *directly* from any of hello sources tooany of hello sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a><span data-ttu-id="f5d43-378">Exemple : Copier des données à partir d’un tooAzure de système de fichiers local stockage d’objets Blob</span><span class="sxs-lookup"><span data-stu-id="f5d43-378">Example: Copy data from an on-premises file system tooAzure Blob storage</span></span>
<span data-ttu-id="f5d43-379">Cet exemple montre comment toocopy des données à partir d’un tooAzure de système de fichiers local stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="f5d43-379">This sample shows how toocopy data from an on-premises file system tooAzure Blob storage.</span></span> <span data-ttu-id="f5d43-380">exemple Hello a hello suivant des entités de fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="f5d43-380">hello sample has hello following Data Factory entities:</span></span>

* <span data-ttu-id="f5d43-381">Un service lié de type [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f5d43-381">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="f5d43-382">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f5d43-382">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="f5d43-383">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f5d43-383">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="f5d43-384">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f5d43-384">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="f5d43-385">Un [pipeline](data-factory-create-pipelines.md) avec activité de copie qui utilise [FileSystemSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f5d43-385">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="f5d43-386">Hello suivant l’exemple copie les données de séries chronologiques à partir d’un tooAzure de système de fichiers local stockage d’objets Blob toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="f5d43-386">hello following sample copies time-series data from an on-premises file system tooAzure Blob storage every hour.</span></span> <span data-ttu-id="f5d43-387">propriétés JSON Hello qui sont utilisées dans ces exemples sont décrits dans les sections hello après les exemples hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-387">hello JSON properties that are used in these samples are described in hello sections after hello samples.</span></span>

<span data-ttu-id="f5d43-388">Dans un premier temps, configurer la passerelle de gestion des données conformément aux instructions hello dans [déplacement des données entre des sources locales et cloud hello avec la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="f5d43-388">As a first step, set up Data Management Gateway as per hello instructions in [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span>

<span data-ttu-id="f5d43-389">**Service lié de serveur de fichiers local :**</span><span class="sxs-lookup"><span data-stu-id="f5d43-389">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="f5d43-390">Nous vous recommandons d’utiliser des hello **encryptedCredential** propriété hello plutôt **userid** et **mot de passe** propriétés.</span><span class="sxs-lookup"><span data-stu-id="f5d43-390">We recommend using hello **encryptedCredential** property instead hello **userid** and **password** properties.</span></span> <span data-ttu-id="f5d43-391">Consultez la page [Service lié de serveur de fichiers](#linked-service-properties) pour plus d’informations sur ce service lié.</span><span class="sxs-lookup"><span data-stu-id="f5d43-391">See [File Server linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="f5d43-392">**Service lié Azure Storage :**</span><span class="sxs-lookup"><span data-stu-id="f5d43-392">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="f5d43-393">**Jeu de données d’entrée de système de fichiers local :**</span><span class="sxs-lookup"><span data-stu-id="f5d43-393">**On-premises file system input dataset:**</span></span>

<span data-ttu-id="f5d43-394">Les données sont récupérées à partir d’un nouveau fichier toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="f5d43-394">Data is picked up from a new file every hour.</span></span> <span data-ttu-id="f5d43-395">Hello folderPath et les propriétés de nom de fichier sont déterminées en fonction de l’heure de début hello de tranche de hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-395">hello folderPath and fileName properties are determined based on hello start time of hello slice.</span></span>  

<span data-ttu-id="f5d43-396">Paramètre `"external": "true"` informe fabrique de données de ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-396">Setting `"external": "true"` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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

<span data-ttu-id="f5d43-397">**Jeu de données de sortie Stockage Blob Azure :**</span><span class="sxs-lookup"><span data-stu-id="f5d43-397">**Azure Blob storage output dataset:**</span></span>

<span data-ttu-id="f5d43-398">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="f5d43-398">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="f5d43-399">chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="f5d43-399">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="f5d43-400">chemin d’accès du dossier Hello utilise hello des parties d’année, mois, jour et heure de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-400">hello folder path uses hello year, month, day, and hour parts of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="f5d43-401">**Activité de copie dans un pipeline avec une source Système de fichiers et un récepteur blob :**</span><span class="sxs-lookup"><span data-stu-id="f5d43-401">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="f5d43-402">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie, et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="f5d43-402">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="f5d43-403">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**FileSystemSource**, et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="f5d43-403">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "FileSystemSource"
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

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a><span data-ttu-id="f5d43-404">Exemple : Copier des données à partir du système de fichiers de base de données SQL Azure tooan local</span><span class="sxs-lookup"><span data-stu-id="f5d43-404">Example: Copy data from Azure SQL Database tooan on-premises file system</span></span>
<span data-ttu-id="f5d43-405">Hello ci-dessous illustre d’exemple :</span><span class="sxs-lookup"><span data-stu-id="f5d43-405">hello following sample shows:</span></span>

* <span data-ttu-id="f5d43-406">Un service lié de type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f5d43-406">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="f5d43-407">Un service lié de type [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f5d43-407">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="f5d43-408">Un jeu de données d’entrée de type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f5d43-408">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="f5d43-409">Un jeu de données de sortie de type [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f5d43-409">An output dataset of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="f5d43-410">Un pipeline avec une activité de copie qui utilise [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) et [FileSystemSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f5d43-410">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span></span>

<span data-ttu-id="f5d43-411">exemple Hello copie les données de séries chronologiques à partir d’un système de fichiers local de SQL Azure table tooan toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="f5d43-411">hello sample copies time-series data from an Azure SQL table tooan on-premises file system every hour.</span></span> <span data-ttu-id="f5d43-412">les propriétés JSON Hello qui sont utilisées dans ces exemples sont décrits dans les sections après les exemples hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-412">hello JSON properties that are used in these samples are described in sections after hello samples.</span></span>

<span data-ttu-id="f5d43-413">**Service lié pour Azure SQL Database :**</span><span class="sxs-lookup"><span data-stu-id="f5d43-413">**Azure SQL Database linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```

<span data-ttu-id="f5d43-414">**Service lié de serveur de fichiers local :**</span><span class="sxs-lookup"><span data-stu-id="f5d43-414">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="f5d43-415">Nous vous recommandons d’utiliser des hello **encryptedCredential** propriété au lieu d’utiliser hello **userid** et **mot de passe** propriétés.</span><span class="sxs-lookup"><span data-stu-id="f5d43-415">We recommend using hello **encryptedCredential** property instead of using hello **userid** and **password** properties.</span></span> <span data-ttu-id="f5d43-416">Consultez la page [Service lié de système de fichiers](#linked-service-properties) pour plus d’informations sur ce service lié.</span><span class="sxs-lookup"><span data-stu-id="f5d43-416">See [File System linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="f5d43-417">**Jeu de données d'entrée SQL Azure :**</span><span class="sxs-lookup"><span data-stu-id="f5d43-417">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="f5d43-418">exemple Hello part du principe que vous avez créé une table « MyTable » dans SQL Azure, et contient une colonne appelée « timestampcolumn » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="f5d43-418">hello sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span></span>

<span data-ttu-id="f5d43-419">Paramètre ``“external”: ”true”`` informe fabrique de données de ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-419">Setting ``“external”: ”true”`` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

<span data-ttu-id="f5d43-420">**Jeu de données de sortie de système de fichiers local :**</span><span class="sxs-lookup"><span data-stu-id="f5d43-420">**On-premises file system output dataset:**</span></span>

<span data-ttu-id="f5d43-421">Données sont copiée tooa nouveau fichier toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="f5d43-421">Data is copied tooa new file every hour.</span></span> <span data-ttu-id="f5d43-422">Hello folderPath et fileName pour l’objet blob de hello sont déterminés en fonction de l’heure de début hello de tranche de hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-422">hello folderPath and fileName for hello blob are determined based on hello start time of hello slice.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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

<span data-ttu-id="f5d43-423">**Activité de copie dans un pipeline avec une source SQL et un récepteur Système de fichiers :**</span><span class="sxs-lookup"><span data-stu-id="f5d43-423">**A copy activity in a pipeline with SQL source and File System sink:**</span></span>

<span data-ttu-id="f5d43-424">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie, et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="f5d43-424">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="f5d43-425">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**SqlSource**et hello **récepteur** type est défini trop**FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="f5d43-425">In hello pipeline JSON definition, hello **source** type is set too**SqlSource**, and hello **sink** type is set too**FileSystemSink**.</span></span> <span data-ttu-id="f5d43-426">la requête SQL Hello qui est spécifiée pour hello **SqlReaderQuery** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.</span><span class="sxs-lookup"><span data-stu-id="f5d43-426">hello SQL query that is specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


<span data-ttu-id="f5d43-427">Vous pouvez également mapper des colonnes à partir de toocolumns du jeu de données source à partir de récepteur de jeu de données dans la définition d’activité de copie de hello.</span><span class="sxs-lookup"><span data-stu-id="f5d43-427">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="f5d43-428">Pour plus d’informations, consultez [Mappage de colonnes de jeux de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="f5d43-428">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="f5d43-429">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="f5d43-429">Performance and tuning</span></span>
 <span data-ttu-id="f5d43-430">toolearn sur la clé de facteurs qui impact hello les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize, consultez hello [guide de paramétrage et de performances de l’activité de copie](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="f5d43-430">toolearn about key factors that impact hello performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>
