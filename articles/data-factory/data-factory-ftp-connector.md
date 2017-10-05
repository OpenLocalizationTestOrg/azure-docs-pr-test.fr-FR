---
title: "Déplacer des données à partir d’un serveur FTP à l’aide d’Azure Data Factory | Microsoft Docs"
description: "Découvrez comment déplacer des données depuis un serveur FTP à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: f8f31f3a2ee02c964737dd32145499f3dcfd0624
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="af20e-103">Déplacer des données à partir d’un serveur FTP à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="af20e-103">Move data from an FTP server by using Azure Data Factory</span></span>
<span data-ttu-id="af20e-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour déplacer des données à partir d’un serveur FTP.</span><span class="sxs-lookup"><span data-stu-id="af20e-104">This article explains how to use the copy activity in Azure Data Factory to move data from an FTP server.</span></span> <span data-ttu-id="af20e-105">Il s’appuie sur l’article relatif aux [activités de déplacement des données](data-factory-data-movement-activities.md), qui présente une vue d’ensemble du déplacement des données avec l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="af20e-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="af20e-106">Vous pouvez copier les données d’un serveur FTP dans tout magasin de données récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="af20e-106">You can copy data from an FTP server to any supported sink data store.</span></span> <span data-ttu-id="af20e-107">Pour obtenir la liste des magasins de données pris en charge en tant que récepteurs par l’activité de copie, voir le tableau [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="af20e-107">For a list of data stores supported as sinks by the copy activity, see the [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="af20e-108">Actuellement, Data Factory prend uniquement en charge le déplacement de données d’un serveur FTP vers d’autres magasins de données, mais pas l’inverse.</span><span class="sxs-lookup"><span data-stu-id="af20e-108">Data Factory currently supports only moving data from an FTP server to other data stores, but not moving data from other data stores to an FTP server.</span></span> <span data-ttu-id="af20e-109">Il prend en charge à la fois les serveurs FTP locaux et cloud.</span><span class="sxs-lookup"><span data-stu-id="af20e-109">It supports both on-premises and cloud FTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="af20e-110">L’activité de copie ne supprime pas le fichier source une fois celui-ci copié vers la destination.</span><span class="sxs-lookup"><span data-stu-id="af20e-110">The copy activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="af20e-111">Si vous devez supprimer le fichier source après copie, créez une activité personnalisée pour supprimer le fichier et utilisez l’activité dans le pipeline.</span><span class="sxs-lookup"><span data-stu-id="af20e-111">If you need to delete the source file after a successful copy, create a custom activity to delete the file, and use the activity in the pipeline.</span></span> 

## <a name="enable-connectivity"></a><span data-ttu-id="af20e-112">Activez la connectivité.</span><span class="sxs-lookup"><span data-stu-id="af20e-112">Enable connectivity</span></span>
<span data-ttu-id="af20e-113">Si vous déplacez des données d’un serveur FTP **local** vers un magasin de données cloud (par exemple, Stockage Blob Azure), installez et utilisez la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="af20e-113">If you are moving data from an **on-premises** FTP server to a cloud data store (for example, to Azure Blob storage), install and use Data Management Gateway.</span></span> <span data-ttu-id="af20e-114">La passerelle de gestion des données est un agent client qui est installé sur votre ordinateur local et permet aux services cloud de se connecter à une ressource locale.</span><span class="sxs-lookup"><span data-stu-id="af20e-114">The Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services to connect to an on-premises resource.</span></span> <span data-ttu-id="af20e-115">Pour plus de détails, voir [Passerelle de gestion des données](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="af20e-115">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="af20e-116">Pour obtenir des instructions détaillées sur la configuration de la passerelle et son utilisation, voir [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="af20e-116">For step-by-step instructions on setting up the gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="af20e-117">Vous utilisez la passerelle pour vous connecter à un serveur FTP, même si le serveur est sur une machine virtuelle IaaS Azure.</span><span class="sxs-lookup"><span data-stu-id="af20e-117">You use the gateway to connect to an FTP server, even if the server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span></span>

<span data-ttu-id="af20e-118">Vous pouvez installer la passerelle sur le même ordinateur local ou sur la machine virtuelle IaaS Azure que le serveur FTP.</span><span class="sxs-lookup"><span data-stu-id="af20e-118">It is possible to install the gateway on the same on-premises machine or IaaS VM as the FTP server.</span></span> <span data-ttu-id="af20e-119">Toutefois, nous vous recommandons d’installer la passerelle sur un ordinateur/une machine virtuelle IaaS distincts afin d’éviter les conflits de ressources, ainsi que pour obtenir de meilleures performances.</span><span class="sxs-lookup"><span data-stu-id="af20e-119">However, we recommend that you install the gateway on a separate machine or IaaS VM to avoid resource contention, and for better performance.</span></span> <span data-ttu-id="af20e-120">Lorsque vous installez la passerelle sur un ordinateur distinct, l’ordinateur doit être en mesure au serveur FTP.</span><span class="sxs-lookup"><span data-stu-id="af20e-120">When you install the gateway on a separate machine, the machine should be able to access the FTP server.</span></span>

## <a name="get-started"></a><span data-ttu-id="af20e-121">Prise en main</span><span class="sxs-lookup"><span data-stu-id="af20e-121">Get started</span></span>
<span data-ttu-id="af20e-122">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’une source FTP à l’aide de différents outils ou API.</span><span class="sxs-lookup"><span data-stu-id="af20e-122">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span></span>

<span data-ttu-id="af20e-123">Le moyen le plus simple de créer un pipeline consiste à utiliser **l’Assistant Copie de Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="af20e-123">The easiest way to create a pipeline is to use the **Data Factory Copy Wizard**.</span></span> <span data-ttu-id="af20e-124">Pour obtenir une procédure rapide, consultez l’article [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="af20e-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span></span>

<span data-ttu-id="af20e-125">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="af20e-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="af20e-126">Consultez le [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="af20e-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="af20e-127">Que vous utilisiez des outils ou des API, la création d’un pipeline qui déplace les données d’un magasin de données source vers un magasin de données récepteur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="af20e-127">Whether you use the tools or APIs, perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="af20e-128">Création de **services liés** pour lier les magasins de données d’entrée et de sortie à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="af20e-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="af20e-129">Création de **jeux de données** pour représenter les données d’entrée et de sortie de l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="af20e-129">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="af20e-130">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="af20e-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="af20e-131">Lorsque vous utilisez l’Assistant, les définitions JSON de ces entités Data Factory (services liés, jeux de données et pipeline) sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="af20e-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="af20e-132">Lorsque vous utilisez les outils ou API (à l’exception de l’API .NET), vous devez définir ces entités Data Factory à l’aide du format JSON.</span><span class="sxs-lookup"><span data-stu-id="af20e-132">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="af20e-133">Pour consulter un exemple contenant des définitions JSON pour les entités Data Factory utilisées pour copier des données d’un magasin de données FTP, voir la section [Exemple JSON : copier des données depuis un serveur FTP vers un objet Blob Azure](#json-example-copy-data-from-ftp-server-to-azure-blob) de cet article.</span><span class="sxs-lookup"><span data-stu-id="af20e-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from an FTP data store, see the [JSON example: Copy data from FTP server to Azure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="af20e-134">Pour plus d’informations sur les formats de fichier et de compression pris en charge à utiliser, voir [Formats de fichier et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="af20e-134">For details about supported file and compression formats to use, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="af20e-135">Les sections suivantes fournissent des informations sur les propriétés JSON utilisées pour définir des entités Data Factory spécifiques pour FTP :</span><span class="sxs-lookup"><span data-stu-id="af20e-135">The following sections provide details about JSON properties that are used to define Data Factory entities specific to FTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="af20e-136">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="af20e-136">Linked service properties</span></span>
<span data-ttu-id="af20e-137">Le tableau suivant décrit les éléments JSON spécifiques pour un service FTP lié.</span><span class="sxs-lookup"><span data-stu-id="af20e-137">The following table describes JSON elements specific to an FTP linked service.</span></span>

| <span data-ttu-id="af20e-138">Propriété</span><span class="sxs-lookup"><span data-stu-id="af20e-138">Property</span></span> | <span data-ttu-id="af20e-139">Description</span><span class="sxs-lookup"><span data-stu-id="af20e-139">Description</span></span> | <span data-ttu-id="af20e-140">Requis</span><span class="sxs-lookup"><span data-stu-id="af20e-140">Required</span></span> | <span data-ttu-id="af20e-141">Default</span><span class="sxs-lookup"><span data-stu-id="af20e-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="af20e-142">type</span><span class="sxs-lookup"><span data-stu-id="af20e-142">type</span></span> |<span data-ttu-id="af20e-143">Définissez ceci sur FtpServer.</span><span class="sxs-lookup"><span data-stu-id="af20e-143">Set this to FtpServer.</span></span> |<span data-ttu-id="af20e-144">Oui</span><span class="sxs-lookup"><span data-stu-id="af20e-144">Yes</span></span> |&nbsp; |
| <span data-ttu-id="af20e-145">host</span><span class="sxs-lookup"><span data-stu-id="af20e-145">host</span></span> |<span data-ttu-id="af20e-146">Spécifiez le nom ou l’adresse IP du serveur FTP.</span><span class="sxs-lookup"><span data-stu-id="af20e-146">Specify the name or IP address of the FTP server.</span></span> |<span data-ttu-id="af20e-147">Oui</span><span class="sxs-lookup"><span data-stu-id="af20e-147">Yes</span></span> |&nbsp; |
| <span data-ttu-id="af20e-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="af20e-148">authenticationType</span></span> |<span data-ttu-id="af20e-149">Spécifiez le type d’authentification.</span><span class="sxs-lookup"><span data-stu-id="af20e-149">Specify the authentication type.</span></span> |<span data-ttu-id="af20e-150">Oui</span><span class="sxs-lookup"><span data-stu-id="af20e-150">Yes</span></span> |<span data-ttu-id="af20e-151">Basic, anonyme</span><span class="sxs-lookup"><span data-stu-id="af20e-151">Basic, Anonymous</span></span> |
| <span data-ttu-id="af20e-152">username</span><span class="sxs-lookup"><span data-stu-id="af20e-152">username</span></span> |<span data-ttu-id="af20e-153">Spécifiez l’utilisateur ayant accès au serveur FTP.</span><span class="sxs-lookup"><span data-stu-id="af20e-153">Specify the user who has access to the FTP server.</span></span> |<span data-ttu-id="af20e-154">Non</span><span class="sxs-lookup"><span data-stu-id="af20e-154">No</span></span> |&nbsp; |
| <span data-ttu-id="af20e-155">password</span><span class="sxs-lookup"><span data-stu-id="af20e-155">password</span></span> |<span data-ttu-id="af20e-156">Spécifiez le mot de passe de l’utilisateur (username).</span><span class="sxs-lookup"><span data-stu-id="af20e-156">Specify the password for the user (username).</span></span> |<span data-ttu-id="af20e-157">Non</span><span class="sxs-lookup"><span data-stu-id="af20e-157">No</span></span> |&nbsp; |
| <span data-ttu-id="af20e-158">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="af20e-158">encryptedCredential</span></span> |<span data-ttu-id="af20e-159">Spécifiez les informations d’identification chiffrées pour accéder au serveur FTP.</span><span class="sxs-lookup"><span data-stu-id="af20e-159">Specify the encrypted credential to access the FTP server.</span></span> |<span data-ttu-id="af20e-160">Non</span><span class="sxs-lookup"><span data-stu-id="af20e-160">No</span></span> |&nbsp; |
| <span data-ttu-id="af20e-161">gatewayName</span><span class="sxs-lookup"><span data-stu-id="af20e-161">gatewayName</span></span> |<span data-ttu-id="af20e-162">Spécifiez le nom de la passerelle dans Passerelle de gestion des données pour la connexion à un serveur FTP local</span><span class="sxs-lookup"><span data-stu-id="af20e-162">Specify the name of the gateway in Data Management Gateway to connect to an on-premises FTP server.</span></span> |<span data-ttu-id="af20e-163">Non</span><span class="sxs-lookup"><span data-stu-id="af20e-163">No</span></span> |&nbsp; |
| <span data-ttu-id="af20e-164">port</span><span class="sxs-lookup"><span data-stu-id="af20e-164">port</span></span> |<span data-ttu-id="af20e-165">Spécifiez le port sur lequel le serveur FTP écoute.</span><span class="sxs-lookup"><span data-stu-id="af20e-165">Specify the port on which the FTP server is listening.</span></span> |<span data-ttu-id="af20e-166">Non</span><span class="sxs-lookup"><span data-stu-id="af20e-166">No</span></span> |<span data-ttu-id="af20e-167">21</span><span class="sxs-lookup"><span data-stu-id="af20e-167">21</span></span> |
| <span data-ttu-id="af20e-168">enableSsl</span><span class="sxs-lookup"><span data-stu-id="af20e-168">enableSsl</span></span> |<span data-ttu-id="af20e-169">Indiquez si vous souhaitez utiliser FTP sur un canal SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="af20e-169">Specify whether to use FTP over an SSL/TLS channel.</span></span> |<span data-ttu-id="af20e-170">Non</span><span class="sxs-lookup"><span data-stu-id="af20e-170">No</span></span> |<span data-ttu-id="af20e-171">true</span><span class="sxs-lookup"><span data-stu-id="af20e-171">true</span></span> |
| <span data-ttu-id="af20e-172">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="af20e-172">enableServerCertificateValidation</span></span> |<span data-ttu-id="af20e-173">Indiquez si vous souhaitez activer la validation des certificats SSL lors de l’utilisation de FTP sur un canal SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="af20e-173">Specify whether to enable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span> |<span data-ttu-id="af20e-174">Non</span><span class="sxs-lookup"><span data-stu-id="af20e-174">No</span></span> |<span data-ttu-id="af20e-175">true</span><span class="sxs-lookup"><span data-stu-id="af20e-175">true</span></span> |

### <a name="use-anonymous-authentication"></a><span data-ttu-id="af20e-176">Utiliser une authentification anonyme</span><span class="sxs-lookup"><span data-stu-id="af20e-176">Use Anonymous authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="af20e-177">Utiliser un nom d’utilisateur et d’un mot de passe en texte brut pour l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="af20e-177">Use username and password in plain text for basic authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="af20e-178">Utiliser un port, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="af20e-178">Use port, enableSsl, enableServerCertificateValidation</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="af20e-179">Utiliser encryptedCredential pour l’authentification et la passerelle</span><span class="sxs-lookup"><span data-stu-id="af20e-179">Use encryptedCredential for authentication and gateway</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="af20e-180">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="af20e-180">Dataset properties</span></span>
<span data-ttu-id="af20e-181">Pour obtenir la liste complète des sections et propriétés disponibles pour la définition de jeux de données, voir [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="af20e-181">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="af20e-182">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données.</span><span class="sxs-lookup"><span data-stu-id="af20e-182">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="af20e-183">La section **typeProperties** est différente pour chaque type de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="af20e-183">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="af20e-184">Elle fournit des informations spécifiques au type de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="af20e-184">It provides information that is specific to the dataset type.</span></span> <span data-ttu-id="af20e-185">La section **typeProperties** pour un jeu de données de type **FileShare** a les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="af20e-185">The **typeProperties** section for a dataset of type **FileShare** has the following properties:</span></span>

| <span data-ttu-id="af20e-186">Propriété</span><span class="sxs-lookup"><span data-stu-id="af20e-186">Property</span></span> | <span data-ttu-id="af20e-187">Description</span><span class="sxs-lookup"><span data-stu-id="af20e-187">Description</span></span> | <span data-ttu-id="af20e-188">Requis</span><span class="sxs-lookup"><span data-stu-id="af20e-188">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af20e-189">folderPath</span><span class="sxs-lookup"><span data-stu-id="af20e-189">folderPath</span></span> |<span data-ttu-id="af20e-190">Sous-chemin d’accès au dossier.</span><span class="sxs-lookup"><span data-stu-id="af20e-190">Subpath to the folder.</span></span> <span data-ttu-id="af20e-191">Utilisez le caractère d’échappement « \ » pour les caractères spéciaux contenus dans la chaîne.</span><span class="sxs-lookup"><span data-stu-id="af20e-191">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="af20e-192">Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples.</span><span class="sxs-lookup"><span data-stu-id="af20e-192">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="af20e-193">Vous pouvez également combiner cette propriété avec **partitionBy** pour que les chemins d’accès soient basés sur les dates et heures de début et de fin de la tranche.</span><span class="sxs-lookup"><span data-stu-id="af20e-193">You can combine this property with **partitionBy** to have folder paths based on slice start and end date-times.</span></span> |<span data-ttu-id="af20e-194">Oui</span><span class="sxs-lookup"><span data-stu-id="af20e-194">Yes</span></span> |
| <span data-ttu-id="af20e-195">fileName</span><span class="sxs-lookup"><span data-stu-id="af20e-195">fileName</span></span> |<span data-ttu-id="af20e-196">Spécifiez le nom du fichier dans l’élément **folderPath** si vous souhaitez que la table se réfère à un fichier spécifique du dossier.</span><span class="sxs-lookup"><span data-stu-id="af20e-196">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="af20e-197">Si vous ne spécifiez aucune valeur pour cette propriété, le tableau pointe vers tous les fichiers du dossier.</span><span class="sxs-lookup"><span data-stu-id="af20e-197">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="af20e-198">Lorsque **fileName** n’est pas spécifié pour un jeu de données de sortie, le nom du fichier généré est au format suivant :</span><span class="sxs-lookup"><span data-stu-id="af20e-198">When **fileName** is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="af20e-199">Data<Guid>.txt (exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="af20e-199">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="af20e-200">Non</span><span class="sxs-lookup"><span data-stu-id="af20e-200">No</span></span> |
| <span data-ttu-id="af20e-201">fileFilter</span><span class="sxs-lookup"><span data-stu-id="af20e-201">fileFilter</span></span> |<span data-ttu-id="af20e-202">Spécifiez un filtre à utiliser pour sélectionner un sous-ensemble de fichiers dans le **folderPath** plutôt que tous les fichiers.</span><span class="sxs-lookup"><span data-stu-id="af20e-202">Specify a filter to be used to select a subset of files in the **folderPath**, rather than all files.</span></span><br/><br/><span data-ttu-id="af20e-203">Les valeurs autorisées sont : `*` (plusieurs caractères) et `?` (caractère unique).</span><span class="sxs-lookup"><span data-stu-id="af20e-203">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="af20e-204">Exemple 1 : `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="af20e-204">Example 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="af20e-205">Exemple 2 : `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="af20e-205">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="af20e-206">**fileFilter** s’applique à un jeu de données FileShare d’entrée.</span><span class="sxs-lookup"><span data-stu-id="af20e-206">**fileFilter** is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="af20e-207">Cette propriété n’est pas pris en charge avec le Système de fichiers DFS Hadoop (HDFS).</span><span class="sxs-lookup"><span data-stu-id="af20e-207">This property is not supported with Hadoop Distributed File System (HDFS).</span></span> |<span data-ttu-id="af20e-208">Non</span><span class="sxs-lookup"><span data-stu-id="af20e-208">No</span></span> |
| <span data-ttu-id="af20e-209">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="af20e-209">partitionedBy</span></span> |<span data-ttu-id="af20e-210">Utilisé pour spécifier un **folderPath** et un **fileName** dynamiques pour des données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="af20e-210">Used to specify a dynamic **folderPath** and **fileName** for time series data.</span></span> <span data-ttu-id="af20e-211">Par exemple, vous pouvez spécifier un **folderPath** paramétré pour chaque heure de données.</span><span class="sxs-lookup"><span data-stu-id="af20e-211">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span></span> |<span data-ttu-id="af20e-212">Non</span><span class="sxs-lookup"><span data-stu-id="af20e-212">No</span></span> |
| <span data-ttu-id="af20e-213">format</span><span class="sxs-lookup"><span data-stu-id="af20e-213">format</span></span> | <span data-ttu-id="af20e-214">Les types de formats suivants sont pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="af20e-214">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="af20e-215">Définissez la propriété **type** située sous Format sur l’une de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="af20e-215">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="af20e-216">Pour en savoir plus, vois les sections [Format Text](data-factory-supported-file-and-compression-formats.md#text-format), [Format Json](data-factory-supported-file-and-compression-formats.md#json-format), [Format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [Format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="af20e-216">For more information, see the [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="af20e-217">Si vous souhaitez copier des fichiers en l’état entre des magasins de fichiers (copie binaire), ignorez la section Format dans les définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="af20e-217">If you want to copy files as they are between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="af20e-218">Non</span><span class="sxs-lookup"><span data-stu-id="af20e-218">No</span></span> |
| <span data-ttu-id="af20e-219">compression</span><span class="sxs-lookup"><span data-stu-id="af20e-219">compression</span></span> | <span data-ttu-id="af20e-220">Spécifiez le type et le niveau de compression pour les données.</span><span class="sxs-lookup"><span data-stu-id="af20e-220">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="af20e-221">Les types pris en charge sont **GZip**, **Deflate**, **BZip2** et **ZipDeflate**. Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="af20e-221">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="af20e-222">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="af20e-222">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="af20e-223">Non</span><span class="sxs-lookup"><span data-stu-id="af20e-223">No</span></span> |
| <span data-ttu-id="af20e-224">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="af20e-224">useBinaryTransfer</span></span> |<span data-ttu-id="af20e-225">Spécifiez s’il faut utiliser le mode de transfert binaire.</span><span class="sxs-lookup"><span data-stu-id="af20e-225">Specify whether to use the binary transfer mode.</span></span> <span data-ttu-id="af20e-226">Les valeurs sont true pour le mode binaire (c’est la valeur par défaut) et false pour ASCII.</span><span class="sxs-lookup"><span data-stu-id="af20e-226">The values are true for binary mode (this is the default value), and false for ASCII.</span></span> <span data-ttu-id="af20e-227">Cette propriété peut être utilisée uniquement lorsque le type de service lié associé est FtpServer.</span><span class="sxs-lookup"><span data-stu-id="af20e-227">This property can only be used when the associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="af20e-228">Non</span><span class="sxs-lookup"><span data-stu-id="af20e-228">No</span></span> |

> [!NOTE]
> <span data-ttu-id="af20e-229">**fileName** et **fileFilter** ne peuvent pas être utilisés simultanément.</span><span class="sxs-lookup"><span data-stu-id="af20e-229">**fileName** and **fileFilter** cannot be used simultaneously.</span></span>

### <a name="use-the-partionedby-property"></a><span data-ttu-id="af20e-230">Utiliser la propriété partitionedBy</span><span class="sxs-lookup"><span data-stu-id="af20e-230">Use the partionedBy property</span></span>
<span data-ttu-id="af20e-231">Comme mentionné dans la section précédente, vous pouvez spécifier un **folderPath** et un **fileName** dynamiques pour les données de série chronologique avec la propriété **partitionedBy**.</span><span class="sxs-lookup"><span data-stu-id="af20e-231">As mentioned in the previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with the **partitionedBy** property.</span></span>

<span data-ttu-id="af20e-232">Pour découvrir les jeux de données de série chronologique, la planification et les segments, voir [Création de jeux de données](data-factory-create-datasets.md), [Planification et exécution](data-factory-scheduling-and-execution.md) et [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="af20e-232">To learn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="af20e-233">Exemple 1</span><span class="sxs-lookup"><span data-stu-id="af20e-233">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="af20e-234">Dans cet exemple, {Slice} est remplacé par la valeur de la variable système Data Factory SliceStart au format spécifié (AAAAMMJJHH).</span><span class="sxs-lookup"><span data-stu-id="af20e-234">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart, in the format specified (YYYYMMDDHH).</span></span> <span data-ttu-id="af20e-235">SliceStart fait référence à l'heure de début du segment.</span><span class="sxs-lookup"><span data-stu-id="af20e-235">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="af20e-236">Le chemine d’accès du dossier est différent pour chaque segment</span><span class="sxs-lookup"><span data-stu-id="af20e-236">The folder path is different for each slice.</span></span> <span data-ttu-id="af20e-237">(par exemple : wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104).</span><span class="sxs-lookup"><span data-stu-id="af20e-237">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span></span>

#### <a name="sample-2"></a><span data-ttu-id="af20e-238">Exemple 2</span><span class="sxs-lookup"><span data-stu-id="af20e-238">Sample 2</span></span>

```json
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
<span data-ttu-id="af20e-239">Dans cet exemple, l’année, le mois, le jour et l’heure de SliceStart sont extraits dans des variables distinctes qui sont utilisées par les propriétés **folderPath** et **fileName**.</span><span class="sxs-lookup"><span data-stu-id="af20e-239">In this example, the year, month, day, and time of SliceStart are extracted into separate variables that are used by the **folderPath** and **fileName** properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="af20e-240">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="af20e-240">Copy activity properties</span></span>
<span data-ttu-id="af20e-241">Pour obtenir la liste complète des sections et propriétés disponibles pour la définition des activités, voir [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="af20e-241">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="af20e-242">Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités.</span><span class="sxs-lookup"><span data-stu-id="af20e-242">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="af20e-243">En revanche, les propriétés disponibles dans la section **typeProperties** de l’activité varient pour chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="af20e-243">Properties available in the **typeProperties** section of the activity, on the other hand, vary with each activity type.</span></span> <span data-ttu-id="af20e-244">Pour l’activité de copie, les propriétés de type dépendent des types de sources et de récepteurs.</span><span class="sxs-lookup"><span data-stu-id="af20e-244">For the copy activity, the type properties vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="af20e-245">Dans une activité de copie, quand la source est de type **FileSystemSource**, les propriétés suivantes sont disponibles dans la section **typeProperties** :</span><span class="sxs-lookup"><span data-stu-id="af20e-245">In copy activity, when the source is of type **FileSystemSource**, the following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="af20e-246">Propriété</span><span class="sxs-lookup"><span data-stu-id="af20e-246">Property</span></span> | <span data-ttu-id="af20e-247">Description</span><span class="sxs-lookup"><span data-stu-id="af20e-247">Description</span></span> | <span data-ttu-id="af20e-248">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="af20e-248">Allowed values</span></span> | <span data-ttu-id="af20e-249">Requis</span><span class="sxs-lookup"><span data-stu-id="af20e-249">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="af20e-250">recursive</span><span class="sxs-lookup"><span data-stu-id="af20e-250">recursive</span></span> |<span data-ttu-id="af20e-251">Indique si les données sont lues de manière récursive à partir des sous-dossiers ou uniquement du dossier spécifié.</span><span class="sxs-lookup"><span data-stu-id="af20e-251">Indicates whether the data is read recursively from the subfolders, or only from the specified folder.</span></span> |<span data-ttu-id="af20e-252">True, False (par défaut)</span><span class="sxs-lookup"><span data-stu-id="af20e-252">True, False (default)</span></span> |<span data-ttu-id="af20e-253">Non</span><span class="sxs-lookup"><span data-stu-id="af20e-253">No</span></span> |

## <a name="json-example-copy-data-from-ftp-server-to-azure-blob"></a><span data-ttu-id="af20e-254">Exemple JSON : copie de données depuis un serveur FTP à un objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="af20e-254">JSON example: Copy data from FTP server to Azure Blob</span></span>
<span data-ttu-id="af20e-255">Cet exemple montre comment copier des données à partir d’un serveur FTP vers un stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="af20e-255">This sample shows how to copy data from an FTP server to Azure Blob storage.</span></span> <span data-ttu-id="af20e-256">Toutefois, il est possible de copier des données directement vers tout récepteur indiqué dans [magasins et formats de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de l’activité de copie dans Data Factory.</span><span class="sxs-lookup"><span data-stu-id="af20e-256">However, data can be copied directly to any of the sinks stated in the [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using the copy activity in Data Factory.</span></span>  

<span data-ttu-id="af20e-257">Les exemples suivants présentent des définitions JSON que vous pouvez utiliser pour créer un pipeline à l’aide du [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), de [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou de [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) :</span><span class="sxs-lookup"><span data-stu-id="af20e-257">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span></span>

* <span data-ttu-id="af20e-258">Un service lié de type [FtpServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="af20e-258">A linked service of type [FtpServer](#linked-service-properties)</span></span>
* <span data-ttu-id="af20e-259">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="af20e-259">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="af20e-260">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [FileShare](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="af20e-260">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span></span>
* <span data-ttu-id="af20e-261">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="af20e-261">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="af20e-262">Un [pipeline](data-factory-create-pipelines.md) avec activité de copie qui utilise [FileSystemSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="af20e-262">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="af20e-263">L’exemple copie des données d’un serveur FTP vers un objet blob Azure toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="af20e-263">The sample copies data from an FTP server to an Azure blob every hour.</span></span> <span data-ttu-id="af20e-264">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="af20e-264">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="ftp-linked-service"></a><span data-ttu-id="af20e-265">Service lié FTP</span><span class="sxs-lookup"><span data-stu-id="af20e-265">FTP linked service</span></span>

<span data-ttu-id="af20e-266">Cet exemple utilise une authentification de base avec le nom d’utilisateur et le mot de passe en texte brut.</span><span class="sxs-lookup"><span data-stu-id="af20e-266">This example uses basic authentication, with the user name and password in plain text.</span></span> <span data-ttu-id="af20e-267">Vous pouvez également utiliser une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="af20e-267">You can also use one of the following ways:</span></span>

* <span data-ttu-id="af20e-268">Authentification anonyme</span><span class="sxs-lookup"><span data-stu-id="af20e-268">Anonymous authentication</span></span>
* <span data-ttu-id="af20e-269">Authentification de base avec des informations d’identification chiffrées</span><span class="sxs-lookup"><span data-stu-id="af20e-269">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="af20e-270">FTP sur SSL/TLS (FTPS)</span><span class="sxs-lookup"><span data-stu-id="af20e-270">FTP over SSL/TLS (FTPS)</span></span>

<span data-ttu-id="af20e-271">Pour connaître les différents types d’authentification que vous pouvez utiliser, voir [Service lié FTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="af20e-271">See the [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
    }
  }
}
```
### <a name="azure-storage-linked-service"></a><span data-ttu-id="af20e-272">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="af20e-272">Azure Storage linked service</span></span>

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
### <a name="ftp-input-dataset"></a><span data-ttu-id="af20e-273">Jeu de données d’entrée FTP</span><span class="sxs-lookup"><span data-stu-id="af20e-273">FTP input dataset</span></span>

<span data-ttu-id="af20e-274">Ce jeu de données fait référence au dossier SFTP `mysharedfolder` et au fichier `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="af20e-274">This dataset refers to the FTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="af20e-275">Le pipeline copie le fichier vers la destination.</span><span class="sxs-lookup"><span data-stu-id="af20e-275">The pipeline copies the file to the destination.</span></span>

<span data-ttu-id="af20e-276">La définition de **external** sur **true** informe le service Data Factory qu’il s’agit d’un jeu de données qui est externe à la fabrique de données et non produit par une activité dans celle-ci.</span><span class="sxs-lookup"><span data-stu-id="af20e-276">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory, and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="af20e-277">Jeu de données de sortie d’objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="af20e-277">Azure Blob output dataset</span></span>

<span data-ttu-id="af20e-278">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="af20e-278">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="af20e-279">Le chemin d’accès du dossier pour l’objet blob est évalué dynamiquement en fonction de l’heure de début du segment en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="af20e-279">The folder path for the blob is dynamically evaluated, based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="af20e-280">Le chemin d’accès du dossier utilise l’année, le mois, le jour et la partie heure de l’heure de début.</span><span class="sxs-lookup"><span data-stu-id="af20e-280">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a><span data-ttu-id="af20e-281">Activité de copie dans un pipeline avec une source Système de fichiers et un récepteur blob</span><span class="sxs-lookup"><span data-stu-id="af20e-281">A copy activity in a pipeline with file system source and blob sink</span></span>

<span data-ttu-id="af20e-282">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d’entrée et de sortie, et qui est planifiée pour s’exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="af20e-282">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="af20e-283">Dans la définition JSON du pipeline, le type **source** est défini sur **FileSystemSource** et le type **sink** sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="af20e-283">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and the **sink** type is set to **BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="af20e-284">Pour savoir comment mapper des colonnes d’un jeu de données source sur des colonnes d’un jeu de données récepteur, consultez [Mappage de colonnes des jeux de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="af20e-284">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="af20e-285">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="af20e-285">Next steps</span></span>
<span data-ttu-id="af20e-286">Consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="af20e-286">See the following articles:</span></span>

* <span data-ttu-id="af20e-287">Pour découvrir les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser, voir [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="af20e-287">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="af20e-288">Pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie, voir [Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="af20e-288">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
