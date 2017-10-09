---
title: "aaaMove des données à partir d’un serveur FTP à l’aide d’Azure Data Factory | Documents Microsoft"
description: "En savoir plus sur la façon de toomove les données à partir d’un serveur FTP à l’aide d’Azure Data Factory."
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
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="4b345-103">Déplacer des données à partir d’un serveur FTP à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="4b345-103">Move data from an FTP server by using Azure Data Factory</span></span>
<span data-ttu-id="4b345-104">Cet article explique comment toouse hello activité de copie de données de toomove Azure Data Factory à partir d’un serveur FTP.</span><span class="sxs-lookup"><span data-stu-id="4b345-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from an FTP server.</span></span> <span data-ttu-id="4b345-105">Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.</span><span class="sxs-lookup"><span data-stu-id="4b345-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="4b345-106">Vous pouvez copier des données à partir d’un magasin de données de récepteur FTP server tooany pris en charge.</span><span class="sxs-lookup"><span data-stu-id="4b345-106">You can copy data from an FTP server tooany supported sink data store.</span></span> <span data-ttu-id="4b345-107">Pour une liste de données pris en charge des magasins récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="4b345-107">For a list of data stores supported as sinks by hello copy activity, see hello [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="4b345-108">Fabrique de données prend en charge seulement stocke de déplacement des données d’un FTP server tooother de données, mais ne pas déplacer les données à partir d’autres données stocke tooan FTP server.</span><span class="sxs-lookup"><span data-stu-id="4b345-108">Data Factory currently supports only moving data from an FTP server tooother data stores, but not moving data from other data stores tooan FTP server.</span></span> <span data-ttu-id="4b345-109">Il prend en charge à la fois les serveurs FTP locaux et cloud.</span><span class="sxs-lookup"><span data-stu-id="4b345-109">It supports both on-premises and cloud FTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="4b345-110">activité de copie Hello ne supprime pas le fichier de source de hello lorsqu’elle est correctement copié toohello destination.</span><span class="sxs-lookup"><span data-stu-id="4b345-110">hello copy activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="4b345-111">Si vous avez besoin de fichier de source de hello toodelete après la copie a réussi, créer un fichier de hello toodelete activité personnalisée et utiliser l’activité hello dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="4b345-111">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file, and use hello activity in hello pipeline.</span></span> 

## <a name="enable-connectivity"></a><span data-ttu-id="4b345-112">Activez la connectivité.</span><span class="sxs-lookup"><span data-stu-id="4b345-112">Enable connectivity</span></span>
<span data-ttu-id="4b345-113">Si vous déplacez des données d’une **local** magasin de données cloud FTP server tooa (par exemple, tooAzure stockage d’objets Blob), installer et utiliser la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="4b345-113">If you are moving data from an **on-premises** FTP server tooa cloud data store (for example, tooAzure Blob storage), install and use Data Management Gateway.</span></span> <span data-ttu-id="4b345-114">Hello passerelle de gestion des données est un agent de client qui est installé sur votre ordinateur local et il permet de ressources de cloud services tooconnect tooan local.</span><span class="sxs-lookup"><span data-stu-id="4b345-114">hello Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services tooconnect tooan on-premises resource.</span></span> <span data-ttu-id="4b345-115">Pour plus de détails, voir [Passerelle de gestion des données](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="4b345-115">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="4b345-116">Pour obtenir des instructions sur la configuration de passerelle de hello et l’utiliser, consultez [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="4b345-116">For step-by-step instructions on setting up hello gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="4b345-117">Vous utilisez server de hello passerelle tooconnect tooan FTP, même si le serveur de hello est sur une infrastructure Windows Azure en tant que service (IaaS) virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="4b345-117">You use hello gateway tooconnect tooan FTP server, even if hello server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span></span>

<span data-ttu-id="4b345-118">Il s’agit de passerelle de hello tooinstall possibles sur hello même local machine ou IaaS VM comme hello du serveur FTP.</span><span class="sxs-lookup"><span data-stu-id="4b345-118">It is possible tooinstall hello gateway on hello same on-premises machine or IaaS VM as hello FTP server.</span></span> <span data-ttu-id="4b345-119">Toutefois, nous vous recommandons d’installer hello passerelle sur un ordinateur distinct ou un conflit de ressources IaaS VM tooavoid et pour de meilleures performances.</span><span class="sxs-lookup"><span data-stu-id="4b345-119">However, we recommend that you install hello gateway on a separate machine or IaaS VM tooavoid resource contention, and for better performance.</span></span> <span data-ttu-id="4b345-120">Lorsque vous installez la passerelle de hello sur un ordinateur distinct, machine de hello doit être le serveur FTP de hello tooaccess en mesure de.</span><span class="sxs-lookup"><span data-stu-id="4b345-120">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello FTP server.</span></span>

## <a name="get-started"></a><span data-ttu-id="4b345-121">Prise en main</span><span class="sxs-lookup"><span data-stu-id="4b345-121">Get started</span></span>
<span data-ttu-id="4b345-122">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’une source FTP à l’aide de différents outils ou API.</span><span class="sxs-lookup"><span data-stu-id="4b345-122">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span></span>

<span data-ttu-id="4b345-123">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="4b345-123">hello easiest way toocreate a pipeline is toouse hello **Data Factory Copy Wizard**.</span></span> <span data-ttu-id="4b345-124">Pour obtenir une procédure rapide, consultez l’article [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="4b345-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span></span>

<span data-ttu-id="4b345-125">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **PowerShell**, **le modèle Azure Resource Manager**, **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="4b345-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="4b345-126">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="4b345-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="4b345-127">Si vous utilisez des API ou des outils de hello, procédez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données sources :</span><span class="sxs-lookup"><span data-stu-id="4b345-127">Whether you use hello tools or APIs, perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="4b345-128">Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.</span><span class="sxs-lookup"><span data-stu-id="4b345-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="4b345-129">Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.</span><span class="sxs-lookup"><span data-stu-id="4b345-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="4b345-130">Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="4b345-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="4b345-131">Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="4b345-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="4b345-132">Lorsque vous utilisez des outils ou des API (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="4b345-132">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="4b345-133">Pour voir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données à partir d’une banque de données FTP, hello [exemple de JSON : copier des données d’objet blob tooAzure de serveur FTP](#json-example-copy-data-from-ftp-server-to-azure-blob) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="4b345-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an FTP data store, see hello [JSON example: Copy data from FTP server tooAzure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="4b345-134">Pour plus d’informations sur la prise en charge toouse de formats de compression des fichiers et, consultez [des formats de fichiers et de compression dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="4b345-134">For details about supported file and compression formats toouse, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="4b345-135">Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifique tooFTP.</span><span class="sxs-lookup"><span data-stu-id="4b345-135">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooFTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="4b345-136">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="4b345-136">Linked service properties</span></span>
<span data-ttu-id="4b345-137">Hello tableau suivant décrit les service FTP lié de JSON éléments tooan spécifique.</span><span class="sxs-lookup"><span data-stu-id="4b345-137">hello following table describes JSON elements specific tooan FTP linked service.</span></span>

| <span data-ttu-id="4b345-138">Propriété</span><span class="sxs-lookup"><span data-stu-id="4b345-138">Property</span></span> | <span data-ttu-id="4b345-139">Description</span><span class="sxs-lookup"><span data-stu-id="4b345-139">Description</span></span> | <span data-ttu-id="4b345-140">Requis</span><span class="sxs-lookup"><span data-stu-id="4b345-140">Required</span></span> | <span data-ttu-id="4b345-141">Default</span><span class="sxs-lookup"><span data-stu-id="4b345-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4b345-142">type</span><span class="sxs-lookup"><span data-stu-id="4b345-142">type</span></span> |<span data-ttu-id="4b345-143">Définissez cette tooFtpServer.</span><span class="sxs-lookup"><span data-stu-id="4b345-143">Set this tooFtpServer.</span></span> |<span data-ttu-id="4b345-144">Oui</span><span class="sxs-lookup"><span data-stu-id="4b345-144">Yes</span></span> |&nbsp; |
| <span data-ttu-id="4b345-145">host</span><span class="sxs-lookup"><span data-stu-id="4b345-145">host</span></span> |<span data-ttu-id="4b345-146">Spécifiez le nom de hello ou adresse IP du serveur FTP de hello.</span><span class="sxs-lookup"><span data-stu-id="4b345-146">Specify hello name or IP address of hello FTP server.</span></span> |<span data-ttu-id="4b345-147">Oui</span><span class="sxs-lookup"><span data-stu-id="4b345-147">Yes</span></span> |&nbsp; |
| <span data-ttu-id="4b345-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="4b345-148">authenticationType</span></span> |<span data-ttu-id="4b345-149">Spécifiez le type d’authentification hello.</span><span class="sxs-lookup"><span data-stu-id="4b345-149">Specify hello authentication type.</span></span> |<span data-ttu-id="4b345-150">Oui</span><span class="sxs-lookup"><span data-stu-id="4b345-150">Yes</span></span> |<span data-ttu-id="4b345-151">Basic, anonyme</span><span class="sxs-lookup"><span data-stu-id="4b345-151">Basic, Anonymous</span></span> |
| <span data-ttu-id="4b345-152">username</span><span class="sxs-lookup"><span data-stu-id="4b345-152">username</span></span> |<span data-ttu-id="4b345-153">Spécifier hello utilisateur a accès toohello FTP serveur.</span><span class="sxs-lookup"><span data-stu-id="4b345-153">Specify hello user who has access toohello FTP server.</span></span> |<span data-ttu-id="4b345-154">Non</span><span class="sxs-lookup"><span data-stu-id="4b345-154">No</span></span> |&nbsp; |
| <span data-ttu-id="4b345-155">password</span><span class="sxs-lookup"><span data-stu-id="4b345-155">password</span></span> |<span data-ttu-id="4b345-156">Spécifiez le mot de passe hello pour hello (nom d’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="4b345-156">Specify hello password for hello user (username).</span></span> |<span data-ttu-id="4b345-157">Non</span><span class="sxs-lookup"><span data-stu-id="4b345-157">No</span></span> |&nbsp; |
| <span data-ttu-id="4b345-158">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="4b345-158">encryptedCredential</span></span> |<span data-ttu-id="4b345-159">Spécifiez hello crypté d’informations d’identification tooaccess hello FTP serveur.</span><span class="sxs-lookup"><span data-stu-id="4b345-159">Specify hello encrypted credential tooaccess hello FTP server.</span></span> |<span data-ttu-id="4b345-160">Non</span><span class="sxs-lookup"><span data-stu-id="4b345-160">No</span></span> |&nbsp; |
| <span data-ttu-id="4b345-161">gatewayName</span><span class="sxs-lookup"><span data-stu-id="4b345-161">gatewayName</span></span> |<span data-ttu-id="4b345-162">Spécifier le nom hello de passerelle de hello dans le serveur de passerelle de gestion des données tooconnect tooan sur site FTP.</span><span class="sxs-lookup"><span data-stu-id="4b345-162">Specify hello name of hello gateway in Data Management Gateway tooconnect tooan on-premises FTP server.</span></span> |<span data-ttu-id="4b345-163">Non</span><span class="sxs-lookup"><span data-stu-id="4b345-163">No</span></span> |&nbsp; |
| <span data-ttu-id="4b345-164">port</span><span class="sxs-lookup"><span data-stu-id="4b345-164">port</span></span> |<span data-ttu-id="4b345-165">Spécifier le port hello sur quel hello FTP serveur écoute.</span><span class="sxs-lookup"><span data-stu-id="4b345-165">Specify hello port on which hello FTP server is listening.</span></span> |<span data-ttu-id="4b345-166">Non</span><span class="sxs-lookup"><span data-stu-id="4b345-166">No</span></span> |<span data-ttu-id="4b345-167">21</span><span class="sxs-lookup"><span data-stu-id="4b345-167">21</span></span> |
| <span data-ttu-id="4b345-168">enableSsl</span><span class="sxs-lookup"><span data-stu-id="4b345-168">enableSsl</span></span> |<span data-ttu-id="4b345-169">Spécifiez si toouse FTP sur un canal SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="4b345-169">Specify whether toouse FTP over an SSL/TLS channel.</span></span> |<span data-ttu-id="4b345-170">Non</span><span class="sxs-lookup"><span data-stu-id="4b345-170">No</span></span> |<span data-ttu-id="4b345-171">true</span><span class="sxs-lookup"><span data-stu-id="4b345-171">true</span></span> |
| <span data-ttu-id="4b345-172">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="4b345-172">enableServerCertificateValidation</span></span> |<span data-ttu-id="4b345-173">Spécifiez si le serveur tooenable SSL la validation des certificats lorsque vous utilisez FTP sur un canal SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="4b345-173">Specify whether tooenable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span> |<span data-ttu-id="4b345-174">Non</span><span class="sxs-lookup"><span data-stu-id="4b345-174">No</span></span> |<span data-ttu-id="4b345-175">true</span><span class="sxs-lookup"><span data-stu-id="4b345-175">true</span></span> |

### <a name="use-anonymous-authentication"></a><span data-ttu-id="4b345-176">Utiliser une authentification anonyme</span><span class="sxs-lookup"><span data-stu-id="4b345-176">Use Anonymous authentication</span></span>

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

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="4b345-177">Utiliser un nom d’utilisateur et d’un mot de passe en texte brut pour l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="4b345-177">Use username and password in plain text for basic authentication</span></span>

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

### <a name="use-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="4b345-178">Utiliser un port, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="4b345-178">Use port, enableSsl, enableServerCertificateValidation</span></span>

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

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="4b345-179">Utiliser encryptedCredential pour l’authentification et la passerelle</span><span class="sxs-lookup"><span data-stu-id="4b345-179">Use encryptedCredential for authentication and gateway</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="4b345-180">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="4b345-180">Dataset properties</span></span>
<span data-ttu-id="4b345-181">Pour obtenir la liste complète des sections et propriétés disponibles pour la définition de jeux de données, voir [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="4b345-181">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="4b345-182">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données.</span><span class="sxs-lookup"><span data-stu-id="4b345-182">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="4b345-183">Hello **typeProperties** section est différente pour chaque type de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="4b345-183">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="4b345-184">Il fournit des informations qui sont le type de jeu de données toohello spécifique.</span><span class="sxs-lookup"><span data-stu-id="4b345-184">It provides information that is specific toohello dataset type.</span></span> <span data-ttu-id="4b345-185">Hello **typeProperties** section pour un jeu de données de type **le partage de fichiers** a hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="4b345-185">hello **typeProperties** section for a dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="4b345-186">Propriété</span><span class="sxs-lookup"><span data-stu-id="4b345-186">Property</span></span> | <span data-ttu-id="4b345-187">Description</span><span class="sxs-lookup"><span data-stu-id="4b345-187">Description</span></span> | <span data-ttu-id="4b345-188">Requis</span><span class="sxs-lookup"><span data-stu-id="4b345-188">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4b345-189">folderPath</span><span class="sxs-lookup"><span data-stu-id="4b345-189">folderPath</span></span> |<span data-ttu-id="4b345-190">Dossier de toohello sous-chemin.</span><span class="sxs-lookup"><span data-stu-id="4b345-190">Subpath toohello folder.</span></span> <span data-ttu-id="4b345-191">Utilisez le caractère d’échappement ' \ ' pour les caractères spéciaux dans la chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="4b345-191">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="4b345-192">Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples.</span><span class="sxs-lookup"><span data-stu-id="4b345-192">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="4b345-193">Vous pouvez combiner cette propriété avec **partitionBy** toohave chemins d’accès basés sur un secteur de démarrage et date-heure de fin.</span><span class="sxs-lookup"><span data-stu-id="4b345-193">You can combine this property with **partitionBy** toohave folder paths based on slice start and end date-times.</span></span> |<span data-ttu-id="4b345-194">Oui</span><span class="sxs-lookup"><span data-stu-id="4b345-194">Yes</span></span> |
| <span data-ttu-id="4b345-195">fileName</span><span class="sxs-lookup"><span data-stu-id="4b345-195">fileName</span></span> |<span data-ttu-id="4b345-196">Spécifiez le nom hello du fichier de hello Bonjour **folderPath** si vous souhaitez hello table toorefer tooa fichier spécifique dans le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="4b345-196">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="4b345-197">Si vous ne spécifiez pas de valeur pour cette propriété, la table de hello pointe tooall des fichiers dans le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="4b345-197">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="4b345-198">Lorsque **nom de fichier** n’est pas spécifié pour un dataset de sortie, hello nom hello généré est Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="4b345-198">When **fileName** is not specified for an output dataset, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="4b345-199">Data<Guid>.txt (exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="4b345-199">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="4b345-200">Non</span><span class="sxs-lookup"><span data-stu-id="4b345-200">No</span></span> |
| <span data-ttu-id="4b345-201">fileFilter</span><span class="sxs-lookup"><span data-stu-id="4b345-201">fileFilter</span></span> |<span data-ttu-id="4b345-202">Spécifiez un tooselect de toobe utilisé filtre un sous-ensemble de fichiers Bonjour **folderPath**, plutôt que tous les fichiers.</span><span class="sxs-lookup"><span data-stu-id="4b345-202">Specify a filter toobe used tooselect a subset of files in hello **folderPath**, rather than all files.</span></span><br/><br/><span data-ttu-id="4b345-203">Les valeurs autorisées sont : `*` (plusieurs caractères) et `?` (caractère unique).</span><span class="sxs-lookup"><span data-stu-id="4b345-203">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="4b345-204">Exemple 1 : `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="4b345-204">Example 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="4b345-205">Exemple 2 : `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="4b345-205">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="4b345-206">**fileFilter** s’applique à un jeu de données FileShare d’entrée.</span><span class="sxs-lookup"><span data-stu-id="4b345-206">**fileFilter** is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="4b345-207">Cette propriété n’est pas pris en charge avec le Système de fichiers DFS Hadoop (HDFS).</span><span class="sxs-lookup"><span data-stu-id="4b345-207">This property is not supported with Hadoop Distributed File System (HDFS).</span></span> |<span data-ttu-id="4b345-208">Non</span><span class="sxs-lookup"><span data-stu-id="4b345-208">No</span></span> |
| <span data-ttu-id="4b345-209">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="4b345-209">partitionedBy</span></span> |<span data-ttu-id="4b345-210">Utilisé toospecify dynamiques **folderPath** et **nom de fichier** pour les données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="4b345-210">Used toospecify a dynamic **folderPath** and **fileName** for time series data.</span></span> <span data-ttu-id="4b345-211">Par exemple, vous pouvez spécifier un **folderPath** paramétré pour chaque heure de données.</span><span class="sxs-lookup"><span data-stu-id="4b345-211">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span></span> |<span data-ttu-id="4b345-212">Non</span><span class="sxs-lookup"><span data-stu-id="4b345-212">No</span></span> |
| <span data-ttu-id="4b345-213">format</span><span class="sxs-lookup"><span data-stu-id="4b345-213">format</span></span> | <span data-ttu-id="4b345-214">Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="4b345-214">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="4b345-215">Ensemble hello **type** propriété sous tooone de format de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="4b345-215">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="4b345-216">Pour plus d’informations, consultez hello [au Format texte](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [le Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), et [Parquet Format ](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="4b345-216">For more information, see hello [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="4b345-217">Si vous souhaitez que les fichiers toocopy lorsqu’ils sont entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="4b345-217">If you want toocopy files as they are between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="4b345-218">Non</span><span class="sxs-lookup"><span data-stu-id="4b345-218">No</span></span> |
| <span data-ttu-id="4b345-219">compression</span><span class="sxs-lookup"><span data-stu-id="4b345-219">compression</span></span> | <span data-ttu-id="4b345-220">Spécifiez le type de hello et le niveau de compression pour les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="4b345-220">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="4b345-221">Les types pris en charge sont **GZip**, **Deflate**, **BZip2** et **ZipDeflate**. Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="4b345-221">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="4b345-222">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="4b345-222">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="4b345-223">Non</span><span class="sxs-lookup"><span data-stu-id="4b345-223">No</span></span> |
| <span data-ttu-id="4b345-224">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="4b345-224">useBinaryTransfer</span></span> |<span data-ttu-id="4b345-225">Spécifiez si le mode de transfert binaire de hello toouse.</span><span class="sxs-lookup"><span data-stu-id="4b345-225">Specify whether toouse hello binary transfer mode.</span></span> <span data-ttu-id="4b345-226">les valeurs Hello sont remplies pour le mode binaire (il s’agit de valeur par défaut de hello) et false pour ASCII.</span><span class="sxs-lookup"><span data-stu-id="4b345-226">hello values are true for binary mode (this is hello default value), and false for ASCII.</span></span> <span data-ttu-id="4b345-227">Cette propriété peut uniquement être utilisée lorsque hello service lié associé est du type : détails.</span><span class="sxs-lookup"><span data-stu-id="4b345-227">This property can only be used when hello associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="4b345-228">Non</span><span class="sxs-lookup"><span data-stu-id="4b345-228">No</span></span> |

> [!NOTE]
> <span data-ttu-id="4b345-229">**fileName** et **fileFilter** ne peuvent pas être utilisés simultanément.</span><span class="sxs-lookup"><span data-stu-id="4b345-229">**fileName** and **fileFilter** cannot be used simultaneously.</span></span>

### <a name="use-hello-partionedby-property"></a><span data-ttu-id="4b345-230">Utilisez la propriété partionedBy de hello</span><span class="sxs-lookup"><span data-stu-id="4b345-230">Use hello partionedBy property</span></span>
<span data-ttu-id="4b345-231">Comme indiqué dans la section précédente de hello, vous pouvez spécifier un dynamique **folderPath** et **nom de fichier** pour les données de série chronologique par hello **partitionedBy** propriété.</span><span class="sxs-lookup"><span data-stu-id="4b345-231">As mentioned in hello previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with hello **partitionedBy** property.</span></span>

<span data-ttu-id="4b345-232">toolearn sur la série de temps des groupes de données, de planification et de secteurs, consultez [création de datasets](data-factory-create-datasets.md), [de planification et de l’exécution](data-factory-scheduling-and-execution.md), et [création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="4b345-232">toolearn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="4b345-233">Exemple 1</span><span class="sxs-lookup"><span data-stu-id="4b345-233">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="4b345-234">Dans cet exemple, {Slice} est remplacé par la valeur hello de variable de système de Data Factory SliceStart, Bonjour format (AAAAMMJJHH) spécifié.</span><span class="sxs-lookup"><span data-stu-id="4b345-234">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart, in hello format specified (YYYYMMDDHH).</span></span> <span data-ttu-id="4b345-235">Hello SliceStart fait référence à des temps de toostart de tranche de hello.</span><span class="sxs-lookup"><span data-stu-id="4b345-235">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="4b345-236">chemin d’accès du dossier Hello est différent pour chaque secteur.</span><span class="sxs-lookup"><span data-stu-id="4b345-236">hello folder path is different for each slice.</span></span> <span data-ttu-id="4b345-237">(par exemple : wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104).</span><span class="sxs-lookup"><span data-stu-id="4b345-237">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span></span>

#### <a name="sample-2"></a><span data-ttu-id="4b345-238">Exemple 2</span><span class="sxs-lookup"><span data-stu-id="4b345-238">Sample 2</span></span>

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
<span data-ttu-id="4b345-239">Dans cet exemple, hello année, mois, jour et l’heure de SliceStart sont extraits dans des variables distinctes qui sont utilisés par hello **folderPath** et **nom de fichier** propriétés.</span><span class="sxs-lookup"><span data-stu-id="4b345-239">In this example, hello year, month, day, and time of SliceStart are extracted into separate variables that are used by hello **folderPath** and **fileName** properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="4b345-240">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="4b345-240">Copy activity properties</span></span>
<span data-ttu-id="4b345-241">Pour obtenir la liste complète des sections et propriétés disponibles pour la définition des activités, voir [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="4b345-241">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="4b345-242">Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités.</span><span class="sxs-lookup"><span data-stu-id="4b345-242">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="4b345-243">Propriétés disponibles dans hello **typeProperties** section de hello activité, hello autre part, varie avec chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="4b345-243">Properties available in hello **typeProperties** section of hello activity, on hello other hand, vary with each activity type.</span></span> <span data-ttu-id="4b345-244">Pour l’activité de copie hello, les propriétés de type hello varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="4b345-244">For hello copy activity, hello type properties vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="4b345-245">Dans l’activité de copie, lors de la source de hello est de type **FileSystemSource**, hello suivant la propriété est disponible dans **typeProperties** section :</span><span class="sxs-lookup"><span data-stu-id="4b345-245">In copy activity, when hello source is of type **FileSystemSource**, hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="4b345-246">Propriété</span><span class="sxs-lookup"><span data-stu-id="4b345-246">Property</span></span> | <span data-ttu-id="4b345-247">Description</span><span class="sxs-lookup"><span data-stu-id="4b345-247">Description</span></span> | <span data-ttu-id="4b345-248">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="4b345-248">Allowed values</span></span> | <span data-ttu-id="4b345-249">Requis</span><span class="sxs-lookup"><span data-stu-id="4b345-249">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4b345-250">recursive</span><span class="sxs-lookup"><span data-stu-id="4b345-250">recursive</span></span> |<span data-ttu-id="4b345-251">Indique si les données de salutation sont lu de manière récursive des sous-dossiers de hello ou uniquement dans le dossier spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="4b345-251">Indicates whether hello data is read recursively from hello subfolders, or only from hello specified folder.</span></span> |<span data-ttu-id="4b345-252">True, False (par défaut)</span><span class="sxs-lookup"><span data-stu-id="4b345-252">True, False (default)</span></span> |<span data-ttu-id="4b345-253">Non</span><span class="sxs-lookup"><span data-stu-id="4b345-253">No</span></span> |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a><span data-ttu-id="4b345-254">Exemple de JSON : copier des données à partir de FTP server tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="4b345-254">JSON example: Copy data from FTP server tooAzure Blob</span></span>
<span data-ttu-id="4b345-255">Cet exemple montre comment toocopy des données à partir d’un tooAzure de serveur FTP stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="4b345-255">This sample shows how toocopy data from an FTP server tooAzure Blob storage.</span></span> <span data-ttu-id="4b345-256">Toutefois, les données peuvent être copiées directement tooany Hello récepteurs hello est indiqué dans [prise en charge des magasins de données et les formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), à l’aide de l’activité de copie hello dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="4b345-256">However, data can be copied directly tooany of hello sinks stated in hello [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using hello copy activity in Data Factory.</span></span>  

<span data-ttu-id="4b345-257">Hello exemples suivants proposent des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="4b345-257">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span></span>

* <span data-ttu-id="4b345-258">Un service lié de type [FtpServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4b345-258">A linked service of type [FtpServer](#linked-service-properties)</span></span>
* <span data-ttu-id="4b345-259">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4b345-259">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="4b345-260">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [FileShare](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="4b345-260">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span></span>
* <span data-ttu-id="4b345-261">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="4b345-261">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="4b345-262">Un [pipeline](data-factory-create-pipelines.md) avec activité de copie qui utilise [FileSystemSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="4b345-262">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="4b345-263">exemple Hello copie des données à partir d’un tooan de serveur FTP blob Azure toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="4b345-263">hello sample copies data from an FTP server tooan Azure blob every hour.</span></span> <span data-ttu-id="4b345-264">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="4b345-264">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="ftp-linked-service"></a><span data-ttu-id="4b345-265">Service lié FTP</span><span class="sxs-lookup"><span data-stu-id="4b345-265">FTP linked service</span></span>

<span data-ttu-id="4b345-266">Cet exemple utilise l’authentification de base, hello nom d’utilisateur et mot de passe en texte brut.</span><span class="sxs-lookup"><span data-stu-id="4b345-266">This example uses basic authentication, with hello user name and password in plain text.</span></span> <span data-ttu-id="4b345-267">Vous pouvez également utiliser un des hello suivant façons :</span><span class="sxs-lookup"><span data-stu-id="4b345-267">You can also use one of hello following ways:</span></span>

* <span data-ttu-id="4b345-268">Authentification anonyme</span><span class="sxs-lookup"><span data-stu-id="4b345-268">Anonymous authentication</span></span>
* <span data-ttu-id="4b345-269">Authentification de base avec des informations d’identification chiffrées</span><span class="sxs-lookup"><span data-stu-id="4b345-269">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="4b345-270">FTP sur SSL/TLS (FTPS)</span><span class="sxs-lookup"><span data-stu-id="4b345-270">FTP over SSL/TLS (FTPS)</span></span>

<span data-ttu-id="4b345-271">Consultez hello [service lié de FTP](#linked-service-properties) section pour différents types d’authentification que vous pouvez utiliser.</span><span class="sxs-lookup"><span data-stu-id="4b345-271">See hello [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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
### <a name="azure-storage-linked-service"></a><span data-ttu-id="4b345-272">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="4b345-272">Azure Storage linked service</span></span>

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
### <a name="ftp-input-dataset"></a><span data-ttu-id="4b345-273">Jeu de données d’entrée FTP</span><span class="sxs-lookup"><span data-stu-id="4b345-273">FTP input dataset</span></span>

<span data-ttu-id="4b345-274">Ce jeu de données fait référence toohello FTP dossier `mysharedfolder` et le fichier `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="4b345-274">This dataset refers toohello FTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="4b345-275">Hello pipeline copies hello toohello destination du fichier.</span><span class="sxs-lookup"><span data-stu-id="4b345-275">hello pipeline copies hello file toohello destination.</span></span>

<span data-ttu-id="4b345-276">Paramètre **externe** trop**true** informe le service de fabrique de données hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="4b345-276">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory, and is not produced by an activity in hello data factory.</span></span>

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="4b345-277">Jeu de données de sortie d’objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="4b345-277">Azure Blob output dataset</span></span>

<span data-ttu-id="4b345-278">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="4b345-278">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="4b345-279">chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement, en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="4b345-279">hello folder path for hello blob is dynamically evaluated, based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="4b345-280">chemin d’accès du dossier Hello utilise hello des parties d’année, mois, jours et heures de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="4b345-280">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a><span data-ttu-id="4b345-281">Activité de copie dans un pipeline avec une source Système de fichiers et un récepteur blob</span><span class="sxs-lookup"><span data-stu-id="4b345-281">A copy activity in a pipeline with file system source and blob sink</span></span>

<span data-ttu-id="4b345-282">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie, et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="4b345-282">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="4b345-283">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**FileSystemSource**et hello **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="4b345-283">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and hello **sink** type is set too**BlobSink**.</span></span>

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
> <span data-ttu-id="4b345-284">colonnes de toomap de toocolumns du jeu de données source à partir du jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="4b345-284">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b345-285">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4b345-285">Next steps</span></span>
<span data-ttu-id="4b345-286">Consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="4b345-286">See hello following articles:</span></span>

* <span data-ttu-id="4b345-287">impact sur les performances de déplacement des données (activité de copie) dans la fabrique de données et différentes façons toooptimize des facteurs toolearn sur la clé, consultez hello [copier activité guide des performances et paramétrage](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="4b345-287">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="4b345-288">Pour obtenir des instructions pour la création d’un pipeline avec une activité de copie, consultez hello [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="4b345-288">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
