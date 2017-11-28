---
title: "Transfert de données à partir d’un HDFS en local | Microsoft Docs"
description: "Découvrez comment transférer des données à partir d’un HDFS en local à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 9a8f3156a62a1a7aa49377349e8a85454efeda50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a><span data-ttu-id="9463e-103">Transfert de données à partir d’un HDFS local à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9463e-103">Move data from on-premises HDFS using Azure Data Factory</span></span>
<span data-ttu-id="9463e-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour déplacer des données à partir d’un HDFS local.</span><span class="sxs-lookup"><span data-stu-id="9463e-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises HDFS.</span></span> <span data-ttu-id="9463e-105">Il s’appuie sur l’article [Activités de déplacement des données](data-factory-data-movement-activities.md), qui présente une vue d’ensemble du déplacement de données avec l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="9463e-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="9463e-106">Vous pouvez copier les données depuis HDFS vers tout magasin de données récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="9463e-106">You can copy data from HDFS to any supported sink data store.</span></span> <span data-ttu-id="9463e-107">Consultez le tableau [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) pour obtenir la liste des magasins de données pris en charge en tant que récepteurs par l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="9463e-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="9463e-108">Actuellement, Data Factory prend uniquement en charge le déplacement de données de HDFS en local vers d’autres magasins de données, mais pas l’inverse.</span><span class="sxs-lookup"><span data-stu-id="9463e-108">Data factory currently supports only moving data from an on-premises HDFS to other data stores, but not for moving data from other data stores to an on-premises HDFS.</span></span>

> [!NOTE]
> <span data-ttu-id="9463e-109">L’activité de copie ne supprime pas le fichier source une fois qu’il est copié sur la destination.</span><span class="sxs-lookup"><span data-stu-id="9463e-109">Copy Activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="9463e-110">Si vous devez supprimer le fichier source une fois qu’il est copié, créez une activité personnalisée pour supprimer le fichier et utilisez l’activité dans le pipeline.</span><span class="sxs-lookup"><span data-stu-id="9463e-110">If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="9463e-111">Activation de la connectivité</span><span class="sxs-lookup"><span data-stu-id="9463e-111">Enabling connectivity</span></span>
<span data-ttu-id="9463e-112">Le service Data Factory prend en charge la connexion à des sources HDFS locales à l’aide de la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="9463e-112">Data Factory service supports connecting to on-premises HDFS using the Data Management Gateway.</span></span> <span data-ttu-id="9463e-113">Consultez l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) pour en savoir plus sur la passerelle de gestion des données et obtenir des instructions détaillées sur la configuration de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="9463e-113">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="9463e-114">Utilisez la passerelle pour vous connecter à HDFS même si elle est hébergée sur des machines virtuelles IaaS Azure.</span><span class="sxs-lookup"><span data-stu-id="9463e-114">Use the gateway to connect to HDFS even if it is hosted in an Azure IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="9463e-115">Assurez-vous que la passerelle de gestion des données peut accéder à **TOUS** les éléments [serveur du nœud de nom]:[port du nœud de nom] et [serveurs du nœud de données]:[port du nœud de données] du cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9463e-115">Make sure the Data Management Gateway can access to **ALL** the [name node server]:[name node port] and [data node servers]:[data node port] of the Hadoop cluster.</span></span> <span data-ttu-id="9463e-116">Le [port du nœud de nom] par défaut est 50070 et le [port du nœud de données] par défaut est 50075.</span><span class="sxs-lookup"><span data-stu-id="9463e-116">Default [name node port] is 50070, and default [data node port] is 50075.</span></span>

<span data-ttu-id="9463e-117">Bien qu’il soit possible d’installer la passerelle sur le même ordinateur local ou la même machine virtuelle Azure que le HDFS, nous vous recommandons de l’installer sur un ordinateur ou une machine virtuelle IaaS Azure distinct(e).</span><span class="sxs-lookup"><span data-stu-id="9463e-117">While you can install gateway on the same on-premises machine or the Azure VM as the HDFS, we recommend that you install the gateway on a separate machine/Azure IaaS VM.</span></span> <span data-ttu-id="9463e-118">Disposer d’une passerelle sur un ordinateur distinct réduit les conflits de ressources et améliore les performances.</span><span class="sxs-lookup"><span data-stu-id="9463e-118">Having gateway on a separate machine reduces resource contention and improves performance.</span></span> <span data-ttu-id="9463e-119">Lorsque vous installez la passerelle sur un ordinateur distinct, l’ordinateur doit être en mesure d’accéder à l’ordinateur qui exécute le système HDFS.</span><span class="sxs-lookup"><span data-stu-id="9463e-119">When you install the gateway on a separate machine, the machine should be able to access the machine with the HDFS.</span></span>

## <a name="getting-started"></a><span data-ttu-id="9463e-120">Prise en main</span><span class="sxs-lookup"><span data-stu-id="9463e-120">Getting started</span></span>
<span data-ttu-id="9463e-121">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’une source HDFS à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="9463e-121">You can create a pipeline with a copy activity that moves data from a HDFS source by using different tools/APIs.</span></span>

<span data-ttu-id="9463e-122">Le moyen le plus simple de créer un pipeline consiste à utiliser **l’Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="9463e-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="9463e-123">Consultez la page [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant Copier des données.</span><span class="sxs-lookup"><span data-stu-id="9463e-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="9463e-124">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="9463e-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="9463e-125">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="9463e-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="9463e-126">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9463e-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="9463e-127">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="9463e-127">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="9463e-128">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="9463e-128">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="9463e-129">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="9463e-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="9463e-130">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="9463e-130">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="9463e-131">Lorsque vous utilisez des outils/API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory au format JSON.</span><span class="sxs-lookup"><span data-stu-id="9463e-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="9463e-132">Pour consulter un exemple contenant des définitions JSON pour les entités Data Factory utilisées pour copier des données d’un magasin de données HDFS local, consultez la section [Exemple JSON : copier des données depuis un HDFS local vers Azure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) de cet article.</span><span class="sxs-lookup"><span data-stu-id="9463e-132">For a sample with JSON definitions for Data Factory entities that are used to copy data from a HDFS data store, see [JSON example: Copy data from on-premises HDFS to Azure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) section of this article.</span></span>

<span data-ttu-id="9463e-133">Les sections suivantes fournissent des informations sur les propriétés JSON utilisées pour définir les entités Data Factory spécifiques à HDFS :</span><span class="sxs-lookup"><span data-stu-id="9463e-133">The following sections provide details about JSON properties that are used to define Data Factory entities specific to HDFS:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="9463e-134">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="9463e-134">Linked service properties</span></span>
<span data-ttu-id="9463e-135">Un service lié lie un magasin de données à une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="9463e-135">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="9463e-136">Vous créez un service lié de type **HDFS** pour lier un système HDFS local à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="9463e-136">You create a linked service of type **Hdfs** to link an on-premises HDFS to your data factory.</span></span> <span data-ttu-id="9463e-137">Le tableau suivant fournit la description des éléments JSON spécifiques au service lié HDFS.</span><span class="sxs-lookup"><span data-stu-id="9463e-137">The following table provides description for JSON elements specific to HDFS linked service.</span></span>

| <span data-ttu-id="9463e-138">Propriété</span><span class="sxs-lookup"><span data-stu-id="9463e-138">Property</span></span> | <span data-ttu-id="9463e-139">Description</span><span class="sxs-lookup"><span data-stu-id="9463e-139">Description</span></span> | <span data-ttu-id="9463e-140">Requis</span><span class="sxs-lookup"><span data-stu-id="9463e-140">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9463e-141">type</span><span class="sxs-lookup"><span data-stu-id="9463e-141">type</span></span> |<span data-ttu-id="9463e-142">La propriété de type doit être définie sur **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="9463e-142">The type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="9463e-143">Oui</span><span class="sxs-lookup"><span data-stu-id="9463e-143">Yes</span></span> |
| <span data-ttu-id="9463e-144">Url</span><span class="sxs-lookup"><span data-stu-id="9463e-144">Url</span></span> |<span data-ttu-id="9463e-145">URL vers le système HDFS</span><span class="sxs-lookup"><span data-stu-id="9463e-145">URL to the HDFS</span></span> |<span data-ttu-id="9463e-146">Oui</span><span class="sxs-lookup"><span data-stu-id="9463e-146">Yes</span></span> |
| <span data-ttu-id="9463e-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="9463e-147">authenticationType</span></span> |<span data-ttu-id="9463e-148">Anonyme ou Windows.</span><span class="sxs-lookup"><span data-stu-id="9463e-148">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="9463e-149">Pour utiliser l’**authentification Kerberos** pour le connecteur HDFS, reportez-vous à [cette section](#use-kerberos-authentication-for-hdfs-connector) pour configurer votre environnement local en conséquence.</span><span class="sxs-lookup"><span data-stu-id="9463e-149">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span></span> |<span data-ttu-id="9463e-150">Oui</span><span class="sxs-lookup"><span data-stu-id="9463e-150">Yes</span></span> |
| <span data-ttu-id="9463e-151">userName</span><span class="sxs-lookup"><span data-stu-id="9463e-151">userName</span></span> |<span data-ttu-id="9463e-152">Nom d’utilisateur de l’authentification Windows</span><span class="sxs-lookup"><span data-stu-id="9463e-152">Username for Windows authentication.</span></span> |<span data-ttu-id="9463e-153">Oui (pour l’authentification Windows)</span><span class="sxs-lookup"><span data-stu-id="9463e-153">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="9463e-154">password</span><span class="sxs-lookup"><span data-stu-id="9463e-154">password</span></span> |<span data-ttu-id="9463e-155">Mot de passe de l’authentification Windows</span><span class="sxs-lookup"><span data-stu-id="9463e-155">Password for Windows authentication.</span></span> |<span data-ttu-id="9463e-156">Oui (pour l’authentification Windows)</span><span class="sxs-lookup"><span data-stu-id="9463e-156">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="9463e-157">gatewayName</span><span class="sxs-lookup"><span data-stu-id="9463e-157">gatewayName</span></span> |<span data-ttu-id="9463e-158">Nom de la passerelle que le service Data Factory doit utiliser pour se connecter au système HDFS.</span><span class="sxs-lookup"><span data-stu-id="9463e-158">Name of the gateway that the Data Factory service should use to connect to the HDFS.</span></span> |<span data-ttu-id="9463e-159">Oui</span><span class="sxs-lookup"><span data-stu-id="9463e-159">Yes</span></span> |
| <span data-ttu-id="9463e-160">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="9463e-160">encryptedCredential</span></span> |<span data-ttu-id="9463e-161">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) des informations d’accès.</span><span class="sxs-lookup"><span data-stu-id="9463e-161">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of the access credential.</span></span> |<span data-ttu-id="9463e-162">Non</span><span class="sxs-lookup"><span data-stu-id="9463e-162">No</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="9463e-163">Utilisation de l’authentification anonyme</span><span class="sxs-lookup"><span data-stu-id="9463e-163">Using Anonymous authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a><span data-ttu-id="9463e-164">Utilisation de l’authentification Windows</span><span class="sxs-lookup"><span data-stu-id="9463e-164">Using Windows authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a><span data-ttu-id="9463e-165">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="9463e-165">Dataset properties</span></span>
<span data-ttu-id="9463e-166">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="9463e-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="9463e-167">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="9463e-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="9463e-168">La section **typeProperties** est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="9463e-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="9463e-169">La section typeProperties du jeu de données de type **FileShare** (comprenant le jeu de données HDFS) présente les propriétés suivantes</span><span class="sxs-lookup"><span data-stu-id="9463e-169">The typeProperties section for dataset of type **FileShare** (which includes HDFS dataset) has the following properties</span></span>

| <span data-ttu-id="9463e-170">Propriété</span><span class="sxs-lookup"><span data-stu-id="9463e-170">Property</span></span> | <span data-ttu-id="9463e-171">Description</span><span class="sxs-lookup"><span data-stu-id="9463e-171">Description</span></span> | <span data-ttu-id="9463e-172">Requis</span><span class="sxs-lookup"><span data-stu-id="9463e-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9463e-173">folderPath</span><span class="sxs-lookup"><span data-stu-id="9463e-173">folderPath</span></span> |<span data-ttu-id="9463e-174">Chemin d'accès au dossier.</span><span class="sxs-lookup"><span data-stu-id="9463e-174">Path to the folder.</span></span> <span data-ttu-id="9463e-175">Exemple : `myfolder`</span><span class="sxs-lookup"><span data-stu-id="9463e-175">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="9463e-176">Utilisez le caractère d’échappement « \ » pour les caractères spéciaux contenus dans la chaîne.</span><span class="sxs-lookup"><span data-stu-id="9463e-176">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="9463e-177">Par exemple : pour dossier\sous-dossier, spécifiez dossier\\\\sous-dossier et pour d:\dossier d’exemple, spécifiez d:\\\\dossier d’exemple.</span><span class="sxs-lookup"><span data-stu-id="9463e-177">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="9463e-178">Vous pouvez également effectuer une combinaison avec la propriété **partitionBy** pour que les chemins d’accès de dossier soient basés sur les dates et heures de démarrage et d’arrêt de la tranche.</span><span class="sxs-lookup"><span data-stu-id="9463e-178">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="9463e-179">Oui</span><span class="sxs-lookup"><span data-stu-id="9463e-179">Yes</span></span> |
| <span data-ttu-id="9463e-180">fileName</span><span class="sxs-lookup"><span data-stu-id="9463e-180">fileName</span></span> |<span data-ttu-id="9463e-181">Spécifiez le nom du fichier dans l’élément **folderPath** si vous souhaitez que la table se réfère à un fichier spécifique du dossier.</span><span class="sxs-lookup"><span data-stu-id="9463e-181">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="9463e-182">Si vous ne spécifiez aucune valeur pour cette propriété, le tableau pointe vers tous les fichiers du dossier.</span><span class="sxs-lookup"><span data-stu-id="9463e-182">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="9463e-183">Lorsque fileName n’est pas spécifié pour un jeu de données de sortie, le nom du fichier généré aura ce format dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="9463e-183">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="9463e-184">Data<Guid>.txt (par exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="9463e-184">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="9463e-185">Non</span><span class="sxs-lookup"><span data-stu-id="9463e-185">No</span></span> |
| <span data-ttu-id="9463e-186">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="9463e-186">partitionedBy</span></span> |<span data-ttu-id="9463e-187">partitionedBy peut être utilisé pour spécifier un folderPath dynamique, fileName pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="9463e-187">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="9463e-188">Exemple : folderPath peut être paramétré pour toutes les heures de données.</span><span class="sxs-lookup"><span data-stu-id="9463e-188">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="9463e-189">Non</span><span class="sxs-lookup"><span data-stu-id="9463e-189">No</span></span> |
| <span data-ttu-id="9463e-190">format</span><span class="sxs-lookup"><span data-stu-id="9463e-190">format</span></span> | <span data-ttu-id="9463e-191">Les types de formats suivants sont pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="9463e-191">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="9463e-192">Définissez la propriété **type** située sous Format sur l’une de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="9463e-192">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="9463e-193">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="9463e-193">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="9463e-194">Si vous souhaitez **copier des fichiers en l’état** entre des magasins de fichiers (copie binaire), ignorez la section Format dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="9463e-194">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="9463e-195">Non</span><span class="sxs-lookup"><span data-stu-id="9463e-195">No</span></span> |
| <span data-ttu-id="9463e-196">compression</span><span class="sxs-lookup"><span data-stu-id="9463e-196">compression</span></span> | <span data-ttu-id="9463e-197">Spécifiez le type et le niveau de compression pour les données.</span><span class="sxs-lookup"><span data-stu-id="9463e-197">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="9463e-198">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="9463e-198">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="9463e-199">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="9463e-199">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="9463e-200">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="9463e-200">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="9463e-201">Non</span><span class="sxs-lookup"><span data-stu-id="9463e-201">No</span></span> |

> [!NOTE]
> <span data-ttu-id="9463e-202">fileName et fileFilter ne peuvent pas être utilisés simultanément.</span><span class="sxs-lookup"><span data-stu-id="9463e-202">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="9463e-203">Utilisation de la propriété partitionedBy</span><span class="sxs-lookup"><span data-stu-id="9463e-203">Using partionedBy property</span></span>
<span data-ttu-id="9463e-204">Comme mentionné dans la section précédente, vous pouvez spécifier un folderPath et un fileName dynamiques pour les données de série chronologique avec la propriété **partitionedBy**, [les fonctions Data Factory et les variables système](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="9463e-204">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="9463e-205">Consultez les articles [Création de jeux de données](data-factory-create-datasets.md), [Planification et exécution](data-factory-scheduling-and-execution.md) et [Création de pipelines](data-factory-create-pipelines.md) pour en savoir plus sur les jeux de données de série chronologique, la planification et les segments.</span><span class="sxs-lookup"><span data-stu-id="9463e-205">To learn more about time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="9463e-206">Exemple 1 :</span><span class="sxs-lookup"><span data-stu-id="9463e-206">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="9463e-207">Dans cet exemple, {Slice} est remplacé par la valeur de la variable système Data Factory SliceStart au format (AAAAMMJJHH) spécifié.</span><span class="sxs-lookup"><span data-stu-id="9463e-207">In this example {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="9463e-208">SliceStart fait référence à l'heure de début du segment.</span><span class="sxs-lookup"><span data-stu-id="9463e-208">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="9463e-209">folderPath est différent pour chaque segment.</span><span class="sxs-lookup"><span data-stu-id="9463e-209">The folderPath is different for each slice.</span></span> <span data-ttu-id="9463e-210">Par exemple : wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="9463e-210">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="9463e-211">Exemple 2 :</span><span class="sxs-lookup"><span data-stu-id="9463e-211">Sample 2:</span></span>

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
<span data-ttu-id="9463e-212">Dans cet exemple, l'année, le mois, le jour et l'heure de SliceStart sont extraits dans des variables distinctes qui sont utilisées par les propriétés folderPath et fileName.</span><span class="sxs-lookup"><span data-stu-id="9463e-212">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="9463e-213">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="9463e-213">Copy activity properties</span></span>
<span data-ttu-id="9463e-214">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="9463e-214">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="9463e-215">Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités.</span><span class="sxs-lookup"><span data-stu-id="9463e-215">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="9463e-216">En revanche, les propriétés disponibles dans la section typeProperties de l’activité varient pour chaque type d'activité.</span><span class="sxs-lookup"><span data-stu-id="9463e-216">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="9463e-217">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="9463e-217">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="9463e-218">Pour une activité de copie, quand la source est de type **FileSystemSource** , les propriétés suivantes sont disponibles dans la section typeProperties :</span><span class="sxs-lookup"><span data-stu-id="9463e-218">For Copy Activity, when source is of type **FileSystemSource** the following properties are available in typeProperties section:</span></span>

<span data-ttu-id="9463e-219">**FileSystemSource** prend en charge les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="9463e-219">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="9463e-220">Propriété</span><span class="sxs-lookup"><span data-stu-id="9463e-220">Property</span></span> | <span data-ttu-id="9463e-221">Description</span><span class="sxs-lookup"><span data-stu-id="9463e-221">Description</span></span> | <span data-ttu-id="9463e-222">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="9463e-222">Allowed values</span></span> | <span data-ttu-id="9463e-223">Requis</span><span class="sxs-lookup"><span data-stu-id="9463e-223">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9463e-224">recursive</span><span class="sxs-lookup"><span data-stu-id="9463e-224">recursive</span></span> |<span data-ttu-id="9463e-225">Indique si les données sont lues de manière récursive dans les sous-dossiers ou uniquement dans le dossier spécifié.</span><span class="sxs-lookup"><span data-stu-id="9463e-225">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="9463e-226">True, False (par défaut)</span><span class="sxs-lookup"><span data-stu-id="9463e-226">True, False (default)</span></span> |<span data-ttu-id="9463e-227">Non</span><span class="sxs-lookup"><span data-stu-id="9463e-227">No</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="9463e-228">Formats de fichier et de compression pris en charge</span><span class="sxs-lookup"><span data-stu-id="9463e-228">Supported file and compression formats</span></span>
<span data-ttu-id="9463e-229">Pour plus d’informations, consultez l’article [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="9463e-229">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-on-premises-hdfs-to-azure-blob"></a><span data-ttu-id="9463e-230">Exemple JSON : copie de données entre un système HDFS local et un objet blob Azure</span><span class="sxs-lookup"><span data-stu-id="9463e-230">JSON example: Copy data from on-premises HDFS to Azure Blob</span></span>
<span data-ttu-id="9463e-231">Cet exemple indique comment copier des données depuis un système HDFS local vers un système Blob Storage Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9463e-231">This sample shows how to copy data from an on-premises HDFS to Azure Blob Storage.</span></span> <span data-ttu-id="9463e-232">Toutefois, les données peuvent être copiées **directement** vers l’un des récepteurs indiqués [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) , via l’activité de copie d’Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9463e-232">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="9463e-233">Cet exemple fournit des définitions JSON pour les entités Data Factory suivantes.</span><span class="sxs-lookup"><span data-stu-id="9463e-233">The sample provides JSON definitions for the following Data Factory entities.</span></span> <span data-ttu-id="9463e-234">Vous pouvez utiliser ces définitions pour créer un pipeline afin de copier des données depuis HDFS vers un Stockage Blob Azure à l’aide du [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), de [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [d’Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9463e-234">You can use these definitions to create a pipeline to copy data from HDFS to Azure Blob Storage by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

1. <span data-ttu-id="9463e-235">Un service lié de type [OnPremisesHdfs](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9463e-235">A linked service of type [OnPremisesHdfs](#linked-service-properties).</span></span>
2. <span data-ttu-id="9463e-236">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9463e-236">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="9463e-237">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9463e-237">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
4. <span data-ttu-id="9463e-238">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9463e-238">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="9463e-239">Un [pipeline](data-factory-create-pipelines.md) avec activité de copie qui utilise [FileSystemSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="9463e-239">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="9463e-240">L’exemple copie toutes les heures les données d’un système HDFS en local vers un objet Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="9463e-240">The sample copies data from an on-premises HDFS to an Azure blob every hour.</span></span> <span data-ttu-id="9463e-241">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="9463e-241">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="9463e-242">Dans un premier temps, configurez la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="9463e-242">As a first step, set up the data management gateway.</span></span> <span data-ttu-id="9463e-243">Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="9463e-243">The instructions in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="9463e-244">**Service lié de HDFS :** cet exemple utilise l’authentification Windows.</span><span class="sxs-lookup"><span data-stu-id="9463e-244">**HDFS linked service:** This example uses the Windows authentication.</span></span> <span data-ttu-id="9463e-245">Consultez la section [Service lié HDFS](#linked-service-properties) pour connaître les différents types d’authentification que vous pouvez utiliser.</span><span class="sxs-lookup"><span data-stu-id="9463e-245">See [HDFS linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="9463e-246">**Service lié Azure Storage :**</span><span class="sxs-lookup"><span data-stu-id="9463e-246">**Azure Storage linked service:**</span></span>

```JSON
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

<span data-ttu-id="9463e-247">**Jeu de données d’entrée HDFS :** ce jeu de données fait référence au dossier HDFS DataTransfer/UnitTest/.</span><span class="sxs-lookup"><span data-stu-id="9463e-247">**HDFS input dataset:** This dataset refers to the HDFS folder DataTransfer/UnitTest/.</span></span> <span data-ttu-id="9463e-248">Le pipeline copie tous les fichiers de son dossier vers la destination.</span><span class="sxs-lookup"><span data-stu-id="9463e-248">The pipeline copies all the files in this folder to the destination.</span></span>

<span data-ttu-id="9463e-249">La définition de « external » : « true» informe le service Data Factory qu’il s’agit d’un jeu de données qui est externe à Data Factory et non produit par une activité dans Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9463e-249">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

<span data-ttu-id="9463e-250">**Jeu de données de sortie Azure Blob :**</span><span class="sxs-lookup"><span data-stu-id="9463e-250">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="9463e-251">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="9463e-251">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="9463e-252">Le chemin d’accès du dossier pour l’objet blob est évalué dynamiquement en fonction de l’heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="9463e-252">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="9463e-253">Le chemin d'accès du dossier utilise l'année, le mois, le jour et l'heure de l'heure de début.</span><span class="sxs-lookup"><span data-stu-id="9463e-253">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="9463e-254">**Activité de copie dans un pipeline avec une source Système de fichiers et un récepteur blob :**</span><span class="sxs-lookup"><span data-stu-id="9463e-254">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="9463e-255">Le pipeline contient une activité de copie qui est configurée pour utiliser ces jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="9463e-255">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="9463e-256">Dans la définition du pipeline JSON, le type **source** est défini sur **FileSystemSource** et le type **sink** est défini sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="9463e-256">In the pipeline JSON definition, the **source** type is set to **FileSystemSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="9463e-257">La requête SQL spécifiée pour la propriété **query** sélectionne les données de la dernière heure à copier.</span><span class="sxs-lookup"><span data-stu-id="9463e-257">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a><span data-ttu-id="9463e-258">Utilisation de l’authentification Kerberos pour le connecteur HDFS</span><span class="sxs-lookup"><span data-stu-id="9463e-258">Use Kerberos authentication for HDFS connector</span></span>
<span data-ttu-id="9463e-259">Il existe deux options de configuration de l’environnement local afin d’utiliser l’authentification Kerberos dans le connecteur HDFS.</span><span class="sxs-lookup"><span data-stu-id="9463e-259">There are two options to set up the on-premises environment so as to use Kerberos Authentication in HDFS connector.</span></span> <span data-ttu-id="9463e-260">Vous pouvez choisir celle qui correspond mieux à votre situation.</span><span class="sxs-lookup"><span data-stu-id="9463e-260">You can choose the one better fits your case.</span></span>
* <span data-ttu-id="9463e-261">Option 1 : [Joindre l’ordinateur de la passerelle au domaine Kerberos](#kerberos-join-realm)</span><span class="sxs-lookup"><span data-stu-id="9463e-261">Option 1: [Join gateway machine in Kerberos realm](#kerberos-join-realm)</span></span>
* <span data-ttu-id="9463e-262">Option 2 : [activer l’approbation mutuelle entre le domaine Windows et le domaine Kerberos](#kerberos-mutual-trust)</span><span class="sxs-lookup"><span data-stu-id="9463e-262">Option 2: [Enable mutual trust between Windows domain and Kerberos realm](#kerberos-mutual-trust)</span></span>

### <span data-ttu-id="9463e-263"><a name="kerberos-join-realm"></a>Option 1 : Joindre l’ordinateur de la passerelle au domaine Kerberos</span><span class="sxs-lookup"><span data-stu-id="9463e-263"><a name="kerberos-join-realm"></a>Option 1: Join gateway machine in Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="9463e-264">Condition :</span><span class="sxs-lookup"><span data-stu-id="9463e-264">Requirement:</span></span>

* <span data-ttu-id="9463e-265">L’ordinateur de passerelle doit rejoindre le domaine Kerberos et ne peut rejoindre aucun domaine Windows.</span><span class="sxs-lookup"><span data-stu-id="9463e-265">The gateway machine needs to join the Kerberos realm and can’t join any Windows domain.</span></span>

#### <a name="how-to-configure"></a><span data-ttu-id="9463e-266">Procédure de configuration :</span><span class="sxs-lookup"><span data-stu-id="9463e-266">How to configure:</span></span>

<span data-ttu-id="9463e-267">**Sur l’ordinateur de la passerelle :**</span><span class="sxs-lookup"><span data-stu-id="9463e-267">**On gateway machine:**</span></span>

1.  <span data-ttu-id="9463e-268">Exécutez l’utilitaire **Ksetup** pour configurer le serveur Kerberos KDC et le domaine.</span><span class="sxs-lookup"><span data-stu-id="9463e-268">Run the **Ksetup** utility to configure the Kerberos KDC server and realm.</span></span>

    <span data-ttu-id="9463e-269">L’ordinateur doit être configuré en tant que membre d’un groupe de travail, car un domaine Kerberos est différent d’un domaine Windows.</span><span class="sxs-lookup"><span data-stu-id="9463e-269">The machine must be configured as a member of a workgroup since a Kerberos realm is different from a Windows domain.</span></span> <span data-ttu-id="9463e-270">Pour ce faire, définissez le domaine Kerberos et ajoutez un serveur KDC comme suit.</span><span class="sxs-lookup"><span data-stu-id="9463e-270">This can be achieved by setting the Kerberos realm and adding a KDC server as follows.</span></span> <span data-ttu-id="9463e-271">Remplacez *REALM.COM* par votre propre domaine respectif en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="9463e-271">Replace *REALM.COM* with your own respective realm as needed.</span></span>

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    <span data-ttu-id="9463e-272">**Redémarrez** l’ordinateur après avoir exécuté ces 2 commandes.</span><span class="sxs-lookup"><span data-stu-id="9463e-272">**Restart** the machine after executing these 2 commands.</span></span>

2.  <span data-ttu-id="9463e-273">Vérifiez la configuration avec la commande **Ksetup**.</span><span class="sxs-lookup"><span data-stu-id="9463e-273">Verify the configuration with **Ksetup** command.</span></span> <span data-ttu-id="9463e-274">La sortie doit être semblable à :</span><span class="sxs-lookup"><span data-stu-id="9463e-274">The output should be like:</span></span>

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

<span data-ttu-id="9463e-275">**Dans Azure Data Factory :**</span><span class="sxs-lookup"><span data-stu-id="9463e-275">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="9463e-276">Configurez le connecteur HDFS à l’aide de l’**authentification Windows** avec votre nom principal Kerberos et le mot de passe pour vous connecter à la source de données HDFS.</span><span class="sxs-lookup"><span data-stu-id="9463e-276">Configure the HDFS connector using **Windows authentication** together with your Kerberos principal name and password to connect to the HDFS data source.</span></span> <span data-ttu-id="9463e-277">Vérifiez les détails de configuration dans la section sur les [propriétés du service lié HDFS](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9463e-277">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

### <span data-ttu-id="9463e-278"><a name="kerberos-mutual-trust"></a>Option 2 : activer l’approbation mutuelle entre le domaine Windows et le domaine Kerberos</span><span class="sxs-lookup"><span data-stu-id="9463e-278"><a name="kerberos-mutual-trust"></a>Option 2: Enable mutual trust between Windows domain and Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="9463e-279">Condition :</span><span class="sxs-lookup"><span data-stu-id="9463e-279">Requirement:</span></span>
*   <span data-ttu-id="9463e-280">L’ordinateur de passerelle doit rejoindre un domaine Windows.</span><span class="sxs-lookup"><span data-stu-id="9463e-280">The gateway machine must join a Windows domain.</span></span>
*   <span data-ttu-id="9463e-281">Vous avez besoin d’autorisations pour mettre à jour les paramètres du contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="9463e-281">You need permission to update the domain controller's settings.</span></span>

#### <a name="how-to-configure"></a><span data-ttu-id="9463e-282">Procédure de configuration :</span><span class="sxs-lookup"><span data-stu-id="9463e-282">How to configure:</span></span>

> [!NOTE]
> <span data-ttu-id="9463e-283">Remplacez REALM.COM et AD.COM dans le didacticiel suivant par votre propre domaine et contrôleur de domaine respectifs en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="9463e-283">Replace REALM.COM and AD.COM in the following tutorial with your own respective realm and domain controller as needed.</span></span>

<span data-ttu-id="9463e-284">**Sur le serveur KDC :**</span><span class="sxs-lookup"><span data-stu-id="9463e-284">**On KDC server:**</span></span>

1.  <span data-ttu-id="9463e-285">Modifiez la configuration KDC dans le fichier **krb5.conf** afin de permettre au KDC d’approuver le domaine Windows faisant référence au modèle de configuration suivant.</span><span class="sxs-lookup"><span data-stu-id="9463e-285">Edit the KDC configuration in **krb5.conf** file to let KDC trust Windows Domain referring to the following configuration template.</span></span> <span data-ttu-id="9463e-286">Par défaut, la configuration se trouve dans **/etc/krb5.conf**.</span><span class="sxs-lookup"><span data-stu-id="9463e-286">By default, the configuration is located at **/etc/krb5.conf**.</span></span>

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  <span data-ttu-id="9463e-287">**Redémarrez** le service KDC après la configuration.</span><span class="sxs-lookup"><span data-stu-id="9463e-287">**Restart** the KDC service after configuration.</span></span>

2.  <span data-ttu-id="9463e-288">Préparez un fichier principal nommé **krbtgt/REALM.COM@AD.COM** dans le serveur KDC avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9463e-288">Prepare a principal named **krbtgt/REALM.COM@AD.COM** in KDC server with the following command:</span></span>

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  <span data-ttu-id="9463e-289">Dans le fichier de configuration du service HDFS **hadoop.security.auth_to_local**, ajoutez `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span><span class="sxs-lookup"><span data-stu-id="9463e-289">In **hadoop.security.auth_to_local** HDFS service configuration file, add `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span></span>

<span data-ttu-id="9463e-290">**Sur le contrôleur de domaine :**</span><span class="sxs-lookup"><span data-stu-id="9463e-290">**On domain controller:**</span></span>

1.  <span data-ttu-id="9463e-291">Exécutez les commandes **Ksetup** suivantes pour ajouter une entrée de domaine :</span><span class="sxs-lookup"><span data-stu-id="9463e-291">Run the following **Ksetup** commands to add a realm entry:</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  <span data-ttu-id="9463e-292">Établir l’approbation entre le domaine Windows et le domaine Kerberos.</span><span class="sxs-lookup"><span data-stu-id="9463e-292">Establish trust from Windows Domain to Kerberos Realm.</span></span> <span data-ttu-id="9463e-293">[password] correspond au mot de passe pour le principal  **krbtgt/REALM.COM@AD.COM** .</span><span class="sxs-lookup"><span data-stu-id="9463e-293">[password] is the password for the principal **krbtgt/REALM.COM@AD.COM**.</span></span>

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  <span data-ttu-id="9463e-294">Sélectionnez l’algorithme de chiffrement utilisé dans Kerberos.</span><span class="sxs-lookup"><span data-stu-id="9463e-294">Select encryption algorithm used in Kerberos.</span></span>

    1. <span data-ttu-id="9463e-295">Accédez à Gestionnaire de serveur > Gestion des stratégies de groupe > Domaine > Objets de stratégie de groupe > Stratégie de domaine par défaut ou actif, puis Modifier.</span><span class="sxs-lookup"><span data-stu-id="9463e-295">Go to Server Manager > Group Policy Management > Domain > Group Policy Objects > Default or Active Domain Policy, and Edit.</span></span>

    2. <span data-ttu-id="9463e-296">Dans la fenêtre contextuelle **Éditeur de gestion des stratégies de groupe**, accédez à Configuration ordinateur > Stratégies > Paramètres Windows > Paramètres de sécurité > Stratégies locales > Options de sécurité, puis configurez **Sécurité réseau : Configurer les types de chiffrement autorisés pour Kerberos**.</span><span class="sxs-lookup"><span data-stu-id="9463e-296">In the **Group Policy Management Editor** popup window, go to Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options, and configure **Network security: Configure Encryption types allowed for Kerberos**.</span></span>

    3. <span data-ttu-id="9463e-297">Sélectionnez l’algorithme de chiffrement à utiliser pour vous connecter à KDC.</span><span class="sxs-lookup"><span data-stu-id="9463e-297">Select the encryption algorithm you want to use when connect to KDC.</span></span> <span data-ttu-id="9463e-298">En règle générale, vous pouvez simplement sélectionner toutes les options.</span><span class="sxs-lookup"><span data-stu-id="9463e-298">Commonly, you can simply select all the options.</span></span>

        ![Configuration des types de chiffrement pour Kerberos](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. <span data-ttu-id="9463e-300">Utilisez la commande **Ksetup** pour spécifier l’algorithme de chiffrement à utiliser dans le domaine spécifique.</span><span class="sxs-lookup"><span data-stu-id="9463e-300">Use **Ksetup** command to specify the encryption algorithm to be used on the specific REALM.</span></span>

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  <span data-ttu-id="9463e-301">Créez le mappage entre le compte de domaine et le principal Kerberos afin de pouvoir utiliser le principal Kerberos dans un domaine Windows.</span><span class="sxs-lookup"><span data-stu-id="9463e-301">Create the mapping between the domain account and Kerberos principal, in order to use Kerberos principal in Windows Domain.</span></span>

    1. <span data-ttu-id="9463e-302">Démarrez Outils d’administration > **Utilisateurs et ordinateurs Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9463e-302">Start the Administrative tools > **Active Directory Users and Computers**.</span></span>

    2. <span data-ttu-id="9463e-303">Pour configurer les fonctionnalités avancées, cliquez sur **Affichage** > **Fonctionnalités avancées**.</span><span class="sxs-lookup"><span data-stu-id="9463e-303">Configure advanced features by clicking **View** > **Advanced Features**.</span></span>

    3. <span data-ttu-id="9463e-304">Recherchez le compte pour lequel vous souhaitez créer des mappages, cliquez avec le bouton droit pour afficher **Mappages des noms** > cliquez sur l’onglet **Noms Kerberos**.</span><span class="sxs-lookup"><span data-stu-id="9463e-304">Locate the account to which you want to create mappings, and right-click to view **Name Mappings** > click **Kerberos Names** tab.</span></span>

    4. <span data-ttu-id="9463e-305">Ajoutez un principal provenant du domaine.</span><span class="sxs-lookup"><span data-stu-id="9463e-305">Add a principal from the realm.</span></span>

        ![Mappage des identités de sécurité](media/data-factory-hdfs-connector/map-security-identity.png)

<span data-ttu-id="9463e-307">**Sur l’ordinateur de la passerelle :**</span><span class="sxs-lookup"><span data-stu-id="9463e-307">**On gateway machine:**</span></span>

* <span data-ttu-id="9463e-308">Exécutez les commandes **Ksetup** suivantes pour ajouter une entrée de domaine.</span><span class="sxs-lookup"><span data-stu-id="9463e-308">Run the following **Ksetup** commands to add a realm entry.</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

<span data-ttu-id="9463e-309">**Dans Azure Data Factory :**</span><span class="sxs-lookup"><span data-stu-id="9463e-309">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="9463e-310">Configurez le connecteur HDFS à l’aide de l’**authentification Windows** avec votre compte de domaine ou le principal Kerberos pour vous connecter à la source de données HDFS.</span><span class="sxs-lookup"><span data-stu-id="9463e-310">Configure the HDFS connector using **Windows authentication** together with either your Domain Account or Kerberos Principal to connect to the HDFS data source.</span></span> <span data-ttu-id="9463e-311">Vérifiez les détails de configuration dans la section sur les [propriétés du service lié HDFS](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9463e-311">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

> [!NOTE]
> <span data-ttu-id="9463e-312">Pour savoir comment mapper des colonnes d’un jeu de données source à des colonnes d’un jeu de données récepteur, consultez [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Mappage des colonnes des jeux de données dans Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="9463e-312">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="performance-and-tuning"></a><span data-ttu-id="9463e-313">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="9463e-313">Performance and Tuning</span></span>
<span data-ttu-id="9463e-314">Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="9463e-314">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
