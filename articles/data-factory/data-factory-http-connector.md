---
title: "Déplacer des données à partir d’une source HTTP - Azure | Microsoft Docs"
description: "Découvrez comment déplacer des données à partir d’une source HTTP locale ou cloud à l’aide d’Azure Data Factory."
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
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 3cc1bd293868b0bb093f617ac12e16c26780fc89
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a><span data-ttu-id="7af2a-103">Déplacer des données à partir d’une source HTTP à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7af2a-103">Move data from an HTTP source using Azure Data Factory</span></span>
<span data-ttu-id="7af2a-104">Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour déplacer des données d’un point de terminaison HTTP local ou cloud vers un magasin de données récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7af2a-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from an on-premises/cloud HTTP endpoint to a supported sink data store.</span></span> <span data-ttu-id="7af2a-105">Cet article s’appuie sur l’article des [activités de déplacement des données](data-factory-data-movement-activities.md) qui présente une vue d’ensemble du déplacement des données avec l’activité de copie et la liste de magasins de données pris en charge comme sources/récepteurs.</span><span class="sxs-lookup"><span data-stu-id="7af2a-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="7af2a-106">À l’heure actuelle, Data Factory prend en charge le déplacement de données d’une source HTTP vers d’autres magasins de données, mais pas le déplacement de données de ces autres magasins vers une destination HTTP.</span><span class="sxs-lookup"><span data-stu-id="7af2a-106">Data factory currently supports only moving data from an HTTP source to other data stores, but not moving data from other data stores to an HTTP destination.</span></span>

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="7af2a-107">Scénarios et types d’authentification pris en charge</span><span class="sxs-lookup"><span data-stu-id="7af2a-107">Supported scenarios and authentication types</span></span>
<span data-ttu-id="7af2a-108">Vous pouvez utiliser ce connecteur HTTP pour récupérer des données d’un **point de terminaison HTTP/s cloud et local** à l’aide de la méthode HTTP **ET** ou **POST**.</span><span class="sxs-lookup"><span data-stu-id="7af2a-108">You can use this HTTP connector to retrieve data from **both cloud and on-premises HTTP/s endpoint** by using HTTP **GET** or **POST** method.</span></span> <span data-ttu-id="7af2a-109">Les types d’authentification suivants sont pris en charge : **Anonymous** (Anonyme), **Basic** (De base), **Digest**, **Windows** et **ClientCertificate** (Certificat client).</span><span class="sxs-lookup"><span data-stu-id="7af2a-109">The following authentication types are supported: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span></span> <span data-ttu-id="7af2a-110">Notez que ce connecteur diffère du [connecteur Table web](data-factory-web-table-connector.md), qui est utilisé pour extraire le contenu d’une table d’une page web HTML.</span><span class="sxs-lookup"><span data-stu-id="7af2a-110">Note the difference between this connector and the [Web table connector](data-factory-web-table-connector.md) is: the latter is used to extract table content from web HTML page.</span></span>

<span data-ttu-id="7af2a-111">Pour copier des données à partir d’un point de terminaison HTTP local, vous devez installer une passerelle de gestion des données dans l’environnement local/sur la machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="7af2a-111">When copying data from an on-premises HTTP endpoint, you need install a Data Management Gateway in the on-premises environment/Azure VM.</span></span> <span data-ttu-id="7af2a-112">Consultez l’article [Déplacement de données entre des emplacements locaux et le cloud](data-factory-move-data-between-onprem-and-cloud.md) pour en savoir plus sur la passerelle de gestion des données et obtenir des instructions détaillées sur la configuration de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="7af2a-112">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="7af2a-113">Prise en main</span><span class="sxs-lookup"><span data-stu-id="7af2a-113">Getting started</span></span>
<span data-ttu-id="7af2a-114">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’une source HTTP à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="7af2a-114">You can create a pipeline with a copy activity that moves data from an HTTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="7af2a-115">Le moyen le plus simple de créer un pipeline consiste à utiliser l’**Assistant de copie**.</span><span class="sxs-lookup"><span data-stu-id="7af2a-115">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="7af2a-116">Consultez la page [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’Assistant Data Factory Copy](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapide sur la création d’un pipeline à l’aide de l’Assistant Copier des données.</span><span class="sxs-lookup"><span data-stu-id="7af2a-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

- <span data-ttu-id="7af2a-117">Vous pouvez également utiliser les outils suivants pour créer un pipeline : le **portail Azure**, **Visual Studio**, **Azure PowerShell**, le **modèle Azure Resource Manager**, l’**API .NET** et l’**API REST**.</span><span class="sxs-lookup"><span data-stu-id="7af2a-117">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="7af2a-118">Pour obtenir des instructions détaillées sur la création d’un pipeline avec une activité de copie, consultez le [didacticiel sur l’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="7af2a-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> <span data-ttu-id="7af2a-119">Pour accéder à des exemples JSON sur la copie de données d’une source HTTP vers le service Stockage Blob Azure, consultez la section [Exemples JSON](#json-examples) de cet article.</span><span class="sxs-lookup"><span data-stu-id="7af2a-119">For JSON samples to copy data from HTTP source to Azure Blob Storage, see [JSON examples](#json-examples) section of this articles.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="7af2a-120">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="7af2a-120">Linked service properties</span></span>
<span data-ttu-id="7af2a-121">Le tableau suivant fournit une description des éléments JSON spécifiques du service lié HTTP.</span><span class="sxs-lookup"><span data-stu-id="7af2a-121">The following table provides description for JSON elements specific to HTTP linked service.</span></span>

| <span data-ttu-id="7af2a-122">Propriété</span><span class="sxs-lookup"><span data-stu-id="7af2a-122">Property</span></span> | <span data-ttu-id="7af2a-123">Description</span><span class="sxs-lookup"><span data-stu-id="7af2a-123">Description</span></span> | <span data-ttu-id="7af2a-124">Requis</span><span class="sxs-lookup"><span data-stu-id="7af2a-124">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7af2a-125">type</span><span class="sxs-lookup"><span data-stu-id="7af2a-125">type</span></span> | <span data-ttu-id="7af2a-126">La propriété type doit être définie sur : `Http`.</span><span class="sxs-lookup"><span data-stu-id="7af2a-126">The type property must be set to: `Http`.</span></span> | <span data-ttu-id="7af2a-127">Oui</span><span class="sxs-lookup"><span data-stu-id="7af2a-127">Yes</span></span> |
| <span data-ttu-id="7af2a-128">url</span><span class="sxs-lookup"><span data-stu-id="7af2a-128">url</span></span> | <span data-ttu-id="7af2a-129">URL de base du serveur web</span><span class="sxs-lookup"><span data-stu-id="7af2a-129">Base URL to the Web Server</span></span> | <span data-ttu-id="7af2a-130">Oui</span><span class="sxs-lookup"><span data-stu-id="7af2a-130">Yes</span></span> |
| <span data-ttu-id="7af2a-131">authenticationType</span><span class="sxs-lookup"><span data-stu-id="7af2a-131">authenticationType</span></span> | <span data-ttu-id="7af2a-132">Spécifie le type d’authentification.</span><span class="sxs-lookup"><span data-stu-id="7af2a-132">Specifies the authentication type.</span></span> <span data-ttu-id="7af2a-133">Les valeurs autorisées sont : **Anonymous** (Anonyme), **Basic** (De base), **Digest**, **Windows**, **ClientCertificate** (Certificat client).</span><span class="sxs-lookup"><span data-stu-id="7af2a-133">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="7af2a-134">Reportez-vous aux sections suivant ce tableau pour accéder à d’autres propriétés et à des exemples JSON sur ces types d’authentification.</span><span class="sxs-lookup"><span data-stu-id="7af2a-134">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="7af2a-135">Oui</span><span class="sxs-lookup"><span data-stu-id="7af2a-135">Yes</span></span> |
| <span data-ttu-id="7af2a-136">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="7af2a-136">enableServerCertificateValidation</span></span> | <span data-ttu-id="7af2a-137">Indiquez si la validation des certificats SSL doit être activée lorsque la source est un serveur web HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7af2a-137">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="7af2a-138">Non, la valeur par défaut est True.</span><span class="sxs-lookup"><span data-stu-id="7af2a-138">No, default is true</span></span> |
| <span data-ttu-id="7af2a-139">gatewayName</span><span class="sxs-lookup"><span data-stu-id="7af2a-139">gatewayName</span></span> | <span data-ttu-id="7af2a-140">Nom de la passerelle de gestion des données pour se connecter à une source HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="7af2a-140">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span></span> | <span data-ttu-id="7af2a-141">Oui en cas de copie de données à partir d’une source HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="7af2a-141">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="7af2a-142">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="7af2a-142">encryptedCredential</span></span> | <span data-ttu-id="7af2a-143">Informations d’identification chiffrées pour accéder au point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="7af2a-143">Encrypted credential to access the HTTP endpoint.</span></span> <span data-ttu-id="7af2a-144">Elles sont générées automatiquement lorsque vous configurez les informations d’authentification dans l’Assistant de copie ou la boîte de dialogue contextuelle ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="7af2a-144">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="7af2a-145">Non.</span><span class="sxs-lookup"><span data-stu-id="7af2a-145">No.</span></span> <span data-ttu-id="7af2a-146">S’applique uniquement pour la copie de données à partir d’un serveur HTTP local.</span><span class="sxs-lookup"><span data-stu-id="7af2a-146">Apply only when copying data from an on-premises HTTP server.</span></span> |

<span data-ttu-id="7af2a-147">Pour plus d’informations sur la définition des informations d’identification pour une source de données de connecteur HTTP local, consultez [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="7af2a-147">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for details about setting credentials for on-premises HTTP connector data source.</span></span>

### <a name="using-basic-digest-or-windows-authentication"></a><span data-ttu-id="7af2a-148">Utilisation de l’authentification Basic (De base), Digest ou Windows</span><span class="sxs-lookup"><span data-stu-id="7af2a-148">Using Basic, Digest, or Windows authentication</span></span>

<span data-ttu-id="7af2a-149">Définissez `authenticationType` sur `Basic`, `Digest` ou `Windows` et spécifiez les propriétés suivantes en plus des propriétés génériques du connecteur HTTP présentées ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="7af2a-149">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="7af2a-150">Propriété</span><span class="sxs-lookup"><span data-stu-id="7af2a-150">Property</span></span> | <span data-ttu-id="7af2a-151">Description</span><span class="sxs-lookup"><span data-stu-id="7af2a-151">Description</span></span> | <span data-ttu-id="7af2a-152">Requis</span><span class="sxs-lookup"><span data-stu-id="7af2a-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7af2a-153">username</span><span class="sxs-lookup"><span data-stu-id="7af2a-153">username</span></span> | <span data-ttu-id="7af2a-154">Nom d’utilisateur pour accéder au point de terminaison HTTP.</span><span class="sxs-lookup"><span data-stu-id="7af2a-154">Username to access the HTTP endpoint.</span></span> | <span data-ttu-id="7af2a-155">Oui</span><span class="sxs-lookup"><span data-stu-id="7af2a-155">Yes</span></span> |
| <span data-ttu-id="7af2a-156">password</span><span class="sxs-lookup"><span data-stu-id="7af2a-156">password</span></span> | <span data-ttu-id="7af2a-157">Mot de passe de l’utilisateur (nom d’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="7af2a-157">Password for the user (username).</span></span> | <span data-ttu-id="7af2a-158">Oui</span><span class="sxs-lookup"><span data-stu-id="7af2a-158">Yes</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="7af2a-159">Exemple : utilisation de l’authentification Basic (De base), Digest ou Windows</span><span class="sxs-lookup"><span data-stu-id="7af2a-159">Example: using Basic, Digest, or Windows authentication</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "basic",
            "url" : "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a><span data-ttu-id="7af2a-160">Utilisation de l’authentification ClientCertificate (Certificat client)</span><span class="sxs-lookup"><span data-stu-id="7af2a-160">Using ClientCertificate authentication</span></span>

<span data-ttu-id="7af2a-161">Pour utiliser l’authentification de base, définissez `authenticationType` sur `ClientCertificate` et spécifiez les propriétés suivantes en plus des propriétés génériques du connecteur HTTP présentées ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="7af2a-161">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="7af2a-162">Propriété</span><span class="sxs-lookup"><span data-stu-id="7af2a-162">Property</span></span> | <span data-ttu-id="7af2a-163">Description</span><span class="sxs-lookup"><span data-stu-id="7af2a-163">Description</span></span> | <span data-ttu-id="7af2a-164">Requis</span><span class="sxs-lookup"><span data-stu-id="7af2a-164">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7af2a-165">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="7af2a-165">embeddedCertData</span></span> | <span data-ttu-id="7af2a-166">Contenu codé en Base64 des données binaires du fichier Personal Information Exchange (PFX).</span><span class="sxs-lookup"><span data-stu-id="7af2a-166">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="7af2a-167">Spécifiez soit la propriété `embeddedCertData`, soit la propriété `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="7af2a-167">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="7af2a-168">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="7af2a-168">certThumbprint</span></span> | <span data-ttu-id="7af2a-169">Empreinte du certificat qui a été installé dans le magasin de certificats de votre ordinateur de passerelle.</span><span class="sxs-lookup"><span data-stu-id="7af2a-169">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="7af2a-170">S’applique uniquement pour la copie de données à partir d’une source HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="7af2a-170">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="7af2a-171">Spécifiez soit la propriété `embeddedCertData`, soit la propriété `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="7af2a-171">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="7af2a-172">password</span><span class="sxs-lookup"><span data-stu-id="7af2a-172">password</span></span> | <span data-ttu-id="7af2a-173">Mot de passe associé au certificat.</span><span class="sxs-lookup"><span data-stu-id="7af2a-173">Password associated with the certificate.</span></span> | <span data-ttu-id="7af2a-174">Non</span><span class="sxs-lookup"><span data-stu-id="7af2a-174">No</span></span> |

<span data-ttu-id="7af2a-175">Si vous utilisez `certThumbprint` pour l’authentification et le certificat est installé dans le magasin personnel de l’ordinateur local, vous devez accorder l’autorisation de lecture au service de passerelle :</span><span class="sxs-lookup"><span data-stu-id="7af2a-175">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span></span>

1. <span data-ttu-id="7af2a-176">Lancez Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="7af2a-176">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="7af2a-177">Ajouter le composant logiciel enfichable **Certificats**ciblant l’**ordinateur local**.</span><span class="sxs-lookup"><span data-stu-id="7af2a-177">Add the **Certificates** snap-in that targets the **Local Computer**.</span></span>
2. <span data-ttu-id="7af2a-178">Développez **Certificats**, **Personnel**, puis cliquez sur **Certificats**.</span><span class="sxs-lookup"><span data-stu-id="7af2a-178">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="7af2a-179">Cliquez avec le bouton droit sur le certificat du magasin personnel, puis sélectionnez **Toutes les tâches**->**Gérer les clés privées...**</span><span class="sxs-lookup"><span data-stu-id="7af2a-179">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="7af2a-180">Dans l’onglet **Sécurité**, ajoutez le compte d’utilisateur sous lequel le service hôte de la passerelle de gestion des données s’exécute avec l’accès en lecture au certificat.</span><span class="sxs-lookup"><span data-stu-id="7af2a-180">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span></span>  

#### <a name="example-using-client-certificate"></a><span data-ttu-id="7af2a-181">Exemple : utilisation d’un certificat client</span><span class="sxs-lookup"><span data-stu-id="7af2a-181">Example: using client certificate</span></span>
<span data-ttu-id="7af2a-182">Ce service lié lie votre fabrique de données à un serveur web HTTP local.</span><span class="sxs-lookup"><span data-stu-id="7af2a-182">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="7af2a-183">Il utilise un certificat client installé sur l’ordinateur doté de la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="7af2a-183">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"

        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="7af2a-184">Exemple : utilisation d’un certificat client dans un fichier</span><span class="sxs-lookup"><span data-stu-id="7af2a-184">Example: using client certificate in a file</span></span>
<span data-ttu-id="7af2a-185">Ce service lié lie votre fabrique de données à un serveur web HTTP local.</span><span class="sxs-lookup"><span data-stu-id="7af2a-185">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="7af2a-186">Il utilise un fichier de certificat client sur l’ordinateur doté de la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="7af2a-186">It uses a client certificate file on the machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="7af2a-187">Propriétés de jeu de données</span><span class="sxs-lookup"><span data-stu-id="7af2a-187">Dataset properties</span></span>
<span data-ttu-id="7af2a-188">Pour obtenir une liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article [Création de jeux de données](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="7af2a-188">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="7af2a-189">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="7af2a-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="7af2a-190">La section **typeProperties** est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement des données dans le magasin de données.</span><span class="sxs-lookup"><span data-stu-id="7af2a-190">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="7af2a-191">La section typeProperties pour le jeu de données de type **Http** présente les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="7af2a-191">The typeProperties section for dataset of type **Http** has the following properties</span></span>

| <span data-ttu-id="7af2a-192">Propriété</span><span class="sxs-lookup"><span data-stu-id="7af2a-192">Property</span></span> | <span data-ttu-id="7af2a-193">Description</span><span class="sxs-lookup"><span data-stu-id="7af2a-193">Description</span></span> | <span data-ttu-id="7af2a-194">Requis</span><span class="sxs-lookup"><span data-stu-id="7af2a-194">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7af2a-195">type</span><span class="sxs-lookup"><span data-stu-id="7af2a-195">type</span></span> | <span data-ttu-id="7af2a-196">Spécifie le type du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="7af2a-196">Specified the type of the dataset.</span></span> <span data-ttu-id="7af2a-197">Cette propriété doit être définie sur `Http`.</span><span class="sxs-lookup"><span data-stu-id="7af2a-197">must be set to `Http`.</span></span> | <span data-ttu-id="7af2a-198">Oui</span><span class="sxs-lookup"><span data-stu-id="7af2a-198">Yes</span></span> |
| <span data-ttu-id="7af2a-199">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="7af2a-199">relativeUrl</span></span> | <span data-ttu-id="7af2a-200">URL relative de la ressource qui contient les données.</span><span class="sxs-lookup"><span data-stu-id="7af2a-200">A relative URL to the resource that contains the data.</span></span> <span data-ttu-id="7af2a-201">Quand le chemin d’accès n’est pas spécifié, seule l’URL spécifiée dans la définition du service lié est utilisée.</span><span class="sxs-lookup"><span data-stu-id="7af2a-201">When path is not specified, only the URL specified in the linked service definition is used.</span></span> <br><br> <span data-ttu-id="7af2a-202">Pour construire une URL dynamique, vous pouvez utiliser [les variables système et les fonctions de Data Factory](data-factory-functions-variables.md), par exemple "relativeUrl": "$$Text.Format(’/my/report?month={0:yyyy}-{0:MM}&fmt=csv’, SliceStart)".</span><span class="sxs-lookup"><span data-stu-id="7af2a-202">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), e.g. "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span></span> | <span data-ttu-id="7af2a-203">Non</span><span class="sxs-lookup"><span data-stu-id="7af2a-203">No</span></span> |
| <span data-ttu-id="7af2a-204">requestMethod</span><span class="sxs-lookup"><span data-stu-id="7af2a-204">requestMethod</span></span> | <span data-ttu-id="7af2a-205">Méthode HTTP.</span><span class="sxs-lookup"><span data-stu-id="7af2a-205">Http method.</span></span> <span data-ttu-id="7af2a-206">Les valeurs autorisées sont **GET** ou **POST**.</span><span class="sxs-lookup"><span data-stu-id="7af2a-206">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="7af2a-207">Non.</span><span class="sxs-lookup"><span data-stu-id="7af2a-207">No.</span></span> <span data-ttu-id="7af2a-208">La valeur par défaut est `GET`.</span><span class="sxs-lookup"><span data-stu-id="7af2a-208">Default is `GET`.</span></span> |
| <span data-ttu-id="7af2a-209">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="7af2a-209">additionalHeaders</span></span> | <span data-ttu-id="7af2a-210">En-têtes de requête HTTP supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="7af2a-210">Additional HTTP request headers.</span></span> | <span data-ttu-id="7af2a-211">Non</span><span class="sxs-lookup"><span data-stu-id="7af2a-211">No</span></span> |
| <span data-ttu-id="7af2a-212">RequestBody</span><span class="sxs-lookup"><span data-stu-id="7af2a-212">requestBody</span></span> | <span data-ttu-id="7af2a-213">Corps de la requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="7af2a-213">Body for HTTP request.</span></span> | <span data-ttu-id="7af2a-214">Non</span><span class="sxs-lookup"><span data-stu-id="7af2a-214">No</span></span> |
| <span data-ttu-id="7af2a-215">format</span><span class="sxs-lookup"><span data-stu-id="7af2a-215">format</span></span> | <span data-ttu-id="7af2a-216">Si vous souhaitez simplement **récupérer les données du point de terminaison HTTP en l’état**, sans les analyser, ignorez ces paramètres de format.</span><span class="sxs-lookup"><span data-stu-id="7af2a-216">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="7af2a-217">Si vous souhaitez analyser le contenu de la réponse HTTP pendant la copie, les types de formats suivants sont pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="7af2a-217">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="7af2a-218">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="7af2a-218">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="7af2a-219">Non</span><span class="sxs-lookup"><span data-stu-id="7af2a-219">No</span></span> |
| <span data-ttu-id="7af2a-220">compression</span><span class="sxs-lookup"><span data-stu-id="7af2a-220">compression</span></span> | <span data-ttu-id="7af2a-221">Spécifiez le type et le niveau de compression pour les données.</span><span class="sxs-lookup"><span data-stu-id="7af2a-221">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="7af2a-222">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="7af2a-222">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="7af2a-223">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="7af2a-223">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="7af2a-224">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="7af2a-224">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="7af2a-225">Non</span><span class="sxs-lookup"><span data-stu-id="7af2a-225">No</span></span> |

### <a name="example-using-the-get-default-method"></a><span data-ttu-id="7af2a-226">Exemple : utilisation de la méthode GET (par défaut)</span><span class="sxs-lookup"><span data-stu-id="7af2a-226">Example: using the GET (default) method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

### <a name="example-using-the-post-method"></a><span data-ttu-id="7af2a-227">Exemple : utilisation de la méthode POST</span><span class="sxs-lookup"><span data-stu-id="7af2a-227">Example: using the POST method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
           "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="7af2a-228">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="7af2a-228">Copy activity properties</span></span>
<span data-ttu-id="7af2a-229">Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Création de pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="7af2a-229">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="7af2a-230">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="7af2a-230">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="7af2a-231">En revanche, les propriétés disponibles dans la section **typeProperties** de l'activité varient pour chaque type d'activité.</span><span class="sxs-lookup"><span data-stu-id="7af2a-231">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="7af2a-232">Pour l’activité de copie, elles dépendent des types de sources et récepteurs.</span><span class="sxs-lookup"><span data-stu-id="7af2a-232">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="7af2a-233">Actuellement, quand la source de l’activité de copie est de type **HttpSource**, les propriétés suivantes sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="7af2a-233">Currently, when the source in copy activity is of type **HttpSource**, the following properties are supported.</span></span>

| <span data-ttu-id="7af2a-234">Propriété</span><span class="sxs-lookup"><span data-stu-id="7af2a-234">Property</span></span> | <span data-ttu-id="7af2a-235">Description</span><span class="sxs-lookup"><span data-stu-id="7af2a-235">Description</span></span> | <span data-ttu-id="7af2a-236">Requis</span><span class="sxs-lookup"><span data-stu-id="7af2a-236">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="7af2a-237">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="7af2a-237">httpRequestTimeout</span></span> | <span data-ttu-id="7af2a-238">Délai d’expiration (TimeSpan) pour l’obtention d’une réponse par la requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="7af2a-238">The timeout (TimeSpan) for the HTTP request to get a response.</span></span> <span data-ttu-id="7af2a-239">Il s’agit du délai d’expiration pour l’obtention d’une réponse, et non du délai d’expiration pour la lecture des données de la réponse.</span><span class="sxs-lookup"><span data-stu-id="7af2a-239">It is the timeout to get a response, not the timeout to read response data.</span></span> | <span data-ttu-id="7af2a-240">Non.</span><span class="sxs-lookup"><span data-stu-id="7af2a-240">No.</span></span> <span data-ttu-id="7af2a-241">Valeur par défaut : 00:01:40</span><span class="sxs-lookup"><span data-stu-id="7af2a-241">Default value: 00:01:40</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="7af2a-242">Formats de fichier et de compression pris en charge</span><span class="sxs-lookup"><span data-stu-id="7af2a-242">Supported file and compression formats</span></span>
<span data-ttu-id="7af2a-243">Pour plus d’informations, voir [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="7af2a-243">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="7af2a-244">Exemples JSON</span><span class="sxs-lookup"><span data-stu-id="7af2a-244">JSON examples</span></span>
<span data-ttu-id="7af2a-245">Les exemples suivants offrent des exemples de définitions JSON que vous pouvez utiliser pour créer un pipeline à l’aide du [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), de [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou d’[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7af2a-245">The following example provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="7af2a-246">Ils montrent comment copier des données d’une source HTTP vers le service Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7af2a-246">They show how to copy data from HTTP source to Azure Blob Storage.</span></span> <span data-ttu-id="7af2a-247">Toutefois, les données peuvent être copiées **directement** vers l’un des récepteurs indiqués [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) , via l’activité de copie de Microsoft Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7af2a-247">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-http-source-to-azure-blob-storage"></a><span data-ttu-id="7af2a-248">Exemple : copier des données d’une source SFTP vers le service Stockage Blob Azure</span><span class="sxs-lookup"><span data-stu-id="7af2a-248">Example: Copy data from HTTP source to Azure Blob Storage</span></span>
<span data-ttu-id="7af2a-249">La solution Data Factory pour cet exemple contient les entités Data Factory suivantes :</span><span class="sxs-lookup"><span data-stu-id="7af2a-249">The Data Factory solution for this sample contains the following Data Factory entities:</span></span>

1. <span data-ttu-id="7af2a-250">Un service lié de type [HTTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7af2a-250">A linked service of type [HTTP](#linked-service-properties).</span></span>
2. <span data-ttu-id="7af2a-251">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7af2a-251">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="7af2a-252">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [Http](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7af2a-252">An input [dataset](data-factory-create-datasets.md) of type [Http](#dataset-properties).</span></span>
4. <span data-ttu-id="7af2a-253">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7af2a-253">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="7af2a-254">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [ttpSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="7af2a-254">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [HttpSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="7af2a-255">L’exemple copie des données d’une source HTTP vers un objet blob Azure toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="7af2a-255">The sample copies data from an HTTP source to an Azure blob every hour.</span></span> <span data-ttu-id="7af2a-256">Les propriétés JSON utilisées dans ces exemples sont décrites dans les sections suivant les exemples.</span><span class="sxs-lookup"><span data-stu-id="7af2a-256">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="http-linked-service"></a><span data-ttu-id="7af2a-257">Service lié HTTP</span><span class="sxs-lookup"><span data-stu-id="7af2a-257">HTTP linked service</span></span>
<span data-ttu-id="7af2a-258">Cet exemple utilise le service lié HTTP avec l’authentification anonyme.</span><span class="sxs-lookup"><span data-stu-id="7af2a-258">This example uses the HTTP linked service with anonymous authentication.</span></span> <span data-ttu-id="7af2a-259">Pour connaître les différents types d’authentification que vous pouvez utiliser, consultez la section [Service lié HTTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7af2a-259">See [HTTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="7af2a-260">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7af2a-260">Azure Storage linked service</span></span>

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

### <a name="http-input-dataset"></a><span data-ttu-id="7af2a-261">Jeu de données d’entrée HTTP</span><span class="sxs-lookup"><span data-stu-id="7af2a-261">HTTP input dataset</span></span>
<span data-ttu-id="7af2a-262">La définition de **external** sur **true** informe le service Data Factory qu’il s’agit d’un jeu de données qui est externe à la Data Factory et non produit par une activité dans la Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7af2a-262">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}

```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="7af2a-263">Jeu de données de sortie d’objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="7af2a-263">Azure Blob output dataset</span></span>

<span data-ttu-id="7af2a-264">Les données sont écrites dans un nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="7af2a-264">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="7af2a-265">Pipeline avec activité de copie</span><span class="sxs-lookup"><span data-stu-id="7af2a-265">Pipeline with Copy activity</span></span>

<span data-ttu-id="7af2a-266">Le pipeline contient une activité de copie qui est configurée pour utiliser les jeux de données d'entrée et de sortie, et qui est planifiée pour s'exécuter toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="7af2a-266">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="7af2a-267">Dans la définition JSON du pipeline, le type **source** est défini sur **ttpSource** et le type **sink** sur **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="7af2a-267">In the pipeline JSON definition, the **source** type is set to **HttpSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="7af2a-268">Pour obtenir la liste des propriétés prises en charge par le type HttpSource, consultez [HttpSource](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="7af2a-268">See [HttpSource](#copy-activity-properties) for the list of properties supported by the HttpSource.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "HttpSourceToAzureBlob",
        "description": "Copy from an HTTP source to an Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "HttpSourceDataInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "HttpSource"
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

> [!NOTE]
> <span data-ttu-id="7af2a-269">Pour savoir comment mapper des colonnes d’un jeu de données source sur des colonnes d’un jeu de données récepteur, consultez [Mappage de colonnes des jeux de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="7af2a-269">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="7af2a-270">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="7af2a-270">Performance and Tuning</span></span>
<span data-ttu-id="7af2a-271">Consultez l’article [Guide sur les performances et le réglage de l’activité de copie](data-factory-copy-activity-performance.md) pour en savoir plus sur les facteurs clés affectant les performances de déplacement des données (activité de copie) dans Azure Data Factory et les différentes manières de les optimiser.</span><span class="sxs-lookup"><span data-stu-id="7af2a-271">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
