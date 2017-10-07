---
title: "aaaMove des données à partir du serveur SFTP à l’aide d’Azure Data Factory | Documents Microsoft"
description: "En savoir plus sur la façon de toomove les données à partir d’un site local ou un serveur SFTP en nuage à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jingwang
ms.openlocfilehash: b976289e2c1b1899634bb5565b375499077fa554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a><span data-ttu-id="cff8e-103">Déplacer des données depuis un serveur SFTP à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="cff8e-103">Move data from an SFTP server using Azure Data Factory</span></span>
<span data-ttu-id="cff8e-104">Cet article décrit comment toouse hello activité de copie de données Azure Data Factory toomove un tooa de serveur SFTP sur le site/cloud prises en charge le magasin de données récepteur.</span><span class="sxs-lookup"><span data-stu-id="cff8e-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises/cloud SFTP server tooa supported sink data store.</span></span> <span data-ttu-id="cff8e-105">Cet article s’appuie sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article qui présente une vue d’ensemble du déplacement des données avec la liste des activités et hello copie de banques de données pris en charge en tant que sources/récepteurs.</span><span class="sxs-lookup"><span data-stu-id="cff8e-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="cff8e-106">Fabrique de données prend actuellement en charge uniquement le déplacement de banques de données à partir d’une données tooother du serveur SFTP, mais pas pour déplacer des données d’autres données de magasins serveur SFTP de tooan.</span><span class="sxs-lookup"><span data-stu-id="cff8e-106">Data factory currently supports only moving data from an SFTP server tooother data stores, but not for moving data from other data stores tooan SFTP server.</span></span> <span data-ttu-id="cff8e-107">Il prend en charge à la fois les serveurs SFTP locaux et cloud.</span><span class="sxs-lookup"><span data-stu-id="cff8e-107">It supports both on-premises and cloud SFTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="cff8e-108">Activité de copie ne supprime pas le fichier de source de hello lorsqu’elle est correctement copié toohello destination.</span><span class="sxs-lookup"><span data-stu-id="cff8e-108">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="cff8e-109">Si vous avez besoin de fichier de source de hello toodelete après la copie a réussi, créer un fichier de hello toodelete activité personnalisée et utiliser l’activité hello dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="cff8e-109">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="cff8e-110">Scénarios et types d’authentification pris en charge</span><span class="sxs-lookup"><span data-stu-id="cff8e-110">Supported scenarios and authentication types</span></span>
<span data-ttu-id="cff8e-111">Vous pouvez utiliser ce SFTP connecteur toocopy les données de **à la fois de cloud computing serveurs SFTP et les serveurs SFTP local**.</span><span class="sxs-lookup"><span data-stu-id="cff8e-111">You can use this SFTP connector toocopy data from **both cloud SFTP servers and on-premises SFTP servers**.</span></span> <span data-ttu-id="cff8e-112">**Base** et **paramètres SshPublicKey** types d’authentification sont pris en charge lors de la connexion du serveur SFTP de toohello.</span><span class="sxs-lookup"><span data-stu-id="cff8e-112">**Basic** and **SshPublicKey** authentication types are supported when connecting toohello SFTP server.</span></span>

<span data-ttu-id="cff8e-113">Lors de la copie des données à partir d’un serveur SFTP de local, vous devez installer une passerelle de gestion des données dans hello local environnement/Azure VM.</span><span class="sxs-lookup"><span data-stu-id="cff8e-113">When copying data from an on-premises SFTP server, you need install a Data Management Gateway in hello on-premises environment/Azure VM.</span></span> <span data-ttu-id="cff8e-114">Consultez [passerelle de gestion des données](data-factory-data-management-gateway.md) pour plus d’informations sur la passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="cff8e-114">See [Data Management Gateway](data-factory-data-management-gateway.md) for details on hello gateway.</span></span> <span data-ttu-id="cff8e-115">Consultez [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) article pour obtenir des instructions sur la configuration de passerelle de hello et l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="cff8e-115">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway and using it.</span></span>

## <a name="getting-started"></a><span data-ttu-id="cff8e-116">Prise en main</span><span class="sxs-lookup"><span data-stu-id="cff8e-116">Getting started</span></span>
<span data-ttu-id="cff8e-117">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’une source SFTP à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="cff8e-117">You can create a pipeline with a copy activity that moves data from an SFTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="cff8e-118">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="cff8e-118">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="cff8e-119">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="cff8e-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

- <span data-ttu-id="cff8e-120">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="cff8e-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="cff8e-121">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="cff8e-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> <span data-ttu-id="cff8e-122">Pour JSON échantillonne les données de toocopy de tooAzure du serveur SFTP stockage d’objets Blob, consultez [exemple de JSON : copier des données d’objet blob tooAzure de serveur SFTP](#json-example-copy-data-from-sftp-server-to-azure-blob) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="cff8e-122">For JSON samples toocopy data from SFTP server tooAzure Blob Storage, see [JSON Example: Copy data from SFTP server tooAzure blob](#json-example-copy-data-from-sftp-server-to-azure-blob) section of this article.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="cff8e-123">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="cff8e-123">Linked service properties</span></span>
<span data-ttu-id="cff8e-124">Hello tableau suivant fournit la description du service de tooFTP spécifique lié éléments JSON.</span><span class="sxs-lookup"><span data-stu-id="cff8e-124">hello following table provides description for JSON elements specific tooFTP linked service.</span></span>

| <span data-ttu-id="cff8e-125">Propriété</span><span class="sxs-lookup"><span data-stu-id="cff8e-125">Property</span></span> | <span data-ttu-id="cff8e-126">Description</span><span class="sxs-lookup"><span data-stu-id="cff8e-126">Description</span></span> | <span data-ttu-id="cff8e-127">Requis</span><span class="sxs-lookup"><span data-stu-id="cff8e-127">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cff8e-128">type</span><span class="sxs-lookup"><span data-stu-id="cff8e-128">type</span></span> | <span data-ttu-id="cff8e-129">propriété de type Hello doit être définie trop`Sftp`.</span><span class="sxs-lookup"><span data-stu-id="cff8e-129">hello type property must be set too`Sftp`.</span></span> |<span data-ttu-id="cff8e-130">Oui</span><span class="sxs-lookup"><span data-stu-id="cff8e-130">Yes</span></span> |
| <span data-ttu-id="cff8e-131">host</span><span class="sxs-lookup"><span data-stu-id="cff8e-131">host</span></span> | <span data-ttu-id="cff8e-132">Nom ou adresse IP du serveur SFTP de hello.</span><span class="sxs-lookup"><span data-stu-id="cff8e-132">Name or IP address of hello SFTP server.</span></span> |<span data-ttu-id="cff8e-133">Oui</span><span class="sxs-lookup"><span data-stu-id="cff8e-133">Yes</span></span> |
| <span data-ttu-id="cff8e-134">port</span><span class="sxs-lookup"><span data-stu-id="cff8e-134">port</span></span> |<span data-ttu-id="cff8e-135">Port d’écoute sur le hello SFTP serveur.</span><span class="sxs-lookup"><span data-stu-id="cff8e-135">Port on which hello SFTP server is listening.</span></span> <span data-ttu-id="cff8e-136">la valeur par défaut Hello est : 21</span><span class="sxs-lookup"><span data-stu-id="cff8e-136">hello default value is: 21</span></span> |<span data-ttu-id="cff8e-137">Non</span><span class="sxs-lookup"><span data-stu-id="cff8e-137">No</span></span> |
| <span data-ttu-id="cff8e-138">authenticationType</span><span class="sxs-lookup"><span data-stu-id="cff8e-138">authenticationType</span></span> |<span data-ttu-id="cff8e-139">Spécification du type d’authentification.</span><span class="sxs-lookup"><span data-stu-id="cff8e-139">Specify authentication type.</span></span> <span data-ttu-id="cff8e-140">Valeurs autorisées : **De base** et **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="cff8e-140">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="cff8e-141">Consultez trop[l’authentification de base à l’aide](#using-basic-authentication) et [à l’aide de SSH authentification par clé publique](#using-ssh-public-key-authentication) sections respectivement sur plus de propriétés et des exemples JSON.</span><span class="sxs-lookup"><span data-stu-id="cff8e-141">Refer too[Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="cff8e-142">Oui</span><span class="sxs-lookup"><span data-stu-id="cff8e-142">Yes</span></span> |
| <span data-ttu-id="cff8e-143">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="cff8e-143">skipHostKeyValidation</span></span> | <span data-ttu-id="cff8e-144">Spécifiez si tooskip validation de clé de l’hôte.</span><span class="sxs-lookup"><span data-stu-id="cff8e-144">Specify whether tooskip host key validation.</span></span> | <span data-ttu-id="cff8e-145">Non.</span><span class="sxs-lookup"><span data-stu-id="cff8e-145">No.</span></span> <span data-ttu-id="cff8e-146">Hello la valeur par défaut : false</span><span class="sxs-lookup"><span data-stu-id="cff8e-146">hello default value: false</span></span> |
| <span data-ttu-id="cff8e-147">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="cff8e-147">hostKeyFingerprint</span></span> | <span data-ttu-id="cff8e-148">Spécifier les empreintes hello de clé d’hôte hello.</span><span class="sxs-lookup"><span data-stu-id="cff8e-148">Specify hello finger print of hello host key.</span></span> | <span data-ttu-id="cff8e-149">Oui si hello `skipHostKeyValidation` a la valeur toofalse.</span><span class="sxs-lookup"><span data-stu-id="cff8e-149">Yes if hello `skipHostKeyValidation` is set toofalse.</span></span>  |
| <span data-ttu-id="cff8e-150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="cff8e-150">gatewayName</span></span> |<span data-ttu-id="cff8e-151">Nom de hello passerelle de gestion des données tooconnect tooan local serveur SFTP.</span><span class="sxs-lookup"><span data-stu-id="cff8e-151">Name of hello Data Management Gateway tooconnect tooan on-premises SFTP server.</span></span> | <span data-ttu-id="cff8e-152">Oui en cas de copie de données à partir d’un serveur SFTP local.</span><span class="sxs-lookup"><span data-stu-id="cff8e-152">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="cff8e-153">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="cff8e-153">encryptedCredential</span></span> | <span data-ttu-id="cff8e-154">Les informations d’identification chiffrées tooaccess hello SFTP le serveur.</span><span class="sxs-lookup"><span data-stu-id="cff8e-154">Encrypted credential tooaccess hello SFTP server.</span></span> <span data-ttu-id="cff8e-155">Généré automatiquement lorsque vous spécifiez l’authentification de base (nom d’utilisateur + mot de passe) ou paramètres SshPublicKey (nom d’utilisateur + chemin d’accès de la clé privée ou contenu) dans la copie Assistant ou hello ClickOnce boîte de dialogue contextuelle.</span><span class="sxs-lookup"><span data-stu-id="cff8e-155">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="cff8e-156">Non.</span><span class="sxs-lookup"><span data-stu-id="cff8e-156">No.</span></span> <span data-ttu-id="cff8e-157">S’applique uniquement pour la copie de données à partir d’un serveur SFTP local.</span><span class="sxs-lookup"><span data-stu-id="cff8e-157">Apply only when copying data from an on-premises SFTP server.</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="cff8e-158">Utilisation de l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="cff8e-158">Using basic authentication</span></span>

<span data-ttu-id="cff8e-159">l’authentification de base toouse, définissez `authenticationType` comme `Basic`et spécifiez les propriétés suivantes en plus de hello connecteur SFTP génériques introduits dans la dernière section de hello de hello :</span><span class="sxs-lookup"><span data-stu-id="cff8e-159">toouse basic authentication, set `authenticationType` as `Basic`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="cff8e-160">Propriété</span><span class="sxs-lookup"><span data-stu-id="cff8e-160">Property</span></span> | <span data-ttu-id="cff8e-161">Description</span><span class="sxs-lookup"><span data-stu-id="cff8e-161">Description</span></span> | <span data-ttu-id="cff8e-162">Requis</span><span class="sxs-lookup"><span data-stu-id="cff8e-162">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cff8e-163">username</span><span class="sxs-lookup"><span data-stu-id="cff8e-163">username</span></span> | <span data-ttu-id="cff8e-164">Utilisateur a accès toohello SFTP serveur.</span><span class="sxs-lookup"><span data-stu-id="cff8e-164">User who has access toohello SFTP server.</span></span> |<span data-ttu-id="cff8e-165">Oui</span><span class="sxs-lookup"><span data-stu-id="cff8e-165">Yes</span></span> |
| <span data-ttu-id="cff8e-166">password</span><span class="sxs-lookup"><span data-stu-id="cff8e-166">password</span></span> | <span data-ttu-id="cff8e-167">Mot de passe pour l’utilisateur hello (nom d’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="cff8e-167">Password for hello user (username).</span></span> | <span data-ttu-id="cff8e-168">Oui</span><span class="sxs-lookup"><span data-stu-id="cff8e-168">Yes</span></span> |

#### <a name="example-basic-authentication"></a><span data-ttu-id="cff8e-169">Exemple : authentification de base</span><span class="sxs-lookup"><span data-stu-id="cff8e-169">Example: Basic authentication</span></span>
```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="cff8e-170">Exemple : authentification de base avec des informations d’identification chiffrées</span><span class="sxs-lookup"><span data-stu-id="cff8e-170">Example: Basic authentication with encrypted credential</span></span>

```JSON
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
      }
}
```

### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="cff8e-171">Utilisation de l’authentification par clé publique SSH</span><span class="sxs-lookup"><span data-stu-id="cff8e-171">Using SSH public key authentication</span></span>

<span data-ttu-id="cff8e-172">toouse SSH authentification par clé publique, définissez `authenticationType` comme `SshPublicKey`et spécifiez les propriétés suivantes en plus de hello connecteur SFTP génériques introduits dans la dernière section de hello de hello :</span><span class="sxs-lookup"><span data-stu-id="cff8e-172">toouse SSH public key authentication, set `authenticationType` as `SshPublicKey`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="cff8e-173">Propriété</span><span class="sxs-lookup"><span data-stu-id="cff8e-173">Property</span></span> | <span data-ttu-id="cff8e-174">Description</span><span class="sxs-lookup"><span data-stu-id="cff8e-174">Description</span></span> | <span data-ttu-id="cff8e-175">Requis</span><span class="sxs-lookup"><span data-stu-id="cff8e-175">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cff8e-176">username</span><span class="sxs-lookup"><span data-stu-id="cff8e-176">username</span></span> |<span data-ttu-id="cff8e-177">Utilisateur qui a accès toohello SFTP serveur</span><span class="sxs-lookup"><span data-stu-id="cff8e-177">User who has access toohello SFTP server</span></span> |<span data-ttu-id="cff8e-178">Oui</span><span class="sxs-lookup"><span data-stu-id="cff8e-178">Yes</span></span> |
| <span data-ttu-id="cff8e-179">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="cff8e-179">privateKeyPath</span></span> | <span data-ttu-id="cff8e-180">Spécifiez le chemin d’accès absolu toohello cette passerelle peut accéder à fichier de clé privée.</span><span class="sxs-lookup"><span data-stu-id="cff8e-180">Specify absolute path toohello private key file that gateway can access.</span></span> | <span data-ttu-id="cff8e-181">Spécifiez soit hello `privateKeyPath` ou `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="cff8e-181">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="cff8e-182">S’applique uniquement pour la copie de données à partir d’un serveur SFTP local.</span><span class="sxs-lookup"><span data-stu-id="cff8e-182">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="cff8e-183">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="cff8e-183">privateKeyContent</span></span> | <span data-ttu-id="cff8e-184">Une chaîne sérialisée de contenu de clé privée hello.</span><span class="sxs-lookup"><span data-stu-id="cff8e-184">A serialized string of hello private key content.</span></span> <span data-ttu-id="cff8e-185">Hello Assistant copie peut lire le fichier de clé privée hello et extraire le contenu de clé privée hello automatiquement.</span><span class="sxs-lookup"><span data-stu-id="cff8e-185">hello Copy Wizard can read hello private key file and extract hello private key content automatically.</span></span> <span data-ttu-id="cff8e-186">Si vous utilisez n’importe quel autre outil/Kit de développement logiciel, utilisez à la place des propriétés de privateKeyPath hello.</span><span class="sxs-lookup"><span data-stu-id="cff8e-186">If you are using any other tool/SDK, use hello privateKeyPath property instead.</span></span> | <span data-ttu-id="cff8e-187">Spécifiez soit hello `privateKeyPath` ou `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="cff8e-187">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="cff8e-188">passPhrase</span><span class="sxs-lookup"><span data-stu-id="cff8e-188">passPhrase</span></span> | <span data-ttu-id="cff8e-189">Spécifiez hello expression/mot de passe toodecrypt hello privée clé si le fichier de clé hello est protégé par un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="cff8e-189">Specify hello pass phrase/password toodecrypt hello private key if hello key file is protected by a pass phrase.</span></span> | <span data-ttu-id="cff8e-190">Oui si le fichier de clé privée hello est protégé par un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="cff8e-190">Yes if hello private key file is protected by a pass phrase.</span></span> |

> [!NOTE]
> <span data-ttu-id="cff8e-191">Le connecteur SFTP prend uniquement en charge la clé OpenSSH.</span><span class="sxs-lookup"><span data-stu-id="cff8e-191">SFTP connector only support OpenSSH key.</span></span> <span data-ttu-id="cff8e-192">Assurez-vous que votre fichier de clé hello format est correct.</span><span class="sxs-lookup"><span data-stu-id="cff8e-192">Make sure your key file is in hello proper format.</span></span> <span data-ttu-id="cff8e-193">Vous pouvez utiliser tooconvert outil Putty depuis le format de tooOpenSSH .ppk.</span><span class="sxs-lookup"><span data-stu-id="cff8e-193">You can use Putty tool tooconvert from .ppk tooOpenSSH format.</span></span>

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a><span data-ttu-id="cff8e-194">Exemple : authentification SshPublicKey à l’aide du chemin du fichier de clé privée</span><span class="sxs-lookup"><span data-stu-id="cff8e-194">Example: SshPublicKey authentication using private key filePath</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="cff8e-195">Exemple : authentification SshPublicKey à l’aide du contenu de clé privée</span><span class="sxs-lookup"><span data-stu-id="cff8e-195">Example: SshPublicKey authentication using private key content</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="cff8e-196">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="cff8e-196">Dataset properties</span></span>
<span data-ttu-id="cff8e-197">Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="cff8e-197">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="cff8e-198">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données.</span><span class="sxs-lookup"><span data-stu-id="cff8e-198">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="cff8e-199">Hello **typeProperties** section est différente pour chaque type de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="cff8e-199">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="cff8e-200">Il fournit des informations qui sont le type de jeu de données toohello spécifique.</span><span class="sxs-lookup"><span data-stu-id="cff8e-200">It provides information that is specific toohello dataset type.</span></span> <span data-ttu-id="cff8e-201">un jeu de données de type Hello typeProperties section **le partage de fichiers** dataset a hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="cff8e-201">hello typeProperties section for a dataset of type **FileShare** dataset has hello following properties:</span></span>

| <span data-ttu-id="cff8e-202">Propriété</span><span class="sxs-lookup"><span data-stu-id="cff8e-202">Property</span></span> | <span data-ttu-id="cff8e-203">Description</span><span class="sxs-lookup"><span data-stu-id="cff8e-203">Description</span></span> | <span data-ttu-id="cff8e-204">Requis</span><span class="sxs-lookup"><span data-stu-id="cff8e-204">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cff8e-205">folderPath</span><span class="sxs-lookup"><span data-stu-id="cff8e-205">folderPath</span></span> |<span data-ttu-id="cff8e-206">Sous-dossier des toohello chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="cff8e-206">Sub path toohello folder.</span></span> <span data-ttu-id="cff8e-207">Utilisez le caractère d’échappement ' \ ' pour les caractères spéciaux dans la chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="cff8e-207">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="cff8e-208">Consultez la section [Exemples de définitions de jeux de données et de service liés](#sample-linked-service-and-dataset-definitions) pour obtenir des exemples.</span><span class="sxs-lookup"><span data-stu-id="cff8e-208">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="cff8e-209">Vous pouvez combiner cette propriété avec **partitionBy** toohave chemins d’accès basés sur un secteur de début et date et l’heure de fin.</span><span class="sxs-lookup"><span data-stu-id="cff8e-209">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="cff8e-210">Oui</span><span class="sxs-lookup"><span data-stu-id="cff8e-210">Yes</span></span> |
| <span data-ttu-id="cff8e-211">fileName</span><span class="sxs-lookup"><span data-stu-id="cff8e-211">fileName</span></span> |<span data-ttu-id="cff8e-212">Spécifiez le nom hello du fichier de hello Bonjour **folderPath** si vous souhaitez hello table toorefer tooa fichier spécifique dans le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="cff8e-212">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="cff8e-213">Si vous ne spécifiez pas de valeur pour cette propriété, la table de hello pointe tooall des fichiers dans le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="cff8e-213">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="cff8e-214">Lorsque le nom de fichier n’est pas spécifié pour un dataset de sortie, nom hello du fichier de hello généré serait Bonjour sous ce format :</span><span class="sxs-lookup"><span data-stu-id="cff8e-214">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="cff8e-215">Data.<Guid>.txt (par exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="cff8e-215">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="cff8e-216">Non</span><span class="sxs-lookup"><span data-stu-id="cff8e-216">No</span></span> |
| <span data-ttu-id="cff8e-217">fileFilter</span><span class="sxs-lookup"><span data-stu-id="cff8e-217">fileFilter</span></span> |<span data-ttu-id="cff8e-218">Spécifier qu'un filtre toobe utilisé tooselect un sous-ensemble de fichiers dans hello folderPath plutôt que tous les fichiers.</span><span class="sxs-lookup"><span data-stu-id="cff8e-218">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="cff8e-219">Les valeurs autorisées sont : `*` (plusieurs caractères) et `?` (caractère unique).</span><span class="sxs-lookup"><span data-stu-id="cff8e-219">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="cff8e-220">Exemple 1 : `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="cff8e-220">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="cff8e-221">Exemple 2 : `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="cff8e-221">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="cff8e-222">fileFilter s’applique à un jeu de données FileShare d’entrée.</span><span class="sxs-lookup"><span data-stu-id="cff8e-222">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="cff8e-223">Cette propriété n’est pas prise en charge avec HDFS.</span><span class="sxs-lookup"><span data-stu-id="cff8e-223">This property is not supported with HDFS.</span></span> |<span data-ttu-id="cff8e-224">Non</span><span class="sxs-lookup"><span data-stu-id="cff8e-224">No</span></span> |
| <span data-ttu-id="cff8e-225">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="cff8e-225">partitionedBy</span></span> |<span data-ttu-id="cff8e-226">partitionedBy peut être utilisé toospecify un folderPath dynamique, le nom de fichier de données de série chronologique.</span><span class="sxs-lookup"><span data-stu-id="cff8e-226">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="cff8e-227">Par exemple, folderPath peut être paramétré pour toutes les heures de données.</span><span class="sxs-lookup"><span data-stu-id="cff8e-227">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="cff8e-228">Non</span><span class="sxs-lookup"><span data-stu-id="cff8e-228">No</span></span> |
| <span data-ttu-id="cff8e-229">format</span><span class="sxs-lookup"><span data-stu-id="cff8e-229">format</span></span> | <span data-ttu-id="cff8e-230">Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="cff8e-230">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="cff8e-231">Ensemble hello **type** propriété sous tooone de format de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="cff8e-231">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="cff8e-232">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="cff8e-232">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="cff8e-233">Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="cff8e-233">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="cff8e-234">Non</span><span class="sxs-lookup"><span data-stu-id="cff8e-234">No</span></span> |
| <span data-ttu-id="cff8e-235">compression</span><span class="sxs-lookup"><span data-stu-id="cff8e-235">compression</span></span> | <span data-ttu-id="cff8e-236">Spécifiez le type de hello et le niveau de compression pour les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="cff8e-236">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="cff8e-237">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="cff8e-237">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="cff8e-238">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="cff8e-238">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="cff8e-239">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="cff8e-239">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="cff8e-240">Non</span><span class="sxs-lookup"><span data-stu-id="cff8e-240">No</span></span> |
| <span data-ttu-id="cff8e-241">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="cff8e-241">useBinaryTransfer</span></span> |<span data-ttu-id="cff8e-242">Spécifiez si vous voulez utiliser le mode de transfert binaire.</span><span class="sxs-lookup"><span data-stu-id="cff8e-242">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="cff8e-243">True pour le mode binaire et false pour ASCII.</span><span class="sxs-lookup"><span data-stu-id="cff8e-243">True for binary mode and false ASCII.</span></span> <span data-ttu-id="cff8e-244">Valeur par défaut : true.</span><span class="sxs-lookup"><span data-stu-id="cff8e-244">Default value: True.</span></span> <span data-ttu-id="cff8e-245">Cette propriété peut uniquement être utilisée lorsque le type de service lié associé est : FtpServer.</span><span class="sxs-lookup"><span data-stu-id="cff8e-245">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="cff8e-246">Non</span><span class="sxs-lookup"><span data-stu-id="cff8e-246">No</span></span> |

> [!NOTE]
> <span data-ttu-id="cff8e-247">fileName et fileFilter ne peuvent pas être utilisés simultanément.</span><span class="sxs-lookup"><span data-stu-id="cff8e-247">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="cff8e-248">Utilisation de la propriété partitionedBy</span><span class="sxs-lookup"><span data-stu-id="cff8e-248">Using partionedBy property</span></span>
<span data-ttu-id="cff8e-249">Comme indiqué dans la section précédente de hello, vous pouvez spécifier un folderPath dynamique, le nom de fichier de données de série chronologique avec partitionedBy.</span><span class="sxs-lookup"><span data-stu-id="cff8e-249">As mentioned in hello previous section, you can specify a dynamic folderPath, filename for time series data with partitionedBy.</span></span> <span data-ttu-id="cff8e-250">Vous pouvez le faire avec les macros Data Factory hello et variable hello système SliceStart, SliceEnd indiquant hello période logique pour une tranche de données spécifiée.</span><span class="sxs-lookup"><span data-stu-id="cff8e-250">You can do so with hello Data Factory macros and hello system variable SliceStart, SliceEnd that indicate hello logical time period for a given data slice.</span></span>

<span data-ttu-id="cff8e-251">toolearn sur la série de temps des groupes de données, de planification et de secteurs, consultez [création de Datasets](data-factory-create-datasets.md), [de planification et l’exécution de](data-factory-scheduling-and-execution.md), et [création de Pipelines](data-factory-create-pipelines.md) articles.</span><span class="sxs-lookup"><span data-stu-id="cff8e-251">toolearn about time series datasets, scheduling, and slices, See [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="cff8e-252">Exemple 1 :</span><span class="sxs-lookup"><span data-stu-id="cff8e-252">Sample 1:</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="cff8e-253">Dans cet exemple {Slice} est remplacé par la valeur hello de fabrique de données variable système SliceStart au format (AAAAMMJJHH) de la hello spécifiée.</span><span class="sxs-lookup"><span data-stu-id="cff8e-253">In this example {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="cff8e-254">Hello SliceStart fait référence à des temps de toostart de tranche de hello.</span><span class="sxs-lookup"><span data-stu-id="cff8e-254">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="cff8e-255">Hello folderPath est différent pour chaque secteur.</span><span class="sxs-lookup"><span data-stu-id="cff8e-255">hello folderPath is different for each slice.</span></span> <span data-ttu-id="cff8e-256">Par exemple : wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="cff8e-256">Example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="cff8e-257">Exemple 2 :</span><span class="sxs-lookup"><span data-stu-id="cff8e-257">Sample 2:</span></span>

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
<span data-ttu-id="cff8e-258">Dans cet exemple, l'année, le mois, le jour et l'heure de SliceStart sont extraits dans des variables distinctes qui sont utilisées par les propriétés folderPath et fileName.</span><span class="sxs-lookup"><span data-stu-id="cff8e-258">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="cff8e-259">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="cff8e-259">Copy activity properties</span></span>
<span data-ttu-id="cff8e-260">Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="cff8e-260">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="cff8e-261">Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités.</span><span class="sxs-lookup"><span data-stu-id="cff8e-261">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="cff8e-262">Alors que les propriétés de hello disponibles dans la section typeProperties hello activité hello varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="cff8e-262">Whereas, hello properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="cff8e-263">Pour l’activité de copie, les propriétés de type hello varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="cff8e-263">For Copy activity, hello type properties vary depending on hello types of sources and sinks.</span></span>

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="cff8e-264">Formats de fichier et de compression pris en charge</span><span class="sxs-lookup"><span data-stu-id="cff8e-264">Supported file and compression formats</span></span>
<span data-ttu-id="cff8e-265">Pour plus d’informations, voir [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="cff8e-265">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-sftp-server-tooazure-blob"></a><span data-ttu-id="cff8e-266">Exemple de JSON : Copier des données d’objet blob tooAzure de serveur SFTP</span><span class="sxs-lookup"><span data-stu-id="cff8e-266">JSON Example: Copy data from SFTP server tooAzure blob</span></span>
<span data-ttu-id="cff8e-267">Hello exemple suivant fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="cff8e-267">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="cff8e-268">Elles montrent comment la source de données de toocopy de SFTP tooAzure stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="cff8e-268">They show how toocopy data from SFTP source tooAzure Blob Storage.</span></span> <span data-ttu-id="cff8e-269">Toutefois, les données peuvent être copiées **directement** de n’importe quelle tooany de sources de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="cff8e-269">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cff8e-270">Cet exemple fournit des extraits de code JSON.</span><span class="sxs-lookup"><span data-stu-id="cff8e-270">This sample provides JSON snippets.</span></span> <span data-ttu-id="cff8e-271">Il n’inclut pas d’instructions détaillées pour créer la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="cff8e-271">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="cff8e-272">Les instructions se trouvent dans l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="cff8e-272">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="cff8e-273">exemple Hello a hello suivant des entités de fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="cff8e-273">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="cff8e-274">Un service lié de type [sftp](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cff8e-274">A linked service of type [sftp](#linked-service-properties).</span></span>
* <span data-ttu-id="cff8e-275">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cff8e-275">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="cff8e-276">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cff8e-276">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="cff8e-277">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cff8e-277">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="cff8e-278">Un [pipeline](data-factory-create-pipelines.md) avec activité de copie qui utilise [FileSystemSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="cff8e-278">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="cff8e-279">exemple Hello copie des données à partir d’un tooan du serveur SFTP blob Azure toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="cff8e-279">hello sample copies data from an SFTP server tooan Azure blob every hour.</span></span> <span data-ttu-id="cff8e-280">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="cff8e-280">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="cff8e-281">**Service lié SFTP**</span><span class="sxs-lookup"><span data-stu-id="cff8e-281">**SFTP linked service**</span></span>

<span data-ttu-id="cff8e-282">Cet exemple utilise l’authentification de base hello avec le nom d’utilisateur et mot de passe en texte brut.</span><span class="sxs-lookup"><span data-stu-id="cff8e-282">This example uses hello basic authentication with user name and password in plain text.</span></span> <span data-ttu-id="cff8e-283">Vous pouvez également utiliser un des hello suivant façons :</span><span class="sxs-lookup"><span data-stu-id="cff8e-283">You can also use one of hello following ways:</span></span>

* <span data-ttu-id="cff8e-284">Authentification de base avec des informations d’identification chiffrées</span><span class="sxs-lookup"><span data-stu-id="cff8e-284">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="cff8e-285">Authentification par clé publique SSH</span><span class="sxs-lookup"><span data-stu-id="cff8e-285">SSH public key authentication</span></span>

<span data-ttu-id="cff8e-286">Consultez la section [Service lié FTP](#linked-service-properties) pour connaître les différents types d’authentification que vous pouvez utiliser.</span><span class="sxs-lookup"><span data-stu-id="cff8e-286">See [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON

{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "myuser",
            "password": "mypassword",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```
<span data-ttu-id="cff8e-287">**Service lié Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="cff8e-287">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="cff8e-288">**Jeu de données d’entrée SFTP**</span><span class="sxs-lookup"><span data-stu-id="cff8e-288">**SFTP input dataset**</span></span>

<span data-ttu-id="cff8e-289">Ce jeu de données fait référence le dossier SFTP toohello `mysharedfolder` et le fichier `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="cff8e-289">This dataset refers toohello SFTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="cff8e-290">Hello pipeline copies hello toohello destination du fichier.</span><span class="sxs-lookup"><span data-stu-id="cff8e-290">hello pipeline copies hello file toohello destination.</span></span>

<span data-ttu-id="cff8e-291">Paramètre « external » : « true » informe service Data Factory de hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="cff8e-291">Setting "external": "true" informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "SFTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "SftpLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="cff8e-292">**Jeu de données de sortie d’objet Blob Azure**</span><span class="sxs-lookup"><span data-stu-id="cff8e-292">**Azure Blob output dataset**</span></span>

<span data-ttu-id="cff8e-293">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="cff8e-293">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="cff8e-294">chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="cff8e-294">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="cff8e-295">chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="cff8e-295">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="cff8e-296">**Pipeline avec activité de copie**</span><span class="sxs-lookup"><span data-stu-id="cff8e-296">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="cff8e-297">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="cff8e-297">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="cff8e-298">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**FileSystemSource** et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="cff8e-298">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource** and **sink** type is set too**BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
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
        "start": "2017-02-20T18:00:00Z",
        "end": "2017-02-20T19:00:00Z"
    }
}
```

## <a name="performance-and-tuning"></a><span data-ttu-id="cff8e-299">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="cff8e-299">Performance and Tuning</span></span>
<span data-ttu-id="cff8e-300">Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="cff8e-300">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cff8e-301">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cff8e-301">Next Steps</span></span>
<span data-ttu-id="cff8e-302">Consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="cff8e-302">See hello following articles:</span></span>

* <span data-ttu-id="cff8e-303">[Didacticiel de l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions détaillées sur la création d’un pipeline avec Activité de copie.</span><span class="sxs-lookup"><span data-stu-id="cff8e-303">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
