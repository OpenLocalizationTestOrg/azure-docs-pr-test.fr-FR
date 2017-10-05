---
title: "Copier des données vers/à partir d’un système de fichiers à l’aide d’Azure Data Factory | Microsoft Docs"
description: "Apprenez à copier des données vers et à partir d’un système de fichiers local à l’aide d’Azure Data Factory."
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
ms.openlocfilehash: 52305e54f539de6aba2ba9cc856a09e04d608ded
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="copy-data-to-and-from-an-on-premises-file-system-by-using-azure-data-factory"></a><span data-ttu-id="09e51-103">Copier des données vers et à partir d’un système de fichiers local à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="09e51-103">Copy data to and from an on-premises file system by using Azure Data Factory</span></span>
<span data-ttu-id="09e51-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour déplacer des données vers et à partir d’un système de fichiers local.</span><span class="sxs-lookup"><span data-stu-id="09e51-104">This article explains how to use the Copy Activity in Azure Data Factory to copy data to/from an on-premises file system.</span></span> <span data-ttu-id="09e51-105">Il s’appuie sur l’article [Activités de déplacement des données](data-factory-data-movement-activities.md), qui présente une vue d’ensemble du déplacement de données avec l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="09e51-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="09e51-106">Scénarios pris en charge</span><span class="sxs-lookup"><span data-stu-id="09e51-106">Supported scenarios</span></span>
<span data-ttu-id="09e51-107">Vous pouvez copier des données **d’un système de fichiers local** vers les magasins de données suivants :</span><span class="sxs-lookup"><span data-stu-id="09e51-107">You can copy data **from an on-premises file system** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="09e51-108">Vous pouvez copier des données des magasins de données suivants **vers un système de fichiers local** :</span><span class="sxs-lookup"><span data-stu-id="09e51-108">You can copy data from the following data stores **to an on-premises file system**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="09e51-109">L’activité de copie ne supprime pas le fichier source une fois qu’il est copié sur la destination.</span><span class="sxs-lookup"><span data-stu-id="09e51-109">Copy Activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="09e51-110">Si vous devez supprimer le fichier source une fois qu’il est copié, créez une activité personnalisée pour supprimer le fichier et utilisez l’activité dans le pipeline.</span><span class="sxs-lookup"><span data-stu-id="09e51-110">If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="09e51-111">Activation de la connectivité</span><span class="sxs-lookup"><span data-stu-id="09e51-111">Enabling connectivity</span></span>
<span data-ttu-id="09e51-112">Data Factory prend en charge la connexion vers et depuis un système de fichiers local via la **passerelle de gestion des données**.</span><span class="sxs-lookup"><span data-stu-id="09e51-112">Data Factory supports connecting to and from an on-premises file system via **Data Management Gateway**.</span></span> <span data-ttu-id="09e51-113">Vous devez installer la passerelle de gestion des données dans votre environnement local pour que le service Data Factory se connecte à tout magasin de données local pris en charge comprenant le système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="09e51-113">You must install the Data Management Gateway in your on-premises environment for the Data Factory service to connect to any supported on-premises data store including file system.</span></span> <span data-ttu-id="09e51-114">Consultez l’article [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) pour en savoir plus sur la passerelle de gestion des données et obtenir des instructions détaillées sur la configuration de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="09e51-114">To learn about Data Management Gateway and for step-by-step instructions on setting up the gateway, see [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="09e51-115">En dehors de la passerelle de gestion des données, aucun autre fichier binaire n’a besoin d’être installé pour communiquer vers et depuis un système de fichiers local.</span><span class="sxs-lookup"><span data-stu-id="09e51-115">Apart from Data Management Gateway, no other binary files need to be installed to communicate to and from an on-premises file system.</span></span> <span data-ttu-id="09e51-116">Vous devez installer et utiliser la passerelle de gestion des données même si le système de fichiers se trouve dans la machine virtuelle Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="09e51-116">You must install and use the Data Management Gateway even if the file system is in Azure IaaS VM.</span></span> <span data-ttu-id="09e51-117">Pour obtenir des informations détaillées sur la passerelle, consultez [Passerelle de gestion des données](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="09e51-117">For detailed information about the gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="09e51-118">Pour utiliser un partage de fichiers Linux, installez [Samba](https://www.samba.org/) sur votre serveur Linux, puis la passerelle de gestion des données sur un serveur Windows.</span><span class="sxs-lookup"><span data-stu-id="09e51-118">To use a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span></span> <span data-ttu-id="09e51-119">L’installation de la passerelle de gestion des données sur un serveur Linux n'est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="09e51-119">Installing Data Management Gateway on a Linux server is not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="09e51-120">Prise en main</span><span class="sxs-lookup"><span data-stu-id="09e51-120">Getting started</span></span>
<span data-ttu-id="09e51-121">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données vers/depuis un système de fichiers à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="09e51-121">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span></span>

<span data-ttu-id="09e51-122">Le moyen le plus simple de créer un pipeline consiste à utiliser **l’Assistant Copie**.</span><span class="sxs-lookup"><span data-stu-id="09e51-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="09e51-123">Consultez la page [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant Copier des données.</span><span class="sxs-lookup"><span data-stu-id="09e51-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="09e51-124">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="09e51-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="09e51-125">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="09e51-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="09e51-126">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="09e51-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="09e51-127">Création d'une **fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="09e51-127">Create a **data factory**.</span></span> <span data-ttu-id="09e51-128">Une fabrique de données peut contenir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="09e51-128">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="09e51-129">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="09e51-129">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="09e51-130">Par exemple, si vous copiez des données d’un Stockage Blob Azure vers un système de fichiers local, vous créez deux services liés pour lier votre système de fichiers local et votre compte de stockage Azure à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="09e51-130">For example, if you are copying data from an Azure blob storage to an on-premises file system, you create two linked services to link your on-premises file system and Azure storage account to your data factory.</span></span> <span data-ttu-id="09e51-131">Pour connaître les propriétés des services liés propres à un système de fichiers local, consultez la section [Propriétés des services liés](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="09e51-131">For linked service properties that are specific to an on-premises file system, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="09e51-132">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="09e51-132">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="09e51-133">Dans l’exemple mentionné à la dernière étape, vous créez un jeu de données pour spécifier le conteneur d’objets Blob et le dossier qui contient les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="09e51-133">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="09e51-134">Vous créez également un autre jeu de données pour spécifier le nom de dossier et de fichier (facultatif) dans votre système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="09e51-134">And, you create another dataset to specify the folder and file name (optional) in your file system.</span></span> <span data-ttu-id="09e51-135">Pour connaître les propriétés des jeux de données propres à un système de fichiers local, consultez la section [Propriétés des jeux de données](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="09e51-135">For dataset properties that are specific to on-premises file system, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="09e51-136">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="09e51-136">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="09e51-137">Dans l’exemple mentionné plus haut, vous utilisez BlobSource comme source et FileSystemSink comme récepteur de l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="09e51-137">In the example mentioned earlier, you use BlobSource as a source and FileSystemSink as a sink for the copy activity.</span></span> <span data-ttu-id="09e51-138">De même, si vous copiez d’un système de fichiers local vers le Stockage Blob Azure, vous utilisez FileSystemSource et BlobSink dans l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="09e51-138">Similarly, if you are copying from on-premises file system to Azure Blob Storage, you use FileSystemSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="09e51-139">Pour connaître les propriétés de l’activité de copie propres à un système de fichiers local, consultez la section [Propriétés de l’activité de copie](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="09e51-139">For copy activity properties that are specific to on-premises file system, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="09e51-140">Pour plus d’informations sur l’utilisation d’un magasin de données comme source ou comme récepteur, cliquez sur le lien de la section précédente de votre magasin de données.</span><span class="sxs-lookup"><span data-stu-id="09e51-140">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="09e51-141">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="09e51-141">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="09e51-142">Lorsque vous utilisez des outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory au format JSON.</span><span class="sxs-lookup"><span data-stu-id="09e51-142">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="09e51-143">Pour obtenir des exemples comportant des définitions JSON d’entités Data Factory utilisées pour copier les données vers ou à partir d’un système de fichiers, consultez la section [Exemples JSON](#json-examples-for-copying-data-to-and-from-file-system) de cet article.</span><span class="sxs-lookup"><span data-stu-id="09e51-143">For samples with JSON definitions for Data Factory entities that are used to copy data to/from a file system, see [JSON examples](#json-examples-for-copying-data-to-and-from-file-system) section of this article.</span></span>

<span data-ttu-id="09e51-144">Les sections suivantes fournissent des informations détaillées sur les propriétés JSON utilisées pour définir les entités Data Factory propres au système de fichiers :</span><span class="sxs-lookup"><span data-stu-id="09e51-144">The following sections provide details about JSON properties that are used to define Data Factory entities specific to file system:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="09e51-145">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="09e51-145">Linked service properties</span></span>
<span data-ttu-id="09e51-146">Vous pouvez lier un système de fichiers local à une fabrique de données Azure avec le service lié **Serveur de fichiers local**.</span><span class="sxs-lookup"><span data-stu-id="09e51-146">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span></span> <span data-ttu-id="09e51-147">Le tableau suivant décrit les éléments JSON spécifiques au service lié Serveur de fichiers local.</span><span class="sxs-lookup"><span data-stu-id="09e51-147">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span></span>

| <span data-ttu-id="09e51-148">Propriété</span><span class="sxs-lookup"><span data-stu-id="09e51-148">Property</span></span> | <span data-ttu-id="09e51-149">Description</span><span class="sxs-lookup"><span data-stu-id="09e51-149">Description</span></span> | <span data-ttu-id="09e51-150">Requis</span><span class="sxs-lookup"><span data-stu-id="09e51-150">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="09e51-151">type</span><span class="sxs-lookup"><span data-stu-id="09e51-151">type</span></span> |<span data-ttu-id="09e51-152">Vérifiez que la propriété type est définie sur **OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="09e51-152">Ensure that the type property is set to **OnPremisesFileServer**.</span></span> |<span data-ttu-id="09e51-153">Oui</span><span class="sxs-lookup"><span data-stu-id="09e51-153">Yes</span></span> |
| <span data-ttu-id="09e51-154">host</span><span class="sxs-lookup"><span data-stu-id="09e51-154">host</span></span> |<span data-ttu-id="09e51-155">Spécifie le chemin d’accès racine du dossier que vous souhaitez copier.</span><span class="sxs-lookup"><span data-stu-id="09e51-155">Specifies the root path of the folder that you want to copy.</span></span> <span data-ttu-id="09e51-156">Utilisez le caractère d’échappement « \ » pour les caractères spéciaux contenus dans la chaîne.</span><span class="sxs-lookup"><span data-stu-id="09e51-156">Use the escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="09e51-157">Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples.</span><span class="sxs-lookup"><span data-stu-id="09e51-157">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="09e51-158">Oui</span><span class="sxs-lookup"><span data-stu-id="09e51-158">Yes</span></span> |
| <span data-ttu-id="09e51-159">userId</span><span class="sxs-lookup"><span data-stu-id="09e51-159">userid</span></span> |<span data-ttu-id="09e51-160">Spécifiez l’ID de l’utilisateur qui a accès au serveur.</span><span class="sxs-lookup"><span data-stu-id="09e51-160">Specify the ID of the user who has access to the server.</span></span> |<span data-ttu-id="09e51-161">Non (si vous choisissez encryptedcredential)</span><span class="sxs-lookup"><span data-stu-id="09e51-161">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="09e51-162">password</span><span class="sxs-lookup"><span data-stu-id="09e51-162">password</span></span> |<span data-ttu-id="09e51-163">Spécifiez le mot de passe de l’utilisateur (userid).</span><span class="sxs-lookup"><span data-stu-id="09e51-163">Specify the password for the user (userid).</span></span> |<span data-ttu-id="09e51-164">Non (si vous choisissez encryptedcredential)</span><span class="sxs-lookup"><span data-stu-id="09e51-164">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="09e51-165">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="09e51-165">encryptedCredential</span></span> |<span data-ttu-id="09e51-166">Spécifiez les informations d’identification chiffrées que vous pouvez obtenir en exécutant l’applet de commande New-AzureRmDataFactoryEncryptValue.</span><span class="sxs-lookup"><span data-stu-id="09e51-166">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="09e51-167">Non (si vous choisissez de spécifier un nom d'utilisateur et un mot de passe en texte brut)</span><span class="sxs-lookup"><span data-stu-id="09e51-167">No (if you choose to specify userid and password in plain text)</span></span> |
| <span data-ttu-id="09e51-168">gatewayName</span><span class="sxs-lookup"><span data-stu-id="09e51-168">gatewayName</span></span> |<span data-ttu-id="09e51-169">Spécifie le nom de la passerelle que Data Factory doit utiliser pour se connecter au serveur de fichiers local.</span><span class="sxs-lookup"><span data-stu-id="09e51-169">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span></span> |<span data-ttu-id="09e51-170">Oui</span><span class="sxs-lookup"><span data-stu-id="09e51-170">Yes</span></span> |


### <a name="sample-linked-service-and-dataset-definitions"></a><span data-ttu-id="09e51-171">Exemples de définitions de jeux de données et de service liés</span><span class="sxs-lookup"><span data-stu-id="09e51-171">Sample linked service and dataset definitions</span></span>
| <span data-ttu-id="09e51-172">Scénario</span><span class="sxs-lookup"><span data-stu-id="09e51-172">Scenario</span></span> | <span data-ttu-id="09e51-173">Hôte dans la définition du service lié</span><span class="sxs-lookup"><span data-stu-id="09e51-173">Host in linked service definition</span></span> | <span data-ttu-id="09e51-174">folderPath dans la définition du jeu de données</span><span class="sxs-lookup"><span data-stu-id="09e51-174">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="09e51-175">Dossier local sur l’ordinateur passerelle de gestion des données : </span><span class="sxs-lookup"><span data-stu-id="09e51-175">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="09e51-176">Exemples : D:\\\* ou D:\dossier\sous-dossier\\*</span><span class="sxs-lookup"><span data-stu-id="09e51-176">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="09e51-177">D:\\\\ (pour la passerelle de gestion des données 2.0 et versions ultérieures)</span><span class="sxs-lookup"><span data-stu-id="09e51-177">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="09e51-178">hôte local (pour les versions de la passerelle de gestion des données antérieures à 2.0)</span><span class="sxs-lookup"><span data-stu-id="09e51-178">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="09e51-179">.\\\\ ou dossier\\\\sous-dossier (pour la passerelle de gestion des données 2.0 et versions ultérieures)</span><span class="sxs-lookup"><span data-stu-id="09e51-179">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="09e51-180">D:\\\\ ou D:\\\\dossier\\\\sous-dossier (pour les versions de la passerelle antérieures à 2.0)</span><span class="sxs-lookup"><span data-stu-id="09e51-180">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="09e51-181">Dossier partagé distant : </span><span class="sxs-lookup"><span data-stu-id="09e51-181">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="09e51-182">Exemples : \\\\myserver\\share\\\* ou \\\\myserver\\share\\dossier\\sous-dossier\\*</span><span class="sxs-lookup"><span data-stu-id="09e51-182">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="09e51-183">\\\\\\\\myserver\\\\share</span><span class="sxs-lookup"><span data-stu-id="09e51-183">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="09e51-184">.\\\\ ou dossier\\\\sous-dossier</span><span class="sxs-lookup"><span data-stu-id="09e51-184">.\\\\ or folder\\\\subfolder</span></span> |


### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="09e51-185">Exemple : utilisation d’un nom d'utilisateur et d’un mot de passe en texte brut</span><span class="sxs-lookup"><span data-stu-id="09e51-185">Example: Using username and password in plain text</span></span>

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

### <a name="example-using-encryptedcredential"></a><span data-ttu-id="09e51-186">Exemple : utilisation de l’élément encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="09e51-186">Example: Using encryptedcredential</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="09e51-187">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="09e51-187">Dataset properties</span></span>
<span data-ttu-id="09e51-188">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="09e51-188">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="09e51-189">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données.</span><span class="sxs-lookup"><span data-stu-id="09e51-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="09e51-190">La section typeProperties est différente pour chaque type de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="09e51-190">The typeProperties section is different for each type of dataset.</span></span> <span data-ttu-id="09e51-191">Elle fournit des informations telles que l’emplacement et le format des données dans la banque de données.</span><span class="sxs-lookup"><span data-stu-id="09e51-191">It provides information such as the location and format of the data in the data store.</span></span> <span data-ttu-id="09e51-192">La section typeProperties pour le jeu de données de type **FileShare** a les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="09e51-192">The typeProperties section for the dataset of type **FileShare** has the following properties:</span></span>

| <span data-ttu-id="09e51-193">Propriété</span><span class="sxs-lookup"><span data-stu-id="09e51-193">Property</span></span> | <span data-ttu-id="09e51-194">Description</span><span class="sxs-lookup"><span data-stu-id="09e51-194">Description</span></span> | <span data-ttu-id="09e51-195">Requis</span><span class="sxs-lookup"><span data-stu-id="09e51-195">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="09e51-196">folderPath</span><span class="sxs-lookup"><span data-stu-id="09e51-196">folderPath</span></span> |<span data-ttu-id="09e51-197">Spécifie le sous-chemin vers le dossier.</span><span class="sxs-lookup"><span data-stu-id="09e51-197">Specifies the subpath to the folder.</span></span> <span data-ttu-id="09e51-198">Utilisez le caractère d’échappement « \ » pour les caractères spéciaux contenus dans la chaîne.</span><span class="sxs-lookup"><span data-stu-id="09e51-198">Use the escape character ‘\’ for special characters in the string.</span></span> <span data-ttu-id="09e51-199">Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples.</span><span class="sxs-lookup"><span data-stu-id="09e51-199">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="09e51-200">Vous pouvez également effectuer une combinaison avec la propriété **partitionBy** pour que les chemins d’accès de dossier soient basés sur les dates et heures de démarrage et d’arrêt de la tranche.</span><span class="sxs-lookup"><span data-stu-id="09e51-200">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="09e51-201">Oui</span><span class="sxs-lookup"><span data-stu-id="09e51-201">Yes</span></span> |
| <span data-ttu-id="09e51-202">fileName</span><span class="sxs-lookup"><span data-stu-id="09e51-202">fileName</span></span> |<span data-ttu-id="09e51-203">Spécifiez le nom du fichier dans l’élément **folderPath** si vous souhaitez que la table se réfère à un fichier spécifique du dossier.</span><span class="sxs-lookup"><span data-stu-id="09e51-203">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="09e51-204">Si vous ne spécifiez aucune valeur pour cette propriété, le tableau pointe vers tous les fichiers du dossier.</span><span class="sxs-lookup"><span data-stu-id="09e51-204">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="09e51-205">Lorsque **fileName** n'est pas spécifié pour un jeu de données de sortie et que **preserveHierarchy** n’est pas spécifié dans le récepteur d’activité, le nom du fichier généré est au format suivant :</span><span class="sxs-lookup"><span data-stu-id="09e51-205">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="09e51-206">`Data.<Guid>.txt` (Exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="09e51-206">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="09e51-207">Non</span><span class="sxs-lookup"><span data-stu-id="09e51-207">No</span></span> |
| <span data-ttu-id="09e51-208">fileFilter</span><span class="sxs-lookup"><span data-stu-id="09e51-208">fileFilter</span></span> |<span data-ttu-id="09e51-209">Spécifiez un filtre à utiliser pour sélectionner un sous-ensemble de fichiers dans le folderPath plutôt que tous les fichiers.</span><span class="sxs-lookup"><span data-stu-id="09e51-209">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="09e51-210">Les valeurs autorisées sont : `*` (plusieurs caractères) et `?` (caractère unique).</span><span class="sxs-lookup"><span data-stu-id="09e51-210">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="09e51-211">Exemple 1 : « fileFilter » : « *.log »</span><span class="sxs-lookup"><span data-stu-id="09e51-211">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="09e51-212">Exemple 2 : « fileFilter » : « 2014-1-?.txt »</span><span class="sxs-lookup"><span data-stu-id="09e51-212">Example 2: "fileFilter": 2014-1-?.txt"</span></span><br/><br/><span data-ttu-id="09e51-213">Remarque : fileFilter s’applique à un jeu de données FileShare d’entrée.</span><span class="sxs-lookup"><span data-stu-id="09e51-213">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="09e51-214">Non</span><span class="sxs-lookup"><span data-stu-id="09e51-214">No</span></span> |
| <span data-ttu-id="09e51-215">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="09e51-215">partitionedBy</span></span> |<span data-ttu-id="09e51-216">partitionedBy peut être utilisé pour spécifier un folderPath/fileName dynamique pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="09e51-216">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="09e51-217">Par exemple, folderPath peut être paramétré pour toutes les heures de données.</span><span class="sxs-lookup"><span data-stu-id="09e51-217">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="09e51-218">Non</span><span class="sxs-lookup"><span data-stu-id="09e51-218">No</span></span> |
| <span data-ttu-id="09e51-219">format</span><span class="sxs-lookup"><span data-stu-id="09e51-219">format</span></span> | <span data-ttu-id="09e51-220">Les types de formats suivants sont pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="09e51-220">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="09e51-221">Définissez la propriété **type** située sous Format sur l’une de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="09e51-221">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="09e51-222">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="09e51-222">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="09e51-223">Si vous souhaitez **copier des fichiers en l’état** entre des magasins de fichiers (copie binaire), ignorez la section Format dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="09e51-223">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="09e51-224">Non</span><span class="sxs-lookup"><span data-stu-id="09e51-224">No</span></span> |
| <span data-ttu-id="09e51-225">compression</span><span class="sxs-lookup"><span data-stu-id="09e51-225">compression</span></span> | <span data-ttu-id="09e51-226">Spécifiez le type et le niveau de compression pour les données.</span><span class="sxs-lookup"><span data-stu-id="09e51-226">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="09e51-227">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="09e51-227">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="09e51-228">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="09e51-228">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="09e51-229">consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="09e51-229">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="09e51-230">Non</span><span class="sxs-lookup"><span data-stu-id="09e51-230">No</span></span> |

> [!NOTE]
> <span data-ttu-id="09e51-231">Vous ne pouvez pas utiliser fileName et fileFilter simultanément.</span><span class="sxs-lookup"><span data-stu-id="09e51-231">You cannot use fileName and fileFilter simultaneously.</span></span>

### <a name="using-partitionedby-property"></a><span data-ttu-id="09e51-232">Utilisation de la propriété partitionedBy</span><span class="sxs-lookup"><span data-stu-id="09e51-232">Using partitionedBy property</span></span>
<span data-ttu-id="09e51-233">Comme mentionné dans la section précédente, vous pouvez spécifier un folderPath et un fileName dynamiques pour les données de série chronologique avec la propriété **partitionedBy**, [les fonctions Data Factory et les variables système](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="09e51-233">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="09e51-234">Consultez les articles [Création de jeux de données](data-factory-create-datasets.md), [Planification et exécution](data-factory-scheduling-and-execution.md) et [Création de pipelines](data-factory-create-pipelines.md) pour mieux comprendre les jeux de données de série chronologique, la planification et les segments.</span><span class="sxs-lookup"><span data-stu-id="09e51-234">To understand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="09e51-235">Exemple 1 :</span><span class="sxs-lookup"><span data-stu-id="09e51-235">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="09e51-236">Dans cet exemple, {Slice} est remplacé par la valeur de la variable système Data Factory SliceStart au format (AAAAMMJJHH).</span><span class="sxs-lookup"><span data-stu-id="09e51-236">In this example, {Slice} is replaced with the value of the Data Factory system variable SliceStart in the format (YYYYMMDDHH).</span></span> <span data-ttu-id="09e51-237">SliceStart fait référence à l’heure de début de la tranche.</span><span class="sxs-lookup"><span data-stu-id="09e51-237">SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="09e51-238">folderPath est différent pour chaque segment.</span><span class="sxs-lookup"><span data-stu-id="09e51-238">The folderPath is different for each slice.</span></span> <span data-ttu-id="09e51-239">Par exemple : wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="09e51-239">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="09e51-240">Exemple 2 :</span><span class="sxs-lookup"><span data-stu-id="09e51-240">Sample 2:</span></span>

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

<span data-ttu-id="09e51-241">Dans cet exemple, l’année, le mois, le jour et l’heure de SliceStart sont extraits dans des variables distinctes qui sont utilisées par les propriétés folderPath et fileName.</span><span class="sxs-lookup"><span data-stu-id="09e51-241">In this example, year, month, day, and time of SliceStart are extracted into separate variables that the folderPath and fileName properties use.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="09e51-242">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="09e51-242">Copy activity properties</span></span>
<span data-ttu-id="09e51-243">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="09e51-243">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="09e51-244">Les propriétés comme le nom, la description, les jeux de données d’entrée et de sortie et les stratégies sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="09e51-244">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="09e51-245">En revanche, les propriétés disponibles dans la section **typeProperties** de l’activité varient pour chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="09e51-245">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span>

<span data-ttu-id="09e51-246">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="09e51-246">For Copy activity, they vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="09e51-247">Si vous déplacez des données à partir d’un système de fichiers local, vous définissez le type de source dans l’activité de copie sur **FileSystemSource**.</span><span class="sxs-lookup"><span data-stu-id="09e51-247">If you are moving data from an on-premises file system, you set the source type in the copy activity to **FileSystemSource**.</span></span> <span data-ttu-id="09e51-248">De même, si vous déplacez des données vers un système de fichiers local, vous définissez le type de récepteur dans l’activité de copie sur **FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="09e51-248">Similarly, if you are moving data to an on-premises file system, you set the sink type in the copy activity to **FileSystemSink**.</span></span> <span data-ttu-id="09e51-249">Cette section fournit une liste de propriétés prises en charge par FileSystemSource et FileSystemSink.</span><span class="sxs-lookup"><span data-stu-id="09e51-249">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span></span>

<span data-ttu-id="09e51-250">**FileSystemSource** prend en charge les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="09e51-250">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="09e51-251">Propriété</span><span class="sxs-lookup"><span data-stu-id="09e51-251">Property</span></span> | <span data-ttu-id="09e51-252">Description</span><span class="sxs-lookup"><span data-stu-id="09e51-252">Description</span></span> | <span data-ttu-id="09e51-253">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="09e51-253">Allowed values</span></span> | <span data-ttu-id="09e51-254">Requis</span><span class="sxs-lookup"><span data-stu-id="09e51-254">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="09e51-255">recursive</span><span class="sxs-lookup"><span data-stu-id="09e51-255">recursive</span></span> |<span data-ttu-id="09e51-256">Indique si les données sont lues de manière récursive à partir des sous-dossiers ou uniquement du dossier spécifié.</span><span class="sxs-lookup"><span data-stu-id="09e51-256">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="09e51-257">True, False (par défaut)</span><span class="sxs-lookup"><span data-stu-id="09e51-257">True, False (default)</span></span> |<span data-ttu-id="09e51-258">Non</span><span class="sxs-lookup"><span data-stu-id="09e51-258">No</span></span> |

<span data-ttu-id="09e51-259">**FileSystemSink** prend en charge les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="09e51-259">**FileSystemSink** supports the following properties:</span></span>

| <span data-ttu-id="09e51-260">Propriété</span><span class="sxs-lookup"><span data-stu-id="09e51-260">Property</span></span> | <span data-ttu-id="09e51-261">Description</span><span class="sxs-lookup"><span data-stu-id="09e51-261">Description</span></span> | <span data-ttu-id="09e51-262">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="09e51-262">Allowed values</span></span> | <span data-ttu-id="09e51-263">Requis</span><span class="sxs-lookup"><span data-stu-id="09e51-263">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="09e51-264">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="09e51-264">copyBehavior</span></span> |<span data-ttu-id="09e51-265">Cette propriété définit le comportement de copie lorsque la source est BlobSource ou FileSystem.</span><span class="sxs-lookup"><span data-stu-id="09e51-265">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="09e51-266">**PreserveHierarchy :** conserve la hiérarchie des fichiers dans le dossier cible.</span><span class="sxs-lookup"><span data-stu-id="09e51-266">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="09e51-267">Le chemin d’accès relatif du fichier source vers le dossier source est identique au chemin d’accès relatif du fichier cible vers le dossier cible.</span><span class="sxs-lookup"><span data-stu-id="09e51-267">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span></span><br/><br/><span data-ttu-id="09e51-268">**FlattenHierarchy**: tous les fichiers du dossier source sont créés dans le premier niveau du dossier cible.</span><span class="sxs-lookup"><span data-stu-id="09e51-268">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="09e51-269">Les fichiers cibles sont créés avec un nom généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="09e51-269">The target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="09e51-270">**MergeFiles** : fusionne tous les fichiers du dossier source dans un même fichier.</span><span class="sxs-lookup"><span data-stu-id="09e51-270">**MergeFiles:** Merges all files from the source folder to one file.</span></span> <span data-ttu-id="09e51-271">Si le nom d’objet blob ou le nom de fichier est spécifié, le nom de fichier fusionné est le nom spécifié.</span><span class="sxs-lookup"><span data-stu-id="09e51-271">If the file name/blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="09e51-272">Dans le cas contraire, il s’agit d’un nom de fichier généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="09e51-272">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="09e51-273">Non</span><span class="sxs-lookup"><span data-stu-id="09e51-273">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="09e51-274">exemples de valeurs recursive et copyBehavior</span><span class="sxs-lookup"><span data-stu-id="09e51-274">recursive and copyBehavior examples</span></span>
<span data-ttu-id="09e51-275">Cette section décrit le comportement résultant de l’opération de copie pour différentes combinaisons de valeurs pour les propriétés recursive et copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="09e51-275">This section describes the resulting behavior of the Copy operation for different combinations of values for the recursive and copyBehavior properties.</span></span>

| <span data-ttu-id="09e51-276">valeur recursive</span><span class="sxs-lookup"><span data-stu-id="09e51-276">recursive value</span></span> | <span data-ttu-id="09e51-277">valeur copyBehavior</span><span class="sxs-lookup"><span data-stu-id="09e51-277">copyBehavior value</span></span> | <span data-ttu-id="09e51-278">Comportement résultant</span><span class="sxs-lookup"><span data-stu-id="09e51-278">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="09e51-279">true</span><span class="sxs-lookup"><span data-stu-id="09e51-279">true</span></span> |<span data-ttu-id="09e51-280">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="09e51-280">preserveHierarchy</span></span> |<span data-ttu-id="09e51-281">Pour un dossier source nommé Dossier1 et structuré comme suit :</span><span class="sxs-lookup"><span data-stu-id="09e51-281">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="09e51-282">Dossier1</span><span class="sxs-lookup"><span data-stu-id="09e51-282">Folder1</span></span><br/><span data-ttu-id="09e51-283">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="09e51-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="09e51-284">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="09e51-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="09e51-285">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="09e51-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="09e51-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="09e51-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="09e51-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="09e51-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="09e51-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="09e51-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="09e51-289">le dossier cible nommé Dossier1 est créé et structuré de la même manière que la source :</span><span class="sxs-lookup"><span data-stu-id="09e51-289">the target folder Folder1 is created with the same structure as the source:</span></span><br/><br/><span data-ttu-id="09e51-290">Dossier1</span><span class="sxs-lookup"><span data-stu-id="09e51-290">Folder1</span></span><br/><span data-ttu-id="09e51-291">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="09e51-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="09e51-292">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="09e51-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="09e51-293">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="09e51-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="09e51-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="09e51-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="09e51-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="09e51-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="09e51-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="09e51-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="09e51-297">true</span><span class="sxs-lookup"><span data-stu-id="09e51-297">true</span></span> |<span data-ttu-id="09e51-298">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="09e51-298">flattenHierarchy</span></span> |<span data-ttu-id="09e51-299">Pour un dossier source nommé Dossier1 et structuré comme suit :</span><span class="sxs-lookup"><span data-stu-id="09e51-299">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="09e51-300">Dossier1</span><span class="sxs-lookup"><span data-stu-id="09e51-300">Folder1</span></span><br/><span data-ttu-id="09e51-301">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="09e51-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="09e51-302">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="09e51-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="09e51-303">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="09e51-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="09e51-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="09e51-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="09e51-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="09e51-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="09e51-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="09e51-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="09e51-307">le dossier cible Dossier1 est créé et structuré comme suit :</span><span class="sxs-lookup"><span data-stu-id="09e51-307">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="09e51-308">Dossier1</span><span class="sxs-lookup"><span data-stu-id="09e51-308">Folder1</span></span><br/><span data-ttu-id="09e51-309">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier1</span><span class="sxs-lookup"><span data-stu-id="09e51-309">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="09e51-310">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier2</span><span class="sxs-lookup"><span data-stu-id="09e51-310">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="09e51-311">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier3</span><span class="sxs-lookup"><span data-stu-id="09e51-311">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="09e51-312">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier4</span><span class="sxs-lookup"><span data-stu-id="09e51-312">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="09e51-313">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier5</span><span class="sxs-lookup"><span data-stu-id="09e51-313">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="09e51-314">true</span><span class="sxs-lookup"><span data-stu-id="09e51-314">true</span></span> |<span data-ttu-id="09e51-315">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="09e51-315">mergeFiles</span></span> |<span data-ttu-id="09e51-316">Pour un dossier source nommé Dossier1 et structuré comme suit :</span><span class="sxs-lookup"><span data-stu-id="09e51-316">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="09e51-317">Dossier1</span><span class="sxs-lookup"><span data-stu-id="09e51-317">Folder1</span></span><br/><span data-ttu-id="09e51-318">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="09e51-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="09e51-319">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="09e51-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="09e51-320">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="09e51-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="09e51-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="09e51-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="09e51-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="09e51-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="09e51-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="09e51-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="09e51-324">le dossier cible Dossier1 est créé et structuré comme suit :</span><span class="sxs-lookup"><span data-stu-id="09e51-324">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="09e51-325">Dossier1</span><span class="sxs-lookup"><span data-stu-id="09e51-325">Folder1</span></span><br/><span data-ttu-id="09e51-326">&nbsp;&nbsp;&nbsp;&nbsp;Le contenu de Fichier1 + Fichier2 + Fichier3 + Fichier4 + Fichier5 est fusionné dans un fichier avec le nom de fichier généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="09e51-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span></span> |
| <span data-ttu-id="09e51-327">false</span><span class="sxs-lookup"><span data-stu-id="09e51-327">false</span></span> |<span data-ttu-id="09e51-328">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="09e51-328">preserveHierarchy</span></span> |<span data-ttu-id="09e51-329">Pour un dossier source nommé Dossier1 et structuré comme suit :</span><span class="sxs-lookup"><span data-stu-id="09e51-329">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="09e51-330">Dossier1</span><span class="sxs-lookup"><span data-stu-id="09e51-330">Folder1</span></span><br/><span data-ttu-id="09e51-331">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="09e51-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="09e51-332">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="09e51-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="09e51-333">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="09e51-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="09e51-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="09e51-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="09e51-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="09e51-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="09e51-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="09e51-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="09e51-337">le dossier cible nommé Dossier1 est créé et structuré comme suit :</span><span class="sxs-lookup"><span data-stu-id="09e51-337">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="09e51-338">Dossier1</span><span class="sxs-lookup"><span data-stu-id="09e51-338">Folder1</span></span><br/><span data-ttu-id="09e51-339">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="09e51-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="09e51-340">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="09e51-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="09e51-341">Sous-dossier1, où Fichier3, Fichier4 et Fichier5 ne sont pas sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="09e51-341">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="09e51-342">false</span><span class="sxs-lookup"><span data-stu-id="09e51-342">false</span></span> |<span data-ttu-id="09e51-343">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="09e51-343">flattenHierarchy</span></span> |<span data-ttu-id="09e51-344">Pour un dossier source nommé Dossier1 et structuré comme suit :</span><span class="sxs-lookup"><span data-stu-id="09e51-344">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="09e51-345">Dossier1</span><span class="sxs-lookup"><span data-stu-id="09e51-345">Folder1</span></span><br/><span data-ttu-id="09e51-346">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="09e51-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="09e51-347">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="09e51-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="09e51-348">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="09e51-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="09e51-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="09e51-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="09e51-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="09e51-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="09e51-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="09e51-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="09e51-352">le dossier cible nommé Dossier1 est créé et structuré comme suit :</span><span class="sxs-lookup"><span data-stu-id="09e51-352">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="09e51-353">Dossier1</span><span class="sxs-lookup"><span data-stu-id="09e51-353">Folder1</span></span><br/><span data-ttu-id="09e51-354">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier1</span><span class="sxs-lookup"><span data-stu-id="09e51-354">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="09e51-355">&nbsp;&nbsp;&nbsp;&nbsp;nom généré automatiquement pour Fichier2</span><span class="sxs-lookup"><span data-stu-id="09e51-355">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><span data-ttu-id="09e51-356">Sous-dossier1, où Fichier3, Fichier4 et Fichier5 ne sont pas sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="09e51-356">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="09e51-357">false</span><span class="sxs-lookup"><span data-stu-id="09e51-357">false</span></span> |<span data-ttu-id="09e51-358">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="09e51-358">mergeFiles</span></span> |<span data-ttu-id="09e51-359">Pour un dossier source nommé Dossier1 et structuré comme suit :</span><span class="sxs-lookup"><span data-stu-id="09e51-359">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="09e51-360">Dossier1</span><span class="sxs-lookup"><span data-stu-id="09e51-360">Folder1</span></span><br/><span data-ttu-id="09e51-361">&nbsp;&nbsp;&nbsp;&nbsp;Fichier1</span><span class="sxs-lookup"><span data-stu-id="09e51-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="09e51-362">&nbsp;&nbsp;&nbsp;&nbsp;Fichier2</span><span class="sxs-lookup"><span data-stu-id="09e51-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="09e51-363">&nbsp;&nbsp;&nbsp;&nbsp;Sousdossier1</span><span class="sxs-lookup"><span data-stu-id="09e51-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="09e51-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier3</span><span class="sxs-lookup"><span data-stu-id="09e51-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="09e51-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier4</span><span class="sxs-lookup"><span data-stu-id="09e51-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="09e51-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fichier5</span><span class="sxs-lookup"><span data-stu-id="09e51-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="09e51-367">le dossier cible nommé Dossier1 est créé et structuré comme suit :</span><span class="sxs-lookup"><span data-stu-id="09e51-367">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="09e51-368">Dossier1</span><span class="sxs-lookup"><span data-stu-id="09e51-368">Folder1</span></span><br/><span data-ttu-id="09e51-369">&nbsp;&nbsp;&nbsp;&nbsp;Le contenu de Fichier1 + Fichier2 est fusionné dans un fichier avec un nom de fichier généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="09e51-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span></span><br/><span data-ttu-id="09e51-370">&nbsp;&nbsp;&nbsp;&nbsp;Nom généré automatiquement pour Fichier1</span><span class="sxs-lookup"><span data-stu-id="09e51-370">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span></span><br/><br/><span data-ttu-id="09e51-371">Sous-dossier1, où Fichier3, Fichier4 et Fichier5 ne sont pas sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="09e51-371">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="09e51-372">Formats de fichier et de compression pris en charge</span><span class="sxs-lookup"><span data-stu-id="09e51-372">Supported file and compression formats</span></span>
<span data-ttu-id="09e51-373">Pour plus d’informations, voir [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="09e51-373">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples-for-copying-data-to-and-from-file-system"></a><span data-ttu-id="09e51-374">Exemples JSON pour copier des données vers et à partir d’un système de fichiers</span><span class="sxs-lookup"><span data-stu-id="09e51-374">JSON examples for copying data to and from file system</span></span>
<span data-ttu-id="09e51-375">Les exemples suivants présentent des exemples de définitions de JSON que vous pouvez utiliser pour créer un pipeline à l’aide [du Portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [de Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [d’Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="09e51-375">The following examples provide sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="09e51-376">Ils indiquent comment copier des données vers et depuis un système de fichiers local et Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="09e51-376">They show how to copy data to and from an on-premises file system and Azure Blob storage.</span></span> <span data-ttu-id="09e51-377">Toutefois, vous pouvez copier les données *directement* à partir de n’importe quelle source vers l’un des récepteurs répertoriés dans [Sources et récepteurs pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de l’activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="09e51-377">However, you can copy data *directly* from any of the sources to any of the sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-an-on-premises-file-system-to-azure-blob-storage"></a><span data-ttu-id="09e51-378">Exemple : copier des données d’un système de fichiers local vers Stockage Blob Azure</span><span class="sxs-lookup"><span data-stu-id="09e51-378">Example: Copy data from an on-premises file system to Azure Blob storage</span></span>
<span data-ttu-id="09e51-379">Cet exemple indique comment copier des données depuis un système de fichiers local vers Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="09e51-379">This sample shows how to copy data from an on-premises file system to Azure Blob storage.</span></span> <span data-ttu-id="09e51-380">L’exemple contient les entités Data Factory suivantes :</span><span class="sxs-lookup"><span data-stu-id="09e51-380">The sample has the following Data Factory entities:</span></span>

* <span data-ttu-id="09e51-381">Un service lié de type [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="09e51-381">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="09e51-382">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="09e51-382">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="09e51-383">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="09e51-383">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="09e51-384">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="09e51-384">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="09e51-385">Un [pipeline](data-factory-create-pipelines.md) avec activité de copie qui utilise [FileSystemSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="09e51-385">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="09e51-386">L’exemple suivant copie toutes les heures des données d’une série horaire d’un système de fichiers local vers Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="09e51-386">The following sample copies time-series data from an on-premises file system to Azure Blob storage every hour.</span></span> <span data-ttu-id="09e51-387">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="09e51-387">The JSON properties that are used in these samples are described in the sections after the samples.</span></span>

<span data-ttu-id="09e51-388">Pour commencer, configurez la passerelle de gestion des données selon les instructions décrites dans [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="09e51-388">As a first step, set up Data Management Gateway as per the instructions in [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span>

<span data-ttu-id="09e51-389">**Service lié de serveur de fichiers local :**</span><span class="sxs-lookup"><span data-stu-id="09e51-389">**On-Premises File Server linked service:**</span></span>

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

<span data-ttu-id="09e51-390">Nous vous recommandons d’utiliser la propriété **encryptedCredential** plutôt que les propriétés **userid** et **password**.</span><span class="sxs-lookup"><span data-stu-id="09e51-390">We recommend using the **encryptedCredential** property instead the **userid** and **password** properties.</span></span> <span data-ttu-id="09e51-391">Consultez la page [Service lié de serveur de fichiers](#linked-service-properties) pour plus d’informations sur ce service lié.</span><span class="sxs-lookup"><span data-stu-id="09e51-391">See [File Server linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="09e51-392">**Service lié Azure Storage :**</span><span class="sxs-lookup"><span data-stu-id="09e51-392">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="09e51-393">**Jeu de données d’entrée de système de fichiers local :**</span><span class="sxs-lookup"><span data-stu-id="09e51-393">**On-premises file system input dataset:**</span></span>

<span data-ttu-id="09e51-394">Les données sont récupérées à partir d’un nouveau fichier toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="09e51-394">Data is picked up from a new file every hour.</span></span> <span data-ttu-id="09e51-395">Les propriétés folderPath et fileName sont déterminées en fonction de l’heure de début de la tranche.</span><span class="sxs-lookup"><span data-stu-id="09e51-395">The folderPath and fileName properties are determined based on the start time of the slice.</span></span>  

<span data-ttu-id="09e51-396">La définition de `"external": "true"` informe Data Factory que le jeu de données est externe à la Data Factory et non produit par une activité dans la Data Factory.</span><span class="sxs-lookup"><span data-stu-id="09e51-396">Setting `"external": "true"` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="09e51-397">**Jeu de données de sortie Stockage Blob Azure :**</span><span class="sxs-lookup"><span data-stu-id="09e51-397">**Azure Blob storage output dataset:**</span></span>

<span data-ttu-id="09e51-398">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="09e51-398">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="09e51-399">Le chemin d’accès du dossier pour l’objet blob est évalué dynamiquement en fonction de l’heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="09e51-399">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="09e51-400">Le chemin d’accès du dossier utilise l’année, le mois, le jour et l’heure de l’heure de début.</span><span class="sxs-lookup"><span data-stu-id="09e51-400">The folder path uses the year, month, day, and hour parts of the start time.</span></span>

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

<span data-ttu-id="09e51-401">**Activité de copie dans un pipeline avec une source Système de fichiers et un récepteur blob :**</span><span class="sxs-lookup"><span data-stu-id="09e51-401">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="09e51-402">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d’entrée et de sortie, et qui est planifiée pour s’exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="09e51-402">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="09e51-403">Dans la définition du pipeline JSON, le type **source** est défini sur **FileSystemSource** et le type **sink** est défini sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="09e51-403">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span></span>

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

### <a name="example-copy-data-from-azure-sql-database-to-an-on-premises-file-system"></a><span data-ttu-id="09e51-404">Exemple : copier des données depuis Azure SQL Database vers un système de fichiers local</span><span class="sxs-lookup"><span data-stu-id="09e51-404">Example: Copy data from Azure SQL Database to an on-premises file system</span></span>
<span data-ttu-id="09e51-405">L’exemple suivant montre :</span><span class="sxs-lookup"><span data-stu-id="09e51-405">The following sample shows:</span></span>

* <span data-ttu-id="09e51-406">Un service lié de type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="09e51-406">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="09e51-407">Un service lié de type [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="09e51-407">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="09e51-408">Un jeu de données d’entrée de type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="09e51-408">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="09e51-409">Un jeu de données de sortie de type [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="09e51-409">An output dataset of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="09e51-410">Un pipeline avec une activité de copie qui utilise [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) et [FileSystemSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="09e51-410">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span></span>

<span data-ttu-id="09e51-411">L’exemple copie chaque heure des données de série horaire à partir d’une table SQL Azure vers un système de fichiers local.</span><span class="sxs-lookup"><span data-stu-id="09e51-411">The sample copies time-series data from an Azure SQL table to an on-premises file system every hour.</span></span> <span data-ttu-id="09e51-412">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="09e51-412">The JSON properties that are used in these samples are described in sections after the samples.</span></span>

<span data-ttu-id="09e51-413">**Service lié pour Azure SQL Database :**</span><span class="sxs-lookup"><span data-stu-id="09e51-413">**Azure SQL Database linked service:**</span></span>

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

<span data-ttu-id="09e51-414">**Service lié de serveur de fichiers local :**</span><span class="sxs-lookup"><span data-stu-id="09e51-414">**On-Premises File Server linked service:**</span></span>

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

<span data-ttu-id="09e51-415">Nous vous recommandons d’utiliser la propriété **encryptedCredential** plutôt que les propriétés **userid** et **password**.</span><span class="sxs-lookup"><span data-stu-id="09e51-415">We recommend using the **encryptedCredential** property instead of using the **userid** and **password** properties.</span></span> <span data-ttu-id="09e51-416">Consultez la page [Service lié de système de fichiers](#linked-service-properties) pour plus d’informations sur ce service lié.</span><span class="sxs-lookup"><span data-stu-id="09e51-416">See [File System linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="09e51-417">**Jeu de données d'entrée SQL Azure :**</span><span class="sxs-lookup"><span data-stu-id="09e51-417">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="09e51-418">L’exemple suppose que vous avez créé une table « MyTable » dans SQL Azure et qu’elle contient une colonne appelée « timestampcolumn » pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="09e51-418">The sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span></span>

<span data-ttu-id="09e51-419">La définition de ``“external”: ”true”`` informe Data Factory que le jeu de données est externe à la Data Factory et non produit par une activité dans la Data Factory.</span><span class="sxs-lookup"><span data-stu-id="09e51-419">Setting ``“external”: ”true”`` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="09e51-420">**Jeu de données de sortie de système de fichiers local :**</span><span class="sxs-lookup"><span data-stu-id="09e51-420">**On-premises file system output dataset:**</span></span>

<span data-ttu-id="09e51-421">Les données sont copiées vers un nouveau fichier toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="09e51-421">Data is copied to a new file every hour.</span></span> <span data-ttu-id="09e51-422">Les paramètres folderPath et fileName pour l’objet Blob sont déterminés en fonction de l’heure de début de la tranche.</span><span class="sxs-lookup"><span data-stu-id="09e51-422">The folderPath and fileName for the blob are determined based on the start time of the slice.</span></span>

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

<span data-ttu-id="09e51-423">**Activité de copie dans un pipeline avec une source SQL et un récepteur Système de fichiers :**</span><span class="sxs-lookup"><span data-stu-id="09e51-423">**A copy activity in a pipeline with SQL source and File System sink:**</span></span>

<span data-ttu-id="09e51-424">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d’entrée et de sortie, et qui est planifiée pour s’exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="09e51-424">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="09e51-425">Dans la définition JSON du pipeline, le type **source** est défini sur **SqlSource** et le type **sink** est défini sur **FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="09e51-425">In the pipeline JSON definition, the **source** type is set to **SqlSource**, and the **sink** type is set to **FileSystemSink**.</span></span> <span data-ttu-id="09e51-426">La requête SQL spécifiée pour la propriété **SqlReaderQuery** sélectionne les données de la dernière heure à copier.</span><span class="sxs-lookup"><span data-stu-id="09e51-426">The SQL query that is specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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


<span data-ttu-id="09e51-427">Vous pouvez également mapper les colonnes du jeu de données source aux colonnes du jeu de données récepteur dans la définition de l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="09e51-427">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="09e51-428">Pour plus d’informations, consultez [Mappage de colonnes de jeux de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="09e51-428">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="09e51-429">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="09e51-429">Performance and tuning</span></span>
 <span data-ttu-id="09e51-430">Consultez le [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="09e51-430">To learn about key factors that impact the performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>
